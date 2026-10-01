# Project Decisions

## 1. Dataset

I used a student placement dataset containing academic performance, educational background, work experience, and placement status.

The target variable is `status`, which contains:
- `Placed`
- `Not Placed`

## 2. Features Excluded

### `sl_no`

`sl_no` was excluded because it is only a serial number and does not represent a meaningful characteristic of a student.

### `salary`

`salary` was excluded because it is only available for students who were placed.

Using salary as an input feature would cause target leakage because salary is information related to the placement outcome.

## 3. Data Preprocessing

The target variable was converted into numerical values:

- `Placed` → 1
- `Not Placed` → 0

Numerical and categorical features were handled separately.

Categorical features were converted into numerical features using `OneHotEncoder`.

The encoder was fitted only on the training data and then used to transform the test data.

## 4. Train-Test Split

The dataset was divided into:

- 80% training data
- 20% testing data

A fixed `random_state=42` was used so that the results could be reproduced.

Stratification was used to maintain the class distribution in the training and testing sets.

## 5. Models Tested

Two classification models were compared:

1. Logistic Regression
2. Decision Tree

The Decision Tree was limited to `max_depth=4` to control its complexity.

## 6. Meaningful Change

During feature selection, `salary` was considered as a possible feature but was removed after identifying that it could cause target leakage.

This was important because the model should make predictions using information available before the placement outcome, rather than information that is already associated with the outcome.

## 7. Evaluation

The models were evaluated using:

- Precision
- Recall
- F1 Score

An example prediction was also checked against its actual value to demonstrate how an individual prediction can be incorrect even when the overall model metrics are reasonably strong.

## 8. Feature Importance

Decision Tree feature importance was examined to understand which features contributed most to the tree's decisions.

The feature importance values were treated as model-specific indicators and not as proof that a feature causes placement.
