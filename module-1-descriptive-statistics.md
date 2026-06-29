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
Key points will be distilled from the lecture transcript.
:::

:::{admonition} Setting up Google Drive and Google Colab
:class: note dropdown
You should use Google Chrome in this class (for a browser) and a dedicated Gmail account (personal Gmail or UConn Gmail). Make folders that match the flow of the class. Install Drive's access to Colab. Save a copy of the blank R notebook. Be careful - you need to use my blank R notebook whenever you get started (otherwise you will be running Python!)
:::

:::{admonition} R basics with ISwR
:class: note dropdown
Let's get our feet wet with some R programming. Introduction to the assignment operator(s) = and <-. How to find help if you need it.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
R is just a big calculator - create a vector and assign to vectors, then manipulate them. Don't forget to use c() when creating a vector. You can use formulas from base R, and nest them (a function in a function) just like Excel. If you are so adventurous, you can also try making some formulas in LaTeX or embedding a picture.
:::

:::{admonition} R basics with ISwR
:class: note dropdown
Scatterplots, overview of data types (strings, logicals, numeric), combining strings and organizing data in vectors, lists and dataframes (most common).
:::

:::{admonition} R basics with ISwR
:class: note dropdown
cbind() through end. Learn how to subset rows and/or columns from a dataframe and make a boxplot.
:::

:::{admonition} Describing Data
:class: note dropdown
Central Tendency - population and sample mean (making nicely labeled histograms).
:::

:::{admonition} Describing Data
:class: note dropdown
Central Tendency and Dispersion - median and mode; range and mean deviation.
:::

:::{admonition} Describing Data
:class: note dropdown
Dispersion - Variance and Standard Deviation - by hand (long-form with dataframes) and with formulas.
:::

:::{admonition} Describing Data
:class: note dropdown
Chebychev's Theorem applies to distributions of any shape (normal or unnormal) whereas the empirical rule applies only to NORMAL distributions. … save for Week 2?
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
Data types and subsetting by group with the Arthritis package. Remember that we can use an ampersand (&) to join to conditions together, and then subset data. Use dim() to check the number of rows and columns, str() for data types, and summary() for a quick peek at the data frame.
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
Tabulation with the whiteside insulation data (select data by group) and create tables and proportion tables prop.table() using the Arthritis dataset.
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
Use tapply() or aggregate() to tabulate data by group, and note that you can use whatever function you want at the end (you don't have to use mean, you can use median or sd or any other custom function - more examples later on).
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
Figures and Graphics - high-level plot commands where R will automatically create a plot based on the data type, and an introduction to some lower-level plotting commands (adding an abline, annotating with text, xlab and ylab).
:::

:::{admonition} Summarizing Data and Visualization
:class: note dropdown
par() and opar() are used to create subplots (with defaults that are applied to each argument). How to plot curves, create univariate plots and bivariate plots. Correlograms to show the positive and negative relationship (correlation) between variables.
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
Reading in a .csv file into Google Colab, exploring the first few rows of data, summary statistics, converting data types (from numeric to character) and using gsub() to replace values.
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
Univariate and bivariate plots including scatterplots - adding a locally weighted smoother (lowess) line to the plot via the lines() function, and adding custom lines and points to graphs to help tell a better story with data.
:::

:::{admonition} Boston Housing EDA
:class: note dropdown
Advanced EDA - for loops for generating plots, using the describeBy() function from psych to analyze data by groups, saving .csv files to the local runtime (and downloading them on your computer).
:::
