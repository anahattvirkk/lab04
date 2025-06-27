Lab 04 - Visualizing Spatial Data
================
Anahatt Virk
06/26/25

### Load packages and data

``` r
install.packages("devtools", repos = "https://cloud.r-project.org")
```

    ## Installing package into '/Users/anahattvirk/Library/R/x86_64/4.5/library'
    ## (as 'lib' is unspecified)

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/tb/8n78wkj122z51qjf26rn855h0000gn/T//RtmpP8Q3JV/downloaded_packages

``` r
devtools::install_github("tidyverse/dsbox")
```

    ## Using GitHub PAT from the git credential store.

    ## Skipping install of 'dsbox' from a github remote, the SHA1 (244ecdfe) has not changed since last install.
    ##   Use `force = TRUE` to force installation

``` r
library(tidyverse) 
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

The Denny’s dataset has 1643 rows and 6 columns. Each row represents one
Denny’s location and the variables are address, city, state, zipcode,
longitude, and latitude.

### Exercise 2

The La Quinta dataset has 909 rows and 6 columns. Each row represents
one La Quinta location and the variables are address, city, state,
zipcode, longitude, and latitude.

### Exercise 3

From looking at the La Quinta website, there are La Quinta hotels
outside of the U.S. These countries include Canada, Mexico, China, New
Zealand, Georgia, Turkey, UAE, Chile, Colombia, and Ecuador. On the
other hand, from looking at the Denny’s website it seems that they only
have locations in the U.S.

### Exercise 4

One way to determine whether either establishment has locations outside
of the U.S. by looking at the data is to filter by state by using code.
This way, you are able to pull out all international locations. You
could also do so by filtering by city.

### Exercise 5

``` r
dn <- dennys %>%
  filter(!(state %in% states$abbreviation))
```

There are 0 Denny’s locations outside the US.

### Exercise 6

``` r
dn %>%
  mutate(country = "United States")
```

    ## # A tibble: 0 × 7
    ## # ℹ 7 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>, country <chr>

There are 0 Denny’s locations outside the US.

### Exercise 7

Outside of the U.S., there are La Quinta hotels in Canada, Mexico,
China, New Zealand, Georgia, Turkey, UAE, Chile, Colombia, and Ecuador.

### Exercise 8

``` r
lq <- laquinta %>% 
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Colombia",
    state == "MX" ~ "Mexico", 
    state == "CH" ~ "China",
    state == "NZ" ~ "New Zealand",
    state == "GE" ~ "Georgia",
    state == "TR" ~ "Turkey",
    state %in% c("AE", "UAE") ~ "UAE",
    state == "CL" ~ "Chile",
    state == "EC" ~ "Ecuador"
  ))
```

``` r
lq <- lq %>%
  filter(country == "United States")
```

### Exercise 9
