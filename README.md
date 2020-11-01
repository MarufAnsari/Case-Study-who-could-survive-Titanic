#Case Study : Who would survive Titanic
----------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------

In this project, we will use the data of the passengers and crew on the Titanic to predict who survived the tragedy. We will not go through all the steps and go directly to the EDA part by using an existing Titanic dataset from Kaggle.com.

BRIEF PEEK INTO THE DATASET :
--------------------------------------------------------------------------
Before we do EDA, we need to peek into the dataset a little to see what the data looks like and what features does it have. The file we have downloaded is .csv file.

The data is a mixture of numerical (PassengerId, Survived, Pclass, Age, SibSp, Parch, Fare), categorical (Sex, Cabin, Embarked), and text data (Name, Ticket). Technically, Survived and Pclass are categorical too, but they are represented in number form in this data. There are missing values too, which are represented as "NaN" as in the "Cabin" column.

The purpose of this project is to predict the "Survived" variable using other variables. "Survived" variable is also known as the "target" and other variables are also known as "features."

EXPLORATORY DATA ANALYSIS (EDA) :
--------------------------------------------------------------------------
EDA is used to explore the target and features so we know if we will need to transform or normalize some of the features based on their distribution, delete some because it might not give us any information in predicting future outcomes, or create some new features that might be useful for prediction.

It's always good if we start our EDA process by asking lots of questions. Then we can generate figures and tables to answer these question. For visualization, I will mainly use matplotlib and yellowbrick.

To start with, I will ask following simple questions and then try to fill in the answers with some figures and tables :

What do the variables look like? For example, are they numerical or categorical data. If they are numerical, what are their distribution; if they are categorical, how many are they in different categories?
Are the numerical variables correlated?
Are the distributions of numerical variables the same or different among survived and not survived? Is the survival rate different for different values? For example, were people more likely to survive if they were younger?
Are there different survival rates in different categories? For example, did more women survived than man?

What do the variables look like?
--------------------------------------------------------------------------
To answer this question, first I'm going to check the summary of the variables, then make some histograms for the numerical variables, and some barplots for the categorical variables.

For all the numerical variables, we will know the average (mean), standard deviation (std), minimum value (min), maximum value (max) and different percentile (25%, 50% and 75%) of the data. Also from the count of data, we could know that there are missing values for some of the variables.
For all the object variables (categorical and text), we can see how many categories are in each variable from the "unique" row.
Summary of all the variables in tables like this can give us a very rough idea of how the variables look. However, to get more details, we will need to dive deeper and use additional visualization techniques.

Histograms are used to visualize the distribution of numerical data. In our data set, "PassengerId" are unique numbers from 1-891 to label each person and "Survived" and "Pclass" are also categorical data, so we will not plot a histogram for these variables.

From the histogram, we see that all the values in the variables seem in the correct range. Most of the passengers are around 20 to 30 years old and don't have siblings or relatives with them. A large amount of the tickets sold were less than $50. There are very few tickets sold where the fare was over $500.

Next we will create barplots for the categorical variables in the data set. Since "Ticket" and "Cabin" have too many levels (more than 100), we will not make the barplot for these.

Are the numerical variables correlated ?
--------------------------------------------------------------------------
In order to get a sense of whether the numerical variables in our data set are correlated, we will create a Pearson Ranking visualization.
From the Pearson ranking figure above, we can see that the correlation between variables are low (<0.5).

Are the distribution of numerical vairables the same or different among survived and not survived ?
--------------------------------------------------------------------------
Next, we will compare the distributions of numerical variables between passengers that survived and those that did not survive to see if there are any significant differences. We can do this with a Parallel Coordinates visualization.

Are there different survival rates in different countries ?
--------------------------------------------------------------------------
Speaking of survival rates, how did they differ across our categorical variables ?
We can get a sense of this by creating faceted stacked barplots for each variable.

Feature Selection and Feature Engineering
--------------------------------------------------------------------------
In this step, we will do lots of things to our data such as drop some features, fill in missing values, log transformations, and One Hot Encoding for the categorical feature
We will delete the features "PassengerId", "Name", "Ticket" and "Cabin" from our model. The reasons are as follows:

PassengerId: just a series of numbers from 1 - 891 which is used to label each person.
Name: the names of all the passengers, which might give some information like if there are some people are related based on the last names. But to simplify things up at this stage, I will pass this feature.
Ticket and Cabin: too many levels with unknown information.

Filling in missing values
--------------------------------------------------------------------------
From EDA, we know there are some missing value in "Age", "Cabin" and "Embarked" variables. Since we are not going to use "Cabin" feature, we will just fill in "Age" and "Embarked." We will fill the missing values in "Age" using the median age and fill the missing value in "Embarked" with "S" since there are only 2 values missing and "S" is the most represent in the dataset.

Log transformation of the fare
--------------------------------------------------------------------------
From the histograms, we can see that the distribution of "Fare" is highly right-skewed. For dealing with highly-skewed positive data, one of the strategies that can be used is log-transformation, so the skewness will be less. Since the minimum is 0, we will add 1 to the raw value, so there will not be any errors when using log-transformation.

One Hot Encoding for categorical features
--------------------------------------------------------------------------
We will use One Hot Encoding on the categorical features to transform them into numbers.

Model training and model evaluation
--------------------------------------------------------------------------
Here we will put model training and model evaluation in one part since Yellowbrick is a very good package that can wrap the model and creates good visualization of the model performance, making model evaluation much easier and fun.
Before we train the model, we will need to split the data into 2 sets: training and validation. We will use the training dataset to train the model and use the validation dataset to evaluate the model.

Model training and evaluation visualisation using Yellowbrick
--------------------------------------------------------------------------
Since the purpose of this project is to predict if a passenger has survived or not, it's a classification problem. There are lots of algorithms that can be used to do classification modeling. Here we will use logistic regression.
There are also lots of evaluation metrics you can use to evaluate your model for classification problem. Here we will use Confusion Matrix, precision, recall, F1 score, and ROC curve.

Confusion matrix
With Yellowbrick, we can create a visual confusion matrix that will allow us to easily see how well we were able to predict and compute our accuracy score.

Precision, Recall and F1-Score
We can also visually generate a classification report, which includes precision, recall, and F1 score for our classification model.

ROC curve and AUC
In addition to the previous two methods, we can also evaluate our classification model using a ROC curve for each class.

Conclusion
--------------------------------------------------------------------------
In this post, We have used the Titanic dataset. Although the model we trained looked good already, there are still lots of opportunities to improve.
