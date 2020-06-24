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

### Since the US male population is approximately 151.8 million,

```
us_male_pop = 151800000 
answer = prob*us_male_pop
```

### gives us 52102447 people able to apply to the blue man group. 
