# Code Book for Getting and Cleaning Course project
##  Student - Author: Hernán Gianini  
  
## 1. Introduction  

The project is based on the input files generated in the experiment "Human Activity Recognition Using Smartphones", developed by the authors: Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio and Luca Oneto, from the Smartlab - Non Linear Complex Systems Laboratory, DITEN - Università degli Studi di Genova.
The following description is taken from the authors definition:  
"The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS,    WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.
For each record it is provided:
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope.
- A 561-feature vector with time and frequency domain variables.
- Its activity label.
- An identifier of the subject who carried out the experiment.

## 2. Transformation proccess and code book
### List of input files

- X_train.txt : Training set.  
- y_train.txt : Training labels (activity labels)
- X_test.txt : Test set.
- y_test.text : Test labels (activity labels)
- subject_train.txt : train subject code
- subject_test.txt : test subject code
  
### Variables description of input files

- subject_train.txt and subject_test.txt (no header files):  
	subject: code assigned to each participant in the experiment (from 1 to 30)  
	  
- y_train.txt and y_test.txt (no header files):  
	activity: experiment activity code (from 1 to 6):  
		1 : WALKING  
		2 : WALKING_UPSTAIRS  
		3 : WALKING_DOWNSTAIRS  
		4 : SITTING  
		5 : STANDING  
		6 : LAYING  
  
- X_train and X_test: 561 measurement (variable colums) for each subject/activity pair (real number):  

### Data transformation proccess description for a tidy data set generation result
  
The following consecutive steps are applied to the input data to generate the final tidy data setfile  
(the corresponding R code is delivered in the run_analysis.R file in this same repository):  
  
a) Merges the training and the test sets to create one data set  
>	i) Get the project data (this is not the R code, it is conceptual pseudo-language):  
>   		- subject_train <- "subject_train.txt"  
>		- subject_test  <- "subject_test.txt"  
>		- activity_train <- "Y_train.txt"  
>		- activity_test <- "Y_test.txt"  
>		- features_test  <- "X_test.txt"  
>		- features_train  <- "X_train.txt"  
>	ii) Merge the test and train files:  
>		- Concatenate the train and test subject, activity and features files by row  
>		- Set names to columns (variables)  
>		- Combine the three resulting files by column to conform one data file (denominated "alldata")  
b) Extracts only the measurements on the mean and standard deviation for each subject/activity pair  
c) Uses descriptive activity names to name the activities in the data set  
d) Appropriately labels the data set with descriptive variable names  
e) creates a second, independent tidy data set with the average of each variable for each activity and each subject  
  		
### Descriptión of Tidy Data Set generated
  
File name: "TidyData.txt"  
   
Variables description:
1	subject
2	activity
3	TimeBodyAccelerometerMean-X
4	TimeBodyAccelerometerMean-Y
5	TimeBodyAccelerometerMean-Z
6	TimeBodyAccelerometerSTD-X
7	TimeBodyAccelerometerSTD-Y
8	TimeBodyAccelerometerSTD-Z
9	TimeGravityAccelerometerMean-X
10	TimeGravityAccelerometerMean-Y
11	TimeGravityAccelerometerMean-Z
12	TimeGravityAccelerometerSTD-X
13	TimeGravityAccelerometerSTD-Y
14	TimeGravityAccelerometerSTD-Z
15	TimeBodyAccelerometerJerkMean-X
16	TimeBodyAccelerometerJerkMean-Y
17	TimeBodyAccelerometerJerkMean-Z
18	TimeBodyAccelerometerJerkSTD-X
19	TimeBodyAccelerometerJerkSTD-Y
20	TimeBodyAccelerometerJerkSTD-Z
21	TimeBodyGyroscopeMean-X
22	TimeBodyGyroscopeMean-Y
23	TimeBodyGyroscopeMean-Z
24	TimeBodyGyroscopeSTD-X
25	TimeBodyGyroscopeSTD-Y
26	TimeBodyGyroscopeSTD-Z
27	TimeBodyGyroscopeJerkMean-X
28	TimeBodyGyroscopeJerkMean-Y
29	TimeBodyGyroscopeJerkMean-Z
30	TimeBodyGyroscopeJerkSTD-X
31	TimeBodyGyroscopeJerkSTD-Y
32	TimeBodyGyroscopeJerkSTD-Z
33	TimeBodyAccelerometerMagnitudeMean
34	TimeBodyAccelerometerMagnitudeSTD
35	TimeGravityAccelerometerMagnitudeMean
36	TimeGravityAccelerometerMagnitudeSTD
37	TimeBodyAccelerometerJerkMagnitudeMean
38	TimeBodyAccelerometerJerkMagnitudeSTD
39	TimeBodyGyroscopeMagnitudeMean
40	TimeBodyGyroscopeMagnitudeSTD
41	TimeBodyGyroscopeJerkMagnitudeMean
42	TimeBodyGyroscopeJerkMagnitudeSTD
43	FrequencyBodyAccelerometerMean-X
44	FrequencyBodyAccelerometerMean-Y
45	FrequencyBodyAccelerometerMean-Z
46	FrequencyBodyAccelerometerSTD-X
47	FrequencyBodyAccelerometerSTD-Y
48	FrequencyBodyAccelerometerSTD-Z
49	FrequencyBodyAccelerometerJerkMean-X
50	FrequencyBodyAccelerometerJerkMean-Y
51	FrequencyBodyAccelerometerJerkMean-Z
52	FrequencyBodyAccelerometerJerkSTD-X
53	FrequencyBodyAccelerometerJerkSTD-Y
54	FrequencyBodyAccelerometerJerkSTD-Z
55	FrequencyBodyGyroscopeMean-X
56	FrequencyBodyGyroscopeMean-Y
57	FrequencyBodyGyroscopeMean-Z
58	FrequencyBodyGyroscopeSTD-X
59	FrequencyBodyGyroscopeSTD-Y
60	FrequencyBodyGyroscopeSTD-Z
61	FrequencyBodyAccelerometerMagnitudeMean
62	FrequencyBodyAccelerometerMagnitudeSTD
63	FrequencyBodyAccelerometerJerkMagnitudeMean
64	FrequencyBodyAccelerometerJerkMagnitudeSTD
65	FrequencyBodyGyroscopeMagnitudeMean
66	FrequencyBodyGyroscopeMagnitudeSTD
67	FrequencyBodyGyroscopeJerkMagnitudeMean
68	FrequencyBodyGyroscopeJerkMagnitudeSTD
