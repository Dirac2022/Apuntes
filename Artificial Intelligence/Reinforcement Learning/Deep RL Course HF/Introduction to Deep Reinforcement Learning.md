
# Introduction to Deep Reinforcement Learning

An agent (an AI) will learn from the environment by interacting with it (through trial and error) and receiving rewards (negative or positive) as feedback for performing actions.

> Reinforcement learning is a framework for solving control tasks (also called decision problems) by building agents that learn from the environment by interacting with it though trial and error and receiving rewards (positive and negative) as unique feedback


![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/RL_process.jpg)

This RL loop outputs a sequence of **state**, **action**, **reward** and **next state**.

$$
S_0 , A_0, R_1, S_1
$$
The agent's goal is to maximize its cumulative reward, called the **expected return**.
Why? Because RL is based on the **reward hypothesis**, which is that all goals can be described as the **maximization of the expected return**.


## Markov Property
RL process is called a Markov Decision Process (MDP).
The Markov Property implies that our agent **needs only the current state to decide** what action to take and not the history of all the states and actions they took before

## Observations / States Space
Observations/States are the **information our agents gets from the environment**. In the case of a video game, it can be a frame (a screenshot). In the case of the trading agent, it can be the value of a certain stock, etc.
- State s: is a complete description of the state of the world
- Observation o: is a partial description of the state.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/obs_space_recap.jpg)

## Action Space

Si the set of all possible actions in an environment. The actions can come from a discrete or continuous space.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/action_space.jpg)

## Rewards and the discounting
The reward is the **only feedback** for the agent. Thanks to it, our agent knows **if the action taken was good or not**.

The cumulative reward at each time step $t$ can be written as:
![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/rewards_1.jpg)

$$
R(\tau) = \sum_{k=0}^\infty r_{t + k +1}
$$
The rewards that come sooner (at the beginning of the game) are more likely to happen since they are more predictable than the long-term future reward.

**Example**
The mouse's goal is to eat the maximum amount of cheese before being eaten by the cat.
![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/rewards_3.jpg)
It's more probable to eat the cheese near us than the cheese close to the cat (the closer we are to the cat, the more dangerous it is).

The reward near the cat, even if it is bigger (more cheese), will be more discounted since we're not really sure we'll be able to eat it.

To discount the rewards, we proceed like this:

1. We define a discount rate called gamma. It must be between 0 and 1. Most of the time between 0.95 and 0.99.
	- The larger the gamma, the smaller the discount. This means our agent **cares more about the long-term reward**.
	- On the other hand, the smaller the gamma, the bigger the discount. This means our **agent cares more about the short term reward (the nearest cheese)**.
2. Then, each reward will be discounted by gamma to the exponent of the time step. As the time step increases, the cat gets closer to us, **so the future reward is less and less likely to happen**.

Our discounted expected cumulative reward is:
![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/rewards_4.jpg)

## Type of tasks

A task is an **instance** of a Reinforcement Learning problem. We can have two types of task: **episodic** and **continuing**.

### Episodic task
In this case, we have a starting point and an ending point (**a terminal state**). **This creates an episode**: a list of States, Actions, Rewards, and new States.

### Continuing tasks
These are task that continue forever (**no terminal state**). In this case, the agent must **learn how to choose the best actions and simultaneously interact with the environment**.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/tasks.jpg)

## The Exploration/Exploitation trade-off

- *Exploration* is exploring the environment by trying random actions in order to find more information about the environment.
- *Exploitation* is exploiting known information to maximize the reward.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/expexpltradeoff.jpg)


## Two main approaches for solving RL problems
How do we build an RL agent that can **select the actions that maximize its expected cumulative reward?**

### The Policy $\pi$: the agent's brain
The Policy $\pi$ is the brain of our Agent, it´s the function that tells us what **action to take given the state we are in**. So it defines the agent's behavior at a given time.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/policy_1.jpg)

This Policy is the function we want to learn, our goal is to find the optimal policy $\pi$\*, the policy that **maximizes expected return** when the agent acts according to it. We find this $\pi$\* through training.

The are two approaches to train our agent to find this optimal policy $\pi$\*
- **Directly**, by teaching the agent to learn which **action to take**, given the current state: **Policy Based Methods**.
- Indirectly, **teach the agent to learn which state is more valuable** and the take the action that **leads to the more valuable states: Value-Based Methods**.

### Policy-Based Methods

>[!info] We learn a policy function directly

This function will define a mapping from each state to the best corresponding action. Alternatively it could define a probability distribution over a set of possible actions at the state.

We have two types of policies:
- Deterministic: a policy at given state will always return the same action
$$ a = \pi(s) $$

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/pbm_1.jpg)

- Stochastic: outputs a probability distribution over actions.
$$  \pi(a | s) = P[A | s]$$
	where $P[A | s]$ is the probability distribution over the set of actions given the state.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/pbm_2.jpg)

### Value-based methods

>[!tip] Instead of learning a policy function, we learn a value function that maps a state to the expected value of being at that state.

The value of a state is the **expected discounted return** the agent can get if it **starts in that state, and then acts according to our policy** (going to the state with the highest value).

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/value_1.jpg)

Here we see that our value function **defined values for each possible state**.

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/vbm_1.jpg)

![](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/vbm_2.jpg)

## Summary
That was a lot of information! Let’s summarize:

- Reinforcement Learning is a computational approach of learning from actions. We build an agent that learns from the environment **by interacting with it through trial and error** and receiving rewards (negative or positive) as feedback.
    
- The goal of any RL agent is to maximize its expected cumulative reward (also called expected return) because RL is based on the **reward hypothesis**, which is that **all goals can be described as the maximization of the expected cumulative reward.**
    
- The RL process is a loop that outputs a sequence of **state, action, reward and next state.**
    
- To calculate the expected cumulative reward (expected return), we discount the rewards: the rewards that come sooner (at the beginning of the game) **are more probable to happen since they are more predictable than the long term future reward.**
    
- To solve an RL problem, you want to **find an optimal policy**. The policy is the “brain” of your agent, which will tell us **what action to take given a state.** The optimal policy is the one which **gives you the actions that maximize the expected return.**
    
- There are two ways to find your optimal policy:
    
    1. By training your policy directly: **policy-based methods.**
    2. By training a value function that tells us the expected return the agent will get at each state and use this function to define our policy: **value-based methods.**
- Finally, we speak about Deep RL because we introduce **deep neural networks to estimate the action to take (policy-based) or to estimate the value of a state (value-based)** hence the name “deep”.