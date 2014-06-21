## Getting and Cleaning Data Course Project
========================================================

This file describes how to replicate the file uploaded into Coursera based on the "run_analysis.R" script included also in this repository.

Follow the next steps:

1. Set your working directory.
1. Download and unzip the data from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip.  
A subfolder called "UCI HAR Dataset" will be created.
2. In RStudio, use the command source("run_analysis.R") to execute the script that creates the "tidy dataset".
3. You will find two output files are generated in the current working directory:
completedata.txt (10.4 Mb): it contains a data frame called data with 10299*90 dimension.
tidydata.txt (287 Kb): it contains a data frame called data2 with 180*90 dimension.
4. Use data <- read.table("tidydata.txt") command in RStudio to read the file. 

The result is 180 rows with all combinations for each of the 90 attributes, as we were required to obtain the average of each variable for each activity and each subject, and there are 6 activities in total and 30 subjects in total.