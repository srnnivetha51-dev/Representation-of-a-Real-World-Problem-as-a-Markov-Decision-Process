# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim
To identify a real-world smart irrigation problem and represent it as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, and discount factor using Python. The aim is to understand how Artificial Intelligence and Reinforcement Learning can optimize water usage, maintain soil moisture, and improve crop growth.


## Problem Statement

### Problem Description

Farmers often face difficulties in deciding when and how much water to supply to crops. Excessive irrigation wastes water and may damage crops, while insufficient irrigation causes the soil to become dry and affects plant growth.

An AI-based Smart Irrigation System monitors soil moisture and selects suitable irrigation actions. Depending on the current soil condition, the intelligent agent can keep the water supply off, provide a small amount of water, or provide a large amount of water.

After an action is performed, the soil moisture may change according to the transition probabilities. The agent receives rewards or penalties based on the resulting soil condition and the amount of water used.

By applying Reinforcement Learning, the system can learn a suitable irrigation strategy to maintain healthy soil moisture, reduce water wastage, and improve crop growth.

Note: The transition probabilities and rewards in this experiment are illustrative assumptions, not measurements from an actual farm.


---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of soil moisture states |
| $A$ | Set of irrigation actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

States: Dry, Moderate, and Wet.
Actions: No Water, Small Irrigation, and Large Irrigation.
Transition probabilities: Probability of reaching a particular soil condition after an irrigation action.
Reward function: Rewards healthy soil moisture and penalizes excessive water usage or dry soil.
Discount factor: \(\gamma=0.90\), which gives importance to future rewards as well as immediate rewards.

---

## State Space



The state space represents all possible soil moisture conditions.

```
S = {Dry,Moderate,Wet,}

```
```
states = {
    "Dry": "Soil moisture below 30%",
    "Moderate": "Soil moisture between 30% and 60%",
    "Wet": "Soil moisture above 60%"
}


```
The states are explained below:
1. Dry: The soil has insufficient moisture, and crops may require irrigation.
2. Moderate: The soil has a suitable moisture level for crop growth.
3. Wet: The soil has high moisture, and additional irrigation may cause water wastage.

## Sample State
Dry is a sample state. It means that the soil moisture is below 30%. The AI agent may choose to provide a small or large amount of water to improve the soil condition.
## Action space

The action space represents all irrigation decisions available to the intelligent agent.



```
A = {No Water, Small Irrigation, Large Irrigation}
```


```
actions = [
    "No Water",
    "Small Irrigation",
    "Large Irrigation"
]
```
The actions are explained below:
1. No Water: Keep the irrigation system switched off.
2. Small Irrigation: Supply a small quantity of water to the crops.
3. Large Irrigation: Supply a larger quantity of water to increase soil moisture quickly.

## Sample Action

When the current state is Dry, the agent may select Small Irrigation to increase soil moisture while avoiding unnecessary water consumption.



## Transition Probability



It represents the probability of reaching the next soil moisture state \(s'\) after taking action \(a\) in the current state \(s\).

General form:

$$
P(s' \mid s,a)
$$

This means:

> Probability of reaching next state $s'$ after taking action $a$ in current state $s$.

Current State	Action	Next Dry	Next Moderate	Next Wet
Dry	No Water	0.90	0.10	0.00
Dry	Small Irrigation	0.30	0.65	0.05
Dry	Large Irrigation	0.05	0.35	0.60
Moderate	No Water	0.30	0.65	0.05
Moderate	Small Irrigation	0.10	0.70	0.20
Moderate	Large Irrigation	0.05	0.35	0.60
Wet	No Water	0.10	0.80	0.10
Wet	Small Irrigation	0.05	0.60	0.35
Wet	Large Irrigation	0.00	0.20	0.80



## Reward Function

Write your answer here.

The reward function defines the feedback received by the agent after taking an action.

General form:

$$
R(s,a,s')
$$



---

## Graphical Representation

Write your answer here.

Draw the MDP graph.

The graph should include:

1. States as nodes.
2. Actions as arrows.
3. Rewards on transitions.
4. Transition probabilities if applicable.


---

## Python Representation

Write your code here.

Use Python dictionaries to represent the MDP.


```python
# MDP Representation using Python
# print("Name:       ")
# print("Register Number:     ")

```
---
## Output

Write your Python output here.


---

## Result

Write your result here.



---

