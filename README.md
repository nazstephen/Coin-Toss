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
