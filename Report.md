[//]: # (Image References)

[image3]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image3.png "QNetwork"
[image4]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image4.png "Algorithm"
[image5]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image5.png "Plot"

[//]: # (Links)
[paper1]: https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf

## Project Report

### Project description

This project aims to train a DQN(Deep Q-learning Networks) agent that can solve a navigation problem where the agent has to navigate in a large square world collecting yellow bananas.
<br>The environment for the navigation problem is provided by Unity-ML Agents which consists of a 37-length vector representing the state and a 4-length vector representing the action space.
<br>The agent will receive a +1 reward when it consumes a yellow banana and will receive a -1 reward when it consumes a blue banana.
<br>The problem is considered to have been solved when the agent achieves an average reward of 13 or more over 100 continuous episodes.

### Learning Algorithm

Q-learning represents action values in a small table called Q-Table which stores action values for each state and action.
<br>DQN applies deep learning techniques to Q-learning representing the action values as neural networks instead of a Q-Table.

But when neural networks are used to represent the action value functions, Q-learning gets very unstable resulting highly diverging losses, often not learning at all.

DQN overcomes this unstability by applying two decent techniques. These are:
* Experience Replay
* Fixed Q-Targets

Consecutive states often form high correlations to each other which can affect the losses to diverge. Experience Replay comes in here to overcome this problem. DQN stores experiences(i.e. [state, action, reward, next_state] tuples) in a container(implemented as ReplayBuffer class in this project) and later randomly samples experiences out from that container, learning from them in order to break the high correlations between experiences.

Also, weights learnt from certain actions can rule over the Q-Network avoiding weights related to other actions to be learnt correctly. Fixed Q-Targets technique comes in here to overcome this problem by creating another Q-Network called Q-Targets which gets updated only by certain steps instead of getting updated every step. In other words, while Q-Network(implemented as qnetwork_local in this project) gets updated every step, Q-Targets remain still for certain steps and gets copied by Q-Network weights after those steps.

Below is the full algorithm pseudo code for training DQN introduced in [DQN Nature paper][paper1] written by Google DeepMind.

![Kernel][image4]

This project implements above algorithm with python.
First, we will initialize replay memory D(implemented as 'ReplayBuffer' class in the code using python built-in library deque) and Q networks with random weights.
<br>Both target and local Q networks will have below structures:

![Kernel][image3]

Each Q network will receive 37-len vector(which represents the environment state) as inputs and then pass it to a 32 units linear layer which will pass the output to a ReLU activation layer.
<br>Then the outputs will be sent to the second linear layer which has 16 units, again passing through a ReLU layer.
<br>Finally the outputs will be sent to the output layer which produces a 4-len vector(representing the action space) each element as the action value for each action.

There are some hyperparameters that can be tuned before training.
<br>In this project, replay buffer size is set to 100,000 and the batch size for sampling is set to 64. The discount factor which will be applied to expected rewards is set to 0.99 and the learning rate for the optimizer(we will use the Adam optimizer) is set to 5e-4. The Q target networks will only get updated every 4 steps.

For each episode while training, we will reset the environment and get a new state.
Since Unity Environment used in this project already returns a well preprocessed state, we don't have to stack the states like the DQN paper algorithm does(in the DQN paper, states are just pixels which cannot represent some valuable information so they stack 3~4 states together to produce a whole state tensor known as phi).

For each step in each episode, we will pass in the state to the Q local network and select an action according to the epsilon-greedy policy(i.e. randomly select an action with the probability of epsilon/1 or select an action according to Q-local).
<br>Then we pass in the selected action to the environment, and receive the next state, reward and done info. We will collect those info, stash them into a tuple and store the tuple in D.

After that, we randomly sample an experience tuple from D and get the action value from Q-targets with the experience(i.e. reward + Q-targets(state, action)). Fixed Q-Targets technique's goal is not letting the Q-local weights to diverge too far away from the fixed Q-targets' weights which means we are kind of assuming the Q-targets as the optimal Q policy.
<br>So, we calculate the loss between Q-local and Q-targets and use the optimizer(Adam in this project) to minimize the losses updating the weights of Q-local.
<br>It is important that we don't update the weights of Q-targets here. They need to be fixed.

After certain steps C, we update the weights of Q-targets. In the paper, Q-local's weights are completely copied over Q-target's weights at every C steps. However, in this project we 'soft update' Q-targets meaning that only a portion of the Q-locsl's weights will be copied to Q-targets' weights. This way, Q-learning can be more stable.

We will keep track of the rewards and check the total rewards earned at each episode. The algorithm will loop through until the total rewards reach the goal we set which is the average of 13 over 100 consecutive episodes(Or until it loops through 2,000 episodes).

### Results

Below is a plot showing the total rewards earned per each episode during training.
This project solved the problem in 537 episodes.

![Kernel][image5]

### Ideas for Future Work

There are some cutting edge DQN algorithms such as Double DQN, Prioritized Experience Replay, Dueling DQN and Rainbow DQN.
<br>I expect that applying those algorithms might allow the agent to solve the problem with less episodes.
