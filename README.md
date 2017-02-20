##Run_analysis will merge the test and train datasets showing mean and standard devitation from wearable device 
##data collected from a samsung galaxy smartphone. Please make sure plyr and dplyr packages are installed 
##before running this script. The object "tidy" is the tidy data set with the averages for each 
##activity for each subject.

##Step 1: load plyr and dplyr packages assign "wd" as working directory and "url" to the data.  
library(plyr)
library(dplyr)
url <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
wd <- getwd()

##Step 2: Download and unzip data, set file paths to data. 
download.file(url, destfile = "HAR_data.zip", method = "curl")
unzip(zipfile = "HAR_data.zip", exdir = wd)
test_path <- file.path("./UCI HAR Dataset", "test")
train_path <- file.path("./UCI HAR Dataset", "train")

##Step 3: Read features datat from features.txt, assign to object "features." Subset features to rows containing ##either mean or stdev. 
features <- read.table("./UCI HAR Dataset/features.txt", stringsAsFactors = FALSE)
mean_std_features <- grep("mean|std", features$V2) 
features_mean_std <- features[mean_std_features, ]

##Step 4: Make features human readable/tidy. Stored in object "features_mean_std""
features_mean_std[1:40, 2] <- gsub("mean\\()", "mean time", features_mean_std[1:40, 2])
features_mean_std[1:40, 2] <- gsub("std\\()", "standard deviation time", features_mean_std[1:40, 2])
features_mean_std[41:79, 2] <- gsub("mean\\()", "mean frequency", features_mean_std[41:79, 2])
features_mean_std[41:79, 2] <- gsub("meanFreq\\()", "weighted mean frequency", features_mean_std[41:79, 2])
features_mean_std[41:79, 2] <- gsub("std\\()", "standard deviation frequency", features_mean_std[41:79, 2])
features_mean_std$V2 <- gsub("(^t|^f)", "", features_mean_std$V2)
features_mean_std$V2 <- gsub("-", " ", features_mean_std$V2)
features_mean_std$V2 <- gsub("Mag", " magnitude", features_mean_std$V2)
features_mean_std$V2 <- gsub("Jerk", " jerk", features_mean_std$V2)
features_mean_std$V2 <- gsub("Acc", " acceleration", features_mean_std$V2)
features_mean_std$V2 <- gsub("Gyro", " angular velocity", features_mean_std$V2)
features_mean_std$V2 <- gsub("BodyBody", "body body", features_mean_std$V2)
features_mean_std$V2 <- gsub("^B", "b", features_mean_std$V2)
features_mean_std$V2 <- gsub("^G", "g", features_mean_std$V2)

##Step 5: Read labels data, remove underscores and replace with spaces.
labels_table <- read.table("./UCI HAR Dataset/activity_labels.txt", stringsAsFactors = FALSE)
labels <- gsub("_", " ", labels_table$V2)

##Step 6: Read activity data. Create a factor with activity numbers converted to descriptive activity names and ##replace underscores with spaces.
test_act <- read.table(file.path(test_path, "y_test.txt"), col.names = "activity", stringsAsFactors = FALSE)
train_act <- read.table(file.path(train_path, "y_train.txt"), col.names = "activity", stringsAsFactors = FALSE)
test_act_factor <- factor(test_act$activity, labels = labels); test_act_factor <- gsub("_", " ", test_act_factor)
train_act_factor <- factor(train_act$activity, labels = labels); test_act_factor<- gsub("_", " ", test_act_factor)
test_act$activity <- test_act_factor
train_act$activity <- train_act_factor

##Step 7: Read in test and train subject and feature data sets and rename features variables (from step 3). 
test_subjects <- read.table(file.path(test_path, "subject_test.txt"), col.names = "subject", stringsAsFactors = FALSE)
train_subjects <- read.table(file.path(train_path, "subject_train.txt"), col.names = "subject", stringsAsFactors = FALSE)
train_set <- read.table(file.path(train_path, "X_train.txt"), col.names = features$V2, stringsAsFactors = FALSE)
test_set <- read.table(file.path(test_path, "X_test.txt"), col.names = features$V2, stringsAsFactors = FALSE)
names(train_set) <- features$V2
names(test_set) <- features$V2

##Step 8: Subset train and test sets to contain only columns with mean or stdev
train_subset <- train_set[ , mean_std_features]
test_subset <- test_set[ , mean_std_features]

##Step 9: Rename test and train subset columns with tidy variables. 
names(train_subset) <- features_mean_std$V2
names(test_subset) <- features_mean_std$V2

##Step 10: Add subject (step 7) and descriptive activity (from step 6) variables to test and train datasets.   
train_bound <- cbind(train_subjects, "activity" = train_act$activity, train_subset)
test_bound <- cbind(test_subjects, "activity" = test_act$activity, test_subset)

##Step 11: Merge test and train data sets
merged <- rbind(train_bound, test_bound)  

##Step 12: create a second tidy data set with average values of each activity for each subject. 
##Subset data from "merged" by activity.
walking <- merged[which(merged$activity == "WALKING"), ]
walking_upstairs <- merged[which(merged$activity == "WALKING UPSTAIRS"), ]
walking_downstairs <- merged[which(merged$activity == "WALKING DOWNSTAIRS"), ]
sitting <- merged[which(merged$activity == "SITTING"), ]
standing <- merged[which(merged$activity == "STANDING"), ]
laying <- merged[which(merged$activity == "LAYING"), ]

##Step 13: Determine average values for each column by subject
w <- cbind(subject = 1:30, activity = "walking", 
           ldply(1:30, function(i) colMeans(walking[which(walking$subject == i), 3:81])))
wu <- cbind(subject = 1:30, activity = "walking upstairs", 
           ldply(1:30, function(i) colMeans(walking_upstairs[which(walking_upstairs$subject == i), 3:81])))
wd <- cbind(subject = 1:30, activity = "walking downstairs", 
           ldply(1:30, function(i) colMeans(walking_downstairs[which(walking_downstairs$subject == i), 3:81])))
sit <- cbind(subject = 1:30, activity = "sitting", 
           ldply(1:30, function(i) colMeans(sitting[which(sitting$subject == i), 3:81])))
stand <- cbind(subject = 1:30, activity = "standing", 
           ldply(1:30, function(i) colMeans(standing[which(standing$subject == i), 3:81])))
l <- cbind(subject = 1:30, activity = "laying", 
           ldply(1:30, function(i) colMeans(laying[which(laying$subject == i), 3:81])))

##step 14: Create data frame built from averages of variables. 
tidy <- rbind(l, sit, stand, w, wd, wu, stringsAsFactors = FALSE)
arrange(tidy, subject, activity)
View(tidy)

