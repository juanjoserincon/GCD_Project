# Getting and Cleaning Data Course Project - CodeBook
========================================================

This file describes the variables, the data, and any transformations or work that it has been performed to clean up the data.

## Summary of the data set information

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

## Source of the information

The site where the data was obtained:  
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The data for the project:  
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 


## Clean up of the data

The run_analysis.R script performs the following steps to clean the data:  

1. Read X_test.txt, y_test.txt and subject_test.txt from the "./UCI HAR Dataset/test" folder and store them in xtest, ytest and stest variables respectively.

2. Read X_train.txt, y_train.txt and subject_train.txt from the "./UCI HAR Dataset/test" folder and store them in xtrain, ytrain and strain variables respectively.

3. Append data of the different "test" object created in point 1 to obtain just one object "test" (using cbind). Also adding a new attribute "Source" with value "test" to indicate that the data came from the test group.

4. Append data of the different "train" object created in point 2 to obtain just one object "train" (using cbind). Also adding a new attribute "Source" with value "train" to indicate that the data came from the train group.

5. Concatenate "train" and "test"" objects to create one object "data"

6. Clean unused object to free memory. These objects are: xtest, ytest, stest, xtrain, ytrain, strain, test and train. Only "data" object remains in memory.

7. Read the features.txt file from the "/UCI HAR Dataset" folder and store the data in an object called "features". 

8. Assign the names of the variables included in "features" to the attributes of the object "data", using a temporary varaibles called "names". In addition, rename the first three columns as "TestLabel", Subject" and "Source".

9. Store in the variable "ms" (for mean-std) the values of "features" that include "mean", "Mean" or "std" in any position of the string. So, we have identified information related with means and standar deviations.

10. Subset the columns of "data" removing the ones that do not appear in "ms".

11. Make the names of the columns of "data" syntactically valid for R using "make.names" function and clean unused object to free memory.

12. Read the information included in the file "/UCI HAR Dataset/activity_labels.txt" and store it in an object called "TestLabels". Rename the names of the columns to help in the following merging process.

13. Merge "data" and "TestLabels" information by "TestLabel" column to add descriptive information for activities to "data". The results include both "TestLabel" and "TestName", even though both contains the same information, as it could be useful to the final user and consistency is assured by the process.

14. After clening memory of unused objects, the initial dity data set is finished, so the next steps focus on obtaining the second tidy data set that includes the averages of each variable. 

15. Create the averages data set called "data2", using aggregate function grouping by columns "TestLabel", Subject" and "Source". As this process is applied to the whole "data" object, not separately column by column for the averages, it creates a duplicate of the "TestLabel", Subject" and "Source" columns (the function consider them the groups but applied the average to this columns also). To differenciate from the previous ones, these columns are named as their original but with and "A" of aggregate at the end: "TestLabelA", SubjectA" and "SourceA". After this, remove the duplicate columns generated.

16. Remove the duplicate columns generated by passing the whole 'data' object to aggregate instead of each column each time

17. Order de dataset by Test-Source-Subject (not completely neccesary but useful to human reading).

18. Write the "data" object to "completedata.txt" file in current working directory.

19. Write the "data2" object to "tidydata.txt" file in current working directory.


## Variable descrition

This section contains an explanation of the columns used to identify the register, as well as a guide to understand the names of the other 86 columns.

### Identification columns

These are the columns that identifies the information included in the register.

Variable name     |      Description
------------------|-------------------
SubjectA          | Subject who performed the activity. Its range is from 1 to 30.
TestNameA         | Activity name. Values: "LAYING", "SITTING", "STANDING", "WALKING", "WALKING_DOWNSTAIRS" and "WALKING_UPSTAIRS".
TestLabelA        | Code of the activity. Its range is from 1 to 6.
SourceA           | Group of study. Values: "test" or "train".

### Other columns

In the following lines, it is explained the components of the names of the variables, so the meaning of the name could be build upon the pieces of which it is formed.

* "t" and "f" stand for "time" and "frequency".

* "Acc" and "Gyro" stand for accelerometer and gyroscope.

* "Body" and "Gravity" stand for the type of acceleration signal.

* "mean" and "std" stand for the mean and the standard deviation.

* "Jerk" stands for the jerk signal.

* "angle" stands for the angle between two vectors.

* "X", "Y" and "Z" is used to denote 3-axial signals in the X, Y and Z directions.