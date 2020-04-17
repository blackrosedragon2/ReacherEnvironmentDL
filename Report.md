# Report
---

## State and Action Spaces
In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector must be a number between -1 and 1.

## Learning Algorithm

The agent training utilises the `DDPG` class in the DDPG_Continuous_Control notebook.

It continues episodical training via the the ddpg agent until `n_episoses` is reached or until the environment tis solved. The  environment is considered solved when the average reward (over the last 100 episodes) is at least +30.0. Note if the number of agents is >1 then the average reward of all agents at that step is used.

Each episode continues until the environment says any one of the 20 agents are done.

As above, a reward of +0.1 is provided for each step that the agent's hand is in the goal location.

The DDPG agent is contained as a class in [`DDPG_Continuous_Control.ipynb`](https://github.com/blackrosedragon2/ReacherEnvironmentDL/blob/master/DDPG_Continuous_Control.ipynb)

For each time step and agent the Agent acts upon the state utilising a shared (at class level) `Memory`, `actorlocal`, `actortarget`, `optimizeractor`, `criticlocal`, `critictarget` and `optimizercritic` networks.
 

### DDPG Hyper Parameters
- n_episodes (int): maximum number of training episodes

Where
`n_episodes=1000`


Upon running this numerous times it became apparent that the environment would return done at 1000 timesteps. Higher values were irrelevant.

### DDPG Agent Hyper Parameters

- LRactor (double): learning rate of the actor optimizer
- LRcritic (double): learning rate of the critic optimizer
- UPDATE_EVERY (int) : Number of timesteps before network learns new weights
- BUFFER_SIZE (int): Size of the Replay Buffer 
- BATCH_SIZE (int): Number of sampled experince tuples from the replay buffer
- GAMMA (double): Discounting Factor
- TAU (double): Soft Update hyperparameter

Where 
`LRactor=5e-4`
`LRcritic=5e-4`
`UPDATE_EVERY=1`
`BUFFER_SIZE=100000`
`BATCH_SIZE=128`
`GAMMA=0.99`
`TAU=0.001`

### Neural Networks

Actor and Critic network models were also defined in [`DDPG_Continuous_Control.py`](https://github.com/blackrosedragon2/ReacherEnvironmentDL/blob/master/DDPG_Continuous_Control.ipynb).

The Actor networks utilised two fully connected layers with both of them having 128 units with relu activation and tanh activation for the action space. The network has an initial dimension the same as the state size.

The Critic networks utilised two fully connected layers with both of them having 128 units with relu activation. The critic network has  an initial dimension the size of the state size plus action size.

## Plot of rewards
![Reward Plot](https://github.com/blackrosedragon2/ReacherEnvironmentDL/blob/master/media/graph.PNG)

```
Episode 81	Average Score: 30.02
Environment solved in 81 episodes!	Average Score: 30.02
```

## Ideas for Future Work

In addition Proximal Policy Optimization (PPO) and Distributed Distributional Deterministic Policy Gradients (D4PG) methods could be explored.
