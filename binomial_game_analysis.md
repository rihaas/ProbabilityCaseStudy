# Case Study: Probability Game Analysis

## Introduction

This case study analyzes a probability game involving drawing balls from a bag with replacement. We will examine the likelihood of different outcomes and determine the expected profitability of the game.

## Game Description

A bag contains 3 Red balls and 2 Blue balls. [cite: 1, 2, 3]

The rules of the game are as follows:

* You pick a ball, write down its color, and put it back in the bag. This is done 4 times in total. [cite: 2, 3]
* If all 4 times the Red balls are drawn, you win Rs 150. [cite: 3]
* Otherwise, you lose Rs 10. [cite: 3]

## Question

Would engaging in this game result in a profit or a loss for you? [cite: 3]

## Problem Breakdown

* The problem states that once you've noted the color, you put the ball back in the bag. [cite: 4]
    * What does this mean in probability terms? [cite: 4]
    * It means that the balls are drawn with replacement. [cite: 5]
* The step of taking out the ball is repeated 4 times. [cite: 5]

## Defining the Random Variable

Whether you end up gaining or losing will depend on how many red balls are drawn. [cite: 5, 6]

Therefore, let's define a random variable X to denote the number of red balls drawn in 4 trials. [cite: 6]

* X is a discrete random variable. [cite: 7]
* Possible outcomes for X: 0, 1, 2, 3, or 4 [cite: 7]

## Theoretical Approach: Compute Probability Using Rules

* What is the probability of 1 red ball in 1 pick? [cite: 39, 40]
    * P(Red) = 3/5 [cite: 40]
* What is the probability of 1 blue ball in 1 pick? [cite: 40, 41]
    * P(Blue) = 2/5 [cite: 41]
* What is the probability of 2 red balls in 2 picks? [cite: 41, 42]
    * P(Red, Red) = (3/5) \* (3/5) [cite: 42]
* What is the probability of 1 red ball in the first pick and 1 blue ball in the second? [cite: 42, 43]
    * P(Red, Blue) = (3/5) \* (2/5) [cite: 43]
* What is the probability of 1 blue ball in the first pick and 1 red ball in the second? [cite: 43]
    * P(Blue, Red) = (2/5) \* (3/5)  
* Probability of other combinations (from notebook):
    * P(Red, Red, Red, Blue) = (3/5)(3/5)(3/5)(2/5)
    * P(Blue, Blue, Blue, Blue) = (2/5)(2/5)(2/5)(2/5)

## Probability of Obtaining 1 Red Ball (X=1) [cite: 45, 46, 47]

For X = 1, we have 4 possible cases:

* BBBR
* BBRB
* BRBB
* RBBB

The probability of each case is (2/5)³ \* (3/5)¹.

Therefore, P(X=1) = 4 \* (2/5)³ \* (3/5)¹

## Probability of Getting 2 Red Balls (X=2) [cite: 47, 48]

There are 6 possible orientations for X=2. [cite: 48, 49]

The probability of each orientation is (2/5)² \* (3/5)². [cite: 50]

Therefore, P(X=2) = 6 \* (2/5)² \* (3/5)²

## General Expression (Binomial Distribution) [cite: 51, 52, 53]

We can generalize this as:

P(X=k) = ⁴Cₖ \* (3/5)ᵏ \* (2/5)⁴⁻ᵏ

Where ⁴Cₖ is the binomial coefficient (math.comb(4, k) in Python). [cite: 53, 54]

Using this, we can calculate probabilities for all X values:

* P(X=0) = ⁴C₀ \* (3/5)⁰ \* (2/5)⁴
* P(X=1) = ⁴C₁ \* (3/5)¹ \* (2/5)³
* P(X=2) = ⁴C₂ \* (3/5)² \* (2/5)²
* P(X=3) = ⁴C₃ \* (3/5)³ \* (2/5)¹
* P(X=4) = ⁴C₄ \* (3/5)⁴ \* (2/5)⁰

## Verification with Code (Theoretical Probabilities) [cite: 54, 55, 56, 57]

The notebook uses `math.comb()` to calculate the binomial coefficients. The calculated probabilities are:

* P(X=0) ≈ 0.0256
* P(X=1) ≈ 0.1536
* P(X=2) ≈ 0.3456
* P(X=3) ≈ 0.3456
* P(X=4) ≈ 0.1296

These values are very close to the empirical probabilities obtained through simulations. [cite: 57, 58]

## Expected Value Calculation (Theoretical)

To determine if the game is profitable, we calculate the expected value:

E(Profit) = (Profit for 4 Reds \* P(X=4)) + (Loss for other outcomes \* P(X<4))

E(Profit) = (150 \* 0.1296) + (-10 \* (1 - 0.1296))

E(Profit) = 19.44 - 8.704

E(Profit) ≈ 10.74

## Conclusion (Theoretical)

The expected profit is approximately Rs 10.74. Therefore, based on the theoretical analysis, playing this game is expected to be profitable in the long run.

## Empirical Approach (From Notebook)

The notebook also demonstrates an empirical approach using Python simulations with `numpy.random.choice()` to estimate the probabilities. It simulates the ball draws 10,000 times and calculates the average number of red balls drawn.

* This approach calculates the empirical probability by simulating the experiment many times. [cite: 13]
* The empirical expected value is calculated as the weighted average of the number of red balls drawn in each simulation. [cite: 25, 26, 27, 28, 29, 30]

## Comparison of Empirical and Theoretical Results [cite: 57, 58, 59]

The empirical probabilities obtained from the simulations are close to the theoretical probabilities, especially with a large number of simulations (10,000). [cite: 57, 58] This validates the theoretical calculations.

## Key Takeaways

* **Theoretical Probability:** Calculated using mathematical rules and formulas.
* **Empirical Probability:** Estimated from observations and experiments.
* The binomial distribution is a useful tool for analyzing events with a fixed number of independent trials and two possible outcomes. [cite: 61, 62, 63, 64]

## Conditions of Binomial Experiment

The notebook outlines the conditions for a binomial experiment:

* Fixed number of trials (n)
* Each trial is independent.
* Each trial has two outcomes: Success or Failure.
* The probability of success (p) is the same for each trial.
