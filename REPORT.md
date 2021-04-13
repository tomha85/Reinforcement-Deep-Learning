# Reinforcement-Deep-Learning
![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/DQN.png)

Deep Q learning combines 2 approaches: A Q-learning(SARSA max) and Deep Neural Network to learn Q table approximation

Q-learning is to learn the action-value function Q(s, a): s: the current state and a: the action being evaluated.
Q-learning is a type of TD-learning, unlike Monte-Carlo methods, this method learn from each step rather than waiting for an episode to terminate. The idea is take an action and put into a new state, we use the current Q-value of that state to estimate for future rewards.

![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/q-learning.png)

Looking at image above, you can see  the whole Deep Q learning algorithm
we use a function approximator, then use mean-square error as the loss function and update the weights accordingly using gradient descent. 
We also have a neural network, then select a 2 fully connected hidden layers network with both the layers having 512 hidden units with relu activation . Adam optimizer was used  for finding the optimal weights.

 ### Hyperparameters

  Here is parameters for code

  | Hyperparameter                      | Value |
  | ----------------------------------- | ----- |
  | Replay buffer size                  | 1e5   |
  | Batch size                          | 64    |
  | gamma (discount factor)             | 0.99  |
  | tau                                 | 1e-3  |
  | Learning rate                       | 5e-4  |
  | update interval                     | 4     |  
  | Max number of timesteps per episode | 2000  |
  | Epsilon start                       | 1.0   |
  | Epsilon minimum                     | 0.1   |
  | Epsilon decay                       | 0.995 |
 
 The Neural Networks architecture :

 Input nodes (37) -> Fully Connected Layer (512 nodes, Relu activation) -> Fully Connected Layer (512 nodes, Relu activation) -> Ouput nodes (4)
 The Neural Networks: Adam optimizer, learning rate LR=5e-4 and batch_size=64
 
 # Results
The average score of agent was able to solve the environment by achieving score of 13 over 100 consecutive episodes after 741 episodes.
 
![image](https://user-images.githubusercontent.com/31414852/114491187-2b864280-9be4-11eb-8ac8-c687a9d8cb80.png)

![image](https://user-images.githubusercontent.com/31414852/114491196-3214ba00-9be4-11eb-8aec-05f9e8d722c1.png)

### Code
  * The DQN agent class, as described in the Deep Q-Learning algorithm. It is included of some methods :
    - constructor : 
        memory buffer,
        inititalize 2 instance of neural network (target network and local network)
    - step() : 
       store a step  by agent that is include of state, reward,next state, done in the replay buffer
       every 4 steps means it has enough samples in the replay buffer, then update target network weights with current weight from local netwrk
    - learn() :
       UPDATE newral network parameters from given batch of experiences in buffer replay
    -soft_update() :
       called by learn() to softly update from target neural network from local network weights
    -the replay buffer ():
       store experiences included state, action,reward,next state,done
       add() to add experience step to memory,
       sample() to random sample a batch of experience     

    - model.py : Fully connected Neural network using Pytorch
       This network was trained to predict the action rely on the environment states observed. 
       The input layer which size is the state size parameter,
       2 hidden fully connected layers of 512 node each,
       The output layer which size is the action_size parameter 
       
### Future work
 Implementaion difference method to increase the performance of agent
 
 Double DNQ
 
 Dueling DNQ
 
 Prioritized experience replay
 
 Now, code was trained on workspace Udacity without lauching simulation video, we can not get the raw images and feeding to newral network. In future work, I wil use own computer should  be set up video of agent, and training with pixel.

