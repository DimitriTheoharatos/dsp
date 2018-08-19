[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

### Solution
In this question, we draw a sample with sizes 10,100, and 1000 from an exponential distribution with lambda = 2.  I then calculated the standard errors and 90% confidence intervals for each of these sample sizes.  The code is shown below:

```python
def SimulateSample(sample_sizes):
    lam = 2
    trials = 1000
    SE = []
    CI = []
    cdfs = []
    
    for j in sample_sizes:
        L = []
        for i in range(trials):
            l_s = np.random.exponential(1.0 / lam, j)
            L.append(1 / np.mean(l_s))
        SE.append(RMSE(L, lam))
        cdf = thinkstats2.Cdf(L)
        cdfs.append(thinkstats2.Cdf(L))
        CI.append((cdf.Percentile(5),cdf.Percentile(95)))

    thinkplot.PrePlot(len(sample_sizes))
    for i,cdf in enumerate(cdfs):
        thinkplot.Cdf(cdf, label = "N = %d" % sample_sizes[i])
    thinkplot.Config(xlabel='Sample mean',ylabel = 'CDF')

    return SE, CI

```

This produces the following values for the standard errors, and confidence intervals:

|Sample Size| Standard Error     | Confidence Interval|
|:---------:|:------------------:|:------------------:|
|10         | 0.804              | [1.298, 3.583]     |
|100        | 0.20               | [1.696, 2.355]     |
|1000       | 0.062              | [1.9, 2.103]       |

As the sample size increases, the standard error of our estimator decreases and our confidence interval becomes more tightly bound. This makes intuitive sense, since as our sample size increase, we have more confidence that our sammple is an accurate representation of the population.  This is also depicted in the following plot:

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/8-2_1.png)
