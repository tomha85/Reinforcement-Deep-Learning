# Reinforcement-Deep-Learning
![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/DQN.png)

The idea of Q-learning is to learn the action-value function, often denoted as Q(s, a) , where s represents the current state and a represents the action being evaluated. Q-learning is a form of Temporal-Difference learning (TD-learning), where unlike Monte-Carlo methods, we can learn from each step rather than waiting for an episode to complete. The idea is that once we take an action and are thrust into a new state, we use the current Q-value of that state as the estimate for future rewards.

![image](https://github.com/tomha85/Reinforcement-Deep-Learning/blob/main/q-learning.png)
we use a Function Approximator. We then use mean-square error as the loss function and update the weights accordingly using gradient descent. Now, the choice remains to choose the function approximator. Enter Deep Learning! We use a neural network as function approximator here. More specifically, we choose a 2-hidden layer network with both the layers having 64 hidden units with relu activation applied after each fully-connected layer. Adam was used as the optimizer for finding the optimal weights
