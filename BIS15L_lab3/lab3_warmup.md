---
title: "Lab 3 Warmup"
author: "Ananda Leia"
date: "2023-01-17"
output: 
  html_document: 
    keep_md: yes
---
### Make height vector

```r
plant_1h <- 30.7
plant_2h <- 37.6
plant_3h <- 28.4
plant_4h <- NA
plant_5h <- 33.2
```


```r
plant_heights <- c(plant_1h, plant_2h, plant_3h, plant_4h, plant_5h)
plant_heights
```

```
## [1] 30.7 37.6 28.4   NA 33.2
```
### Make mass vector

```r
plant_1m <- 4
plant_2m <- 5.2
plant_3m <- 3.7
plant_4m <- NA
plant_5m <- 4.6
```


```r
plant_masses <- c(plant_1m, plant_2m, plant_3m, plant_4m, plant_5m)
plant_masses
```

```
## [1] 4.0 5.2 3.7  NA 4.6
```
### Create data matrix

```r
plant_data <- c(plant_1h, plant_2h, plant_3h, plant_4h, plant_5h, plant_1m, plant_2m, plant_3m, plant_4m, plant_5m)
plant_data
```

```
##  [1] 30.7 37.6 28.4   NA 33.2  4.0  5.2  3.7   NA  4.6
```

```r
plant_matrix <- matrix(plant_data, nrow=5, byrow=F)
plant_matrix
```

```
##      [,1] [,2]
## [1,] 30.7  4.0
## [2,] 37.6  5.2
## [3,] 28.4  3.7
## [4,]   NA   NA
## [5,] 33.2  4.6
```
### Label data matrix

```r
plant_names <- c("Plant 1", "Plant 2", "Plant 3", "Plant 4", "Plant 5")
plant_names
```

```
## [1] "Plant 1" "Plant 2" "Plant 3" "Plant 4" "Plant 5"
```

```r
data_type <- c("Height", "Mass")
data_type
```

```
## [1] "Height" "Mass"
```


```r
rownames(plant_matrix) <- plant_names
```

```r
colnames(plant_matrix) <- data_type
```

```r
plant_matrix
```

```
##         Height Mass
## Plant 1   30.7  4.0
## Plant 2   37.6  5.2
## Plant 3   28.4  3.7
## Plant 4     NA   NA
## Plant 5   33.2  4.6
```
### Calculate means

```r
Average <- colMeans(plant_matrix, na.rm=T)
Average
```

```
## Height   Mass 
## 32.475  4.375
```
### Add means to data matrix

```r
all_plant_matrix <- rbind(plant_matrix, Average)
all_plant_matrix
```

```
##         Height  Mass
## Plant 1 30.700 4.000
## Plant 2 37.600 5.200
## Plant 3 28.400 3.700
## Plant 4     NA    NA
## Plant 5 33.200 4.600
## Average 32.475 4.375
```



