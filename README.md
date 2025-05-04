# Portfolio Part 5: Predicting Australian Vehicle Prices

## Description
This project focuses on predicting the price of cars in the Australian market based on vehicle features. The dataset contains over 16,000 records collected in 2023 from online platforms. The goal is to explore the data, clean it, engineer useful features, and evaluate multiple regression models.

## Table of Contents
- [Dataset](#dataset)
- [Objective](#objective)
- [Data Features](#data-features)
- [Methodology](#methodology)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Feature Engineering](#feature-engineering)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Results](#results)
- [Conclusion](#conclusion)
- [Future Work](#future-work)

## Dataset
- **Source**: Australian Vehicle Prices dataset (2023)
- **Size**: 16,734 records × 19 features
- **Context**: Real-world car listing information scraped from Australian vehicle marketplaces

## Objective
To build regression models that can predict the price of a car based on selected features like:
- Year
- Fuel Consumption
- Engine Size (Displacement)
- Odometer (Kilometres)
- Transmission, Fuel Type, etc.

The project also compares several regression techniques, including:
- Linear Regression
- Decision Tree Regressor
- Multi-layer Perceptron (MLP)
- Random Forest Regressor

## Data Features
Key features used:
- `Year`: Year of manufacture
- `Transmission`: Manual or Automatic
- `FuelConsumption`: L/100km
- `Kilometres`: Distance travelled
- `Displacement`: Engine size in litres
- `FuelType`, `DriveType`, `BodyType`, `Doors`, `Seats`
- `Price`: Target variable

## Methodology
1. **Data Cleaning**: Remove nulls, inconsistent values, and parse strings into numeric values.
2. **Feature Engineering**:
   - Frequency encoding for categorical columns
   - Extracted numeric values from strings (e.g., “5.6 L / 100 km” → 5.6)
3. **EDA**: Visualised distribution of car sales by state, year vs price trends, and correlation matrix.
4. **Feature Selection**: Chose top 5 most correlated predictors with price.
5. **Train/Test Split**: 80% training, 20% testing.

## Exploratory Data Analysis (EDA)
- Majority of listings are from NSW
- Newer cars trend towards higher prices
- Kilometres (used cars) negatively correlated with price
- Strong correlation observed between:
  - Year and Price (positive)
  - Kilometres and Price (negative)
  - Displacement and Price (positive)

## Feature Engineering
- Removed irrelevant columns: `Title`, `ColourExtInt`, `Model`, `Car/Suv`
- Converted fuel consumption, engine data, doors/seats to numeric
- Encoded categorical variables using frequency encoding
- Imputed missing values using mean for numeric, dropped rows with remaining missing values

## Model Training and Evaluation

### Linear Regression
- **R² Score (Train/Test)**: 0.35 / 0.37
- Underfitting observed, unable to capture data complexity.

### Decision Tree Regressor (max_depth=2)
- **R² Score (Train/Test)**: 0.31 / 0.15
- Extremely simple tree, resulted in poor performance.

### Multi-layer Perceptron (MLP)
- **R² Score (Train/Test)**: 0.16 / 0.17
- Non-linear model with hidden layers (100, 100) failed to capture patterns.

### Random Forest Regressor
- **R² Score (Train/Test)**: 0.94 / 0.68
- Best performer but some overfitting. Very low MSE on training, good generalisation.

## Results
```text
Model               | Train R² | Test R² | Test RMSE
--------------------|----------|---------|-----------
Linear Regression   | 0.35     | 0.37    | 23,788
Decision Tree       | 0.31     | 0.15    | 27,744
MLP Regressor       | 0.16     | 0.17    | 27,270
Random Forest       | 0.94     | 0.68    | 17,127
