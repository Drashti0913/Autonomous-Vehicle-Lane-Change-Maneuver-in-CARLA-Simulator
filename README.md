# Autonomous-Vehicle-Lane-Change-Maneuver-in-CARLA-Simulator

This project focuses on the development and implementation of autonomous overtaking maneuvers using advanced Deep Reinforcement Learning (DRL) techniques. The primary goal is to enhance traffic safety by minimizing human errors during lane changes, merging, and overtaking.

## Table of Contents

- [Project Overview](#project-overview)
- [Team Members](#team-members)
- [Guided By](#guided-by)
- [Motivation](#motivation)
- [Methodology](#methodology)
  - [CARLA Simulator Overview](#carla-simulator-overview)
  - [Hierarchical DRL Framework](#hierarchical-drl-framework)
  - [Deep Deterministic Policy Gradient (DDPG)](#deep-deterministic-policy-gradient-ddpg)
  - [Twin Delayed DDPG (TD3)](#twin-delayed-ddpg-td3)
- [Outcomes](#outcomes)
- [Expected Results](#expected-results)
- [Contact](#contact)
- [References](#references)

## Project Overview

This project is aimed at developing an autonomous vehicle capable of performing lane change maneuvers using the CARLA simulator. The approach leverages deep reinforcement learning techniques to achieve reliable and safe autonomous driving behaviors.

## Team Members

- **Drashti Bhavsar**, Pandit Deendayal Energy University, Gandhinagar, Gujarat
- **Animesh Basak**, NIT Arunachal Pradesh, Arunachal Pradesh
- **Ishita Jindal**, Chitkara University Rajpura, Punjab
- **Sanskriti Chandra**, IIIT Naya Raipur, Chhattisgarh

## Guided By

- **Prof. Dr. Neetesh Kumar**, IIT Roorkee
- **Shikhar Singh Lodhi**, IIT Roorkee

## Motivation

According to transportation experts, crashes due to lane change maneuvers constitute 4-10% of all collisions. By implementing dependable automatic overtaking, we can significantly increase traffic safety and pave the way for fully autonomous driving, offering safer roadways, increased productivity, cost savings, and eco-friendly transportation solutions.

## Methodology

### CARLA Simulator Overview

CARLA is an open-source self-driving simulator designed for modularity and flexibility. It facilitates autonomous driving research and development. The simulator utilizes Unreal Engine and follows the OpenDRIVE standard for urban environments and roadways.

- **Input Data**: Utilizes depth cameras to create a depth map of the elements, encoding the distance of each pixel to the camera.

### Hierarchical DRL Framework

1. **Sub-task Division**: The autonomous overtaking maneuver is divided into three sequential sub-tasks: left lane change, straight driving, and right lane change.
2. **Algorithms**: Utilizes Deep Deterministic Policy Gradient (DDPG) and Twin Delayed DDPG (TD3) algorithms for handling continuous action spaces and ensuring learning stability.

### Deep Deterministic Policy Gradient (DDPG)

- A model-free, off-policy algorithm that integrates deep learning and reinforcement learning for handling continuous action spaces.
- Utilizes an actor-critic architecture for precise action determination.

### Twin Delayed DDPG (TD3)

- An enhancement over DDPG that addresses overestimation bias and improves training stability with a twin-critic approach and delayed policy updates.
- Suitable for the straight driving phase, ensuring stable trajectory maintenance amidst dynamic traffic conditions.

## Outcomes

- **Successful Autonomous Overtaking**: Demonstrated effective real-world application of a fully autonomous overtaking maneuver.
- **Advanced DRL Application**: Showcased the adaptability and precision of DRL algorithms in continuous action spaces.
- **Enhanced Learning Stability and Accuracy**: Achieved through the TD3 algorithm, leading to more reliable and consistent autonomous driving behavior.
- **Precision in Action Decisions**: Enabled by the actor-critic architecture of DDPG, crucial for the complex task of overtaking.
- **Real-World Applicability**: Proved the potential for safer, more efficient autonomous driving solutions.
- **Robust Maneuvering in Dynamic Scenarios**: The hierarchical model effectively navigated complex and dynamic driving environments.

## Expected Results

- **Precise Control**: Over continuous driving actions such as steering and acceleration, essential for safely executing autonomous overtaking maneuvers.
- **Low Actor and Critic Loss**: Ensuring reliable and safe execution of overtaking maneuvers.
- **Minimized Risk of Collision**: Demonstrating the practical efficacy of the hierarchical DRL model.

## Contact

- **Drashti Bhavsar**
  - Email: [drashti.bhavsar09@gmail.com](mailto:drashti.bhavsar09@gmail.com)
  - Phone: +91 6354789967

## References

- Li, Dianzhao, and Ostap Okhrin. "A platform-agnostic deep reinforcement learning framework for effective sim2real transfer in autonomous driving." arXiv preprint arXiv:2304.08235 (2023).
- Hu, Xuemin, et al. "How simulation helps autonomous driving: A survey of sim2real, digital twins, and parallel intelligence." IEEE Transactions on Intelligent Vehicles (2023).
- Cimurs, Reinis, Il Hong Suh, and Jin Han Lee. "Goal-driven autonomous exploration through deep reinforcement learning." IEEE Robotics and Automation Letters 7.2 (2021): 730-737.
- Gangopadhyay, Briti, Harshit Soora, and Pallab Dasgupta. "Hierarchical program-triggered reinforcement learning agents for automated driving." IEEE Transactions on Intelligent Transportation Systems 23.8 (2021): 10902-10911.
