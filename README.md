# Coin Toss Application

Welcome to the "Expanding" Coin Toss Application! This README will guide you through the setup, usage, and features of the application.

## Overview

This application allows users to simulate multiple coin tosses, calculate the mean outcome, and visualize the results through a line chart and a results table. It is built using Streamlit, a Python library for creating interactive web applications.

## Features

- **Set Number of Trials**: Use a slider to set the number of coin tosses.
- **Run Simulation**: Start the simulation by clicking a button.
- **Calculate Mean**: Compute the mean outcome of the coin tosses (0 or 1).
- **Visualize Progress**: Display the progress of the mean calculation in a line chart.
- **Results Table**: Show a table of results from all simulation runs.

## Requirements

- Python 3.7 or higher
- Streamlit
- SciPy
- Pandas

## Installation

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Install the required Python packages:
    ```bash
    pip install streamlit scipy pandas
    ```

## Usage

1. Run the Streamlit application:
    ```bash
    streamlit run app.py
    ```

2. Open the provided URL (usually `http://localhost:8501`) in your web browser.

## Code Explanation

### Import Libraries

```python
import streamlit as st
import scipy.stats
import pandas as pd
import time
```

### Initialize Stateful Variables

These variables persist across reruns of the script.

```python
if 'experiment_no' not in st.session_state:
    st.session_state['experiment_no'] = 0

if 'df_experiment_results' not in st.session_state:
    st.session_state['df_experiment_results'] = pd.DataFrame(columns=['no', 'iterations', 'mean'])
```

### Header and Interface Elements

Set up the header, slider, and button for user interaction.

```python
st.header('Tossing a Coin')

number_of_trials = st.slider('Number of trials?', 1, 1000, 10)
start_button = st.button('Run')
```

### Toss Coin Function
Simulate coin tosses, calculate the mean, and update the chart.

```python
def toss_coin(n):
    trial_outcomes = scipy.stats.bernoulli.rvs(p=0.5, size=n)
    mean = None
    outcome_no = 0
    outcome_1_count = 0

    for r in trial_outcomes:
        outcome_no += 1
        if r == 1:
            outcome_1_count += 1
        mean = outcome_1_count / outcome_no
        chart.add_rows([mean])
        time.sleep(0.05)

    return mean
```

### Run Simulation and Update Results
Trigger the simulation, update the session state, and display the results table.

```python
if start_button:
    st.write(f'Running the experiment of {number_of_trials} trials.')
    st.session_state['experiment_no'] += 1
    mean = toss_coin(number_of_trials)
    st.session_state['df_experiment_results'] = pd.concat([
        st.session_state['df_experiment_results'],
        pd.DataFrame(data=[[st.session_state['experiment_no'], number_of_trials, mean]],
                     columns=['no', 'iterations', 'mean'])
    ], axis=0)
    st.session_state['df_experiment_results'] = st.session_state['df_experiment_results'].reset_index(drop=True)

st.write(st.session_state['df_experiment_results'])
```

###Deployment
To deploy the application to Render or any other hosting service, follow these steps:

Commit your changes to a GitHub repository.
Connect your repository to Render (or your chosen service) and follow their deployment instructions.
Conclusion
This application provides an interactive way to explore the statistical behavior of coin tosses. Feel free to modify and expand the application to suit your needs. If you encounter any issues or have suggestions for improvements, please open an issue or submit a pull request.

Happy coding!
