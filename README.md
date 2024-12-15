# NYC Taxi Fare Prediction


View notebook file: https://colab.research.google.com/drive/195FYF83DS3D_GxO2flHYuE2OkTU5X8bI?usp=sharing

## Project Overview
This project aims to predict taxi fares in New York City using machine learning techniques. The NYC Taxi Fare Prediction Dataset, consisting of over 55 million trip records from 2009 to 2015, was used to build and evaluate a neural network model. The dataset includes essential features such as pickup and drop-off coordinates, timestamps, and fare amounts, making it ideal for analyzing urban transportation patterns and implementing predictive models.

## Table of Contents
1. [Introduction](#introduction)
2. [Dataset](#dataset)
3. [Data Preprocessing](#data-preprocessing)
4. [Feature Engineering](#feature-engineering)
5. [Methodology](#methodology)
6. [Experiments and Evaluation](#experiments-and-evaluation)
7. [Visualizations and Insights](#visualizations-and-insights)


## Introduction
This project explores spatial and temporal factors influencing NYC taxi fares and implements a neural network to predict fare amounts. The findings provide actionable insights for improving ride-hailing services, such as optimizing driver allocation, pricing strategies, and better service distribution across boroughs.

## Dataset
- **Source**: [Kaggle: NYC Taxi Fare Prediction Dataset](https://www.kaggle.com/competitions/new-york-city-taxi-fare-prediction)
- **Features**:
  - `pickup_datetime`: Date and time of the trip start.
  - `pickup_longitude` & `pickup_latitude`: Pickup location coordinates.
  - `dropoff_longitude` & `dropoff_latitude`: Drop-off location coordinates.
  - `fare_amount`: Target variable for prediction.
  - `passenger_count`: Number of passengers for the trip.

## Data Preprocessing
- Removed rows with missing or invalid data.
- Filtered trips outside NYC's geographical boundaries (latitude: 40.49–40.92, longitude: -74.27–-73.68).
- Removed outliers (e.g., fares below $2 or above $1000).
- Extracted time-based features from `pickup_datetime` (hour, day, weekday, month).
- Normalized numerical features (e.g., coordinates and distances) for better model convergence.

## Feature Engineering
- **Trip Distance**: Calculated using the Haversine formula based on pickup and drop-off coordinates.
- **Geospatial Clustering**: Applied K-means clustering to group pickup and drop-off locations into 20 clusters, representing different regions in NYC.
- **Peak Hour Indicator**: Flagged trips during peak hours (6–9 AM and 4–7 PM) based on NYC Transit guidelines.

## Methodology
### Model Architecture
- **Model**: Neural Network built using TensorFlow.
- **Architecture**:
  - Input Layer: Processed features such as `trip_distance`, clusters, and time-based features.
  - Three Hidden Layers: Dense layers with 128, 64, and 32 neurons, each using the ReLU activation function.
  - Output Layer: Single neuron for regression output (predicting fare amounts).
- **Optimizer**: Adam optimizer with a learning rate of 0.001.
- **Loss Function**: Mean Absolute Error (MAE).

### Optimization Strategy
- Batch sizes of 32, 64, and 128 were tested, with 64 providing the best balance between training efficiency and performance.
- Early stopping was employed to monitor validation loss and prevent overfitting.
- The model converged around **epoch 37**, demonstrating effective learning.

### Training Process
- Training data was split into 80% training and 20% validation sets.
- Validation MAE was monitored throughout the training process to ensure the model generalizes well to unseen data.

## Experiments and Evaluation
### Validation Performance
- The validation MAE stabilized at approximately **2.003**, meaning the model predictions were within $2 of actual fare amounts on average.
- Residual analysis showed that fares generally increased with trip distance, consistent with real-world expectations.

### Test Dataset Predictions
- The test dataset lacked actual fare values, so predictions were analyzed for logical consistency.
- The predicted fare distribution aligned well with the training data for short and medium trips. However, some deviations were observed for longer trips, which were underpredicted.

### Error Analysis
- Long-distance trips were underpredicted, likely due to missing features such as toll fees or airport flags.
- Temporal analysis showed higher fares during early mornings (4–5 AM), correlated with longer average trip distances.

## Visualizations and Insights
1. **Geospatial Analysis**:
   - Pickup and drop-off locations were concentrated in Manhattan.
   - Sparse activity was observed in Staten Island.
2. **Temporal Analysis**:
   - Peak taxi demand occurred during morning (6–9 AM) and evening rush hours (5–7 PM).
   - The highest average fares were during early mornings (4–5 AM), explained by longer average trip distances.
3. **Trip Distance vs. Fare**:
   - A positive correlation between trip distance and fare amount was observed, validating the model’s predictions.

