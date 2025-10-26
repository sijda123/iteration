Writing Functions
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
# create vector (collection) of numbers
x_vec = rnorm(20, mean = 10, sd = 3.5)

# find z-score for the vector of numbers
(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -1.0087506 -0.2663427 -0.1489646  0.5812239  1.0349536  1.5784870
    ##  [7] -0.1206505 -0.4849178 -0.1977817  0.4424095 -0.3900343 -0.9796468
    ## [13]  2.2705047  0.8952265 -0.7881722 -1.5832394  0.3528677 -0.3496644
    ## [19]  0.7453696 -1.5828773

Write a function to compute z scores.

``` r
# argument does in the parenthesis

z_scores = function(x) {
  
  # update function with why the function might break (when it's not numeric or when it doesn't have enough values)
  if (!is.numeric(x)) {
    stop("The input x should be numeric")
  }
  
  if (length(x) < 5) {
    stop("Only compute z scores when the input has 5 or more numbers")
  }
  
  # don't use x_vec in your function because it's in your global environment
  z = (x - mean(x)) / sd(x)
  
  # output z only exists inside this function
  z
  
}
```

Let’s try our function …

``` r
# compute z score for whatever valued that are put in
z_scores(x = x_vec)
```

    ##  [1] -1.0087506 -0.2663427 -0.1489646  0.5812239  1.0349536  1.5784870
    ##  [7] -0.1206505 -0.4849178 -0.1977817  0.4424095 -0.3900343 -0.9796468
    ## [13]  2.2705047  0.8952265 -0.7881722 -1.5832394  0.3528677 -0.3496644
    ## [19]  0.7453696 -1.5828773

``` r
num_vec = rnorm(123, mean = 14, sd = 0.4)

z_scores(x = num_vec)
```

    ##   [1] -0.480616328  0.805198273 -0.645608800  0.194145094 -0.691515897
    ##   [6] -0.995717213  0.377974701  2.398945640  0.477935452  0.044671946
    ##  [11]  0.016343384  1.051288812  1.381209359  1.233619051 -2.963706452
    ##  [16] -0.128482501 -0.979671204 -0.981758371  0.241867866 -0.582011057
    ##  [21] -0.735657528  0.646631311 -0.525011411 -0.137988434 -0.032451855
    ##  [26] -0.025225300  0.656845553  0.602125718 -1.033711011 -0.149919509
    ##  [31] -0.529888236 -2.512540639  0.432905676 -1.140879706 -0.320798512
    ##  [36]  1.092796954 -0.860344301 -0.457008254 -1.598805391 -0.525245343
    ##  [41]  3.209487683 -1.832930721 -0.569050222 -0.868687391  1.228644206
    ##  [46]  0.301550318 -0.362853053  0.651007726 -0.476711137 -2.509819329
    ##  [51]  1.060951271 -1.028049819  0.564061839  1.142486531 -1.551732937
    ##  [56]  1.117725618  1.033874009 -1.093032953 -0.041241225  0.178266251
    ##  [61]  1.654392047 -0.854062301 -0.236128602  0.573627100 -0.367219360
    ##  [66]  1.914831259 -0.319681665 -0.106648691 -0.517310811  1.216529627
    ##  [71]  0.197992033  0.476881079  1.663267821  0.471231616 -0.664831963
    ##  [76] -0.758756671 -1.704890169  1.498933719 -0.174805385  0.379973209
    ##  [81]  1.730805911  0.995968719 -0.529008525  0.800787546  0.278870620
    ##  [86] -0.008135695  0.968089389 -0.528076814 -0.183743905  0.490148945
    ##  [91] -1.138704560  1.840580028 -1.153744529  0.616942843 -1.411023539
    ##  [96] -0.171732266  0.055458021 -1.744833319  0.546423170  0.340336553
    ## [101]  0.417838361 -0.950716312 -0.591616634  1.242478628  0.590625180
    ## [106] -0.075858455 -0.530147142  0.768526315 -0.471434607  1.620936539
    ## [111] -0.153483432 -0.084208119 -0.772982637  0.080793697  1.138652398
    ## [116] -0.412607774 -0.206434956 -0.771938975  0.263104898  0.342258173
    ## [121]  0.254573417 -0.646834820  0.035855571

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

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("The input x should be numeric")
  }
  
  if (length(x) < 5) {
    stop("Only compute mean and sd when the input has 5 or more numbers")
  }
  
  mean_x = mean(x, na.rm = TRUE)
  sd_x = sd(x, na.rm = TRUE)
  
  # produces tibble as the output
  tibble(
    mean = mean_x, 
    sd = sd_x
  )
  
}

mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  11.3  3.14

## Make up data ..

Let’s *simulate* some data

``` r
# tibble creates a dataframe
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
    ## 1   3.24      2.20

``` r
# you get a different mean and sd everytime you run the code because the values are randomly selected
```

Write a function to do simulations. The inputs are

- `n_subj` is number of subjects
- `mu` is the true mean
- `sigma` is the true sd

Function simulates data from a normal and computes sample mean and sd.

``` r
sim_mean_sd = function(n_subj, mu = 3, sigma = 2) {
  
  sim_df = 
    tibble(
      x = rnorm(n = n_subj, mean = mu, sd = sigma)
    )
  
  sim_df |> 
    summarize(
      mu_hat = mean(x),
      sigma_hat = sd(x)
    )
  
}
```

Let’s run this function.

``` r
# 50 is taken in as the number of subjects
sim_mean_sd(mu = 48, 50)
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   48.3      2.32

``` r
# you will get means and sd close to the inputs or default arguments if an input is not given
```

Import the LoTR data

``` r
# similar code used every time

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

# only the table changes among the three code chunks

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

don’t forget documentation
