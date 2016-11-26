# Tidy
Getting and Cleaning Data: Peer-graded assignment

# R script to produce a tidy data set for accelerometer readings

**Install necessary packages**
```
install.packages("dplyr")
library(dplyr)
```

# Set the working directory
```
setwd("C:/Users/Paul/Desktop/Coursera/UCI HAR Dataset")
```

**Read in the activity data for the test subjects**
```
test_activity <-read.table("./test/y_test.txt",header=FALSE)
```
**Read in the activity data for the training subjects**
```
train_activity <-read.table("./train/y_train.txt",header=FALSE)
```
**ASSIGNMENT 1: Merge these files into one activity files**
```
activity <- rbind(test_activity, train_activity)
```
**Assign a column name** 
``
colnames(activity) <- c("activityid")
```
**Read in test subject data**
```
test_subject <-read.table("./test/subject_test.txt",header=FALSE)
```
**and training subject data**
```
train_subject <-read.table("./train/subject_train.txt", header=FALSE)
```
**and merge these two files   ASSIGNMENT 1**
```
subject<-rbind(test_subject, train_subject)
```
**and assign a column heading**
```
colnames(subject)<-c("subject")
```
**We now read in the features data, starting with the feature labels**
```
f_labels<-read.table("features.txt", header=FALSE, sep=" ")
```
**and adding suitable column headings** 
```
colnames(f_labels)<-c("featureid", "featurename")
```
**We read in the feature data for the test group**
```
test_features <-read.table("./test/X_test.txt",header=FALSE)
```
**and the training group**
```
train_features <-read.table("./train/X_train.txt",header=FALSE)
```
**and we merge these two files**
```
features<-rbind(test_features, train_features)
```
**and we give appropriate column headings to the features data**
```
colnames(features)<-make.names(f_labels$featurename, unique=TRUE)
```
**We now read in the activity labels and assign suitable column headings**
```
activity_labels<-read.table("activity_labels.txt", header=FALSE, sep=" ")
colnames(activity_labels)<-c("activityid", "activity")
```
**We now combine the subject, activity and features data**
```
subject_activity_features <-cbind(subject, activity, features)
```
**Now select out the columns only with mean or standard deviation in the features**
**ASSIGNMENT 2**
```
data_mean_std <- select(subject_activity_features, matches("subject|activityid|mean|std"))
```
**Complete the data file of means and standard deviations by including the activity labels**
```
data_mean_std<-merge(x=data_mean_std, y=activity_labels, by="activityid")
```
**Remove the now redundant activityid column to keep the data tidy**
```
data_mean_std<-select(data_mean_std, -activityid)
```
**Reorder the columns, as the activity has been made last of 89 columns by the merge**
```
data_mean_std<-select(data_mean_std, subject, activity, 2:87)
```
**As a first step to tidy the data, we will look at the column names**
```
colnames <- colnames(data_mean_std)
colnames <- make.names(colnames, unique=TRUE)
```
**Now use regualar expression operators to clean up the names**
**ASSIGNMENT 3**
```
colnames <- make.names(colnames, unique=TRUE)
colnames_temp <- gsub("_","",colnames)
colnames_temp <- gsub("\\.","",colnames_temp)
colnames_temp <- gsub("\\ ","",colnames_temp)
colnames_temp <- gsub("mean", "Mean", colnames_temp)
colnames_temp <- gsub("std", "StdDev", colnames_temp)
colnames_temp <- gsub("^(t)", "time", colnames_temp)
colnames_temp <- gsub("^(f)", "freq", colnames_temp)
colnames_temp <- gsub("BodyBody","Body", colnames_temp)
colnames_temp <- gsub("tBody", "Body", colnames_temp)
colnames_temp <- gsub("^\\s+|\\s+$","",colnames_temp)
```
**and restore the column heading names to their clean versions**
**ASSIGNMENT 4**
```
colnames(data_mean_std)<-colnames_temp
```
**Ensure the column names are now unique**
``
colnames(data_mean_std)<-make.names(colnames(data_mean_std), unique=TRUE)
```
**and produce first "tidy" table** 
```
tidy_mean_std <- tbl_df(data_mean_std)
```
**Note that we could make "subject" more verbose for readability with**
*tidy$subject<-paste0("subject_",tidy$subject)*
**Now sort on subject**
```
tidy_mean_std <-arrange(tidy_mean_std, subject)
```
**Output the tidy_mean_std data to the working directory**
```
save(tidy_mean_std, file="tidy.rda")
```
**We now produce an independent tidy data set with the average of each variable for each activity and each subject** 
**ASSIGNMENT 5**
```
tidy_grouped <-group_by(tidy_mean_std, subject, activity)
tidy_mean<-summarise_each(tidy_grouped, funs(mean))
colnames(tidy_mean)<-colnamesclean
```
**save as data file**
```
save(tidy_mean, file="tidy_mean.rda")
```
**save as a tab-delimited text file**
```
write.table(tidy_mean, file="tidy.txt", row.names=FALSE, col.names=TRUE, sep="\t")
```
