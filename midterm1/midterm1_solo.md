---
title: "Midterm 1"
author: "Ananda Leia"
date: "1/31/2023"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("midterm_data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?

```r
names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
str(ecosphere)
```

```
## spc_tbl_ [551 × 21] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ order                      : chr [1:551] "Anseriformes" "Anseriformes" "Anseriformes" "Anseriformes" ...
##  $ family                     : chr [1:551] "Anatidae" "Anatidae" "Anatidae" "Anatidae" ...
##  $ common_name                : chr [1:551] "American Black Duck" "American Wigeon" "Barrow's Goldeneye" "Black Brant" ...
##  $ scientific_name            : chr [1:551] "Anas rubripes" "Anas americana" "Bucephala islandica" "Branta bernicla" ...
##  $ diet                       : chr [1:551] "Vegetation" "Vegetation" "Invertebrates" "Vegetation" ...
##  $ life_expectancy            : chr [1:551] "Long" "Middle" "Middle" "Long" ...
##  $ habitat                    : chr [1:551] "Wetland" "Wetland" "Wetland" "Wetland" ...
##  $ urban_affiliate            : chr [1:551] "No" "No" "No" "No" ...
##  $ migratory_strategy         : chr [1:551] "Short" "Short" "Moderate" "Moderate" ...
##  $ log10_mass                 : num [1:551] 3.09 2.88 2.96 3.11 3.02 2.88 2.56 2.6 3.45 3.08 ...
##  $ mean_eggs_per_clutch       : num [1:551] 9 7.5 10.5 3.5 9.5 13.5 10 8.5 5 8 ...
##  $ mean_age_at_sexual_maturity: num [1:551] 1 1 3 2.5 2 1 0.6 2 1 1 ...
##  $ population_size            : num [1:551] NA NA NA NA NA NA NA NA NA NA ...
##  $ winter_range_area          : num [1:551] 3212473 7145842 1812841 360134 854350 ...
##  $ range_in_cbc               : num [1:551] 99.1 61.7 69.8 53.7 5.3 0.5 17.9 72.4 93.8 73.4 ...
##  $ strata                     : num [1:551] 82 124 37 19 36 5 26 134 145 103 ...
##  $ circles                    : num [1:551] 1453 1951 502 247 470 ...
##  $ feeder_bird                : chr [1:551] "No" "No" "No" "No" ...
##  $ median_trend               : num [1:551] 1.014 0.996 1.039 0.998 1.004 ...
##  $ lower_95_percent_ci        : num [1:551] 0.971 0.964 1.016 0.956 0.975 ...
##  $ upper_95_percent_ci        : num [1:551] 1.05 1.01 1.1 1.04 1.04 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Order = col_character(),
##   ..   Family = col_character(),
##   ..   `Common Name` = col_character(),
##   ..   `Scientific Name` = col_character(),
##   ..   Diet = col_character(),
##   ..   `Life Expectancy` = col_character(),
##   ..   Habitat = col_character(),
##   ..   `Urban Affiliate` = col_character(),
##   ..   `Migratory Strategy` = col_character(),
##   ..   `log10(mass)` = col_double(),
##   ..   `Mean Eggs per Clutch` = col_double(),
##   ..   `Mean Age at Sexual Maturity` = col_double(),
##   ..   `Population Size` = col_double(),
##   ..   `Winter Range Area` = col_double(),
##   ..   `Range in CBC` = col_double(),
##   ..   Strata = col_double(),
##   ..   Circles = col_double(),
##   ..   `Feeder Bird` = col_character(),
##   ..   `Median Trend` = col_double(),
##   ..   `Lower 95% CI` = col_double(),
##   ..   `Upper 95% CI` = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?

```r
ecosphere %>% 
  summarize(disctince_orders=n_distinct(order))
```

```
## # A tibble: 1 × 1
##   disctince_orders
##              <int>
## 1               19
```

Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?
Woodlands have the highest diverisy, containing 177 distinct species.

```r
ecosphere %>% 
  group_by(habitat) %>% 
  summarize(diversity=sum(n_distinct(scientific_name))) %>% 
  arrange(desc(diversity))
```

```
## # A tibble: 7 × 2
##   habitat   diversity
##   <chr>         <int>
## 1 Woodland        177
## 2 Wetland         153
## 3 Shrubland        82
## 4 Various          45
## 5 Ocean            44
## 6 Grassland        36
## 7 <NA>             14
```

Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?

```r
ecosphere %>% 
  select(common_name, scientific_name, winter_range_area) %>% 
  slice_max(winter_range_area, n=1)
```

```
## # A tibble: 1 × 3
##   common_name      scientific_name  winter_range_area
##   <chr>            <chr>                        <dbl>
## 1 Sooty Shearwater Puffinus griseus         185968946
```


```r
ecosphere %>% 
  select(common_name, scientific_name, winter_range_area) %>% 
  slice_min(winter_range_area, n=1)
```

```
## # A tibble: 1 × 3
##   common_name scientific_name winter_range_area
##   <chr>       <chr>                       <dbl>
## 1 Skylark     Alauda arvensis                11
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
ducks <- ecosphere %>% 
  filter(family=="Anatidae")
ducks
```

```
## # A tibble: 44 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Anserif… Anati… "Ameri… Anas r… Vege… Long    Wetland No      Short      3.09
##  2 Anserif… Anati… "Ameri… Anas a… Vege… Middle  Wetland No      Short      2.88
##  3 Anserif… Anati… "Barro… Buceph… Inve… Middle  Wetland No      Modera…    2.96
##  4 Anserif… Anati… "Black… Branta… Vege… Long    Wetland No      Modera…    3.11
##  5 Anserif… Anati… "Black… Melani… Inve… Middle  Wetland No      Modera…    3.02
##  6 Anserif… Anati… "Black… Dendro… Vege… Short   Wetland No      Withdr…    2.88
##  7 Anserif… Anati… "Blue-… Anas d… Vege… Middle  Wetland No      Modera…    2.56
##  8 Anserif… Anati… "Buffl… Buceph… Inve… Middle  Wetland No      Short      2.6 
##  9 Anserif… Anati… "Cackl… Branta… Vege… Middle  Wetland Yes     Short      3.45
## 10 Anserif… Anati… "Canva… Aythya… Vege… Middle  Wetland No      Short      3.08
## # … with 34 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```
Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.

```r
ducks %>% 
  group_by(habitat) %>% 
  summarize(habitats=sum(n_distinct(habitat)))
```

```
## # A tibble: 2 × 2
##   habitat habitats
##   <chr>      <int>
## 1 Ocean          1
## 2 Wetland        1
```

```r
ducks %>% 
  filter(habitat != "Wetland")
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Anserifo… Anati… Common… Somate… Inve… Middle  Ocean   No      Short      3.31
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?


Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.


Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.


Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?


Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.


Please provide the names of the students you have worked with with during the exam:


Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
