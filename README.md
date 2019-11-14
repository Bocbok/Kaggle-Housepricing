# Kaggle - HousePricing

For this kaggle competition I abitrary choosed tu use the Lasso regression algorithm because of previous attempts giving me good results.

My methodology was : 
* Get the data
* Clean the missing values
* Encode the categorical values
* Scale the numerical values
* Separate the train data in 2 sets : 1 for training and one for validation
* Attempt various configurations of the Lasso algorithm

The objective is to have a baseline eg a first prediction with the raw data and then tweak step by step the features to see any improvment.

## Lasso regression with no feature engineering

First just by using the data as it is with the Lasso algorithm we get a rmse of ~0.19 with a better result if we normalize the data.

This is my baseline, if I submit these predictions to Kaggle I get a score of ~0.18. This mean that my estimation on my validation set approximate well the kaggle score.

![](https://i.imgur.com/E8lir7P.png)

Encoding the numerical values and replacing them by an Int representing the category gave the same result.


## OneHot encoding

Then I chose to OneHot encode the categorical features. 

OneHot encoding will create a new feature for each categorical value that can take a feature and fill it with 0 and 1.

:::info
Example : 
| id | animal | age |
| -------- | -------- | -------- |
| 1     | cat     | 1     |
| 2     | dog     | 5     |

After OneHot encoding : 



| id | age | animal_cat | animal_dog |
| -------- | -------- | -------- | -------- |
| 1     | 1     | 1     | 0 |
| 2     | 5     | 0     | 1 |


:::

With this encoding I get a better rmse of 0.15.
I tried to normalize the values myself in the cell 28 but we see that we  have the same result as when we normalize it with the hyperparameter of Lasso in the cell 27.

![](https://i.imgur.com/xId12ad.png)

## Count encoding

I also tried the Count encoding but the rmse was greater than with OneHot encoding.
With the Count encoding we encode the categorical with the value count of this category. In the example below, all dogs are encoded with the value 3 because there 

:::info
Example : 

| id | animal | age |
| -------- | -------- | -------- |
| 1     | cat     | 1     |
| 2     | dog     | 5     |
| 3     | dog     | 4     |
| 4     | dog     | 4     |

After OneHot encoding : 



| id | age | animal_count |
| -------- | -------- | -------- |
| 1     | 1     | 1     |
| 2     | 5     | 3     |
| 3     | 4     | 3     |
| 4     | 4     | 3     |


:::

![](https://i.imgur.com/y4MfcYH.png)

## Log transform of the target

To improve my rmse I used the log value of the 'SalePrice' to train and test my algorithm.
We see that without encoding the categorical data we get a better result than without the log transformation.

![](https://i.imgur.com/w0YfT0X.png)

Now that we see that the log transformation of the target improve our baseline rmse we can try the different encodings.

### Count encoding

If we count encode the categorical data and use a log transformation of the target we go down to ~0.14.

![](https://i.imgur.com/CV92IE1.png)

### OneHot encoding

OneHot encoding and Log transformation doesn't seem to work better than without encoding.

![](https://i.imgur.com/W0EZwpj.png)


## Log transform and Cross validation

Final step, I use a Cross Validation of 5 folds to attempt to improve my model. I keep the Log transformation since it gave the best results so far.

### Count encoding

Using the Count encoding which gave the best results with the log transform we are able to go down to a ~0.12 rmse with a R2 score of ~0.88 with a 5 folds cross validation and normalized data.

![](https://i.imgur.com/FDZ4UB0.png)

### OneHot encoding

The best results are given by the cross validation of 5 folds with data normalized and encoded with a OneHotEncoder.

We manage to get an rmse of 0.10 and a R2 score of 0.92.

![](https://i.imgur.com/q5vGlbI.png)

## Conclusion

These rmse and R2 scores are calculated on a 20% set I extracted from the train set given by kaggle. By testing our best predictions (eg: Log transform + OneHot encoding + Cross validation + Normalization) on the kaggle platform we get the following result : 

![](https://i.imgur.com/E6Rblva.png)

Finally to have a small final boost we can retrain our regression algorithm but this time on the all train dataset eg without splitting 20% for a validation set.

Final submission : 

![](https://i.imgur.com/Sq6G0ok.png)

