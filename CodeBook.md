This is the code book explaining the project and various features of the data set
The purpose of this project is to demonstrate our ability to collect, work with, and clean a data set. The goal was to prepare tidy data that can be used for later analysis. 
The data provided comes from in the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone.

A full description is available at the site where the data was obtained: 
   http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The data for the project are here: 
  https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

The features other information about the various files and data sets including steps in the gathering of the data has been provided in the main directory. 
For the purpose of understanding this tidydata set, the following information will be important:
  
   R script called run_analysis.R has created that does the following. 
        -Merges the training and the test sets to create one data set.
        -Extracts only the measurements on the mean and standard deviation for each measurement. 
        -Uses descriptive activity names to name the activities in the data set
        -Appropriately labels the data set with descriptive variable names. 
        -From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
  
The tidydata set contains 180 observations for 30 people (variable "Subject_ID") performing 6 activities ("Activity_type") such as 

1 WALKING
2 WALKING_UPSTAIRS
3 WALKING_DOWNSTAIRS
4 SITTING
5 STANDING
6 LAYING

For each person and each activity the mean for the average and the standard deviation of the following measures have been generated and stored as variables:
  
