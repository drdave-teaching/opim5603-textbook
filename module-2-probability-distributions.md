# Chapter 2 — Probability Distributions

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Discrete Distributions** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Discrete_Distributions.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Discrete_Distributions.ipynb)
- **Continuous Distributions** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Continuous_Distributions.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Continuous_Distributions.ipynb)
- **Sampling Methods and CLT** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Sampling_Methods_and_CLT.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Sampling_Methods_and_CLT.ipynb)
- **Estimation and Confidence Intervals** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Estimation_and_Confidence_Intervals.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/Estimation_and_Confidence_Intervals.ipynb)
- **Cheat Sheet — pbinom()** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_pbinom.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_pbinom.ipynb)
- **Cheat Sheet — t.test() for CIs** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_ttest_for_Confidence_Intervals.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module2/CheatSheet_ttest_for_Confidence_Intervals.ipynb)
:::


Probability distributions are how we describe the way data *behaves*. This chapter builds one toolkit you'll reuse everywhere: the four R functions **d / p / q / r**, applied first to **discrete** distributions (binomial, Poisson), then to **continuous** ones (uniform, normal, exponential). From there we reach the keystone idea of inferential statistics — the **Central Limit Theorem** — and turn it into **confidence intervals** that put honest uncertainty around an estimate.

```{admonition} Your four favorite letters: d, p, q, r
:class: note
Every distribution in R shares four functions. **d** = *density* (the bar height for a discrete value; a likelihood for a continuous one). **p** = *percentile/probability* (cumulative — sum from the left up to a value). **q** = *quantile* (the inverse of p — "what value sits at this percentile?"). **r** = *random* draws. Learn them once on the binomial (`dbinom`/`pbinom`/`qbinom`) and they transfer to every other distribution.
```

## 2.1 Discrete probability distributions

Discrete distributions describe **counts** — heads in 10 coin flips, defects per batch. Build intuition by simulation first: `sample()` flips a coin or rolls a die, and a **Monte Carlo** loop turns many trials into an empirical probability distribution.

Given any discrete distribution, two summaries matter:

- **Mean** = Σ (value × probability)
- **Variance** = Σ (value − mean)² × probability

The **binomial** counts successes in *n* independent trials (success probability π): `dbinom` for an exact count, `pbinom` for "k or fewer," `qbinom` for the inverse. Use **complements** (`1 - pbinom(...)`, or `lower.tail = FALSE`) for "more than," and check a `qbinom` answer by feeding it back through `pbinom`. The **Poisson** counts events per unit of time or area with rate λ; the trick is **rescaling λ** to the units in the question (e.g., golf balls landing in the yard per *afternoon* vs. per *hour*).

## 2.2 Continuous probability distributions

Continuous variables take any value in a range, so the probability of an *exact* point is zero — we always work with **ranges**.

```{admonition} dnorm is a likelihood, not a probability
:class: warning
For continuous distributions you cannot read a probability off a single point — `dnorm(3, ...)` returns a *likelihood*, which is undefined as a probability. Always ask for a **range**: `pnorm(3, ...)` ("≤ 3"), or a difference of two `pnorm` calls for an interval.
```

**Uniform (the "rectangle").** Parameterized by min `a` and max `b`. The density is constant — `1/(b - a)` — so every interval of equal width is equally likely. Mean = (a + b)/2 and SD = √((b − a)² / 12). The bus-stop example (a bus every 30 minutes, students arriving at random) is pure uniform: `punif` gives "wait ≤ 25 min," its complement gives "wait > 25 min," and a difference of two `punif` calls gives "wait between 10 and 15."

**Normal.** Parameterized by mean μ and SD σ: bell-shaped, symmetric, with mean = median = mode and tails that are asymptotic (approach but never touch zero). Same μ with different σ "fans" the curve; same σ with different μ slides the peak. `pnorm`/`qnorm` answer probability and quantile questions, and a Monte Carlo simulation lets you *eyeball-check* the math — and rediscover that ~68% of the mass sits within ±1 SD.

**Standard normal & z-scores.** Convert any normal to the standard normal with `z = (x − μ) / σ` — literally "how many SDs from the mean." It makes plots intuitive (the x-axis becomes −3…+3) and lets you reuse `pnorm`/`qnorm` with their defaults (mean 0, sd 1). The General Mills cereal-box weight example walks through converting limits to z and shading the region.

**Empirical rule & exponential.** On a normal curve the empirical rule is exact-ish: **68 / 95 / 99.7%** within ±1 / 2 / 3 SD. The **exponential** distribution is the continuous cousin of the Poisson — time-to-event from 0 → ∞ — using **rate = 1/λ** where λ is the mean (supermarket checkout time, power-supply time-to-failure, and the slightly evil warranty-design example).

## 2.3 Sampling, the Central Limit Theorem & confidence intervals

We sample because reaching a whole population is expensive or impossible (you can't poll every voter or count every blood cell). A **simple random sample** gives every element an equal chance; watch the `replace =` argument (with vs. without replacement changes everything). **Sampling error** is just population mean − sample mean for a given draw.

Here's the keystone experiment (the `women` dataset): draw **10,000 samples of size 5**, keep each sample's *mean*, and plot those 10,000 means.

```r
mean_dist <- replicate(10000, mean(sample(women$weight, size = 5, replace = TRUE)))
hist(mean_dist)
abline(v = mean(women$weight), col = "blue", lwd = 3)            # population mean
abline(v = mean(mean_dist),    col = "red",  lwd = 3, lty = 2)   # mean of means
```

Two things pop out: the **sampling distribution of the mean is normal**, and the **mean of means lands right on the population mean**. That's the **Central Limit Theorem** — and it holds *for any parent distribution* (the notebook proves it on uniform, exponential, and normal parents). The spread of that sampling distribution is the **standard error**, `σ/√n`, which shrinks as the sample grows.

```{admonition} n is the only lever you control
:class: tip
You can't change the population mean or σ — they're fixed by reality. The one knob you own is **n**. Because the standard error is σ/√n, collecting more data is the *only* way to tighten your estimate. And note: a **standard error is not a standard deviation** — it's the SD *of the sampling distribution of the mean*.
```

A **confidence interval** marries a point estimate to that uncertainty. When σ is **known**:

$$\bar{x} \pm z \cdot \frac{\sigma}{\sqrt{n}}$$

with `z = 1.96` for 95% and `2.58` for 99% (get any z from `qnorm`). When σ is **unknown** (almost always), use the sample SD `s` and the **t distribution**, parameterized by **degrees of freedom = n − 1**:

```r
z95 <- qnorm(0.975)              # 1.96  (sigma known)
t95 <- qt(0.975, df = n - 1)     # bigger for small n — the penalty
ci  <- xbar + c(-1, 1) * t95 * s / sqrt(n)
```

The t value is a **penalty for small samples** (more uncertainty when you don't know σ), and it **converges to z** as n grows — so for large samples the two are interchangeable. For **proportions** there's no SD; use `p̂ ± z·√(p̂(1−p̂)/n)` after checking `n·p̂ ≥ 5` and `n·(1−p̂) ≥ 5` (the union-merger example). Finally, you can **plan sample size**: rearrange the error formula to `n = (z·σ / E)²` for a mean (or the proportion analog, using 0.5 when p is unknown) — a tighter margin or higher confidence costs you more observations.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **d / p / q / r** work for every distribution — learn them on the binomial, reuse everywhere; use **complements** and check `q` with `p`.
- **Discrete** (binomial, Poisson): mean = Σ value·prob, variance = Σ (value−mean)²·prob; rescale Poisson λ to the right units.
- **Continuous**: probability is over **ranges** (`dnorm` is a likelihood). Uniform = rectangle; normal = μ, σ; convert to **z-scores** for the standard normal; exponential uses **rate 1/λ**.
- **CLT**: the sampling distribution of the mean is **normal** for any parent, and the **mean of means ≈ the population mean**; spread = **standard error σ/√n**.
- **Confidence intervals**: `x̄ ± z·σ/√n` (σ known) or the **t** version with **df = n−1** (σ unknown); proportions use `p̂ ± z·√(p̂(1−p̂)/n)`.
- You only control **n** — bigger samples shrink the interval; you can solve for the **n** a target margin/confidence requires.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Introduction to discrete distributions (Pt. 1)
:class: note dropdown
- Set up the runtime; simulate randomness with `sample()` (flip a coin, roll a die).
- Introduces the idea of a **probability distribution**.
- Flip a coin 10 times to watch outcomes vary around the expectation.
- Builds intuition before formulas.
:::

:::{admonition} Introduction to discrete distributions (Pt. 2)
:class: note dropdown
- Use **Monte Carlo simulation** to build a probability distribution empirically.
- Introduces the **binomial** (success/failure, e.g., heads/tails).
- Sum probabilities across a distribution in R.
- It gets easier with practice.
:::

:::{admonition} Mean and Variance of a Discrete Distribution
:class: note dropdown
- **Mean** = Σ (value × probability).
- **Variance** = Σ (value − mean)² × probability.
- Compute both directly in R.
- The values can be anything (e.g., 2, 8, 10) — not just 0, 1, 2.
:::

:::{admonition} Binomial Distribution (Pt. 1 — d is for density)
:class: note dropdown
- **`dbinom`** gives the probability of an exact number of successes.
- The binomial counts successes in *n* independent trials.
- "d" = density = the bar height.
- Foundation for the p/q functions next.
:::

:::{admonition} Binomial Distribution (Pt. 2 — p is percentile, q is quantile)
:class: note dropdown
- **p** = cumulative (sum from the left); **q** = the value at a given percentile.
- Use **complements** (1 − P) for "greater than" — not the same as compliments!
- Double-check `qbinom` answers with `pbinom`.
- The d/p/q pattern is now in place.
:::

:::{admonition} Poisson Distribution (D, P, Q for count data)
:class: note dropdown
- Apply d/p/q to the **Poisson** (counts per unit time/area).
- The trick: **rescale λ** for different units of time or area (golf-balls-in-the-yard example).
- d = bar value, p = from the left, q = inverse percentile.
- Same workflow as the binomial.
:::

:::{admonition} Wrapping Up
:class: note dropdown
- Quick recap of discrete distributions.
- Preview of where the course heads next (continuous distributions).
:::

:::{admonition} Introduction to Continuous Variables
:class: note dropdown
- Set up the environment for continuous distributions.
- Contrast **mean and variance** for a continuous vs. a discrete distribution.
- Probability now lives over **ranges**, not single points.
- Sets up uniform / normal / exponential.
:::

:::{admonition} Uniform Distribution
:class: note dropdown
- The "rectangle" distribution, parameterized by min **a** and max **b**; density = 1/(b−a).
- Mean = (a+b)/2; SD = √((b−a)²/12).
- Bus-stop example; `punif` for tails, complement for the upper tail, difference for a middle range.
- Every equal-width interval is equally likely.
:::

:::{admonition} Normal Distribution
:class: note dropdown
- Parameterized by μ and σ; bell-shaped, symmetric, mean = median = mode, asymptotic tails.
- `pnorm`/`qnorm` for probabilities and quantiles; verify with a Monte Carlo simulation.
- Same μ / different σ "fans"; same σ / different μ shifts the peak.
- ~68% within ±1 SD ties back to the empirical rule.
:::

:::{admonition} A Quick Refresh and Intro to the Standard Normal
:class: note dropdown
- Continuous probability is over a range; `dnorm` at a point is a **likelihood**, technically undefined.
- **z-score** = (x − μ)/σ = how many SDs from the mean.
- Any normal converts to the **standard normal** (mean 0, sd 1) — `pnorm`/`qnorm` defaults.
- Cereal-box example: convert limits to z, then shade the region.
:::

:::{admonition} The Empirical Rule and Exponential Distribution
:class: note dropdown
- Empirical rule (normal): **68 / 95 / 99.7%** within ±1 / 2 / 3 SD; matches `pnorm` differences.
- **Exponential** = continuous time-to-event (0 → ∞), the continuous cousin of the Poisson.
- Use **rate = 1/λ** where λ is the mean; `pexp` for probabilities.
- Checkout-time and warranty-design examples.
:::

:::{admonition} Sampling Methods and CLT (Pt. 1)
:class: note dropdown
- Population vs sample; parameters (Greek) estimated by statistics (Roman).
- We sample because populations are costly or infinite; use a **simple random sample**.
- Watch `replace =` (with vs. without replacement); **sampling error** = population − sample mean.
- 10,000 samples of size 5 → the **mean of means ≈ the population mean**.
:::

:::{admonition} Sampling Methods and CLT (Pt. 2)
:class: note dropdown
- Those 10,000 sample means form a **sampling distribution of the mean** — and it's normal.
- **Standard error** = σ/√n = the SD of that sampling distribution (≠ a plain SD).
- Bigger n ⇒ smaller standard error ⇒ tighter estimate.
- The bridge into inferential statistics.
:::

:::{admonition} Sampling Methods and CLT (Pt. 3)
:class: note dropdown
- The **CLT holds for ANY parent** — demonstrated on uniform, exponential, and normal.
- Even tiny samples (n = 2) start to look normal once you average many of them.
- Larger n tightens the spread (σ/√n) and centers on the population mean.
- The biggest takeaway: more data ⇒ less uncertainty.
:::

:::{admonition} Estimation and Confidence Intervals (Pt. 1)
:class: note dropdown
- Don't just report a point estimate — wrap it in a **confidence interval**.
- The sample mean is the best estimate of the population mean.
- **Level of confidence** (e.g., 95%); alpha = 1 − level.
- Two cases ahead: σ known (use z) vs σ unknown (use t — a "penalty shot").
:::

:::{admonition} Estimation and Confidence Intervals (Pt. 2)
:class: note dropdown
- A CI is just **center ± spread** of the sample.
- σ known: `x̄ ± z·σ/√n`; **z = 1.96** (95%), **2.58** (99%) via `qnorm`.
- Standard error σ/√n shrinks with n ⇒ tighter interval.
- You control only n — collect more data to be more confident.
:::

:::{admonition} Estimation and Confidence Intervals (Pt. 3)
:class: note dropdown
- σ **unknown** ⇒ use the sample SD `s` and the **t distribution** (df = n − 1).
- `qt()` gives a bigger multiplier than z for small n — the penalty.
- t **converges to z** as n grows (≈ identical by n ≈ 100+).
- Worked tire-tread example builds and interprets the interval.
:::

:::{admonition} Estimation and Confidence Intervals (Pt. 4)
:class: note dropdown
- **Proportions**: `p̂ ± z·√(p̂(1−p̂)/n)` — no SD term; check `n·p̂ ≥ 5` and `n·(1−p̂) ≥ 5`.
- Union-merger example interprets the interval against a threshold.
- **Sample-size planning**: `n = (z·σ/E)²` for a mean; analog for proportions (use 0.5 when unknown).
- Tighter margin / higher confidence ⇒ more observations.
:::
