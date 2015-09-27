 TidyDataProject
Getting and Cleaning Data, Course Project 
This repo explains how all of the scripts work and how they are connected.  

The data was downloaded and unzipped as follows
if (!file.exists("Projtidy")) {dir.create("Projtidy")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip" 
download.file(fileUrl, destfile = "./Projtidy/FUCI.zip", method = "curl")
unzip("FUCI.zip", exdir =".", unzip = "internal", setTimes = TRUE)
dir()

"run_analysis.R" is the name of the R script consisting of 41 lines of codes as follows

run_analysis <- function() {   ## name of the sript that
  library(dplyr)               ## loads the packages "dplyr", "tidyr", "plyr" which will be used at different stages                                    of the script
  library(tidyr)
  library(plyr)
  c1 = read.table('subject_test.txt') ## c1, c2, and c3 loads the tables "subject_test", "y_test", and "X_test"                                                  respectively
  c2 = read.table('y_test.txt')
  c3 = read.table('X_test.txt')
  testdf <- cbind(c1, c2, c3) ## combines the tables to make one table for the "test" data sets
  d1 = read.table('subject_train.txt')  ## d1, d2, and d3 loads the tables "subject_train", "y_train", and "X_train"
  d2 = read.table('y_train.txt')
  d3 = read.table('X_train.txt')
  traindf <- cbind(d1, d2, d3) ## combines the tables to make one table for the "train" data sets
  combinedf <- rbind(testdf, traindf) ## combines ("merges"?) the two dataframes to create one data set
  asdfcombinedf <- as.data.frame(combinedf) ## ensures that "combinedf" is a data frame
  f1 = read.table('features.txt')   ## loads the "feature" file
  f1df <- as.data.frame(f1[,2]) ## extracts the required row only
  f1transposdf <- t(f1df) ## transposes the rows into columns (561 variables)
  names <- c("Subject_ID", "Activity_type") ## names for the first two columns
  namesdf <- t(data.frame(names)) ## makes a data frame for the names
  completenames <- cbind(namesdf, f1transposdf) ## combines names for all the 563 (Subject_ID, Activty_type and all the 561 variables from the features file) variables
  colnames(asdfcombinedf) <- completenames[,1:563] ## all the variable have their "untidy" names
  ## completes step 1 of the project
  Extractmean<- asdfcombinedf[grep("mean", colnames(asdfcombinedf))] ## Extracts only mean columns
  Extractstd<- asdfcombinedf[grep("std", colnames(asdfcombinedf))]  ## Extracts only the std columns
  subjectactivitydf <- asdfcombinedf[ , 1:2] ## subsets the subject_ID and Activity_type columns
  subactmeanstd <- cbind(subjectactivitydf, Extractmean, Extractstd) ## combines all the three files to make the required data frame  ## completes step 2 of the project
  f2 = read.table('activity_labels.txt') ## loads activity type table
  subactmeanstd$Activity_type <- f2[,2][match(subactmeanstd$Activity_type, f2[,1])] ## labels activity type properly replacing the corresponding integers
  ## completes step 3 of the project
  names(subactmeanstd) <- gsub("BodyBody", "Body", names(subactmeanstd)) ## finds and replaces "BodyBody" with "Body"
  names(subactmeanstd) <- gsub("Acc", "Acceleration", names(subactmeanstd)) ## finds and replaces "Acc" with "Acceleration"
  names(subactmeanstd) <- gsub("mean", "MeanValue", names(subactmeanstd)) ## finds and replaces "mean" with "MeanValue"
  names(subactmeanstd) <- gsub("Mag", "Magnitude", names(subactmeanstd)) ## finds and replaces "Mag" with "Magnitude"
  names(subactmeanstd) <- gsub("std", "StandardDeviation", names(subactmeanstd)) ## finds and replaces "Std" with "StandardDeviation"
  names(subactmeanstd) <- gsub("\\(\\)", "", names(subactmeanstd))  ## completes step 4 of the project
  compdata1 <- arrange(subactmeanstd, -desc(Subject_ID)) ## rearranges the data set with ascending order of the Subject_IDs
  compdata2 <- group_by(compdata1, Activity_type) ## rearranges the data set with groupings of Activity_type
  tidydata <- compdata1 %>% group_by(Subject_ID, Activity_type) %>% summarise_each(funs(mean)) ## takes the data set compdata1 groups                             by the Subject_ID and Activity_type and for each Subject and each Activity takes mean of all the other                               variables and stores it with the variable compdata2
  write.table(tidydata,"tidydata.txt", row.name = FALSE) ## writes a datatable as ".txt" file type and completes step 5 of the                   project
  tidydata
}
