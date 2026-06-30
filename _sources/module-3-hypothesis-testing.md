# Chapter 3 — Hypothesis Testing

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **One-Sample Tests (summarized)** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/One_Sample_Tests_summarized.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/One_Sample_Tests_summarized.ipynb)
- **Two-Sample Tests — Additional Problems** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Two_Sample_Tests_Additional_Problems.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Two_Sample_Tests_Additional_Problems.ipynb)
- **Cheat Sheet — Hypothesis Testing from Scratch** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Cheat_Sheet_Hypothesis_Testing_from_Scratch.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Cheat_Sheet_Hypothesis_Testing_from_Scratch.ipynb)
:::


This is inferential statistics in action: we make a claim about a population, collect a sample, and decide whether the sample is **extreme enough** to overturn the claim. The whole chapter runs on one engine — the **five-step procedure** — applied first to **one-sample** tests (means and proportions) and then to **two-sample** tests, where each assumption we relax makes significance a little harder to declare.

## 3.1 The five-step procedure

Every test follows the same five steps:

1. **State the hypotheses.** The **null** (H₀) is the status-quo claim — what the politician says — and always carries the equality (`=`, `≤`, `≥`). The **alternative** (H₁) is what you're trying to prove with data.
2. **Pick a significance level α** — 0.10, 0.05, or 0.01 (medical work wants 0.01). α is your tolerance for rejecting a true null.
3. **Choose the test statistic** — **z** if the population σ is known, **t** if it isn't.
4. **Form the decision rule** — find the **critical value** (`qnorm`/`qt`) that marks the rejection region.
5. **Compute the statistic and decide** — reject H₀, or "fail to reject" (never "accept").

A **test statistic** like `z = (x̄ − μ) / (σ/√n)` measures how many standard errors your sample sits from the claimed mean. The **p-value** is the probability mass beyond it — *the chance of a sample this extreme if H₀ were true*. Two-tailed tests split α into both tails (so 95% confidence ⇒ critical values ±1.96); one-tailed tests pile all of α into the tail of interest, which makes rejection a bit easier.

```{admonition} Don't memorize rejection rules — draw them
:class: tip
Plot the distribution: the **critical value** is a red line (from `qnorm`/`qt`), the **test statistic** is a purple line, and the **rejection region** is the shaded tail(s). If the purple line lands in the shaded region, reject. This picture makes one- vs two-tailed tests and p-values obvious, and it beats memorizing inequalities.
```

## 3.2 One-sample tests, worked

The notebook walks every flavor with the same desk-manufacturing and claims examples:

- **Two-tailed, σ known** — "is production *different* from 200?" Split α/2 into both tails; `z = (203.5 − 200)/(16/√50) = 1.55` isn't extreme enough → fail to reject.
- **Upper-tailed, σ known** — "did production *increase*?" One tail, one critical value, and the **p-value** emerges cleanly as the mass to the right of the test statistic.
- **Lower-tailed, σ unknown → t** — insurance claims now under \$60? Use the sample SD and `qt(α, df = n − 1)`; the t distribution's fat tails make rejection harder.
- **Proportion** — there's no SD, so `z = (p̂ − π₀)/√(π₀(1−π₀)/n)` (governor's vote share); check `n·π ≥ 5` and `n·(1−π) ≥ 5` first.

## 3.3 Two-sample tests: the big idea

Now we compare two **subpopulations** — plumbers vs. electricians, day vs. night shift — by looking at the **difference of their means** and asking whether it's significantly different from zero. Three facts power every two-sample test:

- The **difference of two normal distributions is itself normal** (courtesy of the CLT).
- **Variance is additive** — combine the uncertainty from both groups rather than picking one.
- Samples can be different sizes, and they're either **independent** (two random groups) or **dependent/paired** (the same units measured twice).

## 3.4 Two-sample means and proportions

We build up in difficulty, and the pattern is the point:

- **σ known → z** (grocery checkout methods): `z = (x̄₁ − x̄₂)/√(σ₁²/n₁ + σ₂²/n₂)`.
- **Proportions → z with a pooled proportion** `p_c` (perfume survey): pool successes across both samples for the standard error.
- **σ unknown, equal variance → t** with a **pooled SD `s_p`** and `df = n₁ + n₂ − 2` (lawn-mower mounting times).
- **σ unknown, unequal variance → t** with the **Welch degrees of freedom** (paper-towel absorbency) — compute the messy df formula and **truncate it down** (10.86 → 10) to stay conservative.

```{admonition} Each relaxed assumption makes rejection harder
:class: note
The ladder z → t(equal variance) → t(unequal variance) adds uncertainty at every rung, so it takes a larger gap to declare significance. Knowing σ is the easy case; assuming **unknown, unequal variance** is the most conservative — and the safest when you really need to be sure two groups differ.
```

## 3.5 Paired (dependent) samples

When the *same* units are measured twice — weight before/after a drug, the same 10 houses appraised by two mortgage companies — use a **paired t-test** on the **differences**: `t = d̄ / (s_d/√n)`, `df = n − 1`. Pairing cancels the between-subject variation, which **shrinks the denominator** and makes significance *easier* to declare. The notebook proves it: on the same mortgage data, the **paired** test finds a real difference while an **independent** two-sample test (big pooled variance) cannot — so matching the test to the data design matters.

```{admonition} Statistical vs. substantive significance
:class: warning
A test statistic is `difference / (spread/√n)`, so with a **large enough n even a trivial difference becomes "significant."** The classic trap: a wine study where one group lives to 80.30 and the other to 80.31 — statistically significant, practically meaningless. Always look at the **size of the effect (the delta)**, not just the p-value.
```

## Wrap-up

```{admonition} Key takeaways
:class: tip
- The **five steps**: hypotheses (H₀ holds the equality) → α → test statistic → decision rule → decide ("fail to reject," never "accept").
- **z when σ is known, t (df = n − 1) when it isn't**; two-tailed splits α/2, one-tailed pools α in one tail.
- The **p-value** is the chance of a sample this extreme if H₀ is true — *draw* the critical (red) and test-statistic (purple) lines.
- **Two-sample**: difference of normals is normal, **variance is additive**; ladder of difficulty z → pooled-t (equal var) → Welch-t (unequal var, truncate df).
- **Proportions** use `p̂`/pooled `p_c` (no SD); check `n·π ≥ 5` and `n·(1−π) ≥ 5`.
- **Paired data** → paired t-test on the differences (easier to detect a real effect); always weigh **substantive vs statistical** significance.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} The Five Steps of Hypothesis Testing
:class: note dropdown
- Inferential stats: use a **sample** to test a claim about a **population**.
- Five steps: state H₀/H₁ → pick α → choose test statistic → decision rule → decide.
- H₀ holds the equality; **p-value** = chance of a sample this extreme if H₀ is true.
- z (σ known) vs t (σ unknown); one- vs two-tailed; "fail to reject," never "accept."
- Type I error ties to α; visualize the rejection region.
:::

:::{admonition} Two-Tail Test: Pop. Std. Dev. Known
:class: note dropdown
- Two-tailed ⇒ split α/2 into **both** tails; critical values ±z via `qnorm`.
- Desk example: `z = (203.5−200)/(16/√50) = 1.55` → not extreme → fail to reject.
- Big population spread ⇒ need to be 2+ SE away to reject.
- Plot it: red critical lines, purple test statistic, shaded tails.
- A large σ makes small mean differences unconvincing.
:::

:::{admonition} Upper-Tail Test: Pop. Std. Dev. Known
:class: note dropdown
- One-tailed ⇒ one rejection region; critical value `z_α` via `qnorm` (easier to reject).
- The alternative points toward the rejection tail.
- **p-value** emerges as the mass to the right of the test statistic (`lower.tail = FALSE`).
- If p < α, reject; the analyst chooses α (0.10/0.05/0.01).
- Same z as the two-tail version — only the rule changes.
:::

:::{admonition} Lower-Tail Test: Pop. Std. Dev. Unknown
:class: note dropdown
- σ unknown ⇒ use sample SD and the **t distribution** (fat tails, harder to reject).
- Critical value via **`qt(α, df = n − 1)`** — not `qnorm`.
- Insurance-claims example: t = −1.81 vs −2.485 → fail to reject at 0.01.
- The alternative ("less than 60") signals a lower-tail test.
- Decision flips at looser α (0.05/0.10) — α is a real choice.
:::

:::{admonition} Proportions (one-sample)
:class: note dropdown
- Proportion `p = x/n`; no SD, so `z = (p̂ − π₀)/√(π₀(1−π₀)/n)`.
- Requires count data, two outcomes, independent trials, `n·π ≥ 5` and `n·(1−π) ≥ 5`.
- Governor-vote example: p̂ = 0.775 vs claimed 0.80 → z = −2.8 → reject.
- Uses the normal approximation to the binomial.
- Same five-step logic, different statistic.
:::

:::{admonition} More Examples on Hypothesis Testing
:class: note dropdown
- A grid of lower/upper/two-tail tests for means (z and t) and proportions.
- Light bulbs (z = −4.56, reject fast), cookies (upper-tail, reject), penguins (two-tail, borderline).
- Same example with t shifts the critical value out (fat tails) — harder to reject.
- How you frame one- vs two-tailed changes the conclusion.
- Reinforces drawing the picture over memorizing rules.
:::

:::{admonition} Introduction to Two-Sample Tests of Hypothesis
:class: note dropdown
- Compare two **subpopulations** via the **difference of means** (is it ≠ 0?).
- Samples can be different sizes; **variance is additive**.
- The difference of two normal distributions is itself normal.
- Independent (two random groups) vs dependent (paired) samples.
- Don't memorize formulas — read how each combines mean, spread, and n.
:::

:::{admonition} Comparing Population Means — Pop. Std. Dev. Known
:class: note dropdown
- `z = (x̄₁ − x̄₂)/√(σ₁²/n₁ + σ₂²/n₂)` — additive variance in the denominator.
- Assumes normal populations, independent samples, known σ's.
- Grocery checkout example: z = 3.12 > 2.33 → the fast lane really is faster.
- The simplest (toy) case before σ becomes unknown.
- Subtracting in either order just flips the sign.
:::

:::{admonition} Comparing Proportions for Different Populations
:class: note dropdown
- Two-sample proportion z uses a **pooled proportion** `p_c` = combined successes / combined n.
- Perfume example: younger 19% vs older 31% (pooled 27%) → z = −2.21 → difference is real.
- Normal approximation to the binomial.
- Multiply the tail probability by 2 for a two-tailed p-value.
- Proportions "play nice" — no SD needed.
:::

:::{admonition} Comparing Means — Std. Dev. Unknown, Assume Equal
:class: note dropdown
- σ unknown ⇒ **t**; assume equal group variance ⇒ **pooled SD `s_p`**.
- `df = n₁ + n₂ − 2`.
- Lawn-mower example: t = −0.66 → fail to reject (an outlier inflates one group's spread).
- Equal-variance assumption makes significance easier than unequal.
- Look at means *and* spread before trusting your gut.
:::

:::{admonition} Comparing Means — Std. Dev. Unknown, Assume Unequal
:class: note dropdown
- Most conservative case: unknown **and unequal** variance.
- Uses the **Welch degrees of freedom** — compute it, then **truncate down** (10.86 → 10).
- Paper-towel example: clearly different means + spreads → reject.
- Hardest test to reject, so a rejection is very trustworthy.
- The safe default when you must be sure two groups differ.
:::

:::{admonition} Two-Sample Test for Dependent Samples (Paired Tests)
:class: note dropdown
- Paired = same units measured twice (before/after; same 10 houses, two appraisers).
- `t = d̄ / (s_d/√n)`, `df = n − 1` — work on the **differences**.
- Pairing removes between-subject variation ⇒ easier to detect a real effect.
- Mortgage example: t = 3.3 → a real difference in appraisals.
- Small s_d + large n ⇒ large t.
:::

:::{admonition} Comparison of Dependent vs. Independent Tests
:class: note dropdown
- The **same** mortgage data: paired test rejects; independent two-sample test does **not**.
- Independent test's large pooled variance shrinks t toward 0.
- Matching the **test to the data design** is essential.
- Use the paired test when data is genuinely paired — or miss a real effect.
- Wrong test ⇒ wrong (and costly) conclusion.
:::
