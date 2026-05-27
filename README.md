Portuguese Bank Marketing Campaign Prediction

## Problem Statement

The objective of this project is to predict whether a customer will subscribe to a term deposit based on demographic information, economic indicators, and previous marketing campaign interactions. The prediction can help financial institutions improve marketing efficiency by identifying customers with a higher likelihood of subscription.

## Objective

The primary objectives of this project are:

-To analyze customer and campaign-related data.
-To identify factors influencing term deposit subscriptions.
-To build and compare multiple machine learning classification models.
-To determine the most effective model for predicting customer subscription behavior.
-To derive actionable business insights using feature importance analysis.
-Dataset Description

The dataset contains information related to direct marketing campaigns conducted by a Portuguese banking institution.

Target Variable

y

yes → Customer subscribed to a term deposit.
no → Customer did not subscribe to a term deposit.

Feature Categories

-Customer Demographics
-Economic Indicators
-Previous Campaign Information
-Contact Information
-Loan and Housing Information

## Initial Data Inspection

The dataset was initially inspected to understand its structure and quality.

Inspection Activities:

-Checked dataset dimensions.
-Reviewed feature names and data types.
-Examined summary statistics.
-Identified missing values.
-Checked duplicate records.
-Analyzed target variable distribution.

Observations:

-The dataset contains both numerical and categorical features.
-No significant missing values were observed.
-Duplicate records were identified and removed.
-The target variable was imbalanced, with significantly more "no" responses than "yes" responses.

## Exploratory Data Analysis (EDA)

EDA was performed to understand feature distributions, detect anomalies, and identify patterns related to customer subscription behavior.

Numerical Feature Analysis

Histograms were generated for all numerical variables to understand their distributions.

Observations :

-Age distribution was slightly right-skewed, with most customers between 30 and 45 years.
-Duration exhibited a highly positively skewed distribution, indicating that most marketing calls were relatively short.
-Campaign-related features contained extreme values, suggesting the presence of outliers.
-The pdays feature contained a large concentration of values indicating customers who had not been previously contacted.
Outlier Analysis

Box plots were generated for all numerical variables.

Observations :

-Outliers were present in several variables including age, duration, campaign, and previous.
-Most outliers appeared to represent legitimate business observations rather than data entry errors.
-Therefore, no aggressive outlier treatment was applied.

Categorical Feature Analysis

Count plots were generated for categorical features against the target variable.

Observations :

-Cellular contact methods resulted in more successful subscriptions compared to telephone contacts.
-Customers with successful previous campaign outcomes were more likely to subscribe again.
-Subscription behavior varied across different months, indicating possible seasonal patterns.
-Students and retired customers appeared to have relatively higher subscription tendencies.

Correlation Analysis

A correlation heatmap was generated to analyze relationships among numerical features.

Observations:

-Strong positive correlations were observed among economic indicators such as emp.var.rate, euribor3m, and nr.employed.
-Previous campaign variables showed relationships with customer response behavior.
-No severe multicollinearity issues were identified that would significantly affect model performance.

## Data Preprocessing

Several preprocessing steps were applied before model development.

Encoding Categorical Variables

One-Hot Encoding was applied using pandas get_dummies().

Justification:

Most categorical variables in the dataset are nominal and do not possess an inherent order. One-Hot Encoding preserves categorical information while avoiding incorrect ordinal relationships.

## Train-Test Split

The dataset was divided into training and testing subsets.

Configuration:

Training Set: 80%
Testing Set: 20%

This ensures that model performance is evaluated on previously unseen data.

Feature Scaling

StandardScaler was applied to numerical features.

Justification

Feature scaling was performed because algorithms such as Logistic Regression and KNN are sensitive to feature magnitudes. Standardization helps improve convergence and ensures that all features contribute equally during model training.

## Model Building

Multiple machine learning algorithms were implemented and evaluated.

Logistic Regression:

Logistic Regression was used as the baseline classification model.

Observations:

-Achieved strong overall accuracy.
-Demonstrated stable performance.
-Struggled to identify the minority subscription class due to dataset imbalance.

K-Nearest Neighbors (KNN):

Observations :

-Performance was lower than Logistic Regression.
-Minority class detection remained weak.
-Performance was likely affected by dataset imbalance and high dimensionality resulting from one-hot encoding.

Decision Tree:

Decision Tree was implemented to capture non-linear relationships between variables.

Observations :

-Improved recall for subscription customers.
-Demonstrated better identification of minority-class observations.
-Showed signs of overfitting before hyperparameter tuning.

Decision Tree Hyperparameter Tuning:

The following parameters were tuned:

max_depth
min_samples_split
min_samples_leaf

Observations :

-A shallow tree achieved the highest recall.
-Hyperparameter tuning improved model generalization.
-Tuned Decision Tree achieved the highest recall among all evaluated models.

Random Forest:

Random Forest was implemented as an ensemble learning method.

Observations :

-Improved overall stability and accuracy.
-Reduced overfitting compared to a single Decision Tree.
-Produced balanced performance across classes.

Random Forest Hyperparameter Tuning:

Hyperparameter tuning was performed using different values of:

n_estimators
max_depth

Observations:

-Increasing tree depth improved recall.
-Performance gains remained limited due to class imbalance.
-Tuned Random Forest did not outperform the tuned Decision Tree.

XGBoost:

XGBoost was implemented as a gradient boosting model.

Observations :

-Achieved the highest overall accuracy.
-Maintained a strong balance between precision and recall.
-Demonstrated superior generalization compared to other models.

Model Comparison :

Multiple machine learning models were compared using Accuracy, Recall, and F1-Score.

Key Findings
Logistic Regression provided a strong baseline.
KNN produced the weakest performance.
Tuned Decision Tree achieved the highest recall for identifying subscription customers.
XGBoost achieved the highest overall accuracy and balanced performance.

		 Model  Accuracy  Recall  F1-Score
0  Logistic Regression    0.9056    0.41      0.50
1                  KNN    0.8925    0.32      0.41
2        Decision Tree    0.8888    0.54      0.53
3  Tuned Decision Tree    0.9027    0.59      0.59
4        Random Forest    0.9089    0.46      0.55
5              XGBoost    0.9128    0.54      0.59

Feature Importance Analysis

Feature importance analysis was performed using XGBoost.

Top Influential Features
nr.employed
2. poutcome_success
3. duration
4. month_oct
5. cons.conf.idx
6. emp.var.rate

## Business Insights

-Economic indicators significantly influence subscription decisions.
-Previous campaign success strongly impacts future customer responses.
-Call duration is an important predictor of subscription likelihood.
-Seasonal campaign timing affects customer behavior.


## Conclusion

The objective of this project was to predict customer subscription behavior for term deposits using machine learning techniques.

Several classification models were evaluated, including Logistic Regression, KNN, Decision Tree, Random Forest, and XGBoost.

Among all evaluated models, XGBoost achieved the highest overall accuracy of approximately 91.28%, demonstrating strong predictive capability and balanced classification performance. The tuned Decision Tree achieved the highest recall for identifying potential subscribers, making it particularly useful when maximizing customer identification is the primary business objective.

Feature importance analysis revealed that economic indicators, previous campaign success, and call duration were among the most influential factors affecting subscription decisions.

The developed models can support banks in improving marketing efficiency by focusing resources on customers with a higher probability of subscription.

## Challenges Faced

-Handling class imbalance in the target variable.
-Selecting appropriate evaluation metrics beyond accuracy.
-Optimizing model performance through hyperparameter tuning.
-Managing high-dimensional data after One-Hot Encoding.
-Balancing recall and precision for the minority class.
