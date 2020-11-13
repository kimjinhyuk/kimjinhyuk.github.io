---
layout: post
title: practice movie ratings R - Data analysis
excerpt: "Data analysis is a process of inspecting, cleansing, transforming and modeling data with the goal of discovering useful information, informing conclusions and supporting decision-making. Data analysis has multiple facets and approaches, encompassing diverse techniques under a variety of names, and is used in different business, science, and social science domains. In today's business world, data analysis plays a role in making decisions more scientific and helping businesses operate more effectively"
categories: [Data analysis]
use_math: true
comments: true
tag: [Data analysis, R, markdown]
---



First R Markdown with movie rating data
---------------------------------------

-   Read data

``` r
movies <- read.csv('data/Movie Ratings.csv',header=T)
```

``` r
summary(movies)
```

    ##      Film              Genre           Rotten.Tomatoes.Ratings..
    ##  Length:562         Length:562         Min.   : 0.0             
    ##  Class :character   Class :character   1st Qu.:25.0             
    ##  Mode  :character   Mode  :character   Median :46.0             
    ##                                        Mean   :47.4             
    ##                                        3rd Qu.:70.0             
    ##                                        Max.   :97.0             
    ##  Audience.Ratings.. Budget..million... Year.of.release
    ##  Min.   : 0.00      Min.   :  0.0      Min.   :2007   
    ##  1st Qu.:47.00      1st Qu.: 20.0      1st Qu.:2008   
    ##  Median :58.00      Median : 35.0      Median :2009   
    ##  Mean   :58.83      Mean   : 50.1      Mean   :2009   
    ##  3rd Qu.:72.00      3rd Qu.: 65.0      3rd Qu.:2010   
    ##  Max.   :96.00      Max.   :300.0      Max.   :2011

\* change the column names
--------------------------

``` r
colnames(movies) <- c('name','genre','criticsratings','audienceratings','budgetmillions','releaseyear')
```

To see the types of genre
-------------------------

``` r
levels(movies$genre)
```

    ## NULL

``` r
head(movies)
```

    ##                    name     genre criticsratings audienceratings budgetmillions
    ## 1 (500) Days of Summer     Comedy             87              81              8
    ## 2           10,000 B.C. Adventure              9              44            105
    ## 3            12 Rounds     Action             30              52             20
    ## 4             127 Hours Adventure             93              84             18
    ## 5             17 Again     Comedy             55              70             20
    ## 6                  2012    Action             39              63            200
    ##   releaseyear
    ## 1        2009
    ## 2        2008
    ## 3        2009
    ## 4        2010
    ## 5        2009
    ## 6        2009

changing the numeric column to categorical
------------------------------------------

``` r
movies$releaseyear<-as.factor(movies$releaseyear)
levels(movies$releaseyear)
```

    ## [1] "2007" "2008" "2009" "2010" "2011"

ggplot2 package
---------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-3-1.png?raw=true)

color and size setting
----------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-4-1.png?raw=true)

Color and Size mapping
----------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-5-1.png?raw=true)![](01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-5-2.png?raw=true)

changing the graph type
-----------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-6-1.png?raw=true)

genre mappig
------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-7-1.png?raw=true)

Using facet grid to divide the graph according to genre
-------------------------------------------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-8-1.png?raw=true)

    ## Warning: Ignoring unknown parameters: stack

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-9-1.png?raw=true)

Adding new layer for limiting the yscale
----------------------------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-10-1.png?raw=true)

histograms with facet grid
--------------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-11-1.png?raw=true)

Scaling x and y coordinates
---------------------------

    ## Warning: Removed 371 rows containing missing values (geom_point).

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-12-1.png?raw=true)

adding themes to plots
----------------------

see the difference between d & d + theme\_economist()
-----------------------------------------------------

![](https://github.com/kimjinhyuk/kimjinhyuk.github.io/blob/master/img/01_basic_vidualization_files/figure-markdown_github/unnamed-chunk-14-1.png?raw=true)
