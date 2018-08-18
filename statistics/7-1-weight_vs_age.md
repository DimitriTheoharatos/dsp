[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

### Solution

In this problem, the relationship between a mother's age and her baby's birth weight is investigated.  First, a scatterplot is generated to visualize any correlations.  The code and plots are shown below:

```python
mother_age = live['agepreg']
baby_weight = live['totalwgt_lb']
thinkplot.Scatter(mother_age, baby_weight, alpha=0.1)
thinkplot.Config(xlabel="Mother's Age (yrs)",
                 ylabel="Baby's Weight (lbs)",
                 axis=[10, 45, 0, 16],
                 legend=False)
```

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/7-1_1.png)




An initial glance at the above plot implies that there is little to no correlation between the two variables, but we can verify by calculating the Pearson and Spearman Correlation coefficients:

```python

def SpearmanCorr(xs, ys):
    xs = pd.Series(xs)
    ys = pd.Series(ys)
    return xs.corr(ys, method='spearman')

def Corr(xs, ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    meanx, varx = thinkstats2.MeanVar(xs)
    meany, vary = thinkstats2.MeanVar(ys)

    corr = Cov(xs, ys, meanx, meany) / np.sqrt(varx * vary)
    return corr
 ```

 Using the above functions, we get values of 0.069 and 0.095 for the Pearson and Spearman coefficients, implying no correlation as suggested by the plot.  

 Finally, we can plot the percentiles to see if we can detect any patterns at either end of the interquartile range (25/75th percentiles) and the median. 
 
 ```python
bins = np.arange(10, 45, 5)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

ages = [group.agepreg.mean() for i, group in groups][1:-1]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]

thinkplot.PrePlot(3)
for percent in [75, 50, 25]:
    weight_percentiles = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages, weight_percentiles, label=label)

thinkplot.Config(xlabel="Mother's age (yrs)",
                     ylabel='Birth weight (lbs)',
                     xlim=[16, 42], legend=True)
 ```  

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/7-1_2.png)

The percentile plot also does not look to have a strong correlation- though it seems that each group tends to increase as the mother's age increases from 15 to 25.  Based on the previous scatterplot and correlation computations however, it does not seem to be a compelling correlation. 