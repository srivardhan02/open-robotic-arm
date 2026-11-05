# Robotic Arm Description (ROS 2)
![Uploading image.png…]()


A ROS 2 description package for a CAD-derived robotic arm. It includes the URDF model, STL visual/collision meshes, and an RViz configuration for visualization.

## Package contents

```text
robotic_arm_description/
├── launch/
│   └── display.launch.py
├── meshes/                 # STL files referenced by the URDF
├── rviz/
│   └── display.rviz
├── urdf/
│   └── robotic_arm.urdf
├── CMakeLists.txt
├── package.xml
├── LICENSE
└── README.md
```

## Requirements

- Ubuntu with ROS 2 installed (instructions below use ROS 2 Jazzy)
- `robot_state_publisher`
- `joint_state_publisher_gui`
- `rviz2`

Install the ROS 2 dependencies:

```bash
sudo apt update
sudo apt install ros-jazzy-robot-state-publisher \
  ros-jazzy-joint-state-publisher-gui \
  ros-jazzy-rviz2
```

## Build and run

Create a workspace if you do not already have one, then place this package in its `src` directory:

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
# Clone this repository here, or copy the robotic_arm_description folder here.
```

Build and source the workspace:

```bash
cd ~/ros2_ws
source /opt/ros/jazzy/setup.bash
colcon build --packages-select robotic_arm_description
source install/setup.bash
```

Launch the model in RViz:

```bash
ros2 launch robotic_arm_description display.launch.py
```

The launch file starts `robot_state_publisher`, `joint_state_publisher_gui`, and RViz. Use the joint-state GUI sliders to change the displayed joint positions. This is a visualization setup; it does not by itself provide physics simulation or hardware/servo control.

## Model notes

- The model has five arm joints and one independently commanded gripper joint.
- Additional gripper linkage joints are configured as mimic joints.
- The URDF references meshes using `package://robotic_arm_description/meshes/...` paths. Keep the `meshes` directory in the package when cloning or copying it.
- Joint limits, inertial values, and the estimated tool-tip location should be checked against the physical build before using the model for motion planning, dynamics, or hardware control.

## License

See [LICENSE](LICENSE). Before publishing, replace the copyright-holder placeholder with the correct owner(s), and confirm that you have permission to distribute the URDF and all included mesh/CAD-derived files.

## Maintainer

The maintainer name and contact in `package.xml` should be reviewed and updated by the project owner before publication.
