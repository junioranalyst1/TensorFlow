# Inspiration

This project was inspired by the following talk: https://www.youtube.com/watch?v=QDXfKXi_Q_A

# Notes

### Cell 1
This cell imports necessary libraries and modules:
- `math`, `random`, `numpy`, and `pandas` are foundational Python libraries for scientific computing.
- `tensorflow` is for building and training machine learning models.
- `matplotlib.pyplot` is for creating plots and visualizations.
- `pandas_datareader` and `yfinance` are for fetching financial data.
- `tqdm` is for displaying progress bars.
- `deque` is a double-ended queue from the collections module, often used for efficiently adding/removing items from either end.

### Cell 2
This cell checks the version of TensorFlow being used in the notebook.

### Cell 3
This cell defines a class `AI_Trader` which seems to be implementing a trading agent, possibly using Reinforcement Learning. 

- The `__init__` method initializes the instance variables such as `state_size`, `action_space`, `memory`, `inventory`, and `model`. It also sets some hyperparameters like `gamma`, `epsilon`, `epsilon_final`, and `epsilon_decay`.
  
- The `model_builder` method builds a simple neural network model using TensorFlow's Keras API. This model likely represents the Q-function in Q-learning, a form of Reinforcement Learning.
  
- The `trade` method chooses an action. It either selects a random action (exploration) with probability `epsilon`, or selects the action with the highest Q-value (exploitation) based on the current state.
  
- The `batch_train` method trains the model with a batch of experiences from the memory. It updates the Q-values towards the target Q-values and applies epsilon decay.

### Cell 4
This cell defines a function, `sigmoid`, which takes a number `x` as input and returns the sigmoid of `x`. The sigmoid function maps any input value to a value between 0 and 1, often used to squash the output of a neuron in neural networks to be in the range of 0 to 1.

### Cell 5
This cell defines a function, `stocks_price_format`, which formats a number `n` to a string representing a dollar amount, with a minus sign prefix if the number is negative.

### Cell 6
This cell defines a function, `dataset_loader`, to download stock data for a given `stock_name` using the `yfinance` library and return the 'Close' prices of the stock. It then calls this function with "AAPL" as the `stock_symbol` and prints the returned close prices.

### Cell 7
This cell defines a function, `state_creator`, which creates the state representation for the model, given the data, a timestep, and a window size. It processes a window of stock prices, applying the sigmoid function to the differences between consecutive prices, and returns the processed window as the state.

### Cell 8
This cell loads the dataset for "AAPL" by calling the `dataset_loader` function defined earlier.

### Cell 9
This cell defines some parameters: `window_size` is the size of the window of stock prices used to create the state, `episodes` is the number of episodes for training the model, `batch_size` is the number of samples used in each training batch, and `data_samples` is the number of samples in the data.

### Cell 10
This cell creates an instance of the `AI_Trader` class defined earlier, passing the `window_size` as a parameter.

### Cell 11
This cell contains the main training loop. For each episode, it resets the environment and the agent, then iterates over the data samples, making the agent choose actions and training the agent's model with the experiences collected. After each episode, if the episode number is a multiple of 10, it saves the model.

- The agent receives a reward when it sells stocks, equivalent to the price difference between the buying and selling actions.
- The agent trains its model using a batch of experiences from its memory if the memory has more than `batch_size` experiences.
- It prints the total profit obtained in each episode.