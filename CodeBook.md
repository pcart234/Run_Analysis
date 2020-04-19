# Getting and Cleaning Data - Final Project (Week 4)

# call required packages
# Read in the test files for x, subject, and y
# Read in the train files for x, subject, and y
# Read in the activity labels and the features of the columns

subject_test <- read.table("UCI HAR Dataset/test/subject_test.txt",col.names="subject",header=FALSE)
subject_train<- read.table("UCI HAR Dataset/train/subject_train.txt",col.names="subject",header=FALSE)
test_numbers<- read.table("UCI HAR Dataset/test/y_test.txt", col.names="id",header=FALSE)
train_numbers<-read.table("UCI HAR Dataset/train/y_train.txt",col.names="id",header=FALSE)
activities<-read.table("UCI HAR Dataset/activity_labels.txt",col.names=c("id","activity"),header=FALSE)

# 1. Merge the training data and the test sets to create one data set
  # merge xtrain and xtest files (train first, then test) for x, y, and subject
  # Update column names using the features
features <- read.table("UCI HAR Dataset/features.txt")
features[,2] <- as.character(features[,2])
New_train <-read.table(file="UCI HAR Dataset/train/X_train.txt", header=FALSE, col.names=features[,2],colClasses="numeric",stringsAsFactors = FALSE)
New_test <-read.table(file="UCI HAR Dataset/test/X_test.txt", header=FALSE, col.names=features[,2],colClasses="numeric",stringsAsFactors = FALSE)
Test<-rbind(New_test,New_train)
St <- rbind (subject_test, subject_train)
Yt <-rbind(test_numbers,train_numbers)

newdata<-cbind(St,Yt,Test)
colnames(newdata)[2]<-"id"

# 2. Extracts only the measurements on the mean and standard deviation for each measurement

namesfilter<-grep(".*mean.*|.*std.*", features[,2])
namesfilter<-grep("mean|std",names(newdata), ignore.case=TRUE,value=TRUE)

# 3. Uses descriptive activity names to name the activities in the data set

test2<-data.frame(newdata$subject,newdata$id,newdata[,namesfilter])


# 4. Appropriately labels the data with descriptive variable names

test2$newdata.id <- activities[test2$newdata.id, 2]


# 5. From step 4, create a second, independent tidy data set with the average of each 
# variable for each activity and each subject

write.table(test2,"test2.txt",row.name=TRUE)

# Save final tidy data file as a .txt using write.table
test2.txt
