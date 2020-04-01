## Merging data - merge()
## Merges data frames; Important parameters: x,y,by,by.x,by.y,all

x <- trainingset
y <- testset


merge(x, y)

##	Extracts only the measurements on the mean and standard deviation for each measurement. 
mean(x, ...)
mean(x, y)
## Default S3 method:
mean(x, trim = 0, na.rm = FALSE, ...)


summary(x)
summary(y)
sd(x, na.rm = FALSE)
sd(1:2) ^ 2

list(mean(x), sd(x))



From the data set in step 4, I created a second, independent tidy data set
## with the average of each variable for each activity and each subject.

mergedData2 = merge(trainingset,testset,by.x="testset",by.y=" ",all=TRUE)
head(mergedData2) 
mean(mergeData2)
