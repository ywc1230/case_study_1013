Case study
================

## Load the airbnb data

``` r
data("nyc_airbnb")
```

## Brainstorm some questions

*What is the best Airbnb in Staten Island for \< 100? *What price range
is popular in each borough? most rented? *What apartment features are
related to price? *Cheapest room type in each neighborhood? \*Hosts have
higher ratings?

## Answer some questions

data cleaning

``` r
nyc_airbnb = 
  nyc_airbnb %>% 
  mutate(stars = review_scores_location/2)
```

``` r
nyc_airbnb %>%
  count(neighbourhood_group, room_type) %>%
  pivot_wider(
    names_from = room_type, 
    values_from = n
  )
```

    ## # A tibble: 5 x 4
    ##   neighbourhood_group `Entire home/apt` `Private room` `Shared room`
    ##   <chr>                           <int>          <int>         <int>
    ## 1 Bronx                             192            429            28
    ## 2 Brooklyn                         7427           9000           383
    ## 3 Manhattan                       10814           7812           586
    ## 4 Queens                           1388           2241           192
    ## 5 Staten Island                     116            144             1

``` r
nyc_airbnb %>%
  group_by(neighbourhood_group, room_type) %>%
  summarize(mean_price = mean(price))
```

    ## `summarise()` regrouping output by 'neighbourhood_group' (override with `.groups` argument)

    ## # A tibble: 15 x 3
    ## # Groups:   neighbourhood_group [5]
    ##    neighbourhood_group room_type       mean_price
    ##    <chr>               <chr>                <dbl>
    ##  1 Bronx               Entire home/apt      125. 
    ##  2 Bronx               Private room          65.5
    ##  3 Bronx               Shared room           57.5
    ##  4 Brooklyn            Entire home/apt      175. 
    ##  5 Brooklyn            Private room          76.7
    ##  6 Brooklyn            Shared room           59.6
    ##  7 Manhattan           Entire home/apt      238. 
    ##  8 Manhattan           Private room         107. 
    ##  9 Manhattan           Shared room           84.7
    ## 10 Queens              Entire home/apt      140. 
    ## 11 Queens              Private room          70.6
    ## 12 Queens              Shared room           49.1
    ## 13 Staten Island       Entire home/apt      207. 
    ## 14 Staten Island       Private room          65.4
    ## 15 Staten Island       Shared room           25
