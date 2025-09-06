<div align="center">
  <h1>Concise Explanation</h1>
</div>

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
	
---
---

# CRM Digital Twin and Interactive Business Intelligence Dashboard

This project demonstrates an end-to-end data science workflow, transforming raw transactional data into a predictive, interactive "what-if" simulation tool for Customer Relationship Management (CRM). It functions as a **Digital Twin** of the customer base, allowing users to test marketing campaign strategies and receive data-backed ROI projections and strategic advice.

The final output is an interactive BI dashboard built within a Jupyter Notebook using `ipywidgets`.

---

## Strategic Value

The primary goal is to move beyond traditional descriptive analytics (what happened) and predictive analytics (what will happen) into **prescriptive analytics** (what should we do?). This tool acts as a "co-pilot" for decision-makers, enabling them to:
* **Test Strategies Virtually**: Simulate marketing campaigns without committing real-world resources.
* **Get Instant Feedback**: Understand the likely financial impact (CLV uplift, ROI) of different campaign parameters.
* **Make Data-Driven Decisions**: Receive clear, actionable recommendations based on the simulation results.

---

## Methodology Workflow

The project follows a multi-stage data science pipeline:

### 1. Data Preparation
* Loads raw online retail data from an Excel file.
* Performs essential cleaning by removing null values, duplicates, and transactions that don't represent a purchase (e.g., returns with negative quantity).
* Engineers a `TotalPrice` feature by multiplying `Quantity` and `Price`.

### 2. RFM Feature Engineering
* Transforms the transactional data into a customer-centric view using **RFM (Recency, Frequency, Monetary)** analysis.
    * **Recency**: How recently a customer made a purchase.
    * **Frequency**: How often they make purchases.
    * **Monetary**: The total value of their purchases.

### 3. K-Means Customer Segmentation
* Uses the unsupervised **K-Means Clustering** algorithm to group customers into distinct segments based on their RFM behavior.
* The **Elbow Method** is used to determine that **k=4** is the optimal number of segments.
* The clusters are analyzed and given meaningful business names:
    * **Champions**: Best customers; high frequency/monetary, low recency.
    * **At-Risk**: Valuable customers who haven't purchased recently.
    * **Potential Loyalists**: Recent customers with potential to become more valuable.
    * **Lost Customers**: High recency, low frequency/monetary.

### 4. Predictive Modeling
* **Customer Lifetime Value (CLV)**: The `lifetimes` library is used to forecast the future value of each customer over the next 6 months. This involves:
    * A **BG/NBD model** to predict future purchase frequency.
    * A **Gamma-Gamma model** to predict the monetary value of those purchases.
* **Churn Prediction**: An **XGBoost Classifier** is trained to predict the probability that a customer will churn (defined as not making a purchase in the last 180 days).

### 5. "What-If" Simulation Engine
* The core of the digital twin is a simulation function that takes campaign parameters (target segment, discount, expected uplift) as input.
* It simulates the effect of the campaign by updating the RFM values of responsive customers, then uses the trained models to predict the new CLV and churn probability for the segment.
* The final output is a calculation of the total campaign cost, CLV uplift, and projected **Return on Investment (ROI)**.

### 6. Interactive Dashboard
* The entire system is wrapped in an interactive dashboard using `ipywidgets`.
* Users can select a segment, adjust campaign parameters with sliders, and click "Run Simulation" to see the results and an AI-generated strategic recommendation in real-time.

---

## Key Concepts Explained

* **Digital Twin**: A virtual replica of a real-world system (in this case, the customer base) that can be used for simulation and analysis.
* **RFM Analysis**: A marketing technique for segmenting customers based on their Recency, Frequency, and Monetary behavior.
* **K-Means Clustering**: An unsupervised machine learning algorithm that groups data points into a predefined number of clusters (`k`).
* **Elbow Method**: A technique used to find the optimal number of clusters for the K-Means algorithm.
* **Customer Lifetime Value (CLV)**: A prediction of the net profit attributed to the entire future relationship with a customer.
* **Churn Prediction**: The process of identifying customers who are likely to stop using a service or product.
* **XGBoost**: A powerful and popular gradient-boosting algorithm used for classification and regression tasks.
* **`lifetimes` library**: A Python library specifically designed for CLV modeling.
* **`ipywidgets`**: A library for creating interactive user interface elements within Jupyter Notebooks.

---
---
# Reinforcement Learning for Dynamic Pricing

This project builds an autonomous AI agent that learns an optimal **dynamic pricing** strategy to maximize revenue in an e-commerce setting. Using a Deep Q-Network (DQN), the agent is trained through trial-and-error in a custom-built simulation that models real-world customer behavior, including price elasticity.

The final learned policy is evaluated against static pricing strategies (e.g., a fixed price) to demonstrate its superior performance.

---

## Strategic Value

The purpose of this project is to create a prescriptive and automated pricing engine that can adapt to changing conditions (like remaining inventory and time) to maximize profitability. It showcases how Reinforcement Learning can be used to build intelligent agents that actively make strategic business decisions, moving beyond simple analytics to generate tangible value.

---

## Methodology Workflow

The project is structured as a complete Reinforcement Learning pipeline:

1. **Environment Creation**: A custom e-commerce simulation (`EcommerceEnv`) is built using the **OpenAI Gymnasium** framework. This environment acts as the "game" for the AI agent, defining:
    * **State Space**: What the agent can see (time remaining, inventory left).
    * **Action Space**: The decisions it can make (a set of 5 price multipliers).
    * **Demand Curve**: A function that simulates how customer demand changes as the price changes.
    * **Reward Function**: The goal the agent tries to maximize (the daily revenue).

2. **Agent Development**: A **Deep Q-Network (DQN) Agent** (`DQNAgent`) is created using TensorFlow/Keras. This agent's "brain" is a neural network that learns to predict the best action (price) to take in any given state.

3. **Training**: The agent is trained over 500 **episodes** (simulated 30-day sales periods). In each episode, it interacts with the environment and learns from its experiences using key techniques:
    * **Epsilon-Greedy Strategy**: The agent balances exploring random prices to discover new information with exploiting its current best-known strategy.
    * **Experience Replay**: The agent stores its experiences in a memory buffer and learns from a random sample of them, leading to more stable and efficient training.

4. **Evaluation**: After training, the agent's learned dynamic pricing policy is tested and compared against two baseline strategies: a fixed base price and a fixed 20% discount. The results clearly demonstrate that the dynamic approach learned by the RL agent generates significantly higher total revenue.

---

## Key Concepts Explained

* **Reinforcement Learning (RL)**: A type of machine learning where an agent learns to make decisions by performing actions in an environment and receiving rewards or penalties.
* **Deep Q-Network (DQN)**: An RL algorithm that uses a deep neural network to learn a policy. The network learns to predict a **Q-value** (quality score) for each action in a given state.
* **Environment (`EcommerceEnv`)**: The simulated world where the agent learns. It defines the rules, states, actions, and rewards.
* **Price Elasticity**: The economic principle that demand for a product changes in response to its price. This is simulated by the `_get_demand` function.
* **Policy**: The strategy that the agent learns. In this case, it's a mapping from a state (time/inventory) to the optimal action (price).
* **Exploration vs. Exploitation**: The trade-off an RL agent must make between exploring new, random actions and exploiting its current best-known strategy.
* **Experience Replay**: A technique where the agent stores past experiences in a memory buffer and trains on random samples to improve learning stability.

---

## Key Libraries

* **TensorFlow**: The deep learning framework used to build and train the agent's neural network.
* **OpenAI Gymnasium**: The toolkit used to provide a standardized structure for the custom RL environment.
* **Pandas**: Used for data manipulation and analysis.
* **Matplotlib & Seaborn**: Used for creating plots to visualize the training progress and final results.

---
---
# Causal Inference for Personalized Marketing Analytics

This project moves beyond traditional A/B testing to determine the *causal impact* of different marketing actions on individual customer spending. Using the Hillstrom email marketing dataset, it builds a Causal Forest model to provide personalized, data-driven recommendations for which marketing email—men's, women's, or no email—will be most effective for each customer.

The final output is a prescriptive action plan that segments customers based on their predicted responsiveness to each campaign. 

---

## The Problem: Why Averages Aren't Enough

Traditional A/B testing is excellent for measuring the *average* effect of a campaign. For example, it can tell us if, on average, customers who received the "Women's E-Mail" spent more than those who received no email.

However, this average hides crucial details. Some customers in the group might have responded very positively, while others may not have responded at all, or may have even been annoyed by the email. Sending a generic email to everyone can be inefficient and wasteful.

**Causal Inference** allows us to estimate the effect of an action on each *individual*, enabling true personalization.

---

## Methodology Workflow

This project uses the **Double Machine Learning (DML)** framework with a Causal Forest model to isolate the causal impact of multiple treatments.

1. **Data Preparation**:
    * The Hillstrom dataset is loaded, containing 64,000 customers.
    * The core variables for the causal model are defined:
        * **Outcome (Y)**: The target variable we want to maximize, which is `spend`.
        * **Treatment (T)**: The marketing action taken for each customer. The text labels ('No E-Mail', 'Womens E-Mail', 'Mens E-Mail') are mapped to numerical values (0, 1, 2).
        * **Features / Confounders (X, W)**: Customer characteristics known *before* the treatment was applied, such as `recency`, `history`, `zip_code`, and `channel`.

2. **Preprocessing**:
    * A `ColumnTransformer` pipeline is created to prepare the features for the model.
    * **`StandardScaler`** is applied to numerical features to ensure they are on a similar scale.
    * **`OneHotEncoder`** is applied to categorical features (like `zip_code`) to convert them into a numerical format.

3. **Causal Forest Model**:
    * A `CausalForestDML` model from the **EconML** library is trained.
    * The model estimates the **Conditional Average Treatment Effect (CATE)**, also known as **uplift**. This is the predicted increase in spending for a specific customer if they are given a particular treatment compared to the control group (no email).
    * Two sets of uplift scores are calculated: `uplift_womens` (Women's Email vs. No Email) and `uplift_mens` (Men's Email vs. No Email).

4. **Model Interpretation (SHAP Analysis)**:
    * The **SHAP (SHapley Additive exPlanations)** library is used to explain the model's predictions.
    * SHAP summary plots are generated to identify the key customer features (like `history` and `recency`) that have the biggest influence on the uplift scores for each campaign. This helps build trust and provides strategic insights. 

5. **Prescriptive Recommendations**:
    * The uplift scores for each customer are compared.
    * The action with the highest predicted uplift (including the "No E-Mail" option, which has an uplift of zero) is assigned as the `recommended_action`.
    * The final customer base is segmented into three groups based on this optimal action, providing a clear and actionable marketing plan.

---

## Key Concepts Explained

* **Causal Inference**: A branch of statistics and data science focused on determining the cause-and-effect relationship between variables, going beyond simple correlation.
* **Uplift / CATE**: The Conditional Average Treatment Effect. It measures the additional impact (e.g., increase in spending) of a treatment on an individual, given their specific characteristics.
* **Confounders**: Variables (customer features) that can influence both the treatment assignment and the outcome. The model must account for these to avoid biased results.
* **Causal Forest**: An advanced, tree-based machine learning model specifically designed for estimating heterogeneous (individualized) treatment effects.
* **SHAP**: A game theory-based approach for explaining the output of any machine learning model, providing insights into feature importance and impact.

---

## Results & Business Action Plan

The model generated the following prescriptive segments:

* **Womens E-Mail (21,379 Customers)**: This group is predicted to spend the most if they receive the Women's E-Mail. They have a high purchase history and are overwhelmingly previous buyers of women's products.
* **Mens E-Mail (10,477 Customers)**: This smaller but valuable group is most responsive to the Men's E-Mail. Unsurprisingly, they are almost all previous buyers of men's products.
* **No E-Mail (32,144 Customers)**: This large group is predicted to not respond positively to either campaign. Targeting them would likely be a waste of marketing budget. They have the lowest purchase history and highest recency (haven't visited in a while).

This analysis allows the business to focus its marketing efforts on the customers who are most likely to respond, thereby maximizing the return on investment.
	
---
---
# Credit Card Default Prediction with XAI and Fairness Audit

This project demonstrates a complete, end-to-end workflow for building a responsible AI system. It goes beyond simple prediction to create a model that is not only **accurate** but also **transparent** and **fair**.

The project uses the UCI Credit Card Default dataset to:
1. **Predict** which customers are likely to default.
2. **Explain (XAI)** *why* the model makes its predictions.
3. **Audit and Mitigate** potential gender bias in the model's decisions.



---

## Methodology Workflow

The project is structured in three key phases:

### 1. Predictive Modeling
* **Data Exploration**: The dataset is loaded, cleaned, and analyzed. A key finding is the **class imbalance**, with far more non-defaulters than defaulters.
* **Model Training**: An **XGBoost Classifier** is trained to predict the probability of default. The `scale_pos_weight` parameter is used to handle the class imbalance, ensuring the model pays attention to the less frequent but critical default cases.
* **Evaluation**: The model's performance is measured using the **ROC AUC score** and a **confusion matrix**, confirming its strong predictive accuracy.

### 2. Explainable AI (XAI)
* **SHAP (SHapley Additive exPlanations)** is used to "open the black box" of the XGBoost model.
* **Global Explanations**: SHAP summary plots are generated to identify the most influential features globally. This revealed that the most recent payment status (`PAY_0`) and the credit limit (`LIMIT_BAL`) are the top predictors. 
* **Local Explanations**: SHAP force plots (demonstrated in the notebook) can be used to explain the prediction for a single, individual customer.

### 3. Fairness Audit & Mitigation
* **Audit**: The **Fairlearn** library is used to conduct a fairness audit, checking for disparities in the model's performance based on the sensitive feature `SEX`. The audit revealed a bias, quantified by the **Equalized Odds Difference**.
* **Mitigation**: A post-processing technique called `ThresholdOptimizer` is applied. This method adjusts the decision threshold for each gender group to balance the error rates without retraining the entire model.
* **Re-Evaluation**: The audit is run again on the mitigated predictions, confirming that the bias was significantly reduced.

---

## Key Concepts Explained

* **XGBoost**: A powerful and efficient gradient-boosting algorithm used for building high-performance predictive models.
* **SHAP (Explainable AI)**: A method for explaining the output of a machine learning model by calculating the contribution of each feature to a prediction.
* **Fairlearn**: A Python toolkit for assessing and improving the fairness of machine learning systems.
* **Equalized Odds**: A definition of fairness that requires a model to have equal true positive rates and equal false positive rates across different sensitive groups (e.g., male and female).

---

## Conclusion & Key Insight

This project successfully demonstrates a mature data science workflow that balances performance with responsibility.

* **Prediction**: An accurate model was built (ROC AUC of 0.778).
* **Explanation**: The model's decisions were made transparent using SHAP.
* **Fairness**: An initial gender bias was identified and then successfully mitigated, reducing the **Equalized Odds Difference from 0.0465 to 0.0199**.

Most importantly, the project quantifies the **accuracy-fairness trade-off**. Improving fairness resulted in a slight drop in overall accuracy (from 82.03% to 80.95%). This highlights the complex, real-world considerations required when deploying AI systems that impact people's lives.

---
---
# Multi-Label Product Classification and Topic Modeling

This project uses Natural Language Processing (NLP) to tackle two key e-commerce challenges: automatically categorizing products and discovering hidden themes within their descriptions. It builds a complete pipeline that includes a **multi-label classification** model to assign existing category tags and an unsupervised **topic modeling** algorithm to identify new, latent topics from the raw text data.

The project features advanced EDA with an interactive sunburst chart and an interactive topic visualization dashboard.

---

## Strategic Value & Purpose

For a large e-commerce platform, manually categorizing millions of products is inefficient and inconsistent. This project provides a two-pronged solution:

1. **Automated Categorization**: The classification model acts as an intelligent tagging system, reading a product's description and assigning it to multiple relevant categories (e.g., a "smart watch" could be tagged under "Electronics," "Wearable Technology," and "Fitness"). This improves product discovery and user experience.
2. **Uncovering Hidden Insights**: Topic modeling acts as a market research tool. By analyzing the language in product descriptions, it can discover underlying themes or trends in the product catalog (e.g., identifying a growing cluster of products related to "sustainable materials" or "smart home integration") that may not be captured by the existing category structure.


---

## Key Concepts Explained

### Core Machine Learning & NLP Concepts

* **NLP (Natural Language Processing)**
    A field of artificial intelligence that focuses on enabling computers to understand, interpret, process, and generate human language. NLP is the technology behind translation services, chatbots, and the text analysis performed in this project.

* **TfidfVectorizer**
    A method for converting a collection of text documents into a matrix of numerical features. It calculates a score for each word based on two factors:
    * **Term Frequency (TF)**: How often a word appears in a single document.
    * **Inverse Document Frequency (IDF)**: How rare the word is across all documents.
    Words that are frequent in one document but rare overall receive the highest scores, making them powerful predictive features.

* **OneVsRestClassifier**
    A strategy for handling multi-class or multi-label classification problems. It works by training a separate binary (yes/no) classifier for each class. To make a prediction for a new product, it runs all classifiers and assigns all the tags for which the classifier predicts "yes".

* **Logistic Regression**
    A fundamental classification algorithm used to predict the probability of a binary outcome (e.g., yes/no). In this project, it's used as the base estimator within the `OneVsRestClassifier`, where it builds a separate logistic regression model for each category.

* **LabelEncoder**
    A utility for converting categorical text labels into numerical integers (e.g., `['cat', 'dog', 'cat']` becomes `[0, 1, 0]`). While `LabelEncoder` is for single-label problems, this project uses its multi-label equivalent, `MultiLabelBinarizer`, to transform the list of category tags for each product into a binary format the model can learn.

### Visualization & Evaluation Concepts

* **Wordcloud library**
    A visualization tool that creates an image composed of words from a text. The size of each word is proportional to its frequency. While not used in this notebook, it's a popular alternative for quick text exploration. This project uses more advanced visualizations like the sunburst chart and `pyLDAvis`. 

* **t-SNE (t-Distributed Stochastic Neighbor Embedding)**
    An advanced visualization algorithm for exploring high-dimensional data. It creates a 2D or 3D "map" where similar data points are modeled as being close together. This is excellent for discovering underlying clusters. The `pyLDAvis` tool used in this project is based on a similar dimensionality reduction principle to map out the topics. 

* **Confusion Matrix**
    A table used to evaluate the performance of a classification model. It provides a detailed breakdown of predictions by showing the counts of True Positives, True Negatives, False Positives, and False Negatives. Though not explicitly plotted, the `classification_report` in this notebook provides metrics (like precision and recall) that are derived directly from the values in a confusion matrix.

---
---

# Supply Chain Forecasting with Graph Neural Networks

This project demonstrates an advanced forecasting technique using a **Graph Neural Network (GNN)** combined with an LSTM to predict sales and production units for a complex supply chain. Traditional time-series models often fail to capture the intricate relationships between different parts of a supply chain (e.g., how the sales of one product affect the demand for its components). This GNN-based approach learns from the entire interconnected network, leading to significantly more accurate forecasts.

The model's performance is benchmarked against a standard LSTM and a simple moving average to prove its effectiveness.

---

## The Problem: Forecasting in an Interconnected World

Traditional forecasting models typically treat each product's sales history as an independent time series. However, in a real-world supply chain, entities are deeply interconnected:
* The demand for a finished product (e.g., a car tire) directly impacts the required production of its raw materials (e.g., rubber).
* Products sold at the same distribution center may influence each other's sales.
* A promotion for one brand can affect the sales of another.

A **Graph Neural Network (GNN)** is perfectly suited for this problem because it is designed to learn from graph-structured data, allowing it to incorporate the relationships between nodes into its predictions.

---

## Methodology Workflow

The project follows a multi-stage pipeline to build, train, and evaluate the GNN forecasting model.

### 1. Data Loading and Assembly
* Loads multiple CSV files representing different facets of the supply chain:
    * **`nodes.csv`**: Contains the static features of each item (products, plants, etc.).
    * **`edges.csv`**: Defines the relationships (connections) between the nodes.
    * **`temporal.csv`**: Contains the historical time-series data (sales and production quantity) for each node.
* The data is merged and cleaned to create a unified dataset.

### 2. Graph Construction
* The `networkx` library is used to construct a graph that represents the entire supply chain network.
    * **Nodes**: Each unique item (product, plant) becomes a node in the graph, with its features attached as attributes.
    * **Edges**: The relationships from the edges file are used to create connections between the nodes.


### 3. Feature Engineering & Preprocessing
* **Feature Creation**: The node features (both numerical and categorical) are preprocessed. `StandardScaler` is used for numerical features, and `OneHotEncoder` is used for categorical ones.
* **Adjacency Matrix**: The graph's structure is converted into an **adjacency matrix**, a numerical representation that the GNN can understand.
* **Sequence Creation**: The time-series data is transformed into sequences suitable for an LSTM model (e.g., using the past 12 months of data to predict the next month).

### 4. Model Development
Three different models are built for comparison:
1.  **Simple Moving Average**: A basic baseline forecast.
2.  **Standard LSTM Model**: A powerful time-series forecasting model that learns from the historical sequence of each node *independently*.
3.  **GNN-LSTM Model**: The main model. This hybrid architecture uses:
    * A **Graph Convolutional Layer (`GCNConv`)** from the `spektral` library to learn from the features of a node and its neighbors in the graph.
    * An **LSTM layer** to learn from the time-series sequence data.
This allows the model to make predictions based on both a node's own history and the state of the surrounding supply chain.

### 5. Training and Evaluation
* All models are trained on the same training dataset.
* Their performance is evaluated on an unseen test set using the **Mean Absolute Error (MAE)**.
* The results are visualized, clearly showing that the **GNN-LSTM model significantly outperforms** the baseline models, demonstrating the value of incorporating the graph structure into the forecast.

---

## Key Concepts Explained

* **Graph Neural Network (GNN)**: A type of neural network designed to work directly with graph-structured data. It learns by passing messages between connected nodes, allowing it to understand and leverage the relationships within the network.
* **LSTM (Long Short-Term Memory)**: A specialized type of Recurrent Neural Network (RNN) that is excellent at learning patterns in sequential data, such as time-series.
* **Graph Convolutional Layer (`GCNConv`)**: The core building block of the GNN. It's a layer that aggregates information from a node's direct neighbors in the graph, allowing the network to learn from local network structures.
* **Adjacency Matrix**: A square matrix used to represent a graph. The entry in the i-th row and j-th column is 1 if there is an edge connecting node i and node j, and 0 otherwise.
* **`networkx`**: A Python library for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks.

---
---
# Predictive Maintenance for NASA Turbofan Engines using a Bi-LSTM Network

This project demonstrates the application of deep learning for **predictive maintenance**. It builds and trains a **Bidirectional Long Short-Term Memory (Bi-LSTM)** network to accurately predict the **Remaining Useful Life (RUL)** of NASA turbofan jet engines based on time-series sensor data.

The model learns to identify patterns of degradation from the engine sensor readings, providing a forecast that enables maintenance to be performed proactively, before a failure occurs.

---

## Strategic Value & Purpose

In industries like aviation, manufacturing, and energy, unexpected equipment failure can be catastrophic and extremely costly. Predictive maintenance aims to solve this by shifting from a reactive ("fix it when it breaks") or scheduled ("fix it every 1000 hours") approach to a proactive, data-driven one.

The goal of this project is to create an intelligent system that can:
* **Forecast Failures**: Predict the RUL of an engine with high accuracy.
* **Increase Safety**: Prevent in-service failures by scheduling maintenance before the predicted end-of-life.
* **Optimize Maintenance**: Reduce costs by avoiding unnecessary scheduled maintenance on healthy engines.

---

## Methodology Workflow

The project follows a standard time-series deep learning pipeline:

### 1. Data Loading and Preparation
* The NASA C-MAPSS dataset (`train_FD001.txt`, `test_FD001.txt`, `RUL_FD001.txt`) is loaded. This data contains the operational history of 100 turbofan engines run to failure in a simulation.
* Each record includes the engine unit number, the current operational cycle (time), 3 operational settings, and 21 sensor readings.

### 2. Feature Engineering
* The most critical feature, the **Remaining Useful Life (RUL)**, is calculated for the training data. The RUL at any given cycle is the total lifespan of the engine minus its current age (in cycles).
* A domain-specific technique of **RUL capping** is applied. The RUL is clipped at a maximum value of 125 cycles. This forces the model to focus on the period where sensor data shows clear signs of degradation, rather than the long, stable period of early life.

### 3. Data Preprocessing
* **Feature Scaling**: The sensor and operational setting data are normalized using a `MinMaxScaler`. This rescales all features to a consistent range (0 to 1), which improves the stability and speed of neural network training.
* **Time-Series Sequencing**: The flat time-series data is transformed into sequences of a fixed length (50 cycles). This creates "clips" of engine history that the LSTM model can learn from, where each 50-cycle sequence is used to predict the RUL at the end of that sequence. 

### 4. Model Building
* A **Bidirectional LSTM (Bi-LSTM)** network is built using TensorFlow/Keras. This advanced architecture is chosen for its ability to learn from the sequence data in both the forward and backward directions, allowing it to capture a more complete picture of the temporal patterns.
* The model consists of two stacked Bi-LSTM layers and a final `Dense` output layer with a single neuron for the RUL prediction.
* **Mean Squared Error (MSE)** is used as the loss function, as this is a standard regression problem.

### 5. Training and Evaluation
* The model is trained for 100 epochs on the prepared training sequences.
* The training and validation loss are plotted to ensure the model is learning effectively without overfitting.
* The final trained model is used to make predictions on the unseen test set. The performance is evaluated using standard regression metrics:
    * **Mean Absolute Error (MAE)**
    * **Root Mean Squared Error (RMSE)**
    * **R-squared (R²)** score

---

## Key Concepts Explained

* **Predictive Maintenance**: The practice of using data analysis and machine learning techniques to detect anomalies and predict equipment failures in advance.
* **Remaining Useful Life (RUL)**: A prediction of how much longer a piece of equipment (in this case, an engine) will be able to operate before it is likely to fail.
* **LSTM (Long Short-Term Memory)**: A special type of Recurrent Neural Network (RNN) that is exceptionally good at learning patterns from sequential data, like time-series or text. It has internal "memory cells" that allow it to remember important information over long sequences.
* **Bidirectional LSTM (Bi-LSTM)**: An extension of the standard LSTM. A Bi-LSTM processes the sequence data in both the forward (past to future) and backward (future to past) directions. This allows it to capture a more complete context when making a prediction at any given time step. 

---

## Results

The trained Bi-LSTM model demonstrate
d strong performance on the test set, achieving an **R² score of 0.697** and a **Root Mean Squared Error (RMSE) of approximately 17.8 cycles**. This indicates that the model's predictions are, on average, within about 18 cycles of the true RUL, providing a valuable and actionable forecast for scheduling maintenance. The detailed performance plots in the notebook show a strong positive correlation between the predicted and true RUL values.
	
---
---
# Discovering Product Ecosystems with Network Analysis

This project uses **Network Analysis** to uncover the hidden relationships between products based on customer co-purchase behavior. By transforming a raw transaction log from an online retail dataset into a product network, this analysis identifies the most influential "hub" products and automatically discovers natural "product ecosystems"—groups of items that are frequently bought together.

The final output is a rich, interactive visualization of the product network and a data-driven map of these ecosystems, providing deep strategic insights for marketing, merchandising, and recommendation systems.

---

## The Problem: Beyond Bestsellers

Standard sales analysis can easily identify top-selling products. However, it often fails to reveal the *context* of those sales. Understanding which products are purchased *together* is crucial for optimizing store layout, creating effective product bundles, and building a smart recommendation engine.

**Network Analysis** is a powerful technique that models a system as a graph of interconnected nodes, making it the perfect tool to explore these co-purchase relationships.

---

## Methodology Workflow

The project follows a multi-stage pipeline to transform transaction data into an actionable product network:

### 1. Data Preparation
* The "Online Retail" dataset is loaded from an Excel file.
* Essential data cleaning is performed, including removing returns (negative quantity) and transactions without a `CustomerID`.

### 2. Transaction Basket Creation
* The core data transformation step is performed here. The row-by-row transaction log is grouped by `InvoiceNo` to create "baskets"—a list of all products purchased in a single transaction. This is the foundational step for counting co-purchases. 

### 3. Network Construction
* The `networkx` library is used to build a co-purchase graph:
    * **Nodes**: Each unique product becomes a node in the network.
    * **Edges**: A connection (edge) is created between any two products that appear in the same basket.
    * **Weights**: The "weight" of each edge is the number of times the two connected products were purchased together. A higher weight signifies a stronger relationship.

### 4. Network Analysis
Once the graph is built, two key analyses are performed:

* **Centrality Analysis**: This quantitatively identifies the most important products in the network. Three metrics are calculated:
    * **Degree Centrality**: Measures how many direct connections a product has (a measure of its general popularity in baskets).
    * **Betweenness Centrality**: Identifies "bridge" products that connect different parts of the network.
    * **Eigenvector Centrality**: Measures a product's influence based on its connection to *other influential products*.

* **Community Detection**: This analysis automatically discovers clusters of densely connected products within the network.
    * The **Louvain algorithm** is used to partition the graph into communities. These communities represent "product ecosystems"—natural groupings of items that fulfill a common customer need (e.g., a "baking ecosystem" or a "tea time ecosystem").

### 5. Visualization
* The final product network, with nodes colored by their detected community, is visualized using the `plotly` library. This creates a powerful, interactive graph that allows for deep exploration of the product catalog's structure. 

---

## Key Concepts Explained

* **Network Analysis**: A field of data science that studies relationships between entities by modeling them as a graph with nodes and edges.
* **Nodes and Edges**: The fundamental components of a graph. In this project, nodes are products and edges represent co-purchases.
* **Centrality Metrics**: A set of measures used to quantify the importance or influence of a node within a network.
* **Community Detection**: An unsupervised algorithm used in network science to find clusters (communities) of nodes that are more densely connected to each other than to the rest of the network.
* **Louvain Algorithm**: A popular and highly efficient method for community detection in large networks.

---

## Results & Business Applications

The analysis successfully identified several key products and distinct product ecosystems. For example, it found central "hub" products like "JUMBO BAG RED RETROSPOT" and discovered clear communities related to themes like "afternoon tea" and "children's party supplies".

These insights can be directly applied to drive business value:
* **Merchandising**: Create data-driven product bundles and promotions based on the discovered ecosystems.
* **Store Layout/UX**: Place co-purchased items near each other in a physical store or on a website to increase cross-selling.
* **Recommendation Engines**: Build a more sophisticated recommendation system that suggests items from the same product ecosystem.
* **Inventory Management**: Understand how the stock levels of one key product can impact the sales of related items.
	
---
---

# Real-Time IoT Intrusion Detection using LightGBM

This project develops a high-performance machine learning model for **real-time intrusion detection** in Internet of Things (IoT) networks. Using the comprehensive `RT-IoT2022` dataset, it trains a **LightGBM classifier** to accurately identify and categorize various types of cyberattacks, ranging from DDoS to port scanning.

The project emphasizes a robust machine learning workflow, including advanced exploratory data analysis with PCA, a sophisticated preprocessing pipeline, and careful handling of class imbalance to ensure the model is effective in a real-world cybersecurity context.

---

## Strategic Value & Purpose

As IoT devices become ubiquitous in homes, industries, and critical infrastructure, they are increasingly targeted by malicious actors. A reliable, real-time intrusion detection system is essential for protecting these networks. The goal of this project is to:
* **Build a High-Accuracy Classifier**: Create a model that can distinguish between benign network traffic and various types of attacks with a high degree of precision.
* **Enable Real-Time Detection**: Utilize a fast and efficient model (LightGBM) capable of analyzing network traffic and flagging threats as they occur.
* **Provide Actionable Insights**: The multi-class nature of the model provides security analysts with specific information about the type of attack, enabling a faster and more effective response.

---

## Methodology Workflow

The project is structured as a complete data science pipeline for building a robust classification system.

### 1. Data Loading and Preparation
* The `RT-IoT2022` dataset is loaded from a CSV file.
* Initial data cleaning is performed, which includes removing a redundant `time` column.

### 2. Exploratory Data Analysis (EDA)
* The distribution of the target variable (`Attack_type`) is analyzed, revealing a significant **class imbalance**, where some attack types are far more frequent than others.
* **Principal Component Analysis (PCA)** is used for dimensionality reduction. This technique condenses the 83 complex features into just two components, allowing the high-dimensional data to be visualized on a 2D scatter plot. The plot effectively shows that the different attack types form distinct clusters, indicating that they are separable and that a machine learning model is likely to perform well. 

### 3. Preprocessing Pipeline
* The dataset is split into features (`X`) and the target variable (`y`).
* A sophisticated **`ColumnTransformer`** pipeline is built to handle the mixed-type data:
    * **Numerical Features**: `StandardScaler` is applied to scale all numerical features to a consistent range.
    * **Categorical Features**: `OneHotEncoder` is used to convert categorical columns (like `Protocol`) into a numerical format the model can understand.

### 4. Model Training
* The data is split into training (80%) and testing (20%) sets.
* A **LightGBM Classifier** is trained on the data. A key parameter, `class_weight='balanced'`, is used to address the class imbalance. This tells the model to give more importance to the less frequent attack types during training, preventing it from becoming biased towards the most common ones.

### 5. Evaluation
* The trained model is evaluated on the unseen test set using several standard metrics:
    * **Accuracy Score**: The overall percentage of correct predictions.
    * **Classification Report**: A detailed report showing the **precision, recall, and F1-score** for each individual attack category. This is crucial for understanding the model's performance on the rarer attack types.
    * **Confusion Matrix**: A visual breakdown of the model's predictions, showing which classes it is confusing with each other. The resulting matrix shows a strong diagonal, indicating very few misclassifications. 

---

## Key Concepts Explained

* **Intrusion Detection System (IDS)**: A system that monitors network traffic for suspicious activity and alerts security personnel.
* **Multi-Class Classification**: A classification task where each instance can be categorized into one of more than two classes.
* **LightGBM**: A high-performance, open-source gradient boosting framework that uses tree-based learning algorithms. It is known for its speed and efficiency.
* **Class Imbalance**: A common problem in classification where the different classes are not represented equally in the dataset.
* **PCA (Principal Component Analysis)**: A statistical procedure used for dimensionality reduction. It transforms a set of correlated variables into a smaller set of uncorrelated variables called principal components.
* **One-Hot Encoding**: A technique for converting categorical variables into a numerical format that can be provided to machine learning algorithms.

---

## Results & Conclusion

The trained LightGBM model achieved outstanding performance on the test set, with an overall **accuracy of 99.98%**. The detailed classification report shows a macro-averaged **F1-score of 0.96**, indicating that the model performs exceptionally well across all attack categories, including the very rare ones.

This project successfully demonstrates that a well-tuned machine learning model, combined with a robust preprocessing pipeline, can serve as a highly effective and reliable tool for real-time intrusion detection in complex IoT environments.

---
---
# Fraud Detection with a TensorFlow LSTM Autoencoder

This project builds an advanced **anomaly detection system** to identify fraudulent credit card transactions from a real-world dataset. It uses an **unsupervised learning** approach, training a deep learning model exclusively on normal (non-fraudulent) transactions to learn what "normal" behavior looks like.

The core of the model is a **TensorFlow LSTM Autoencoder**, a type of neural network excellent at learning sequential patterns in data. Fraud is detected by calculating the **"reconstruction error"**: the model tries to reconstruct each transaction it sees, and fraudulent transactions, being different from the normal patterns it learned, result in a high error.

---

## Strategic Value & Purpose

Fraud detection is a critical task where fraudulent transactions are rare compared to legitimate ones. Traditional supervised methods often struggle with this severe class imbalance. This project's unsupervised approach offers a powerful alternative:

* **No Need for Labeled Fraud Data for Training**: The model learns the deep patterns of *normal* behavior, which is abundant, rather than trying to learn from the few available fraud examples.
* **Detects New Types of Fraud**: Because the model identifies anything that deviates from the norm, it can flag new, unseen types of fraud that a supervised model trained on past fraud types might miss.
* **Scalable and Real-Time**: This architecture can be deployed to provide real-time risk scoring for incoming transactions, helping to prevent financial losses and protect customers.

---

## Methodology Workflow

The project follows a complete deep learning pipeline for anomaly detection:

### 1. Data Loading and EDA
* Loads the Kaggle "Credit Card Fraud Detection" dataset.
* **Exploratory Data Analysis (EDA)** reveals a severe **class imbalance**: only 0.17% of the transactions are fraudulent. This key insight justifies the use of an unsupervised, anomaly detection approach.

### 2. Data Preprocessing
* The transaction `Amount` feature is scaled using `StandardScaler` to ensure it doesn't dominate other features.
* The data is then split into three sets:
    1. A training set containing **only normal transactions**.
    2. A testing set containing both normal and fraudulent transactions.
    3. A validation set for monitoring training.

### 3. Sequence Creation
* A helper function is used to transform the data into **time-series sequences**. This is a crucial step for the LSTM model, which learns from patterns over a sequence of events, not just a single transaction.

### 4. Model Building (LSTM Autoencoder)
* A sophisticated **LSTM Autoencoder** is built using TensorFlow/Keras. This model has two main parts:
    * **Encoder**: A stack of LSTM layers that reads an input sequence and compresses it into a smaller, dense representation (a "bottleneck").
    * **Decoder**: A stack of LSTM layers that attempts to reconstruct the original input sequence from the compressed representation. 

### 5. Training
* The autoencoder is trained **exclusively on the sequences of normal transactions**. The goal of the training is to teach the model to become very good at reconstructing normal data, minimizing the reconstruction error (Mean Absolute Error).
* The training and validation loss are plotted to ensure the model learns effectively without overfitting.

### 6. Anomaly Detection and Evaluation
* The trained model is used to calculate the **reconstruction error** for every transaction in the test set.
* The key insight is that the model will be good at reconstructing normal transactions (resulting in a low error) but poor at reconstructing fraudulent transactions (resulting in a high error).
* A **threshold** is determined from the distribution of errors. Any transaction with an error above this threshold is flagged as fraudulent.
* The model's performance is evaluated using a **confusion matrix** and a **classification report**, demonstrating high **precision** and **recall** for the critical fraud class.

---

## Key Concepts Explained

* **Anomaly Detection**: The task of identifying data points that deviate significantly from the majority of the data. In this context, fraudulent transactions are the anomalies.
* **Unsupervised Learning**: A type of machine learning where the model is trained on data without explicit labels. Here, the model learns the structure of normal data without being told which transactions are fraudulent.
* **Autoencoder**: A type of neural network trained to reconstruct its input. It's composed of an encoder that compresses the data and a decoder that uncompresses it.
* **LSTM (Long Short-Term Memory)**: A special type of Recurrent Neural Network (RNN) that is excellent at learning patterns in sequential data. It has internal "memory cells" that allow it to remember important information over long sequences.
* **Reconstruction Error**: The difference between the original input and the output reconstructed by the autoencoder. A high error indicates an anomaly.

---

## Results

The LSTM Autoencoder proved to be a highly effective anomaly detector. By setting an appropriate threshold on the reconstruction error, the model was able to identify a majority of the fraudulent transactions while maintaining a low number of false positives. The confusion matrix and classification report confirm that this unsupervised deep learning approach is a powerful and viable solution for real-world fraud detection.
	
---
---
# Predicting a Customer's Next Action in an Online Shopping Clickstream

This project uses a deep learning sequence model to predict the next action a customer will take based on their real-time browsing behavior (clickstream) on an e-commerce website. By analyzing the sequence of events in a user's session, the model learns to anticipate their immediate next step, such as viewing another product, adding an item to the cart, or proceeding to checkout.

The core of the model is a **Long Short-Term Memory (LSTM)** network, a type of recurrent neural network that is exceptionally well-suited for learning patterns from sequential data.

---

## Strategic Value & Purpose

Understanding and predicting user behavior in real-time is crucial for personalizing the online shopping experience and optimizing conversion rates. This project provides the foundation for a system that can:

* **Proactively Personalize the User Experience**: If the model predicts a user is likely to `view_cart`, the website could dynamically display a more prominent "Checkout" button.
* **Prevent Cart Abandonment**: If a user's actions suggest they might leave the site after adding an item to the cart, a timely promotional offer or a "related items" recommendation could be triggered.
* **Optimize Website Flow**: By analyzing common user paths and prediction outcomes, businesses can identify points of friction in the user journey and improve the website's layout and navigation.

---

## Methodology Workflow

The project follows a complete pipeline for building and training a sequence-based prediction model.

### 1. Data Loading and EDA
* The e-commerce clickstream dataset is loaded. It contains user sessions with a sequence of events like `view`, `cart`, and `purchase`
* 
* **Exploratory Data Analysis (EDA)** is performed to understand the data's characteristics. This includes visualizing the distribution of different event types and analyzing the lengths of user sessions, which are crucial insights for preparing the sequence data 

### 2. Data Preprocessing
This is the most critical phase for preparing the data for the LSTM model.
* **Session Creation**: The raw event log is grouped by `session_id` to create individual user journeys
* **Label Encoding**: The text-based event names (e.g., `'cart'`, `'view'`) are converted into numerical integers using a `LabelEncoder`. This is necessary as neural networks can only work with numerical data 
* **Sequence Generation**: The long sessions are transformed into smaller, fixed-length input sequences. For example, a sequence of the first 5 actions in a session is used to predict the 6th action. This process is repeated, creating many training examples from the original sessions.
* **Padding**: Since user sessions have varying lengths, `pad_sequences` is used to ensure that every input sequence fed to the LSTM has the exact same length. Shorter sequences are padded with zeros 

### 3. Model Building (LSTM)
* A sequential deep learning model is built using TensorFlow/Keras with the following key layers
  
    * **Embedding Layer**: This is the first layer. Instead of using the simple integer-encoded events, this layer learns a dense, meaningful vector representation for each unique event type. This helps the model understand the relationships between different actions.
    * **LSTM Layer**: The core of the model. This recurrent layer processes the sequence of event vectors, learning the temporal patterns and dependencies between actions in the clickstream.
    * **Dense (Output) Layer**: The final layer with a `softmax` activation function. It outputs a probability distribution over all possible next actions, allowing the model to make its final prediction.

### 4. Training and Evaluation
* The model is trained on the prepared sequence data for 10 epochs 
* The model's performance is evaluated on an unseen test set using 
    * **Accuracy Score**: The overall percentage of correct next-action predictions.
    * **Classification Report**: A detailed breakdown of precision, recall, and F1-score for each event type.
    * **Confusion Matrix**: A visual matrix showing which actions the model predicted correctly and which ones it tended to confuse.

---

## Key Concepts Explained

* **Clickstream Analysis**: The process of analyzing the path a user takes through a website, which is represented as a sequence of clicks or events.
* **LSTM (Long Short-Term Memory)**: A special type of Recurrent Neural Network (RNN) that is excellent at learning patterns from sequential data. It has internal "memory cells" that allow it to remember important information over long sequences, making it ideal for understanding user journeys. 
* **Embedding Layer**: A deep learning layer used in NLP and sequence modeling that learns a dense vector representation for each item in a vocabulary (e.g., each event type). This allows the model to capture the semantic similarity between items.
* **Padding**: The process of adding a special value (usually zero) to shorter sequences to ensure that all sequences in a batch have the same length, which is a requirement for training deep learning models.

---
---
