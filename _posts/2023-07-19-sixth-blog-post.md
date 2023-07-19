Most Interesting Machine Learning Method
================
Simon Weisenhorn
2023-07-19

I gained a lot of very helpful knowledge following the exploration we
had with machine learning in this course. The machine learning method
that I found most interesting was boosted trees. A boosted tree is a
ensemble based model that treats the errors created by previous decision
trees. By considering the errors of trees in previous rounds, the
boosted tree model forms new trees sequentially where each tree is
dependent on the previous tree. This adjustment accounts for overfitting
which is one of the major drawbacks of regular decision trees. These
kinds of models are also useful for non-linear data, which make them
great for real world applications. Let’s explore a situation where a
boosting tree might be helpful below.

### Set Up

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.1     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.1     
    ## ── Conflicts ────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(datasets)
library(caret)
```

    ## Loading required package: lattice
    ## 
    ## Attaching package: 'caret'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     lift

``` r
#loading the necessary libraries for the code below

Titanic <- data.frame(Titanic) #converting Titanic data to data frame
Titanic <- uncount(Titanic, weights=Freq) 
#duplicating rows based on weighted variable (Freq)

set.seed(558) #setting seed for reproducibility 

trainIndex <- createDataPartition(Titanic$Survived, p = 0.75, 
                                  list = FALSE)
#Creating indexes for training data 

TitanicTrain <- Titanic[trainIndex, ] #Creating training dataset
TitanicTest <- Titanic[-trainIndex, ] #Creating testing dataset
```

In the chunk above, I loaded in the data and partitioned it into a 75/25
training testing split. The data consists of information about the
Titanic passengers, such as their class, age, and gender, as well as
whether they survived the wreck or not. The analysis below will utilize
the variables in a boosted tree model to predict whether a passenger
survived.

### Boosted Tree

``` r
library(gbm) #Need this library to run the training function

allTuningParameters <- expand.grid(n.trees=c(25,50,100,150,200), interaction.depth=c(1,2,3,4), shrinkage=0.1, n.minobsinnode = 10)
#Creating dataframe for the tuneGrid arguement using expand.grid

boostTreeFit <- train(Survived ~ ., data = TitanicTrain,
                      method = "gbm",
                      preProcess = c("center", "scale"),
                      trControl = trainControl(method = "repeatedcv", 
                                               number = 5, repeats=3),
                      tuneGrid=allTuningParameters,
                      verbose=FALSE)
#Fitting the boosted tree model

boostTreeFit
```

    ## Stochastic Gradient Boosting 
    ## 
    ## 1652 samples
    ##    3 predictor
    ##    2 classes: 'No', 'Yes' 
    ## 
    ## Pre-processing: centered (5), scaled (5) 
    ## Resampling: Cross-Validated (5 fold, repeated 3 times) 
    ## Summary of sample sizes: 1322, 1322, 1321, 1322, 1321, 1321, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   interaction.depth  n.trees  Accuracy   Kappa    
    ##   1                   25      0.7736245  0.4316263
    ##   1                   50      0.7736245  0.4316263
    ##   1                  100      0.7750368  0.4358804
    ##   1                  150      0.7760457  0.4388676
    ##   1                  200      0.7762477  0.4394593
    ##   2                   25      0.7879453  0.4244758
    ##   2                   50      0.7911758  0.4363936
    ##   2                  100      0.7942012  0.4439415
    ##   2                  150      0.7938002  0.4439805
    ##   2                  200      0.7938002  0.4439805
    ##   3                   25      0.7899637  0.4303027
    ##   3                   50      0.7946053  0.4452959
    ##   3                  100      0.7938002  0.4439805
    ##   3                  150      0.7948073  0.4459321
    ##   3                  200      0.7938002  0.4439805
    ##   4                   25      0.7911746  0.4342293
    ##   4                   50      0.7948073  0.4459321
    ##   4                  100      0.7948073  0.4459321
    ##   4                  150      0.7948073  0.4459321
    ##   4                  200      0.7948073  0.4459321
    ## 
    ## Tuning parameter 'shrinkage' was held constant at a value of 0.1
    ## Tuning
    ##  parameter 'n.minobsinnode' was held constant at a value of 10
    ## Accuracy was used to select the optimal model using the largest value.
    ## The final values used for the model were n.trees = 50, interaction.depth = 4, shrinkage
    ##  = 0.1 and n.minobsinnode = 10.

``` r
#viewing the resulting model
```

The chunk above was used to fit the boosted tree model, which uses 5
fold repeated cross validation.

``` r
confusionMatrix(data = TitanicTest$Survived, 
                reference = predict(boostTreeFit, newdata = TitanicTest))
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction  No Yes
    ##        No  366   6
    ##        Yes 116  61
    ##                                           
    ##                Accuracy : 0.7778          
    ##                  95% CI : (0.7406, 0.8119)
    ##     No Information Rate : 0.878           
    ##     P-Value [Acc > NIR] : 1               
    ##                                           
    ##                   Kappa : 0.3924          
    ##                                           
    ##  Mcnemar's Test P-Value : <2e-16          
    ##                                           
    ##             Sensitivity : 0.7593          
    ##             Specificity : 0.9104          
    ##          Pos Pred Value : 0.9839          
    ##          Neg Pred Value : 0.3446          
    ##              Prevalence : 0.8780          
    ##          Detection Rate : 0.6667          
    ##    Detection Prevalence : 0.6776          
    ##       Balanced Accuracy : 0.8349          
    ##                                           
    ##        'Positive' Class : No              
    ## 

``` r
#checking how well the model does on the test set using the confusionMatrix 
#function
```

Finally, in the last chunk, I used the confusionMatrix function to check
how well the model did on the test set. The accuracy was 77.78% so not
too bad overall, but it could certainly improve. The best way to explore
further improvement would be to fit different ensemble models or adding
additional tuning parameters.

Overall, the boosted tree method is a very interesting machine learning
method and I look forward to exploring where I can utilize methods like
this one in future projects!
