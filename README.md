# Vehicle-price-prediction-using-Linear-Regression
This project is to predict the used Vehicle price according to several parameters using linear Regression algorithum and I aiming to test my Linear rgression model assumption and sure it's satisfied.  

# Dataset:  
## Vehicle dataset: it is dataset for cars prices collected from websites  
This dataset contains information about used cars.  
This data can be used for a lot of purposes such as price prediction to exemplify the use of linear regression in Machine Learning.
Dataset consists of ```8 columns and 309 rows```.   
The columns in the given dataset are as follows:  
1-car_name  
2-year  
3-selling_price  
4-km_driven  
5-fuel  
6-seller_type  
7-transmission  
8-Owner  
dataset link: https://www.kaggle.com/datasets/nehalbirla/vehicle-dataset-from-cardekho  

# Data Preperation:  
1-Drop ```Car_Name``` column as we will not use it.  
2-I replaced ```Year``` column with the cars age attribute.To calculate the age, I consider the origin time to be 1 year older than the maximum model year.  
3-Outlier Detection : I found the outlier in the following columns ```selling_price,present_price,kms_driven,Transimision,seller_type, fuel_type,seller_type,Transimision```  
screenshot
4-Discover missing values: there were no missing values.  
5-Check Duplicates: I found 2 duplicates rows but I don't remove it as it is noraml to found duplicates in this case.  

# Data Preprocessing:  
1- For outliers I remove some of outliers only not all outliers after invistgae it as some measures cna be outliers and other may be cause by wrong measurments.
you will find it in section ```4.3 Outlier Detection``` 

2- Made Standard Scaler to the dataset

# Exploratory Data analysis:  
1- Categorical Distribution Univariate Analysis:  
**-There are 3 fuel_types petrol>dessel>CNG
-There are 2 seller_types dealer is more than individuals
-There are 2 Transsimision types the Manual one is the hiegher
**
screen chot

2-Nmerical variables univariate analysis: 

screen shot
**All the numerical variables is right skewed**

3- Categorical Encoding

# First Experiment: 
I made a basic linear Regression model and feed it the dataset and the results was good  
which give me a R2-Score = 0.88%  
screen shot 


# Second Experiment:  
In second experiment I invistgate the Linear Regression Assumptions to try to increase the model accuracy.  
## 1-Linearity:  
**This assumption assume there is a linear realtionship between the predictors(x) and the outcomes(y)
to detect the non linearity:**  
**To investigate this assumption:**
* **plots of actual vs. predicted values -> The desired output is that points is symmetric around the diagonal line**  
* **plots of tesiduals vs. predicted values -> The desired outcome is that points are symetrically distributed around horizontal line**  
screen shot 

**As we can see for the predicted vs. actual plot the it seems to be linear relation**  
**But if we look at the residuals vs. predicted the points are not symmetric about the line and the line is not horizontal also**    
**Also there is a big probelm here which in the variavnce not constant and we need it constant**  

## 2-Normality:  
**This assumes that the error terms of the model are normally distributed with a mean value of zero.**  
**To investigate this assumption:**  
* **Check residuals histogram**   
* **Quantile-Quantile probability plot -> plotting the residuals vs the order of statistic**  
* **Anderson-Darling test**  
screen shot  
**In QQ Plot of residuals:**  
* **The bow-shaped pattern of deviations from the diagonal implies that the residuals have excessive skewness.**
* **The s-shaped pattern of deviations from the diagonal implies excessive kurtosis of the residuals (there are either too many or too few large errors in both directions.)**  

## 3-No Multicollinearity:  
**Multicollinearity occurs when the independent variables are correlated to each other. It becomes difficult for the model to estimate the relationship between each independent variable and the dependent variable independently because the independent variables tend to change in unison. The coefficient estimates can swing wildly based on which other independent variables are in the model and they become very sensitive to small changes in the model. Therefore, the estimates will be less precise and highly sensitive to particular sets of data. This increases the standard error of the coefficients, which results in them potentially showing as statistically insignificant when they might actually be significant. On the other hand, the simultaneous changes of the independent variables can lead to large fluctuations of the target variable, which leads to the overfitting of the model and the reduction of its performance.**  

**To investigate this assumption:**   
* **Use a heatmap of the correlation**  
* **Examine the variance inflation factor (VIF)**  
screen shot  
**The higher the value of VIF the higher correlation between this variable and the rest. A rule of thumb is that if VIF > 10 then multicollinearity is high.**  
**Fuel_Type_Petrol is highly mutlicollinearity with others**  


## 4-No Autocorrelation of residuals:  
**This assumes no autocorrelation of the residuals.**  
**To investigate this assumption we can perform a Durbin-Watson test to determine whether the correlation is positive or negative:**  
* **The test statistic always has a value between 0 and 4**  
* **Values of 1.5 < d < 2.5 means that there is no autocorrelation in the data**  
* **Values < 1.5 indicate positive autocorrelation, values > 2.5 indicate negative autocorrelation**  

## 5-Homoscedasticity:  
**Homoscedasticity means that the residuals doesn’t change across all the values of the target variable.**  
screen   
**We can not see a fully uniform variance across our residuals because the orange line is not flat. The assumption is not satisfied.**  


### Solution For Linear Assumptions:  
**1-To satisfy the multicollinearity assuption, we remove the Fuel_Type_Petorl feature**  
**2-Make Box-Cox Transformtaion to the whole dataset to solve the Linearity assumption**  
**3-By applying polynomial regression, we will try to improve the satisfaction of homoscedasticity and normality of residuals**  
### Results:  
screen shots   

**The model R2-Score increased to be 98.1% which is great improvments**  



