# data.table.examples

https://github.com/Rdatatable/data.table/wiki
```
install.packages("data.table", type = "source",
    repos = "http://Rdatatable.github.io/data.table")
```

https://s3.amazonaws.com/assets.datacamp.com/img/blog/data+table+cheat+sheet.pdf

http://www.r-bloggers.com/advanced-tips-and-tricks-with-data-table/

GForce

```
set.seed(1L)
dt = lapply(1:20, function(x) sample(c(-100:100), 5e6L, TRUE))
setDT(dt)[, id := sample(1e5, 5e6, TRUE)]
print(object.size(dt), units="Mb") # 400MB, not huge, but will do

# optimisation of 'mean'
options(datatable.optimize = 1L) # optimisation 'on'
system.time(ans1 <- dt[, lapply(.SD, mean), by=id])
system.time(ans2 <- dt[, lapply(.SD, base::mean), by=id])
identical(ans1, ans2)
```

```
set.seed(45L)
DT <- data.table(V1=c(1L,2L),
V2=LETTERS[1:3],
V3=round(rnorm(4),4),
V4=1:12)

DT[, as.list(summary(V3)), V1]
```

```
microbenchmark::microbenchmark({setthreads(32); CJ(1:1000,1:10000)}, {setthreads(1); CJ(1:1000,1:10000)}, times = 500)

truelength
alloc.col
```

## foverlaps

`?foverlaps`

Usually, x is a very large data.table with small interval ranges, and y is much smaller keyed data.table with relatively larger interval spans

Very briefly, foverlaps() collapses the two-column interval in y to one-column of unique values to generate a lookup table, and then performs the join depending on the type of overlap, using the already available binary search feature of data.table.


| function | speed | usability |
| ---- | --- | --- |
| fread / fwrite |  |  |
| dt[i, j, by] |  |  |
| merge / rbind | | |
| inrange / foverlaps |  |  |
| dcast / melt |  |  |
| duplicated, frank etc. |  |  |

https://github.com/hadley/dtplyr
