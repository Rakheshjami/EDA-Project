# Adult Income Data Analysis Project

## 📌 Project Overview

This project performs **Data Analysis and Exploratory Data Analysis
(EDA)** on the Adult Income dataset using Python.

The project covers:

-   Loading and understanding the dataset
-   Checking dataset shape and columns
-   Detecting missing values
-   Handling missing values
-   Detecting duplicate records
-   Detecting outliers
-   Using IQR and Z-score methods
-   Winsorization
-   Creating visualizations with Matplotlib and Seaborn
-   Automated EDA using AutoViz
-   Automated EDA using Sweetviz
-   Automated profiling using YData Profiling

## 📂 Project Files

``` text
Adult-Income-Data-Analysis/
│
├── DAproj.ipynb
├── adult.csv
├── README.md
└── sweetviz_report.html       # Generated after running the Sweetviz section
```

## 📊 Dataset

The project uses an **Adult Income dataset** containing **32,561 rows
and 15 columns**.

Main columns include:

-   `Age`
-   `Workclass`
-   `Final Weight`
-   `Education`
-   `EducationNum`
-   `Marital Status`
-   `Occupation`
-   `Relationship`
-   `Race`
-   `Gender`
-   `Capital Gain`
-   `capital loss`
-   `Hours per Week`
-   `Native Country`
-   `Income`

The `Income` column contains income categories such as `<=50K` and
`>50K`.

## 🛠️ Technologies Used

-   Python
-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   SciPy
-   AutoViz
-   Sweetviz
-   D-Tale
-   YData Profiling
-   Jupyter Notebook / Google Colab

## 🔍 Data Cleaning

The notebook checks for missing values and duplicate records.

Example:

``` python
print(df.isna().sum().sum())
print(df.duplicated().sum())
```

Missing values are handled using different techniques, including:

### Mean

``` python
df['Age'] = df['Age'].fillna(df['Age'].mean())
```

### Median

``` python
df['Hours per Week'] = df['Hours per Week'].fillna(
    df['Hours per Week'].median()
)
```

### Forward Fill

``` python
df['Native Country'].ffill()
```

### Backward Fill

``` python
df['Native Country'].bfill()
```

Categorical missing values are also handled using replacement values
such as `Unknown` and `Not Available`.

## 📈 Outlier Detection

The project uses the **IQR (Interquartile Range)** method.

``` python
Q1 = df['Age'].quantile(0.25)
Q3 = df['Age'].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

Outliers are identified using:

``` python
age_outlier = df[
    (df['Age'] < lower) |
    (df['Age'] > upper)
]
```

The same approach is applied to:

-   `Age`
-   `EducationNum`
-   `Hours per Week`

## 📐 Z-Score Method

The notebook also uses Z-score to identify unusual values.

``` python
from scipy.stats import zscore

df['Age_zscore'] = zscore(df['Age'])

z_outliers = df[df['Age_zscore'].abs() > 3]
```

A Z-score whose absolute value is greater than 3 is treated as an
outlier in this analysis.

## ✂️ Winsorization

Winsorization is also demonstrated for the `Age` column.

``` python
from scipy.stats.mstats import winsorize

df['Age_winsorized'] = winsorize(
    df['Age'],
    limits=[0, 0.5]
)
```

## 📊 Data Visualization

The project includes visualizations using **Matplotlib** and
**Seaborn**.

### Histogram

Shows the distribution of age:

``` python
plt.hist(df['Age'], bins=20)

plt.title('Age Distribution')
plt.xlabel('Age')
plt.ylabel('Count')

plt.show()
```

### Bar Chart

Shows education categories and education numbers:

``` python
plt.bar(
    df['Education'],
    df['EducationNum']
)

plt.title('Education')
plt.xlabel('Education')
plt.ylabel('years')

plt.show()
```

### Box Plot

Shows age distribution by income:

``` python
sns.boxplot(
    data=df,
    x='Income',
    y='Age'
)

plt.title('Age Distribution by Income')
plt.xlabel('Income')
plt.ylabel('Age')

plt.show()
```

### Scatter Plot

Shows the relationship between age and hours worked per week:

``` python
sns.scatterplot(
    data=df,
    x='Age',
    y='Hours per Week'
)

plt.title('Age vs Hours per Week')
plt.xlabel('Age')
plt.ylabel('Hours per Week')

plt.show()
```

## 🤖 Automated EDA

The notebook demonstrates several automated EDA tools.

### AutoViz

``` python
from autoviz.AutoViz_Class import AutoViz_Class

AV = AutoViz_Class()

AV.AutoViz(
    filename='adult.csv',
    sep=',',
    depVar='Income',
    dfte=data
)
```

### Sweetviz

``` python
import sweetviz as sv

report = sv.analyze(data)
report.show_html('sweetviz_report.html')
```

### YData Profiling

``` python
from ydata_profiling import ProfileReport

profile = ProfileReport(
    data,
    title='Adult Dataset Report'
)

profile.to_notebook_iframe()
```

## 🚀 How to Run the Project

### 1. Clone the repository

``` bash
git clone https://github.com/your-username/your-repository-name.git
```

### 2. Open the notebook

Open:

``` text
DAproj.ipynb
```

using Jupyter Notebook, JupyterLab, or Google Colab.

### 3. Keep the dataset available

Place:

``` text
adult.csv
```

in the same project folder as the notebook.

### 4. Install required libraries

``` bash
pip install pandas matplotlib seaborn scipy autoviz sweetviz dtale ydata-profiling
```

### 5. Run the notebook

Run the cells from top to bottom.

## 🎯 Learning Outcomes

Through this project, I practiced:

-   Python-based data analysis
-   Pandas DataFrame operations
-   Data cleaning
-   Missing-value handling
-   Duplicate detection
-   Outlier detection
-   IQR method
-   Z-score method
-   Winsorization
-   Data visualization
-   Exploratory Data Analysis
-   Automated EDA tools

## 👨‍💻 Author

**Rakesh Jami**

Data Analytics Learner \| Python \| Pandas \| Data Visualization \| SQL

## ⭐ Project Purpose

This project was created as a practical learning project to strengthen
Python and Data Analytics skills by working with a real-world tabular
dataset.
