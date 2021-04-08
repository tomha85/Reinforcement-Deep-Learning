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

The code consist of :

- model.py : In this python file, a PyTorch QNetwork class is implemented. This is a regular fully connected Deep Neural Network using the [PyTorch Framework](https://pytorch.org/docs/0.4.0/). This network will be trained to predict the action to perform depending on the environment observed states. This Neural Network is used by the DQN agent and is composed of :
  - the input layer which size depends of the state_size parameter passed in the constructor
  - 2 hidden fully connected layers of 1024 cells each
  - the output layer which size depends of the action_size parameter passed in the constructor
- dqn_agent.py : In this python file, a DQN agent and a Replay Buffer memory used by the DQN agent) are defined.
  - The DQN agent class is implemented, as described in the Deep Q-Learning algorithm. It provides several methods :
    - constructor : 
      - Initialize the memory buffer (*Replay Buffer*)
      - Initialize 2 instance of the Neural Network : the *target* network and the *local* network
    - step() : 
      - Allows to store a step taken by the agent (state, action, reward, next_state, done) in the Replay Buffer/Memory
      - Every 4 steps (and if their are enough samples available in the Replay Buffer), update the *target* network weights with the current weight values from the *local* network (That's part of the Fixed Q Targets technique)
    - act() which returns actions for the given state as per current policy (Note : The action selection use an Epsilon-greedy selection so that to balance between *exploration* and *exploitation* for the Q Learning)
    - learn() which update the Neural Network value parameters using given batch of experiences from the Replay Buffer. 
    - soft_update() is called by learn() to softly updates the value from the *target* Neural Network from the *local* network weights (That's part of the Fixed Q Targets technique)
  - The ReplayBuffer class implements a fixed-size buffer to store experience tuples  (state, action, reward, next_state, done) 
    - add() allows to add an experience step to the memory
    - sample() allows to randomly sample a batch of experience steps for the learning       
- DQN_Banana_Navigation.ipynb : This Jupyter notebooks allows to train the agent. More in details it allows to :
  - Import the Necessary Packages 
  - Examine the State and Action Spaces
  - Take Random Actions in the Environment (No display)
  - Train an agent using DQN
  - Plot the scores


