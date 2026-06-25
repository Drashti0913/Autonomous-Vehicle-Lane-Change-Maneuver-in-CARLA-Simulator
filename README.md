# AutoDrive-HRL — Hierarchical Deep RL for Autonomous Lane Change & Overtaking in CARLA

> Research project at **IIT Roorkee** (Google ExploreCSR Program) · Published findings · 94% success rate in simulated urban scenarios

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-DDPG%20%7C%20TD3-EE4C2C?style=flat-square&logo=pytorch)
![CARLA](https://img.shields.io/badge/Simulator-CARLA%200.9.x-brightgreen?style=flat-square)
![Status](https://img.shields.io/badge/Status-Research%20Complete-lightgrey?style=flat-square)

---

## Overview

Autonomous lane changes and overtaking maneuvers account for **4–10% of all traffic collisions**. This project implements a **Hierarchical Deep Reinforcement Learning (HDRL)** framework to solve this problem end-to-end inside the CARLA simulator — decomposing the complex overtaking task into three sequential sub-tasks, each governed by a specialized DRL agent.

Conducted under **Prof. Dr. Neetesh Kumar** and **Shikhar Singh Lodhi** at IIT Roorkee as part of the Google ExploreCSR program.

---

## Key Results

| Metric | Value |
|---|---|
| Urban scenario success rate | **94%** |
| Real-time inference latency | **< 50ms** |
| Decision-making accuracy improvement | **+25%** over baseline |
| Training episodes to convergence | ~1500 |

---

## Approach

### Hierarchical Task Decomposition

Rather than training a single monolithic policy, the overtaking maneuver is split into three sequential sub-tasks — each handled by a dedicated agent:

```
┌─────────────────────────────────────────────────────────┐
│                  Overtaking Maneuver                     │
├─────────────────┬───────────────────┬───────────────────┤
│  1. Left Lane   │  2. Straight      │  3. Right Lane    │
│     Change      │     Driving       │     Change        │
│    (DDPG)       │    (TD3)          │    (DDPG)         │
└─────────────────┴───────────────────┴───────────────────┘
```

This decomposition dramatically reduces the policy search space and enables each agent to specialize — DDPG for precise maneuvering, TD3 for stable trajectory maintenance.

### Why DDPG for Lane Changes?
DDPG's actor-critic architecture handles **continuous action spaces** (steering angle, throttle, brake) with high precision. The lane-change sub-task requires fine-grained control where discrete action spaces fail.

### Why TD3 for Straight Driving?
TD3 addresses DDPG's overestimation bias using a **twin-critic architecture** and delayed policy updates — critical for maintaining stable trajectories in dynamic traffic with unpredictable agents.

---

## Sensor & Input Pipeline

```
Depth Camera → Depth Map (per-pixel distance encoding)
                    ↓
           Obstacle Detection Module
                    ↓
           State Vector Construction
           [ego velocity, lane position,
            lead vehicle distance, heading error]
                    ↓
            HDRL Policy Network
                    ↓
           Continuous Action Output
           [steering ∈ [-1,1], throttle ∈ [0,1]]
```

---

## Training Curves

Actor and critic loss curves at 500, 1000, and 1500 episodes are included in the repo (`Actor Loss_500.png`, `Critic Loss_1000.png`, etc.), showing convergence behavior across training stages.

---

## Getting Started

### Prerequisites

- CARLA Simulator 0.9.x ([download](https://carla.org/))
- Python 3.8+
- PyTorch, NumPy, OpenCV

```bash
pip install -r requirements.txt
```

### Run the DDPG Agent

```bash
# Start CARLA server first
./CarlaUE4.exe -windowed -ResX=800 -ResY=600

# Train the lane-change agent
python carla_DDPG.py --episodes 1500 --task lane_change
```

### Run Automatic Control (Baseline)

```bash
python automatic_control.py
```

### Replay a Recorded Session

```bash
python start_replaying.py --file <recording_file>
```

---

## Project Structure

```
├── carla_DDPG.py          # Main DDPG training loop
├── nn_actor_critic.py     # Actor-Critic network definitions
├── model.py               # TD3 model implementation
├── environment.py         # CARLA environment wrapper
├── utility.py             # Reward shaping, state extraction
├── TD3/                   # TD3 agent implementation
├── Lane_Change_Model_*.pth # Pretrained DDPG checkpoints
├── automatic_control.py   # Baseline autopilot
└── requirements.txt
```

---

## Pretrained Models

Pretrained DDPG checkpoints are included for immediate evaluation:

| File | Description |
|---|---|
| `Lane_Change_Model_DDPGactor.pth` | Actor network weights |
| `Lane_Change_Model_DDPGcritic.pth` | Critic network weights |
| `Lane_Change_Model_target_actor.pth` | Target actor (stable training copy) |
| `Lane_Change_Model_target_critic.pth` | Target critic |

---

## Research Context

This work was conducted as part of **IIT Roorkee's Google ExploreCSR program** — a competitive research initiative focused on advancing core computer science research. The hierarchical DRL approach directly addresses the **sim-to-real transfer** challenge in autonomous driving, with architecture decisions informed by:

- Li & Okhrin (2023) — platform-agnostic deep RL for sim2real transfer
- Gangopadhyay et al. (2021) — hierarchical program-triggered RL for automated driving
- Cimurs et al. (2021) — goal-driven autonomous exploration via deep RL

---

## Team

| Name | Institution |
|---|---|
| **Drashti Bhavsar** | Pandit Deendayal Energy University |
| Animesh Basak | NIT Arunachal Pradesh |
| Ishita Jindal | Chitkara University |
| Sanskriti Chandra | IIIT Naya Raipur |

**Guided by:** Prof. Dr. Neetesh Kumar & Shikhar Singh Lodhi, IIT Roorkee

---

## License

MIT — see [LICENSE](LICENSE)
### Why DDPG for Lane Changes?
DDPG's actor-critic architecture handles **continuous action spaces** (steering angle, throttle, brake) with high precision. The lane-change sub-task requires fine-grained control where discrete action spaces fail.

### Why TD3 for Straight Driving?
TD3 addresses DDPG's overestimation bias using a **twin-critic architecture** and delayed policy updates — critical for maintaining stable trajectories in dynamic traffic with unpredictable agents.

---

## Sensor & Input Pipeline

```
Depth Camera → Depth Map (per-pixel distance encoding)
                    ↓
           Obstacle Detection Module
                    ↓
           State Vector Construction
           [ego velocity, lane position,
            lead vehicle distance, heading error]
                    ↓
            HDRL Policy Network
                    ↓
           Continuous Action Output
           [steering ∈ [-1,1], throttle ∈ [0,1]]
```

---

## Training Curves

Actor and critic loss curves at 500, 1000, and 1500 episodes are included in the repo (`Actor Loss_500.png`, `Critic Loss_1000.png`, etc.), showing convergence behavior across training stages.

---

## Getting Started

### Prerequisites

- CARLA Simulator 0.9.x ([download](https://carla.org/))
- Python 3.8+
- PyTorch, NumPy, OpenCV

```bash
pip install -r requirements.txt
```

### Run the DDPG Agent

```bash
# Start CARLA server first
./CarlaUE4.exe -windowed -ResX=800 -ResY=600

# Train the lane-change agent
python carla_DDPG.py --episodes 1500 --task lane_change
```

### Run Automatic Control (Baseline)

```bash
python automatic_control.py
```

### Replay a Recorded Session

```bash
python start_replaying.py --file <recording_file>
```

---

## Project Structure

```
├── carla_DDPG.py          # Main DDPG training loop
├── nn_actor_critic.py     # Actor-Critic network definitions
├── model.py               # TD3 model implementation
├── environment.py         # CARLA environment wrapper
├── utility.py             # Reward shaping, state extraction
├── TD3/                   # TD3 agent implementation
├── Lane_Change_Model_*.pth # Pretrained DDPG checkpoints
├── automatic_control.py   # Baseline autopilot
└── requirements.txt
```

---

## Pretrained Models

Pretrained DDPG checkpoints are included for immediate evaluation:

| File | Description |
|---|---|
| `Lane_Change_Model_DDPGactor.pth` | Actor network weights |
| `Lane_Change_Model_DDPGcritic.pth` | Critic network weights |
| `Lane_Change_Model_target_actor.pth` | Target actor (stable training copy) |
| `Lane_Change_Model_target_critic.pth` | Target critic |

---

## Research Context

This work was conducted as part of **IIT Roorkee's Google ExploreCSR program** — a competitive research initiative focused on advancing core computer science research. The hierarchical DRL approach directly addresses the **sim-to-real transfer** challenge in autonomous driving, with architecture decisions informed by:

- Li & Okhrin (2023) — platform-agnostic deep RL for sim2real transfer
- Gangopadhyay et al. (2021) — hierarchical program-triggered RL for automated driving
- Cimurs et al. (2021) — goal-driven autonomous exploration via deep RL

---

## Team

| Name | Institution |
|---|---|
| **Drashti Bhavsar** | Pandit Deendayal Energy University |
| Animesh Basak | NIT Arunachal Pradesh |
| Ishita Jindal | Chitkara University |
| Sanskriti Chandra | IIIT Naya Raipur |

**Guided by:** Prof. Dr. Neetesh Kumar & Shikhar Singh Lodhi, IIT Roorkee

---

## License

MIT — see [LICENSE](LICENSE)
