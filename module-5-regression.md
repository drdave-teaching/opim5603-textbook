# Chapter 5 — Regression

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Correlation and Simple Linear Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Correlation_and_Simple_Linear_Regression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Correlation_and_Simple_Linear_Regression.ipynb)
- **Recipe: Simple Linear Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_SimpleLinearRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_SimpleLinearRegression.ipynb)
- **Recipe: Multiple Linear Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_MultipleLinearRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_MultipleLinearRegression.ipynb)
- **Recipe: Logistic Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_LogisticRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_LogisticRegression.ipynb)
- **Recipe: Stepwise Logistic Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_Stepwise_LogisticRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_Stepwise_LogisticRegression.ipynb)
- **Recipe: Poisson Regression** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_PoissonRegression.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module5/Recipe_PoissonRegression.ipynb)
- **Categorical Data Analysis (Nominal)** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module6/Categorical_Data_Analysis_Nominal_Data.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module6/Categorical_Data_Analysis_Nominal_Data.ipynb)
:::


This capstone ties the whole course together. We move from **correlation** to **simple** and **multiple linear regression**, extend to **generalized linear models** (logistic and Poisson), and finish with **categorical data analysis** (chi-square). Throughout, the theme is **inference**: not just predicting, but understanding and defending what drives the outcome.

## 5.1 Correlation and simple linear regression

The **correlation coefficient** `r` (−1 to +1) measures the *strength of a linear relationship*; `cor.test()` even tests whether it's significantly different from zero (a t-test with `df = n − 2`). But beware: correlation is not causation.

```{admonition} Correlation ≠ causation
:class: warning
Strong correlations can be **spurious** — donkey populations and PhDs granted, peanut and aspirin consumption. A significant `r` says two variables *move together*, never that one *causes* the other.
```

**Least squares** fits the line that minimizes squared error: slope `b = r · (s_y / s_x)`, intercept `a = ȳ − b·x̄`. (For a linear model with normal errors, least squares and MLE give the **same** answer.) Then we test the slope: `t = b / SE_b`, where `SE_b`'s numerator is the **standard error of the estimate** `S_yx`. A neat result — in simple regression the **slope test and the correlation test produce the identical t and p-value**, and `R² = r²`.

```r
m <- lm(sales ~ calls, data = df)
summary(m)                 # slope, SE, t, p, R²
predict(m, newdata, interval = "confidence")   # mean response
predict(m, newdata, interval = "prediction")   # a single new case (wider)
```

A **confidence interval** estimates the *mean* response for given X; a **prediction interval** covers a *single new* observation and is always wider (the formula differs by a `+1`). If the target is skewed, a **log transform** can dramatically improve fit (the golf-winnings example jumps from R² 0.61 to 0.93).

## 5.2 Multiple linear regression

More predictors, same machinery. Use the clean `y ~ .` syntax ("everything else predicts y"), read **R²**, and prune **insignificant predictors one at a time** (drop the highest p-value, refit, repeat). Watch the sign convention: a **residual = actual − predicted**, so an *under*-estimate is *positive*.

Two preprocessing best practices: **transform the target** toward normality (check with the Anderson-Darling test in `goftest`; pick a power with **Tukey's ladder** / `car::powerTransform`), and optionally **standardize X** (z-score or, Dave's preference, min-max so every column lives on 0–1).

```{admonition} Multicollinearity wrecks inference — check VIF
:class: warning
**Correlated predictors** add no information, destabilize coefficients (even flipping signs), and can make you delete the wrong variable. Compute the **variance inflation factor** `VIF_j = 1/(1 − R²_j)`; drop any predictor with **VIF > 5**, highest first, then refit. (In *prediction*-only data-science work you may not care — but a stats class cares about **inference**.)
```

Once predictors are uncorrelated, replace manual p-pruning with **stepwise selection** (`stepAIC`, forward or backward) — it adds/removes terms to minimize **AIC** (= −2·log-likelihood + 2k), favoring **parsimony**. Evaluate with **MAE / RMSE / MAPE**, an **actual-vs-predicted** plot (the 45° line), and confidence/prediction intervals. The full **soup-to-nuts recipe**: read → explore → full model → VIF prune → stepwise → error metrics → actual-vs-predicted → inference.

## 5.3 Generalized linear models

When the target isn't continuous-normal, keep the linear core and **transform** (a GLM).

**Logistic regression** (binary target). Most of the work is **data cleaning**: coerce mistyped columns to numeric, drop NAs/ID columns, **balance the classes** (downsample the majority), and recode the target to 0/1. Fit with `glm(..., family = binomial)`, then **exponentiate coefficients** to read them as **odds** (a coefficient giving `e^β = 1.80` is a ~80% increase in the odds). Evaluate with the **confusion matrix** → accuracy, precision, recall, AUC. Prune insignificant predictors iteratively (Dave's affectionate "p-hacking") or let **`stepAIC`** do it.

**Poisson regression** (count target). Fit with `family = poisson`, modeling `log λ` as linear and **exponentiating** coefficients for a *multiplicative* effect. Encode categoricals as **k−1 dummies** (`fastDummies`); an `NA` coefficient flags a **linear combination** (e.g., total meds = prescribed + non-prescribed). Watch **over-dispersion** (variance ≫ mean) — if the deviance/df ratio is well above 1, the standard errors are wrong and you'd reach for **quasi-Poisson** (at the cost of losing AIC/log-likelihood).

```{admonition} Stats vs. data science
:class: note
Two mindsets share these tools. **Inference** (this course): keep models clean — check VIF, prune to significant predictors, interpret coefficients. **Prediction** (black-box ML): throw everything in, standardize, and optimize accuracy while ignoring the coefficients. Same `glm`, different goals.
```

## 5.4 Special topics — categorical data analysis (chi-square)

Not every relationship needs a regression. For **nominal** (unordered) categories, the **chi-square** distribution lets us compare **observed vs. expected frequencies**. It's never negative, right-skewed, and parameterized by **degrees of freedom** based on the number of *categories*, not the sample size. The statistic is always

$$\chi^2 = \sum \frac{(O - E)^2}{E}$$

Three tests:

- **Goodness of fit, equal frequencies** — do restaurant entrée choices differ from uniform? `df = categories − 1`.
- **Goodness of fit, unequal frequencies** — local vs. national hospitalization rates; expected = proportion × total. **Rule:** every expected cell ≥ 5, or combine categories (small expected cells falsely inflate χ²).
- **Test of independence** — are two categorical variables related (smoking & drinking; hometown & behavior)? `E = row total × column total / grand total`, `df = (rows − 1)(cols − 1)` (Weldon's 26,000 dice rolls turn out biased).

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **Correlation** `r` measures linear strength (≠ causation); test it, and remember in SLR the **slope test = correlation test** and **R² = r²**.
- **Least squares** = MLE under normal errors; **CI** (mean response) vs **PI** (single case, wider); **transform** skewed targets.
- **MLR**: prune insignificant terms; **residual = actual − predicted**; kill multicollinearity with **VIF > 5**, then **stepAIC** for parsimony; report **MAE/RMSE/MAPE** + actual-vs-predicted.
- **Logistic GLM**: clean + balance data, `family = binomial`, **exponentiate to odds**, judge with the **confusion matrix**.
- **Poisson GLM**: `family = poisson`, `log λ` linear, **exponentiate** for multiplicative effects; dummy-encode categoricals; watch **over-dispersion**.
- **Chi-square** for nominal data: `χ² = Σ(O−E)²/E`; goodness-of-fit (equal/unequal) and **independence**; mind df and the expected-≥5 rule.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Correlation Analysis
:class: note dropdown
- `r` ∈ [−1, 1] measures the **strength of a linear** relationship.
- Compute by hand or with `cor()`; test it with `cor.test()` (t, `df = n − 2`).
- **Correlation ≠ causation** — beware spurious correlations.
- A 0.76 is a moderately strong positive trend.
:::

:::{admonition} Regression Analysis
:class: note dropdown
- **Least squares** fits the line minimizing squared error.
- Slope `b = r · s_y/s_x`; intercept `a = ȳ − b·x̄`.
- Same estimates as **MLE** when errors are normal.
- The line passes through (x̄, ȳ); predictions fall on it.
:::

:::{admonition} Testing the Significance of the Slope
:class: note dropdown
- `t = b / SE_b`; `SE_b` has the **standard error of estimate** `S_yx` as numerator.
- Two-tailed test, `df = n − 2`.
- In SLR this gives the **same t and p as the correlation test**.
- `lm()` + `summary()` reports it directly.
:::

:::{admonition} R2
:class: note dropdown
- **Coefficient of determination** `R² = 1 − SSE/SST` (variance explained).
- In simple regression, `R² = r²`.
- `S_yx` (std error of estimate) drives both `SE_b` and the intervals.
- Better fit ⇒ smaller `S_yx`, bigger `R²`.
:::

:::{admonition} Confidence Intervals vs. Prediction Intervals
:class: note dropdown
- **CI** = the *mean* response for given X; **PI** = a *single new* case.
- Formulas differ only by a `+1` ⇒ the **PI is always wider**.
- Both shrink when the model fits well (small `S_yx`).
- `predict(m, interval = "confidence" / "prediction")`.
:::

:::{admonition} Transforming Data
:class: note dropdown
- A skewed target hurts fit; a **log transform** can fix it.
- Golf winnings: R² jumps **0.61 → 0.93** after `log`.
- Transforming changes interpretation (you're modeling `log y`).
- Also clean dirty fields (strip commas, coerce to numeric).
:::

:::{admonition} Following a Recipe — Simple Linear Regression
:class: note dropdown
- Workflow: read → clean → explore → `lm` → error metrics → actual-vs-predicted.
- Fit `log(winnings) ~ score`; interpret slope and R² (0.94).
- **MAE / MAPE / RMSE** for performance; bias for over/under.
- Plot the 45° actual-vs-predicted line (+ CI/PI for SLR).
:::

:::{admonition} Getting Started with Boston Housing and MLR
:class: note dropdown
- Predict `medv` (dependent) from many **independent** variables.
- Convert the `chas` 0/1 indicator to a **factor**; `str`/`summary` recon.
- Check the **target's distribution** before modeling.
- Independence of predictors matters — correlation check comes later.
:::

:::{admonition} Distribution of Target Variable and Transformations
:class: note dropdown
- A normal target ⇒ normal errors (a key assumption).
- **Anderson-Darling** (`goftest`) tests normality quantitatively.
- **Tukey's ladder** / `car::powerTransform` picks the power (e.g., cube root).
- Transform improves fit but complicates coefficient interpretation.
:::

:::{admonition} Standardization Techniques
:class: note dropdown
- **z-score** = (x − mean)/sd; **min-max** = (x − min)/range (0–1).
- Puts predictors on a level playing field (optional in stats).
- Dave prefers **min-max** (coefficients read as per-1% change).
- Helpful for stability/prediction; less so for inference.
:::

:::{admonition} Model Fitting, Interpretation and Iterative Variable Selection
:class: note dropdown
- `y ~ .` hack models against all other columns (clean data only).
- Read **R²**; prune the **highest p-value** predictor, refit, repeat.
- **Residual = actual − predicted** (under-estimates are positive).
- Check residuals are ~normal and centered on zero.
:::

:::{admonition} Error Metrics and Intervals
:class: note dropdown
- **MAE** (avg absolute error), **MAPE** (percent), **RMSE** (penalizes outliers).
- Residual vs error sign convention (residual = actual − predicted).
- Confidence intervals on **coefficients** (≈ estimate ± 2·SE).
- CI vs PI for predictions; the recipe summary for MLR.
:::

:::{admonition} Stepwise Variable Selection and AIC for Model Comparison
:class: note dropdown
- **Correlated predictors** destabilize inference → compute **VIF**, drop > 5.
- `VIF_j = 1/(1 − R²_j)` — how predictable a predictor is from the rest.
- **stepAIC** (forward/backward) prunes to minimize **AIC** (parsimony).
- Game plan: full model → VIF → stepwise → evaluate.
:::

:::{admonition} Recipe: Multiple Linear Regression
:class: note dropdown
- Soup-to-nuts: read → full model → VIF prune → stepAIC → metrics → inference.
- Drop `tax` (highest VIF), then stepwise removes weak terms.
- Compare AICs; favor the simpler model (parsimony).
- Interpret signs (rooms ↑ price, NOx ↓ price); note underestimated high-value homes.
:::

:::{admonition} Introduction to logistic regression and data clean-up (Pt. 1)
:class: note dropdown
- Logistic = a **GLM** for a 0/1 target.
- Clean: coerce the `?`-laden numeric column, drop NAs and the **ID** column.
- **Balance classes** by downsampling the majority (set a seed).
- Recode the target (2/4 → 0/1) before fitting.
:::

:::{admonition} Fitting the (full) logistic regression and interpreting its output (Pt. 2)
:class: note dropdown
- `glm(class ~ ., family = binomial)`; **stars** mark significance.
- Predictions are probabilities → **round at 0.5** to 0/1.
- **Exponentiate coefficients** to read **odds** (e.g., 1.80 = +80% odds).
- Positive coef ↑ odds; ignore the intercept's meaning.
:::

:::{admonition} Calculate error metrics, remove insignificant predictors, reinterpret (Pt. 3)
:class: note dropdown
- **Confusion matrix** → accuracy, precision, recall (+ AUC).
- Precision = TP/(TP+FP); recall = TP/(TP+FN).
- Iteratively drop the highest-p predictor, refit ("p-hacking" lovingly).
- Compare full vs reduced by **AIC** (lower wins; nearly equal fit).
:::

:::{admonition} Fitting a stepwise logistic regression model
:class: note dropdown
- `MASS::stepAIC` automates backward elimination for a GLM.
- Correlated/weak predictors drop out as AIC falls.
- Reduced model ≈ full model accuracy with ~half the predictors.
- Optionally remove a last borderline term for all-significant predictors.
:::

:::{admonition} Fitting a Poisson model (Pt. 1 — fastDummies)
:class: note dropdown
- Poisson = count target (0 → ∞, integers); mean = variance = λ.
- Encode categoricals as **k − 1 dummies** with `fastDummies` (avoid collinearity).
- Drop the original factor columns after dummying.
- Reference category is the one left out.
:::

:::{admonition} Fitting a Poisson model (Pt. 2 — Evaluation)
:class: note dropdown
- `glm(..., family = poisson)`, model `log λ`; **exponentiate** for multiplicative effects.
- **`NA` coefficient** = a linear combination (medicine = prescribed + non-prescribed) — drop one.
- Evaluate with MAE/RMSE/MAPE, actual-vs-predicted; `stepAIC` to prune.
- Watch **over-dispersion** (deviance/df ≫ 1) → consider **quasi-Poisson**.
:::

:::{admonition} Introduction to Categorical Data Analysis
:class: note dropdown
- For **nominal** (unordered) categories vs **ordinal** (ranked).
- The **chi-square** distribution: never negative, right-skewed, df by **categories**.
- Visualize with `table()`, `prop.table()`, and bar plots.
- Sets up goodness-of-fit and independence tests.
:::

:::{admonition} Goodness of Fit with Equal Frequencies
:class: note dropdown
- Compare observed counts to a **uniform** expectation (restaurant entrées).
- `χ² = Σ (O − E)²/E`; right-tailed test, `df = categories − 1`.
- Big O−E gaps ⇒ reject "all equal."
- Verify with base R `chisq.test()`.
:::

:::{admonition} Goodness of Fit with Unequal Frequencies
:class: note dropdown
- Expected counts from given proportions × total (local vs national).
- Same `χ² = Σ(O−E)²/E`, `df = categories − 1`.
- **Rule:** each expected cell ≥ 5, or **combine** categories.
- Small expected cells falsely inflate χ² and over-reject.
:::

:::{admonition} Chi-square Test for Independence
:class: note dropdown
- Tests whether **two categorical variables** are related (smoking & drinking).
- Expected `E = (row total × column total) / grand total`.
- `df = (rows − 1)(columns − 1)`; feed a table to `chisq.test()`.
- Weldon's 26,000 dice rolls come out **biased** (distributions don't match).
:::
