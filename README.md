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

The following transition probabilities are illustrative.

| Current State | Action | Next Dry | Next Moderate | Next Wet |
|---|---|---:|---:|---:|
| Dry | No Water | 0.90 | 0.10 | 0.00 |
| Dry | Small Irrigation | 0.30 | 0.65 | 0.05 |
| Dry | Large Irrigation | 0.05 | 0.35 | 0.60 |
| Moderate | No Water | 0.30 | 0.65 | 0.05 |
| Moderate | Small Irrigation | 0.10 | 0.70 | 0.20 |
| Moderate | Large Irrigation | 0.05 | 0.35 | 0.60 |
| Wet | No Water | 0.10 | 0.80 | 0.10 |
| Wet | Small Irrigation | 0.05 | 0.60 | 0.35 |
| Wet | Large Irrigation | 0.00 | 0.20 | 0.80 |

Each row sums to 1.0, representing all possible next soil moisture states for that state-action pair.

Example: If the current state is Dry and the agent selects Small Irrigation, there is a 30% probability of remaining Dry, a 65% probability of reaching Moderate, and a 5% probability of reaching Wet.


## Reward Function



The reward function defines the feedback received by the agent after taking an action.

General form:

$$
R(s,a,s')
$$

### State Rewards

| Next Soil State | Reward |
|---|---:|
| Dry | -10 |
| Moderate | +10 |
| Wet | -3 |

Action rewards


| Action | Additional Reward |
|---|---:|
| No water | 0|
| Small irrigation | -1 |
| Large irrigation | -4 |

The total reward is calculated as:

R(s,a,s')=R_{\text{state}}(s')+R_{\text{action}}(a)


For example, if the agent selects Small Irrigation and the next state becomes Moderate:

R=10+(-1)=+9

Positive rewards encourage suitable soil moisture, while negative rewards discourage dry soil, excessive moisture, and unnecessary water consumption.

Discount factor

gamma=0.90


The discount factor encourages the agent to consider future soil conditions and rewards in addition to immediate rewards.

## Graphical Representation

The graph should include:

1. States as nodes.
2. Actions as arrows.
3. Rewards on transitions.
4. Transition probabilities if applicable.

The following diagram illustrates the MDP states and example transitions.
```
       +-------------------------+
       |        DRY SOIL         |
       |   Moisture below 30%    |
       |       Reward: -10       |
       +-------------------------+
                  |
                  | Small Irrigation
                  | P(Moderate) = 0.65
                  v
       +-------------------------+
       |     MODERATE SOIL       |
       |    Moisture 30%-60%     |
       |       Reward: +10       |
       +-------------------------+
                  |
                  | Large Irrigation
                  | May increase moisture
                  v
       +-------------------------+
       |        WET SOIL         |
       |   Moisture above 60%    |
       |        Reward: -3       |
       +-------------------------+

       Available Actions:
       1. No Water
       2. Small Irrigation
       3. Large Irrigation

```
The following diagram illustrates the MDP states and example transitions.

## Python Representation

Write your code here.

Use Python dictionaries to represent the MDP.


```python
# MDP Representation using Python
# print("Name: S R NIVEDHITHA      ")
# print("Register Number: 212225240102    ")
states = ["Dry", "Moderate", "Wet"]

actions = [
    "No Water",
    "Small Irrigation",
    "Large Irrigation"
]

transitions = {
    "Dry": {
        "No Water": {
            "Dry": 0.90, "Moderate": 0.10, "Wet": 0.00},
        "Small Irrigation": {
            "Dry": 0.30, "Moderate": 0.65, "Wet": 0.05},
        "Large Irrigation": {
            "Dry": 0.05, "Moderate": 0.35, "Wet": 0.60}
    },
    "Moderate": {
        "No Water": {
            "Dry": 0.30, "Moderate": 0.65, "Wet": 0.05},
        "Small Irrigation": {
            "Dry": 0.10, "Moderate": 0.70, "Wet": 0.20},
        "Large Irrigation": {
            "Dry": 0.05, "Moderate": 0.35, "Wet": 0.60}
    },
    "Wet": {
        "No Water": {
            "Dry": 0.10, "Moderate": 0.80, "Wet": 0.10},
        "Small Irrigation": {
            "Dry": 0.05, "Moderate": 0.60, "Wet": 0.35},
        "Large Irrigation": {
            "Dry": 0.00, "Moderate": 0.20, "Wet": 0.80}
    }
}

state_rewards = {
    "Dry": -10,
    "Moderate": 10,
    "Wet": -3
}

action_rewards = {
    "No Water": 0,
    "Small Irrigation": -1,
    "Large Irrigation": -4
}

gamma = 0.90

print("\nStates:", states)
print("Actions:", actions)
print("Discount Factor:", gamma)

print("\nTransition Probability Validation:")

for state in states:
    for action in actions:
        total = sum(transitions[state][action].values())
        print(state, "-", action, "=", round(total, 2))
        assert abs(total - 1.0) < 1e-9

print("All transition probabilities are valid.")

current_state = "Dry"
selected_action = "Small Irrigation"

print("\nSample Decision")
print("Current State:", current_state)
print("Selected Action:", selected_action)

print("Next State Probabilities:",
      transitions[current_state][selected_action])

expected_reward = 0

for next_state, probability in (
    transitions[current_state][selected_action].items()
):
    reward = (
        state_rewards[next_state]
        + action_rewards[selected_action]
    )
    expected_reward += probability * reward

print("Expected Immediate Reward:",
      round(expected_reward, 2))
```
---
## Output

The output of the above program will be:
```
Name: S R NIVEDHITHA
Register Number: 212225240102

States: ['Dry', 'Moderate', 'Wet']
Actions: ['No Water', 'Small Irrigation', 'Large Irrigation']
Discount Factor: 0.9

Transition Probability Validation:
Dry - No Water = 1.0
Dry - Small Irrigation = 1.0
Dry - Large Irrigation = 1.0
Moderate - No Water = 1.0
Moderate - Small Irrigation = 1.0
Moderate - Large Irrigation = 1.0
Wet - No Water = 1.0
Wet - Small Irrigation = 1.0
Wet - Large Irrigation = 1.0
All transition probabilities are valid.

Sample Decision
Current State: Dry
Selected Action: Small Irrigation
Next State Probabilities: {'Dry': 0.3, 'Moderate': 0.65, 'Wet': 0.05}
Expected Immediate Reward: 2.35
```

CALCULATIION

For the current state `Dry` and action `Small Irrigation`:

| Next State | Probability | Total Reward | Weighted Reward |
|---|---:|---:|---:|
| Dry | 0.30 | -10 - 1 = -11 | -3.30 |
| Moderate | 0.65 | 10 - 1 = 9 | 5.85 |
| Wet | 0.05 | -3 - 1 = -4 | -0.20 |

Therefore, the expected immediate reward is:

$$
\begin{aligned}
E[R] &= 0.30(-11) + 0.65(9) + 0.05(-4)\\
&= -3.30 + 5.85 - 0.20\\
&= \boxed{2.35}
\end{aligned}
$$

The expected immediate reward is **2.35**.

## Result

The real-world problem of an AI-Based Smart Irrigation System was successfully represented as a Markov Decision Process using Python. The state space, action space, transition probabilities, reward function, and discount factor were defined.

The program validated all transition probabilities and calculated an expected immediate reward of 2.35 when the soil was Dry and the agent selected Small Irrigation.

This experiment demonstrates how Reinforcement Learning can help optimize irrigation decisions, conserve water, maintain suitable soil moisture, and support healthy crop growth. Further algorithms, such as Q-learning, can be implemented to help the agent learn an effective irrigation policy through repeated interactions with the environment.



---

