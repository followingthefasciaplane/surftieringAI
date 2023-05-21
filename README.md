# Surf Map Tiering AI

## Overview

This is an idea to develop an Artificial Intelligence model to objectively rank the difficulty of surf maps in Source engine games. Surf map difficulty rankings are currently determined subjectively by players, leading to inconsistent tiering, and what is known as "tier-deflation". 

## Objectives

The main objective of this is to create an AI model that takes gameplay data as input, and outputs an objective difficulty ranking for each surf map.

The gameplay data I have considered potentially useful include the following parameters:

1. Average time spent in-zone and the number of failed attempts before successful completion.
2. The number of players who completed the map in relation to its release date.
3. The average number of completions by players who have completed the map multiple times.
4. The average skill level of players completing the map, gauged by the number of more difficult maps they have completed prior.
5. A calculation based on the fastest and slowest completion times, with the hypothesis that the error margin is smaller on more difficult maps (potentially unreliable, many factors and inconsistent between maps).
6. Average amount of players who gave up on completing the map (eg. over x time in zone and over y attempts without achieving a completion).
7. Average skill level of players who gave up on completing the map.
8. Comparison of this map data with other maps or benchmark maps.

## Approach

The approach for this idea would be data-driven and I have drafted some steps for a potential approach outlined below:

**Data Collection:** Gather gameplay data, potentially through an API, web scraping, or custom scripts. User privacy should be taken into account during this process.

**Data Quality Assessment:** Ensure that the collected data is precise, accurate, and of high quality to train the model effectively.

**Feature Engineering:** Transform the collected parameters into a form that can be effectively used by a machine learning model. Additional factors, like the number of unique paths to complete the map or the variance in completion times, might also be considered.

**Model Selection:** Choose an appropriate machine learning model for the task. As the target variable (tier / difficulty) is continuous, a regression model will be the initial focus. Potential models include linear regression, support vector regression, random forests, or even neural networks.

**Evaluation:** Evaluate the model using metrics like Mean Absolute Error (MAE), Mean Squared Error (MSE), or Root Mean Squared Error (RMSE).

**Iterative Refinement:** Revisit feature engineering, model selection, and evaluation steps as needed to refine the model based on its performance.

## Potential Models

Assuming that difficulty is a numerical linear score between 0 and 1, there could be certain scoring thresholds (eg. difficulty 0.854 output from model could be T7, which could assigned for scores within the 0.8-0.9 range).
Here are some potential models that could be useful:

**Lienar Regression:** Linear regression is a simple and commonly used model for predicting a continuous output variable. It can be a good starting point to establish a baseline performance for the problem.

**Support Vector Regression:** SVR is a version of Support Vector Machine, a powerful, flexible machine learning algorithm, adapted for regression problems. SVR can model non-linear relationships, which could be beneficial since the difficulty level is influenced by complex interactions between different features.

**Random Forest Regression:** This is a more robust and sophisticated model that can capture non-linear relationships and interactions between features without requiring a lot of hyperparameter tuning. Random forest regression can also handle overfitting well and provide feature importance, which could give insights into which parameters most strongly predict difficulty.

**Gradient Boosting Regression (eg. XGBoost, LightGBM):** These are advanced, highly accurate models that build many decision trees in a sequence, each trying to correct the mistakes of the previous one. They often top Kaggle competitions but may require more careful tuning and have higher computational cost.

**Neural Networks (e.g., MLP, CNN, RNN, or Transformer-based models):** Neural networks can model very complex functions and capture intricate patterns in data. They have been highly successful in many areas of AI. However, they require large amounts of data and computational resources, and can be tricky to optimize due to many hyperparameters. This one is probably less practical.

It may be a good idea to start simple and progressively increase complexity, using multiple models and benchmarking their performance against each other. Data should also be split into training and validation (and possibly test) sets to assess the model's performance on unseen data and prevent overfitting. This could be done with certain benchmark maps (eg. surf_666 could be a benchmark for Tier 6).

Let me know if you have any ideas.
