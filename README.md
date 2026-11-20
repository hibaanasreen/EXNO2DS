# EXNO2DS
# Reg.No: 212224040117
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
### Code :
```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
data = pd.read_csv('titanic_dataset.csv')
for column in data.columns:
       if data[column].dtype == 'object':
                 data[column] = data[column].fillna(data[column].mode()[0])  # Fill with mode
       else:
                 data[column] = data[column].fillna(data[column].mean())  # Fill with mean
print(" Missing values handled.")
sns.boxplot(x=data['Fare'])
plt.title("Boxplot - Fare")
plt.xlabel("Fare")
plt.show()
```
### Output :
<img width="520" height="455" alt="image" src="https://github.com/user-attachments/assets/1bf788e4-6de3-46e5-9dc4-3d152a4e090e" />



### Code :
```
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]
data = remove_outliers_iqr(data, 'Fare')
print("Outliers removed using IQR method.")
```
### Output :
<img width="413" height="75" alt="image" src="https://github.com/user-attachments/assets/92d80ba5-5a3b-4206-a700-766598e6a719" />

### Code :
```
sns.countplot(x='Sex', data=data)
plt.title("Countplot - Sex")
plt.xticks(rotation=45)
plt.show()
```
### Output :
<img width="571" height="485" alt="image" src="https://github.com/user-attachments/assets/8889bbfe-3313-421f-a7ee-39576a856753" />


### Code :
```
sns.displot(data['Age'], kde=True)
plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()

```
### Output :
<img width="489" height="512" alt="image" src="https://github.com/user-attachments/assets/6cba1e09-b76b-487e-b5b4-aa79d9716ff7" />

### Code :
```
# Example: Sex vs Survived

crosstab_result = pd.crosstab(data['Sex'], data['Survived'])

print("\nCross Tabulation Result:")
print(crosstab_result)
# Only numeric columns are considered for correlation

correlation_matrix = data.corr(numeric_only=True)

sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()
```
### Output :
<img width="596" height="505" alt="image" src="https://github.com/user-attachments/assets/b19b3610-c263-4516-8392-7aa1ea49a6cb" />

# Output Interpretation:

From the outputs, I observed that the Titanic dataset contains more male passengers than female passengers. However, the survival count shows that more female passengers survived, while more male passengers did not survive. The boxplot shows some outliers in passenger fares, indicating that a few passengers paid much higher fares. The age distribution shows that most passengers were adults, mainly between 20 and 40 years. The cross-tabulation helps compare survival based on gender. Finally, the correlation heatmap shows that Pclass and Fare have a negative correlation (-0.59), while SibSp and Parch have a positive correlation (0.41).

# RESULT
Thus, the Titanic dataset was successfully loaded, cleaned, and analyzed using Python. The correlation heatmap was generated and displayed, showing the relationships between numerical attributes such as Age, Fare, Pclass, SibSp, Parch, and Survived.
