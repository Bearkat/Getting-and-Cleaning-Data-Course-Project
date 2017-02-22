##Contents:

-run_analysis.R obtains and cleans wearable device data from the link found in codebook.md

-codebook modifies and updates the codebooks that were provided with the original data

-cleaned dataset "tidy.txt"

##run_analysis.R description:
run_analysis.R will merge the test and train datasets showing mean and standard devitation from wearable device data collected from a samsung galaxy smartphone. Please make sure plyr and dplyr packages are installed before running this script. The object "tidy" is the tidy data set with the averages for each activity for each subject. CodeBook.md describes the variables and how they are derived. 

Step 1: load plyr and dplyr packages assign values to working directory and url objects.  

Step 2: Download and unzip data, set file paths to data. 

Step 3: Read features datat from features.txt, assign to object "features." Subset features to rows containing either mean or stdev. 

Step 4: Make features human readable/tidy. Stored in object "features_mean_std"

Step 5: Read labels data, remove underscores and replace with spaces.

Step 6: Read activity data. Create a factor with activity numbers converted to descriptive activity names and replace underscores with spaces.

Step 7: Read in test and train subject and feature data sets and rename features variables (from step 3). 

Step 8: Subset train and test sets to contain only columns with mean or stdev

Step 9: Rename test and train subset columns with tidy variables. 

Step 10: Add subject (step 7) and descriptive activity (from step 6) variables to test and train datasets.   

Step 11: Merge test and train data sets

Step 12: create a second tidy data set with average values of each activity for each subject. Subset data from "merged" by activity.

Step 13: Determine average values for each column by subject

Step 14: Create data frame built from averages of variables. 