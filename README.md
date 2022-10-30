# Enhance EDA 📊

![EDA title.png](./media/EDA%20title.png)

## Table of Contents

- [What is EDA?  ](#introduction)
  - [Steps involved in EDA ](#steps)
- [Libraries used in EDA](#libraries)
- [Pandas Cheatsheet for EDA](#handsOn)
  - [How to approach the cheatsheet](#approach)
  - [Understanding the dataset](#understandingData)
  - [Modifying the dataset](#modifying)
  - [Dealing with null/NaN/Missing values](#missingvalues)
  - [Encoding](#encoding)
- [Plotting the analysis](#plotting)
- [Contributing](#contribute)

---

# What is EDA? <a id="introduction"> </a>

EDA(Exploratory Data Analysis) is a very important phase in a Data Science life cycle, which is a part of Feature Engineering. It is a glimpse into the data you will be analyzing, Finding junk, removing it, finding outliers and replacing them in proper fashion are some of the tasks this usually entails.

As the name suggests it is a phase in which we explore the collected data from different sources, do some data cleaning, and analyse the stats through plotting graphs, and provide the optimized data to build model with high accuracy.

## Steps involved in EDA <a id= steps > </a>

1) Understanding the dataset
2) Modifying the dataset
3) Dealing with missing values
4) Plotting graphs to get realtionship between the features.
   
   > **NOTE:** We'll sneak peek into each step in the _[Pandas cheatsheet for EDA](#handsOn)_ section

---

# Libraries used in EDA <a id = libraries> </a>

As we are talking about exploring the dataset , the top libraries which deals with datasets are `numpy` and `pandas` and for plotting the analysis and observations we have many different options to go for. We have , the traditional `matplotlib` library and some mordern options like `seaborn` which is built on matplotlib and `plotly` which is made out of javascript giving the most handy graphs ever, and we have many other libraries regarding the plotting part.

> __NOTE:__ The Plots made in this repositories notebooks are made by seaborn. you can find the alternative codes for plots from the respective documents. feel free to check them out.

---

# Pandas Cheatsheet for EDA <a id = handsOn ></a>

`pandas` library is used throughout the EDA, for all the exploring,seeking for missing values, dealing with them, cleaning the redundent data. 
So this Section will give you the overview of the most common methods used in each step of EDA.

#### How to approach this cheatsheet? <a id = approach ></a>

This cheat sheet is made based on an assumption that the dataset is read with a variable `df` and the features , dataset is consisting of are `x1` , `x2` , `x3` .

```Python
import numpy as np
import pandas as pd
df = pd.read_csv('sample_data.csv')
df.columns 
# Output: Index(['x1','x2','x3'],dtype='object')
```

so , Open your jupyter notebook in a new window and get hands on with the cheat sheet. 

## 1) Understanding the data 📑 <a id = understandingData ></a>

| Methods/tuples                         | Description                                                                                                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `df.head()`                            | Returns the first 5 records of the dataset you can also try passing any positive integer value as argument (`df.head(10)`)                                                            |
| `df.columns`                           | Returns a series consisting of all the column names.                                                                                                                                  |
| `df.info()`                            | Returns the detailed dataframe consisting of feature names , the count of non-null cells and data type of each feature as column names.                                               |
| `df.shape`                             | Returns the dimensions of the dataset in the form of (no. of rows , no. of columns)                                                                                                   |
| `df.describe()`                        | Returns a dataframe consisting of all the statistical calculations such as count , mean , std , min etc., for all the numeric class(ie. int32/int64 , float32/float64,etc.) features. |
| `df.nunique()`                         | Returns the no. of categories each feature is containing in a form of dataframe.                                                                                                      |
| `df.dtypes`                            | Returns the datatypes of the each features                                                                                                                                            |
| `df.x1.unique()` / `df['x1'].unique()` | Returns the index consisting of all the distinct categories `x1` feature has                                                                                                          |
| `df.x1.value_count()`                  | Returns a dataframe consisting of the count of records ,each category of `x1` feature consists of.                                                                                    |
| `df.corr()`                            | Returns a dataframe consisting of the correlation among the features of the dataset                                                                                                   |

## 2) Modifying the dataset (_if required_) <a id = modifying ></a>

| Methods/tuples                                           | Description                                                                                                                                                                                                                               |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `df =df.iloc[row_start:row_end,column_start:column_end]` | You can trim your dataset using this code.                                                                                                                                                                                                |
| `pd.merge(df1,df2,on='column_name',how='')`              | you can merge two dataset(here `df1` and `df2` ) using this command. Here `on` specifies the column name to use as the primary key to join and `how` specifies the way you want it to be joined (`left`/`right`/`outer`/`inner`/`cross`). |
| `df1.append(df2)`                                        | this is used to append the dataframes one above another.                                                                                                                                                                                  |
| `pd.concat([df1,df2],axis=0/1)`                          | this command is widely used to join the datasets. you can give any no. of Dataframs in the form of list and the `axis` specifies weatheer to join it horizontally(`0`) or vertically(`1`).                                                |
| `df.drop(x1,axis = 0/1,inplace = True`                   | this is used to remove record or a column from the dataset. here inplace specifices the method to be executed on the parent dataset                                                                                                       |
| `df.x1 = df.x1.astype(int/float...)`                     | This is used to change the datatype of the feature.                                                                                                                                                                                       |

## 3) Working on missing values ❔ <a id = missingvalues ></a>

| Methods/tuples                    | Description                                                                                                                                                                                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `df.isna().sum/df.isnull().sum()` | both methods work exactly similar, It gives the total no. of NaN or null values present in each feature column.                                                                                                                                  |
| `df.fillna()`                     | this method is used to fill the missing value cells with the value passed as argument. in most cases mode or mean of each feature column calculated using `df.x1.mean()` , `df.x2.mode()` methods to replace the NaN cells of respective column. |
| `df[df.index.duplicated]`         | This returns a dataframe will all the records which have duplicates.                                                                                                                                                                             |

## 4) Encoding 🧮 <a id = encoding ></a>

Encoding is usually used to deal with labeled categorical data. where the categories as labeled with strings instead of any numeric values. so we can use following methods to convert the labeled value to numeric value. There are many other encoding methods(feel free to contribute).
| Methods/tuples | Description |
|----|----|
| `pd.get_dummies(df.x1,drop_first = True)` | this will perform one hot encoding to the categorical variables of the features. and `drop_first = True` will drop the first variables ecoded value, which will in turn reduce the burden on the model to learn. you can refer _[<u>this</u>](https://stackoverflow.com/questions/63661560/drop-first-true-during-dummy-variable-creation-in-pandas)_. to get more knowledge.
|`df.x1 = df.x1.map({xa1:1,xa2:2....})`| This code is used for label encoding the categorical varibles of the feature. here `xa1`, `xa2` are the current categories and `1`,`2` are the respective modified value often referred as the ranks.

---
# Plotting in EDA <a id = plotting> </a>

plotting different types of realations between the features and varibles, gives the clear insights and makes it very easy to explain the observation to the client, instead of showing them the excel sheet and writing the observations beneath. there are different types of plots you can use to analyse the dataset, most commonly used plots are:

- [bar plot](https://seaborn.pydata.org/generated/seaborn.barplot.html)
- [count plot](https://seaborn.pydata.org/generated/seaborn.countplot.html)
- [pair plot](https://seaborn.pydata.org/generated/seaborn.pairplot.html)
- [heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html?highlight=heatmap#seaborn.heatmap)
- [scatter plot](https://seaborn.pydata.org/generated/seaborn.scatterplot.html)
- [box plot](https://seaborn.pydata.org/generated/seaborn.boxplot.html)
- [piechart](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html)
- [histogram](https://seaborn.pydata.org/generated/seaborn.histplot.html)

Go though the jupyter notebooks present in the repository to get better understanding on how each graph is used. 

---
# Contributing <a id = contribute ></a>
Got any ideas that you want to contribute to this repository? Sure, you are open to contribute. 
fork,clone,commit,send the PR. 

---
Make sure you star the repo if you gain any value through this repo :-)
#### Hail Data 🖖🏾.