# Getting-and-Cleaning-Data  
"Getting and Cleaning Data" Course Project Repository  
# Getting and Cleanind Data - Course Project  
# Student - Author: Hernán Gianini  
#  
# Part 1: Merges the training and the test sets to create one data set.  
#  
# Set the working directory  
setwd("C:/Users/hgian/OneDrive/Desktop/datasciencecoursera/Getting and Cleaning Data/Course Project")  
library(dplyr)  
#  
# Get de project data  
if(!file.exists("./data")){dir.create("./data")}  
dataurl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"  
download.file(dataurl,destfile="./data/Dataset.zip")  
unzip(zipfile="./data/Dataset.zip",exdir="./data")  
path_data <- file.path("./data" , "UCI HAR Dataset")  
datafiles <- list.files(path_data, recursive=TRUE)  
datafiles  
#  
# Read the subject files  
subject_train <- read.table(file.path(path_data, "train", "subject_train.txt"),header = FALSE)  
str(subject_train)  
tail(subject_train)  
subject_test  <- read.table(file.path(path_data, "test" , "subject_test.txt"),header = FALSE)  
str(subject_test)  
tail(subject_test)  
#  
# Read the activity files  
activity_train <- read.table(file.path(path_data, "train", "Y_train.txt"),header = FALSE)
str(activity_train)
tail(activity_train)
activity_test <- read.table(file.path(path_data, "test", "Y_test.txt"),header = FALSE)
str(activity_test)
tail(activity_test)
#
# Read the features files
features_test  <- read.table(file.path(path_data, "test" , "X_test.txt" ),header = FALSE)
str(features_test)
tail(features_test)
features_train  <- read.table(file.path(path_data, "train" , "X_train.txt" ),header = FALSE)
str(features_train)
tail(features_train)
#
# Merge the test and train files
#
# Concatenate the files by rows
subject_file <- rbind(subject_train,subject_test)
activity_file <- rbind(activity_train,activity_test)
features_file <- rbind(features_train,features_test)
#
# Set names to columns (variables)
names(subject_file) <- c("subject")
names(activity_file) <- c("activity")
features_names <- read.table(file.path(path_data, "features.txt"),head=FALSE)
names(features_file)<- features_names$V2
str(features_file)
#
# Concatenate the files by columns
data1 <- cbind(subject_file, activity_file)
alldata <- cbind(data1, features_file)
str(alldata)
tail(alldata)
#
# Part 2: Extracts only the measurements on the mean and standard deviation
#         for each mex <-asurement.
#
colums <- grep("subject|activity|mean\\(\\)|std\\(\\)",names(alldata))
meanstd_file <- subset(alldata, select = colums)
str(meanstd_file)
tail(meanstd_file)
#
# Part 3: Uses descriptive activity names to name the activities in the data set
#
# Get the activity labels
activity_labels <- read.table(file.path(path_data, "activity_labels.txt"),header = FALSE)
# Put descriptive activity names in variable "activity"
meanstd_file$activity <- activity_labels[meanstd_file$activity, 2]
str(meanstd_file)
tail(meanstd_file)
#
# Part 4: Appropriately labels the data set with descriptive variable names.
#
names(meanstd_file)<-gsub("^t", "Time", names(meanstd_file))
names(meanstd_file)<-gsub("^f", "Frequency", names(meanstd_file))
names(meanstd_file)<-gsub("Acc", "Accelerometer", names(meanstd_file))
names(meanstd_file)<-gsub("Gyro", "Gyroscope", names(meanstd_file))
names(meanstd_file)<-gsub("Mag", "Magnitude", names(meanstd_file))
names(meanstd_file)<-gsub("BodyBody", "Body", names(meanstd_file))
names(meanstd_file)<-gsub("-mean\\(\\)", "Mean", names(meanstd_file))
names(meanstd_file)<-gsub("-std\\(\\)", "STD", names(meanstd_file))
str(meanstd_file)
#
# Part 5: From the data set in step 4, creates a second, independent tidy data set
#         with the average of each variable for each activity and each subject.
#
TidyData <- meanstd_file %>%
    group_by(subject, activity) %>%
    summarise_all(funs(mean))
str(TidyData)
write.table(TidyData, "TidyData.txt", row.name=FALSE)
