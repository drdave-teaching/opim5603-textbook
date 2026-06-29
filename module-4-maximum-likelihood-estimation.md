# Module 4 — Maximum Likelihood Estimation

Maximum likelihood for statistical estimation: given the data, what parameter values most likely generated it? We use analytical and numerical methods, and connect MLE directly to fitting regression models.

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **MLE and Regression R** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module4/MLE_and_Regression_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module4/MLE_and_Regression_R.ipynb)
:::

## 4.1 MLE Theory

### Video 1: Intro to Statistical Estimation

**Overview.** How to upload a .csv file from your computer desktop to the local runtime. Using dnorm() to calculate the likelihood of observing a datapoint from a normal distribution. Likelihood is not the same as probability, but it is closely related.

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: How to Calculate Likelihood and Log-Likelihood

**Overview.** The difference between likelihood and log-likelihood. When multiplying a bunch of small numbers together (product (pi) operator), it gets difficult for a computer (and humas) to keep track of all of those digits. Instead, we can calculate the log-likelihood and sum them up (sum (sigma) operator). The log-likelihood will be a negative number. Careful: students often get confused with this - we want to maximize log likelihood - and maximizing the log likelihood means selecting the most positive value (even if it's a small negative number).

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Analytical vs. Numeric Approaches for MLE

**Overview.** We just saw that the sample mean is MLE of the population mean - how do analytical methods work for the Bernoulli and Poisson distributions? Spoiler alert - the answer is pretty boring - the MLE estimate of pi (prob of success) is just count of successes/total successes; the MLE estimate of lambda for a Poisson distribution is just the mean value…

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: data2.csv, Zero-Inflated Poisson and the need for Numeric Approaches

**Overview.** Let's explore how things can start to break down when our distribution isn't as simple as a Bernoulli and Poisson distribution. Introduction to numeric approaches and the 'bbmle' library and the mle2() function.

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Estimating parameters from different distributions (normal, Poisson, zero-inflated Poisson)

**Overview.** How to use user-written functions for log-likelihood and the 'bbmle' package to estimate the mean and standard deviation of a distribution. The importance of providing bounds and initial values to aid convergence. Note that 'bbmle' requires you return a -LL even though it gives you -2LL in the output. Why -2LL? The reason -2LL is show in the output is because this quantity is used to calculate model fit metrics (like AIC - more on this later.)

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Confidence Intervals and Standard Errors estimates

**Overview.** How to obtain a confidence interval for the parameter estimate to better reflect the population via bootstrapping (repeated sampling). The basic idea is simple. Generate a bootstrap sample and compute the parameter estimate using maximum likelihood approach. Repeat this for a large number of bootstrap samples, each time computing the estimate value. This will create the sampling distribution of the parameter estimate values. Use the sampling distribution to generate the confidence intervals for the parameter estimate.

*✍️ Full narrative coming from the lecture transcript.*

## 4.2 MLE and Regression

### Video 1: Linear regression with Corn.csv (Pt. 1)

**Overview.** We start to tie maximum likelihood estimation to regression - and everything is going to hinge upon our error term… our quest begins! We start our lecture by trying to relate crop yield to fertilizer amounts. Our hope is that crop yield goes up as fertilizer goes up. A linear model is a great choice here for our problem. Though not discussed yet, by using a linear model we are assuming our response (target) variable is normally distributed. We also assume that our ERROR term is normally distributed. We will exploit this error term in the next video in order to get a model that can relate fertilizer to crop yield.

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: Linear regression with Corn.csv (Pt. 2)

**Overview.** Understanding linear regression and model fit. We learn that SSE are the sum of the squared errors from our fitted model, and we hope that this quantity is smaller than SST (the sum of the squared errors from the baseline model). Using SSE and SST, we can calculate the R2 value (it is 1 - SSE/SST). We show that our model can explain 20% of the variance that we observe.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Closing Thoughts on Linear Regression (Pt. 3)

**Overview.** Suggestions for getting 'bbmle' to converge and an overview of the four assumptions of linear models. (1) target variable must be normally distributed; (2) no 'fanning' of predictions on actual vs. predicted (we want constant variance, no heteroskedasticity). (3) power terms/interaction terms are included so there's no systemic problems with model fit. (4) no time dependence in the data (assume independence among observations).

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: Regression with binary outcomes with Admit.csv (Pt. 1)

**Overview.** We show how, even though our target variable only takes on 0/1 values, that we can apply the 'logistic transformation' which allows us to leverage the linear form of the model. When you are trying to predict a 0/1 value, you are using a 'generalized linear model' (GLM) that is known as a logistic regression.

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Understanding logistic regression and model fit (Pt. 2)

**Overview.** A gentle introduction to the interpretation of the logistic regression coefficients and application of information criterion (AIC, BIC) for model comparison - it is all a function of -2LL!

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Regression for count outcomes with student.csv

**Overview.** A gentle introduction to the fitting of a Poisson model (for target variables that are COUNT DATA from 0 to +Inf). Interpretation of coefficients and calculation of AIC using a built-in R function.

*✍️ Full narrative coming from the lecture transcript.*

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **Likelihood vs. log-likelihood** — we maximize log-likelihood (sums, not products).
- Estimate a distribution's parameters with `bbmle::mle2()` using bounds + initial values.
- MLE underpins **linear, logistic, and Poisson regression** coefficients.
- Linear model vs. **generalized linear model (GLM)** — and when to use each.
```

---

## 📌 Lecture key points

*Quick reference — one card per lecture (click to expand).*

:::{admonition} Intro to Statistical Estimation
:class: note dropdown
How to upload a .csv file from your computer desktop to the local runtime. Using dnorm() to calculate the likelihood of observing a datapoint from a normal distribution. Likelihood is not the same as probability, but it is closely related.
:::

:::{admonition} How to Calculate Likelihood and Log-Likelihood
:class: note dropdown
The difference between likelihood and log-likelihood. When multiplying a bunch of small numbers together (product (pi) operator), it gets difficult for a computer (and humas) to keep track of all of those digits. Instead, we can calculate the log-likelihood and sum them up (sum (sigma) operator). The log-likelihood will be a negative number. Careful: students often get confused with this - we want to maximize log likelihood - and maximizing the log likelihood means selecting the most positive value (even if it's a small negative number).
:::

:::{admonition} Analytical vs. Numeric Approaches for MLE
:class: note dropdown
We just saw that the sample mean is MLE of the population mean - how do analytical methods work for the Bernoulli and Poisson distributions? Spoiler alert - the answer is pretty boring - the MLE estimate of pi (prob of success) is just count of successes/total successes; the MLE estimate of lambda for a Poisson distribution is just the mean value…
:::

:::{admonition} data2.csv, Zero-Inflated Poisson and the need for Numeric Approaches
:class: note dropdown
Let's explore how things can start to break down when our distribution isn't as simple as a Bernoulli and Poisson distribution. Introduction to numeric approaches and the 'bbmle' library and the mle2() function.
:::

:::{admonition} Estimating parameters from different distributions
:class: note dropdown
How to use user-written functions for log-likelihood and the 'bbmle' package to estimate the mean and standard deviation of a distribution. The importance of providing bounds and initial values to aid convergence. Note that 'bbmle' requires you return a -LL even though it gives you -2LL in the output. Why -2LL? The reason -2LL is show in the output is because this quantity is used to calculate model fit metrics (like AIC - more on this later.)
:::

:::{admonition} Confidence Intervals and Standard Errors estimates
:class: note dropdown
How to obtain a confidence interval for the parameter estimate to better reflect the population via bootstrapping (repeated sampling). The basic idea is simple. Generate a bootstrap sample and compute the parameter estimate using maximum likelihood approach. Repeat this for a large number of bootstrap samples, each time computing the estimate value. This will create the sampling distribution of the parameter estimate values. Use the sampling distribution to generate the confidence intervals for the parameter estimate.
:::

:::{admonition} Linear regression with Corn.csv
:class: note dropdown
We start to tie maximum likelihood estimation to regression - and everything is going to hinge upon our error term… our quest begins! We start our lecture by trying to relate crop yield to fertilizer amounts. Our hope is that crop yield goes up as fertilizer goes up. A linear model is a great choice here for our problem. Though not discussed yet, by using a linear model we are assuming our response (target) variable is normally distributed. We also assume that our ERROR term is normally distributed. We will exploit this error term in the next video in order to get a model that can relate fertilizer to crop yield.
:::

:::{admonition} Linear regression with Corn.csv
:class: note dropdown
Understanding linear regression and model fit. We learn that SSE are the sum of the squared errors from our fitted model, and we hope that this quantity is smaller than SST (the sum of the squared errors from the baseline model). Using SSE and SST, we can calculate the R2 value (it is 1 - SSE/SST). We show that our model can explain 20% of the variance that we observe.
:::

:::{admonition} Closing Thoughts on Linear Regression
:class: note dropdown
Suggestions for getting 'bbmle' to converge and an overview of the four assumptions of linear models. (1) target variable must be normally distributed; (2) no 'fanning' of predictions on actual vs. predicted (we want constant variance, no heteroskedasticity). (3) power terms/interaction terms are included so there's no systemic problems with model fit. (4) no time dependence in the data (assume independence among observations).
:::

:::{admonition} Regression with binary outcomes with Admit.csv
:class: note dropdown
We show how, even though our target variable only takes on 0/1 values, that we can apply the 'logistic transformation' which allows us to leverage the linear form of the model. When you are trying to predict a 0/1 value, you are using a 'generalized linear model' (GLM) that is known as a logistic regression.
:::

:::{admonition} Understanding logistic regression and model fit
:class: note dropdown
A gentle introduction to the interpretation of the logistic regression coefficients and application of information criterion (AIC, BIC) for model comparison - it is all a function of -2LL!
:::

:::{admonition} Regression for count outcomes with student.csv
:class: note dropdown
A gentle introduction to the fitting of a Poisson model (for target variables that are COUNT DATA from 0 to +Inf). Interpretation of coefficients and calculation of AIC using a built-in R function.
:::
