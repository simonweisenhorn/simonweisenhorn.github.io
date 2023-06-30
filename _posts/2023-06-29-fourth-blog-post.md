Coolest Thing in R
================
Simon Weisenhorn
2023-06-30

Although we have certainly covered a lot of interesting material this
semester, I think the coolest thing we have learned so far is learning
how to write our own functions in R. This ability is super helpful for
automating programming tasks and can assist with creating straight
forward or more complicated calculations. I will demonstrate a great
example of this below!

``` r
poundsToKilograms <- function(lbs){
  return(0.45359237*lbs)
}
# Here is an example of writing a simple function that I had no knowledge of
# existing before
```

``` r
"I weigh" 
```

    ## [1] "I weigh"

``` r
poundsToKilograms(167) 
```

    ## [1] 75.74993

``` r
"Kilograms!"
```

    ## [1] "Kilograms!"

``` r
# An example of applying the function
```

Above, I have shown a great example of where writing a custom function
is very helpful. Although I have shown just one input, we can create
straight forward conversions and calculations that can be applied to
large inputs of data beyond a singular data point. Prior to writing this
function, I had no knowledge of a function like this existing so I was
able to use general knowledge of how to convert from pounds to kilograms
to write one myself. This goes to show just how great the ability to
write functions in R is because of the flexibility it offers users to
apply whatever they can imagine to any given data set.
