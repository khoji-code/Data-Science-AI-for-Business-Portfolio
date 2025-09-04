<div align="center">
  <img/>
</div>
<div align="center">
  <img/>
  <h1>📊 Concise Explanation 📈</h1>
</div>
---

# Deep Reinforcement Learning for Strategic Budget Allocation

This project uses Deep Reinforcement Learning (DRL) to train an AI agent that learns an optimal budget allocation strategy. The agent is trained in a custom business simulation built with real-world e-commerce data.

---
## Core AI Concepts

* **Deep Learning**: A type of AI that uses multi-layered neural networks (inspired by the brain) to learn complex patterns from large amounts of data. The "deep" refers to having many layers.
* **Reinforcement Learning (RL)**: A training method where an AI agent learns by performing actions in an environment and receiving rewards or penalties. The agent's goal is to maximize its total long-term reward.
* **Deep Q-Network (DQN)**: The specific RL algorithm used in this project. It combines Q-Learning with a deep neural network to predict the best action to take in complex situations.

---
## Reinforcement Learning Components

* **Environment (`BusinessEnv`)**: The "world" or "game" where the agent learns. In this project, it's a custom-built business simulator.
* **Agent (`DQNAgent`)**: The "brain" or "player" that makes decisions. Its goal is to learn a winning strategy, or **policy**.
* **State Space (Observation Space)**: The set of all possible situations the agent can be in. Here, it's the list of 5 key business metrics (e.g., review score, new customers).
* **Action Space**: The set of all possible moves the agent can make. Here, it's the 3 investment choices: Marketing, Seller Incentives, or Logistics.
* **Reward**: The feedback score the agent receives after taking an action. It guides the learning process by telling the agent if its move was good or bad.
* **Step**: A single moment in the environment. The `step()` function moves the simulation forward by one "turn" (one month) in response to the agent's action.
* **Episode**: One full run of the simulation from start to finish. The agent learns by playing through many episodes.

---
## The AI Agent (DQN) Explained

* **Q-value**: A score that represents the "quality" or expected long-term reward of taking a specific **action** in a particular **state**. The agent's goal is to choose the action with the highest Q-value.
* **Q-table**: A simple "cheat sheet" that stores the Q-value for every possible action in every state. It's only practical for simple problems.
* **Loss Function**: A formula used to measure the error in the agent's predictions (the difference between the predicted Q-value and the target Q-value). The goal of training is to minimize this loss.
* **Memory Buffer (Experience Replay)**: A memory bank where the agent stores its past experiences. It learns by studying a random sample of these memories, which makes training more stable and efficient.
* **Gamma ($\gamma$)**: The **discount factor** (0 to 1). It controls the agent's foresight, balancing the importance of immediate rewards versus future rewards. A high gamma encourages long-term planning.
* **Epsilon ($\epsilon$)**: The **exploration rate**. It controls the balance between exploring random moves to discover new strategies and exploiting the current best-known strategy.
* **Learning Rate**: A small number that controls how much the agent's neural network is updated during training. It's the "step size" of the learning process.
* **Adam Optimizer**: An efficient algorithm for adjusting the neural network's parameters to minimize the loss.

---
## Key Libraries & Code Components

* **Gymnasium (formerly OpenAI Gym)**: A toolkit that provides a standard structure (`gym.Env`) for building RL environments, making them compatible with different agents.
* **TensorFlow**: The deep learning library used to build, train, and manage the neural network that powers the agent.
* **`__init__()`**: The constructor method in a Python class. It initializes an object's attributes when it is first created.
* **`super()`**: A function that calls a method from a parent class. It's used here to ensure the standard setup of the `gym.Env` is run before custom initializations are added.
* **`pandas.merge`**: A function used to combine data tables based on a common column, similar to a JOIN in SQL.
	
