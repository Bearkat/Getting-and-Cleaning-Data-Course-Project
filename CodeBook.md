Each of the features/variables in R objects “tidy” and "merged"" are derived from the dataset found in: 

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

Original data were downloaded from: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Descriptions of the original features, from which we have derived these data can be found below. We extracted mean and standard deviation variables of each of the described features from X_test.txt and X_train.txt for each subject. We then determined the average value of each extracted variable for each subject for each activity. Angular velocity units are in radians per second. Acceleration data are in "gravity" units (presumably meters per second^2). Time and frequency indicate domains in which acceleration and angular velocity were obtained from accelerometer and gyroscope, respectively. Frequency signals are derived from time domain signals by application of a fast Fourier transform. X, Y and Z indicate relative direction.

We renamed the features into the following:

 [1] "body acceleration mean time X"                                         
 [2] "body acceleration mean time Y"                                         
 [3] "body acceleration mean time Z"                                         
 [4] "body acceleration standard deviation time X"                           
 [5] "body acceleration standard deviation time Y"                           
 [6] "body acceleration standard deviation time Z"                           
 [7] "gravity acceleration mean time X"                                      
 [8] "gravity acceleration mean time Y"                                      
 [9] "gravity acceleration mean time Z"                                      
[10] "gravity acceleration standard deviation time X"                        
[11] "gravity acceleration standard deviation time Y"                        
[12] "gravity acceleration standard deviation time Z"                        
[13] "body acceleration jerk mean time X"                                    
[14] "body acceleration jerk mean time Y"                                    
[15] "body acceleration jerk mean time Z"                                    
[16] "body acceleration jerk standard deviation time X"                      
[17] "body acceleration jerk standard deviation time Y"                      
[18] "body acceleration jerk standard deviation time Z"                      
[19] "body angular velocity mean time X"                                     
[20] "body angular velocity mean time Y"                                     
[21] "body angular velocity mean time Z"                                     
[22] "body angular velocity standard deviation time X"                       
[23] "body angular velocity standard deviation time Y"                       
[24] "body angular velocity standard deviation time Z"                       
[25] "body angular velocity jerk mean time X"                                
[26] "body angular velocity jerk mean time Y"                                
[27] "body angular velocity jerk mean time Z"                                
[28] "body angular velocity jerk standard deviation time X"                  
[29] "body angular velocity jerk standard deviation time Y"                  
[30] "body angular velocity jerk standard deviation time Z"                  
[31] "body acceleration magnitude mean time"                                 
[32] "body acceleration magnitude standard deviation time"                   
[33] "gravity acceleration magnitude mean time"                              
[34] "gravity acceleration magnitude standard deviation time"                
[35] "body acceleration jerk magnitude mean time"                            
[36] "body acceleration jerk magnitude standard deviation time"              
[37] "body angular velocity magnitude mean time"                             
[38] "body angular velocity magnitude standard deviation time"               
[39] "body angular velocity jerk magnitude mean time"                        
[40] "body angular velocity jerk magnitude standard deviation time"          
[41] "body acceleration mean frequency X"                                    
[42] "body acceleration mean frequency Y"                                    
[43] "body acceleration mean frequency Z"                                    
[44] "body acceleration standard deviation frequency X"                      
[45] "body acceleration standard deviation frequency Y"                      
[46] "body acceleration standard deviation frequency Z"                      
[47] "body acceleration weighted mean frequency X"                           
[48] "body acceleration weighted mean frequency Y"                           
[49] "body acceleration weighted mean frequency Z"                           
[50] "body acceleration jerk mean frequency X"                               
[51] "body acceleration jerk mean frequency Y"                               
[52] "body acceleration jerk mean frequency Z"                               
[53] "body acceleration jerk standard deviation frequency X"                 
[54] "body acceleration jerk standard deviation frequency Y"                 
[55] "body acceleration jerk standard deviation frequency Z"                 
[56] "body acceleration jerk weighted mean frequency X"                      
[57] "body acceleration jerk weighted mean frequency Y"                      
[58] "body acceleration jerk weighted mean frequency Z"                      
[59] "body angular velocity mean frequency X"                                
[60] "body angular velocity mean frequency Y"                                
[61] "body angular velocity mean frequency Z"                                
[62] "body angular velocity standard deviation frequency X"                  
[63] "body angular velocity standard deviation frequency Y"                  
[64] "body angular velocity standard deviation frequency Z"                  
[65] "body angular velocity weighted mean frequency X"                       
[66] "body angular velocity weighted mean frequency Y"                       
[67] "body angular velocity weighted mean frequency Z"                       
[68] "body acceleration magnitude mean frequency"                            
[69] "body acceleration magnitude standard deviation frequency"              
[70] "body acceleration magnitude weighted mean frequency"                   
[71] "body body acceleration jerk magnitude mean frequency"                  
[72] "body body acceleration jerk magnitude standard deviation frequency"    
[73] "body body acceleration jerk magnitude weighted mean frequency"         
[74] "body body angular velocity magnitude mean frequency"                   
[75] "body body angular velocity magnitude standard deviation frequency"     
[76] "body body angular velocity magnitude weighted mean frequency"          
[77] "body body angular velocity jerk magnitude mean frequency"              
[78] "body body angular velocity jerk magnitude standard deviation frequency"
[79] "body body angular velocity jerk magnitude weighted mean frequency" 


The following is a description of the "features" taken from a Samsung Galaxy Smartphone by Anguita et al., 2012. 

Copied from features_info.txt and README.txt:

“The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details.

The features selected for this database come from the accelerometer and gyroscope 3-
axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to
denote time) were captured at a constant rate of 50 Hz. Then they were filtered using
a median filter and a 3rd order low pass Butterworth filter with a corner frequency
of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into
body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using
another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time 
to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude 
of these three-dimensional signals were calculated using the Euclidean norm 
(tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing 
fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, 
fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag"


