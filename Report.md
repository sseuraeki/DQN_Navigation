[//]: # (Image References)

[image4]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image4.png "Algorithm"

[//]: # (Links)
[paper1]: https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf

## Project Report

### Project description

This project aims to train a DQN(Deep Q-learning Networks) agent that can solve a navigation problem where the agent has to navigate in a large square world collecting yellow bananas.
<br>The environment for the navigation problem is provided by Unity-ML Agents which consists of a 37-length vector representing the state and a 4-length vector representing the action space.
<br>The agent will receive a +1 reward when it consumes a yellow banana and will receive a -1 reward when it consumes a blue banana.
<br>The problem is considered to have been solved when the agent achieves an average reward of 13 or more over 100 continuous episodes.

### Learning Algorithm

Q-learning represents action values in a small table called Q-Table.
<br>DQN applies deep learning techniques to Q-learning representing the action values as neural networks instead of a Q-Table.

But when neural networks are used to represent the action value functions, Q-learning gets very unstable resulting highly diverging losses, often not learning at all.

DQN overcomes this unstability by applying two decent techniques. These are:
* Experience Replay
* Fixed Q-Targets

Below is the full algorithm pseudo code for training DQN introduced in [DQN Nature paper][paper1] written by Google DeepMind.

![Kernel][image4]

