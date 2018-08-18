[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

### Solution

The following solution investigates the distribution of wealth in the United States by finding several statistics (median, mean, skew, and Pearson skew).  The data was gathered from the Current Population Survey and is in the form of various income ranges ranging from bins of under $5000 to above $250,000. 

The following functions were used to calculate each statistic:

```python
def Median(xs):
    cdf = thinkstats2.Cdf(xs)
    return cdf.Value(0.5)

 def StandardizedMoment(xs, k):
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    return CentralMoment(xs, k) / std**k   

def Skewness(xs):
    return StandardizedMoment(xs, 3)

def PearsonMedianSkewness(xs):
    median = Median(xs)
    mean = RawMoment(xs, 1)
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    gp = 3 * (mean - median) / std
    return gp
```

Using the above functions results in the following:


| Statistic     | Value         |
| ------------- |:-------------:|
| Median        | $51226.45     | 
| Mean          | $74278.71     | 
|Skewness       | 4.95          | 
|Pearson Skew   | 0.736         |


Note that the above values were computed under the assumption that the highest income is one million dollars, which is clearly not true.  However, even with this conservative limit, there is still a clear right skew of the distribution, since both normalized skew values are positive and the mean is significantly larger than the median. 

In order to find the fraction of people below the mean income, we can use the Cdf's class Prob function:

```python 
cdf.Prob(Mean(sample))
```

This returns a value of 0.66, meaning that around two-thirds of the population makes below the average income in this country, given this model. 