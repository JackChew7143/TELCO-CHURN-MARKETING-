# TELCO-CHURN-MARKETING-
As this project will follow CRISP-DM methodology, the researcher will demonstrate how predictive analytics for business problems in customer retention will start and progress from business understanding until the last phases of deployment 
It covers:

4.1.1 STAGE 1: BUSINESS UNDERSTANDING

In this stage, researchers aim to understand the telecommunications business context, customer needs, and requirements for predictive analytics. The business objective is to identify at-risk customers for churn early, enabling proactive retention measures. Key stakeholders include the marketing department, customer support, technical department, and executive leadership. Churn, defined as customer cancellations, impacts revenue and reflects internal service issues. Success criteria include reducing churn, uncovering insights, and achieving a classification model with over 80% accuracy and unbiased results.

4.1.2 STAGE 2: DATA UNDERSTANDING AND STAGE 3: DATA PREPARATION

These phases, though distinct, may overlap. The dataset, retrieved from IBM Business Analytics, focuses on analyzing customer behavior for predicting churn. It consists of 7043 entries covering demographics, location, services, and status. Data exploration reveals columns with integer data types, indicating a classification problem. Data integration involves merging datasets using the merge function. Data preparation includes cleaning to ensure consistency, accuracy, and relevance.

4.1.2.1 DATA UNDERSTANDING: DATA EXPLORATION

The dataset includes demographics, location, services, and status. Most columns are integers, and the target variable, churn value, is categorical. It's identified as a classification problem.

4.1.2.2 DATA UNDERSTANDING: DATA INTEGRATION

Integration involves using the merge function to combine datasets through inner merge operations based on matched column values.

4.1.2.3 DATA PREPARATION: DATA PREPROCESSING & TRANSFORMATION

Data cleaning involves removing inconsistent, irrelevant data to enhance model performance. Missing values and duplicate values are addressed.

4.1.2.3.1 MISSING VALUES AND DUPLICATION VALUES

Missing values are checked and found to be absent, ensuring a complete dataset. Duplicate values are also checked and found to be non-existent, preventing potential issues with data consistency.

The summary provides a clear understanding of the business objectives, stakeholders, context, success criteria, and the intertwining nature of data understanding and preparation phases. It also outlines the key steps in data exploration, integration, and preparation, emphasizing the importance of addressing missing and duplicate values for a robust predictive model.
4.1.2.3.2 One Hot Encoding

Categorical data is converted to numerical values using one-hot encoding to avoid creating a false hierarchy or ordinal trend in the model. This method creates new columns for each unique value in the original column, eliminating the issue of ordinality.

4.1.2.3.4 Label Encoding

For categorical data with an inherent ordinal characteristic, like the "Contract" column, numerical values are directly assigned to represent the order (e.g., 0, 1, 2) without creating new columns.

4.1.2.3.5 Outlier Detection and Removal

Outliers can lead to misleading conclusions and biased models. The Z-Score method is applied to measure data point distances, classifying values above -3 or 3 as outliers. Eleven continuous columns undergo outlier detection, except for "Population," "Total Refunds," and "Total Extra Data Charges," where a percentile-based method is used due to skewed distributions.

4.1.2.3.6 Power Transformation

Power transformation, specifically Yeo-Johnson transform, is applied to normalize skewed data, scale variables to a common scale, and mitigate the impact of outliers. This process, combined with Z-Score outlier removal and percentile-based handling, effectively addresses and minimizes the impact of outliers.

The approach ensures data quality and prepares the dataset for further analysis, reducing sensitivity to extreme values and enhancing the model's robustness.
 
4.1.2.3.7 Multicollinearity Issue and Selected Important Features

Multicollinearity, where independent variables are highly correlated, can hinder model interpretation and reliability. The VIF (Variance Inflation Factor) method is employed to identify and address multicollinearity issues among 'Total Charges,' 'Total Extra Data Charges,' 'Total Long-Distance Charges,' and 'Total Revenue.' Removal of the redundant variable 'Total Revenue' mitigates multicollinearity, with VIF scores below 5 for the remaining variables.

Feature Selection (Backward Feature Elimination)

Backward feature elimination is used to select important features, starting with all features and iteratively removing the least important. This method, based on F1 score, ensures only relevant features are retained. Step 31 is chosen as it yields the highest avg_score while excluding seven features.

Pearson Correlation

Analysis reveals that 'Referred a Friend_Yes' is redundant, highly correlated with 'Number of Referrals' (correlation coefficient: 0.708). T-tests and Pearson correlation confirm the relationship, leading to the removal of 'Referred a Friend_Yes' as it provides no additional information.

T-test

Similarly, 'phone_service_yes' is redundant as it is closely related to 'Avg Monthly Long Distance Charges.' A T-test indicates a significant difference in mean charges between customers with and without phone service. Thus, 'phone_service_yes' is removed due to redundancy.

Chi-Squared Test

The Chi-squared test identifies the relationship between "Internet Service" and "Internet Type," confirming redundancy. The P-value is less than 0.05, indicating a non-random relationship. 'Internet Service' is removed as it can be explained by 'Internet Type.'

This streamlined approach addresses multicollinearity, ensures relevant feature selection, and eliminates redundant variables, enhancing the model's interpretability and performance.

4.1.3	STAGE 4: MODELLING
4.1.3.1		TRAIN-TEST-SPLIT
	The final dataset will be split into two sets which are training dataset and testing dataset. For training dataset will be used for model to train, and testing set will be used for model to evaluate the model performance on the unseen data, in other words how well the model in classifying churn and not churn given unseen data. Lastly stratified sampling will be applied to ensure that the class distribution (churn and no churn) are evenly distributed among training and testing dataset to minimize the issue of model biased toward certain class (imbalanced class).
 
4.1.3.2		OVERSAMPLING
	In real-world data, class imbalanced is a common issue where one of the classes is dominated over another class. In other words, instances of class churn is significantly fewer than instances of class not churn, that make minority class (churn) underrepresented compared to other as shown in below Figure. Ignore class imbalance issue can result model become biased as it may perform very well in majority class (not churn) but poor at classify instances belong to churn (minority class).
	Therefore, oversampling will be utilized to increase the instances of minority class, to enhance the representation of minority churn class in dataset. This approach can make the model to learn more about minority class such as underlying pattern or trend that may missed from the original dataset.

4.1.3.3 MODELLING PROCESS

After data processing and splitting into training and testing sets, the XGBoost classifier is chosen for churn prediction due to its effectiveness in classification tasks. The model is trained on the oversampled training dataset, while the testing dataset remains unaltered to assess real-world scenario performance.

For initial training, default XGBoost parameters are used, and an initial model assessment is conducted. The default parameters include regularization hyperparameters like gamma and lambda, helping mitigate overfitting. A subsequent hyperparameter tuning process is performed using random search cv to optimize model performance.

4.1.4 STAGE 5: EVALUATION

4.1.4.1 EVALUATION

The XGBoost model is evaluated using various metrics such as F1 score, recall score, ROC graph, and confusion matrix. The model demonstrates a good balance between precision and recall, with a macro-average F1 score of 0.81. The ROC graph with an AUC score of 0.90 indicates the model's ability to achieve a good balance in predicting actual positive instances (churn) and reducing false alarms.

Oversampling helps the model achieve a balanced performance across both classes, avoiding bias towards the majority class. Recall score increases from 0.70 to 0.74 after oversampling, ensuring the model's ability to correctly identify positive instances (churn).

The model is further validated for real-world applicability by predicting new data points not from the original dataset.

4.1.4.2 HYPERPARAMETER TUNING AND EVALUATION

Hyperparameter tuning using random search cv improves the model's recall score from 0.74 to 0.78 in predicting churn (class 1). The tuned parameters, including increased reg_lambda and gamma values, contribute to better generalization, preventing overfitting and enhancing the model's performance.

This streamlined modelling process, from initial training to hyperparameter tuning, ensures the XGBoost classifier's effectiveness in predicting churn and provides a robust solution for telecom marketing.
