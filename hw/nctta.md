R Notebook
================

Helpful Notes
-------------

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code.

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd+Shift+Enter*.

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Cmd+Option+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Cmd+Shift+K* to preview the HTML file).

The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike *Knit*, *Preview* does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed.

Load Match Data for Northwestern vs Everyone Else
-------------------------------------------------

The data came from the [team seedings table](http://www.nctta.org/champs/2018/news/2018%20team%20seeding.pdf). We are the 19th seed.

``` r
nu_weights <- c(0,0,1,0,0.02,0.02,0.03,0.78,2,0.94,1.25,0.13,1.08,1.18,1.1,2.12,1.59,2.03,-1,0.83,1.69,2.29,2.3,2.89)
other_weights <- c(5,5,4,5,4.98,4.98,4.97,4.22,3,4.06,3.75,4.87,3.92,3.82,3.9,2.88,3.41,2.97,-1,4.17,3.31,2.71,2.7,2.11)
teams <- c('Texas Wesleyan', 'Mississippi College', 'Pillar College', 'California', 'NYU', 'Lindenwood', 'Northeastern', 'UC Davis', 'Maryland', 'Stony Brook', 'Florida', 'Texas', 'UCSD', 'Minnesota', 'UCLA', 'Binghamton', 'Duke', 'Brown', 'Northwestern', 'UBC', 'Washington', 'Ottawa', 'Brandeis', 'UT Dallas')
group_seeds <- ceiling(1:24 / 6)

matches <- data.frame(teams, group_seeds, nu_weights, other_weights, nu_weights - other_weights, sign(nu_weights - other_weights))
colnames(matches) <- c("teams", "groupseed", "nu_score", "others_score", "difference", "nu_wins")
```

Comparing Weightings for our Groups
-----------------------------------

``` r
attach(matches)
```

    ## The following object is masked _by_ .GlobalEnv:
    ## 
    ##     teams

``` r
matches[order(difference),]
```

    ##                  teams groupseed nu_score others_score difference nu_wins
    ## 1       Texas Wesleyan         1     0.00         5.00      -5.00      -1
    ## 2  Mississippi College         1     0.00         5.00      -5.00      -1
    ## 4           California         1     0.00         5.00      -5.00      -1
    ## 5                  NYU         1     0.02         4.98      -4.96      -1
    ## 6           Lindenwood         1     0.02         4.98      -4.96      -1
    ## 7         Northeastern         2     0.03         4.97      -4.94      -1
    ## 12               Texas         2     0.13         4.87      -4.74      -1
    ## 8             UC Davis         2     0.78         4.22      -3.44      -1
    ## 20                 UBC         4     0.83         4.17      -3.34      -1
    ## 10         Stony Brook         2     0.94         4.06      -3.12      -1
    ## 3       Pillar College         1     1.00         4.00      -3.00      -1
    ## 13                UCSD         3     1.08         3.92      -2.84      -1
    ## 15                UCLA         3     1.10         3.90      -2.80      -1
    ## 14           Minnesota         3     1.18         3.82      -2.64      -1
    ## 11             Florida         2     1.25         3.75      -2.50      -1
    ## 17                Duke         3     1.59         3.41      -1.82      -1
    ## 21          Washington         4     1.69         3.31      -1.62      -1
    ## 9             Maryland         2     2.00         3.00      -1.00      -1
    ## 18               Brown         3     2.03         2.97      -0.94      -1
    ## 16          Binghamton         3     2.12         2.88      -0.76      -1
    ## 22              Ottawa         4     2.29         2.71      -0.42      -1
    ## 23            Brandeis         4     2.30         2.70      -0.40      -1
    ## 19        Northwestern         4    -1.00        -1.00       0.00       0
    ## 24           UT Dallas         4     2.89         2.11       0.78       1
