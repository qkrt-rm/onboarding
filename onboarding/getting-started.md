---
layout: onboarding
title: Getting Started
---

# Getting Started

Here, you will learn about what we're doing and how you can get started on your journey developing drive control systems for the Queen's Knights Robotics Team.

## Our Goal

Become RoboMaster.

## The Basics

### The C++ Programming Language

C++ is our programming language of choice when it comes to developing drive control systems for our robots. It gives you granular control over the device its code runs on and is a mature language that has been running the world for decades. Unfortunately, C++ is not the most intuitive language to learn for new programmers, but there are an incredible amount of resources online that can help you learn it. Below are various sources we recommend, including our very own which you will eventually go through in its entirety.

-   [QKRT C++ Getting Started Guide](https://www.notion.so/C-1211ea6d75cd8135bcc6e53c699f216a?pvs=21)
-   [W3 Schools C++ Tutorials]()

### Our Target Board

All of our control code will be written to run on the [RoboMaster Development Board Type C](https://www.robomaster.com/en-US/products/components/general/development-board-type-c/info), a small computer that sits on each of our robots. We will refer to this computer as our **target board**.

STM32

### Taproot API Introduction

The Taproot API is the software interface that lets us control and communicate with the RoboMaster robot.
It’s like a bridge between our code and the robot’s hardware — we write code using Taproot functions, and those commands get sent to the robot to make it move, turn, shoot, and read sensors.

We shall be making a modified version of the Tank Drive tutorial made by the University of Washington.

- [University of Washington Guide Wiki](https://aruw.gitlab.io/controls/aruw-edu/tutorials/1_tank_drive.html)
- [University of Washington Tutorial Code Github](https://gitlab.com/aruw/controls/aruw-edu)
- [University of Washington Tutorial Code Solutions](https://gitlab.com/aruw/controls/aruw-edu/-/tree/solutions?ref_type=heads)