# Predict Calorie Expenditure - Kaggle Playground Series S5E5

This repository contains the code and documentation for my solution to the [Kaggle Playground Series - Season 5, Episode 5](https://www.kaggle.com/competitions/playground-series-s5e5) competition. The goal was to predict calorie expenditure during exercise based on features such as `Sex`, `Age`, `Height`, `Weight`, `Duration`, `Heart_Rate`, and `Body_Temp`. My approach achieved a **top 18% ranking** (771 out of 4316 participants) on the leaderboard.

---

## Table of Contents
- [Approach](#approach)
  - [Data Preprocessing](#data-preprocessing)
  - [Feature Engineering](#feature-engineering)
  - [Data Visualization](#data-visualization)
  - [Model Selection and Training](#model-selection-and-training)
  - [Evaluation](#evaluation)
- [Results](#results)
- [Usage](#usage)
- [Dependencies](#dependencies)

---

## Approach

### Data Preprocessing
The initial step involved preparing the raw data for modeling:
- **Mapping Categorical Variables:** Converted the `Sex` column to numerical values (`male: 1`, `female: 0`) to ensure compatibility with machine learning algorithms.
- **Handling Duplicates:** Removed duplicates across all feature columns in the training set. For each unique combination of features, retained the minimum `Calories` value to maintain consistency and avoid overestimation.

### Feature Engineering
Feature engineering played a critical role in improving model performance. The following features were added:
- **BMI:** Calculated as `Weight / (Height / 100)^2` to capture body composition.
- **Exercise Intensity:** Derived as `Heart_Rate / Duration` to reflect the intensity of the workout.
- **Body Surface Area (BSA):** Computed using the formula `0.007184 * (Height^0.725) * (Weight^0.425)` to estimate physiological surface area.
- **Metabolic Age:** Adjusted as `Age * (BMI / 25)` to account for age and body composition effects.
- **Height-Weight Ratio:** Added as `Height / Weight` to explore the relationship between height and weight.
- **Temperature Deviation:** Calculated as `Body_Temp - 37` to measure deviation from normal body temperature.
- **Interaction Features:** Created interactions between `Duration`, `Heart_Rate`, and `Body_Temp` with `Sex` to capture gender-specific effects (e.g., `Duration_x_Sex`).
- **Grouped Features:** Generated features like `HR_Dur_[duration]` and `Temp_Age_[age]` for each unique `Duration` and `Age` value, encoding specific effects of heart rate and body temperature.

### Data Visualization
Exploratory visualizations were used to validate the approach:
- **Correlation Heatmap:** Visualized correlations between features to identify strong relationships and potential multicollinearity, guiding feature selection.
- **Histogram of Each Feature:** Plotted distributions of individual features (e.g., `Age`, `Height`, `Weight`) to assess their spread, skewness, and potential need for transformation.
- **Violin Plot:** Illustrated the distribution and density of features across `Sex` or other categorical variables, highlighting variations in feature behavior.
- **KMeans 3D PCA Projection:** Applied PCA to reduce dimensionality and visualized KMeans clustering in 3D to explore natural groupings in the data.
- **Histograms of OOF Predictions:** Plotted out-of-fold (OOF) predictions from CatBoost and XGBoost models to analyze the distribution of predicted calorie expenditures and ensure alignment with the target variable.
- - [Histograms of OOF Predictions](https://github.com/LutherYTT/Kaggle-Playground-Series-Season-5-Ep.5-Predict-Calorie-Expenditure/blob/main/assets/Histograms%20of%20OOF%20Predictions.png)

### Model Selection and Training
The solution leveraged an ensemble approach:
- **Models Used:** Combined CatBoost and XGBoost regressors, chosen for their ability to handle structured data and model complex interactions effectively.
- **Cross-Validation:** Employed K-Fold cross-validation to ensure robust performance estimation and mitigate overfitting.
- **Training Process:** Trained both models on the engineered feature set, then blended their predictions to enhance accuracy and generalization.

### Evaluation
Model performance was assessed as follows:
- **Metric:** Used Root Mean Squared Log Error (RMSLE), the competition's evaluation metric, to measure prediction accuracy.
- **Out-of-Fold Predictions:** Computed OOF predictions to evaluate model performance on unseen data during cross-validation.
- **Ensemble Benefit:** The ensemble of CatBoost and XGBoost outperformed individual models, achieving a lower RMSLE and better leaderboard ranking.

---

## Results
- **Final Ranking:** Top 18% (771/4316) on the Kaggle leaderboard.
- **Key Insights:** Feature engineering, particularly the inclusion of physiological metrics (e.g., BMI, BSA) and interaction terms, significantly boosted model performance. The ensemble approach further enhanced generalization.

---

## Usage
To reproduce or explore the solution:
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/predict-calorie-expenditure-s5e5.git
   ```
2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the Notebook:**
   Open `PS_S5E5_Predict_Calorie_Expenditure_(CatBoost_+_XGBoost_+_Feature_Engineering).ipynb` in Jupyter Notebook or Google Colab and execute the cells sequentially.

---

## Dependencies
- Python 3.11
- pandas
- numpy
- matplotlib
- scikit-learn
- catboost
- xgboost

---
