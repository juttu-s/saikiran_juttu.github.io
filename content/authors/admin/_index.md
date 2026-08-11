
---
title: Saikiran Juttu
first_name: Saikiran
last_name: Juttu
status:
  icon: 🤖
superuser: true
highlight_name: true
role: Robotics Software Engineer
avatar:
  size: 10000  # You can increase this to 180 or 200 if you'd like
  shape: rectangle # Or use "rectangle" for a square image

organizations:
  - name: Northeastern University
    url: https://www.northeastern.edu/

profiles:
  - icon: at-symbol
    url: 'mailto:juttu.s@northeastern.edu'
    label: E-mail
  - icon: brands/github
    url: https://github.com/juttu-s
  - icon: brands/linkedin
    url: https://www.linkedin.com/in/saikiran-juttu/

interests:
  - SLAM & State Estimation
  - Multi-Robot Planning
  - Robot Perception
  - Embedded Systems

education:
  - area: MS Robotics
    institution: Northeastern University, Boston
    date_start: 2023-01-01
    date_end: 2025-12-31
    summary: |
      GPA: 3.99/4.0  
      Courses: Pattern Recognition and Computer Vision, Control Systems, Robotics Sensing and Navigation, Mobile Robotics,Autonomous Field Robotics, Robot Mechanics and Control, Reinforcement Learning
  - area: BTech Mechanical Engineering
    institution: NIT Jalandhar, India
    date_start: 2016-01-01
    date_end: 2020-05-31
    summary: |
      Courses: Mechatronics, CAD, Material Science, Industrial Automation, Machine Design, Operations Research, Electronics

work:
  - position: Robotics Research Intern
    company_name: Northeastern University — Mechanical & Industrial Engineering
    date_start: 2026-05-01
    date_end: ''
    summary: |
      - Developing perception, planning, and control algorithms for heterogeneous multi-robot exploration in C++ and Python, under Prof. Yasin Yazicioglu.
      - Validating algorithms across simulation benchmarks and hardware experiments to close the sim-to-real gap on field platforms.
  - position: Robotics Engineer
    company_name: Barn Owl AG
    date_start: 2026-03-01
    date_end: 2026-04-30
    summary: |
      - Built and containerized motion control features (in-place rotation, reverse driving) using the Stanley controller in Docker; validated end-to-end in simulation and field deployments on an autonomous agricultural platform.
      - Integrated a BMS over CAN bus and designed electrical systems for IPC auto-ignition and Wake-on-LAN on Jetson AGX, enabling automated power sequencing and reducing manual intervention in field deployments.
      - Deployed and configured field hardware; performed servo and rail calibration for precision automation.
  - position: Graduate Research Assistant
    company_name: Multi-Agent Robotics Laboratory
    date_start: 2024-04-01
    date_end: 2025-12-31
    summary: |

      - Architected a heterogeneous UAV–AGV system in ROS 2/C++, implementing a centralized Finite State Machine (FSM) coordinator to synchronize autonomous exploration, precise docking, and failure-recovery triggers.
      - Engineered a multithreaded Dynamic Exploration Planner that solves the Orienteering Problem using GRASP metaheuristics, improving path-planning efficiency by 40% while computing obstacle-aware costs via Dijkstra's algorithm.
      - Implemented battery-aware planning logic that dynamically adjusts solver constraints based on real-time flight metrics, ensuring safe UAV return while maximizing information gain.
      - Designed and tested custom FPV drone hardware, tuning flight controllers with ArduPilot/PX4 to improve performance in GPS-denied environments.
      - [Click here for more details](/saikiran_juttu.github.io/details/grad-research-assistant)

  - position: Robotics Engineer Co-op
    company_name: Northeastern University
    date_start: 2025-01-15
    date_end: 2025-06-01
  
    summary: |
      - Engineered a robust autonomy stack for the Scout Mini Rover using ROS 2, achieving time-synchronized sensor fusion of 3D LiDAR and Intel RealSense RGB-D data on an NVIDIA Jetson Orin.
      - Implemented and tuned state-of-the-art SLAM solutions (Fast-LIO, LIO-SAM, VIO) in C++, optimizing backend parameters to reduce translation drift by 35% in GPS-denied environments.
      - Configured Nav2 behavior trees and costmaps running at 20 Hz to enable dynamic obstacle avoidance and autonomous waypoint navigation with a 95% success rate in cluttered environments.
      - Developed waypoint navigation pipelines for UAVs using the OptiTrack motion capture system, achieving fully automated takeoff, trajectory execution, and precision landing with sub-centimeter accuracy.
      - Built a Dockerized deployment pipeline to standardize build environments, reducing device setup time by 80% and ensuring reproducibility across development and field units.
      - [Click here for more details](/saikiran_juttu.github.io/details/robotics-coop)
  - position: Teaching Assistant
    company_name: Northeastern University
    date_start: 2024-09-01
    date_end: 2025-04-30
    summary: |
      - Architected a remote Sim-to-Real workflow, creating a high-fidelity Simscape simulation that requires students to validate kinematic safety and control logic before unlocking remote execution on physical hardware.
      - Engineered a modular perception-and-control stack for the PincherX-100, implementing a custom analytical Inverse Kinematics (IK) solver and ArUco-based extrinsic calibration to achieve ±2.5 mm precision.
      - Established the standard laboratory framework for a MathWorks-funded, cost-optimized curriculum, deploying a structured software repository that empowered students to bridge theory with hands-on robot control.
  - position: Mechanical Engineer
    company_name: Technip Energies
    date_start: 2021-02-01
    date_end: 2023-07-31
    summary: |
      - Designed and optimized large-scale piping systems using Smart3D, Navisworks, SolidWorks, and CATIA, gaining expertise in CAD modeling, system integration, and safety-compliant mechanical design.
      - Engineered a predictive Load Monitoring System using signal processing on sensor data to estimate equipment fatigue life and reduce unplanned downtime.
      - Collaborated with clients, vendors, and cross-functional teams to manage on-site integration and digitize workflows, implementing version control to ensure timely delivery of engineering assets.
      - Gained expertise in large-scale system engineering and validation through EPC projects, building a foundation for developing robust, safety-critical robotic systems.
  - position: Computer Vision Intern
    company_name: Robic Rufarm
    date_start: 2019-06-01
    date_end: 2019-08-01
    summary: |
      - Built a real-time defect detection pipeline using Python and OpenCV, applying morphological operations and contour detection to classify manufacturing defects.
      - Optimized image processing algorithms for an edge device, increasing throughput by 75% while maintaining 90% detection accuracy.
      - Built an automated edge-length measuring device and designed a pH sensing solution for aquaculture.
  - position: Brakes and Testing Head
    company_name: Off-Road Racing Team (NIT Jalandhar)
    date_start: 2017-01-01
    date_end: 2019-05-01
    summary: |
      - Built the lightest ATV ever built in the country for BAJA SAE INDIA 2019, achieved 4th fastest ATV in BAJA SAE Illinois 2017.
      - Designed Floating Brake Caliper in Catia V5 using the parameters measured from hydraulic pressure sensors and tested it on ATV
      - Employed FEA to optimize brake rotor structure, integrating aluminum with SS420 coating to enhance cooling capacity and hardness, reducing brake fading and achieving a remarkable 40% weight reduction through compact assembly.
      - Validated braking pedal force using a load cell & developed a setup to measure acceleration using an LDR sensor and Arduino Uno.
      - [Click here for more details](/saikiran_juttu.github.io/details/brakes_testing_head)

skills:
  - name: Languages & Middleware
    items:
      - name: C++ (14/17)
        percent: 88
      - name: Python
        percent: 90
      - name: ROS 1 / ROS 2 (Nav2, Gazebo, TF2)
        percent: 85
      - name: MATLAB / Simulink
        percent: 75
  - name: Algorithms & Math
    items:
      - name: Graph SLAM (GTSAM)
        percent: 85
      - name: Kalman Filtering (EKF/UKF)
        percent: 80
      - name: Motion Planning (A*, RRT*)
        percent: 82
      - name: Projective Geometry (ICP, PnP)
        percent: 80
  - name: Libraries & Tools
    items:
      - name: OpenCV, PCL, Eigen, Ceres
        percent: 85
      - name: PyTorch, NumPy, SciPy
        percent: 82
      - name: Linux, Docker, Git
        percent: 85
  - name: Hardware
    items:
      - name: NVIDIA Jetson, Intel RealSense
        percent: 85
      - name: 3D LiDAR (Velodyne/Ouster), IMU
        percent: 80
      - name: CAN Bus, ODrive Motor Controllers
        percent: 78
---
**Saikiran Juttu is a Robotics Software Engineer who recently earned his MS in Robotics from Northeastern University. He specializes in SLAM, state estimation, and multi-robot planning, with extensive experience deploying ROS 2 navigation stacks on embedded edge devices (NVIDIA Jetson). His work spans graph-based optimization (GTSAM), perception pipelines, and autonomy in GPS-denied environments, bridging academic research and industry-grade robotics systems.**
