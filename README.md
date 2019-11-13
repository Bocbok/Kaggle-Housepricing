# Kaggle - House Prices: Advances Regression Techniques

## Introduction

To complete this Kaggle competition I used this [tutorial](https://www.kaggle.com/dejavu23/house-prices-eda-to-ml-beginner) written by [dejavu23](https://www.kaggle.com/dejavu23).

## Methodology

In a first time we explore the data in order to familiarize ourself with the data structures, the number of features and we visualize them.

We then have a look at the relation between each feature and the target eg the sale price.
Thanks to the correlation matrix we can determine which feature is strongly correlated to the sale price and also which features are correlated between each others.

We can then in a second part do some feature engineering such as applying log function to some features or convert categorical columns to numerical. We can also choose to drop some features based on their correlation with the target.
Finally we scale the values of the data so every value is scaled on a normal distribution between 0 and 1.

In the last part we test some regression models and tweak their hyper-parameters thanks to GridSearchCV.
We compare the performance of each model based on the RMSE.
We then choose a model or a combination of models to submit our predictions.

## Conclusion

At final we use a combination of 4 models : 
* Lasso
* Elastic Net
* Random Forest
* Stochastic Gradient Descent

We get the prediction by computing the mean of the prediction of each model.

![](https://i.imgur.com/RhJ01Q9.png)

Finally when submitting our predictions on Kaggle we get a score of 0.14660 which is not perfect but is a good start.

What we can do to improve the score : 
* Add features we removed to see if they improve the result
* Better fine-tuning our models
* Try other models

With this project I learned that it is important to analyze and tweak the data before trying to fit a model on it and not just throw all the features as they are to a neural network and expect a good result.

I learned a lot of plot methods to visualize data which help a lot in ML. I also learned a lot about correlation matrix and how they can be used to understand the problem and the data.
