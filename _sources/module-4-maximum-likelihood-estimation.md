# Chapter 4 — Maximum Likelihood Estimation

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **MLE and Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module4/MLE_and_Regression_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module4/MLE_and_Regression_R.ipynb)
:::


Hypothesis testing asked, "given a claim about the population, is my sample extreme?" **Maximum likelihood estimation (MLE)** flips the question: *given the data, what population most likely produced it?* This chapter builds likelihood from scratch, optimizes it three ways, and then delivers the payoff — MLE is the engine under **regression**, including the **generalized linear models** (logistic, Poisson) you'll use constantly.

## 4.1 Likelihood vs. probability

Back with continuous distributions we avoided point estimates and `dnorm`. Now we use it on purpose: `dnorm(x, mean, sd)` is the **likelihood** of observing one data point under an assumed mean and SD. If the data clusters around 5 and you *assume* the mean is 10, the low observations become very unlikely — that mismatch is exactly what likelihood measures. Likelihood is *like* a probability (bounded 0–1) but describes the parameters given the data, not the other way around.

## 4.2 The likelihood function and log-likelihood

Assuming observations are **independent**, the likelihood of the *whole* sample is the product of each point's `dnorm` — just like "the probability of rolling three sixes is 1/6 × 1/6 × 1/6":

$$L(m) = \prod_{i=1}^{n} P(x_i \mid m)$$

Multiplying 56 tiny numbers underflows, so we take the **log** and *sum* instead — the **log-likelihood**. Maximizing it (the **least-negative** value) gives the **maximum likelihood estimate**.

```r
LL_mean <- function(m) sum(dnorm(x, mean = m, sd = 2, log = TRUE))  # log-likelihood
ms  <- seq(0, 10, by = 0.1)
res <- sapply(ms, LL_mean)
plot(ms, res, type = "l");  ms[which.max(res)]   # the peak ≈ the sample mean
```

The grid search peaks at the **sample mean** — a first hint that MLE recovers the estimators you already know.

## 4.3 Three ways to optimize

Every MLE problem is: **specify the model form → write the likelihood → take the log → optimize.** Three ways to do that last step:

- **Grid search** — try many parameter values and keep the best (fine for one parameter, hopeless for many).
- **Analytical** — calculus: set the derivative of the log-likelihood to zero (a flat slope = the top of the hill). For a **Bernoulli** the MLE of π is *successes/total*; for a **Poisson** the MLE of λ is the *mean*. Tidy, but only for simple cases.
- **Numeric** — let an optimizer search the parameter space with gradients. We use **`bbmle::mle2()`**, which *minimizes*, so we feed it the **negative** log-likelihood.

## 4.4 Over-dispersion and the zero-inflated Poisson

A core Poisson assumption is **mean = variance = λ**. In `data2`, `x1` honors that, but `x2` is swamped with **zeros** (variance ≈ 2× the mean) — **over-dispersion**. A plain Poisson with λ = the mean puts too much mass in the "1" bin and misses reality. The fix is a **zero-inflated Poisson**: a **Bernoulli** part for the structural zeros times a **Poisson** part for the counts (think safe vs. reckless drivers — most file zero claims; the rest follow a Poisson). The math gets intractable by hand, which is exactly why we lean on **numeric optimization**.

## 4.5 From MLE to regression — the linear model

Here's the light-bulb. Write the linear model with its **error term**:

$$y = \beta_0 + \beta_1 x_1 + \varepsilon, \qquad \varepsilon \sim \text{Normal}(0, \sigma)$$

Rearranged, the error `y − β₀ − β₁x` is normally distributed — so we can **maximize the likelihood of the errors** and solve for β₀, β₁, and σ *simultaneously* with `mle2()`. On the corn/nitrate data, the **baseline** (predict the mean) has SST with σ = 2171; the fitted model gets σ = **1940** (smaller error). `R² = 1 − SSE/SST = 0.20` — fertilizer explains ~20% of yield. `lm()` reproduces the same coefficients, the **slope** is the marginal effect (one unit of nitrate → +51.5 yield), and each coefficient's **p-value** tests H₀: coef = 0.

```{admonition} bbmle in practice
:class: tip
Give `mle2()` sensible **starting values** (coefficients at 0, σ at the target's SD) and **bounds** (no negative σ — use the `L-BFGS-B` method). It's gradient-based, so it can land in a local optimum — try a few starts. In real work you'll just call **`lm()`/`glm()`**; the MLE machinery is what's running underneath.
```

Linear-model assumptions to honor before you trust inference: **(1)** a normally distributed target, **(2)** homoscedastic errors (no fanning in actual-vs-error), **(3)** errors uncorrelated with the predictors, **(4)** independent observations (no time dependence).

## 4.6 Generalized linear models: logistic & Poisson regression

When the target isn't continuous-normal, **transform it** and keep the linear core (a GLM):

- **Logistic regression** (binary target — grad-school `admit`): the **logistic transform** `π = eˣ/(1 + eˣ)` turns log-odds into a linear model. `mle2` estimates the coefficients; **stars = significant** (GRE wasn't). Interpret on the **odds** scale: a coefficient of 0.88 means `e^0.88 = 2.41×` the odds of admission per +1 GPA.
- **Poisson regression** (count target — `days absent` in `student.csv`): model `log λ` as linear, then **exponentiate** coefficients for a *multiplicative* effect (e.g., `e^-0.6 = 0.45×` fewer absences as progress rises).

```{admonition} Comparing models: −2 log-likelihood → AIC/BIC
:class: note
`mle2` reports **−2 log-likelihood** as a fit metric (smaller is better). **AIC** and **BIC** add it to a penalty for the number of parameters (BIC also for sample size). The numbers are meaningless alone — they matter when you **compare** models: if dropping an insignificant term barely changes the fit, prefer the simpler model (**parsimony**).
```

## 4.7 Confidence intervals by bootstrap

One sample gives one MLE. To put uncertainty around it, **bootstrap**: resample the data *with replacement* many times, re-estimate the parameter each time, and read the 2.5th/97.5th percentiles. For `data1$x1`, the mean MLE is 5.73 with a 95% bootstrap CI of roughly **5.2–6.27** — the CLT idea from Chapter 2, reused.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **MLE** asks which parameters make the observed data most likely; `dnorm`/`dpois` give per-point **likelihood**.
- Likelihood is a **product** over independent points → use **log-likelihood** (a sum) and **maximize** it (least-negative).
- Optimize by **grid search**, **analytical calculus** (Bernoulli MLE = successes/total; Poisson MLE = mean), or **numeric `bbmle::mle2`** (minimize the *negative* log-likelihood).
- **Over-dispersion** (variance ≫ mean, excess zeros) calls for a **zero-inflated Poisson** (Bernoulli × Poisson).
- Regression *is* MLE on a **normal error term**: `mle2` (or `lm`) solves β's and σ; check **R²**, the slope's meaning, the p-value, and the **four LM assumptions**.
- **GLMs**: logistic (logistic transform, interpret **odds** via `e^coef`) and Poisson (`log λ` linear, interpret multiplicatively); compare models with **−2 log-likelihood → AIC/BIC** and favor parsimony.
- Put a **bootstrap** confidence interval around any MLE.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Intro to Statistical Estimation
:class: note dropdown
- Estimation flips testing: *given the data, what population most likely generated it?*
- `dnorm(x, mean, sd)` = the **likelihood** of one point under assumed parameters.
- Assume the wrong mean (e.g., 10 for data centered at 5) and low values become very unlikely.
- Likelihood is like a probability (0–1) but about parameters given data.
- Visualize a point's likelihood on the assumed curve.
:::

:::{admonition} How to Calculate Likelihood and Log-Likelihood
:class: note dropdown
- Independence ⇒ sample **likelihood = product** of each point's `dnorm`.
- Tiny products underflow ⇒ take the **log** and **sum** (`log = TRUE`).
- **Maximize** log-likelihood = pick the least-negative value.
- Grid search over m peaks at the **sample mean**.
- Wrap it in a function and `sapply` over candidate values, then plot.
:::

:::{admonition} Analytical vs. Numeric Approaches for MLE
:class: note dropdown
- Steps: model form → likelihood → log-likelihood → optimize.
- **Analytical**: set the derivative to 0 — Bernoulli MLE = successes/total; Poisson MLE = mean.
- A zero slope is the top of the likelihood hill.
- **Numeric**: optimizers (gradients) scale to many parameters.
- You won't do the calculus by hand — `bbmle` handles it.
:::

:::{admonition} data2.csv, Zero-Inflated Poisson & Numeric Approaches
:class: note dropdown
- Poisson assumes **mean = variance**; excess zeros break that (over-dispersion).
- `data2$x2`: variance ≈ 2× mean ⇒ a plain Poisson misfits.
- **Zero-inflated Poisson** = Bernoulli (structural zeros) × Poisson (counts).
- Safe-vs-reckless-driver intuition for the two processes.
- Analytical math gets intractable ⇒ use numeric `mle2`.
:::

:::{admonition} Estimating parameters from different distributions
:class: note dropdown
- `bbmle::mle2()` with a negative-log-likelihood function + starting values.
- Estimate mean alone, or **mean and σ together** (needs bounds: no negative σ, `L-BFGS-B`).
- Poisson λ and zero-inflated-Poisson (λ and p) likewise.
- Summary gives estimate, standard error, z, and −2 log-likelihood.
- Wrong model form can "wash out" (e.g., p → 0) — read the output.
:::

:::{admonition} Confidence Intervals and Standard Errors estimates
:class: note dropdown
- One sample → one MLE; quantify it with a **bootstrap**.
- Resample **with replacement** to the same size, re-estimate many times.
- The spread of estimates is the sampling distribution → a **95% CI**.
- `data1$x1`: mean 5.73, CI ≈ 5.2–6.27.
- Reuses the CLT/bootstrapping idea from Module 2.
:::

:::{admonition} Linear regression with Corn.csv (Pt. 1)
:class: note dropdown
- Goal: predict **yield** from **nitrate**; the payoff tying MLE to regression.
- **Baseline** = predict the mean; error = **SST** (sum of squared totals).
- The linear model `y = β₀ + β₁x + ε` hinges on the **error term** `ε ~ Normal(0, σ)`.
- Hope: fitted σ < the baseline SD (2171).
- Squaring errors penalizes big misses.
:::

:::{admonition} Linear regression with Corn.csv (Pt. 2)
:class: note dropdown
- `mle2` solves **β₀, β₁, σ simultaneously** by maximizing the likelihood of the errors.
- Result: σ = 1940 < 2171, slope = 51.5 (marginal effect of nitrate).
- `lm()` reproduces the same coefficients — a sanity check.
- **R² = 1 − SSE/SST = 0.20**: nitrate explains ~20% of yield.
- p-value tests H₀: coefficient = 0.
:::

:::{admonition} Closing Thoughts on Linear Regression (Pt. 3)
:class: note dropdown
- `bbmle` tips: start coefficients at 0, σ at the target's SD; add bounds; try multiple starts (local optima).
- In practice use **`lm`/`glm`**, not `bbmle`.
- Four LM assumptions: normal target, **homoscedastic** errors, errors uncorrelated with X, independent obs.
- Biggest one: make the **target roughly normal** before fitting.
- Assumptions are what make **inference** (not just prediction) valid.
:::

:::{admonition} Regression with binary outcomes with Admit.csv (Pt. 1)
:class: note dropdown
- Binary target (`admit`) ⇒ **logistic regression** (a GLM).
- **Logistic transform** `π = eˣ/(1+eˣ)` keeps the model linear in log-odds.
- `mle2` estimates β's; **stars** flag significance (GRE wasn't significant).
- Baseline likelihood uses `π^(#1s)·(1−π)^(#0s)`; track **−2 log-likelihood**.
- Higher GPA ↑ admission; higher (worse) class rank ↓ it.
:::

:::{admonition} Understanding logistic regression and model fit (Pt. 2)
:class: note dropdown
- **Odds** = π/(1−π); log-odds is the linear quantity.
- Interpret coefficients via `e^coef`: +1 GPA ⇒ **2.41×** the odds of admission.
- Drop insignificant predictors (GRE) and refit.
- **AIC/BIC** from −2 log-likelihood penalize extra parameters (and samples).
- Smaller AIC/BIC + similar fit ⇒ choose the simpler model.
:::

:::{admonition} Regression for count outcomes with student.csv
:class: note dropdown
- Count target (**days absent**) ⇒ **Poisson regression**.
- Model `log λ` as linear, then **exponentiate** coefficients.
- `e^-0.6 = 0.45×` fewer absences as progress rises (multiplicative).
- All predictors significant; ignore/interpret the intercept loosely.
- Compare with −2 log-likelihood / AIC / BIC (meaningful only vs another model).
:::
