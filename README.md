SmartKart Customer Churn Prediction
An end-to-end Machine Learning project for predicting customer churn using Logistic Regression.

Project Overview
Customer churn is an important business problem for retail companies. Identifying customers who are likely to leave allows businesses to take proactive retention actions.

This project uses SmartKart customer data to predict whether a customer is likely to churn based on customer age, monthly spending, and number of complaints.

The project follows a complete machine learning pipeline:

Data Collection → Data Understanding → Data Cleaning → Outlier Detection & Treatment → Feature Selection → Target Definition → Target Encoding → Train-Test Split → Feature Standardisation → Model Building → Model Training → Prediction → Model Evaluation → Model Interpretation → Final Output

The complete 15-step workflow is implemented in the SmartKart.ipynb notebook.

Objective
The main objectives of this project are:

Clean and prepare a real-world-style customer dataset
Identify and handle data-quality issues
Detect and treat outliers
Select relevant features for churn prediction
Build a Logistic Regression classification model
Evaluate model performance
Interpret the model coefficients
Generate customer-level churn probabilities
Identify customers who are more likely to churn
Dataset
The project uses the following dataset:

SmartKart_dirty_100_rows.csv

The dataset contains 100 customer records with five columns:

Column	Description
Customer_ID	Unique customer identifier
Age	Customer age
Monthly_Spend	Customer monthly spending
Complaints	Number of customer complaints
Churn	Target variable: 1 = Churn, 0 = No Churn
The dataset intentionally contains data-quality issues such as duplicate records, missing values, invalid values, inconsistent formatting, and outliers.

Data Quality Issues
The original dataset contains several issues that simulate a real-world data-cleaning scenario.

Duplicate Records
Five duplicate customer records are present in the original 100-row dataset.

Examples include duplicate records for:

C005
C030
C050
C070
C080
These duplicate rows are removed during preprocessing.

Missing Values
Missing values are present in:

Age
Monthly_Spend
Complaints
The project handles these missing values using median imputation.

Invalid Age Values
The Age column contains inconsistent and invalid values, including:

"thirty"
-5
150
whitespace-formatted values
The project converts the column to numeric format, converts "thirty" to 30, and treats unrealistic ages outside the 15–90 range as missing values.

Invalid Monthly Spend
The dataset contains a negative monthly spending value:

-1000

Since negative spending is invalid, this value is converted to missing and subsequently replaced using median imputation.

Outliers
The dataset contains extreme values such as:

Monthly_Spend = 99999
Complaints = 50
These are treated using the Interquartile Range method.

Data Cleaning
The preprocessing workflow includes:

Removing unnecessary whitespace
Removing duplicate records
Correcting inconsistent data types
Converting invalid numeric values
Identifying unrealistic ages
Handling negative monthly spending
Filling missing values using the median
After cleaning, the dataset contains 95 records and no remaining missing values.

Outlier Detection and Treatment
The project uses the IQR (Interquartile Range) method.

The lower and upper limits are calculated as:

Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR
Instead of deleting outlier records, the project caps extreme values using the calculated boundaries.

This approach preserves the customer record while reducing the influence of extreme observations on the Logistic Regression model.

Feature Selection
The following three features are used for predicting churn:

Age
Monthly_Spend
Complaints
Customer_ID is excluded because it is an identifier and does not represent a meaningful predictive feature.

Target Variable
The target variable is:

Churn
The values are:

0 = No Churn
1 = Churn
The target variable is already numeric, so no additional encoding is required.

Train-Test Split
The cleaned dataset is divided into:

80% training data
20% testing data
The split uses:

random_state=42
and stratification to maintain a similar churn distribution in both datasets.

Feature Standardisation
The project uses StandardScaler to standardise the numerical features.

The scaler is fitted only on the training dataset and then applied to the testing dataset.

This prevents information from the test dataset from leaking into the training process.

Machine Learning Model
The project uses:

Logistic Regression

Logistic Regression is suitable for this problem because customer churn is a binary classification problem.

The model also provides churn probabilities, which can be used to rank customers according to their estimated churn risk.

Model Evaluation
The model is evaluated using:

Confusion Matrix
Accuracy
Precision
Recall
F1-Score
Classification Report
The notebook specifically evaluates the model using these metrics and visualises the confusion matrix using a heatmap.

The exact metrics are calculated when the notebook is executed.

Model Interpretation
One of the advantages of Logistic Regression is that its coefficients can be interpreted to understand the relationship between the features and churn.

The project examines the coefficients for:

Age
Monthly Spend
Complaints
According to the notebook's interpretation:

Higher Monthly_Spend is associated with lower churn risk.
Higher Complaints are associated with higher churn risk.
Age has a comparatively smaller effect on churn in this dataset.
The project therefore highlights customer complaints and spending behaviour as important factors for understanding churn.

Customer Churn Risk
The final stage converts model predictions into a customer-level risk report.

The output contains:

Customer ID
Age
Monthly Spend
Complaints
Actual Churn
Predicted Churn
Churn Probability
Risk Label
Customers can then be ranked according to their predicted churn probability so that the retention team can prioritise higher-risk customers.

Business Application
The model can support a retail business in:

Identifying customers at higher risk of churn
Prioritising customer retention activities
Monitoring complaint-related churn risk
Understanding factors associated with customer churn
Ranking customers according to estimated churn probability
Supporting data-driven customer retention decisions
Project Structure
SmartKart/
│
├── SmartKart.ipynb
├── SmartKart_dirty_100_rows.csv
├── smartkart_churn_risk_report.csv
└── README.md
SmartKart.ipynb
Contains the complete 15-step machine learning workflow, from data collection through final churn-risk output.

SmartKart_dirty_100_rows.csv
Original 100-row customer dataset containing intentionally introduced data-quality problems.

smartkart_churn_risk_report.csv
Business-oriented output containing customer churn predictions and estimated churn probabilities.

Technologies Used
Python
Pandas
NumPy
Scikit-learn
Matplotlib
Seaborn
Jupyter Notebook
Installation
Clone the repository:

git clone <repository-url>
cd SmartKart
Install the required Python libraries:

pip install pandas numpy scikit-learn matplotlib seaborn jupyter
How to Run
Start Jupyter Notebook:

jupyter notebook
Open:

SmartKart.ipynb
Run the notebook cells sequentially from Step 1 through Step 15.

The original notebook is designed for Google Colab and includes a file-upload step for the CSV dataset.

Machine Learning Workflow
Raw Customer Data
        |
        v
Data Inspection
        |
        v
Data Cleaning
        |
        v
Outlier Treatment
        |
        v
Feature Selection
        |
        v
Target Definition
        |
        v
Train-Test Split
        |
        v
Feature Standardisation
        |
        v
Logistic Regression
        |
        v
Prediction
        |
        v
Model Evaluation
        |
        v
Model Interpretation
        |
        v
Customer Churn Risk Report
Key Takeaway
This project demonstrates an end-to-end approach to customer churn prediction, starting with a deliberately messy customer dataset and transforming it into a machine learning-ready dataset.

The final model provides both churn predictions and churn probabilities, allowing the results to be interpreted from a business perspective and used to prioritise customer retention activities.
