# pdc-ros

Setup

```
git clone https://github.com/RobotLocomotion/pdc-ros.git
cd pdc-ros
git submodule update --init --recursive
cd docker
./docker_build.py
```

Run a simple node to stream descriptor images

(To configure, edit `config/trained_networks.yaml`, and then `NETWORK_NAME` and `RGB_TOPIC` at the top of `pdc_ros/src/pdc_ros/pdc_ros_simple_streaming.py`)

```
./docker_run.py
use_all
cd ..
cd catkin_ws
catkin_make
use_all
python src/pdc_ros/nodes/simple_descriptor_streaming.py 
```

Run a node to respond to ROS actions to find best descriptor matches

```
./docker_run.py
use_all
cd ..
cd catkin_ws
catkin_make
use_all
python src/pdc_ros/nodes/find_best_match_node.py 
```

## Running Caterpillar Tail Pick Demo

You can edit the file `pdc_ros_wrapper.py` in `pdc-ros` and choose which demo to run (ear, tail, shoe).

1. Launch `spartan` and startup robot as usual.

2. In pdc-ros container launch node to respond to ROS actions to find best descriptor matches.

```
cd ..
cd catkin_ws
catkin_make
use_all
python src/pdc_ros/nodes/find_best_match_node.py 
```

3. Launch `spartan_grasp` container from `manuelli` user. Inside the spartan_grasp container do

```
use_ros
use_spartan_grasp
use_spartan_grasp_ros
roslaunch spartan_grasp_wrapper spartan_grasp_wrapper.launch
```

4. In `director` use `graspSupervisor.test_find_best_match_and_grasp_and_stow()` to execute the pick. 


## Running Poser

1. Launch `spartan` and startup robot as usual.

2. In pdc-ros container launch node to respond to ROS actions to find best descriptor matches.

```
cd ..
cd catkin_ws
catkin_make
use_all
python src/pdc_ros/nodes/poser_server_node.py 
```

3. Launch `spartan_grasp` container from `manuelli` user. Inside the spartan_grasp container do

```
use_ros
use_spartan_grasp
use_spartan_grasp_ros
roslaunch spartan_grasp_wrapper spartan_grasp_wrapper.launch
```

4. In `director` use `graspSupervisor.test_run_poser()`. This will collect and RGBD image at the current location, then call poser.

5. To visualize the results use `graspSupervisor.visualize_poser_result()`

6. Re-orient the object to the desired configuration by running `grasp_supervisor.test_run_manipulate_object()`.







