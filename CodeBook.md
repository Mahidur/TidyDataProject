This is the code book explaining the project and various features of the data set
The purpose of this project is to demonstrate our ability to collect, work with, and clean a data set. The goal was to prepare tidy data that can be used for later analysis. 
The data provided comes from in the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone.

A full description is available at the site where the data was obtained: 
   http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The data for the project are here: 
  https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

The features and other information about the various files and data sets including steps in the gathering of the data has been provided in the main directory. 
For the purpose of understanding this tidydata set, the following information will be important:
  After downloading and unzipping the file, I moved all the required files such as 
"features.txt", 
"activity_labels.txt"
 "subject_test.txt"
 "y_test.txt"
 "X_test.txt"
 "subject_train.txt"
 "y_train.txt"
 "X_train.txt"
 
 into another directory called "Tidydata". I have saved my script "run_analysis.R" in this directory too. Thus my working directory was 
 "/Users/mrahman/Desktop/Data Science Course/Getting and Cleaning data/Course Project/Projtidy/Tidydata"
 
 I have left out the intertia directory from the test and the train directories as those data were not required for the project. 
 
  My R script called run_analysis.R does the following to clean the data and prepare the submitted tidy data:
    
        -Merges the training and the test sets to create one data set: 
          Step 1: Created a data frame for the training data files by columnbinding subject_train, y_train, and X-train files.
          Step 2: Created a second data frame for the test data files by columnbinding subject_test, y_test, and X-test files.
          Step 3: Combined the train and the test data frames by rbinding
        
        -Extracts only the measurements on the mean and standard deviation for each measurement.
          Step 1: First Labelled the combined dataframe with the apropriate variable names. The variable names in the feature file for the 561
          variables were in one variable. So I transfromed this file to change the rows into columns and thus have the names for the 561 variables.
          Step 2: Subjcet_ID, Activity_type and all the variables for the 561 columns were combined and transformed to make a data frame with the variable names in order.
          Step 3: Using colnames() function, the complete data set was labelled appropriately.
          Step 4. Exctracted the mean and standard deviation values only using grep() function.
          
       -Uses descriptive activity names to name the activities in the data set
         The various activity types were labelled by matching the numeric values to the corresponding labels using match()
        
         -Appropriately labels the data set with descriptive variable names.
          Step: using gsub() function and repeating several times various components of the vriable names were changed to tidy format.
  
        -From the data set in step 4, creates a second, independent tidy data set (submitted as 'tidydata.txt') with the average of each variable for each activity and each subject.
          Step : group_by() and summarise() functions were used to get the final tidydat table with the mean values for the variables for each subject and each activity type.
The tidydata set contains 180 observations for 30 people (variable "Subject_ID") performing 6 activities ("Activity_type") such as 

1 WALKING

2 WALKING_UPSTAIRS

3 WALKING_DOWNSTAIRS

4 SITTING

5 STANDING

6 LAYING

For each person and each activity the mean for the average and the standard deviation of measures (from the signals) have been generated and stored as variables:
  
$ Subject_ID                                     
$ Activity_type                                   
$ tBodyAcceleration.MeanValue.X                   
$ tBodyAcceleration.MeanValue.Y                   
$ tBodyAcceleration.MeanValue.Z                   
$ tGravityAcceleration.MeanValue.X                
$ tGravityAcceleration.MeanValue.Y                
$ tGravityAcceleration.MeanValue.Z                
$ tBodyAccelerationJerk.MeanValue.X               
$ tBodyAccelerationJerk.MeanValue.Y               
$ tBodyAccelerationJerk.MeanValue.Z               
$ tBodyGyro.MeanValue.X                           
$ tBodyGyro.MeanValue.Y                           
$ tBodyGyro.MeanValue.Z                           
$ tBodyGyroJerk.MeanValue.X                       
$ tBodyGyroJerk.MeanValue.Y                       
$ tBodyGyroJerk.MeanValue.Z                       
$ tBodyAccelerationMagnitude.MeanValue            
$ tGravityAccelerationMagnitude.MeanValue         
$ tBodyAccelerationJerkMagnitude.MeanValue        
$ tBodyGyroMagnitude.MeanValue                    
$ tBodyGyroJerkMagnitude.MeanValue                
$ fBodyAcceleration.MeanValue.X                   
$ fBodyAcceleration.MeanValue.Y                   
$ fBodyAcceleration.MeanValue.Z                   
$ fBodyAcceleration.MeanValueFreq.X               
$ fBodyAcceleration.MeanValueFreq.Y               
$ fBodyAcceleration.MeanValueFreq.Z             
$ fBodyAccelerationJerk.MeanValue.X               
$ fBodyAccelerationJerk.MeanValue.Y               
$ fBodyAccelerationJerk.MeanValue.Z               
$ fBodyAccelerationJerk.MeanValueFreq.X           
$ fBodyAccelerationJerk.MeanValueFreq.Y           
$ fBodyAccelerationJerk.MeanValueFreq.Z           
$ fBodyGyro.MeanValue.X                           
$ fBodyGyro.MeanValue.Y                           
$ fBodyGyro.MeanValue.Z                           
$ fBodyGyro.MeanValueFreq.X                       
$ fBodyGyro.MeanValueFreq.Y                       
$ fBodyGyro.MeanValueFreq.Z                       
$ fBodyAccelerationMagnitude.MeanValue            
$ fBodyAccelerationMagnitude.MeanValueFreq        
$ fBodyAccelerationJerkMagnitude.MeanValue        
$ fBodyAccelerationJerkMagnitude.MeanValueFreq    
$ fBodyGyroMagnitude.MeanValue                    
$ fBodyGyroMagnitude.MeanValueFreq                
$ fBodyGyroJerkMagnitude.MeanValue                
$ fBodyGyroJerkMagnitude.MeanValueFreq            
$ tBodyAcceleration.StandardDeviation.X           
$ tBodyAcceleration.StandardDeviation.Y           
$ tBodyAcceleration.StandardDeviation.Z           
$ tGravityAcceleration.StandardDeviation.X        
$ tGravityAcceleration.StandardDeviation.Y        
$ tGravityAcceleration.StandardDeviation.Z        
$ tBodyAccelerationJerk.StandardDeviation.X       
$ tBodyAccelerationJerk.StandardDeviation.Y       
$ tBodyAccelerationJerk.StandardDeviation.Z       
$ tBodyGyro.StandardDeviation.X                   
$ tBodyGyro.StandardDeviation.Y                   
$ tBodyGyro.StandardDeviation.Z                   
$ tBodyGyroJerk.StandardDeviation.X               
$ tBodyGyroJerk.StandardDeviation.Y               
$ tBodyGyroJerk.StandardDeviation.Z               
$ tBodyAccelerationMagnitude.StandardDeviation    
$ tGravityAccelerationMagnitude.StandardDeviation 
$ tBodyAccelerationJerkMagnitude.StandardDeviation
$ tBodyGyroMagnitude.StandardDeviation            
$ tBodyGyroJerkMagnitude.StandardDeviation        
$ fBodyAcceleration.StandardDeviation.X           
$ fBodyAcceleration.StandardDeviation.Y           
$ fBodyAcceleration.StandardDeviation.Z           
$ fBodyAccelerationJerk.StandardDeviation.X       
$ fBodyAccelerationJerk.StandardDeviation.Y       
$ fBodyAccelerationJerk.StandardDeviation.Z       
$ fBodyGyro.StandardDeviation.X                   
$ fBodyGyro.StandardDeviation.Y                   
$ fBodyGyro.StandardDeviation.Z                   
$ fBodyAccelerationMagnitude.StandardDeviation    
$ fBodyAccelerationJerkMagnitude.StandardDeviation
$ fBodyGyroMagnitude.StandardDeviation            
$ fBodyGyroJerkMagnitude.StandardDeviation        

here, t stands for Time and f- for Fast Fourier Transformation. Freq stands for frequency and X, Y, and Z represents the axis of motion. 

Units:
The units for Time and Frequency are in 'seconds' and 'Hertz (Hz)'

Acknowledgement:
Successful completion of this project would not have been possible without the online help forums such as
CRAN and StackOverflow. In particular,  I would like to thank David Hood in the discussion forum, who has really transformed this course into something intellectually exciting. 

Citations:
[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
