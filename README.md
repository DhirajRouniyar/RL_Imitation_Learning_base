# RL : Imitation_Learning_base

Proximal Policy Optimization (PPO) can be used for imitation learning on robotic manipulators.

Here, I first explored value-based approaches like DQN and Dueling DQN. Working with these algorithms helped me build a solid understanding of reinforcement learning fundamentals, such as Q-function approximation, experience replay, stability through target networks, and improvements from the dueling architecture in separating state value and action advantage. These concepts provided the groundwork for moving toward policy-gradient methods. In the case of manipulators, PPO can be used for imitation learning by first collecting expert demonstrations of robot arm trajectories and translating them into state-action pairs. 

The pipeline typically involves: 
(1) collecting demonstration data, 
(2) using an inverse reinforcement learning (IRL) or adversarial imitation learning approach to extract a reward signal, 
(3) training the policy with PPO to maximize this learned reward while ensuring stable updates, and 
(4) evaluating and refining the policy on the manipulator tasks. This combination allows the manipulator to not only mimic expert actions but also generalize to unseen states, achieving robust performance beyond simple behavior cloning.

## Implementation

- Dueling DDQN, DQN and PPO on Lunar Lander environment

#### Code structure

- A jupyter notebook with the implementation of DQN, Dueling DDQN and PPO is available in the Policy_vs_Value folder.


#### Implementation Details
##### Algorithms:

1. Deep Q-Network (DQN)
  - DQN uses a neural network to approximate the Q-function, allowing it to handle high-dimensional state spaces.
  - To reduce instability when training with neural networks, experience replay is introduced. In this method, past transitions are stored in a replay buffer and sampled randomly, which breaks temporal correlations and stabilizes learning.
  - Additionally, DQN employs two networks: the online (actor) network and the target network. The online network is updated at every step, while the target network provides stable Q-value estimates for the next state during training. The target values are then used to compute the loss and update the online network, improving training stability.
  - (For code and details, refer to the Jupyter notebook.)

2. Dueling Double DQN (Dueling DDQN)
  - Standard DQN often overestimates Q-values, which can result in learning a weaker policy. Double DQN addresses this by decoupling action selection and action evaluation across two networks, reducing bias in Q-value estimation.
  - Dueling DQN further enhances this by introducing a dueling architecture. Instead of a single stream producing Q-values, the network is split into two branches: one branch estimates the state value (V(s)), and the other estimates the advantage of each action (A(a)). The outputs are then combined to generate Q-values.
  - This design helps the agent better distinguish between valuable states and unimportant ones, even when specific actions don’t matter much.
  - (For implementation, see the Jupyter notebook.)

3. Proximal Policy Optimization (PPO)

  - PPO is a policy-gradient method, in contrast to DQN and DDQN which are value-based. It directly learns the policy instead of approximating action values.
  - The algorithm optimizes a surrogate objective function that restricts policy updates from moving too far away from the previous policy, preventing instability.
  - This objective encourages the policy to assign higher probabilities to actions that yield greater returns while discouraging poor actions. The clipping mechanism ensures updates remain within a safe range, avoiding destructive policy shifts.
  - (Refer to the Jupyter notebook for implementation details.)
  - [Implementation Matters in Deep Policy Gradients: A Case Study on PPO and TRPO,Logan et. al.](https://doi.org/10.48550/arXiv.2005.12729)
  
#### Run Locally
clone the project 
``` bash
git clone git@github.com:Hussain7252/ReinforcementLearning_Odessey.git
```
```bash
cd PolicybasedVSvaluebased
```
In the anaconda prompt
```bash
conda create --name myenv python=3.9
conda activate myenv
```
```bash
conda install --file requirements.txt
```
Launch jypter notebook
```bash
Run the DQN.ipynb for DQN on Lunar Lander
Run the deulingdoubleql.ipynb for  Dueling DDQN on Lunar Lander
Run the PPO.ipynb for PPO on Lunar Lander
```

#### Results
<p align="center">
  <img src="https://github.com/DhirajRouniyar/RL_Imitation_Learning_base/blob/main/Output/Final%20plots%20comparision.png">
</p>

#### Acknowledgements:
- [Reinforcement Learning: An Introduction, Suttton et. al.](https://doi.org/10.1016/S1364-6613(99)01331-5)
- [OpenAI](https://openai.com/research/openai-baselines-ppo)
