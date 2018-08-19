[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

### Solution

In this question, the number of goals scored in a game is modeled by modeling the time between goals as an exponential distribution.  We first simulate a single game with the following code:

```python
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
```

Once we simulate a single game, we can build on this code to simulate N games as follows:

```python
def SimulateNGames(lam, N):
    games = [SimulateGame(lam) for game in range(N)]
    rmse = RMSE(games, lam)
    mean_error = MeanError(games, lam)
    return rmse, mean_error, games
```

It will be useful to look at the histogram for the distribution of values using this simulation setup.  I do so with the following:

```python
def histogram(N_simulations):
    hist = thinkstats2.Hist(N_simulations[2])
    thinkplot.Hist(hist)
    thinkplot.Config(xlabel = 'Goals Scored', ylabel = 'Count')
    print("rmse = %f" %N_simulations[0])
    print("Mean Error = %f" %N_simulations[1])

```

When the goals scored on average is five and 100,000 games are simulated, the following distribution forms:

![alt text](https://github.com/DimitriTheoharatos/dsp/blob/master/statistics/exercise_images/8-3_1.png)

In order to determine if our estimator is unbiased, we can look at the mean error as the sample size increases.  These results are shown below:

| Sample Size   | Mean Error    | RMSE  |
|:-------------:|:-------------:|:-----:|
| 10            | 0.2           | 1.612 |
| 1000          | -0.086        | 2.333 |
| 100000        | 0.0018        | 2.237 |


Since the mean error tends towards zero as the sample size is increasing, I would consider this an unbiased estimator. 
