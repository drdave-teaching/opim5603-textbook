# Module 3 — Hypothesis Testing

Our first real dive into inferential statistics: using a sample to say something about a population. We define hypothesis testing, work the five-step procedure, and run one- and two-sample tests for means and proportions, including paired (dependent) data.

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** (R notebooks).

- **Cheat Sheet Hypothesis Testing from Scratch** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Cheat_Sheet_Hypothesis_Testing_from_Scratch.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Cheat_Sheet_Hypothesis_Testing_from_Scratch.ipynb)
- **One Sample Tests summarized** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/One_Sample_Tests_summarized.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/One_Sample_Tests_summarized.ipynb)
- **Two Sample Tests Additional Problems** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Two_Sample_Tests_Additional_Problems.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5603-notebooks/blob/main/Module3/Two_Sample_Tests_Additional_Problems.ipynb)
:::

## 3.1 One-Sample Test of Hypothesis

### Video 1: The Five Steps of Hypothesis Testing

**Overview.** We provide some motivation for one-sample tests of hypothesis - which is our first real exposure to inferential statistics! There are many different flavors of hypothesis testing (one-sample tests, two-sample tests, pop. std. dev. known vs. unknown, testing for a mean of proportion). Regardless, you are trying to use a sample to show that your sample is SO EXTREME that you fundamentally reject your notion of reality (the population parameter that you are trying to disprove). Pay attention to the test statistic (calculated from the sample data you collected) and the critical value (which you will use qnorm() for).

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: Two-Tail Test: Pop. Std. Dev. Known

**Overview.** We get some practice writing the null and alternate hypothesis. We calculate the critical value(s) (z.half.alpha, big red lines) and shade the rejection region in blue. Then we calculate our test statistic (big purple line) and add it to the plot. If the purple line is in the rejection region (the tails), we reject the null hypothesis! Otherwise, we fail to reject the null hypothesis.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Upper-Tail Test: Pop. Std. Dev. Known

**Overview.** A one-tail test allows you to focus on more specific questions - like, 'did the new procedures at the factory result in a statistically significant increase in the number of desks we made?' This is different to the two-tail test where you say 'did the new procedures at the factory result in a statistically significant difference (regardless of direction) in the number of desks we made?' We focus a lot of DRAWING the critical value, the rejection region and the test statistic. You need to plug and chug the formula to calculate your test statistic (z). You will use qnorm() to get the critical value. If you are in the rejection region, namely - your sample is so extreme that you reject reality (the population parameter), you reject the null hypothesis!

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: Lower-Tail Test: Pop. Std. Dev. Unknown

**Overview.** In this example, we introduce t which is used when you don't know the population standard deviation (which is common!). Your test statistic is now 't' and your critical value is 't.alpha'. We show that if you change your level of significance, you could in fact declare that there is a difference (the claims processing cost is less) - but at the 0.01 level, you can't reject.

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Proportions

**Overview.** Everything you learned about one-tailed and two-tailed tests applies to proportions - the only difference is that you need to use a different method of calculating your test statistic (z). Keep in mind that proportions use the standard normal distribution so long as n > 5 and n(1-pi) > 5. This ensures that you have enough of a sample size to detect a rare event (think about it!)

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: More Examples on Hypothesis Testing

**Overview.** An overview of additional problems to really help the content stick. Try these on your own and appreciate the difference in test statistic values when you use the z and t distributions. Corresponds to (One Sample Hypothesis Testing - Examples (R)): https://drive.google.com/file/d/1z6T49B0i3YlCPDd59b-ePLavRidWiHaE/view?usp=sharing

*✍️ Full narrative coming from the lecture transcript.*

## 3.2 Two-Sample Tests of Hypothesis

### Video 1: Introduction to Two-Sample Tests of Hypothesis

**Overview.** A general overview of where we are going in these videos, and motivation for the types of problems we are trying to solve with a two-sample tests. We are going to look at examples when population standard deviations are known and unknown. When we have examples where pop standard deviation is unknown, we can assume that the variance in the groups are either the same (easier to declare statistical significance) or different (harder to declare statistical significance). We'll look at how we can deal with proportions, and how to deal with independent (random samples) or dependent (paired, before and after a drug trial intervention), and how we declare statistical significance.

*✍️ Full narrative coming from the lecture transcript.*

### Video 2: Comparing Population Means when Pop. Std. Dev. is Known

**Overview.** A one-tail test when a) samples come from independent populations and b) both population standard deviations are known (NOTE: we rarely know this! This is a toy example). We show how to calculate our test statistic, z, to show that the difference in groups is significantly different than 0. I think the tough part in the grocery example is writing out the null and alternate hypothesis - the null hypothesis is that the checkout time for the Standard method is less than or equal to Fast Lane. The alternate hypothesis is that the Standard method is greater than the Fast Lane method.

*✍️ Full narrative coming from the lecture transcript.*

### Video 3: Comparing Proportions for Different Populations

**Overview.** We will use z as our test statistic here (normal approximation to the binomial) and will see that compared to the one sample test, we have some extra terms in the formula. We learn a new term 'pooled proportion' or (p sub c), which I like to think of as a 'global' proportion… with our perfume example, the pooled proportion might just represent a random sample of 'women' instead of 'younger women' and 'older women'. Be careful calculating the p-value for this example - by switching p1 and p2 you could end up on either side of the rejection region, and so you need to multiply by 2.

*✍️ Full narrative coming from the lecture transcript.*

### Video 4: Comparing Population Means when Pop. Std. Dev. is Unknown - Assume Equal

**Overview.** An example comparing two manufacturing techniques - one has a lower average time and a higher standard deviation, one group has a higher average time but a lower standard deviation - what do we do?! We pool our variance, assume that each group has equal variance, and will use the t distribution (which gives us a penalty/more uncertainty = harder to declare statistical significance.) We declare that there is no difference between the two groups.

*✍️ Full narrative coming from the lecture transcript.*

### Video 5: Comparing Population Means when Pop. Std. Dev. is Unknown - Assume Unequal

**Overview.** Chugging right along here - we know it's eas(ier) to declare statistical significance when the pop std dev is known - it's a little hard(er) to declare statistical significance when the pop std dev is unknown and you make a simplifying assumption that the variance in each group is equal (but, do you really know this?!) - it is hardest to declare significance when you don't know the pop std dev and you assume that the variance in each group might be unequal! This is penalizing but in the best way, because if you can declare significance when pop std dev is unknown and variance is unequal in each group, you can feel really good about it.

*✍️ Full narrative coming from the lecture transcript.*

### Video 6: Two-Sample Test for Dependent Samples (Paired Tests)

**Overview.** Paired tests are great - we see them all the time in medicine (a person's blood pressure before and after a surgery) and business (speed for a machine to produce a widget before and after maintenance). We are visiting the sample observation twice - in our example, we have 10 houses. Mortgage Company A appraises the value of the 10 houses. Mortgage Company B appraises the value of the same 10 houses. Can you conclude whether or not there is a difference in the average appraisal of these ten homes? We find it's easier to declare significance with a paired sample.

*✍️ Full narrative coming from the lecture transcript.*

### Video 7: Comparison of Dependent vs. Independent Tests

**Overview.** If you have paired data - use the paired test! The denominator in the test statistic, t, is smaller in the paired data example vs. the independent random samples (where we need to pool our variance). You may incorrectly fail to declare statistical significance if you use a regular t-test instead of the paired t-test!

*✍️ Full narrative coming from the lecture transcript.*

## Wrap-up

```{admonition} Key takeaways
:class: tip
- The **five-step** hypothesis-testing procedure; one-tailed vs. two-tailed.
- Test statistic vs. **critical value** (`qnorm`/`qt`); reject when the sample is extreme.
- Use **z** when σ is known, **t** when σ is unknown (more uncertainty = harder to reject).
- **Paired** tests beat independent tests when data is naturally paired (before/after).
```

---

## 📌 Lecture key points

*Quick reference — one card per lecture (click to expand).*

:::{admonition} The Five Steps of Hypothesis Testing
:class: note dropdown
We provide some motivation for one-sample tests of hypothesis - which is our first real exposure to inferential statistics! There are many different flavors of hypothesis testing (one-sample tests, two-sample tests, pop. std. dev. known vs. unknown, testing for a mean of proportion). Regardless, you are trying to use a sample to show that your sample is SO EXTREME that you fundamentally reject your notion of reality (the population parameter that you are trying to disprove). Pay attention to the test statistic (calculated from the sample data you collected) and the critical value (which you will use qnorm() for).
:::

:::{admonition} Two-Tail Test: Pop. Std. Dev. Known
:class: note dropdown
We get some practice writing the null and alternate hypothesis. We calculate the critical value(s) (z.half.alpha, big red lines) and shade the rejection region in blue. Then we calculate our test statistic (big purple line) and add it to the plot. If the purple line is in the rejection region (the tails), we reject the null hypothesis! Otherwise, we fail to reject the null hypothesis.
:::

:::{admonition} Upper-Tail Test: Pop. Std. Dev. Known
:class: note dropdown
A one-tail test allows you to focus on more specific questions - like, 'did the new procedures at the factory result in a statistically significant increase in the number of desks we made?' This is different to the two-tail test where you say 'did the new procedures at the factory result in a statistically significant difference (regardless of direction) in the number of desks we made?' We focus a lot of DRAWING the critical value, the rejection region and the test statistic. You need to plug and chug the formula to calculate your test statistic (z). You will use qnorm() to get the critical value. If you are in the rejection region, namely - your sample is so extreme that you reject reality (the population parameter), you reject the null hypothesis!
:::

:::{admonition} Lower-Tail Test: Pop. Std. Dev. Unknown
:class: note dropdown
In this example, we introduce t which is used when you don't know the population standard deviation (which is common!). Your test statistic is now 't' and your critical value is 't.alpha'. We show that if you change your level of significance, you could in fact declare that there is a difference (the claims processing cost is less) - but at the 0.01 level, you can't reject.
:::

:::{admonition} Proportions
:class: note dropdown
Everything you learned about one-tailed and two-tailed tests applies to proportions - the only difference is that you need to use a different method of calculating your test statistic (z). Keep in mind that proportions use the standard normal distribution so long as n > 5 and n(1-pi) > 5. This ensures that you have enough of a sample size to detect a rare event (think about it!)
:::

:::{admonition} More Examples on Hypothesis Testing
:class: note dropdown
An overview of additional problems to really help the content stick. Try these on your own and appreciate the difference in test statistic values when you use the z and t distributions. Corresponds to (One Sample Hypothesis Testing - Examples (R)): https://drive.google.com/file/d/1z6T49B0i3YlCPDd59b-ePLavRidWiHaE/view?usp=sharing
:::

:::{admonition} Introduction to Two-Sample Tests of Hypothesis
:class: note dropdown
A general overview of where we are going in these videos, and motivation for the types of problems we are trying to solve with a two-sample tests. We are going to look at examples when population standard deviations are known and unknown. When we have examples where pop standard deviation is unknown, we can assume that the variance in the groups are either the same (easier to declare statistical significance) or different (harder to declare statistical significance). We'll look at how we can deal with proportions, and how to deal with independent (random samples) or dependent (paired, before and after a drug trial intervention), and how we declare statistical significance.
:::

:::{admonition} Comparing Population Means when Pop. Std. Dev. is Known
:class: note dropdown
A one-tail test when a) samples come from independent populations and b) both population standard deviations are known (NOTE: we rarely know this! This is a toy example). We show how to calculate our test statistic, z, to show that the difference in groups is significantly different than 0. I think the tough part in the grocery example is writing out the null and alternate hypothesis - the null hypothesis is that the checkout time for the Standard method is less than or equal to Fast Lane. The alternate hypothesis is that the Standard method is greater than the Fast Lane method.
:::

:::{admonition} Comparing Proportions for Different Populations
:class: note dropdown
We will use z as our test statistic here (normal approximation to the binomial) and will see that compared to the one sample test, we have some extra terms in the formula. We learn a new term 'pooled proportion' or (p sub c), which I like to think of as a 'global' proportion… with our perfume example, the pooled proportion might just represent a random sample of 'women' instead of 'younger women' and 'older women'. Be careful calculating the p-value for this example - by switching p1 and p2 you could end up on either side of the rejection region, and so you need to multiply by 2.
:::

:::{admonition} Comparing Population Means when Pop. Std. Dev. is Unknown - Assume Equal
:class: note dropdown
An example comparing two manufacturing techniques - one has a lower average time and a higher standard deviation, one group has a higher average time but a lower standard deviation - what do we do?! We pool our variance, assume that each group has equal variance, and will use the t distribution (which gives us a penalty/more uncertainty = harder to declare statistical significance.) We declare that there is no difference between the two groups.
:::

:::{admonition} Comparing Population Means when Pop. Std. Dev. is Unknown - Assume Unequal
:class: note dropdown
Chugging right along here - we know it's eas(ier) to declare statistical significance when the pop std dev is known - it's a little hard(er) to declare statistical significance when the pop std dev is unknown and you make a simplifying assumption that the variance in each group is equal (but, do you really know this?!) - it is hardest to declare significance when you don't know the pop std dev and you assume that the variance in each group might be unequal! This is penalizing but in the best way, because if you can declare significance when pop std dev is unknown and variance is unequal in each group, you can feel really good about it.
:::

:::{admonition} Two-Sample Test for Dependent Samples
:class: note dropdown
Paired tests are great - we see them all the time in medicine (a person's blood pressure before and after a surgery) and business (speed for a machine to produce a widget before and after maintenance). We are visiting the sample observation twice - in our example, we have 10 houses. Mortgage Company A appraises the value of the 10 houses. Mortgage Company B appraises the value of the same 10 houses. Can you conclude whether or not there is a difference in the average appraisal of these ten homes? We find it's easier to declare significance with a paired sample.
:::

:::{admonition} Comparison of Dependent vs. Independent Tests
:class: note dropdown
If you have paired data - use the paired test! The denominator in the test statistic, t, is smaller in the paired data example vs. the independent random samples (where we need to pool our variance). You may incorrectly fail to declare statistical significance if you use a regular t-test instead of the paired t-test!
:::
