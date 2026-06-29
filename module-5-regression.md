# Module 5 — Regression

Relationships between variables: correlation, simple and multiple linear regression, and generalized linear models (logistic, Poisson). We close with categorical data analysis using the chi-square distribution.

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Correlation and Simple Linear Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Correlation_and_Simple_Linear_Regression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Correlation_and_Simple_Linear_Regression.ipynb)
- **Recipe LogisticRegression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_LogisticRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_LogisticRegression.ipynb)
- **Recipe MultipleLinearRegression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_MultipleLinearRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_MultipleLinearRegression.ipynb)
- **Recipe PoissonRegression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_PoissonRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_PoissonRegression.ipynb)
- **Recipe SimpleLinearRegression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_SimpleLinearRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_SimpleLinearRegression.ipynb)
- **Recipe Stepwise LogisticRegression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_Stepwise_LogisticRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_Stepwise_LogisticRegression.ipynb)
- **Categorical Data Analysis Nominal Data** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module6/Categorical_Data_Analysis_Nominal_Data.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module6/Categorical_Data_Analysis_Nominal_Data.ipynb)
:::

## 5.1 Correlation and Simple Linear Regression

### Video: Correlation Analysis

**Overview.** Let's go back to some of our earlier EDA and quantitatively calculate whether or not there is a linear relationship (positive or negative) between X and Y. We calculate the correlation coefficient (r ) and then test whether or not the correlation is significantly different than zero (which requires us to run a t-test). The most important thing to take away here is the calculation of the test statistic, t, and the calculation of the p-value (remember, we need to multiply by 2… this is because we could've calculated the correlation between X and Y as well as Y and X… this relates to the symmetry of a two-tailed test!)

*✍️ Full narrative coming from the lecture transcript.*

### Video: Regression Analysis

**Overview.** We will discuss how we relate correlation to regression - in fact, simple linear regression is a function of r (which means r is used in the regression equation). 'r' is going to be used in the slope (b), the intercept (a) is a function of the slope. Study these equations and start to see the relationship between everything.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Testing the Significance of the Slope

**Overview.** We learn some new terminology and learn how to define and calculate the 'standard error of the slope' (sb) - which is a function of your actual (Y) vs predicted (Y-hat) results. We calculate sb and then calculate the test statistic, t = b/sb, and then run a two-tailed test with the t distribution (with df = n-2, due to symmetry). We reject the null hypothesis that the population slope is actually 0. Be careful - we do a slightly different example than the narrative in the book here - but our numbers match the printout in the book!!!

*✍️ Full narrative coming from the lecture transcript.*

### Video: R2

**Overview.** There is a big love triangle going on here - you have three quantities - sb, syx, and R2. syx is the numerator of sb. SSE is the numerator of the syx. R2 is a function of SSE. Hence, the R2, syx and sb are all a function of how well the model is fitting the data. Only the R2 and sb are presented in the summary(model) code… and hence, the precision/uncertainty (sb) of your estimated coefficient (b) is a function of how well the model fits the data (R2). WOOT! So, if the points on the scatterplot are close to the regression line, you will probably have a small standard error of the slope (sb), a big R2 and a small p-value.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Confidence Intervals vs. Prediction Intervals

**Overview.** A confidence interval is used to answer the question ' how many sales could the average person make if they make 25 calls? (n=Inf)'. A prediction interval answers the question 'how many sales could this person standing right next to me make if she made 25 phone calls? (n=1)'. Of course, we are going to be MORE UNCERTAIN when we are talking about a single person, so our prediction interval is going to be larger than our confidence interval. We also demonstrate how to calculate a confidence interval by hand, and show that it's way easier to just use R to do these calculations. Graphing is a little bit involved but the plot looks nice.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Transforming Data

**Overview.** We show the value of transforming your target variable (via a log transform) such that we force it to be more normally distributed, which results in a better fitting model.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Following a Recipe - Simple Linear Regression

**Overview.** A clean real-world example of how to perform a simple linear regression.

*✍️ Full narrative coming from the lecture transcript.*

## 5.2 Multiple Linear Regression

### Video: Getting Started with Boston Housing and Multiple Linear Regression

**Overview.** Comparison of simple vs. multiple linear regression; introduction to the Boston Housing dataset; exploratory data analysis and summary statistics. A quick peek at the distribution of the target variable and motivation for whether to change it or not.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Distribution of Target Variable and Transformations

**Overview.** A key assumption of linear models is that your target variable/dependent variable/Y variable follows a normal distribution. Visual inspection is typically accepted here, but we can be quantitative instead of qualitative. We can use the Anderson-Darling test from the goftest package to test whether or not our target variable is normally distributed. We discuss Tukey's ladder of transformations to understand the transformations available to use to coerce our 'medv' column to follow a normal distribution. We use the 'car' package and the powertransform() function to let R tell us what we should do to our target variable so that it follows a normal distribution.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Standardization Techniques

**Overview.** A quick comparison of z-score vs. min/max scaling. Z-score tells you how many observations away from the mean your data point is, vs. min/max tells you which percentile of the distribution the data point is.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Model Fitting, Interpretation and Iterative Variable Selection

**Overview.** Let's build our first multiple linear regression and then delete variables one at a time based on p-values. This is a first generation approach to modeling, which is valid but a lot of manual work to do the updating. After we delete insignificant variables, we look at the actual vs. predicted scatterplot, the distribution of residuals (to ensure the univariate distribution of residuals is essentially normally distributed), and a scatterplot of actual (X) vs. residuals to make sure that errors are randomly distributed.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Error Metrics and Intervals (for model parameters and predictions)

**Overview.** Everything we learned about error metrics (MAE, RMSE, MAPE) and intervals (confidence vs. prediction intervals) applies here. We conclude with the common steps for fitting a multiple linear regression.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Stepwise Variable Selection and AIC for Model Comparison

**Overview.** An overview of the problems with correlated predictors and how we can be more efficient by evaluating variance inflation factors (VIF) instead of correlation values. Then we will run a stepwise regression such that we choose a combination of X variables that improves (lowers) our AIC.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Recipe: Multiple Linear Regression

**Overview.** A soup-to-nuts, concise example of how to perform a multiple linear regression with VIF and stepwise.

*✍️ Full narrative coming from the lecture transcript.*

## 5.3 Generalized Linear Models

### Video: Introduction to logistic regression and data clean-up (Pt. 1)

**Overview.** We will read in the Wisconsin Breast Cancer data from an online repository and clean it up for modeling (delete the ID column, address any missing or erroneous data and recode the target variable from 2 and 4 to 0 and 1).

*✍️ Full narrative coming from the lecture transcript.*

### Video: Fitting the (full) logistic regression and interpreting its output (Pt. 2)

*✍️ Full narrative coming from the lecture transcript.*

### Video: Calculate error metrics, remove insignificant predictors, and then reinterpret logistic regression (Pt. 3)

**Overview.** Common error metrics for a regression problem include accuracy Insignificant predictors in the model can cause unwanted noise - it is best to remove them if they are not contributing anything. Start with the highest p-value and delete one at a time. We then use AIC for model comparison (lower is always better) and choose the reduced model - which had SLIGHTLY worst accuracy with half the predictors ( but if we get essentially the same accuracy with less predictors, that's a good thing!)

*✍️ Full narrative coming from the lecture transcript.*

### Video: Fitting a stepwise logistic regression model

**Overview.** Stepwise takes all the hard work out of fitting a model - just let it rip! You will probably get a 'very good' fitting model with (mostly) significant predictors. If you have anything insignificant at the end, delete one at a time.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Fitting a Poisson model (Pt. 1 - fastDummies)

**Overview.** Poisson regression is for when your target variable takes on values between 0 and +Inf and takes on integer values (count data). Whenever you have a variable with multiple categories (say, 'color' = ('red', 'green', 'blue')... you will want to recode this as three new dummy variables for red (0/1), green (0/1) or blue (0/1). Due to collinearity, you will only need k-1 categories as a dummy variable (if it's not red and if it's not green then it has to be blue!) In this video, we will process the data for modeling.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Fitting a Poisson model (Pt. 2 - Evaluation of Model Output)

**Overview.** In this video, we run the stepwise regression, interpret the model output and evaluate the quality of the predictions with error metrics and visualizations.

*✍️ Full narrative coming from the lecture transcript.*

## 5.4 Special Topics

### Video: Introduction to Categorical Data Analysis

**Overview.** In this notebook, we will cover three different flavors of categorical data analysis: 1) Chi-square Goodness-of-Fit Test: Equal Expected Frequencies; 2) Goodness-of-fit test: Unequal Expected Frequencies; 3) Chi-square Test for independence.Introduction to the chi-squared distribution and its properties.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Goodness of Fit with Equal Frequencies

**Overview.** We look at an example of a restaurant with 4 food categories - you are sampling people as they come out of the restaurant and ask them what they ate: fish, meat, chicken or pasta. Your job is to determine if there is a difference between the 4 categories or if they are all the same. You need to run a hypothesis test with the chi squared distribution which is parameterized by the number of categories (k) minus 1 degrees of freedom.  Solved by hand and then with one line of R code.

*✍️ Full narrative coming from the lecture transcript.*

### Video: Goodness of Fit with Unequal Frequencies

**Overview.** Not everything has equal frequencies! Is this example we show how we can compare distributions at the national and local level to determine if a policy is effective. We also discuss some pitfalls of chi-square and some rules of thumb to follow to ensure you don't erroneously reject the null hypothesis (remember - if expected frequency is smaller than 5, you need to combine groups or not run the test!)

*✍️ Full narrative coming from the lecture transcript.*

### Video: Chi-square Test for Independence

**Overview.** Is there a relationship between smoking and drinking? How about income and education? In this video, we show you how to test whether or not there is a difference between to types of categorical variables. We conclude with a brief discussion on 'Welden's Dice' - the poor guy rolled dice 26000 times for the purpose of creating an old school number generator - and it turns out, his dice were biased!!! So he unnecessarily rolled 26k dice.

*✍️ Full narrative coming from the lecture transcript.*

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **Correlation → regression**: r drives the slope; test the slope with a t-test.
- Model fit ties together **R², s(y·x), and the standard error of the slope**.
- **Multiple LR**: check normality of the target, scale, prune by p-value, then **VIF + stepwise/AIC**.
- **GLMs**: logistic (binary) and Poisson (counts); **chi-square** for categorical data.
```

---

## 📌 Lecture key points

*Quick reference — one card per lecture (click to expand).*

:::{admonition} Correlation Analysis
:class: note dropdown
Let's go back to some of our earlier EDA and quantitatively calculate whether or not there is a linear relationship (positive or negative) between X and Y. We calculate the correlation coefficient (r ) and then test whether or not the correlation is significantly different than zero (which requires us to run a t-test). The most important thing to take away here is the calculation of the test statistic, t, and the calculation of the p-value (remember, we need to multiply by 2… this is because we could've calculated the correlation between X and Y as well as Y and X… this relates to the symmetry of a two-tailed test!)
:::

:::{admonition} Regression Analysis
:class: note dropdown
We will discuss how we relate correlation to regression - in fact, simple linear regression is a function of r (which means r is used in the regression equation). 'r' is going to be used in the slope (b), the intercept (a) is a function of the slope. Study these equations and start to see the relationship between everything.
:::

:::{admonition} Testing the Significance of the Slope
:class: note dropdown
We learn some new terminology and learn how to define and calculate the 'standard error of the slope' (sb) - which is a function of your actual (Y) vs predicted (Y-hat) results. We calculate sb and then calculate the test statistic, t = b/sb, and then run a two-tailed test with the t distribution (with df = n-2, due to symmetry). We reject the null hypothesis that the population slope is actually 0. Be careful - we do a slightly different example than the narrative in the book here - but our numbers match the printout in the book!!!
:::

:::{admonition} R2
:class: note dropdown
There is a big love triangle going on here - you have three quantities - sb, syx, and R2. syx is the numerator of sb. SSE is the numerator of the syx. R2 is a function of SSE. Hence, the R2, syx and sb are all a function of how well the model is fitting the data. Only the R2 and sb are presented in the summary(model) code… and hence, the precision/uncertainty (sb) of your estimated coefficient (b) is a function of how well the model fits the data (R2). WOOT! So, if the points on the scatterplot are close to the regression line, you will probably have a small standard error of the slope (sb), a big R2 and a small p-value.
:::

:::{admonition} Confidence Intervals vs. Prediction Intervals
:class: note dropdown
A confidence interval is used to answer the question ' how many sales could the average person make if they make 25 calls? (n=Inf)'. A prediction interval answers the question 'how many sales could this person standing right next to me make if she made 25 phone calls? (n=1)'. Of course, we are going to be MORE UNCERTAIN when we are talking about a single person, so our prediction interval is going to be larger than our confidence interval. We also demonstrate how to calculate a confidence interval by hand, and show that it's way easier to just use R to do these calculations. Graphing is a little bit involved but the plot looks nice.
:::

:::{admonition} Transforming Data
:class: note dropdown
We show the value of transforming your target variable (via a log transform) such that we force it to be more normally distributed, which results in a better fitting model.
:::

:::{admonition} Following a Recipe - Simple Linear Regression
:class: note dropdown
A clean real-world example of how to perform a simple linear regression.
:::

:::{admonition} Getting Started with Boston Housing and Multiple Linear Regression
:class: note dropdown
Comparison of simple vs. multiple linear regression; introduction to the Boston Housing dataset; exploratory data analysis and summary statistics. A quick peek at the distribution of the target variable and motivation for whether to change it or not.
:::

:::{admonition} Distribution of Target Variable and Transformations
:class: note dropdown
A key assumption of linear models is that your target variable/dependent variable/Y variable follows a normal distribution. Visual inspection is typically accepted here, but we can be quantitative instead of qualitative. We can use the Anderson-Darling test from the goftest package to test whether or not our target variable is normally distributed. We discuss Tukey's ladder of transformations to understand the transformations available to use to coerce our 'medv' column to follow a normal distribution. We use the 'car' package and the powertransform() function to let R tell us what we should do to our target variable so that it follows a normal distribution.
:::

:::{admonition} Standardization Techniques
:class: note dropdown
A quick comparison of z-score vs. min/max scaling. Z-score tells you how many observations away from the mean your data point is, vs. min/max tells you which percentile of the distribution the data point is.
:::

:::{admonition} Model Fitting, Interpretation and Iterative Variable Selection
:class: note dropdown
Let's build our first multiple linear regression and then delete variables one at a time based on p-values. This is a first generation approach to modeling, which is valid but a lot of manual work to do the updating. After we delete insignificant variables, we look at the actual vs. predicted scatterplot, the distribution of residuals (to ensure the univariate distribution of residuals is essentially normally distributed), and a scatterplot of actual (X) vs. residuals to make sure that errors are randomly distributed.
:::

:::{admonition} Error Metrics and Intervals
:class: note dropdown
Everything we learned about error metrics (MAE, RMSE, MAPE) and intervals (confidence vs. prediction intervals) applies here. We conclude with the common steps for fitting a multiple linear regression.
:::

:::{admonition} Stepwise Variable Selection and AIC for Model Comparison
:class: note dropdown
An overview of the problems with correlated predictors and how we can be more efficient by evaluating variance inflation factors (VIF) instead of correlation values. Then we will run a stepwise regression such that we choose a combination of X variables that improves (lowers) our AIC.
:::

:::{admonition} Recipe: Multiple Linear Regression
:class: note dropdown
A soup-to-nuts, concise example of how to perform a multiple linear regression with VIF and stepwise.
:::

:::{admonition} Introduction to logistic regression and data clean-up
:class: note dropdown
We will read in the Wisconsin Breast Cancer data from an online repository and clean it up for modeling (delete the ID column, address any missing or erroneous data and recode the target variable from 2 and 4 to 0 and 1).
:::

:::{admonition} Fitting the
:class: note dropdown
Key points will be distilled from the lecture transcript.
:::

:::{admonition} Calculate error metrics, remove insignificant predictors, and then reinterpret logistic regression
:class: note dropdown
Common error metrics for a regression problem include accuracy Insignificant predictors in the model can cause unwanted noise - it is best to remove them if they are not contributing anything. Start with the highest p-value and delete one at a time. We then use AIC for model comparison (lower is always better) and choose the reduced model - which had SLIGHTLY worst accuracy with half the predictors ( but if we get essentially the same accuracy with less predictors, that's a good thing!)
:::

:::{admonition} Fitting a stepwise logistic regression model
:class: note dropdown
Stepwise takes all the hard work out of fitting a model - just let it rip! You will probably get a 'very good' fitting model with (mostly) significant predictors. If you have anything insignificant at the end, delete one at a time.
:::

:::{admonition} Fitting a Poisson model
:class: note dropdown
Poisson regression is for when your target variable takes on values between 0 and +Inf and takes on integer values (count data). Whenever you have a variable with multiple categories (say, 'color' = ('red', 'green', 'blue')... you will want to recode this as three new dummy variables for red (0/1), green (0/1) or blue (0/1). Due to collinearity, you will only need k-1 categories as a dummy variable (if it's not red and if it's not green then it has to be blue!) In this video, we will process the data for modeling.
:::

:::{admonition} Fitting a Poisson model
:class: note dropdown
In this video, we run the stepwise regression, interpret the model output and evaluate the quality of the predictions with error metrics and visualizations.
:::

:::{admonition} Introduction to Categorical Data Analysis
:class: note dropdown
In this notebook, we will cover three different flavors of categorical data analysis: 1) Chi-square Goodness-of-Fit Test: Equal Expected Frequencies; 2) Goodness-of-fit test: Unequal Expected Frequencies; 3) Chi-square Test for independence.Introduction to the chi-squared distribution and its properties.
:::

:::{admonition} Goodness of Fit with Equal Frequencies
:class: note dropdown
We look at an example of a restaurant with 4 food categories - you are sampling people as they come out of the restaurant and ask them what they ate: fish, meat, chicken or pasta. Your job is to determine if there is a difference between the 4 categories or if they are all the same. You need to run a hypothesis test with the chi squared distribution which is parameterized by the number of categories (k) minus 1 degrees of freedom.  Solved by hand and then with one line of R code.
:::

:::{admonition} Goodness of Fit with Unequal Frequencies
:class: note dropdown
Not everything has equal frequencies! Is this example we show how we can compare distributions at the national and local level to determine if a policy is effective. We also discuss some pitfalls of chi-square and some rules of thumb to follow to ensure you don't erroneously reject the null hypothesis (remember - if expected frequency is smaller than 5, you need to combine groups or not run the test!)
:::

:::{admonition} Chi-square Test for Independence
:class: note dropdown
Is there a relationship between smoking and drinking? How about income and education? In this video, we show you how to test whether or not there is a difference between to types of categorical variables. We conclude with a brief discussion on 'Welden's Dice' - the poor guy rolled dice 26000 times for the purpose of creating an old school number generator - and it turns out, his dice were biased!!! So he unnecessarily rolled 26k dice.
:::
