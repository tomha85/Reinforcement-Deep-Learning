# Reinforcement-Deep-Learning
![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/DQN.png)

Deep Q learning combines 2 approaches: A Q-learning(SARSA max) and Deep Neural Network to learn Q table approximation

The idea of Q-learning is to learn the action-value function Q(s, a) 
    where s represents the current state and a represents the action being evaluated.
 Q-learning is a type of TD-learning, unlike Monte-Carlo methods, this method learn from each step rather than waiting for an episode to terminate. The idea is take an action and put into a new state, we use the current Q-value of that state to estimate for future rewards.

![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/q-learning.png)

Looking at image above, you ca see whole Deep Q learning
we use a function approximator, then use mean-square error as the loss function and update the weights accordingly using gradient descent. 
We use a neural network as function approximator here. we select a 2-hidden layers network with both the layers having 512 hidden units with relu activation applied after each fully-connected layer. Adam was used as the optimizer for finding the optimal weights.

 ### Hyperparameters

  Here is parameters for code

  | Hyperparameter                      | Value |
  | ----------------------------------- | ----- |
  | Replay buffer size                  | 1e5   |
  | Batch size                          | 64    |
  | $\gamma$ (discount factor)          | 0.99  |
  | $\tau$                              | 1e-3  |
  | Learning rate                       | 5e-4  |
  | update interval                     | 4     |
  | Number of episodes                  | 500   |
  | Max number of timesteps per episode | 2000  |
  | Epsilon start                       | 1.0   |
  | Epsilon minimum                     | 0.1   |
  | Epsilon decay                       | 0.995 |
 
 The Neural Networks architecture :

 Input nodes (37) -> Fully Connected Layer (512 nodes, Relu activation) -> Fully Connected Layer (512 nodes, Relu activation) -> Ouput nodes (4)
 The Neural Networks use the Adam optimizer with a learning rate LR=5e-4 and are trained using a BATCH_SIZE=64
 
 # Results
 
 
![image](https://user-images.githubusercontent.com/31414852/114082292-8eda4280-987b-11eb-8934-c4be170d675d.png)

### Code
  * The DQN agent class, as described in the Deep Q-Learning algorithm. It is included of some methods :
    - constructor : 
        memory buffer
        inititalize 2 instance of newral network (target network and local net work
    - step() : 
       store a step  by agent that is include of state, reward,next state, done in the replay buffer
       every 4 steps means it has enough samples in the replay buffer, then update target network weights with current weight from local netwrk
    - learn() :
       UPDATE newral network parameters from given batch of experiences in buffer replay
    -soft_update() :
       called by learn() to softly update from target neural network from local network weights
    -the replay buffer ():
       store experiences included state, action,reward,next state,done
       add() to add experience step to memory
       sample() to random sample a batch of experience     

    - model.py : Fully connected Neural network using Pytorch
       This network was trained to predict the action rely on the environment states observed. 
       The input layer which size is the state size parameter
       2 hidden fully connected layers of 512 node each
       The output layer which size is the action_size parameter       



