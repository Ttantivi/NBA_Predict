# NBA_Predict

This project was done in Collaboration with Jeffrey Kuo, jrkuo2015 [at] berkeley [dot] edu

To view detailed derivation of methods, please read Mtehod_Details.pdf

## Introduction

This repository houses the predictive models we've created for predicting win/loss outcomes of NBA regular seasons. The current focus is on the latest 2022-2023 season, where we employ historical team performance data, home field advantage and additional factors to inform our predictions.

Instructions: 
* Run NBA_Predict_Models.Rmd to create design matrix csv
* Models are contained in NBA_Predict_Models.rmd

## Motivation

With an emphasis on interpretability over complexity, we chose to utilize linear models as our primary tool for this task, starting with data from the 2012 season onward. The implications of such analysis are far reaching for NBA teams. The insights can affect decisions related to player acquisition and coaching strategies, potentially altering a team's revenues by hundreds of millions of dollars each year.

## Data

The data employed in this project is sourced from the nbastatR package. This comprehensive package includes data for every NBA game played in a particular season, covering various facets such as player performance (e.g., total points, minutes played) and home field advantage, among other factors. For this specific analysis, we leveraged the past 10 seasons of data, with the 2022 season alone contributing 26039 rows of observations.

## Models and Results

# Modeling Probability of Home Team Winning vs. Away Team

This repository focuses on modeling the probability of the Home Team winning versus the Away Team based on available data. Our aim is to predict the outcome of a game using a binary function and understand the underlying factors contributing to the predicted probability.

## Probability Estimation

We seek to estimate the probability using the equation:

![equation](https://latex.codecogs.com/png.latex?\Prob%28%5Ctext%7BHome%20Team%20wins%20vs.%20Away%20Team%7D%7C%20%5Ctext%7Bdata%7D%20%29%20%3D%20%5Chat%7Bp%7D)

where ![equation](https://latex.codecogs.com/png.latex?0%20%5Cleq%20%5Chat%7Bp%7D%20%5Cleq%201). However, the initial equation provided is invalid and needs further correction.

## Predicted Outcome

The predicted outcome of the game is determined by a binary function:

![equation](https://latex.codecogs.com/png.latex?%5Chat%7By%7D%20%3D%20%5Cbegin%7Bcases%7D%20%5Ctext%7BHome%20Team%20wins%7D%20%26%20%5Chat%7Bp%7D_i%20%5Cgeq%200.5%20%5C%5C%20%5Ctext%7BAway%20Team%20wins%7D%20%26%20%5Chat%7Bp%7D_i%20%3C%200.5.%20%5Cend%7Bcases%7D)

## Data and Features

To calculate the probability, we utilize data from the 2012 season up to the prediction day. For instance, when predicting the winners of teams playing on 12/12/2022, the training data includes all games from 2012 to 12/11/2022. Our covariates are constructed as the home team's average stats over their last 10 games minus the away team's average stats over their last 10 games. The following stats are used: total rebounds, steals, blocks, turnovers, offensive rating, defensive rating, true shooting, and win rate. To account for the pace of the game, all stats except true shooting and win rate are adjusted on a per 100 possessions basis.

## Dual-Model Approach

We initially aimed for a single model that excelled in both prediction accuracy and inferential capability. However, we discovered a trade-off between the two objectives. A model with excellent prediction accuracy suffered from multi-collinearity, impairing its inferential abilities. Therefore, we implemented a dual-model approach:

1. Logistic Regression with LASSO Penalty: Emphasizes prediction accuracy.
2. Regular Logistic Regression: Focuses on extracting meaningful insights.

This approach enables us to achieve our objectives using separate, specialized models.

## Back-to-Back Games

We include a covariate to indicate the relative difference between each team in terms of whether the current game is a back-to-back (consecutive game). The covariate takes the following values:
- 1: Current game is a back-to-back for the home team only.
- 0: Current game is a back-to-back for both teams or for neither team.
- -1: Current game is a back-to-back for the away team only.

For additional details on the model and its implications, refer to Section 3.

Please note that this is a simplified

Our logistic regression model serves a dual purpose: to maximize prediction accuracy and provide actionable insights for NBA teams. Thus, we provide two versions of our model:

* Prediction-focused model: A logistic model with a LASSO penalty, optimized for prediction accuracy (achieved 71.22% accuracy).
* Precision: 0.7428
* Recall: 0.7689
![Confusion Matrix](./Images/heatmap_lasso.png)
![Model Performance Over time](./Images/lasso_plot.png)

* Inference-focused model: A standard logistic regression model, tailored to offer valuable insights (achieved 68.94% accuracy).
![Summary table](./Images/Logistic_Summary.png)