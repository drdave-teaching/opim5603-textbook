# Module 2 — Probability Distributions

How probability distributions describe data behavior. We master the four core functions — d (density), p (cumulative), q (quantile), r (random) — for discrete (binomial, Poisson) and continuous (uniform, normal, exponential) distributions, then build to sampling distributions, the Central Limit Theorem, and confidence intervals.

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **CheatSheet pbinom** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_pbinom.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_pbinom.ipynb)
- **CheatSheet ttest for Confidence Intervals** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_ttest_for_Confidence_Intervals.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_ttest_for_Confidence_Intervals.ipynb)
- **Continuous Distributions** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Continuous_Distributions.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Continuous_Distributions.ipynb)
- **Discrete Distributions** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Discrete_Distributions.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Discrete_Distributions.ipynb)
- **Estimation and Confidence Intervals** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Estimation_and_Confidence_Intervals.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Estimation_and_Confidence_Intervals.ipynb)
- **Sampling Methods and CLT** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Sampling_Methods_and_CLT.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Sampling_Methods_and_CLT.ipynb)
:::

## 2.1 Discrete Probability Distributions

### Video 1: Introduction to discrete distributions (Pt. 1)

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 2: Introduction to discrete distributions (Pt. 2)

**Overview.** Using Monte Carlo simulation to create a probability distribution. Introduction to the binomial distribution (heads and tail; successful vs. unsuccessful operation). Advanced use of R code to sum values in a probability distribution (don't worry - it gets easier!).

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 3: Mean and Variance of a Discrete Distribution

**Overview.** If someone gives you a discrete probability distribution - you are able to calculate the mean and variance of the distribution. You can use R to do this. Mean is just value times probability then sum. Variance is value minus mean, square the difference, multiply times probability, then sum. Note how the probability distribution can be (2, 8, 10) and does not need to be (0, 1, 2)!

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 4: Binomial Distribution (Pt. 1 - d is for density)

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 5: Binomial Distribution (Pt. 2 - p is for percentile, q is for quantile)

**Overview.** P stands for percentile, which means we are using the cumulative density function (summing all values from the left, up to and including the value of interest!) Q stands for quantile, which means you return the value of the distribution where this is true ('tell me the value of the distribution where 90% of the values will be equal to or below this value'). We also try out complements (1-X) which is not the same things as compliments, and also double check our qbinom() functions by using pbinom().

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 6: Poisson Distribution (D, P, Q for count data)

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 7: Wrapping Up

**Overview.** Quick wrap up and discussion on where we are going next week.

*✍️ Full narrative coming from the lecture transcript (video being located).*

## 2.2 Continuous Probability Distributions

### Video 1 - (Introduction to Continuous Variables)

**Overview.** Setting up your environment, and a comparison of the mean and variance for a continuous distribution vs. a discrete distribution.

*✍️ Full narrative coming from the lecture transcript (video being located).*

### Video 2 - (Uniform Distribution)

**Overview.** We'll introduce one of the simpler distributions, the uniform distribution (also known as the rectangle distribution). Your old tools d, p, q, and r work here - we'll apply it to an example where students are waiting for a bus to arrive on campus.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3 - (Normal Distribution)

**Overview.** The normal distribution is used all over the place and has many desirable properties and attributes. D, p, q and r will be our tools for answering interesting questions about the normal distribution.

*✍️ Full narrative coming from the lecture transcript.*

### Video 4 - (A Quick Refresh and Intro to Standard Normal Distribution)

**Overview.** A quick refresh on probability concepts for continuous distributions, a practice problem for normal distribution, and an overview of z scores and how any normal distribution (with a mean and sd) can be converted into the standard normal distribution (with a mean =0 and sd=1).

*✍️ Full narrative coming from the lecture transcript.*

### Video 5 - (The Empirical Rule and Exponential Distribution)

**Overview.** A deeper understanding of the empirical rule (and standard deviations) and an example of how to use the exponential distribution.

*✍️ Full narrative coming from the lecture transcript.*

## 2.3 Sampling Methods Confidence Intervals

### Video 1: Sampling Methods and CLT (Pt. 1)

**Overview.** Explanation of various sampling methods, motivation for the central limit theorem using the 'women' dataset. Note how the population mean and the 'mean of means' lie directly on top of each other!

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: Sampling Methods and CLT (Pt. 2)

**Overview.** Definition of a sampling distribution, formal definition of the central limit theorem and standard error.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Sampling Methods and CLT (Pt. 3)

**Overview.** Some examples in action to show that the central limit theorem really holds true for ANY distribution of ANY shape.

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: Estimation and Confidence Intervals (Pt. 1)

**Overview.** A motivating introduction of why you shouldn't just report the point estimate - use a confidence interval!

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Estimation and Confidence Intervals (Pt. 2)

**Overview.** We will explore the general formula for making a confidence interval for the population mean when the standard deviation is KNOWN. In practice, you will probably NEVER know the population standard deviation. But you should be familiar with the formula, z distribution (standard normal distribution) and z related values, and how this all ties back to the Central Limit Theorem.

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Estimation and Confidence Intervals (Pt. 3)

**Overview.** A worked example for when the population standard deviation is known (use the z-distribution). Then, a worked example for when the population standard deviation is unknown (use the t-distribution!) Note that t should be a little bigger than z when sample size is small, this is because we are MORE UNCERTAIN for a given level of confidence.

*✍️ Full narrative coming from the lecture transcript.*

### Video 7: Estimation and Confidence Intervals (Pt. 4)

**Overview.** Let's extend what we have learned to proportions. Proportions are weird quantities - there is no standard deviation involved! We'll show you that the math is not too hard - you just need to manipulate your sample proportion and sample size to calculate your confidence interval. We'll also show how to calculate sample size needed given constraints (like you must be within $10 and a level of 95% confidence) - this holds true for both population means and proportions.

*✍️ Full narrative coming from the lecture transcript.*

## Wrap-up

```{admonition} Key takeaways
:class: tip
- Discrete vs. continuous distributions; compute a distribution's **mean and variance**.
- Master **d / p / q / r** for binomial, Poisson, uniform, normal, exponential.
- The **Central Limit Theorem**: the mean of sample means approximates the population mean.
- Build **confidence intervals** for the mean (σ known → z; σ unknown → t).
```

---

## 📌 Lecture key points

*Quick reference — one card per lecture (click to expand).*

:::{admonition} Introduction to discrete distributions
:class: note dropdown
Key points will be distilled from the lecture transcript.
:::

:::{admonition} Introduction to discrete distributions
:class: note dropdown
Using Monte Carlo simulation to create a probability distribution. Introduction to the binomial distribution (heads and tail; successful vs. unsuccessful operation). Advanced use of R code to sum values in a probability distribution (don't worry - it gets easier!).
:::

:::{admonition} Mean and Variance of a Discrete Distribution
:class: note dropdown
If someone gives you a discrete probability distribution - you are able to calculate the mean and variance of the distribution. You can use R to do this. Mean is just value times probability then sum. Variance is value minus mean, square the difference, multiply times probability, then sum. Note how the probability distribution can be (2, 8, 10) and does not need to be (0, 1, 2)!
:::

:::{admonition} Binomial Distribution
:class: note dropdown
Key points will be distilled from the lecture transcript.
:::

:::{admonition} Binomial Distribution
:class: note dropdown
P stands for percentile, which means we are using the cumulative density function (summing all values from the left, up to and including the value of interest!) Q stands for quantile, which means you return the value of the distribution where this is true ('tell me the value of the distribution where 90% of the values will be equal to or below this value'). We also try out complements (1-X) which is not the same things as compliments, and also double check our qbinom() functions by using pbinom().
:::

:::{admonition} Poisson Distribution
:class: note dropdown
Key points will be distilled from the lecture transcript.
:::

:::{admonition} Wrapping Up
:class: note dropdown
Quick wrap up and discussion on where we are going next week.
:::

:::{admonition} Video 1 -
:class: note dropdown
Setting up your environment, and a comparison of the mean and variance for a continuous distribution vs. a discrete distribution.
:::

:::{admonition} Video 2 -
:class: note dropdown
We'll introduce one of the simpler distributions, the uniform distribution (also known as the rectangle distribution). Your old tools d, p, q, and r work here - we'll apply it to an example where students are waiting for a bus to arrive on campus.
:::

:::{admonition} Video 3 -
:class: note dropdown
The normal distribution is used all over the place and has many desirable properties and attributes. D, p, q and r will be our tools for answering interesting questions about the normal distribution.
:::

:::{admonition} Video 4 -
:class: note dropdown
A quick refresh on probability concepts for continuous distributions, a practice problem for normal distribution, and an overview of z scores and how any normal distribution (with a mean and sd) can be converted into the standard normal distribution (with a mean =0 and sd=1).
:::

:::{admonition} Video 5 -
:class: note dropdown
A deeper understanding of the empirical rule (and standard deviations) and an example of how to use the exponential distribution.
:::

:::{admonition} Sampling Methods and CLT
:class: note dropdown
Explanation of various sampling methods, motivation for the central limit theorem using the 'women' dataset. Note how the population mean and the 'mean of means' lie directly on top of each other!
:::

:::{admonition} Sampling Methods and CLT
:class: note dropdown
Definition of a sampling distribution, formal definition of the central limit theorem and standard error.
:::

:::{admonition} Sampling Methods and CLT
:class: note dropdown
Some examples in action to show that the central limit theorem really holds true for ANY distribution of ANY shape.
:::

:::{admonition} Estimation and Confidence Intervals
:class: note dropdown
A motivating introduction of why you shouldn't just report the point estimate - use a confidence interval!
:::

:::{admonition} Estimation and Confidence Intervals
:class: note dropdown
We will explore the general formula for making a confidence interval for the population mean when the standard deviation is KNOWN. In practice, you will probably NEVER know the population standard deviation. But you should be familiar with the formula, z distribution (standard normal distribution) and z related values, and how this all ties back to the Central Limit Theorem.
:::

:::{admonition} Estimation and Confidence Intervals
:class: note dropdown
A worked example for when the population standard deviation is known (use the z-distribution). Then, a worked example for when the population standard deviation is unknown (use the t-distribution!) Note that t should be a little bigger than z when sample size is small, this is because we are MORE UNCERTAIN for a given level of confidence.
:::

:::{admonition} Estimation and Confidence Intervals
:class: note dropdown
Let's extend what we have learned to proportions. Proportions are weird quantities - there is no standard deviation involved! We'll show you that the math is not too hard - you just need to manipulate your sample proportion and sample size to calculate your confidence interval. We'll also show how to calculate sample size needed given constraints (like you must be within $10 and a level of 95% confidence) - this holds true for both population means and proportions.
:::
