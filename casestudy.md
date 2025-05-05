# Case Study: Probability Game Analysis

## Introduction

... (Game description, etc.)

## Python Implementation

Here's the Python code used to simulate the game and calculate the probabilities and expected value. This code helps to verify the theoretical calculations.

```python
import math
import numpy as np
import pandas as pd

# Simulate drawing balls
def simulate_draws(num_simulations=10000):
    outcomes = ["R", "R", "R", "B", "B"]
    draws_per_trial = 4
    red_counts = []

    for _ in range(num_simulations):
        draw = np.random.choice(outcomes, size=draws_per_trial)
        red_count = np.count_nonzero(draw == "R")
        red_counts.append(red_count)
    return red_counts

# Calculate empirical probabilities
def empirical_probabilities(draw_counts):
    return pd.value_counts(draw_counts, normalize=True).sort_index()

# Calculate empirical expected value
def empirical_expected_value(draw_counts):
    return np.mean(draw_counts)

# Theoretical probabilities
def theoretical_probabilities(n, p, k_values):
    return [math.comb(n, k) * (p**k) * ((1-p)**(n-k)) for k in k_values]

# Game parameters
n_draws = 4
p_red = 3/5
possible_red_balls = range(n_draws + 1)  # [0, 1, 2, 3, 4]

# Run simulation
simulated_red_counts = simulate_draws()

# Analyze results
emp_probs = empirical_probabilities(simulated_red_counts)
emp_expected = empirical_expected_value(simulated_red_counts)
theoretical_probs = theoretical_probabilities(n_draws, p_red, possible_red_balls)

print("Empirical Probabilities:\n", emp_probs)
print("\nEmpirical Expected Value:\n", emp_expected)
print("\nTheoretical Probabilities:\n", dict(zip(possible_red_balls, theoretical_probs)))

# Expected value calculation (theoretical)
win_amount = 150
loss_amount = -10
prob_win = theoretical_probs[-1]  # Probability of 4 reds
expected_profit = (win_amount * prob_win) + (loss_amount * (1 - prob_win))

print(f"\nTheoretical Expected Profit: {expected_profit:.2f}")
