data_from_the_web
================
Shina Min
2023-10-22

## Scarpe a table

I want the first table from \[this page\]
(<https://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm>)

read in the html

``` r
url = "https://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

drug_use_html = read_html(url)
```

extract the table(s); focus on the first one

``` r
table_marj = 
  drug_use_html %>%  
  html_table() %>%  
  first() %>%
  slice(-1) %>% # access specific rows in a data set (removing the first row)
  as_tibble() # converting to a tibble
view(table_marj)
```

## non-table collection of data from a website

## Star Wars Movie info

I want the dat from \[here\]
(“<https://www.imdb.com/list/ls070150896/>”)

``` r
url = "https://www.imdb.com/list/ls070150896/"

swm_html = read_html(url)
```

Grab elements that I want.

``` r
title_vec =
  swm_html %>%
  html_nodes(css = ".lister-item-header a") %>%
  html_text() # converting an html object to just the text

gross_rev_vec =
  swm_html %>%
  html_nodes(css = ".text-small:nth-child(7) span:nth-child(5)") %>%
  html_text()
  
runtime_vec = # I want to know how long this movies are
  swm_html %>%
  html_nodes(css = ".runtime") %>%
  html_text()
```