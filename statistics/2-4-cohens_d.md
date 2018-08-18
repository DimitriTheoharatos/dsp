[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

>> To solve this problem, we will need to first break the original pregnancy date frames into two distinct data frames: the first born and not first born.  We can do this as follows:

```python
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]
```
Note that the live data frame contains all of the rows in the pregnancy data in which there was a live birth.  To compute the Cohen Effect size, use the function below, which is found in the Think Stats textbook:

```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
```

Finally, we can call this function, for both the total weight and pregnancy lengths for both first born babies and not first born babies to compare the differences. 

```python
print("Pregnancy Length Cohen Effect Size: " + 
      str(CohenEffectSize(firsts.prglngth, others.prglngth)))

print("Total Weight Cohen Effect Size:    " + 
      str(CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)))
```

This results in a Cohen Effect size of approximately 0.029 and -0.089 for pregancy length and total weight, respectively. In plain English, this means that mothers with first babies have a longer mean pregnancy length by approximately 0.03 standard deviations, which is very small. Furthermore, the average weight of first babies is smaller by approximately 0.09 standard deviations, which is also insignficant. 