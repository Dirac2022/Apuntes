
**Goals**
- Learn about **value-based methods**
- Learn about the **differences between Monte Carlo and Temporal Difference Learning**
- Study and implement **our first RL algorithm**: Q-Learning.


## What is RL? A short recap

The **agent's decision-making process is calle the policy $\pi$**: given a state, a policy will output an action or a probability distribution over actions. That is, given an observation of the environment, a policy will provide an action (or multiple probabilities for each action) that the agent should take.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit3/policy.jpg)

Our goal is to **find an optimal policy $\pi$**, aka., a policy that leads to the best expected cumulative reward.

There are **two main types of RL methods**
- *Policy-based methods*: Train the policy directly to learn which action to take given a state.
- *Value-based methods*: ==Train a value function== to learn ==which state is more valuable== and use this value function ==to take the action that leads to it==.
![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit3/two-approaches.jpg)

## Two types of value-based methods

In value-based methods, **we learn a value function** that **maps a state to the expected value of being at that state.**

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit3/vbm-1.jpg)

> But what does it mean to act according to our policy? After all, we don't have a policy in value-based methods since we train a value function and not a policy.

