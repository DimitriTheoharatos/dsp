[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

### Solution

In order to solve this problem, the norm function from the scipy.stats.norm module is used.  

First, we must create a normal distribution model with mean 178 cm and standard deviation 7.7 cm to model the heights of the US male population. This is done using the scipy.stats.norm function. 

```python
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
```

Since we are trying to find the percentage of the male population between the heights 5'10" and 6'1", we must first convert these to centimeters, which are 177.8 and 185.42 cm respectively.  Then, we find the CDFs for each of these values, and calculate the difference.  Doing so will give you the proportion of the US male population that falls within that range:

```python
#5'10 and 6'1 in centimeters
lower_bound = 177.8
upper_bound = 185.42

#convert these to CDFs
lower = dist.cdf(lower_bound)
higher = dist.cdf(upper_bound)

#calculate the difference between the two CDFs
(higher - lower)
```

Doing the above calculations results in the following percentage: 34.27%.  This means that 34.27% of the US male population is allowed to be in the Blue Man Group- sadly, I didn't make the cut. 