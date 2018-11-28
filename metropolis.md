

### Metropolis Algorithm: a very simple example


Here we show how the Metropolis algorithm can be used to draw samples from a target distribution (`p()`) generating candidates 
from another distribution (q`(x)`). For the metropolis algorithm `q(x)` must be symmetric and have the same support than that of `p(x)`.

In the example below `x~N(0,1)`; we draw `n` samples from this distribution and use these samples for comparison with samples drawn
with a Metropolis algorithm.

```r
 n=100000    # number of samples we want to draw
 x=rnorm(n)  # samples from the target distribution (used for comparison only).
 
 z= rep(NA,n) 
 z[1]=-1
 for(i in 2:n){
 	candidate=runif(min=-5,max=5,n=1) # symmetric candidate generator
 	r=dnorm(candidate)/dnorm(z[i-1])
 	accept<-runif(1)<r
 	if(accept){
 		z[i]=candidate
 	}else{
 		z[i]=z[i-1]
 	}
 	print(i)
 	
 }
 
 plot(density(x),col=4)
 tmp=density(z)
 lines(x=tmp$x,y=tmp$y,col=2)
 
```
We will use this algorithm to draw samples from the posterior distribution of a logistic regression model. The following [sampler]() implements that.
