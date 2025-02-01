# Reinforcement Learning for Cryptocurrency Trading

## Project Overview

This project presents an RL approach for trading in the cryptocurrency market, using historical ETH–CAD data from Yahoo Finance as a case study. The trading problem is formulated as a Markov Decision Process (MDP), where the proposed agent leverages a deep Q-network (DQN) with a fully connected neural network architecture to approximate the Q-values and inform its trading decisions.

## Background

Cryptocurrencies represent a digital or virtual form of currency secured by cryptography. Diverging from traditional currencies issued by central authorities, cryptocurrencies function on decentralized networks utilizing blockchain technology. Financial trading problems, and in particular, cryptocurrency trading, present challenging non-stationary environments where decisions must be made sequentially under uncertainty. Reinforcement learning has emerged as a promising technique to learn optimal trading policies directly from data. In this work, I explore a deep reinforcement learning approach for automated trading using historical ETH–CAD price data.

![image](https://github.com/user-attachments/assets/033b6a1e-b9de-413f-b5ac-d9ae7f53b4a4)

_Figure 1: ETH vs Bitcoin_

To tackle this challenge machine learning and specifically RL can be of great support. The idea is to represent the crypto trading problem as a Markov Decision Process (MDP) and use RL for decision-making, planning, learning, and determining optimal strategies to ultimately maximize rewards. Some several algorithms or agents can be trained to make these decisions, some of them are mentioned below:

![image](https://github.com/user-attachments/assets/6b37d2b4-30c5-407c-aebc-11d9d332f73b)

_Figure 2: Overview of RL algorithms_

The agent is trained using a Deep Q-network (DQN) framework, where the environment is defined by a windowed price trend extracted from the data. The decision process is modeled as an MDP, where at each time step the agent must choose among three actions: hold, buy, or sell. The report describes the design of the agent, the underlying MDP formulation, and the training procedure.

## Markov Decision Process (MDP)
In reinforcement learning, a problem is typically formalized as an MDP defined by the tuple (𝑆, 𝐴, 𝑃, 𝑅, 𝛾)

In this trading application, these components are detailed as follows:

### **State Space 𝑆**

Each state represents the market’s short-term price trend. The state is encoded as the difference between consecutive price points over a sliding window of fixed length. The method get_state(t) extracts a segment of the price trend from time 𝑡 − window_size (with appropriate handling for the initial time steps). The state is a vector of differences:

![image](https://github.com/user-attachments/assets/ff5baae8-a739-4592-8919-701c5c401029)

where ![image](https://github.com/user-attachments/assets/30af31e7-8f0c-40b2-942b-3dd2894bc4f1) is the price at time 𝑡.

### **Action Space 𝐴**

The agent has three possible actions:

1. Hold (action 0): No transaction is executed.
2. Buy (action 1): Purchase one unit of the asset if sufficient funds are available.
3. Sell (action 2): Sell one unit from the agent’s inventory, if any asset is held.

Buying is allowed only if the agent’s current balance is greater than or equal to the asset price at that time. Selling is only possible if there exists at least one asset in the inventory.

### **Transition Dynamics 𝑃**

#### Deterministic Price Evolution

Although the underlying price trend is exogenous (read from historical data), the transition in the MDP is determined by the shift in the sliding window of prices. The environment transitions deterministically from state 𝑠𝑡 to state 𝑠𝑡+1 as the time index increases, while the agent’s account balance and inventory evolve according to its actions.

#### Agent-Environment Interaction

The state transition depends on both the external price dynamics and the agent’s actions. For example, buying reduces available funds and increases inventory, while selling realizes profits or losses based on the difference between the sale price and the original purchase price.

### **Reward Function 𝑅**

The immediate reward is derived from the agent’s change in wealth (or investment performance) after taking an action. In the training loop, the reward is calculated as the relative change in available money compared to the initial balance.

#### Reward Calculation

For each time step, after executing an action:

![image](https://github.com/user-attachments/assets/c13be399-3bfb-4d66-907e-0ffd146cd4e7)

Additionally, the terminal state is reached when the balance falls below the initial investment (a proxy for incurring a loss), which helps shape the agent’s risk-aware decisions.

### **Discount Factor 𝛾**

The discount factor is set to 𝛾 = 0.99, reflecting a high weight for future rewards. This choice encourages the agent to plan for long-term gains rather than focusing solely on immediate returns.

Training Procedure
Iterations:
The train method iterates over the entire dataset for a specified number of epochs. At each time step 𝑡, the agent:

1. Observes the current state 𝑠𝑡 computed from the price differences.
2. Selects an action 𝑎𝑡 based on the epsilon-greedy policy.
3. Executes the action, updating the agent’s balance and inventory.
4. Computes the immediate reward 𝑟𝑡 and the next state 𝑠𝑡+1
5. Stores the experience in the replay memory.
6. Periodically samples a batch from the memory to perform gradient descent and update the Q-network.

The cost (loss) is reported every checkpoint epochs. Additionally, the exploration rate 𝜖 decays gradually, shifting the balance towards exploitation as the agent’s performance improves.

## Trading Strategy Implementation

Buy Action
When the agent chooses to buy (action 1) and if sufficient funds are available, it purchases one unit of the asset. The purchase price is subtracted from the available money, and the asset is added to the inventory.

Sell Action
When the agent chooses to sell (action 2) and if there is at least one unit in the inventory, it sells the asset at the current market price, realizing a profit (or loss) relative to the purchase price. The sale updates the agent’s balance.

Total Gains
The overall profit is computed as the difference between the final and initial amounts of money after the trading period.

Investment Return
The return is expressed as a percentage change relative to the initial investment:

![image](https://github.com/user-attachments/assets/4686f9b7-6c1b-4b95-918c-4e59b244900f)

By formulating the problem as an MDP, the agent was able to learn a trading policy that balances exploration and exploitation using a deep Q-network. The state representation based on price differences over a sliding window, coupled with the reward structure based on investment returns, provides a principled framework for sequential decision-making in volatile financial markets.

## **Experimental Results**

The experimental evaluation of the reinforcement learning trading agent produced the following key results:

During the training phase, the agent's performance was periodically monitored through metrics such as the total reward (or profit) and the training cost (loss) at each checkpoint. The training logs indicate that, over multiple epochs, the agent gradually improved its decision-making capability as evidenced by the declining cost values and the stabilization of profit accumulation.

Figure 3 (shown below) illustrates the training performance across epochs.

![image](https://github.com/user-attachments/assets/70f1d8e6-1932-4119-bb77-983faacbc78e)

_Figure 3: Training performance over epochs showing convergence of the cost function and improvement in total rewards_

Following training, the agent was evaluated in a simulated trading environment using historical ETH–CAD price data. The simulation output detailed logs of every trading decision made by the agent (buy/sell actions) along with corresponding account balances. The resulting buy and sell signals were then overlaid on the price trend to visualize the agent’s performance.

Figure 4 (shown below) presents a plot of the ETH–CAD price history with markers indicating the agent’s buy (upward arrows) and sell (downward arrows) signals. This visual representation highlights how the learned policy corresponds with fluctuations in the market price. Additionally, the figure caption details the total gains and investment return achieved during the simulation.

![image](https://github.com/user-attachments/assets/5ae38ed5-f11f-48ea-aa67-4ede2a69eb56)

![image](https://github.com/user-attachments/assets/07c0409e-eea0-48ad-9fb9-f4b45a909e9c)

_Figure 4: ETH–CAD price trend with trading signals_
