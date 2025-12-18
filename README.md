## Reinforcement Learning with Customised Gymnasium Environments

### Overview
This project explores Reinforcement Learning (RL) applied to a customised Gymnasium environment, using the Atari IceHockey-v5 environment as a case study.
The main focus of the work is to analyse the impact of reward engineering on the learning performance of different RL algorithms in environments with sparse rewards and long-horizon episodes.

The project was developed as part of Assignment 2 of the Intelligent Systems and Artificial Intelligence course.

**Authors:**
Inês Castro — up202304060
Simão Gomes — up202304752
Soraia Costa — up202305078

***
### Environment: IceHockey-v5
IceHockey-v5 is a competitive Atari environment where:

- The agent controls a single hockey player

- The opponent is controlled by the environment

- The objective is to score more goals than the opponent

- The game runs in continuous time with decisions at every timestep

### Observations

The environment provides observations in the form of raw RGB frames captured directly from the game screen. The agent has no access to the internal game state, such as exact positions, velocities, or puck ownership, resulting in a partially observable environment.

This design transforms the problem from a purely reactive setting into one where short-term temporal dependencies can be learned, which is particularly important in continuous-time sports environments. However, it also significantly increases the dimensionality of the state space, making the learning problem more challenging and placing greater importance on the quality of the reward signal.

As a result, the agent must learn meaningful behaviours based solely on visual input and short-term temporal context, closely resembling real-world scenarios in vision-based reinforcement learning.


### Actions

- Discrete action space with 18 possible actions

- Combination of movement directions and the FIRE action

### Original Reward Function

+1 for scoring a goal

−1 for conceding a goal

This reward structure is highly sparse, providing feedback only on rare terminal events.

***
### Motivation for changes: Sparse Rewards
Sparse rewards pose a major challenge in Reinforcement Learning, especially in long-horizon tasks, continuous-time environments, and competitive settings.

In IceHockey-v5, an agent can perform hundreds of actions without receiving any reward signal, making it difficult to assign credit to intermediate actions and learn meaningful behaviours.

Motivated by findings in the literature on robot football, simulated sports, and multi-agent reinforcement learning, this project investigates whether reward engineering can improve learning efficiency and stability.

### Custom Environment Modifications
The original objective reward (+1 / −1) was preserved, ensuring alignment with the real goal of the game.
Several reward shaping strategies were tested empirically, leading to the final custom reward design.


### Final Implemented Changes:

- Original goal-based reward maintained

- Light incentive for player movement

- Moderate incentive for using the FIRE action

- Penalty for excessive repetition of the same action

- Penalty for prolonged absence of shots

- Temporal penalty removed due to training instability

***
### Algorithms Used
To analyse how different learning paradigms react to reward shaping, three reinforcement learning algorithms were evaluated.

*PPO (Proximal Policy Optimization)*
On-policy algorithm known for stability and robustness

*DQN (Deep Q-Network)*
Off-policy, value-based method, sensitive to reward design

*A2C (Advantage Actor-Critic)*
On-policy algorithm with fast initial learning but lower long-term stability

***
### Experimental Evaluation
The evaluation compares learning curves, reward distributions, mean episode rewards, and training stability across episodes.

### Key Results:
- DQN showed a significant improvement in the custom environment

- A2C achieved a moderate improvement and increased stability

- PPO experienced a slight performance degradation

These results demonstrate that reward engineering is algorithm-dependent and must be carefully designed and validated empirically.

***
### Conclusions:
- Sparse rewards significantly hinder learning in complex environments.
- Reward engineering can greatly improve learning efficiency and stability.
- Different RL algorithms respond differently to the same reward modifications.
- Empirical validation is essential when modifying reward functions.

***
### Future Work
Potential extensions of this project include:

- Integration of Computer Vision techniques for feature extraction

- Learning from higher-level visual representations instead of raw pixels