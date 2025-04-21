# DATA SCIENCE SKILL ASSESSEMENT-2
## EXPLORATORY DATA ANALYSIS AND OUTLIER DETECTION

## AIM:
1. **To perform data cleaning as needed** to ensure the dataset is ready for analysis.  
2. **To use the Boxplot technique** to identify potential outliers in the dataset.  
3. **To apply the Interquartile Range (IQR) method** to remove outliers from the data.  
4. **To create a Count Plot** for univariate analysis to visualize the distribution of categorical variables.  
5. **To generate a Distribution Plot (DistPlot)** for multivariate analysis to examine relationships between variables.

```
NAME : PREETHI D
REG NO : 212224040250

```
## ALGORITHM
1. **Import Libraries**  
   Load `pandas`, `numpy`, `matplotlib.pyplot`, and `seaborn`.

2. **Load Dataset**  
   Read `IOT.csv` and preview the data.

3. **Data Cleaning**  
   - Drop null values and duplicates.  
   - Remove irrelevant or inconsistent columns.

4. **Detect Outliers (Boxplot Method)**  
   - Plot boxplots for numerical features  to identify outliers visually.

5. **Remove Outliers (IQR Method)**  
   - Calculate Q1, Q3, and IQR.  
   - Filter out values outside the range:  
     (Q1 - 1.5 * IQR) or above (Q3 + 1.5 * IQR).
6. **Univariate Analysis**  
   - Use `seaborn.countplot()` for categorical features like `FuelType`.

7. **Multivariate Analysis**  
   - Use `seaborn.histplot()` with `hue` to compare numerical data across categories.

## PROGRAM AND OUTPUT
### Importing Required Libraries and loading the dataset
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
df = pd.read_csv("IOT.csv")
df
```
![image](https://github.com/user-attachments/assets/8e1febe9-db24-41af-a768-833f540a4b1a)
### Handling Missing Values
```
df.isnull().sum()

```
![image](https://github.com/user-attachments/assets/f5aea546-0098-4936-896c-058d7935f8d6)
```
df.noted_date.fillna(method='ffill',inplace = True)
df.isna().sum()
```
![image](https://github.com/user-attachments/assets/e57fff2b-94c9-4e8c-9802-470e6a1b7f8d)
### Data Cleaning
```
df.rename(columns ={'out/in':'status'},inplace = True)
df
```
![image](https://github.com/user-attachments/assets/af063fe0-b460-422f-9784-ed1760d00be3)
```
df.dtypes
```
![image](https://github.com/user-attachments/assets/9adedd82-7c3f-4794-8425-d363f1aab7c3)
### Filling Missing Values in temp
```
df.columns
tp = df.temp.median()
tp
```
![image](https://github.com/user-attachments/assets/51f5a7ab-651e-42ba-a4d1-be1366df9199)
```
df.temp.fillna(tp,inplace = True)
df
```
![image](https://github.com/user-attachments/assets/0335d164-ee8e-4341-81dd-6c35e64d024f)
```
df.isna().sum()
df.status.fillna(method='bfill',inplace = True)
df.isna().sum()
```

![image](https://github.com/user-attachments/assets/2df3b12a-eccc-4dd4-b18c-f5e66936c18c)
### Outlier Detection Using Boxplot
```
sns.boxplot(data=df['temp'])
```
![image](https://github.com/user-attachments/assets/117f43bd-f674-4393-bff9-0728951dcd12)
```
sns.boxenplot(data=df['temp'])
```
![image](https://github.com/user-attachments/assets/ad54b19e-e44a-48e2-9180-cc92e3806be0)
### Outlier Removal Using IQR Method
```
Q1 = np.percentile(df['temp'],25)
Q3 = np.percentile(df['temp'],75)
IQR = Q3 - Q1
IQR
LB = Q1 -1.5*IQR
HB = Q3 + 1.5*IQR
LB
HB
```
![image](https://github.com/user-attachments/assets/5113a43b-9b0b-4e4c-9d33-68c3652bc107)
### Filtering the DataFrame to Remove Outliers
```
df = df[((df['temp']>=LB)&(df['temp']<=HB))]
df
```
![image](https://github.com/user-attachments/assets/557ecfcb-31a0-4bc6-aabb-e7f87fe15461)
### Boxplot After Outlier Removal
```
sns.boxplot(data=df['temp'])
```
![image](https://github.com/user-attachments/assets/2f114544-7c31-4b5f-b225-7d06a9644def)
```
sns.boxenplot(data=df['temp'])
```
![image](https://github.com/user-attachments/assets/96ab4cb4-dfe7-492c-b61b-2093c09c7eab)
### UNIVARIATE ANALYSIS USING COUNTPLOT
```
sns.countplot(data=df, x='status')
```
![image](https://github.com/user-attachments/assets/f3ec0a68-b02e-4a95-bad2-b424f2a3823a)
### MULTIVARIATE ANALYSIS USING DISTPLOT
```
sns.displot(data=df,x='temp',hue='status', palette=['black','skyblue],kde=True)
```
![image](https://github.com/user-attachments/assets/58b72140-6f34-4eb0-b956-c45d6a1c3588)

## RESULT
The program was successfully executed. Data was cleaned, outliers were detected and removed using boxplot and IQR methods, and both univariate and multivariate analyses were performed using count plot and distplot.
