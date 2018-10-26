# Ames Housing Data and Kaggle Challenge

# Executive Summary
We used a Kaggle dataset to predict what features were best for predicting housing prices. This project made me focus a lot on feature engineering and removing multicollinear features. I also tranformed the dataset using standard scaler and ran models before and after the transformation to compare them. 

The models I have used in this project are lassoCV, random forest, and gradient boost. For each model, I used gridsearch to find the most optimal parameters and these were the results:
<img src = "https://github.com/wsuh60/ames_housing_prices/blob/master/Assets/schema.png">

# EDA & Data Cleaning
The data was from Kaggle and it was divided as train and test already. When I saw the data, I decided to drop the property ID features because they were unncessary. I also dropped the sale price because that was the y value I needed to predict.

After I dropped features, I used kernel density estimation (KDE) to detect any interesting patterns. I noticed that:

1) A lot of remodeling/additions to homes happened around 2000.
2) A lot of homes were built around 2000.
3) Most common Overall condition is 5.
4) Most homes have 3 bedrooms above ground.
5) Most garages were built in 2000. (and most are for 2 cars).
6) Looks like June is the most popular month for homes sold.

After KDE, I looked into categorical data and noticed the following:

1) North Ames had a lot homes built (over 300)!
2) Most homes were sold as warranty deed.

As for data cleaning, whenever the numerical categories had a NaN value, I imputed a large negative number (-999 in this case) because it would be easy to discard them later or have them not affect my models due to its negative value.

## Iteration 1 (GridSearch without StandardScaler (submission.csv)):
I used Random Forest without any parameter optimization and received a score of .86 and when I used gridsearch, I received a score of .88 with n_estimator of 85.

## Iteration 2 (Gridsearch with StandardScaler (submission2.csv)):
I tried the same process but scaled my data. I also used two different models. The random forest model provided a score of .88 while the gradient boost provided .91.

## Iteration 3 (Gridsearch Standard Scale and one pair of Multicollinearity columns taken out (submission3.csv)):
For the third iteration, I scaled my data and took out three multicollinear features: Year Built, Year Remod/Add, and Gr Liv Area. I ran the same models again to see what would happen.

The random forest model return a score of .86 and the gradient boost returned a score of .89. It performed worse than Iteration 2.

## Iteration 4 (Feature Selection using LassoCV and SelectFromModel (submission4.csv)):
I used "Select From Model" combined with LassoCV with a threshold of .25 to find five most important features. Those features were: 'Overall Qual', 'Year Built', 'BsmtFin SF 1', 'Gr Liv Area', and 'Garage Area'. 

I used those features and imputed them to the random forest and gradient boost models to see what scores I would get.

Random forest provided a score of .87 and gradient boost returned a score of .88. 

# Conclusion
This exercise persuaded me that working with more data is useful. Even when I thought I was optimizing my models by dropping multicollinear features or only using the top five most important features, the models performed worse. 

Instead of dropping features, it is better to engineer features -- such as combining all the sq. feet of the living room, garage, bathroom, bedroom, etc. 
