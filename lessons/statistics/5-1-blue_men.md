[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

## According to the Blue Man Group, you have to be between 5'10'' and 6'1'' to apply. What is the percentage of U.S male population that is in this range?

### We will be using the BRFSS dataset to answer this question. First we begin by importing and cleaning the relavent data.

```
import brfss
import scipy
df = brfss.ReadBrfss()
#From brfss.py, I found that 1 == Male, 2 == Female
heights = df[df.sex == 1].htm3.dropna()

```

### Since the distrubution of human height can be modelled very effectively by a normal distribution, I will make a normal distribution based on the mean and standard deviation of the data set.

```
mean = heights.mean()
std = heights.std()
dist = scipy.stats.norm(loc=mean, scale=std)
```

### With our model in place, I can use the CDF of the distribution to answer the question, but first, note that P(a<X<=b) = P(X<=b) - P(X<=a).

```
prob = dist.cdf(185.42) - dist.cdf(177.8) #Heights converted to cm
```

### So the probability of being able to apply, given that you are male is .343. To fix for total population, we just need to find the probability of being male.

```
151800000/328200000 = 0.463
```
### This does the trick, given a total population of 328.2 million and male population of 151.8 million, there is a .463 chance of being male, so the probability of being able to apply to the blue man group is .463*.343 = .159! I guess the blue man group is more selective than I originally thought, maybe they should make it the blue people group to be more with the times.