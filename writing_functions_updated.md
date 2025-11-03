Writing Functions Updated
================

Load key packages.

``` r
library(tidyverse)
library(readxl)
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

## Start small!

Everyone loves z scores.

``` r
x_vec = rnorm(20, mean = 10, sd = 3.5)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.6302384  0.9304688 -2.3842093  0.1516948 -0.3083902 -0.1339625
    ##  [7] -0.5561797 -0.7365122 -1.2368797  0.3637414  0.5210232  1.9386778
    ## [13]  1.5358570  0.8637064  0.1110485  0.1363894 -0.5644969 -0.2656452
    ## [19]  0.3236123 -1.3201823

Write a function to compute z scores.

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("The input x should be numeric")
  }
  
  if (length(x) < 5) {
    stop("Only compute z scores when the input has 5 or more numbers")
  }
  
  z = (x - mean(x)) / sd(x)
  
  z
  
}
```

Let’s try our function …

``` r
z_scores(x = x_vec)
```

    ##  [1]  0.6302384  0.9304688 -2.3842093  0.1516948 -0.3083902 -0.1339625
    ##  [7] -0.5561797 -0.7365122 -1.2368797  0.3637414  0.5210232  1.9386778
    ## [13]  1.5358570  0.8637064  0.1110485  0.1363894 -0.5644969 -0.2656452
    ## [19]  0.3236123 -1.3201823

``` r
num_vec = rnorm(123, mean = 14, sd = 0.4)

z_scores(x = num_vec)
```

    ##   [1] -1.915754982  0.573047724 -0.300322902  1.615785249  0.474023926
    ##   [6] -1.455241237  1.213411924  0.608396781 -0.823189523 -1.365536193
    ##  [11] -0.367788055 -0.569751692  1.107336300 -0.863558419  0.241041633
    ##  [16] -0.350186901 -1.781697052 -1.413705223 -2.615472638  0.099357421
    ##  [21]  1.318815761 -1.403942385 -0.719167621 -0.403074927 -0.215328915
    ##  [26] -0.034553239 -0.597936208 -1.056727270  1.859278750  2.505241064
    ##  [31]  1.119690409 -0.473903456 -1.023662985  0.408434258 -1.650117275
    ##  [36]  0.143126733 -0.090880600  1.218130634 -1.256575020  0.444939060
    ##  [41]  1.083249821  1.001968318  1.557025850 -2.022656353 -1.152429439
    ##  [46] -0.016157149 -1.838005740  1.108469583 -0.842979695 -0.099566246
    ##  [51]  0.107471421 -1.436343834  0.211855711  0.108528543  1.543117034
    ##  [56] -0.385196252 -0.171600948 -0.577901621  0.779405080 -1.208843113
    ##  [61] -0.610796662 -1.947264239  0.840731035 -0.979111008 -0.068914924
    ##  [66] -0.141743120  0.950933525 -0.166588536  0.286240562  0.370640257
    ##  [71]  1.564780634  0.074702951  0.483928937  0.656891446  0.076946425
    ##  [76] -0.227977749  0.417924346  1.141982949  1.397574936 -0.104502327
    ##  [81] -1.397003122  0.641982584 -0.091930251 -0.628050267 -1.147357041
    ##  [86]  0.857378649  1.555106517  0.975737940  0.667548752  1.753177226
    ##  [91]  1.789425855 -0.515801010 -1.127967028  0.286947175 -1.423347910
    ##  [96]  0.150876655  0.085363879  0.835148100 -0.102270392 -0.546847284
    ## [101] -0.741382730  1.064836461 -0.074747887  0.001950921  1.100859335
    ## [106]  0.011702821  0.410177919 -0.334698074  0.821736273  0.412382242
    ## [111]  0.379332180 -0.068217690 -0.308624103  0.288569294 -0.193682166
    ## [116]  1.781468247  1.049151281  0.112546077  0.894072298 -0.196715065
    ## [121] -0.066015999 -1.699158598 -1.231435379

Let’s break our function …

``` r
z_scores(3)
```

    ## Error in z_scores(3): Only compute z scores when the input has 5 or more numbers

``` r
z_scores("my name is jeff")
```

    ## Error in z_scores("my name is jeff"): The input x should be numeric

## Let’s compute some stuff

Let’s compute and return the mean and sd of a numeric vector.

I’ve written that function and saved it to `source/mean_and_sd.R`, along
with some documentation. For completeness, I’m printing that R script
below.

    ## #' mean_and_sd
    ## #' 
    ## #' Takes a numeric input vector and computes the mean and standard deviation
    ## #'
    ## #' @param x the input vector (must be numeric with 5 or more elements)
    ## #'
    ## #' @returns a dataframe containing the mean and sd of x
    ## #' 
    ## mean_and_sd = function(x) {
    ##   
    ##   if (!is.numeric(x)) {
    ##     stop("The input x should be numeric")
    ##   }
    ##   
    ##   if (length(x) < 5) {
    ##     stop("Only compute mean and sd when the input has 5 or more numbers")
    ##   }
    ##   
    ##   mean_x = mean(x, na.rm = TRUE)
    ##   sd_x = sd(x, na.rm = TRUE)
    ##   
    ##   tibble(
    ##     mean = mean_x, 
    ##     sd = sd_x
    ##   )
    ##   
    ## }

This will import the function for use here.

``` r
source("source/mean_and_sd.R")
```

``` r
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.60  4.29

## Make up data ..

Let’s *simulate* some data

``` r
sim_df = 
  tibble(
    x = rnorm(n = 30, mean = 3, sd = 2)
  )

sim_df |> 
  summarize(
    mu_hat = mean(x),
    sigma_hat = sd(x)
  )
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   2.73      1.87

Write a function to do simulations. The inputs are

- `n_subj` is number of subjects
- `mu` is the true mean
- `sigma` is the true sd

Function simulates data from a normal and computes sample mean and sd.

(We wrote this in a code chunk last time; now it’s being sourced.)

``` r
source("source/sim_mean_sd.R")
```

Let’s run this function.

``` r
# you get different estimates every time
sim_mean_sd(mu = 48, 50)
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   47.6      2.03

``` r
sim_mean_sd(n_subj = 30)
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   3.47      2.30

Import the LoTR data

``` r
fellowship_ring = 
  read_excel("data/LotR_Words.xlsx", range = "B3:D6") |> 
  mutate(movie = "Fellowship of the Ring")

two_towers = 
  read_excel("data/LotR_Words.xlsx", range = "F3:H6") |> 
  mutate(movie = "Two Towers")

return_of_the_king = 
  read_excel("data/LotR_Words.xlsx", range = "J3:L6") |> 
  mutate(movie = "Return of the King")

lotr_df = 
  bind_rows(fellowship_ring, two_towers, return_of_the_king)
```

Turn this into a function

``` r
lotr_import = function(cell_range, movie_title) {
  
  df = 
    read_excel("data/LotR_Words.xlsx", range = cell_range) |> 
    mutate(movie = movie_title)
  
  df
  
}

fellowship = lotr_import(cell_range = "B3:D6", movie_title = "Fellowship")
two_towers = lotr_import(cell_range = "F3:H6", movie_title = "Two Towers")
return =     lotr_import(cell_range = "J3:L6", movie_title = "Return")

bind_rows(fellowship, two_towers, return)
```

    ## # A tibble: 9 × 4
    ##   Race   Female  Male movie     
    ##   <chr>   <dbl> <dbl> <chr>     
    ## 1 Elf      1229   971 Fellowship
    ## 2 Hobbit     14  3644 Fellowship
    ## 3 Man         0  1995 Fellowship
    ## 4 Elf       331   513 Two Towers
    ## 5 Hobbit      0  2463 Two Towers
    ## 6 Man       401  3589 Two Towers
    ## 7 Elf       183   510 Return    
    ## 8 Hobbit      2  2673 Return    
    ## 9 Man       268  2459 Return

Look at one more example.

``` r
nsduh_url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

nsduh_html = read_html(nsduh_url)

data_marj_year = 
  nsduh_html |> 
  html_table() |> 
  nth(1) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))

data_marj_month = 
  nsduh_html |> 
  html_table() |> 
  nth(2) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))

data_marj_first = 
  nsduh_html |> 
  html_table() |> 
  nth(3) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))
```

write an import function

``` r
nsduh_import = function(html, table_num) {
  
  data = 
    html |> 
    html_table() |> 
    nth(table_num) |>
    slice(-1) |> 
    select(-contains("P Value")) |>
    pivot_longer(
      -State,
      names_to = "age_year", 
      values_to = "percent") |>
    separate(age_year, into = c("age", "year"), sep = "\\(") |>
    mutate(
      year = str_replace(year, "\\)", ""),
      percent = str_replace(percent, "[a-c]$", ""),
      percent = as.numeric(percent)) |>
    filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))
  
  data
  
}

nsduh_import(nsduh_html, table_num = 1)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    9.98
    ##  2 Alabama 12+   2014-2015    9.6 
    ##  3 Alabama 12-17 2013-2014    9.9 
    ##  4 Alabama 12-17 2014-2015    9.71
    ##  5 Alabama 18-25 2013-2014   27.0 
    ##  6 Alabama 18-25 2014-2015   26.1 
    ##  7 Alabama 26+   2013-2014    7.1 
    ##  8 Alabama 26+   2014-2015    6.81
    ##  9 Alabama 18+   2013-2014    9.99
    ## 10 Alabama 18+   2014-2015    9.59
    ## # ℹ 500 more rows

``` r
nsduh_import(nsduh_html, table_num = 2)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    5.57
    ##  2 Alabama 12+   2014-2015    5.35
    ##  3 Alabama 12-17 2013-2014    4.98
    ##  4 Alabama 12-17 2014-2015    5.16
    ##  5 Alabama 18-25 2013-2014   15.0 
    ##  6 Alabama 18-25 2014-2015   14.3 
    ##  7 Alabama 26+   2013-2014    4.03
    ##  8 Alabama 26+   2014-2015    3.86
    ##  9 Alabama 18+   2013-2014    5.63
    ## 10 Alabama 18+   2014-2015    5.37
    ## # ℹ 500 more rows

``` r
nsduh_import(nsduh_html, table_num = 3)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    1.42
    ##  2 Alabama 12+   2014-2015    1.49
    ##  3 Alabama 12-17 2013-2014    4.46
    ##  4 Alabama 12-17 2014-2015    4.36
    ##  5 Alabama 18-25 2013-2014    6.04
    ##  6 Alabama 18-25 2014-2015    6.39
    ##  7 Alabama 26+   2013-2014    0.15
    ##  8 Alabama 26+   2014-2015    0.2 
    ##  9 Alabama 18+   2013-2014    0.95
    ## 10 Alabama 18+   2014-2015    1.05
    ## # ℹ 500 more rows
