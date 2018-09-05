[//]: # (Image References)

[image1]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image1.gif "Kernel"
[image2]: https://github.com/sseuraeki/DQN_Navigation/blob/master/images/image2.png "Kernel"

## Navigation

### Introduction

This project aims to train a DQN(Deep Q-learning Networks) agent that can solve a navigation problem where the agent has to navigate in a large square world collecting yellow bananas.
<br>The environment for the navigation problem is provided by Unity-ML Agents which consists of a 37-length vector representing the state and a 4-length vector representing the action space.
<br>The agent will receive a +1 reward when it consumes a yellow banana and will receive a -1 reward when it consumes a blue banana.
<br>The problem is considered to have been solved when the agent achieves an average reward of 13 or more over 100 continuous episodes.

![Kernel][image1]

### Dependencies

To set up your python environment to run the code in this repository, follow the instructions below.

1. Create (and activate) a new environment(i.e Anaconda environment) with Python 3.6.

	- __Linux__ or __Mac__: 
	```bash
	conda create --name dqn_navigation python=3.6
	source activate dqn_navigation
	```
	- __Windows__: 
	```bash
	conda create --name dqn_navigation python=3.6 
	activate dqn_navigation
	```

2. Clone the repository (if you haven't already!), and navigate to the python/ folder. Then, install several dependencies.
```bash
git clone https://github.com/sseuraeki/DQN_Navigation.git
cd DQN_Navigation/python
pip install .
```
This project needs unityagents 0.4.0 to be installed which requires pyTorch 0.4.0 as a dependency.
<br>If above commands fail to install pyTorch 0.4.0(possibly because there is a new version), please read the instructions and follow the guidelines in this link: https://pytorch.org/previous-versions/

Or, you can find windows related whl files for previous versions of pytorch at these links:
* CUDA 8.0: http://download.pytorch.org/whl/cu80/torch-0.4.0-cp36-cp36m-win_amd64.whl
* CUDA 9.0: http://download.pytorch.org/whl/cu90/torch-0.4.0-cp36-cp36m-win_amd64.whl
* CUDA 9.1: http://download.pytorch.org/whl/cu91/torch-0.4.0-cp36-cp36m-win_amd64.whl
* CPU: http://download.pytorch.org/whl/cpu/torch-0.4.0-cp36-cp36m-win_amd64.whl

3. Download the Unity environment

Below are links for pre-built Unity environment by Udacity.
<br>Select the environment that matches your OS.

* Linux: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip
* Mac OSX: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip
* Windows(32-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip
* Windows(64-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip

Then, unzip the content to /Banana_Env under the repository directory. (i.e DQN_Navigation/Banana_Env/)

4. Create an [IPython kernel](http://ipython.readthedocs.io/en/stable/install/kernel_install.html) for the `dqn_navigation` environment.  
```bash
python -m ipykernel install --user --name dqn_navigation --display-name "DQN_Navigation"
```

5. Before running code in a notebook, change the kernel to match the `dqn_navigation` environment by using the drop-down `Kernel` menu. 

![Kernel][image2]


### Running the code

1. Training the agent
To see how the agent gets trained and learns, follow the instructions in Navigation.ipynb file. Jupyter Notebook is recommended to open and view this file.
<br>This project already has learnt weights in checkpoint.chp file. Demonstration of this project will use this file to load up the weights.

2. Watching the trained agent
If you want to just see the trained agent in action, run Navigation.py.

