---
title: "Teaching Assistant — Robot Mechanics & Control"
summary: "A sim-to-real teaching lab for the PincherX-100: analytical IK, ArUco pose estimation, Dynamixel PID, and a safety gate students must clear in simulation before touching hardware."
date: 2024-09-01
tags: ["MATLAB", "Simscape", "Inverse Kinematics", "ArUco", "Dynamixel", "Sim-to-Real"]
image:
  filename: /saikiran_juttu.github.io/uploads/px100_lab_cell.png
  preview_only: true
---

## The lab

Northeastern, Sep 2024 – Apr 2025. A MathWorks-funded, cost-optimised robotics
curriculum built around the **PincherX-100** — a four-DOF arm with Dynamixel
servos, cheap enough to put a cell in front of every student group.

![Annotated PincherX-100 workstation: overhead camera, side-view camera, marked workspace, payload and control computer](/saikiran_juttu.github.io/uploads/px100_lab_cell.png)
*One lab cell. Overhead camera for marker-based pose estimation, side camera for
recording runs, and a marked workspace the arm has to localise targets within.*

The teaching problem with a shared robot cell is that students have to write
code that drives real motors, and a sign error in an IK solver drives the
gripper into the table. So the framework is built in two tiers: everything runs
in simulation first, and the same student code moves to hardware unchanged.

---

## Analytical IK

Rather than hand students a numerical solver, the arm's kinematics are solved
in closed form — the geometry is simple enough that it's tractable by hand,
which is the point of the exercise.

Strip the fixed wrist-to-end-effector transform off the target pose, then:

```matlab
theta1 = atan2(y4, x4);                                  % waist, from the base projection

D = (r^2 + z_eff^2 - L2^2 - L3^2) / (2 * L2 * L3);       % law of cosines
if abs(D) > 1
    error('Target is out of reach — no IK solution.');
end
theta3 = atan2(sqrt(1 - D^2), D);                        % elbow-up branch

alpha  = atan2(z_eff, r);
beta   = atan2(L3*sin(theta3), L2 + L3*cos(theta3));
theta2 = -(alpha + beta);

theta234 = atan2(-T_04(3,1), -T_04(3,2));                % wrist from the rotation block
theta4   = theta234 - theta2 - theta3;
```

Link lengths `L2 = 0.1059`, `L3 = 0.1`, shoulder height `0.0931` m. Two things
worth noting pedagogically: the `abs(D) > 1` check means an unreachable target
fails loudly with a message rather than returning a complex angle that silently
becomes garbage downstream, and the elbow-up branch is selected explicitly —
students have to decide which of the two solutions they want rather than
discovering the arm occasionally folds the other way.

## The safety gate

This is the piece that makes remote hardware execution viable. Every commanded
configuration goes through `set_joint_pos`, which refuses it on two grounds:

- **Joint limits** — each of the four angles checked against the URDF's range.
- **Table collision** — forward kinematics is run to `px100/ee_gripper_link` and
  the resulting world-frame *z* is compared against a floor threshold.

The second check is the important one. Joint limits alone don't protect
anything — every individual joint can be in range while the arm as a whole is
below the table. Running FK on the commanded pose before sending it to the
servos catches the combination, and it means a student's broken IK produces a
refusal instead of a repair ticket.

## Perception

Target positions come from markers rather than hardcoded coordinates, so the
arm has to actually localise the object. Calibrated overhead camera, with
intrinsics measured for the cell:

| | |
|---|---|
| Focal length | 1216.56, 1216.90 px |
| Principal point | 645.49, 363.51 px |
| Radial distortion | −0.4428, 0.2414 |
| Resolution | 1280 × 720 |

Markers are assigned by role — ID 0 is the base frame, ID 1 sits on the object
to pick, IDs 2–5 are candidate drop locations. The base marker is what makes
the whole thing work: detections arrive in camera coordinates, and composing
through the base tag puts the target in the robot's frame without anyone
measuring where the camera is. Tag sizes differ deliberately (2 cm for base and
drop, 1 cm for the pick marker) so a small marker can sit on top of a small
object without occluding it.

Combined with the IK above, the cell reaches **±2.5 mm** end-effector precision.

## Motor control

Students also get underneath the position controller. `set_dynamixel_pid` writes
straight to the Dynamixel control table — addresses 80, 82 and 84 for the D, I
and P gains — and `pid_checking.m` is a step-response harness: command the waist
joint from 0 to 1 rad, log actual position against time, change a gain, run it
again.

Reading an encoder trace that overshoots and oscillates, then watching it settle
after raising D, is a more durable lesson about PID than a Bode plot. Gripper
control is similarly concrete: open and closed are literally encoder counts
2573 and 2048.

## Sim-to-real

The two entry points are deliberately near-identical:

| | Simulation | Hardware |
|---|---|---|
| Script | `Visual.m` | `pick_place.m` |
| Target poses | set in-script | detected from markers |
| Obstacles | toggleable | the real table |
| Output | Simscape animation | recorded video of the run |

Both drive the same `ikpincher100`, the same `set_joint_pos` safety gate, and
the same URDF — `px100.urdf` with eight STL meshes, imported through
`importrobot` for simulation and shipped alongside a Simscape model
(`px100_simple.slx`) for the dynamics exercises. The simulation path adds
approach waypoints above the pick and drop poses, so students meet the idea
that a straight line between two valid poses is not necessarily a valid path.

Library loading is handled per-platform (Windows, Linux, macOS) in
`init_robot.m`, which sounds trivial and is the kind of thing that otherwise
eats the first hour of every lab session.

---

## What the framework ships

| File | Role |
|---|---|
| `init_robot.m` | Dynamixel SDK bringup, URDF import, robot struct |
| `ikpincher100.m` | Closed-form inverse kinematics |
| `set_joint_pos.m` | Joint-limit and table-collision safety gate |
| `get_joint_pos.m` | Bulk encoder read, counts → radians |
| `get_pick_and_place_position.m` | Marker detection and base-frame transform |
| `pick_place.m` / `Visual.m` | Hardware and simulation task entry points |
| `pid_checking.m`, `set_dynamixel_pid.m` | Servo gain tuning exercise |
| `closeGripper.m` | Gripper open/close |
| `px100.urdf`, `*.stl`, `px100_simple.slx` | Robot model and Simscape dynamics |
