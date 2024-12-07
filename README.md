# Harnessing Machine Learning to Predict and Analyze Diabetes Risk

![](./img/diabetes.jpg)

## Introduction:

Diabetes mellitus is a global health concern, impacting millions of lives annually. Early detection and proactive management are critical to reducing its impact. This project utilized machine learning (ML) to predict diabetes risk based on patient data, offering insights into key risk factors and the potential for data-driven healthcare interventions.
To understand more about diabetes, I outlined very concisely all you need to know in these posts.

Post 1: [I discussed diabetes, touching on its prevalence, symptoms, causes, types, and risk factors here](https://www.linkedin.com/posts/onyemacemmanuel_diabetes-bloodsugar-sugar-activity-7263635107389833216-O1PT?utm_source=share&utm_medium=member_desktop).

Post 2: [I discussed testing, prevention, and management here](https://www.linkedin.com/posts/onyemacemmanuel_diabetes-bloodsugar-sugar-activity-7264980105133740032-xF9s?utm_source=share&utm_medium=member_desktop).

---

## Objectives:

- Develop a machine learning model to predict diabetes risk with high accuracy, F1 score and Recall of 80% +.
- Analyze data to identify significant predictors of diabetes.

---

## Workflow:

1. Data Loading
2. Data Cleaning
3. EDA and Feature Engineering
4. Data Preprocessing
5. Model Selection and Training
6. Model Evaluation
7. Conclusion and Reporting

---

## Understanding the Dataset:

### Dataset Overview

This dataset is originally from the National Institute of Diabetes and Digestive and Kidney Diseases. This dataset contains 768 rows, and 9 columns. Several constraints were placed on the selection of these instances from a larger database. In particular, all patients here are females at least 21 years old of Pima Indian heritage. [Diabetes dataset](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)

> Features:

- Glucose Level
- Blood Pressure
- Insulin Levels
- BMI (Body Mass Index)
- Age
- Skin Thickness
- Number of Pregnancies
- Diabetes Pedigree Function (Genetic Risk Factor)

> Target Variable:

- Outcome (binary: 0 = No, 1 = Yes).

---

## Data Cleaning:

At first glance, it seemed there were no missing values. However, a closer examination with an industry perspective of the descriptive summary revealed inconsistencies in the data, as it is unusual for the minimum value of some of the features to be zero (0).

![](./img/missing%20values.png)

### Handling Missing Values:

Replaced zero values in features like Glucose, BMI, Insulin, BloodPressure, SkinThickness, with NaN value to reveal missing values. The missing values were imputed by replacing zero values based on the median of each column, grouped by the 'Outcome' column.

|      Replacing zero values       |         Visualization         |
| :------------------------------: | :---------------------------: |
| ![](./img/replace%20missing.png) | ![](./img/output_missing.png) |

---

## Exploratory Data Analysis (EDA):

EDA provided critical insights into the dataset:
Key Findings after the features were cut into bins

- **Insulin Levels**: Strongly correlated with diabetes. Individuals with abnormal levels above 166 showed a higher probability of diabetes.
  ![](./img/Insulin.png)

- **Glucose Levels**: Strongly correlated with diabetes. Individuals with glucose levels above 100 mg/dL showed a higher probability of diabetes.
  ![](./img/glucose.png)

- **BMI**: Higher BMI values significantly increased diabetes risk, emphasizing the role of weight management.
  ![](./img/BMI.png)
- **Age**: Older individuals, had a higher prevalence of diabetes.
  ![](./img/Age.png)

### Feature Interactions:

Combined Glucose, BMI, BloodPressure, Insulin and Pregnancy levels to create a risk score to revealed individuals with heightened risk.

```
 df['risk'] = ((df['Glucose'] >110).astype(int)+(df['BMI']>30).astype(int)+(df['BloodPressure']>130).astype(int)+(df['Insulin']>100).astype(int)+(df['Pregnancies']>5).astype(int))
```

![](./img/Risk.png)

#### Visualization Techniques

**Correlation Heatmap**: Highlighted relationships between features.
![](./img/corr.png)
**Pair Plots**: Revealed feature interactions and data distributions.
![](./img/pairplot.png)
**Scatter Plots**: Revealed feature interactions and data distributions.
![](./img/scatterplot.png)
**Box Plots**: Identified outliers in critical features like glucose and insulin levels which was clipped.
![](./img/Outlier.png)
![](./img/no%20outlier.png)

---

## Data Preprocessing:

### One hot encoding

The categorical features such as 'bmi_class', 'insulin_class', 'glucose_class' were one hot encoded.

### Data Scaling

The data dataframe was separated into a numerical and categorical dataframe to allow the numerical data to be scaled only, as its not ideal for the categorical to be scaled after being one hot encoded.

### Scaling and Splitting

Robust scaler was used to scale the numerical data, after which both numerical and categorical data was concatenated and split into X and Training and testing in the ratio of 80:20.

## Model Development:

We implemented various ML algorithms to predict diabetes and selected the best-performing model.
Algorithms Used

- Logistic Regression
- Random Forest
- Support Vector Machine
- Decision Tree
- K-Nearest Neighbour
- Naive Bayes
- Gradient boosting

---

## Model Evaluation Metrics:

- **F1-Score**: Balances precision and recall.
- **Recall**: Measures the ability to identify actual diabetic patients (True Positives).
- **Accuracy**: Overall correctness of predictions.
- **Precision**: Proportion of positive identifications that were correct.

![](./img/model%20performance.png)

The Gradient Boosting Classifier model achieved the highest metrics making it the best choice for this dataset.

---

## Interpretability and Insights

### Key Metrics used to rank result

- **Recall** (Sensitivity/True Positive Rate):
  Recall measures the proportion of actual diabetics (positives) correctly identified by the model.
  High recall ensures that fewer diabetics are misclassified as non-diabetic (false negatives are minimized).

- **F1-Score** ()How many predicted diabetics are actually diabetic)
  F1-Score balances precision and recall. This is particularly useful in imbalanced datasets where both false positives and false negatives matter.

### Feature Importance

Insulin and Glucose levels had the highest impact on predictions, followed by Age and BMI.

Insulin - 0.683831
Glucose - 0.119013
Age - 0.056160
BMI - 0.041287

---

## Implications and Applications

- **Healthcare Screening**: The model can assist healthcare professionals in identifying at-risk individuals for early intervention.
- **Public Health Insights**: Data-driven insights can guide awareness campaigns, focusing on lifestyle modifications and regular check-ups.
- **Policy Recommendations**.

---

## Challenges and Limitations

- **Data Imbalance**: The dataset had more non-diabetic cases.
- **Limited Features**: The dataset lacked information on dietary habits, physical activity, etc.
- **Generalizability**: Results are specific to the dataset used, as all patients here are females of Pima Indian heritage
  and require validation on larger, diverse populations.

---

## Future Directions

- **Expanding Features**: Incorporate additional factors such as lifestyle habits, and genetic markers.
- **Hyperparameter Tuning**
- **Deployment**: Develop a user-friendly app or API for clinicians and individuals to leverage the model's predictions.

---

## Conclusion

This project demonstrated the potential of machine learning in addressing diabetes, a critical global health issue. By combining advanced algorithms with detailed data analysis, we can pave the way for smarter, more effective healthcare solutions.

## What's Next?

Thank you for taking the time to explore this project!. Please star the repo.
I welcome feedback and suggestions to enhance the project. If you spot any areas that need improvement, raise an issue in the repository.

### Suggestions and Improvements

Found a bug? Raise an issue.
Have an idea for a new feature? Share your thoughts!
Want to improve the documentation or code? Contributions are always welcome.

If you'd like to contribute to this project, feel free to fork the repository, make changes, and submit a pull request. I’m excited to learn from your expertise and incorporate new perspectives into the work.

> To contribute:

- Fork this repository.
- Create a feature branch (git checkout -b feature-name).
- Commit your changes (git commit -m "Add your message here").
- Push to your branch (git push origin feature-name).
- Open a pull request with a description of your changes.

#### Collaboration Opportunities

I’m open to collaborating with individuals or teams working on similar or entirely different projects. If you are working on an exciting project and think we could achieve more together, please reach out! I’m always looking forward to learning, sharing ideas, and building impactful solutions as a team.

##### You can reach me via:

Email: cemmanuelonyema@gmail.com
LinkedIn: [My LinkedIn Profile](https://www.linkedin.com/in/onyemacemmanuel/)
Twitter: [My Twitter Handle](https://twitter.com/ceonyema_)
Medium: [Read my Data Articles here](https://medium.com/@ceonyema)
Let’s connect and discuss ideas, and make a difference!
