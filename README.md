# Dual-Tag UWB/INS Navigation System

An indoor UAV navigation system for position and heading estimation using dual UWB tags, UWB ranging, IMU measurements, and a PX4 on-board EKF.

## Project Overview

Conventional UWB RTLS systems can estimate the position of a mobile tag, but a single-tag configuration cannot directly estimate the heading of a UAV.
This project proposes a dual-tag UWB/INS navigation system that estimates both position and heading by attaching two UWB tags to the front and rear of a UAV.

The RTLS hardware was built using [Makerfabs ESP32 UWB DW3000 modules](https://www.makerfabs.com/esp32-uwb-dw3000.html).
A 7-state Extended Kalman Filter (EKF) was implemented on PX4 to estimate position, velocity, and yaw in real time.
The estimated states computed by the on-board EKF were transmitted from PX4 to a PC via MAVLink and visualized in a Python-based monitoring program.

## Key Features

* Indoor UAV localization using 4 UWB anchors and 2 UWB tags
* Dual-tag configuration for heading estimation
* IMU propagation and UWB range update
* 7-state EKF implementation on PX4
* Custom uORB topic and MAVLink message integration
* Real-time visualization of position, velocity, and yaw

## System Configuration

The system consists of fixed UWB anchors, dual UWB tags, Assembler, a PX4-based flight controller, and a Python-based visualization program.

* **Anchors**: Fixed UWB nodes installed at known positions
* **Tags**: Two UWB tags attached to the front and rear of the UAV
* **Assembler** : Combines 8 UWB range measurements into a single observation packet
* **Flight Controller**: PX4-based on-board EKF implementation
* **Sensor Fusion**: IMU propagation and UWB range update
* **Visualization**: Python-based real-time monitoring program

## Experimental Setup

Experiments were conducted in an indoor RTLS environment with fixed UWB anchors.
The UAV was operated within the anchor-covered area, and the estimated trajectory and heading were evaluated using ground-truth references.

Experimental configuration:

* Indoor RTLS test area
* 4 fixed UWB anchors
* 2 UWB tags mounted on the UAV
* PX4 flight controller
* MAVLink-based communication
* Python-based real-time visualization

## Demo Video

Experiment and visualization videos will be added after uploading them to YouTube.

* Indoor experiment: Coming soon
* Real-time visualization: Coming soon

## Results

The system was evaluated through indoor experiments.

Main evaluation items:

* Position estimation performance
* Heading estimation using dual UWB tags
* EKF trajectory compared with UWB-only estimation
* Real-time PX4 on-board operation
* MAVLink-based visualization result

Result figures will be added after organizing the experiment images and plots.

## Analysis

The dual-tag configuration enabled heading estimation in addition to position tracking.
Compared with UWB-only estimation, the EKF-based approach provided smoother and more stable trajectory estimation by integrating IMU measurements with UWB ranging data.

However, the RTLS configuration was still affected by geometric dilution of precision (DOP), especially in the vertical direction.
Since the anchors were installed in a fixed indoor layout, the x-y position estimates showed relatively small errors, while the z-axis estimate had larger errors due to weaker vertical observatbility.

The experiment also confirmed that the estimated navigation states could be computed on-board in PX4 and transmitted to an external monitoring program through MAVLink in real time.

## Project Status

This repository currently summarizes the overall project concept, system configuration, experiment setup, and results.

Detailed implementation repositories and source code will be organized separately, including:

* ESP32 UWB RTLS firmware
* PX4 on-board EKF module
* MAVLink-based Python visualization program
* MATLAB-based post-processing and analysis scripts
