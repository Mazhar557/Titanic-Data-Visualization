

# Data Visualization with Seaborn: Exploring the Titanic Dataset

In this GitHub post, we'll delve into the world of data visualization using Seaborn by exploring the Titanic dataset. We'll walk through various Seaborn plot functions and demonstrate how they can be used to gain insights from the data.

## Getting Started
First, let's import the necessary libraries and load the Titanic dataset:

    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    %matplotlib inline
    import sklearn
    import seaborn as sns

    import warnings
    warnings.filterwarnings('ignore')
    ### Sets the warning filter to ignore all warnings. This line suppresses warning messages that might otherwise be displayed during the execution of the code.
    plt.rcParams["figure.figsize"] = [10,5]
    ### Ignore warnings

    import warnings
    ### Set the warning filter to ignore FutureWarning
    warnings.simplefilter(action = "ignore", category = FutureWarning)


    %matplotlib inline

    import numpy as np
    import pandas as pd
    import seaborn as sns
    import matplotlib.pyplot as plt

## Seaborn functionality

Seaborn offers lot of functionality which makes it effective for many data visualization tasks. These functionalities are listed below:-

• Seaborn provides a dataset-oriented API to examine relationships between variables.

• It provides functions to fit and visualize linear regression models for different types of independent and dependent variables.

• Seaborn provide functions for visualizing univariate and bivariate distributions and for comparing them between subsets of data.

• It provides plotting functions for using categorical variables to show observations or aggregate statistics.

• It helps us to visualize matrices of data and use clustering algorithms to discover structure in those matrices.

• Seaborn provides a plotting function to plot statistical time series data. The function provides flexible estimation and representation of uncertainty around the estimate.

• It provide tools for choosing styles, colour palettes, palette widgets and utility functions. These tools help us to make beautiful plots that reveal patterns in the data.

• It provides several built-in themes for producing stylish looking Matplotlib graphics.


## Seaborn on Titanic dataset
-- In this tutorial, we will learn to use different Searbon plot functions to get insight from data. We will use Titanic dataset to experiment these searbon kind of plot.

### Prerequisites
You should have a basic understanding of computer programming terminologies. A basic understanding of Python and any of the programming languages is a plus. Seaborn library is built on top of Matplotlib. Having basic idea of Matplotlib will help you understand this tutorial in a better way.


## Import the Data
Let's extract the our Titanic data from the .csv file, create a pandas DataFrame and look at the available indicators:


• Survived: Outcome of survival (0 = No; 1 = Yes)

• Pclass: Socio-economic class (1 = Upper class; 2 = Middle class; 3 = Lower class)

• Name: Name of passenger

• Sex: Sex of the passenger

• Age: Age of the passenger (Some entries contain NaN)

• SibSp: Number of siblings and spouses of the 
passenger aboard

• Parch: Number of parents and children of the passenger aboard

• Ticket: Ticket number of the passenger

• Fare: Fare paid by the passenger

• Cabin: Cabin number of the passenger (Some entries contain NaN)

• Embarked: Port of embarkation of the passenger (C = Cherbourg; Q = Queenstown; S = Southampton)


### Analysing the Titanic data

    full_data = pd.read_csv('/content/titanic_dataset.csv')
The line of code full_data = pd.read_csv('/content/titanic_dataset.csv') reads a CSV file named "titanic_dataset.csv" and stores its contents in a pandas DataFrame named full_data.

    full_data.shape 
output :- (891, 12)

full_data.shape indicates that the DataFrame full_data has 891 rows and 12 columns.

    full_data.head()

![titanic ss1](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/08011c11-e808-4339-a12e-74ed132ff922)



## 2. Distribution plots
Distribution of data is the foremost thing that we need to understand while analysing the data. Here, we will see how seaborn helps us in understanding the distribution of our data.


### 2.1. distplot
The distplot() function provides the most convenient way to take a quick look at univariate distribution. This function will plot a histogram that fits the kernel density estimation(KDE) of the data.


Now let's plot the histogram of Number of parents and children of the passenger aboard(parch).

    sns.histplot(full_data['Parch'],kde=False)
    plt.show()

![titanic ss2](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/6241955a-fb4f-4e92-8bc8-affc332afe3c)

As we can see, most passengers don't have neither parents nor children aboard.

### 2.2. kdeplot
Kernel Density Estimation (KDE) is a way to estimate the probability density function of a continuous random variable. It is used for non-parametric analysis. Setting the hist flag to False in distplot will yield the KDE plot. For bivariate distribution, we can plot a kde by using jointplot(). Pass value ‘kde’ to the parameter kind to plot kernel plot.

Note: distplot(data) is used to visualize the parametric distribution of data. It plot both KDE and histogram on the same figure.

    sns.distplot(full_data['Age'], hist=False)
    plt.show()

![titanic ss3](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/2a9881d0-367d-4c8d-a41c-16ee009f4ab2)

As we can see that most of the passenger has the age between 20 to 40

    plt.figure(figsize=(8,8))
    sns.distplot(full_data['Age'])
    plt.show()

![titanic ss4](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/f8f30acf-b217-4f5b-82d8-5ae92c593a7e)


## 3. Relational plots

### 3.1. relplot
Figure-level interface for drawing relational plots onto a FacetGrid.

The function relplot() is named that way because it is designed to visualize many different statistical relationships. While scatter plots are a highly effective way of doing this, relationships where one variable represents a measure of time are better represented by a line. The relplot() function has a convenient kind parameter to let you easily switch to this alternate representation.

    sns.relplot(x="Age", y="Fare", col="Pclass", hue="Sex", style="Sex",kind="line", data=full_data) # scatter can be used instead of "line" plot
    plt.show()

![titanic ss5](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/ddf9f7ac-904a-4a96-b715-f0e42a4788d1)



### 3.2. scatterplot
Scatter plot is the most convenient way to visualize the distribution where each observation is represented in two -dimensional plot via x and y axis.

    plt.figure(figsize=(8,8))
    sns.scatterplot(x="Age", y="Fare", hue="Sex", data=full_data)
    plt.show()

![titanic ss6](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/a6fac56b-9f1f-4221-ad26-8547507ac79e)


### 3.3. lineplot
Draw a line plot with possibility of several semantic groupings.

The relationship between x and y can be shown for different subsets of the data using the hue, size, and style parameters. These parameters control what visual semantics are used to identify the different subsets. It is possible to show up to three dimensions independently by using all three semantic types, but this style of plot can be hard to interpret and is often ineffective. Using redundant semantics (i.e. both hue and style for the same variable) can be helpful for making graphics more accessible.

The default treatment of the hue (and to a lesser extent, size) semantic, if present, depends on whether the variable is inferred to represent “numeric” or “categorical” data. In particular, numeric variables are represented with a sequential colormap by default, and the legend entries show regular “ticks” with values that may or may not exist in the data. This behavior can be controlled through various parameters.

By default, the plot aggregates over multiple y values at each value of x and shows an estimate of the central tendency and a confidence interval for that estimate.

    plt.figure(figsize=(8,8))
    sns.lineplot(x="Age", y="Fare", hue="Sex", style="Sex", data=full_data)
    plt.show()

![titanic ss7](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/228eec88-ce76-4e5a-b1b2-a8bbd1e25b46)


## 4. Categorical Plot
When one or both the variables under study are categorical, we use plots like striplot(), swarmplot(), etc,. Seaborn provides interface to do so.

### 4.1. barplot
The barplot() shows the relation between a categorical variable and a continuous variable. The data is represented in rectangular bars where the length the bar represents the proportion of the data in that category. Bar plot represents the estimate of central tendency.

Note: don't confuse Bar plot and Histogram. Please back to 2.1. distplot section to see the difference.

    plt.figure(figsize=(8,8))
    sns.barplot(x="Sex", y="Survived", hue="Pclass", data=full_data)
    plt.show()

![titanic ss8](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/f6a26f27-3dd8-4692-bf88-bff463766541)


### 4.2. stripplot
stripplot() is used when one of the variable under study is categorical. It represents the data in sorted order along any one of the axis.

    plt.figure(figsize=(8,8))
    sns.stripplot(x="Sex", y="Age",hue='Sex', data=full_data)
    plt.show()

![titanic ss9](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/36861051-1fc5-42b0-8fd7-b9437c32d696)



To avoid the overlapping of the points, we can use the jitter to add some random noise to the data. This parameter will adjust the positions along the categorical axis. But Another option which can be used as an alternate to ‘Jitter’ is function swarmplot().

### 4.3. swarmplot
This function positions each point of scatter plot on the categorical axis and thereby avoids overlapping points:

    plt.figure(figsize=(8,8))
    sns.swarmplot(x="Sex", y="Age",hue='Sex', data=full_data)
    plt.show()

![titanic ss10](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/b95f5c65-a6a7-4554-a159-8639b102f6b9)


We can said that more passengers are approximally between 18 and 40 years old.

### 4.4. boxplot
Boxplot is a convenient way to visualize the distribution of data through their quartiles. Box plots usually have vertical lines extending from the boxes which are termed as whiskers. These whiskers indicate variability outside the upper and lower quartiles, hence Box Plots are also termed as box-and-whisker plot and box-and-whisker diagram. Any Outliers in the data are plotted as individual points.

    plt.figure(figsize=(8,8))
    sns.boxplot(x="Survived", y="Age", data=full_data)
    plt.show()

![titanic ss11](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/6189b3ce-e44d-4913-9d5a-15480def2e80)


### 4.5. violinplot
Violin Plots are a combination of the box plot with the kernel density estimates. So, these plots are easier to analyze and understand the distribution of the data.

    sns.violinplot(x="Survived", y="Age", hue='Sex', data=full_data)
    plt.show()

![titanic ss12](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/d7f4aebe-f054-4cb7-acf2-2b29f63dec59)

### 4.6. countplot
A special case in barplot is to show the no of observations in each category rather than computing a statistic for a second variable. For this, we use countplot().

    sns.countplot(x="Survived", data=full_data, palette="Blues");
    plt.show()

![titanic ss13](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/a1bb325d-24b7-428d-b032-b3c7117232c6)

### 4.7. pointplot
Point plots serve same as bar plots but in a different style. Rather than the full bar, the value of the estimate is represented by the point at a certain height on the other axis.

    plt.subplots(figsize=(8, 8))
    sns.pointplot(x="Sex", y="Survived", hue="Pclass", data=full_data)
    plt.show()

![titanic ss14](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/974fa8f7-1680-4598-a835-6deaf7eb22c5)

## 5. Regression plots
Most of the times, we use datasets that contain multiple quantitative variables, and the goal of an analysis is often to relate those variables to each other. This can be done through the regression lines.

While building the regression models, we often check for multicollinearity, where we had to see the correlation between all the combinations of continuous variables and will take necessary action to remove multicollinearity if exists.

There are two main functions in Seaborn to visualize a linear relationship determined through regression. These functions are regplot() and lmplot().
### 5.1. lmplot
lmplot has data as a required parameter and the x and y variables must be specified as strings. This data form at is called “long -form ” data

    sns.lmplot(x="Age", y="Fare", data=full_data)
    plt.show()

![titanic ss15](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/d983c42c-8b7e-426f-8585-d99ee643b51e)

### 5.2. regplot
regplot accepts the x and y variables in a variety of formats including simple numpy arrays, pandas Series objects, or as references to variables in a pandas DataFrame.

    plt.subplots(figsize=(10, 10))
    sns.regplot(x="Age", y="Fare", data=full_data)
    plt.show()

![titanic ss16](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/f1129647-7972-4722-871f-9a0a933eec17)

    plt.subplots(figsize=(10, 10))
    sns.regplot(x="Fare", y="Fare", data=full_data)
    plt.show()

![titanic ss17](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/bfb30ea3-efb7-42e0-a6ed-12fdb58ebf5f)

## 6. Matrix plots

### 6.1. heatmap
Visualizing data with heatmaps is a great way to do exploratory data analysis, when you have a data set with multiple variables. Heatmaps can reveal general pattern in the dataset, instantly. And it is very easy to make beautiful heatmaps with Seaborn library in Python.

Now let's plot the correlation matrix of our data with a heatmap.

    plt.subplots(figsize=(10, 10))
    sns.heatmap(full_data.corr(), cmap = "YlGnBu", annot=True, fmt=".2f")
    plt.show()

![titanic ss18](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/e4e319c6-7327-4fca-90f9-de8b577091a5)


## 7. Multi-plot grids

### 7.1. Facet grids
A useful approach to explore medium-dimensional data, is by drawing multiple instances of the same plot on different subsets of your dataset. This technique is commonly called as “lattice”, or “trellis” plotting, and it is related to the idea of “small multiples”. To use these features, your data has to be in a Pandas DataFrame.

Facet grid forms a matrix of panels defined by row and column by dividing the variables. Due of panels, a single plot looks like multiple plots. It is very helpful to analyze all combinations in two discrete variables.

FacetGrid object takes a dataframe as input and the names of the variables that will form the row, column, or hue dimensions of the grid. The variables should be categorical and the data at each level of the variable will be used for a facet along that axis.

The advantage of using Facet is, we can input another variable into the plot. We can make many column facets and align them with the rows of the grid:

FacetGrid.map
The main approach for visualizing data on this grid is with the FacetGrid.map() method.

## initialize the FacetGrid object
    g = sns.FacetGrid(full_data, col='Survived', row='Pclass')

    g.map(plt.hist, 'Age')
    g.add_legend()
    plt.show()

![titanic ss19](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/3363da52-c327-4ef1-9260-d4c809c1309c)

![titanic ss20](https://github.com/Mazhar557/Titanic-Data-Visualization/assets/128870716/f9adc9c7-14a1-420a-bd2d-cf6898a6f92f)

## Conclusion
This tutorial took you through the basics and various functions of Seaborn. It is specifically useful for people working on data analysis. After completing this tutorial, you are now at a moderate level of expertise from where you can take yourself to higher levels of expertise.


Stay update, practice, practice and practice to developpe data visualization skill.

Thanks and Good luck.
