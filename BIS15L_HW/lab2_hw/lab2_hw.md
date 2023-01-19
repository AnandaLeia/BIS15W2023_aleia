---
title: "Lab 2 Homework"
author: "Ananda Leia"
date: "1/17/2023"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?
Vectors are sets of data. They may be composed of any of the five classes of date (numeric, integer, character, logical, complex). In RStudio, they are entered into code chunks using the compand "c" for concatenate. When they are run, the vectors appear as objects in the environment quadrant of RStudio.

2. What is a data matrix in R?  
A data matrix is a series of stacked values, essentially a data table composed of multiple vectors.

3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.
Combine the vectors into 1:

```r
spring_temps <- c(spring_1,spring_2, spring_3, spring_4, spring_5, spring_6, spring_7, spring_8)
spring_temps
```

```
##  [1] 36.25 35.40 35.30 35.15 35.35 33.35 30.70 29.65 29.20 39.70 40.05 38.65
## [13] 31.85 31.40 29.30 30.20 30.65 29.75 32.90 32.50 32.80 36.80 36.45 33.15
```
Create hot spring matrix from single vector

```r
hot_spring_matrix <- matrix(spring_temps, nrow=8, byrow=T)
hot_spring_matrix
```

```
##       [,1]  [,2]  [,3]
## [1,] 36.25 35.40 35.30
## [2,] 35.15 35.35 33.35
## [3,] 30.70 29.65 29.20
## [4,] 39.70 40.05 38.65
## [5,] 31.85 31.40 29.30
## [6,] 30.20 30.65 29.75
## [7,] 32.90 32.50 32.80
## [8,] 36.80 36.45 33.15
```
5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.

```r
scientist <- c("Jill", "Steve", "Susan")
scientist
```

```
## [1] "Jill"  "Steve" "Susan"
```

```r
spring_names <- c("Bluebell Spring", "Opal Spring", "Riverside Spring", 
                  "Too Hot Spring", "Mystery Spring", 
                  "Emerald Spring", "Black Spring", "Pearl Spring")
spring_names
```

```
## [1] "Bluebell Spring"  "Opal Spring"      "Riverside Spring" "Too Hot Spring"  
## [5] "Mystery Spring"   "Emerald Spring"   "Black Spring"     "Pearl Spring"
```

```r
colnames(hot_spring_matrix) <- scientist
```

```r
rownames(hot_spring_matrix) <- spring_names
```

```r
hot_spring_matrix
```

```
##                   Jill Steve Susan
## Bluebell Spring  36.25 35.40 35.30
## Opal Spring      35.15 35.35 33.35
## Riverside Spring 30.70 29.65 29.20
## Too Hot Spring   39.70 40.05 38.65
## Mystery Spring   31.85 31.40 29.30
## Emerald Spring   30.20 30.65 29.75
## Black Spring     32.90 32.50 32.80
## Pearl Spring     36.80 36.45 33.15
```

```r
Average <- rowMeans(hot_spring_matrix)
Average
```

```
##  Bluebell Spring      Opal Spring Riverside Spring   Too Hot Spring 
##         35.65000         34.61667         29.85000         39.46667 
##   Mystery Spring   Emerald Spring     Black Spring     Pearl Spring 
##         30.85000         30.20000         32.73333         35.46667
```

```r
hot_spring_average_matrix <- cbind (hot_spring_matrix, Average)
hot_spring_average_matrix
```

```
##                   Jill Steve Susan  Average
## Bluebell Spring  36.25 35.40 35.30 35.65000
## Opal Spring      35.15 35.35 33.35 34.61667
## Riverside Spring 30.70 29.65 29.20 29.85000
## Too Hot Spring   39.70 40.05 38.65 39.46667
## Mystery Spring   31.85 31.40 29.30 30.85000
## Emerald Spring   30.20 30.65 29.75 30.20000
## Black Spring     32.90 32.50 32.80 32.73333
## Pearl Spring     36.80 36.45 33.15 35.46667
```
6. Calculate the mean temperature of all eight springs.
See the column "Average" in the matrix "hot_spring_average_matrix" above or run the code for "Average" below.

```r
Average
```

```
##  Bluebell Spring      Opal Spring Riverside Spring   Too Hot Spring 
##         35.65000         34.61667         29.85000         39.46667 
##   Mystery Spring   Emerald Spring     Black Spring     Pearl Spring 
##         30.85000         30.20000         32.73333         35.46667
```
7. Add this as a new column in the data matrix.
See "hot_spring_average_matrix" above.

```r
hot_spring_average_matrix
```

```
##                   Jill Steve Susan  Average
## Bluebell Spring  36.25 35.40 35.30 35.65000
## Opal Spring      35.15 35.35 33.35 34.61667
## Riverside Spring 30.70 29.65 29.20 29.85000
## Too Hot Spring   39.70 40.05 38.65 39.46667
## Mystery Spring   31.85 31.40 29.30 30.85000
## Emerald Spring   30.20 30.65 29.75 30.20000
## Black Spring     32.90 32.50 32.80 32.73333
## Pearl Spring     36.80 36.45 33.15 35.46667
```

8. Show Susan's value for Opal Spring only.

```r
hot_spring_average_matrix[2,3]
```

```
## [1] 33.35
```

```r
hot_spring_average_matrix["Opal Spring", "Susan"]
```

```
## [1] 33.35
```

9. Calculate the mean for Jill's column only.  

```r
Jill_Measurements <- hot_spring_average_matrix[ ,"Jill"]
Jill_Measurements
```

```
##  Bluebell Spring      Opal Spring Riverside Spring   Too Hot Spring 
##            36.25            35.15            30.70            39.70 
##   Mystery Spring   Emerald Spring     Black Spring     Pearl Spring 
##            31.85            30.20            32.90            36.80
```

```r
Jill_Average <- mean(Jill_Measurements)
Jill_Average
```

```
## [1] 34.19375
```

10. Use the data matrix to perform one calculation or operation of your interest.

```r
Scientist_Average <- colMeans(hot_spring_average_matrix)
Scientist_Average
```

```
##     Jill    Steve    Susan  Average 
## 34.19375 33.93125 32.68750 33.60417
```

```r
hot_springs_all_averages_matrix <- rbind(hot_spring_average_matrix, Scientist_Average)
hot_springs_all_averages_matrix
```

```
##                       Jill    Steve   Susan  Average
## Bluebell Spring   36.25000 35.40000 35.3000 35.65000
## Opal Spring       35.15000 35.35000 33.3500 34.61667
## Riverside Spring  30.70000 29.65000 29.2000 29.85000
## Too Hot Spring    39.70000 40.05000 38.6500 39.46667
## Mystery Spring    31.85000 31.40000 29.3000 30.85000
## Emerald Spring    30.20000 30.65000 29.7500 30.20000
## Black Spring      32.90000 32.50000 32.8000 32.73333
## Pearl Spring      36.80000 36.45000 33.1500 35.46667
## Scientist_Average 34.19375 33.93125 32.6875 33.60417
```

```r
Spring_SD = NULL
for (i in 1:nrow(hot_spring_matrix))
  {Spring_SD [i]=sd(hot_spring_matrix[i,])}

sd_spring_matrix <- cbind(hot_spring_matrix, Spring_SD)
sd_spring_matrix
```

```
##                   Jill Steve Susan Spring_SD
## Bluebell Spring  36.25 35.40 35.30 0.5220153
## Opal Spring      35.15 35.35 33.35 1.1015141
## Riverside Spring 30.70 29.65 29.20 0.7697402
## Too Hot Spring   39.70 40.05 38.65 0.7285831
## Mystery Spring   31.85 31.40 29.30 1.3610658
## Emerald Spring   30.20 30.65 29.75 0.4500000
## Black Spring     32.90 32.50 32.80 0.2081666
## Pearl Spring     36.80 36.45 33.15 2.0139100
```

```r
Scientist_SD = NULL
for (i in 1:ncol(hot_spring_matrix)) {Scientist_SD[i]=sd(hot_spring_matrix[ ,i])}

sd_scientist_matrix <- rbind(hot_spring_matrix, Scientist_SD)
sd_scientist_matrix
```

```
##                       Jill    Steve     Susan
## Bluebell Spring  36.250000 35.40000 35.300000
## Opal Spring      35.150000 35.35000 33.350000
## Riverside Spring 30.700000 29.65000 29.200000
## Too Hot Spring   39.700000 40.05000 38.650000
## Mystery Spring   31.850000 31.40000 29.300000
## Emerald Spring   30.200000 30.65000 29.750000
## Black Spring     32.900000 32.50000 32.800000
## Pearl Spring     36.800000 36.45000 33.150000
## Scientist_SD      3.329032  3.49499  3.279999
```
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
