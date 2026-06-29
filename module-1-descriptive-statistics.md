# Module 1 — Descriptive Statistics

Getting started with data analysis in R: descriptive statistics, exploratory data analysis (plots and tables), and dealing with messy data. R runs inside Google Colab via a small hack, and we learn by doing from the very first lecture.

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Blank R Notebook** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Blank_R_Notebook.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Blank_R_Notebook.ipynb)
- **Describing Data R** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Describing_Data_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Describing_Data_R.ipynb)
- **EDA Boston R** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/EDA_Boston_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/EDA_Boston_R.ipynb)
- **Summarizing Data and Visualization R** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Summarizing_Data_and_Visualization_R.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/Summarizing_Data_and_Visualization_R.ipynb)
- **ch01 ISWR withComments** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/ch01_ISWR_withComments.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module1/ch01_ISWR_withComments.ipynb)
:::

## 1.1 Welcome to R

### Video 0: Welcome to Dr. Dave (Stats with R)

*✍️ Full narrative coming from the lecture transcript.*

### Video 1: Setting up Google Drive and Google Colab (with R)

**Overview.** You should use Google Chrome in this class (for a browser) and a dedicated Gmail account (personal Gmail or UConn Gmail). Make folders that match the flow of the class. Install Drive's access to Colab. Save a copy of the blank R notebook. Be careful - you need to use my blank R notebook whenever you get started (otherwise you will be running Python!)

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: R basics with ISwR (Pt. 1)

**Overview.** Let's get our feet wet with some R programming. Introduction to the assignment operator(s) = and <-. How to find help if you need it.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: R basics with ISwR (Pt. 2)

**Overview.** R is just a big calculator - create a vector and assign to vectors, then manipulate them. Don't forget to use c() when creating a vector. You can use formulas from base R, and nest them (a function in a function) just like Excel. If you are so adventurous, you can also try making some formulas in LaTeX or embedding a picture.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: R basics with ISwR (Pt. 3)

**Overview.** Scatterplots, overview of data types (strings, logicals, numeric), combining strings and organizing data in vectors, lists and dataframes (most common).

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: R basics with ISwR (Pt. 4)

**Overview.** cbind() through end. Learn how to subset rows and/or columns from a dataframe and make a boxplot.

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Describing Data (Pt. 1)

**Overview.** Central Tendency - population and sample mean (making nicely labeled histograms).

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Describing Data (Pt. 2)

**Overview.** Central Tendency and Dispersion - median and mode; range and mean deviation.

*✍️ Full narrative coming from the lecture transcript.*

### Video 7: Describing Data (Pt. 3)

**Overview.** Dispersion - Variance and Standard Deviation - by hand (long-form with dataframes) and with formulas.

*✍️ Full narrative coming from the lecture transcript.*

### Video 8: Describing Data (Pt. 4)

**Overview.** Chebychev's Theorem applies to distributions of any shape (normal or unnormal) whereas the empirical rule applies only to NORMAL distributions. … save for Week 2?

*✍️ Full narrative coming from the lecture transcript.*

## 1.2 Exploratory Data Analysis

### Video 1: Summarizing Data and Visualization (Pt. 1)

**Overview.** Data types and subsetting by group with the Arthritis package. Remember that we can use an ampersand (&) to join to conditions together, and then subset data. Use dim() to check the number of rows and columns, str() for data types, and summary() for a quick peek at the data frame.

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: Summarizing Data and Visualization (Pt. 2)

**Overview.** Tabulation with the whiteside insulation data (select data by group) and create tables and proportion tables prop.table() using the Arthritis dataset.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Summarizing Data and Visualization (Pt. 3)

**Overview.** Use tapply() or aggregate() to tabulate data by group, and note that you can use whatever function you want at the end (you don't have to use mean, you can use median or sd or any other custom function - more examples later on).

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: Summarizing Data and Visualization (Pt. 4)

**Overview.** Figures and Graphics - high-level plot commands where R will automatically create a plot based on the data type, and an introduction to some lower-level plotting commands (adding an abline, annotating with text, xlab and ylab).

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Summarizing Data and Visualization (Pt. 5)

**Overview.** par() and opar() are used to create subplots (with defaults that are applied to each argument). How to plot curves, create univariate plots and bivariate plots. Correlograms to show the positive and negative relationship (correlation) between variables.

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Boston Housing EDA (Pt. 1)

**Overview.** Reading in a .csv file into Google Colab, exploring the first few rows of data, summary statistics, converting data types (from numeric to character) and using gsub() to replace values.

*✍️ Full narrative coming from the lecture transcript.*

### Video 7: Boston Housing EDA (Pt. 2)

**Overview.** Univariate and bivariate plots including scatterplots - adding a locally weighted smoother (lowess) line to the plot via the lines() function, and adding custom lines and points to graphs to help tell a better story with data.

*✍️ Full narrative coming from the lecture transcript.*

### Video 8: Boston Housing EDA (Pt. 3)

**Overview.** Advanced EDA - for loops for generating plots, using the describeBy() function from psych to analyze data by groups, saving .csv files to the local runtime (and downloading them on your computer).

*✍️ Full narrative coming from the lecture transcript.*

## Wrap-up

```{admonition} Key takeaways
:class: tip
- R runs in Colab via a hack — always start from the **blank R notebook** (or you'll be running Python).
- Describe **center** (mean, median, mode) and **spread** (range, variance, standard deviation).
- Build an **EDA** from labeled plots and summary/proportion tables.
- **Chebyshev's theorem** applies to any distribution; the **empirical rule** only to normal data.
```

---

## 📌 Lecture key points

*Quick reference — one card per lecture (click to expand).*

:::{admonition} Welcome to Dr. Dave
:class: note dropdown
- Course welcome from Dr. Dave; R was his first language and stats is foundational for any analyst/data scientist.
- Five themes for the term: descriptive statistics → probability distributions → hypothesis testing → maximum likelihood → regression.
- Goal by the end: a real command of R, fearless EDA, and the confidence to fit a model and say something intelligent about it.
:::

:::{admonition} Setting up Google Drive and Google Colab
:class: note dropdown
- Set up Google Drive + Colab: one class folder, a subfolder per week; install the Colaboratory app in Drive.
- Always start from the **blank R notebook** — Colab defaults to Python, so check the `version` cell says R.
- `File → Download .ipynb` to keep your own copy; notebooks mix formatted text cells with code cells.
- Code along (run cells with Ctrl+Enter) — nobody learns to code just by watching.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
- Assignment uses `=` or `<-` (R descends from Bell Labs' S language).
- Get help with `?rnorm` or Google; `rnorm(n)` draws from a normal (defaults mean 0, sd 1).
- 'Restart and run all' executes top-to-bottom — a notebook is a linear recipe.
- R is case-sensitive; x/y are safe variable names.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
- R is a big calculator: `hist()`, `mean()`, `sd()` (sample), `median()`; random draws vary slightly per run.
- Build vectors with `c()`; arithmetic is vectorized (applies element-wise).
- `length()`, `round()`, and nested functions (like Excel); `var()` = sample variance.
- Text cells render LaTeX and embedded images.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
- Scatter with `plot(x, y, col=, pch=19, cex=, main=)`; use `args()` or Google for options.
- Core data types: numeric, character (quoted strings — no math), logical (T/F).
- Logical conditions (e.g., `bmi > 25`) return T/F vectors used for subsetting.
- `paste()`/`cat()` join strings; mixing types coerces to string; lists vs data frames, accessed with `$`.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
- `cbind()` columns into a matrix, then `as.data.frame()` — prefer data frames.
- Square brackets select: `v[5]`, `v[c(3,5,7)]`, ranges `1:5`, and drop with `-`.
- Logical subsetting across vectors; `df[rows, cols]` (leave blank = all); `head()`/`tail()`.
- `install.packages("ISwR")` (quoted) then `library(ISwR)` (unquoted); boxplot by group.
:::

:::{admonition} Describing Data
:class: note dropdown
- Population vs sample — parameters are Greek letters, statistics are Roman letters.
- Mean = sum / n (same formula for both); the mean is the data's balance point and is sensitive to outliers.
- Median is rank-based and robust to outliers.
- `mean()`, `length()`, and `abline(v = mean(x), col, lwd, lty=2)` to mark the mean on a histogram.
:::

:::{admonition} Describing Data
:class: note dropdown
- Median = 50th percentile (robust); mode = most frequent value — no base-R function, write one with `table()`/`unique()`.
- Overlay mean/median/mode lines on a skewed histogram to compare.
- Spread matters (the river-depth analogy): `range()` returns min & max; the range is max − min.
- Mean deviation = average absolute deviation from the mean (absolute value keeps it from cancelling to 0).
:::

:::{admonition} Describing Data
:class: note dropdown
- Population variance σ² = Σ(x − mean)² / n; squaring penalizes outliers; SD = √variance (original units).
- Sample variance s² divides by n − 1 — a penalty that adds uncertainty when using a sample.
- `var()` and `sd()` return the **sample** versions (what you use ~99% of the time).
- Worked by hand with a data-frame column per step, then verified with the built-ins.
:::

:::{admonition} Describing Data
:class: note dropdown
- Chebyshev's theorem holds for ANY shape: ≥75% within ±2 SD, ≥88% within ±3 SD.
- Empirical rule (NORMAL data only): ~68% / 95% / 99.7% within ±1 / 2 / 3 SD.
- Use mean ± k·SD to bound real ranges (rent/price worked examples).
- Visualize with shaded SD bands over a simulated normal distribution.
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
- EDA building blocks: summarize → tabulate → plot, all in service of telling a story.
- Datasets hide in packages (e.g., `Arthritis` in VCD) — `install.packages()` then `library()`.
- `summary()` gives per-column stats or category counts; `str()` shows data types; `dim()` shows shape.
- Logical conditions + `[ ]` subset into smaller data frames.
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
- Package name clashes happen (uninstall/reinstall, e.g., VCD vs MASS); Whiteside insulation dataset.
- One-way `table(df$col)` and two-way `table(a, b)` are pivot tables in R.
- `prop.table()` for proportions; `prop.table(x, 1)` row %, `prop.table(x, 2)` column %.
- Column-wise percentages tell a richer story (treated vs placebo improvement).
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
- Three-way `table()` output is messy — `ftable()` flattens it into a clean layout.
- `tapply(value, group, FUN)` computes a statistic by group (mean/median/sd).
- `aggregate(y ~ g1 + g2, FUN = mean)` (Dave's go-to) returns a tidy data frame.
- Rename columns for presentation-ready tables (salary by sex × rank).
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
- R chooses a plot from the data type: numeric→index scatter, factor→bar, num~cat→boxplot, cat~cat→mosaic, num~num→scatter.
- High-level plot + low-level styling: `col`, `pch=19`, `cex`, `type` (l / h / o).
- Grouped, horizontal, labeled `boxplot()` (`las`); annotate with `abline()` + `text()`.
- Overlay groups: `plot()` the first group, then `points()` the second (before/after in two colors).
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
- `par(mfrow=c(2,2))` (via opar) for subplots; reset opar afterward.
- Univariate plots: box, histogram, density — `hist(prob=TRUE)`, `density()` + `polygon()` fill.
- Box-plot anatomy: Q1/median/Q3, whiskers ~1.5·IQR, outliers; read skew direction.
- `smoothScatter()` for overplotting; `cor()` + corrgram/`corrplot` for relationships (Boston teaser).
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
- First local-CSV read in Colab-R: upload via the folder icon (R can't point at Drive like Python can).
- `colnames()`, `str()`, `dim()`/`nrow()`/`ncol()`, `summary()`; `medv` is the target variable.
- Spot 0/1 indicators (min 0, max 1), e.g., `chas`; count with `table()`.
- Recode with `as.character()`/`as.logical()` and `gsub()` (0→"away from", 1→"next to").
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
- Dress up histograms: color, labels, title, mean/median `abline`, and a `legend()` (use `bty="n"`).
- `boxplot()` plus the mean as a `points()` marker (pch 21 with bg/col).
- KDE via `density()`: red line + `polygon()` fill + dashed mean line.
- Bivariate scatter + `lowess()` smoother to reveal the trend; a missing quote is your bug, not R's.
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
- Drop a column with `-`; base `pairs()` is ugly — `psych::pairs.panels()` adds correlations, hist/density, and ellipses.
- `corrplot()` for a polished correlation matrix (size + color, upper triangle).
- `barplot(table(...))` needs table input; a **for-loop** auto-histograms every numeric column (titled after itself).
- `psych::describeBy(df, group)` for grouped summaries; `write.csv()` to export and download.
:::
