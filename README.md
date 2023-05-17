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

Our logistic regression model serves a dual purpose: to maximize prediction accuracy and provide actionable insights for NBA teams. Thus, we provide two versions of our model:

* Prediction-focused model: A logistic model with a LASSO penalty, optimized for prediction accuracy (achieved 71.22% accuracy).
* Inference-focused model: A standard logistic regression model, tailored to offer valuable insights (achieved 68.94% accuracy).