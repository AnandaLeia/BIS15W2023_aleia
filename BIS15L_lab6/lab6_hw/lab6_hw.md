---
title: "Lab 6 Homework"
author: "Ananda Leia"
date: "1/30/2023"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "lab6_hw_data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
skim(fisheries)
```


Table: Data summary

|                         |          |
|:------------------------|:---------|
|Name                     |fisheries |
|Number of rows           |17692     |
|Number of columns        |71        |
|_______________________  |          |
|Column type frequency:   |          |
|character                |69        |
|numeric                  |2         |
|________________________ |          |
|Group variables          |None      |


**Variable type: character**

|skim_variable           | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-----------------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|Country                 |         0|          1.00|   4|  25|     0|      204|          0|
|Common name             |         0|          1.00|   3|  30|     0|     1553|          0|
|ISSCAAP taxonomic group |         0|          1.00|   5|  36|     0|       30|          0|
|ASFIS species#          |         0|          1.00|  10|  13|     0|     1553|          0|
|ASFIS species name      |         0|          1.00|   6|  32|     0|     1548|          0|
|Measure                 |         0|          1.00|  17|  17|     0|        1|          0|
|1950                    |     15561|          0.12|   1|   6|     0|      513|          0|
|1951                    |     15550|          0.12|   1|   7|     0|      536|          0|
|1952                    |     15501|          0.12|   1|   7|     0|      553|          0|
|1953                    |     15439|          0.13|   1|   6|     0|      570|          0|
|1954                    |     15417|          0.13|   1|   7|     0|      588|          0|
|1955                    |     15382|          0.13|   1|   7|     0|      589|          0|
|1956                    |     15331|          0.13|   1|   7|     0|      633|          0|
|1957                    |     15253|          0.14|   1|   7|     0|      627|          0|
|1958                    |     15138|          0.14|   1|   6|     0|      643|          0|
|1959                    |     15110|          0.15|   1|   7|     0|      641|          0|
|1960                    |     15016|          0.15|   1|   7|     0|      673|          0|
|1961                    |     14922|          0.16|   1|   8|     0|      713|          0|
|1962                    |     14801|          0.16|   1|   8|     0|      729|          0|
|1963                    |     14707|          0.17|   1|   8|     0|      760|          0|
|1964                    |     14349|          0.19|   1|   8|     0|      759|          0|
|1965                    |     14241|          0.20|   1|   8|     0|      798|          0|
|1966                    |     14187|          0.20|   1|   8|     0|      801|          0|
|1967                    |     14047|          0.21|   1|   8|     0|      815|          0|
|1968                    |     13963|          0.21|   1|   8|     0|      829|          0|
|1969                    |     13920|          0.21|   1|   8|     0|      853|          0|
|1970                    |     13113|          0.26|   1|   8|     0|     1225|          0|
|1971                    |     12925|          0.27|   1|   8|     0|     1326|          0|
|1972                    |     12749|          0.28|   1|   8|     0|     1372|          0|
|1973                    |     12673|          0.28|   1|   8|     0|     1432|          0|
|1974                    |     12583|          0.29|   1|   8|     0|     2601|          0|
|1975                    |     12333|          0.30|   1|   8|     0|     2767|          0|
|1976                    |     12177|          0.31|   1|   8|     0|     2804|          0|
|1977                    |     12014|          0.32|   1|   8|     0|     2867|          0|
|1978                    |     11847|          0.33|   1|   8|     0|     2901|          0|
|1979                    |     11820|          0.33|   1|   8|     0|     2932|          0|
|1980                    |     11747|          0.34|   1|   8|     0|     2956|          0|
|1981                    |     11713|          0.34|   1|   8|     0|     2996|          0|
|1982                    |     11558|          0.35|   1|   9|     0|     3030|          0|
|1983                    |     11453|          0.35|   1|   8|     0|     3031|          0|
|1984                    |     11309|          0.36|   1|   8|     0|     3076|          0|
|1985                    |     11212|          0.37|   1|   8|     0|     3161|          0|
|1986                    |     11086|          0.37|   1|   8|     0|     3242|          0|
|1987                    |     10930|          0.38|   1|   8|     0|     3255|          0|
|1988                    |     10493|          0.41|   1|   8|     0|     3435|          0|
|1989                    |     10435|          0.41|   1|   8|     0|     3425|          0|
|1990                    |     10293|          0.42|   1|   8|     0|     3446|          0|
|1991                    |     10364|          0.41|   1|   8|     0|     3420|          0|
|1992                    |     10435|          0.41|   1|   8|     0|     3322|          0|
|1993                    |     10522|          0.41|   1|   8|     0|     3313|          0|
|1994                    |     10400|          0.41|   1|   8|     0|     3313|          0|
|1995                    |     10148|          0.43|   1|   8|     0|     3329|          0|
|1996                    |      9990|          0.44|   1|   7|     0|     3358|          0|
|1997                    |      9773|          0.45|   1|   9|     0|     3393|          0|
|1998                    |      9579|          0.46|   1|   9|     0|     3399|          0|
|1999                    |      9265|          0.48|   1|   9|     0|     3428|          0|
|2000                    |      8899|          0.50|   1|   9|     0|     3481|          0|
|2001                    |      8646|          0.51|   1|   9|     0|     3490|          0|
|2002                    |      8590|          0.51|   1|   9|     0|     3507|          0|
|2003                    |      8383|          0.53|   1|   9|     0|     3482|          0|
|2004                    |      7977|          0.55|   1|   9|     0|     3505|          0|
|2005                    |      7822|          0.56|   1|   9|     0|     3532|          0|
|2006                    |      7699|          0.56|   1|   9|     0|     3565|          0|
|2007                    |      7589|          0.57|   1|   8|     0|     3551|          0|
|2008                    |      7667|          0.57|   1|   8|     0|     3537|          0|
|2009                    |      7573|          0.57|   1|   8|     0|     3572|          0|
|2010                    |      7499|          0.58|   1|   8|     0|     3590|          0|
|2011                    |      7371|          0.58|   1|   8|     0|     3618|          0|
|2012                    |      7336|          0.59|   1|   8|     0|     3609|          0|


**Variable type: numeric**

|skim_variable          | n_missing| complete_rate|  mean|    sd| p0| p25| p50| p75| p100|hist  |
|:----------------------|---------:|-------------:|-----:|-----:|--:|---:|---:|---:|----:|:-----|
|ISSCAAP group#         |         0|             1| 37.38|  7.88| 11|  33|  36|  38|   77|▁▇▂▁▁ |
|FAO major fishing area |         0|             1| 45.34| 18.33| 18|  31|  37|  57|   88|▇▇▆▃▃ |

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
names(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
anyNA(fisheries)
```

```
## [1] TRUE
```

```r
str(fisheries)
```

```
## spc_tbl_ [17,692 × 71] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ Country                : chr [1:17692] "Albania" "Albania" "Albania" "Albania" ...
##  $ Common name            : chr [1:17692] "Angelsharks, sand devils nei" "Atlantic bonito" "Barracudas nei" "Blue and red shrimp" ...
##  $ ISSCAAP group#         : num [1:17692] 38 36 37 45 32 37 33 45 38 57 ...
##  $ ISSCAAP taxonomic group: chr [1:17692] "Sharks, rays, chimaeras" "Tunas, bonitos, billfishes" "Miscellaneous pelagic fishes" "Shrimps, prawns" ...
##  $ ASFIS species#         : chr [1:17692] "10903XXXXX" "1750100101" "17710001XX" "2280203101" ...
##  $ ASFIS species name     : chr [1:17692] "Squatinidae" "Sarda sarda" "Sphyraena spp" "Aristeus antennatus" ...
##  $ FAO major fishing area : num [1:17692] 37 37 37 37 37 37 37 37 37 37 ...
##  $ Measure                : chr [1:17692] "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" ...
##  $ 1950                   : chr [1:17692] NA NA NA NA ...
##  $ 1951                   : chr [1:17692] NA NA NA NA ...
##  $ 1952                   : chr [1:17692] NA NA NA NA ...
##  $ 1953                   : chr [1:17692] NA NA NA NA ...
##  $ 1954                   : chr [1:17692] NA NA NA NA ...
##  $ 1955                   : chr [1:17692] NA NA NA NA ...
##  $ 1956                   : chr [1:17692] NA NA NA NA ...
##  $ 1957                   : chr [1:17692] NA NA NA NA ...
##  $ 1958                   : chr [1:17692] NA NA NA NA ...
##  $ 1959                   : chr [1:17692] NA NA NA NA ...
##  $ 1960                   : chr [1:17692] NA NA NA NA ...
##  $ 1961                   : chr [1:17692] NA NA NA NA ...
##  $ 1962                   : chr [1:17692] NA NA NA NA ...
##  $ 1963                   : chr [1:17692] NA NA NA NA ...
##  $ 1964                   : chr [1:17692] NA NA NA NA ...
##  $ 1965                   : chr [1:17692] NA NA NA NA ...
##  $ 1966                   : chr [1:17692] NA NA NA NA ...
##  $ 1967                   : chr [1:17692] NA NA NA NA ...
##  $ 1968                   : chr [1:17692] NA NA NA NA ...
##  $ 1969                   : chr [1:17692] NA NA NA NA ...
##  $ 1970                   : chr [1:17692] NA NA NA NA ...
##  $ 1971                   : chr [1:17692] NA NA NA NA ...
##  $ 1972                   : chr [1:17692] NA NA NA NA ...
##  $ 1973                   : chr [1:17692] NA NA NA NA ...
##  $ 1974                   : chr [1:17692] NA NA NA NA ...
##  $ 1975                   : chr [1:17692] NA NA NA NA ...
##  $ 1976                   : chr [1:17692] NA NA NA NA ...
##  $ 1977                   : chr [1:17692] NA NA NA NA ...
##  $ 1978                   : chr [1:17692] NA NA NA NA ...
##  $ 1979                   : chr [1:17692] NA NA NA NA ...
##  $ 1980                   : chr [1:17692] NA NA NA NA ...
##  $ 1981                   : chr [1:17692] NA NA NA NA ...
##  $ 1982                   : chr [1:17692] NA NA NA NA ...
##  $ 1983                   : chr [1:17692] NA NA NA NA ...
##  $ 1984                   : chr [1:17692] NA NA NA NA ...
##  $ 1985                   : chr [1:17692] NA NA NA NA ...
##  $ 1986                   : chr [1:17692] NA NA NA NA ...
##  $ 1987                   : chr [1:17692] NA NA NA NA ...
##  $ 1988                   : chr [1:17692] NA NA NA NA ...
##  $ 1989                   : chr [1:17692] NA NA NA NA ...
##  $ 1990                   : chr [1:17692] NA NA NA NA ...
##  $ 1991                   : chr [1:17692] NA NA NA NA ...
##  $ 1992                   : chr [1:17692] NA NA NA NA ...
##  $ 1993                   : chr [1:17692] NA NA NA NA ...
##  $ 1994                   : chr [1:17692] NA NA NA NA ...
##  $ 1995                   : chr [1:17692] "0 0" "1" NA "0 0" ...
##  $ 1996                   : chr [1:17692] "53" "2" NA "3" ...
##  $ 1997                   : chr [1:17692] "20" "0 0" NA "0 0" ...
##  $ 1998                   : chr [1:17692] "31" "12" NA NA ...
##  $ 1999                   : chr [1:17692] "30" "30" NA NA ...
##  $ 2000                   : chr [1:17692] "30" "25" "2" NA ...
##  $ 2001                   : chr [1:17692] "16" "30" NA NA ...
##  $ 2002                   : chr [1:17692] "79" "24" NA "34" ...
##  $ 2003                   : chr [1:17692] "1" "4" NA "22" ...
##  $ 2004                   : chr [1:17692] "4" "2" "2" "15" ...
##  $ 2005                   : chr [1:17692] "68" "23" "4" "12" ...
##  $ 2006                   : chr [1:17692] "55" "30" "7" "18" ...
##  $ 2007                   : chr [1:17692] "12" "19" NA NA ...
##  $ 2008                   : chr [1:17692] "23" "27" NA NA ...
##  $ 2009                   : chr [1:17692] "14" "21" NA NA ...
##  $ 2010                   : chr [1:17692] "78" "23" "7" NA ...
##  $ 2011                   : chr [1:17692] "12" "12" NA NA ...
##  $ 2012                   : chr [1:17692] "5" "5" NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Country = col_character(),
##   ..   `Common name` = col_character(),
##   ..   `ISSCAAP group#` = col_double(),
##   ..   `ISSCAAP taxonomic group` = col_character(),
##   ..   `ASFIS species#` = col_character(),
##   ..   `ASFIS species name` = col_character(),
##   ..   `FAO major fishing area` = col_double(),
##   ..   Measure = col_character(),
##   ..   `1950` = col_character(),
##   ..   `1951` = col_character(),
##   ..   `1952` = col_character(),
##   ..   `1953` = col_character(),
##   ..   `1954` = col_character(),
##   ..   `1955` = col_character(),
##   ..   `1956` = col_character(),
##   ..   `1957` = col_character(),
##   ..   `1958` = col_character(),
##   ..   `1959` = col_character(),
##   ..   `1960` = col_character(),
##   ..   `1961` = col_character(),
##   ..   `1962` = col_character(),
##   ..   `1963` = col_character(),
##   ..   `1964` = col_character(),
##   ..   `1965` = col_character(),
##   ..   `1966` = col_character(),
##   ..   `1967` = col_character(),
##   ..   `1968` = col_character(),
##   ..   `1969` = col_character(),
##   ..   `1970` = col_character(),
##   ..   `1971` = col_character(),
##   ..   `1972` = col_character(),
##   ..   `1973` = col_character(),
##   ..   `1974` = col_character(),
##   ..   `1975` = col_character(),
##   ..   `1976` = col_character(),
##   ..   `1977` = col_character(),
##   ..   `1978` = col_character(),
##   ..   `1979` = col_character(),
##   ..   `1980` = col_character(),
##   ..   `1981` = col_character(),
##   ..   `1982` = col_character(),
##   ..   `1983` = col_character(),
##   ..   `1984` = col_character(),
##   ..   `1985` = col_character(),
##   ..   `1986` = col_character(),
##   ..   `1987` = col_character(),
##   ..   `1988` = col_character(),
##   ..   `1989` = col_character(),
##   ..   `1990` = col_character(),
##   ..   `1991` = col_character(),
##   ..   `1992` = col_character(),
##   ..   `1993` = col_character(),
##   ..   `1994` = col_character(),
##   ..   `1995` = col_character(),
##   ..   `1996` = col_character(),
##   ..   `1997` = col_character(),
##   ..   `1998` = col_character(),
##   ..   `1999` = col_character(),
##   ..   `2000` = col_character(),
##   ..   `2001` = col_character(),
##   ..   `2002` = col_character(),
##   ..   `2003` = col_character(),
##   ..   `2004` = col_character(),
##   ..   `2005` = col_character(),
##   ..   `2006` = col_character(),
##   ..   `2007` = col_character(),
##   ..   `2008` = col_character(),
##   ..   `2009` = col_character(),
##   ..   `2010` = col_character(),
##   ..   `2011` = col_character(),
##   ..   `2012` = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 


```r
fisheries <- janitor::clean_names(fisheries)
names(fisheries)
```

```
##  [1] "country"                 "common_name"            
##  [3] "isscaap_group_number"    "isscaap_taxonomic_group"
##  [5] "asfis_species_number"    "asfis_species_name"     
##  [7] "fao_major_fishing_area"  "measure"                
##  [9] "x1950"                   "x1951"                  
## [11] "x1952"                   "x1953"                  
## [13] "x1954"                   "x1955"                  
## [15] "x1956"                   "x1957"                  
## [17] "x1958"                   "x1959"                  
## [19] "x1960"                   "x1961"                  
## [21] "x1962"                   "x1963"                  
## [23] "x1964"                   "x1965"                  
## [25] "x1966"                   "x1967"                  
## [27] "x1968"                   "x1969"                  
## [29] "x1970"                   "x1971"                  
## [31] "x1972"                   "x1973"                  
## [33] "x1974"                   "x1975"                  
## [35] "x1976"                   "x1977"                  
## [37] "x1978"                   "x1979"                  
## [39] "x1980"                   "x1981"                  
## [41] "x1982"                   "x1983"                  
## [43] "x1984"                   "x1985"                  
## [45] "x1986"                   "x1987"                  
## [47] "x1988"                   "x1989"                  
## [49] "x1990"                   "x1991"                  
## [51] "x1992"                   "x1993"                  
## [53] "x1994"                   "x1995"                  
## [55] "x1996"                   "x1997"                  
## [57] "x1998"                   "x1999"                  
## [59] "x2000"                   "x2001"                  
## [61] "x2002"                   "x2003"                  
## [63] "x2004"                   "x2005"                  
## [65] "x2006"                   "x2007"                  
## [67] "x2008"                   "x2009"                  
## [69] "x2010"                   "x2011"                  
## [71] "x2012"
```


```r
fisheries <- fisheries %>% 
  mutate(across(c(country, isscaap_group_number, asfis_species_number,fao_major_fishing_area), as_factor))
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries %>% 
  summarize(countries=n_distinct(country))
```

```
## # A tibble: 1 × 1
##   countries
##       <int>
## 1       204
```

```r
fisheries %>% 
  tabyl(country) %>% 
  adorn_pct_formatting(digits = 2) %>% 
  arrange(desc(n))
```

```
##                    country   n percent
##                      Spain 915   5.17%
##                   Portugal 763   4.31%
##   United States of America 627   3.54%
##         Korea, Republic of 620   3.50%
##                      Japan 611   3.45%
##         Russian Federation 523   2.96%
##         Un. Sov. Soc. Rep. 515   2.91%
##                     France 489   2.76%
##             United Kingdom 362   2.05%
##   Taiwan Province of China 310   1.75%
##                    Germany 306   1.73%
##                  Australia 301   1.70%
##                    Ukraine 294   1.66%
##                     Poland 263   1.49%
##                      Italy 261   1.48%
##                      China 236   1.33%
##                  Indonesia 223   1.26%
##                  Lithuania 215   1.22%
##                New Zealand 208   1.18%
##               South Africa 200   1.13%
##                     Mexico 198   1.12%
##                   Bulgaria 197   1.11%
##                    Ireland 191   1.08%
##                    Romania 191   1.08%
##                     Norway 188   1.06%
##                    Estonia 184   1.04%
##                   Malaysia 166   0.94%
##                       Cuba 162   0.92%
##                     Latvia 162   0.92%
##                Netherlands 155   0.88%
##                    Morocco 153   0.86%
##                   Thailand 150   0.85%
##                      Chile 141   0.80%
##                  Argentina 140   0.79%
##                    Senegal 140   0.79%
##                Philippines 138   0.78%
##                     Brazil 136   0.77%
##                     Belize 133   0.75%
##                    Uruguay 131   0.74%
##               Saudi Arabia 128   0.72%
##                     Canada 125   0.71%
##                     Greece 125   0.71%
##                     Panama 121   0.68%
##                      India 108   0.61%
##                    Iceland 107   0.60%
##                      Malta 104   0.59%
##                    Croatia 103   0.58%
##                    Denmark 103   0.58%
##                    Ecuador 100   0.57%
##                  Other nei 100   0.57%
##                     Cyprus  96   0.54%
##              Faroe Islands  96   0.54%
##                      Ghana  94   0.53%
##                 Mauritania  93   0.53%
##                     Angola  88   0.50%
##                      Egypt  87   0.49%
##                    Georgia  86   0.49%
##                    Tunisia  85   0.48%
##                   Colombia  81   0.46%
##    Venezuela, Boliv Rep of  80   0.45%
##                     Israel  79   0.45%
##                       Togo  78   0.44%
##                    Liberia  76   0.43%
##                    Namibia  76   0.43%
##                     Turkey  76   0.43%
##                     Sweden  72   0.41%
##   Saint Vincent/Grenadines  71   0.40%
##                    Vanuatu  71   0.40%
##                 Seychelles  70   0.40%
##                      Benin  68   0.38%
##                   Honduras  68   0.38%
##                    Albania  67   0.38%
##           C\xf4te d'Ivoire  67   0.38%
##            Channel Islands  65   0.37%
##     Iran (Islamic Rep. of)  64   0.36%
##                    Bahrain  62   0.35%
##                  Greenland  60   0.34%
##                   Pakistan  60   0.34%
##                    Algeria  59   0.33%
##                  Nicaragua  59   0.33%
##               Sierra Leone  59   0.33%
##                    Belgium  57   0.32%
##                     Guinea  56   0.32%
##                      Libya  56   0.32%
##               Cook Islands  55   0.31%
##                       Peru  54   0.31%
##         Congo, Republic of  53   0.30%
##                       Oman  53   0.30%
##       United Arab Emirates  52   0.29%
##         Dominican Republic  50   0.28%
##          Fiji, Republic of  50   0.28%
##                    Nigeria  50   0.28%
##                   Slovenia  50   0.28%
##                    Eritrea  49   0.28%
##                     Gambia  49   0.28%
##                Puerto Rico  49   0.28%
##   Tanzania, United Rep. of  49   0.28%
##                    Bermuda  47   0.27%
##                    Grenada  47   0.27%
##                 Costa Rica  45   0.25%
##                      Gabon  45   0.25%
##      Serbia and Montenegro  45   0.25%
##                    Comoros  43   0.24%
##                Isle of Man  41   0.23%
##                  Singapore  40   0.23%
##    St. Pierre and Miquelon  40   0.23%
##        Trinidad and Tobago  39   0.22%
##                      Yemen  39   0.22%
##                  Guatemala  38   0.21%
##                 R\xe9union  37   0.21%
##                   Cameroon  36   0.20%
##             Yugoslavia SFR  36   0.20%
##                 Madagascar  35   0.20%
##                      Qatar  35   0.20%
##      Sao Tome and Principe  35   0.20%
##                  Sri Lanka  34   0.19%
##       Syrian Arab Republic  34   0.19%
##     Falkland Is.(Malvinas)  33   0.19%
##                      Palau  33   0.19%
##             American Samoa  32   0.18%
##       China, Hong Kong SAR  32   0.18%
##               GuineaBissau  32   0.18%
##           French Polynesia  31   0.18%
##                      Kenya  31   0.18%
##                  Mauritius  30   0.17%
##                 Mozambique  30   0.17%
##          US Virgin Islands  29   0.16%
##      Saint Kitts and Nevis  28   0.16%
##                   Kiribati  27   0.15%
##                Saint Lucia  27   0.15%
##                   Suriname  27   0.15%
##                 Cabo Verde  26   0.15%
##              New Caledonia  26   0.15%
##                El Salvador  25   0.14%
##    Palestine, Occupied Tr.  25   0.14%
##                 Montenegro  24   0.14%
##                       Guam  23   0.13%
##                     Kuwait  23   0.13%
##        Antigua and Barbuda  22   0.12%
##                   Barbados  21   0.12%
##    Congo, Dem. Rep. of the  21   0.12%
##                    Lebanon  20   0.11%
##           Papua New Guinea  20   0.11%
##       Northern Mariana Is.  19   0.11%
##               Saint Helena  19   0.11%
##                   Zanzibar  19   0.11%
##     British Virgin Islands  18   0.10%
##              French Guiana  18   0.10%
##            Solomon Islands  18   0.10%
##       Netherlands Antilles  17   0.10%
##                    Finland  16   0.09%
##                       Iraq  16   0.09%
##                 Martinique  16   0.09%
##          Equatorial Guinea  15   0.08%
##                      Samoa  15   0.08%
##                    Bahamas  14   0.08%
##                   Djibouti  14   0.08%
##   Korea, Dem. People's Rep  14   0.08%
##                    Mayotte  14   0.08%
##                      Tonga  14   0.08%
##                   Viet Nam  14   0.08%
##                   Dominica  13   0.07%
##           Marshall Islands  13   0.07%
##  Micronesia, Fed.States of  13   0.07%
##                     Jordan  12   0.07%
##                   Maldives  12   0.07%
##                     Guyana  11   0.06%
##                       Niue  11   0.06%
##                    Tokelau  10   0.06%
##                     Tuvalu  10   0.06%
##                 Cura\xe7ao   9   0.05%
##                      Nauru   9   0.05%
##                 Bangladesh   8   0.05%
##          Brunei Darussalam   8   0.05%
##                   Cambodia   8   0.05%
##                 Guadeloupe   8   0.05%
##   British Indian Ocean Ter   7   0.04%
##                 TimorLeste   7   0.04%
##                      Haiti   6   0.03%
##                    Jamaica   6   0.03%
##       Turks and Caicos Is.   6   0.03%
##                      Aruba   5   0.03%
##                   Ethiopia   5   0.03%
##                    Myanmar   5   0.03%
##      Wallis and Futuna Is.   5   0.03%
##             Cayman Islands   4   0.02%
##           China, Macao SAR   4   0.02%
##                   Anguilla   3   0.02%
##       French Southern Terr   3   0.02%
##                    Somalia   3   0.02%
##                      Sudan   3   0.02%
##             Sudan (former)   3   0.02%
##             Western Sahara   3   0.02%
##   Bonaire/S.Eustatius/Saba   2   0.01%
##               Sint Maarten   2   0.01%
##     Bosnia and Herzegovina   1   0.01%
##                  Gibraltar   1   0.01%
##                     Monaco   1   0.01%
##                 Montserrat   1   0.01%
##             Norfolk Island   1   0.01%
##           Pitcairn Islands   1   0.01%
##        Saint Barth\xe9lemy   1   0.01%
##                SaintMartin   1   0.01%
##     Svalbard and Jan Mayen   1   0.01%
```

```r
str(fisheries$country)
```

```
##  Factor w/ 204 levels "Albania","Algeria",..: 1 1 1 1 1 1 1 1 1 1 ...
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_specie…¹  year catch
##    <fct>   <chr>                   <chr>              <fct>          <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2004     4
## # … with 376,761 more rows, and abbreviated variable name ¹​asfis_species_number
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries %>% 
  summarize(distinct_species=n_distinct(asfis_species_number))
```

```
## # A tibble: 1 × 1
##   distinct_species
##              <int>
## 1             1553
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  filter(year==2000) %>% 
  group_by(country) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 193 × 2
##    country                  catch_total
##    <fct>                          <dbl>
##  1 China                          25899
##  2 Russian Federation             12181
##  3 United States of America       11762
##  4 Japan                           8510
##  5 Indonesia                       8341
##  6 Peru                            7443
##  7 Chile                           6906
##  8 India                           6351
##  9 Thailand                        6243
## 10 Korea, Republic of              6124
## # … with 183 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  filter(between(year, 1990, 2000)) %>% 
  filter(asfis_species_name=="Sardina pilchardus") %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>%
  arrange(desc(catch_total))
```

```
## # A tibble: 37 × 2
##    country               catch_total
##    <fct>                       <dbl>
##  1 Morocco                      7470
##  2 Spain                        3507
##  3 Russian Federation           1639
##  4 Ukraine                      1030
##  5 France                        966
##  6 Portugal                      818
##  7 Greece                        528
##  8 Italy                         507
##  9 Serbia and Montenegro         478
## 10 Denmark                       477
## # … with 27 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  filter(between(year, 2008, 2012)) %>% 
  filter(asfis_species_name=="Cephalopoda") %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>%
  arrange(desc(catch_total))
```

```
## # A tibble: 16 × 2
##    country                  catch_total
##    <fct>                          <dbl>
##  1 India                            570
##  2 China                            257
##  3 Spain                            198
##  4 Algeria                          162
##  5 France                           101
##  6 Mauritania                        90
##  7 TimorLeste                        76
##  8 Italy                             66
##  9 Mozambique                        16
## 10 Cambodia                          15
## 11 Taiwan Province of China          13
## 12 Madagascar                        11
## 13 Croatia                            7
## 14 Israel                             0
## 15 Somalia                            0
## 16 Viet Nam                           0
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)



```r
fisheries_tidy %>% 
  filter(asfis_species_name !="Osteichthyes") %>% 
  group_by (asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>%  
  arrange(desc(catch_total))
```

```
## # A tibble: 1,545 × 2
##    asfis_species_name      catch_total
##    <chr>                         <dbl>
##  1 Engraulis ringens            540739
##  2 Theragra chalcogramma        473722
##  3 Clupea harengus              264304
##  4 Gadus morhua                 217930
##  5 Katsuwonus pelamis           194923
##  6 Sardinops sagax              176094
##  7 Scomber japonicus            175444
##  8 Trachurus murphyi            152034
##  9 Sardinops melanostictus      144774
## 10 Mallotus villosus            131239
## # … with 1,535 more rows
```

10. Use the data to do at least one analysis of your choice.

```r
fisheries_tidy %>% 
  select(common_name, country, year, catch, asfis_species_name) %>% 
  filter(year==2012) %>% 
  slice_max(catch, n=5)
```

```
## # A tibble: 5 × 5
##   common_name                    country                   year catch asfis_sp…¹
##   <chr>                          <fct>                    <dbl> <dbl> <chr>     
## 1 Marine fishes nei              Myanmar                   2012  9613 Osteichth…
## 2 Alaska pollock(=Walleye poll.) Russian Federation        2012  8188 Theragra …
## 3 Anchoveta(=Peruvian anchovy)   Peru                      2012  6880 Engraulis…
## 4 Largehead hairtail             China                     2012  6694 Trichiuru…
## 5 Alaska pollock(=Walleye poll.) United States of America  2012  2815 Theragra …
## # … with abbreviated variable name ¹​asfis_species_name
```


```r
fisheries_tidy %>% 
  select(common_name, country, year, catch, asfis_species_name) %>% 
  filter(year==1950) %>% 
  slice_max(catch, n=5)
```

```
## # A tibble: 6 × 5
##   common_name            country                   year catch asfis_species_name
##   <chr>                  <fct>                    <dbl> <dbl> <chr>             
## 1 American cupped oyster United States of America  1950   935 Crassostrea virgi…
## 2 Atlantic menhaden      United States of America  1950   913 Brevoortia tyrann…
## 3 Atlantic cod           Iceland                   1950   900 Gadus morhua      
## 4 Chub mackerel          Japan                     1950   900 Scomber japonicus 
## 5 Atlantic cod           Norway                    1950   900 Gadus morhua      
## 6 Percoids nei           Philippines               1950   900 Percoidei
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
