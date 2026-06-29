# Chapter 1 — Describing Data with R

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Blank R Notebook** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Blank_R_Notebook.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Blank_R_Notebook.ipynb)
- **R basics with ISwR** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/ch01_ISWR_withComments.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/ch01_ISWR_withComments.ipynb)
- **Describing Data** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Describing_Data_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Describing_Data_R.ipynb)
- **Summarizing Data and Visualization** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Summarizing_Data_and_Visualization_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Summarizing_Data_and_Visualization_R.ipynb)
- **EDA: Boston Housing** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/EDA_Boston_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/EDA_Boston_R.ipynb)
:::


This chapter gets you **speaking R** and **describing data**. We set up a free coding environment, treat R as a calculator that operates on whole vectors at once, learn the handful of data types you'll use forever, and then put them to work: measuring the **center** and **spread** of data and turning a raw dataset into a clear exploratory data analysis (EDA). The best way to learn a language is to speak it — so open a notebook and code along.

## 1.1 Getting started: R inside Google Colab

We write R in **Google Colab** notebooks. Colab is Python-first, so we use a small hack: start from the shared **blank R notebook**, which already has the R kernel wired up. Make a Google Drive folder for the class with a subfolder per week, install the Colaboratory app in Drive, and always begin from that blank R notebook (or a copy).

```{admonition} Always check you're running R
:class: warning
Colab defaults to Python. The first cell of every notebook is `version` — run it and confirm it says **R**. If it says Python, stop and start again from the blank **R** notebook, or you'll spend an hour debugging code that was never going to run.
```

A notebook mixes **text cells** (formatted notes, with `#`/`##`/`###` headings that build a table of contents) and **code cells** (run with **Ctrl+Enter**). "Restart and run all" executes everything top-to-bottom — a notebook is a linear recipe. Keep the video on a second screen and type along; nobody ever learned to code by only watching.

## 1.2 R is a big calculator

Assign values with `=` or the old-school `<-` (R grew out of Bell Labs' **S** language). The real power is the **vector**: build one with `c()` ("combine") and math applies to every element at once.

```r
weight <- c(60, 72, 57, 90, 95, 72)   # a numeric vector
height <- c(1.75, 1.80, 1.65, 1.90, 1.74, 1.91)
bmi <- weight / height^2              # vectorized — no loop needed
round(mean(bmi), 2)                   # nest functions like Excel
```

Base R hands you `mean()`, `median()`, `sd()` (the **sample** standard deviation), `var()`, `length()`, `round()`, and `sum()` for free. Stuck on a function? `?rnorm` or just Google "rnorm r". R is **case-sensitive**, and `x`/`y` are safe variable names.

## 1.3 Data types and subsetting

Three data types cover almost everything early on:

- **numeric** — numbers you can do math on.
- **character** — quoted strings (`"placebo"`); you *cannot* do math on them.
- **logical** — `TRUE`/`FALSE`, produced by conditions like `bmi > 25`.

Logical vectors are the key to **subsetting**. Think *square brackets* whenever you select:

```r
v <- c(5640, 6180, 6390, 6515, 6805, 7515)
v[5]            # the 5th element
v[c(3, 5, 7)]   # several elements
v[1:5]          # a range
v[-3]           # drop the 3rd
df[df$pre > 7000, ]   # rows where a condition is TRUE; blank after the comma = all columns
```

Most real data arrives as a **data frame** (rows × columns, each column a type). Grab a column with the `$` accessor (`df$age`), peek with `head()`/`tail()`, and load datasets that live in packages:

```r
install.packages("ISwR")   # quoted — downloading from CRAN
library(ISwR)              # unquoted — now loaded and ready
```

## 1.4 Central tendency — where is the middle?

First, a vocabulary distinction that runs through the whole course: a **population** is every element of a group; a **sample** is a subset we use to *infer* something about that population. **Parameters** describe populations (Greek letters); **statistics** describe samples (Roman letters).

- **Mean** = sum ÷ n. It's the data's **balance point**, which makes it **sensitive to outliers** — one huge value drags it.
- **Median** = the 50th percentile. It's rank-based and **robust** to outliers.
- **Mode** = the most frequent value. Base R has no `mode()` for this, so we write a tiny function with `table()` and `unique()`.

Overlay all three on a histogram to see how a skewed distribution pulls the mean away from the median:

```r
hist(temp, col = "orange", main = "Highway exit distances", xlab = "miles")
abline(v = mean(temp),   col = "red",   lwd = 3, lty = 2)   # dashed = mean
abline(v = median(temp), col = "blue",  lwd = 3, lty = 2)
```

## 1.5 Dispersion — how spread out is it?

A center alone can mislead (a river "3 feet deep on average" can still be 20 feet deep in the middle). We need **spread**:

- **Range** — `range()` returns the min and max; the range itself is max − min.
- **Mean deviation** — the average *absolute* distance from the mean (absolute value stops positives and negatives from cancelling to zero).
- **Variance** and **standard deviation** — square the deviations so outliers are penalized; the SD is the square root, back in the original units.

```{admonition} var() and sd() are the SAMPLE versions
:class: warning
Population variance divides by **n**; sample variance divides by **n − 1**. That smaller denominator inflates the estimate — a deliberate penalty for the extra uncertainty of using a sample. R's `var()` and `sd()` use **n − 1** by default, which is what you want ~99% of the time. Computing the *population* version takes a manual workaround.
```

## 1.6 Chebyshev's theorem and the empirical rule

Once you have a mean and an SD, you can say where the data lives:

- **Chebyshev's theorem** works for **any** distribution shape: at least **75%** of the data falls within ±2 SD, at least **89%** within ±3 SD. Conservative, but always true.
- **The empirical rule** is the bonus you get for a **normal** distribution: ~**68% / 95% / 99.7%** within ±1 / 2 / 3 SD.

So if apartments rent for \$500/day on average with an SD of \$20, the empirical rule says ~95% rent between \$460 and \$540. (Note the backslash-escaped dollar signs in prose so they aren't read as math.)

## 1.7 Exploratory data analysis, end to end

EDA is **summarize → tabulate → plot**, all in service of telling a story. The reconnaissance trio for any new data frame:

```r
summary(df)   # per-column stats, or counts for categories
str(df)       # data type of every column
dim(df)       # rows and columns
```

**Tables** are pivot tables: `table(df$col)` (one-way), `table(a, b)` (two-way), `prop.table()` for proportions (`prop.table(x, 1)` = row %, `prop.table(x, 2)` = column %), and `ftable()` to flatten a messy three-way table. For statistics *by group*, `tapply(value, group, FUN)` or — Dave's preference — `aggregate(y ~ g1 + g2, FUN = mean)`, which returns a tidy data frame.

**Plots**: R chooses a default from the data types you feed it (numeric → index scatter, factor → bar, numeric-by-category → boxplot, two categories → mosaic, two numerics → scatter). Start with a high-level plot, then layer low-level styling — `col`, `pch = 19`, `cex`, titles, `abline()`, `legend(..., bty = "n")`. A `lowess()` smoother makes a trend idiot-proof; `density()` + `polygon()` makes a smooth, filled distribution.

```{admonition} Reading a local CSV in Colab-R
:class: tip
Unlike Python, R in Colab can't point straight at a Drive file — click the **folder icon** and upload the CSV into the runtime, then `read.csv("BostonHousing.csv")`. You *can* write results out with `write.csv()` and download them.
```

The Boston Housing EDA ties it together: read the CSV, spot 0/1 indicators (min 0, max 1, e.g. `chas`), recode them with `as.character()` and `gsub()`, then go visual — `psych::pairs.panels()` (correlations + histograms + ellipses), `corrplot()` for a polished correlation matrix, a **for-loop** that auto-histograms every numeric column, and `psych::describeBy(df, group)` for grouped summaries. By the end you can hand someone a clean dataset and tell its story.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- Code in **Colab** from the **blank R notebook**; confirm the `version` cell says R, and code along.
- R is **vectorized**: build with `c()`, and `mean()`/`median()`/`sd()`/`var()` come for free.
- Three data types — **numeric, character, logical** — and logical conditions drive **`[ ]` subsetting**; real data lives in **data frames**.
- Describe the **center** (mean = balance point, median = robust, mode = most frequent) and the **spread** (range, variance, SD).
- `var()`/`sd()` are the **sample** versions (**n − 1**).
- **Chebyshev** bounds any distribution; the **empirical rule** (68/95/99.7) is the reward for normality.
- **EDA = summarize → tabulate → plot**: `summary`/`str`/`dim`, `table`/`prop.table`/`aggregate`, and layered plots with `lowess`, `corrplot`, and `describeBy`.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Welcome to Dr. Dave (Stats with R)
:class: note dropdown
- Course welcome; R was Dr. Dave's first language and stats is foundational for any analyst/data scientist.
- Five themes: descriptive stats → probability distributions → hypothesis testing → maximum likelihood → regression.
- Goal: a real command of R, fearless EDA, and the confidence to fit a model and interpret it.
:::

:::{admonition} Setting up Google Drive and Google Colab (with R)
:class: note dropdown
- One class folder in Drive, a subfolder per week; install the Colaboratory app.
- Always start from the **blank R notebook** — Colab defaults to Python; check the `version` cell says R.
- `File → Download .ipynb` to keep your own copy.
- Notebooks mix text and code cells (Ctrl+Enter to run); code along, don't just watch.
:::

:::{admonition} R basics with ISwR (Pt. 1)
:class: note dropdown
- Assignment uses `=` or `<-` (R descends from Bell Labs' S).
- Get help with `?rnorm` or Google; `rnorm(n)` draws from a normal (defaults mean 0, sd 1).
- "Restart and run all" runs top-to-bottom — a notebook is a linear recipe.
- R is case-sensitive; x/y are safe names.
:::

:::{admonition} R basics with ISwR (Pt. 2)
:class: note dropdown
- R is a big calculator: `hist()`, `mean()`, `sd()` (sample), `median()`.
- Build vectors with `c()`; arithmetic is vectorized.
- `length()`, `round()`, nested functions; `var()` = sample variance.
- Text cells render LaTeX and embedded images.
:::

:::{admonition} R basics with ISwR (Pt. 3)
:class: note dropdown
- Scatter with `plot(x, y, col=, pch=19, cex=, main=)`.
- Data types: numeric, character (quoted, no math), logical (T/F).
- Logical conditions return T/F vectors used for subsetting.
- `paste()`/`cat()` join strings; lists vs data frames, accessed with `$`.
:::

:::{admonition} R basics with ISwR (Pt. 4)
:class: note dropdown
- `cbind()` columns into a matrix, then `as.data.frame()`.
- Square brackets select: `v[5]`, `v[c(3,5,7)]`, `1:5`, drop with `-`.
- Logical subsetting; `df[rows, cols]` (blank = all); `head()`/`tail()`.
- `install.packages("ISwR")` (quoted) then `library(ISwR)` (unquoted).
:::

:::{admonition} Describing Data (Pt. 1)
:class: note dropdown
- Population vs sample — parameters (Greek) vs statistics (Roman).
- Mean = sum / n; it's the balance point and is sensitive to outliers.
- Median is rank-based and robust.
- `abline(v = mean(x), lty = 2)` marks the mean on a histogram.
:::

:::{admonition} Describing Data (Pt. 2)
:class: note dropdown
- Median = 50th percentile; mode = most frequent (write your own with `table()`/`unique()`).
- Overlay mean/median/mode on a skewed histogram to compare.
- Spread matters (river-depth analogy); `range()` returns min & max.
- Mean deviation = average absolute deviation from the mean.
:::

:::{admonition} Describing Data (Pt. 3)
:class: note dropdown
- Population variance σ² = Σ(x − mean)² / n; squaring penalizes outliers; SD = √variance.
- Sample variance s² divides by n − 1 (uncertainty penalty).
- `var()`/`sd()` are the **sample** versions.
- Worked by hand with a column per step, then verified with built-ins.
:::

:::{admonition} Describing Data (Pt. 4)
:class: note dropdown
- Chebyshev holds for ANY shape: ≥75% within ±2 SD, ≥89% within ±3 SD.
- Empirical rule (normal data): ~68/95/99.7% within ±1/2/3 SD.
- Use mean ± k·SD to bound real ranges.
- Visualize with shaded SD bands over a simulated normal.
:::

:::{admonition} Summarizing Data and Visualization (Pt. 1)
:class: note dropdown
- EDA building blocks: summarize → tabulate → plot, to tell a story.
- Datasets hide in packages (e.g., `Arthritis` in VCD).
- `summary()` (stats/counts), `str()` (types), `dim()` (shape).
- Logical conditions + `[ ]` subset into smaller data frames.
:::

:::{admonition} Summarizing Data and Visualization (Pt. 2)
:class: note dropdown
- Package name clashes happen (VCD vs MASS); Whiteside insulation data.
- One-way `table(df$col)` and two-way `table(a, b)` are pivot tables.
- `prop.table()` for proportions; `,1)` row %, `,2)` column %.
- Column-wise percentages tell a richer story.
:::

:::{admonition} Summarizing Data and Visualization (Pt. 3)
:class: note dropdown
- Three-way `table()` is messy — `ftable()` flattens it.
- `tapply(value, group, FUN)` computes a statistic by group.
- `aggregate(y ~ g1 + g2, FUN = mean)` returns a tidy data frame.
- Rename columns for presentation-ready tables.
:::

:::{admonition} Summarizing Data and Visualization (Pt. 4)
:class: note dropdown
- R picks a plot from the data type (scatter/bar/boxplot/mosaic).
- High-level plot + low-level styling: `col`, `pch=19`, `cex`, `type`.
- Grouped, horizontal, labeled `boxplot()`; annotate with `abline()`+`text()`.
- Overlay groups: `plot()` then `points()` (before/after in two colors).
:::

:::{admonition} Summarizing Data and Visualization (Pt. 5)
:class: note dropdown
- `par(mfrow=c(2,2))` for subplots; reset opar afterward.
- Univariate: box/hist/density — `hist(prob=TRUE)`, `density()` + `polygon()`.
- Box-plot anatomy: Q1/median/Q3, whiskers ~1.5·IQR, outliers.
- `smoothScatter()` for overplotting; `cor()` + `corrplot` for relationships.
:::

:::{admonition} Boston Housing EDA (Pt. 1)
:class: note dropdown
- First local-CSV read in Colab-R: upload via the folder icon.
- `colnames()`, `str()`, `dim()`, `summary()`; `medv` is the target.
- Spot 0/1 indicators (min 0, max 1), e.g. `chas`; count with `table()`.
- Recode with `as.character()`/`as.logical()` and `gsub()`.
:::

:::{admonition} Boston Housing EDA (Pt. 2)
:class: note dropdown
- Dress up histograms: color, labels, mean/median `abline`, `legend(bty="n")`.
- `boxplot()` plus the mean as a `points()` marker.
- KDE via `density()`: red line + `polygon()` fill + dashed mean.
- Bivariate scatter + `lowess()` smoother; a missing quote is your bug, not R's.
:::

:::{admonition} Boston Housing EDA (Pt. 3)
:class: note dropdown
- Drop a column with `-`; `psych::pairs.panels()` beats base `pairs()`.
- `corrplot()` for a polished correlation matrix.
- `barplot(table(...))` needs table input; a for-loop auto-histograms every numeric column.
- `psych::describeBy(df, group)` for grouped summaries; `write.csv()` to export.
:::
