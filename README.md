# Deep Reinforcement Learning – Adroit Door Manipulation (PPO vs SAC)

# Project Description

This project implements Deep Reinforcement Learning agents to solve a robotic manipulation task in the AdroitHandDoor-v1 environment using Proximal Policy Optimization (PPO) and Soft Actor-Critic (SAC) algorithms with the Stable-Baselines3 library.

The goal of the agent is to learn how to control a robotic hand with multiple degrees of freedom to interact with a door handle and execute movements to open the door. 
Deep Reinforcement Learning – Adroit Door Manipulation (PPO vs SAC)

## What is Adroit Hand Door?

The Adroit Hand Door environment belongs to the Gymnasium Robotics package and simulates a Shadow Hand robotic system with approximately 30 degrees of freedom.

The agent must learn to:

- Position the hand correctly in front of the door
- Move toward the handle
- Perform grasping movements
- Apply coordinated actions to open the door

From a reinforcement learning perspective, this environment presents significant challenges:

High-dimensional continuous action space
Large number of degrees of freedom
Complex physics dynamics simulated in MuJoCo
Fine coordination required between joints

These characteristics make it a suitable environment for evaluating advanced continuous control algorithms.

## Objetivo del Proyecto

Train agents capable of learning a policy that outperforms random behavior in the AdroitHandDoor-v1 environment using different deep reinforcement learning algorithms.

This project specifically compares the performance of:

Proximal Policy Optimization (PPO)
Soft Actor-Critic (SAC)

Analyzing:
- Learning stability
- Training efficiency
- Exploration capability
- Final agent performance

## Implemented Algorithms

### Proximal Policy Optimization (PPO)

PPO is an on-policy policy-gradient algorithm that optimizes the agent’s policy using a clipped objective function, preventing excessively large updates that could destabilize learning.

Key features:
- Stable policy updates
- Generalized Advantage Estimation (GAE)
- Minibatch optimization
- Joint actor-critic training

Although PPO is robust and widely used, in high-dimensional continuous control environments it may require more interactions with the environment. Algoritmos Implementados

### Soft Actor-Critic (SAC)

SAC is an off-policy algorithm designed for continuous action spaces. It uses the maximum entropy principle, encouraging exploration during training.

Key features:
- Replay buffer for experience reuse
- Actor-critic optimization
- Entropy regularization
- Efficient exploration via State Dependent Exploration (SDE)

This approach enables more efficient learning in complex environments such as robotic manipulation.

## Configuración del Entrenamiento

### PPO

- Total timesteps: 120,000 – 286,000  
- Learning rate: 3e-4  
- Batch size: 256  
- Epochs: 10  
- Gamma: 0.99  
- GAE lambda: 0.95  
- Clip range: 0.2  
- Entropy coefficient: 0.01  

### SAC

Optimized configuration used:

- Total timesteps: 300,000  
- Learning rate: 3e-4  
- Replay buffer: 300,000  
- Batch size: 256  
- Learning starts: 10,000  
- Gamma: 0.99  
- Tau: 0.005  
- Entropy coefficient: auto  
- State Dependent Exploration: True  
- Red neuronal: [256,256]  
- Activación: ReLU  
- Dispositivo: GPU (CUDA)  

## Results

The experiments show clear differences between algorithms.

### PPO
- Approximate average reward: -31
- Limited learning
- Slight improvement over random policy 

### SAC (optimized)
- Average reward: 1111.60
- High variability between episodes
- Episodes with rewards above 3000

This indicates that SAC better explores the action space and learns more effective behaviors to manipulate the door.

## TensorBoard Analysis

TensorBoard graphs clearly show differences in learning behavior between both algorithms.

PPO curves remain close to negative values during training.
SAC curves show a significant increase in average reward after approximately 200k steps, reaching values above 200 on average.

This demonstrates that SAC develops a more effective policy for this continuous control environment.

## Contenido del Repositorio
```
AdroitDoor/
│
├── sac_adroit_door_model_v2.zip
├── video_entrenamiento.mp4
├── video_r2737.mp4
│
├── logs/
│   ├── adroit_sac_3/
│   └── checkpoints/
└── Adroit_Door_PPO_SAC_final.ipynb
```
The included videos show the learned agent behavior during training..

## Hardware Used

- Google Colab  
- GPU NVIDIA (CUDA)  
- Stable-Baselines3  
- Gymnasium Robotics  
- MuJoCo
  
## Conclusion

The results show that Soft Actor-Critic (SAC) is significantly more effective than PPO for solving the robotic manipulation problem in AdroitHandDoor-v1.

While PPO shows limited improvement over a random policy, SAC learns more complex behaviors thanks to its off-policy approach, replay buffer, and maximum entropy optimization, which enables more efficient exploration of the action space.

Therefore, the experiments demonstrate that off-policy algorithms such as SAC provide important advantages in high-dimensional continuous control environments, particularly in robotic manipulation tasks.
