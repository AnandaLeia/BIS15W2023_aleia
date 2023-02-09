---
title: "Lab 7 Homework"
author: "Ananda Leia"
date: "2/7/2023"
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

## Data
**1. For this homework, we will use two different data sets. Please load `amniota` and `amphibio`.**  

`amniota` data:  
Myhrvold N, Baldridge E, Chan B, Sivam D, Freeman DL, Ernest SKM (2015). “An amniote life-history
database to perform comparative analyses with birds, mammals, and reptiles.” _Ecology_, *96*, 3109.
doi: 10.1890/15-0846.1 (URL: https://doi.org/10.1890/15-0846.1).

```r
amniota <- read_csv("lab7_hw_data/amniota.csv")
```

```
## Rows: 21322 Columns: 36
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (6): class, order, family, genus, species, common_name
## dbl (30): subspecies, female_maturity_d, litter_or_clutch_size_n, litters_or...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
amniota
```

```
## # A tibble: 21,322 × 36
##    class order      family genus species subsp…¹ commo…² femal…³ litte…⁴ litte…⁵
##    <chr> <chr>      <chr>  <chr> <chr>     <dbl> <chr>     <dbl>   <dbl>   <dbl>
##  1 Aves  Accipitri… Accip… Acci… albogu…    -999 Pied G…   -999  -999       -999
##  2 Aves  Accipitri… Accip… Acci… badius     -999 Shikra     363.    3.25       1
##  3 Aves  Accipitri… Accip… Acci… bicolor    -999 Bicolo…   -999     2.7     -999
##  4 Aves  Accipitri… Accip… Acci… brachy…    -999 New Br…   -999  -999       -999
##  5 Aves  Accipitri… Accip… Acci… brevip…    -999 Levant…    363.    4          1
##  6 Aves  Accipitri… Accip… Acci… castan…    -999 Chestn…   -999  -999       -999
##  7 Aves  Accipitri… Accip… Acci… chilen…    -999 Chilea…   -999     2.7     -999
##  8 Aves  Accipitri… Accip… Acci… chiono…    -999 White-…    548.    4.25       1
##  9 Aves  Accipitri… Accip… Acci… cirroc…    -999 Collar…   -999     3.25    -999
## 10 Aves  Accipitri… Accip… Acci… cooper…    -999 Cooper…    730     4.35       1
## # … with 21,312 more rows, 26 more variables: adult_body_mass_g <dbl>,
## #   maximum_longevity_y <dbl>, gestation_d <dbl>, weaning_d <dbl>,
## #   birth_or_hatching_weight_g <dbl>, weaning_weight_g <dbl>, egg_mass_g <dbl>,
## #   incubation_d <dbl>, fledging_age_d <dbl>, longevity_y <dbl>,
## #   male_maturity_d <dbl>, inter_litter_or_interbirth_interval_y <dbl>,
## #   female_body_mass_g <dbl>, male_body_mass_g <dbl>, no_sex_body_mass_g <dbl>,
## #   egg_width_mm <dbl>, egg_length_mm <dbl>, fledging_mass_g <dbl>, …
```

`amphibio` data:  
Oliveira BF, São-Pedro VA, Santos-Barrera G, Penone C, Costa GC (2017). “AmphiBIO, a global database
for amphibian ecological traits.” _Scientific Data_, *4*, 170123. doi: 10.1038/sdata.2017.123 (URL:
https://doi.org/10.1038/sdata.2017.123).

```r
amphibio <- read_csv("lab7_hw_data/amphibio.csv")
```

```
## Rows: 6776 Columns: 38
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (6): id, Order, Family, Genus, Species, OBS
## dbl (31): Fos, Ter, Aqu, Arb, Leaves, Flowers, Seeds, Arthro, Vert, Diu, Noc...
## lgl  (1): Fruits
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
amphibio
```

```
## # A tibble: 6,776 × 38
##    id    Order Family Genus Species   Fos   Ter   Aqu   Arb Leaves Flowers Seeds
##    <chr> <chr> <chr>  <chr> <chr>   <dbl> <dbl> <dbl> <dbl>  <dbl>   <dbl> <dbl>
##  1 Anf0… Anura Allop… Allo… Alloph…    NA     1     1     1     NA      NA    NA
##  2 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA    NA
##  3 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA    NA
##  4 Anf0… Anura Alyti… Alyt… Alytes…    NA     1     1     1     NA      NA    NA
##  5 Anf0… Anura Alyti… Alyt… Alytes…    NA     1    NA     1     NA      NA    NA
##  6 Anf0… Anura Alyti… Alyt… Alytes…     1     1     1     1     NA      NA    NA
##  7 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA    NA
##  8 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA    NA
##  9 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA    NA
## 10 Anf0… Anura Alyti… Disc… Discog…     1     1     1    NA     NA      NA    NA
## # … with 6,766 more rows, and 26 more variables: Fruits <lgl>, Arthro <dbl>,
## #   Vert <dbl>, Diu <dbl>, Noc <dbl>, Crepu <dbl>, Wet_warm <dbl>,
## #   Wet_cold <dbl>, Dry_warm <dbl>, Dry_cold <dbl>, Body_mass_g <dbl>,
## #   Age_at_maturity_min_y <dbl>, Age_at_maturity_max_y <dbl>,
## #   Body_size_mm <dbl>, Size_at_maturity_min_mm <dbl>,
## #   Size_at_maturity_max_mm <dbl>, Longevity_max_y <dbl>,
## #   Litter_size_min_n <dbl>, Litter_size_max_n <dbl>, …
```

## Questions  
**2. Do some exploratory analysis of the `amniota` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  

```r
str(amniota)
```

```
## spc_tbl_ [21,322 × 36] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ class                                : chr [1:21322] "Aves" "Aves" "Aves" "Aves" ...
##  $ order                                : chr [1:21322] "Accipitriformes" "Accipitriformes" "Accipitriformes" "Accipitriformes" ...
##  $ family                               : chr [1:21322] "Accipitridae" "Accipitridae" "Accipitridae" "Accipitridae" ...
##  $ genus                                : chr [1:21322] "Accipiter" "Accipiter" "Accipiter" "Accipiter" ...
##  $ species                              : chr [1:21322] "albogularis" "badius" "bicolor" "brachyurus" ...
##  $ subspecies                           : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ common_name                          : chr [1:21322] "Pied Goshawk" "Shikra" "Bicolored Hawk" "New Britain Sparrowhawk" ...
##  $ female_maturity_d                    : num [1:21322] -999 363 -999 -999 363 ...
##  $ litter_or_clutch_size_n              : num [1:21322] -999 3.25 2.7 -999 4 -999 2.7 4.25 3.25 4.35 ...
##  $ litters_or_clutches_per_y            : num [1:21322] -999 1 -999 -999 1 -999 -999 1 -999 1 ...
##  $ adult_body_mass_g                    : num [1:21322] 252 140 345 142 204 ...
##  $ maximum_longevity_y                  : num [1:21322] -999 -999 -999 -999 -999 ...
##  $ gestation_d                          : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ weaning_d                            : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ birth_or_hatching_weight_g           : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 28 ...
##  $ weaning_weight_g                     : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ egg_mass_g                           : num [1:21322] -999 21 32 -999 21.9 ...
##  $ incubation_d                         : num [1:21322] -999 30 -999 -999 32.5 ...
##  $ fledging_age_d                       : num [1:21322] -999 32 -999 -999 42.5 ...
##  $ longevity_y                          : num [1:21322] -999 -999 -999 -999 -999 ...
##  $ male_maturity_d                      : num [1:21322] -999 -999 -999 -999 -999 -999 -999 365 -999 730 ...
##  $ inter_litter_or_interbirth_interval_y: num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_body_mass_g                   : num [1:21322] 352 168 390 -999 230 ...
##  $ male_body_mass_g                     : num [1:21322] 223 125 212 142 170 ...
##  $ no_sex_body_mass_g                   : num [1:21322] -999 123 -999 -999 -999 ...
##  $ egg_width_mm                         : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ egg_length_mm                        : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ fledging_mass_g                      : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ adult_svl_cm                         : num [1:21322] -999 30 39.5 -999 33.5 -999 39.5 29 32.5 42 ...
##  $ male_svl_cm                          : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_svl_cm                        : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ birth_or_hatching_svl_cm             : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_svl_at_maturity_cm            : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ female_body_mass_at_maturity_g       : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ no_sex_svl_cm                        : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  $ no_sex_maturity_d                    : num [1:21322] -999 -999 -999 -999 -999 -999 -999 -999 -999 -999 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   class = col_character(),
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   genus = col_character(),
##   ..   species = col_character(),
##   ..   subspecies = col_double(),
##   ..   common_name = col_character(),
##   ..   female_maturity_d = col_double(),
##   ..   litter_or_clutch_size_n = col_double(),
##   ..   litters_or_clutches_per_y = col_double(),
##   ..   adult_body_mass_g = col_double(),
##   ..   maximum_longevity_y = col_double(),
##   ..   gestation_d = col_double(),
##   ..   weaning_d = col_double(),
##   ..   birth_or_hatching_weight_g = col_double(),
##   ..   weaning_weight_g = col_double(),
##   ..   egg_mass_g = col_double(),
##   ..   incubation_d = col_double(),
##   ..   fledging_age_d = col_double(),
##   ..   longevity_y = col_double(),
##   ..   male_maturity_d = col_double(),
##   ..   inter_litter_or_interbirth_interval_y = col_double(),
##   ..   female_body_mass_g = col_double(),
##   ..   male_body_mass_g = col_double(),
##   ..   no_sex_body_mass_g = col_double(),
##   ..   egg_width_mm = col_double(),
##   ..   egg_length_mm = col_double(),
##   ..   fledging_mass_g = col_double(),
##   ..   adult_svl_cm = col_double(),
##   ..   male_svl_cm = col_double(),
##   ..   female_svl_cm = col_double(),
##   ..   birth_or_hatching_svl_cm = col_double(),
##   ..   female_svl_at_maturity_cm = col_double(),
##   ..   female_body_mass_at_maturity_g = col_double(),
##   ..   no_sex_svl_cm = col_double(),
##   ..   no_sex_maturity_d = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```
NA's are represented by "-999" in the amniota dataframe.

**3. Do some exploratory analysis of the `amphibio` data set. Use the function(s) of your choice. Try to get an idea of how NA's are represented in the data.**  

```r
str(amphibio)
```

```
## spc_tbl_ [6,776 × 38] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ id                     : chr [1:6776] "Anf0001" "Anf0002" "Anf0003" "Anf0004" ...
##  $ Order                  : chr [1:6776] "Anura" "Anura" "Anura" "Anura" ...
##  $ Family                 : chr [1:6776] "Allophrynidae" "Alytidae" "Alytidae" "Alytidae" ...
##  $ Genus                  : chr [1:6776] "Allophryne" "Alytes" "Alytes" "Alytes" ...
##  $ Species                : chr [1:6776] "Allophryne ruthveni" "Alytes cisternasii" "Alytes dickhilleni" "Alytes maurus" ...
##  $ Fos                    : num [1:6776] NA NA NA NA NA 1 1 1 1 1 ...
##  $ Ter                    : num [1:6776] 1 1 1 1 1 1 1 1 1 1 ...
##  $ Aqu                    : num [1:6776] 1 1 1 1 NA 1 1 1 1 1 ...
##  $ Arb                    : num [1:6776] 1 1 1 1 1 1 NA NA NA NA ...
##  $ Leaves                 : num [1:6776] NA NA NA NA NA NA NA NA NA NA ...
##  $ Flowers                : num [1:6776] NA NA NA NA NA NA NA NA NA NA ...
##  $ Seeds                  : num [1:6776] NA NA NA NA NA NA NA NA NA NA ...
##  $ Fruits                 : logi [1:6776] NA NA NA NA NA NA ...
##  $ Arthro                 : num [1:6776] 1 1 1 NA 1 1 1 1 1 NA ...
##  $ Vert                   : num [1:6776] NA NA NA NA NA NA 1 NA NA NA ...
##  $ Diu                    : num [1:6776] 1 NA NA NA NA NA 1 1 1 NA ...
##  $ Noc                    : num [1:6776] 1 1 1 NA 1 1 1 1 1 NA ...
##  $ Crepu                  : num [1:6776] 1 NA NA NA NA 1 NA NA NA NA ...
##  $ Wet_warm               : num [1:6776] NA NA NA NA 1 1 NA NA NA NA ...
##  $ Wet_cold               : num [1:6776] 1 NA NA NA NA NA 1 NA NA NA ...
##  $ Dry_warm               : num [1:6776] NA NA NA NA NA NA NA NA NA NA ...
##  $ Dry_cold               : num [1:6776] NA NA NA NA NA NA NA NA NA NA ...
##  $ Body_mass_g            : num [1:6776] 31 6.1 NA NA 2.31 13.4 21.8 NA NA NA ...
##  $ Age_at_maturity_min_y  : num [1:6776] NA 2 2 NA 3 2 3 NA NA NA ...
##  $ Age_at_maturity_max_y  : num [1:6776] NA 2 2 NA 3 3 5 NA NA NA ...
##  $ Body_size_mm           : num [1:6776] 31 50 55 NA 40 55 80 60 65 NA ...
##  $ Size_at_maturity_min_mm: num [1:6776] NA 27 NA NA NA 35 NA NA NA NA ...
##  $ Size_at_maturity_max_mm: num [1:6776] NA 36 NA NA NA 40.5 NA NA NA NA ...
##  $ Longevity_max_y        : num [1:6776] NA 6 NA NA NA 7 9 NA NA NA ...
##  $ Litter_size_min_n      : num [1:6776] 300 60 40 NA 7 53 300 1500 1000 NA ...
##  $ Litter_size_max_n      : num [1:6776] 300 180 40 NA 20 171 1500 1500 1000 NA ...
##  $ Reproductive_output_y  : num [1:6776] 1 4 1 4 1 4 6 1 1 1 ...
##  $ Offspring_size_min_mm  : num [1:6776] NA 2.6 NA NA 5.4 2.6 1.5 NA 1.5 NA ...
##  $ Offspring_size_max_mm  : num [1:6776] NA 3.5 NA NA 7 5 2 NA 1.5 NA ...
##  $ Dir                    : num [1:6776] 0 0 0 0 0 0 0 0 0 0 ...
##  $ Lar                    : num [1:6776] 1 1 1 1 1 1 1 1 1 1 ...
##  $ Viv                    : num [1:6776] 0 0 0 0 0 0 0 0 0 0 ...
##  $ OBS                    : chr [1:6776] NA NA NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   id = col_character(),
##   ..   Order = col_character(),
##   ..   Family = col_character(),
##   ..   Genus = col_character(),
##   ..   Species = col_character(),
##   ..   Fos = col_double(),
##   ..   Ter = col_double(),
##   ..   Aqu = col_double(),
##   ..   Arb = col_double(),
##   ..   Leaves = col_double(),
##   ..   Flowers = col_double(),
##   ..   Seeds = col_double(),
##   ..   Fruits = col_logical(),
##   ..   Arthro = col_double(),
##   ..   Vert = col_double(),
##   ..   Diu = col_double(),
##   ..   Noc = col_double(),
##   ..   Crepu = col_double(),
##   ..   Wet_warm = col_double(),
##   ..   Wet_cold = col_double(),
##   ..   Dry_warm = col_double(),
##   ..   Dry_cold = col_double(),
##   ..   Body_mass_g = col_double(),
##   ..   Age_at_maturity_min_y = col_double(),
##   ..   Age_at_maturity_max_y = col_double(),
##   ..   Body_size_mm = col_double(),
##   ..   Size_at_maturity_min_mm = col_double(),
##   ..   Size_at_maturity_max_mm = col_double(),
##   ..   Longevity_max_y = col_double(),
##   ..   Litter_size_min_n = col_double(),
##   ..   Litter_size_max_n = col_double(),
##   ..   Reproductive_output_y = col_double(),
##   ..   Offspring_size_min_mm = col_double(),
##   ..   Offspring_size_max_mm = col_double(),
##   ..   Dir = col_double(),
##   ..   Lar = col_double(),
##   ..   Viv = col_double(),
##   ..   OBS = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```
NA's are represented by "NA" in the amphibio data frame.

**4. How many total NA's are in each data set? Do these values make sense? Are NA's represented by values?**   

`amniota`  

```r
count(amniota, "-999")
```

```
## # A tibble: 1 × 2
##   `"-999"`     n
##   <chr>    <int>
## 1 -999     21322
```

`amphibio`  

```r
count(amphibio, NA)
```

```
## # A tibble: 1 × 2
##   `NA`      n
##   <lgl> <int>
## 1 NA     6776
```

**5. Make any necessary replacements in the data such that all NA's appear as "NA".**   

```r
amniota_tidy <- amniota %>% 
  na_if("-999")
```

**6. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amniota` data.**  

```r
naniar::miss_var_summary(amniota_tidy)
```

```
## # A tibble: 36 × 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <dbl>
##  1 subspecies                      21322    100  
##  2 female_body_mass_at_maturity_g  21318    100. 
##  3 female_svl_at_maturity_cm       21120     99.1
##  4 fledging_mass_g                 21111     99.0
##  5 male_svl_cm                     21040     98.7
##  6 no_sex_maturity_d               20860     97.8
##  7 egg_width_mm                    20727     97.2
##  8 egg_length_mm                   20702     97.1
##  9 weaning_weight_g                20258     95.0
## 10 female_svl_cm                   20242     94.9
## # … with 26 more rows
```

**7. Use the package `naniar` to produce a summary, including percentages, of missing data in each column for the `amphibio` data.**

```r
naniar::miss_var_summary(amphibio)
```

```
## # A tibble: 38 × 3
##    variable n_miss pct_miss
##    <chr>     <int>    <dbl>
##  1 Fruits     6774    100. 
##  2 Flowers    6772     99.9
##  3 Seeds      6772     99.9
##  4 Leaves     6752     99.6
##  5 Dry_cold   6735     99.4
##  6 Vert       6657     98.2
##  7 OBS        6651     98.2
##  8 Wet_cold   6625     97.8
##  9 Crepu      6608     97.5
## 10 Dry_warm   6572     97.0
## # … with 28 more rows
```

**8. For the `amniota` data, calculate the number of NAs in the `egg_mass_g` column sorted by taxonomic class; i.e. how many NA's are present in the `egg_mass_g` column in birds, mammals, and reptiles? Does this results make sense biologically? How do these results affect your interpretation of NA's?**  

```r
amniota_tidy %>% 
  group_by(class) %>% 
  count(egg_mass_g==NA) %>% 
  select(class, "number NA" = n)
```

```
## # A tibble: 3 × 2
## # Groups:   class [3]
##   class    `number NA`
##   <chr>          <int>
## 1 Aves            9802
## 2 Mammalia        4953
## 3 Reptilia        6567
```

**9. The `amphibio` data have variables that classify species as fossorial (burrowing), terrestrial, aquatic, or arboreal. Calculate the number of NA's in each of these variables. Do you think that the authors intend us to think that there are NA's in these columns or could they represent something else? Explain.**

```r
amphibio %>% 
  count(across(c("Fos", "Ter", "Aqu", "Arb"))) %>% 
  select("fossorial" = Fos, "terrestrial" = Ter, "aquatic" = Aqu, "arboreal" = Arb, "n_individuals" = n)
```

```
## # A tibble: 15 × 5
##    fossorial terrestrial aquatic arboreal n_individuals
##        <dbl>       <dbl>   <dbl>    <dbl>         <int>
##  1         1           1       1        1             1
##  2         1           1       1       NA           534
##  3         1           1      NA        1             8
##  4         1           1      NA       NA            82
##  5         1          NA       1       NA            56
##  6         1          NA      NA        1             2
##  7         1          NA      NA       NA            40
##  8        NA           1       1        1          1165
##  9        NA           1       1       NA          1997
## 10        NA           1      NA        1           846
## 11        NA           1      NA       NA          1039
## 12        NA          NA       1        1            97
## 13        NA          NA       1       NA           116
## 14        NA          NA      NA        1           310
## 15        NA          NA      NA       NA           483
```

**10. Now that we know how NA's are represented in the `amniota` data, how would you load the data such that the values which represent NA's are automatically converted?**

```r
amniota <- read_csv("lab7_hw_data/amniota.csv") %>% 
  na_if("-999")
```

```
## Rows: 21322 Columns: 36
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (6): class, order, family, genus, species, common_name
## dbl (30): subspecies, female_maturity_d, litter_or_clutch_size_n, litters_or...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
amniota
```

```
## # A tibble: 21,322 × 36
##    class order      family genus species subsp…¹ commo…² femal…³ litte…⁴ litte…⁵
##    <chr> <chr>      <chr>  <chr> <chr>     <dbl> <chr>     <dbl>   <dbl>   <dbl>
##  1 Aves  Accipitri… Accip… Acci… albogu…      NA Pied G…     NA    NA         NA
##  2 Aves  Accipitri… Accip… Acci… badius       NA Shikra     363.    3.25       1
##  3 Aves  Accipitri… Accip… Acci… bicolor      NA Bicolo…     NA     2.7       NA
##  4 Aves  Accipitri… Accip… Acci… brachy…      NA New Br…     NA    NA         NA
##  5 Aves  Accipitri… Accip… Acci… brevip…      NA Levant…    363.    4          1
##  6 Aves  Accipitri… Accip… Acci… castan…      NA Chestn…     NA    NA         NA
##  7 Aves  Accipitri… Accip… Acci… chilen…      NA Chilea…     NA     2.7       NA
##  8 Aves  Accipitri… Accip… Acci… chiono…      NA White-…    548.    4.25       1
##  9 Aves  Accipitri… Accip… Acci… cirroc…      NA Collar…     NA     3.25      NA
## 10 Aves  Accipitri… Accip… Acci… cooper…      NA Cooper…    730     4.35       1
## # … with 21,312 more rows, 26 more variables: adult_body_mass_g <dbl>,
## #   maximum_longevity_y <dbl>, gestation_d <dbl>, weaning_d <dbl>,
## #   birth_or_hatching_weight_g <dbl>, weaning_weight_g <dbl>, egg_mass_g <dbl>,
## #   incubation_d <dbl>, fledging_age_d <dbl>, longevity_y <dbl>,
## #   male_maturity_d <dbl>, inter_litter_or_interbirth_interval_y <dbl>,
## #   female_body_mass_g <dbl>, male_body_mass_g <dbl>, no_sex_body_mass_g <dbl>,
## #   egg_width_mm <dbl>, egg_length_mm <dbl>, fledging_mass_g <dbl>, …
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
