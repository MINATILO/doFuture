# doFuture: Foreach Parallel Adaptor using the Future API of the 'future' Package

## Introduction
The [future] package provides a generic API for using futures in R.
A future is a simple yet powerful mechanism to evaluate an R expression
and retrieve its value at some point in time.  Futures can be resolved
in many different ways depending on which strategy is used.
There are various types of synchronous and asynchronous futures to
choose from in the [future] package.
Additional futures are implemented in other packages.
For instance, the [future.BatchJobs] package provides futures for
_any_ type of backend that the [BatchJobs] package supports.
For an introduction to futures in R, please consult the
vignettes of the [future] package.

The [doFuture] package provides a `%dopar%` adaptor for the [foreach]
package that works with _any_ type of future.
Below is an example showing how to make `%dopar%` work with
_multiprocess_ futures.  A multiprocess future will be evaluated in
parallel using forked processes.  If process forking is not supported
by the operating system, then multiple background R sessions will
instead be used to resolve the futures.

```r
library('doFuture')
registerDoFuture()
plan(multiprocess)

mu <- 1.0
sigma <- 2.0
foreach(i=1:3) %dopar% {
  rnorm(i, mean=mu, sd=sigma)
}
```

To do the same on high-performance computing (HPC) cluster, the
[future.BatchJobs] package can be used.  Assuming BatchJobs has
been configured for the HPC cluster, then just use:
```r
plan(future.BatchJobs::batchjobs)
```


## Comparison to other doNnn packages

Due to the generic nature of future, the [doFuture] package
provides the same functionality as many of the existing doNnn
packages combined.

### doMC()
Instead of using
```r
library('doMC')
registerDoMC()
```
one can use
```r
library('doFuture')
registerDoFuture()
plan(multicore)
```

### doParallel()
Instead of using
```r
library('doParallel')
registerDoParallel()
```
one can use
```r
library('doFuture')
registerDoFuture()
plan(multiprocess)
```

Instead of using
```r
library('doParallel')
cl <- makeCluster(4)
registerDoParallel(cl)
```
one can use
```r
library('doFuture')
registerDoFuture()
cl <- makeCluster(4)
plan(cluster, cluster=cl)
```

### doSNOW()
Instead of using
```r
library('doSNOW)
cl <- makeCluster(4)
registerDoSNOW(cl)
```
one can use
```r
library('doFuture')
registerDoFuture()
cl <- makeCluster(4)
plan(cluster, cluster=cl)
```


There are currently no known `doFuture` alternatives for the `doMPI` and `doRedis` packages.




[BatchJobs]: http://cran.r-project.org/package=BatchJobs
[doFuture]: https://github.com/HenrikBengtsson/doFuture
[foreach]: http://cran.r-project.org/package=foreach
[future]: http://cran.r-project.org/package=future
[future.BatchJobs]: https://github.com/HenrikBengtsson/future.BatchJobs

## Installation
R package doFuture is only available via [GitHub](https://github.com/HenrikBengtsson/doFuture) and can be installed in R as:
```r
source('http://callr.org/install#HenrikBengtsson/doFuture')
```




## Software status

| Resource:     | GitHub        | Travis CI     | Appveyor         |
| ------------- | ------------------- | ------------- | ---------------- |
| _Platforms:_  | _Multiple_          | _Linux_       | _Windows_        |
| R CMD check   |  | <a href="https://travis-ci.org/HenrikBengtsson/doFuture"><img src="https://travis-ci.org/HenrikBengtsson/doFuture.svg" alt="Build status"></a> | <a href="https://ci.appveyor.com/project/HenrikBengtsson/dofuture"><img src="https://ci.appveyor.com/api/projects/status/github/HenrikBengtsson/doFuture?svg=true" alt="Build status"></a> |
| Test coverage |                     |    |                  |
