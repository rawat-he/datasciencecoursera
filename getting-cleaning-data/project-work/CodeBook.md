---
title: "Project - Code Book"
output:
  html_document:
    toc: yes
---
*********
# About Data
One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained: 

[Original Data Link](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

**Note:** Please refer `README.md` for data set link.

### UCI HAR Dataset
     + train (have all training data set)
     + test (have all test data set)
     + README.txt
     + features_info.txt
     + features.txt
     + activit_labels.txt

# Data Files

File Name                   |   Information
-----------------           |   ------------
activity_lables.txt         |   It contains information about the activities performed by each subject
features.txt                |   Shows information about the variables used for the feature vector. Links to **features_info.txt**. 561-feature vector with time and frequency domain variables.
features_info.txt           |   This file lists all the features/experiments exercised. They were calculated, seperated and filtered at different levels. `**f**` stands for frequency and `**t**` for time.
train/y_train.txt           |   This is the activity performed. Links to **activity_lables.txt**. 
train/subjects_train.txt    |   Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30.
train/X_train.txt           |   Training data. Values calculated after the subjects performed different activities.Links to **features_info.txt**

**Note: Above is applicable for test as well.**

For more information, please read <span style="color:red;">`README.txt`</span>.

# Variables

Below are the variable objects constructed after reading the data files.

Name                        |   Information
-------------               |   -------------
activity.labels             |   This object represents activities performed read from `activity_lables.txt`.
features                    |   This objects represents features calculated read from `features.txt`.
test.observations           |   This objects represents test data read from `X_test.txt`.
test.activity               |   This objects represents test activity data read from `y_test.txt`.
test.subjects               |   This objects represents test subjects data read from `subjects_test.txt`.
train.observations          |   This objects represents training data read from `X_train.txt`.
train.activity              |   This objects represents training activity data read from `y_train.txt`.
train.subjects              |   This objects represents training subjects data read from `subjects_train.txt`.

# Transformations

After the reading the data files, data has to undergo lot of transformations. Information is provided below.

## Binding Rows and Columns
Name                        |   Information
-------------               |   -------------
merged.observations         |   All the rows from test and train observations were stacked and appended together.
merged.activity             |   All the rows from test and train activities were stacked and appended together.
merged.subjects             |   All the rows from test and train subjects were stacked and appended together.
final.merge                 |   Binded together by columns `(merged.subjects,merged.activity,merged.observations)` into a single data frame.

## Filtering
Name                        |   Information
-------------               |   -------------
final.merge.filtered        |   `final.merge` was filtered by column names having `mean or std` because project requirements says extract only the measurements on the mean and standard deviation for each observations/measurement.

## Descriptive and Labelling

1. `final.merge.filtered` data frame column name `Activity` values were then given appropriate descriptive activity name from `activity.lables` object. 
2. `final.merge.filtered` data frame column names (except Activity and Subjects) were then appropriately labelled with descriptive variable names. 

Any column name having :
```
Acc -> Accelerometer
Gyro -> Gyroscope
BodyBody -> Body
Mag -> Magnitude
t -> Time
f -> Frequency
Body -> TimeBody
-mean() -> Mean
-std() -> SD
-freq() -> Frequency
angle -> Angle
gravity -> Gravity
```

## Transformations

`dplyr` package is utilised for the data transformations. Group by and summarise operations were chained together to produce tidy data set

1. `group by` **Activity and Subject**.
2. `summarise each column` for **mean**.

# Output
`tidy-data-set.txt` is the independent tidy data set produced.

*******