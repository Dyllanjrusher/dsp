[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)
## We are asked to look at Cohen's d effect size measure on first born children and other born children on their total weight and their mother's pregnancy length. In other words, we are asked to  measure the effect of first borns on weight and pregnancy length compared to the weight  and pregnancy length of other born children. 

### First we need a function to compute Cohen's d. Then we break up our data into first born pregnancies and other born pregnancies.

```def Cohen(g1, g2):
    '''Compute's Cohen's effect size for 2 groups.
    
    gn: Series or DataFrame
    
    returns: float if args are Series;
            Series if args are Dataframes
    '''
    mean_diff = g1.mean() - g2.mean()
    n1, n2 = len(g1), len(g2)
    
    pooled_var = (n1*g1.var() + n2*g2.var())/(n1+n2)
    return mean_diff / np.sqrt(pooled_var)
    
    firsts = live[live.birthord == 1]
    others = live[live.birthord != 1]
    Cohen(firsts.totalwgt_lb, others.totalwgt_lb)
```
### Thus Cohen's d is -.09 for totalwgt_lb between the first born child and the others. Furthermore, 
```
Cohen(firsts.prglngth, others.prglngth)
```
### gives us a Cohen d of 0.029 for pregnancy length. Cohen suggested that a Cohen d below .2 should be considers a "small" effect. Thus, The difference between groups to the variability within groups of pregnancy length is extremely small. Furthermore The difference between groups to the variability within groups of the total weight is very small and inversly related. Thus, under this effect size measure, there is practically no effect on pregnancy length and a very small effect on weight of the baby. This makes sense because the longer you keep the baby in the womb, the longer the baby has time to grow.

