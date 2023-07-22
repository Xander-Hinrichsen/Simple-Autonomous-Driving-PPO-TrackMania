# Deep RL for Trackmania

PPO implementation from scratch for learning how to race in TrackMania with continuous action space, using the [tmrl Trackmania Environment](https://github.com/trackmania-rl/tmrl)

## Results:
![IMG-2018](https://github.com/Xander-Hinrichsen/Simple-Autonomous-Driving-PPO-TrackMania/assets/115660089/e3747bfc-9034-4b4c-9038-2143d7b564ff) \
*preview only, full resuts in [Results/Testdrive.mp4](Results/Testdrive.mp4)

My Record 1:09.43 \
PPO Record: 3:00.9 \
My mom's Record: 4:32.91

## Problem complexity
The tmrl environment is implemented to support a continuous action space: [-1,1], [-1,1], [-1,1],  \
these spaces represent acceleraction, deceleration, and left/right turning respectively 

Since you should be able to do all actions simultaneously, i.e. floor the gas, break, and turn left, \
I chose to implement the action sampling as sampling from a multivariate normal distribution, where the \
neural network has the freedom to determine the mean and logvariance of each distrubtion - \
given the current state - the current in-game lidar measurements, as well as a history of lidar measurements

By creating a multivariate distribution to sample from, and having the current velocity as part of the observation \
space, the neural network should be equipped to handle turning at different speeds and at different accelerations. \
However, this was the one thing that the agent seemed to struggle with the most, as the agent's ability \
to drive without steering left and right needlessly seems to deteriorate as the model learns basic driving capability \
and begins to increase its speed to increase reward.

It is unclear if this problem is due to limitations of model free reinforcement learning - i.e. my model-free ppo is not \
capable of predicting a best case straight trajectory, or if it is because of my choice to allow the model to predict the \
variance of the distrubtion for the action space - i.e. manually decaying the variance over time could allow for more \
stable  action prediction in later training, since if my model is predicting high variance for turning in later traing, it \
will seem like the car is randomly turning

## How to run:
First, follow all of the directions given by the [tmrl Trackmania Environment](https://github.com/trackmania-rl/tmrl) to set up the environment \
Otherwise, all of the RL is implemented in one file, here, within [TrackManiaPPO.ipynb](TrackManiaPPO.ipynb), have fun!
