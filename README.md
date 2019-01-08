[//]: # (Image References)
[image_0]: ./misc/rover_image.jpg
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
