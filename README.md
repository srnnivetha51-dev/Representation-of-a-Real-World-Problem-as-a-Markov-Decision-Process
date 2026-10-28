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

states = {
    "S1": "Dry",
    "S2": "Moderate",
    "S3": "Wet"
}

actions = {
    "A1": "No Water",
    "A2": "Small Irrigation",
    "A3": "Large Irrigation"
}

transitions = {
    ("S1", "A1"): {"S1": 0.90, "S2": 0.10, "S3": 0.00},
    ("S1", "A2"): {"S1": 0.30, "S2": 0.65, "S3": 0.05},
    ("S1", "A3"): {"S1": 0.05, "S2": 0.35, "S3": 0.60},

    ("S2", "A1"): {"S1": 0.30, "S2": 0.65, "S3": 0.05},
    ("S2", "A2"): {"S1": 0.10, "S2": 0.70, "S3": 0.20},
    ("S2", "A3"): {"S1": 0.05, "S2": 0.35, "S3": 0.60},

    ("S3", "A1"): {"S1": 0.10, "S2": 0.80, "S3": 0.10},
    ("S3", "A2"): {"S1": 0.05, "S2": 0.60, "S3": 0.35},
    ("S3", "A3"): {"S1": 0.00, "S2": 0.20, "S3": 0.80}
}

state_rewards = {
    "S1": -10,
    "S2": 10,
    "S3": -3
}

action_rewards = {
    "A1": 0,
    "A2": -1,
    "A3": -4
}

gamma = 0.90

print("\n--- SMART IRRIGATION MDP DETAILS ---")
print(f"{'State':<12} {'Action':<20} {'Next State':<12} {'Probability':<12} {'Total Reward':<12}")

for (state, action), next_states in transitions.items():
    for next_state, probability in next_states.items():
        if probability > 0:
            reward = state_rewards[next_state] + action_rewards[action]

            print(
                f"{states[state]:<12} "
                f"{actions[action]:<20} "
                f"{states[next_state]:<12} "
                f"{probability:<12.2f} "
                f"{reward:<12}"
            )

print("\nDiscount Factor (Gamma):", gamma)

print("\n--- EXPECTED IMMEDIATE REWARD ---")

current_state = "S1"
selected_action = "A2"

print("Current State:", states[current_state])
print("Selected Action:", actions[selected_action])

expected_reward = 0

print(f"\n{'Next State':<12} {'Probability':<12} {'Total Reward':<15} {'Weighted Reward':<15}")

for next_state, probability in transitions[(current_state, selected_action)].items():
    reward = state_rewards[next_state] + action_rewards[selected_action]
    weighted_reward = probability * reward
    expected_reward += weighted_reward

    print(
        f"{states[next_state]:<12} "
        f"{probability:<12.2f} "
        f"{reward:<15} "
        f"{weighted_reward:<15.2f}"
    )

print("\nExpected Immediate Reward:", round(expected_reward, 2))
print("Future rewards are discounted using Gamma =", gamma)
     
```
---
## Output

The output of the above program will be:
```
Name: S R NIVEDHITHA
Register Number: 212225240102

--- SMART IRRIGATION MDP DETAILS ---
State        Action               Next State   Probability  Total Reward
Dry          No Water             Dry          0.90         -10         
Dry          No Water             Moderate     0.10         10          
Dry          Small Irrigation     Dry          0.30         -11         
Dry          Small Irrigation     Moderate     0.65         9           
Dry          Small Irrigation     Wet          0.05         -4          
Dry          Large Irrigation     Dry          0.05         -14         
Dry          Large Irrigation     Moderate     0.35         6           
Dry          Large Irrigation     Wet          0.60         -7          
Moderate     No Water             Dry          0.30         -10         
Moderate     No Water             Moderate     0.65         10          
Moderate     No Water             Wet          0.05         -3          
Moderate     Small Irrigation     Dry          0.10         -11         
Moderate     Small Irrigation     Moderate     0.70         9           
Moderate     Small Irrigation     Wet          0.20         -4          
Moderate     Large Irrigation     Dry          0.05         -14         
Moderate     Large Irrigation     Moderate     0.35         6           
Moderate     Large Irrigation     Wet          0.60         -7          
Wet          No Water             Dry          0.10         -10         
Wet          No Water             Moderate     0.80         10          
Wet          No Water             Wet          0.10         -3          
Wet          Small Irrigation     Dry          0.05         -11         
Wet          Small Irrigation     Moderate     0.60         9           
Wet          Small Irrigation     Wet          0.35         -4          
Wet          Large Irrigation     Moderate     0.20         6           
Wet          Large Irrigation     Wet          0.80         -7          

Discount Factor (Gamma): 0.9

--- EXPECTED IMMEDIATE REWARD ---
Current State: Dry
Selected Action: Small Irrigation

Next State   Probability  Total Reward    Weighted Reward
Dry          0.30         -11             -3.30          
Moderate     0.65         9               5.85           
Wet          0.05         -4              -0.20          

Expected Immediate Reward: 2.35
Future rewards are discounted using Gamma = 0.9

​
```
<img width="206" height="288" alt="image" src="https://github.com/user-attachments/assets/1dabfbff-c2b0-474b-9fbc-1f2a0bfd67dc" />

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
INTEFERENCES
Inferences – Smart Irrigation System
1. The Smart Irrigation System represents the real-world problem of maintaining proper soil moisture using a Markov Decision Process (MDP).

2. The system has three states: Dry, Moderate, and Wet, representing different soil moisture conditions.

3. The system has three actions: No Water, Small Irrigation, and Large Irrigation to control soil moisture.

4. Transition probabilities describe the likelihood of the soil moving from one moisture state to another after an irrigation action.

5. The Moderate state provides a positive reward of +10, indicating the ideal soil moisture condition.

6. The Dry state gives a reward of -10, while the Wet state gives a reward of -3, discouraging unsuitable soil moisture conditions.

7. For the current state Dry and action Small Irrigation, the expected immediate reward is 2.35.

8. The discount factor γ = 0.90 indicates that future rewards are considered, with less weight given to rewards further in the future.

9. The MDP model helps the irrigation system choose suitable actions to maintain soil moisture and reduce unnecessary water usage.

10. Therefore, the Smart Irrigation System demonstrates how MDP can support intelligent and efficient water management in agriculture.
