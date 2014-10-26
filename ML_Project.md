# Analysis on Weight Lifting Exercises data
sdd1012  
Saturday, October 21, 2014  

## Introduction
The project analyses the **Weight Lifting Exercises Dataset** , which is a data frame with 19622 observations with 160 variables. The "classe" variable represents manner in which the participants did the exercise. See **Reference** section below.
The goal of the project is to build model to predict the manner, the "classe", with out of sample accuracy higher than 95%.


## Approach
1.      The **caret** R package with rpart and randomForest are installed and loaded for analysis using tree and random forest. 



2.      The features of dataset is cleaned for columns having more than 50% NA value or blank value. The first 7 variables are also removed as they are ID, timestamp or not measurement.

3.      The dataset pml_training is partitioned into train/test in 70/30 ratio.

[1] "The no. of features chosen for tree = 52"


4.      The train set is trained using **rpart**, and the test set is evaluated for out of sample accuracy.

[1] "In Sample accuracy percentage of tree model = 49.50"
[1] "Out Of Sample accuracy percentage of tree model = 49.62"


5.      The importance of the variables are further studied for the tree model as the accuracy is significantly low. The variables with very low importance are removed, so the data can be used for random forest effectively.  



```
## rpart variable importance
## 
##   only 20 most important variables shown (out of 52)
## 
##                   Overall
## pitch_forearm       100.0
## roll_forearm         72.0
## roll_belt            70.3
## magnet_dumbbell_y    48.4
## accel_belt_z         43.2
## yaw_belt             40.4
## magnet_belt_y        39.1
## total_accel_belt     35.5
## accel_arm_x          26.5
## magnet_arm_x         26.2
## magnet_dumbbell_z    18.5
## roll_dumbbell        18.4
## magnet_dumbbell_x    18.2
## accel_dumbbell_y     15.7
## roll_arm             14.0
## magnet_belt_x         0.0
## total_accel_arm       0.0
## magnet_forearm_y      0.0
## yaw_arm               0.0
## magnet_belt_z         0.0
```

6.      The train set is trained using **rf**, and the test set is evaluated for out of sample accuracy


```
## [1] "In Sample accuracy percentage of RF model = 100.00"
```

```
## [1] "Out Of Sample accuracy percentage of RF model = 98.91"
```


7.    Some metrics of the random forest model with test set follows:  


```
##           Reference
## Prediction    A    B    C    D    E
##          A 1673    6    0    3    0
##          B    1 1120    9    1    2
##          C    0   11 1013   18    2
##          D    0    2    4  940    3
##          E    0    0    0    2 1075
```

```
##          Sensitivity Specificity Pos Pred Value Neg Pred Value Prevalence
## Class: A      0.9994      0.9979         0.9946         0.9998     0.2845
## Class: B      0.9833      0.9973         0.9885         0.9960     0.1935
## Class: C      0.9873      0.9936         0.9703         0.9973     0.1743
## Class: D      0.9751      0.9982         0.9905         0.9951     0.1638
## Class: E      0.9935      0.9996         0.9981         0.9985     0.1839
##          Detection Rate Detection Prevalence Balanced Accuracy
## Class: A         0.2843               0.2858            0.9986
## Class: B         0.1903               0.1925            0.9903
## Class: C         0.1721               0.1774            0.9905
## Class: D         0.1597               0.1613            0.9866
## Class: E         0.1827               0.1830            0.9966
```


### Conclusion
The random forest model is promising and a model with following variables in the order of importance can be chosen.


```
## rf variable importance
## 
##                   Overall
## roll_belt          100.00
## yaw_belt            73.09
## pitch_forearm       62.54
## magnet_dumbbell_z   59.60
## roll_forearm        43.65
## magnet_dumbbell_y   42.94
## accel_dumbbell_y    31.42
## magnet_dumbbell_x   27.13
## roll_dumbbell       21.58
## magnet_belt_y       21.01
## roll_arm            19.80
## accel_belt_z        17.85
## accel_arm_x         11.83
## magnet_arm_x         9.31
## total_accel_belt     0.00
```


#### Reference:
Velloso, E.; Bulling, A.; Gellersen, H.; Ugulino, W.; Fuks, H. [Qualitative Activity Recognition of Weight Lifting Exercises](http://groupware.les.inf.puc-rio.br/work.jsf?p1=11201) Proceedings of 4th International Conference in Cooperation with SIGCHI (Augmented Human '13) . Stuttgart, Germany: ACM SIGCHI, 2013.

