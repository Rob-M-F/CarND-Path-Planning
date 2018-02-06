# Path-Planning-CarND (Self Driving Car Nanodegree Path Planning Project)
This path planner uses waypoints along splines to create smooth lane transitions and velocity adjustments. It is designed to work with the [Udacity Term 3 Self Driving Car simulator](https://github.com/udacity/self-driving-car-sim/releases). The environment includes a 7,000 meter, 6 lane undivided highway with a speed limit of 50 miles per hour. There is traffic present in all lanes driving within 10 MPH of the speed limit and initiating lane changes of their own. Finally the car is required to limit total acceleration to below 10 m/s^2 and total jerk to below 50 m/s^3.

## Prerequisites

* cmake >= 3.5  
 * All OSes: [click here for installation instructions](https://cmake.org/install/)  
* make >= 4.1  
  * Linux: make is installed by default on most Linux distros  
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)  
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)  
* gcc/g++ >= 5.4  
  * Linux: gcc / g++ is installed by default on most Linux distros  
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)  
  * Windows: recommend using [MinGW](http://www.mingw.org/)  
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)  
  * Run either `install-mac.sh` or `install-ubuntu.sh`.  
* [Spline library](http://kluge.in-chemnitz.de/opensource/spline/)  

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

Here is the data provided from the Simulator to the C++ Program

## Data Provided from the Simulated Car to the Path Planner

["x"] The car's x position in map coordinates  
["y"] The car's y position in map coordinates  
["s"] The car's s position in frenet coordinates  
["d"] The car's d position in frenet coordinates  
["yaw"] The car's yaw angle in the map  
["speed"] The car's speed in MPH  

["previous_path_x"] The previous list of unused x points previously given to the simulator  
["previous_path_y"] The previous list of unused y points previously given to the simulator  

["end_path_s"] The previous list's last point's frenet s value  
["end_path_d"] The previous list's last point's frenet d value  

["sensor_fusion"] A 2d vector of cars consisting of the following for each car:
   [unique ID] of each car  
   [x position] in map coordinates  
   [y position] in map coordinates  
   [x velocity] in m/s  
   [y velocity] in m/s  
   [s position] in frenet coordinates  
   [d position] in frenet coordinates  

## Details

My path planner predicts the future expected path of each detected vehicle within their lanes, adding an uncertainty factor to account for variations in speed. It then determines if there is an obstruction in the path ahead. If it finds an obstruction, it begins searching the neighboring lanes for a large enough gap to allow a lane change. Once a suitable gap is found, the car moves into that lane, using a spline for smoothing, and begins the search process again.  
