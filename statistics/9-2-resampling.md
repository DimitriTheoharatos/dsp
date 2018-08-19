[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

### Solution

In this problem, we simulate the null hypothesis using resampling instead of permutations.  To do so, I created a class called `DiffMeansResample` that inherits from `DiffMeansPremute`.  The only difference between the classes is the `RunModel` method, which now resamples rather than permutates.  This class is replicated below:

```python 
class DiffMeansResample(DiffMeansPermute):
    def RunModel(self):
        data1 = np.random.choice(self.pool, self.n, replace = True)
        data2 = np.random.choice(self.pool, self.m, replace = True)
        return data1, data2
```

Now that we have our class generated, we can use this model to test the differences in pregnancy length and birth weight. The code to do so for pregnancy length is as follows:

```python
live, firsts, others = first.MakeFrames()
data = firsts.prglngth.values, others.prglngth.values
ht = DiffMeansResample(data)
pvalue = ht.PValue()
pvalue
```


Doing the above results in pvalues of 0.159 and 0 for differences in pregnancy length and birth weight, respectively.  This is not very different from using permutations.  