# Heart Disease Classification using Logistic Regression

This project focuses on building a logistic regression model to predict the presence of heart disease based on patient characteristics. The dataset is obtained from the UCI Machine Learning Repository and can be found [here](https://archive.ics.uci.edu/dataset/45/heart+disease). The project follows a standard machine learning pipeline: data exploration and preprocessing, feature selection, model building, and evaluation.

## Data Description

The dataset contains several features related to patient health, including:

-   **age**: Age of the patient.
-   **sex**: Sex of the patient (1 = male; 0 = female).
-   **cp**: Chest pain type (4 values).
-   **trestbps**: Resting blood pressure.
-   **chol**: Serum cholesterol in mg/dl.
-   **fbs**: Fasting blood sugar > 120 mg/dl (1 = true; 0 = false).
-   **restecg**: Resting electrocardiographic results (values 0,1,2).
-   **thalach**: Maximum heart rate achieved.
-   **exang**: Exercise induced angina (1 = yes; 0 = no).
-   **oldpeak**: ST depression induced by exercise relative to rest.
-   **slope**: The slope of the peak exercise ST segment.
-   **ca**: Number of major vessels (0-3) colored by flouroscopy.
-   **thal**: 3 = normal; 6 = fixed defect; 7 = reversible defect.
-   **present**: Target variable (1 = heart disease present; 0 = heart disease not present).

The dataset can be found in the `data` folder as `heart_disease.csv`.

## Methodology

### 1. Data Loading and Exploration

The dataset is loaded using pandas, and initial exploration is done to understand the data types and distributions.

### 2. Data Cleaning

-   **Handling Missing Values**: The `ca` and `thal` columns had '?' entries, which were treated as null values and imputed with the mode of their respective columns.

-   **Type Conversion**: The `ca` and `thal` columns were converted to numeric data types.
-   **Dropping Unnecessary Columns**: The index column was dropped.
-   **Verifying Duplicate Rows**: Checked for duplicates (found none).

### 3. Feature Selection

-   **Correlation Analysis**: A correlation heatmap and table were used to identify the most impactful features on the target variable (`present`).
-   **Feature Visualization**: Histograms were created to compare the distribution of features between present and non-present cases.
-   **Selected Features**: Based on this analysis, the following features were chosen: `thal`, `ca`, `cp`, and `oldpeak`.

### 4. Data Splitting

-   The data was split into training (80%) and testing (20%) sets using `train_test_split` with a random state of 2837 to ensure a balanced distribution of the target variable within the training set.

### 5. Model Building

-   **Model Initialization**: A logistic regression model was initialized using `LogisticRegression` from `sklearn.linear_model`.
-   **Model Training**: The model was trained using the training data.
-   **Prediction**: Predictions were made on both the training and test sets.

### 6. Model Evaluation

-   **Metrics**: The model's performance was evaluated using accuracy, sensitivity, and specificity.
-   **Classification Report**: A classification report was printed for more in-depth results.

-   **Coefficient Interpretation**:  The model's coefficients were transformed into odds ratios to understand the impact of each feature on the likelihood of heart disease.

## Results

The model achieved good accuracy and specificity, indicating it's proficient at predicting non-presence of heart disease. However, the model shows lower sensitivity, suggesting it has difficulty in predicting true cases of heart disease.

The odds ratios suggest the following (holding other variables constant):

-   **thal**: Higher stress test results indicate lower odds of having heart disease.
-   **ca**: Higher number of colored blood vessels indicate higher odds of having heart disease.
-   **cp**: Exhibiting Constrictive Pericarditis indicates lower odds of having heart disease.
-   **oldpeak**: Higher amounts ST Depression induced by exercise indicate lower odds of having heart disease.

## Conclusion and Recommendations

The model is more effective at predicting the absence of heart disease rather than its presence. This bias may be due to the limited set of features and potential class imbalance within the dataset.

**Recommendations:**

-   **Feature Enrichment:** Include stronger predictive features, such as cholesterol levels, blood pressure, or diabetes status.
-   **Class Imbalance:** Investigate class imbalances and consider oversampling or undersampling methods.
-   **Alternative Models:** Explore other models such as tree-based models (e.g. Random Forest, Gradient Boosting) to try and achieve better performance.
-   **Threshold Adjustment:** Adjust the classification threshold to improve sensitivity, although it may impact specificity.