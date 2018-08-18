[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)


## Solution

This problem uses the NSFG respondent variable `numkdhh` to construct the distribution for the number of children under 18 in the respondent's households.  This can be done with the following code:

```python
#read in the data
resp = nsfg.ReadFemResp()

#compute the PMF using the thinkstats2 package
actual_pmf = thinkstats2.Pmf(resp.numkdhh, label='Actual')

#plot the actual PMF
thinkplot.Pmf(actual_pmf)
thinkplot.Config(xlabel='Number of Children in Household', ylabel='PMF')
```



The above code results in the following plot:

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/Q2_1.png)


Now that we have the actual distribution, we can calculate the biased PMF using the following function:

```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```

Once we call this function, we can plot it alongside the actual PMF as follows:

```python
biased_pmf = BiasPmf(unbiased_pmf, label = 'Biased')
thinkplot.PrePlot(2)
thinkplot.Pmfs([actual_pmf, biased_pmf])
thinkplot.Config(xlabel='Number of children in Household', ylabel='PMF')
```

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/Q2_2.png)

Finally, we compute the means using the Pf object's mean function:

```python
print('Actual mean', actual_pmf.Mean())
print('Observed mean', biased_pmf.Mean())
```


| Actual Mean   | Biased Mean   | 
| ------------- |:-------------:| 
| 1.024         | 2.404         |

