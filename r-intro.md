r-intro
================

## Data Science <http://r4ds.had.co.nz/>

<img src="ds_pkg.png" align="right" width = 750 />

## <https://www.tidyverse.org/>

<img src="tidyverse.png" align="right" width = 750 />

# Transform data (~80% of your time)

## Tools for data science

``` r
library(tidyverse)
## -- Attaching packages --------------------------------------------- tidyverse 1.2.1 --
## v ggplot2 3.0.0     v purrr   0.2.5
## v tibble  1.4.2     v dplyr   0.7.6
## v tidyr   0.8.1     v stringr 1.3.1
## v readr   1.1.1     v forcats 0.3.0
## -- Conflicts ------------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

## Example dataset

``` r
library(fgeo.data)
dim(luquillo_tree6_random)
## [1] 1004   19
```

## Overview

``` r
luquillo_tree6_random
## # A tibble: 1,004 x 19
##    treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##     <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
##  1    104    143 10009 10009   DACE~ 113      10.3  245.    582850        6
##  2    119    158 1001~ 100104  MYRS~ 1021    183.   410.    578696        6
##  3    180    225 1001~ 100174  CASA~ 921     165.   410.    617049        6
##  4    602    736 1006~ 100649  GUAG~ 821     149.   414.    614253        6
##  5    631    775 10069 10069   PREM~ 213      38.3  245.    598429        6
##  6    647    793 1007~ 100708  SCHM~ 821     143.   411.    614211        6
##  7   1086   1339 10122 10122   DRYG~ 413      68.9  253.    603131        6
##  8   1144   1410 1012~ 101285  SCHM~ 920     161.   395.    616923        6
##  9   1168   1438 10131 10131   DACE~ 413      70.6  252.    603151        6
## 10   1380   1702 1015~ 101560  CASA~ 820     142.   386.    614023        6
## # ... with 994 more rows, and 9 more variables: dbh <dbl>, pom <chr>,
## #   hom <dbl>, ExactDate <dbl>, DFstatus <chr>, codes <chr>,
## #   nostems <dbl>, status <chr>, date <dbl>
```

## Main verbs

<img src="verbs.png" align="right" width = 750 />

``` r
tree <- luquillo_tree6_random
```

## Filter rows with `filter()`

``` r
filter(tree, sp == "PREMON", quadrat == "1017")
## # A tibble: 5 x 19
##   treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##    <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
## 1  23886  29878 14617 14617   PREM~ 1017     182.  330.    578115        6
## 2  23903  29911 14637 14637   PREM~ 1017     194.  334.    578189        6
## 3  23909  29927 14642 14642   PREM~ 1017     191.  337.    578196        6
## 4 122801 160013 38574 38574   PREM~ 1017     185.  324.    578109        6
## 5 125513     NA 14617 <NA>    PREM~ 1017     182.  330.        NA       NA
## # ... with 9 more variables: dbh <dbl>, pom <chr>, hom <dbl>,
## #   ExactDate <dbl>, DFstatus <chr>, codes <chr>, nostems <dbl>,
## #   status <chr>, date <dbl>
```

## Roughtly equivalent

``` r
tree[tree$sp == "PREMON" & tree$quadrat == "1017", ]
## # A tibble: 5 x 19
##   treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##    <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
## 1  23886  29878 14617 14617   PREM~ 1017     182.  330.    578115        6
## 2  23903  29911 14637 14637   PREM~ 1017     194.  334.    578189        6
## 3  23909  29927 14642 14642   PREM~ 1017     191.  337.    578196        6
## 4 122801 160013 38574 38574   PREM~ 1017     185.  324.    578109        6
## 5 125513     NA 14617 <NA>    PREM~ 1017     182.  330.        NA       NA
## # ... with 9 more variables: dbh <dbl>, pom <chr>, hom <dbl>,
## #   ExactDate <dbl>, DFstatus <chr>, codes <chr>, nostems <dbl>,
## #   status <chr>, date <dbl>
```

## Arrange rows with `arrange()`

``` r
arrange(tree, sp, quadrat)
## # A tibble: 1,004 x 19
##    treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##     <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
##  1  78221  95215 91969 91969   ALCF~ 518      90.4 340.     606006        6
##  2 104760 139181 1495~ 149560  ALCF~ 820     140.  395.     614037        6
##  3  59773  72453 69811 69811   ALCF~ 914     160.  268.     616272        6
##  4  19961  24771 12354 12354   ALCL~ 914     167.  270.     616286        6
##  5  19965  24786 1235~ 123547  ANDI~ 425      70.4 481.     604320        6
##  6  39681  48857 33319 33319   ANDI~ 810     146.  191.     612949        6
##  7 120711 157828 1687~ 168752  ARDG~ 1605    315.   91.6    595640        6
##  8  33658  42059 25092 25092   ARDG~ 1606    305.  107.     595666        6
##  9  49466  59981 57479 57479   ARTA~ 412      62.3 235.     603020        6
## 10  37703  46647 30594 30594   BRUP~ 1407    265.  123.     590198        6
## # ... with 994 more rows, and 9 more variables: dbh <dbl>, pom <chr>,
## #   hom <dbl>, ExactDate <dbl>, DFstatus <chr>, codes <chr>,
## #   nostems <dbl>, status <chr>, date <dbl>
```

## Arrange in descending order with `desc()`

``` r
arrange(tree, desc(sp), quadrat)
## # A tibble: 1,004 x 19
##    treeID stemID tag   StemTag sp    quadrat     gx    gy MeasureID
##     <int>  <int> <chr> <chr>   <chr> <chr>    <dbl> <dbl>     <int>
##  1  21971  27365 12600 12600   ZANM~ 115       0.01 280.     583015
##  2  98940 132754 1387~ 138778  UREB~ 1014    196.   262.     577799
##  3  58640  71135 68475 68475   UREB~ 1114    210.   269.     581419
##  4  35856  44596 28156 28156   UREB~ 306      45.7  103.     600399
##  5  43923  53793 46485 46485   UREB~ 409      78.0  161.     602836
##  6  34977  43627 27108 27108   TRIP~ 1005    188.    83.0    576789
##  7  37918  46881 30831 30831   TRIP~ 1207    221.   137.     584220
##  8  70362  85902 82942 82942   TRIP~ 1516    295.   315.     594238
##  9  21157  26316 1250~ 125043  TRIP~ 225      39.3  490.     599894
## 10  62931  76415 73761 73761   TRIP~ 317      56.2  330.     601329
## # ... with 994 more rows, and 10 more variables: CensusID <int>,
## #   dbh <dbl>, pom <chr>, hom <dbl>, ExactDate <dbl>, DFstatus <chr>,
## #   codes <chr>, nostems <dbl>, status <chr>, date <dbl>
```

## Select columns with `select()`

## Select by column name

``` r
select(tree, sp, quadrat, treeID, status, dbh)
## # A tibble: 1,004 x 5
##    sp     quadrat treeID status   dbh
##    <chr>  <chr>    <int> <chr>  <dbl>
##  1 DACEXC 113        104 A      195  
##  2 MYRSPL 1021       119 A       44.9
##  3 CASARB 921        180 A       46.1
##  4 GUAGUI 821        602 A       33.1
##  5 PREMON 213        631 A      139  
##  6 SCHMOR 821        647 A      248  
##  7 DRYGLA 413       1086 A      176  
##  8 SCHMOR 920       1144 A       75  
##  9 DACEXC 413       1168 A      613  
## 10 CASARB 820       1380 D       NA  
## # ... with 994 more rows
```

## Select range

``` r
select(tree, treeID:quadrat)
## # A tibble: 1,004 x 6
##    treeID stemID tag    StemTag sp     quadrat
##     <int>  <int> <chr>  <chr>   <chr>  <chr>  
##  1    104    143 10009  10009   DACEXC 113    
##  2    119    158 100104 100104  MYRSPL 1021   
##  3    180    225 100171 100174  CASARB 921    
##  4    602    736 100649 100649  GUAGUI 821    
##  5    631    775 10069  10069   PREMON 213    
##  6    647    793 100708 100708  SCHMOR 821    
##  7   1086   1339 10122  10122   DRYGLA 413    
##  8   1144   1410 101285 101285  SCHMOR 920    
##  9   1168   1438 10131  10131   DACEXC 413    
## 10   1380   1702 101560 101560  CASARB 820    
## # ... with 994 more rows
```

## Exclude range

``` r
select(tree, -(treeID:quadrat))
## # A tibble: 1,004 x 13
##       gx    gy MeasureID CensusID   dbh pom     hom ExactDate DFstatus
##    <dbl> <dbl>     <int>    <int> <dbl> <chr> <dbl>     <dbl> <chr>   
##  1  10.3  245.    582850        6 195   1.45   1.45     16911 alive   
##  2 183.   410.    578696        6  44.9 1.25   1.26     17017 alive   
##  3 165.   410.    617049        6  46.1 1.35   1.34     17017 alive   
##  4 149.   414.    614253        6  33.1 1.3    1.3      17011 alive   
##  5  38.3  245.    598429        6 139   1.25   1.25     16912 alive   
##  6 143.   411.    614211        6 248   1.35   1.35     17011 alive   
##  7  68.9  253.    603131        6 176   1.4    1.42     16913 alive   
##  8 161.   395.    616923        6  75   1.3    1.3      17015 alive   
##  9  70.6  252.    603151        6 613   1.25   1.25     16913 alive   
## 10 142.   386.    614023        6  NA   <NA>  NA        17014 dead    
## # ... with 994 more rows, and 4 more variables: codes <chr>,
## #   nostems <dbl>, status <chr>, date <dbl>
```

## Rename columns with `rename()`

``` r
rename(tree, tree_id = treeID)
## # A tibble: 1,004 x 19
##    tree_id stemID tag   StemTag sp    quadrat    gx    gy MeasureID
##      <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>
##  1     104    143 10009 10009   DACE~ 113      10.3  245.    582850
##  2     119    158 1001~ 100104  MYRS~ 1021    183.   410.    578696
##  3     180    225 1001~ 100174  CASA~ 921     165.   410.    617049
##  4     602    736 1006~ 100649  GUAG~ 821     149.   414.    614253
##  5     631    775 10069 10069   PREM~ 213      38.3  245.    598429
##  6     647    793 1007~ 100708  SCHM~ 821     143.   411.    614211
##  7    1086   1339 10122 10122   DRYG~ 413      68.9  253.    603131
##  8    1144   1410 1012~ 101285  SCHM~ 920     161.   395.    616923
##  9    1168   1438 10131 10131   DACE~ 413      70.6  252.    603151
## 10    1380   1702 1015~ 101560  CASA~ 820     142.   386.    614023
## # ... with 994 more rows, and 10 more variables: CensusID <int>,
## #   dbh <dbl>, pom <chr>, hom <dbl>, ExactDate <dbl>, DFstatus <chr>,
## #   codes <chr>, nostems <dbl>, status <chr>, date <dbl>
```

## Add new columns with mutate()

``` r
mutate(tree, 
  dbh_mm = dbh,
  dbh_m = dbh_mm / 1000
)
## # A tibble: 1,004 x 21
##    treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##     <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
##  1    104    143 10009 10009   DACE~ 113      10.3  245.    582850        6
##  2    119    158 1001~ 100104  MYRS~ 1021    183.   410.    578696        6
##  3    180    225 1001~ 100174  CASA~ 921     165.   410.    617049        6
##  4    602    736 1006~ 100649  GUAG~ 821     149.   414.    614253        6
##  5    631    775 10069 10069   PREM~ 213      38.3  245.    598429        6
##  6    647    793 1007~ 100708  SCHM~ 821     143.   411.    614211        6
##  7   1086   1339 10122 10122   DRYG~ 413      68.9  253.    603131        6
##  8   1144   1410 1012~ 101285  SCHM~ 920     161.   395.    616923        6
##  9   1168   1438 10131 10131   DACE~ 413      70.6  252.    603151        6
## 10   1380   1702 1015~ 101560  CASA~ 820     142.   386.    614023        6
## # ... with 994 more rows, and 11 more variables: dbh <dbl>, pom <chr>,
## #   hom <dbl>, ExactDate <dbl>, DFstatus <chr>, codes <chr>,
## #   nostems <dbl>, status <chr>, date <dbl>, dbh_mm <dbl>, dbh_m <dbl>
```

## Keep the new variables with `transmute()`

``` r
transmute(tree, 
  dbh_mm = dbh,
  dbh_m = dbh_mm / 1000
)
## # A tibble: 1,004 x 2
##    dbh_mm   dbh_m
##     <dbl>   <dbl>
##  1  195    0.195 
##  2   44.9  0.0449
##  3   46.1  0.0461
##  4   33.1  0.0331
##  5  139    0.139 
##  6  248    0.248 
##  7  176    0.176 
##  8   75    0.075 
##  9  613    0.613 
## 10   NA   NA     
## # ... with 994 more rows
```

## Summarise values with `summarise()`

``` r
summarise(tree,
  mean_dbh = mean(dbh, na.rm = TRUE)
)
## # A tibble: 1 x 1
##   mean_dbh
##      <dbl>
## 1     115.
```

## Randomly sample rows with `sample_n()`

``` r
sample_n(tree, 5)
## # A tibble: 5 x 19
##   treeID stemID tag   StemTag sp    quadrat    gx    gy MeasureID CensusID
##    <int>  <int> <chr> <chr>   <chr> <chr>   <dbl> <dbl>     <int>    <int>
## 1  23209  28941 13869 13869   LAEP~ 1016    195.  301.     578080        6
## 2  49561  60080 5758  5758    PREM~ 807     154.  138.     612615        6
## 3  28615  36279 19556 19556   PREM~ 1625    306.  493.     597377        6
## 4  48991  59449 5600  5600    PREM~ 307      55.4 125.     600495        6
## 5 122727 159939 35588 35588   PREM~ 905     172.   95.2    615386        6
## # ... with 9 more variables: dbh <dbl>, pom <chr>, hom <dbl>,
## #   ExactDate <dbl>, DFstatus <chr>, codes <chr>, nostems <dbl>,
## #   status <chr>, date <dbl>
```

# Learn more

## <https://www.rstudio.com/>

<img src="rstudio.png" align="right" width = 750 />

## <https://rstudio.cloud/learn/primers>

<img src="primers.png" align="right" width = 750 />

## <https://www.rstudio.com/resources/cheatsheets/>

<img src="cheet.png" align="right" width = 750 />
