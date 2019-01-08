[//]: # (Image References)
[image_0]: ./misc/rover_image.jpg
[image_1]: ./misc/sample.png
[image_2]: ./misc/color-channels.png
[image_3]: ./misc/color-threshold.png
[image_4]: ./misc/perspective-transform.png
[image_5]: ./misc/rover-centric.png
[image_6]: ./misc/world-map.png
[image_7]: ./misc/map-to-world.png
[image_8]: ./misc/angle-decision.png
[gif_0]: ./misc/spinning-rover.gif
[![Udacity - Robotics NanoDegree Program](https://s3-us-west-1.amazonaws.com/udacity-robotics/Extra+Images/RoboND_flag.png)](https://www.udacity.com/robotics)
# Search and Sample Return Project


![alt text][image_0]

This project is modeled after the [NASA Sample Return Robot Challenge](https://www.nasa.gov/directorates/spacetech/centennial_challenges/sample_return_robot/index.html) and we can get experience with the three essential elements of robotics, which are perception, decision making and actuation.  We will carry out this project in a simulator environment built with the Unity game engine. All the setup codes and simulator are referenced from original [Udacity Github Repo](https://github.com/udacity/RoboND-Rover-Project).

## Unity Environment

We'll use the Unity game engine to build the simulated environment you'll be navigating through in this project. You don't need to know anything more about Unity to use the simulator, but if you want to learn more or get started building your own environments check out [their website](https://unity3d.com/unity)!

The first step of the project is to download the simulator and familiarize yourself with how it works. Use the links below to get the simulator version that's appropriate for your operating system.

[MacOS Simulator Build](https://s3-us-west-1.amazonaws.com/udacity-robotics/Rover+Unity+Sims/Mac_Roversim.zip)  
[Linux Simulator Build](https://s3-us-west-1.amazonaws.com/udacity-robotics/Rover+Unity+Sims/Linux_Roversim.zip)  
[Windows Simulator Build](https://s3-us-west-1.amazonaws.com/udacity-robotics/Rover+Unity+Sims/Windows_Roversim.zip)  

When you launch (double click on) the simulator you will have the option to set the resolution and graphics quality. You could choose lower resolution / quality for faster rendering. Be sure to check the box next to **Windowed** so the simulator doesn't take up the full screen. Click on the **input** tab to change the keyboard input definitions; this may be necessary if you are on a non-U.S. keyboard. The next time you launch, these settings will be restored. Click **Play** to launch the simulator!

## Manual Controls

Experiment in Training Mode with the various manual functions.

- Throttle, brake and steering: **wasd** letters or **arrow keys** (can also steer with mouse)
- Toggle mouse function between camera perspective and steering: **esc** key
- Change the viewing perspective: **tab** key or mouse
- Change zoom on the viewing camera: mouse **scroll**
- Reset viewing camera zoom: **middle mouse button**
- Activate the robot arm to pick up a sample: **left mouse button** or **enter** key (only works when **is near objective = yes**)

Have a look around and explore the environment!

## Dependencies

You'll need Python 3 and Jupyter Notebooks installed to do this project. The best way to get setup with these if you are not already is to install [Anaconda](https://www.anaconda.com).

## Installation

Download this repo, change directory to *code* and then you can run the following command to test this project.
```
python drive_rover.py
```

## Project Walkthrough

Lets dive into some details implementations of the project. First step is image analysis of the navigable terrain.

### Reading in Color Images

In order to navigate autonomously through the environment, we will use 320x160 pixel camera images to determine where it is possible to drive. Now, we are going to use the following sample image for our analysis.

![alt text][image_1]  

We can explore what it's size and datatype are as well as minimum and maximum values in the array by using *numpy*.

```
# Import the "numpy" package for working with arrays
import numpy as np
print(image.dtype, image.shape, np.min(image), np.max(image))
# uint8 (160, 320, 3) 0 255
```
So, here we can see it's an 8-bit unsigned integer array (uint8), where the size of the array is (160, 320, 3) meaning the image size is 160 pixels in the y-direction (height), 320 pixels in the x-direction (width) and it has 3 layers or "color channels".

The three color channels of the image are red, green and blue or "RGB" for short. We can also look at each color channel side by side.

![alt text][image_2]

### Color Thresholding

Now we can see that, while the mountains are relatively dark (low intensity values) in all three color channels, both the ground and the sky are brighter (higher intensity) in the red, green and blue channels. However, in all cases it looks like the ground is a bit brighter than the sky, so we can identify pixels associated with the ground using a simple color threshold.

![alt text][image_3]

### Perspective Transform

In the training mode, we can press **G** to display the grids in the terrain. We now then use one sample grid image to apply perspective transform and warp our image to a top-down view. For this, we are going to use [OpenCV Geometric Transforms](https://docs.opencv.org/trunk/da/d6e/tutorial_py_geometric_transformations.html).

![alt text][image_4]

### Warp, Threshold, and Map to Rover-Centric Coordinates

To make a map of the environment, we're going to first apply a perspective transform and then apply a color threshold (or vice versa, doesn't really matter). This color thresholded image is now a map of the navigable terrain in front of the rover. Then, we'll extract the pixel positions of all navigable terrain (white) pixels and then transform those values to "rover-centric" coordinates, meaning a coordinate frame where the rover camera is at (x, y) = (0, 0).

![alt text][image_5]

### Map to World Coordinates

![alt text][image_6]

The environment we will be navigating with the rover in this project is roughly 200 x 200 meters and looks like the image above from a top-down view. The white areas represent the navigable terrain. Then, we will use the rover's position, orientation and camera image to map its environment and compare against this ground truth map.

![alt text][image_7]

## Decision: Where to Go?

![alt text][gif_0]

The goal of this project is to perform autonomous navigation and mapping. We now finish the mapping so hard work is done. With each new image we receive from the rover's camera, we will have the opportunity to make a decision about sending commands like throttle, brake and steering.

We will use one sample image and we'd like to decide which direction to steer the rover. One simple way to decide is to choose the direction with the clearest path or in other words, the most navigable terrain pixels.

![alt text][image_8]

You can find the implementations of the above image analysis and decision making strategies in the code folder.

## Improvements and Future Work

This is still the working project but there are more improvements and left a lot of issues unsolved so I'll try my best to update the rover in the near future.
