---
title: "Graduate Research Assistant"
summary: "Energy-aware UAV–UGV collaborative exploration: coupled orienteering over a layered PRM, with the ground robot as a mobile charging station."
date: 2024-04-01
tags: ["ROS", "Gazebo", "PRM", "Multi-Robot", "Orienteering Problem", "C++"]
url_code: 'https://github.com/juttu-s/uav-ugv-collaborative-exploration'
url_pdf: 'https://arxiv.org/abs/2603.22507'
image:
  filename: /saikiran_juttu.github.io/uploads/uav_ugv_banner.png
  preview_only: true
---

## Energy-Aware Collaborative Exploration for a UAV–UGV Team

Multi-Agent Robotics and Autonomy Lab, Northeastern University.

> Er, Juttu, Yazıcıoğlu — submitted to **IROS 2026**.
> [arXiv:2603.22507](https://arxiv.org/abs/2603.22507) ·
> [code](https://github.com/juttu-s/uav-ugv-collaborative-exploration)

<video controls width="100%" muted autoplay loop>
  <source src="/saikiran_juttu.github.io/uploads/uav_ugv_exploration.mp4" type="video/mp4">
</video>

*Hardware run at 10× speed, terminating once the team passes 95% coverage. The
[full-resolution video](https://github.com/juttu-s/uav-ugv-collaborative-exploration/releases/latest)
is attached to the release.*

---

## The problem

A quadrotor has maybe fifteen minutes of flight time. That is the binding
constraint on aerial exploration, and the usual fix — fly back to a fixed
charging station — wastes an increasing fraction of each tour on transit as the
frontier moves away.

So the ground robot becomes the charging station. The UAV flies a sequence of
**energy-bounded tours**, each ending in a rendezvous where it lands on a
platform mounted on the UGV and recharges. The UGV explores the ground in the
meantime, so the recharge leg is not dead time for the team.

The pairing is genuinely complementary in both directions: the UGV drives
through passages the UAV cannot fly, and the UAV reaches elevated structure the
UGV cannot climb. In the test arenas neither robot alone achieves full coverage.

## Planning

Exploration targets are sampled into a **density-aware layered PRM** spanning
air and ground, and each pair of tours comes from solving **coupled orienteering
problems** — maximise information gain subject to a shared rendezvous time
budget.

The coupling lives in one line. Candidate aerial targets are scored

```
score = info_gain · exp(−λ · t_ugv_path)
```

so the UAV's goal is its information gain **discounted by how far the UGV has to
drive to get underneath it**. A target rich in unexplored volume but far from
any drivable ground is worth less than a mediocre one the UGV can already reach,
because the rendezvous has to be feasible or the tour strands the drone. Four
hard gates sit on top: a candidate is rejected if its gain is ≤ 10, if it has no
ground twin, if the vertical corridor between the aerial node and its twin is
not collision-free, or if that twin is unreachable in the ground graph.

The orienteering problems are solved with **GRASP with path relinking** —
randomised greedy insertion by score-to-time ratio, 2-opt and swap-insert local
search, then path relinking between elite solutions. Every move is validated
against the roadmap, with infinite time-matrix entries for non-edges, so no tour
can shortcut off a collision-checked edge.

## Coordination

A 20 Hz state machine runs the mission: initial takeoff, a 360° scan to seed the
map, then plan → execute → rendezvous → recharge until the planner latches
completion at 97% coverage. Both tours execute **simultaneously** — the UAV gets
its whole path at once, the UGV gets waypoints dispatched one at a time through
`move_base`.

Three details that only show up once it runs on hardware:

**Landing alignment.** Each UGV waypoint is given a yaw pointing at the next one,
for smooth navigation — except the last, which instead inherits the *UAV's* final
orientation. That is what squares the landing platform up with the descending
drone.

**Touchdown debouncing.** Touchdown is confirmed only after the UAV holds below
0.75 m for two consecutive seconds. A single noisy altitude sample would
otherwise end a tour early, mid-descent.

**Replanning has to be joint.** If the UAV replans around an obstacle during
execution, the coordinator cancels the UGV's active goal and recomputes *both*
tours. The tours are coupled through a shared rendezvous — replanning one in
isolation silently breaks the guarantee that the drone can reach the ground
robot before its budget runs out.

## Shared mapping

Mapping is bidirectional, planning is not: the UGV contributes Velodyne scans
and odometry, and the planner runs in the UAV's process, projecting the aerial
roadmap down to the ground and publishing both tours. There is no second planner
on the rover.

One necessary piece of bookkeeping: the UGV's own footprint is erased from the
occupancy map before its scans are injected. Without that the rover carves a
moving phantom obstacle through the roadmap it is itself driving on.

## Stack

C++ / ROS Noetic / Gazebo 11, OctoMap for occupancy mapping, `gmapping` for the
2D ground map, `move_base` with TEB for UGV navigation, B-spline trajectory
generation and time-optimal reparameterisation on the UAV side. The UAV
autonomy stack extends
[CERLAB-UAV-Autonomy](https://github.com/Zhefan-Xu/CERLAB-UAV-Autonomy) (CMU);
the UGV packages derive from the AgileX `scout_ros` family.

Benchmarks compare the method against a single-UAV ablation and a sequential
baseline, selected as drop-in planner variants at configure time.
