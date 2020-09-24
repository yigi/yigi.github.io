### 1. What Are the Different Types of Machine Learning?
There are three types of machine learning:

- Supervised Learning
In supervised machine learning, a model makes predictions or decisions based on past or labeled data. Labeled data refers to sets of data that are given tags or labels, and thus made more meaningful.
- Unsupervised Learning
In unsupervised learning, we don't have labeled data. A model can identify patterns, anomalies, and relationships in the input data.
- Reinforcement Learning
Using reinforcement learning, the model can learn based on the rewards it received for its previous action.
Consider an environment where an agent is working. The agent is given a target to achieve. Every time the agent takes some action toward the target, it is given positive feedback. And, if the action taken is going away from the goal, the agent is given negative feedback. 

### 2. What Is Overfitting, and How Can You Avoid It? 
Overfitting is a situation that occurs when a model learns the training set too well, taking up random fluctuations in the training data as concepts. These impact the model’s ability to generalize and don’t apply to new data. 

There are multiple ways of avoiding overfitting, such as:

- Regularization. It involves a cost term for the features involved with the objective function
- Making a simple model. With lesser variables and parameters, the variance can be reduced 
- Cross-validation methods like k-folds can also be used
- If some model parameters are likely to cause overfitting, techniques for regularization like LASSO can be used that penalize these parameters
