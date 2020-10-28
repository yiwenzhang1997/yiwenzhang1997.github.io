---
layout: post
title: "Course 2 Week 1 Monte Carlo Methods"
date: 2020-10-24
abstract: "My notes of Coursera - Reinforcement Learning Specialization by University of Alberta"
---

When I'm learning courses on Coursera, I usually benefit a lot from other students' notes posted on Github or other platform. Recently I've been learning the Reinforcement Learning Specialization from Coursera and I found very few resourses about this course so I decided to take some notes and post them here. Hopefully it will be helpful for those who are also learning this specialization.


**Lesson 1: Introduction to Monte-Carlo Methods**

- Monte-Carlo (MC) methods estimates value functions based on averaging sample (complete) returns
    - Why need MC? In some problems, we don't know the environment transition probability - computation can be tedious
    - to ensure that well-defined returns are available, MC here only for episodic tasks
    - Value estimates and policies only changed when an episodic was completed. Thus MC updated episodic by episodic but not step by step
    - a Monte Carlo method for learning a value function would first observe multiple returns from the same state. Then, it average those observed returns to estimate the expected return from that state. As the number of samples increases, the average tends to get closer and closer to the expected return.

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled.png)

    Each return is included in the equation for the previous time steps return. That means we can avoid duplicating computations by starting at G_5 and working our way backwards.

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%201.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%201.png)

- Use Monte-Carlo prediction to estimate the value function for a given policy.
    - in order to get q*, first we need to do policy evaluation q(s,a) under pi
        - the value estimates of a state-action pair are obtained by the average of the returns
    - One problem: many state-action pairs may never be visited. if pi is a deterministic policy, one will observe returns only for one of the
    actions from each state.
    - Monte Carlo methods can estimate the value of an individual state independently of the values of any other states.
        - In dynamic programming, the value of each state depends on the values of other states.

**Lesson 2: Monte-Carlo for Control**

- Estimate action-value functions using Monte-Carlo
    - Learning action values is almost exactly the same process as learning state values.
    - We collect returns following a policy from state-action pair and then take their average.
    - Why we learn action value?
        - They allow us to compare different actions in the same state. Then, we can switch to a better action if one is available.
    - We need to let MC explore every possible action when it's sampling
        - One way to maintain exploration is called exploring starts.
            - episodes start in every state-action pair. Afterwards, the agent simply follows its policy
- Understand how to use Monte-Carlo methods to implement a GPI algorithm
    - GPI: Genralized policy iteration
        - GPI includes a policy evaluation and a policy improvement step.
        - GPI algorithms produce sequences of policies that are at least as good as the policies before them.
    - For the policy evaluation step, we will use a Monte Carlo method to estimate the action values.
    - For the policy improvement step, we can make the policy greedy with respect to the agent's current action value estimates.
    - Monte Carlo control methods combined policy improvement and policy evaluation on an episode-by-episode basis.

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%202.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%202.png)

**Lesson 3: Exploration Methods for Monte-Carlo**

- Understand why exploring starts can be problematic in real problems
    - It can be difficult to randomly sample an initial State action pair. for example self-drive car - it would be dangerous and impractical to take a random start
- Describe an alternative exploration method for Monte-Carlo control
    - Epsilon greedy expiration: They usually take the greedy action, but occasionally take a random action.
    - epsilonϵ-greedy exploration the agent will find an \epsilonϵ-soft policy, which is stochastic and might not be the optimal deterministic policy

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%203.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%203.png)

**Lesson 4: Off-policy learning for prediction**

- Understand how off-policy learning can help deal with the exploration problem
    - don't need to deal with exploration-exploitation trade-off
    - On policy: it improve and evaluates the policy being used to select actions (this is the method we have been talking so far)
        - target policy = behavior policy
    - Off policy: improve and evaluate a different policy from the one used to select action
        - you could learn the optimal policy while following a totally random policy
        - If our aging can behave according to a policy that favors exploration. It can experience a much larger number of states.
        - One key rule of off policy learning is that the behavior policy must cover the target policy
- Produce examples of target policies and examples of behavior policies
    - Applications of off-policy learning include learning from data generated by a non-learning agent or human expert. The policy that is being learned (the target policy) can be different from the human expert’s policy (the behavior policy).
- Understand importance sampling
    - importance sampling allows us to do off-policy learning - learning with one policy while following another.

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%204.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%204.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%205.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%205.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%206.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%206.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%207.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%207.png)

- Use importance sampling to estimate the expected value of a target distribution using samples from a different distribution
- Understand how to use importance sampling to correct returns

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%208.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%208.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%209.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%209.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2010.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2010.png)

    ![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2011.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2011.png)

- Understand how to modify the Monte-Carlo prediction algorithm for off-policy learning.

![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2012.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2012.png)

![C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2013.png](C2W1%20Monte%20Carlo%20Methods%204d1b8a57c19e4b708f425ca558f45026/Untitled%2013.png)