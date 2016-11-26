The variables used are determined by the nature of the experiment. We have subjects, activities and measurements derived from the activities. 

Thus we define the main variables to be "subject", "activity", "activity_id", and the measurements involving time and frequency variabes. 

The variables "subject" and "activity" are defined as column headings, as they are implicit in the orginal data. 

The original activity measurement variables have names defined in the original codebook, and are contained in the file "features", beginning 

1 tBodyAcc-mean()-X
2 tBodyAcc-mean()-Y
3 tBodyAcc-mean()-Z
4 tBodyAcc-std()-X
5 tBodyAcc-std()-Y
6 tBodyAcc-std()-Z
7 tBodyAcc-mad()-X
8 tBodyAcc-mad()-Y
9 tBodyAcc-mad()-Z
10 tBodyAcc-max()-X
11 tBodyAcc-max()-Y
12 tBodyAcc-max()-Z
13 tBodyAcc-min()-X
14 tBodyAcc-min()-Y
15 tBodyAcc-min()-Z
16 tBodyAcc-sma()
17 tBodyAcc-energy()-X
18 tBodyAcc-energy()-Y
19 tBodyAcc-energy()-Z
20 tBodyAcc-iqr()-X
21 tBodyAcc-iqr()-Y
22 tBodyAcc-iqr()-Z
23 tBodyAcc-entropy()-X
24 tBodyAcc-entropy()-Y
25 tBodyAcc-entropy()-Z etc

From this, we extract all that contain the expression "mean" or "std" to arrive at the following (apart from "subject" and "activity"), which we then 'clean' according to the rules set out below.

 [1] "subject"                              "activity"                            
 [3] "tBodyAcc.mean...X"                    "tBodyAcc.mean...Y"                   
 [5] "tBodyAcc.mean...Z"                    "tBodyAcc.std...X"                    
 [7] "tBodyAcc.std...Y"                     "tBodyAcc.std...Z"                    
 [9] "tGravityAcc.mean...X"                 "tGravityAcc.mean...Y"                
[11] "tGravityAcc.mean...Z"                 "tGravityAcc.std...X"                 
[13] "tGravityAcc.std...Y"                  "tGravityAcc.std...Z"                 
[15] "tBodyAccJerk.mean...X"                "tBodyAccJerk.mean...Y"               
[17] "tBodyAccJerk.mean...Z"                "tBodyAccJerk.std...X"                
[19] "tBodyAccJerk.std...Y"                 "tBodyAccJerk.std...Z"                
[21] "tBodyGyro.mean...X"                   "tBodyGyro.mean...Y"                  
[23] "tBodyGyro.mean...Z"                   "tBodyGyro.std...X"                   
[25] "tBodyGyro.std...Y"                    "tBodyGyro.std...Z"                   
[27] "tBodyGyroJerk.mean...X"               "tBodyGyroJerk.mean...Y"              
[29] "tBodyGyroJerk.mean...Z"               "tBodyGyroJerk.std...X"               
[31] "tBodyGyroJerk.std...Y"                "tBodyGyroJerk.std...Z"               
[33] "tBodyAccMag.mean.."                   "tBodyAccMag.std.."                   
[35] "tGravityAccMag.mean.."                "tGravityAccMag.std.."                
[37] "tBodyAccJerkMag.mean.."               "tBodyAccJerkMag.std.."               
[39] "tBodyGyroMag.mean.."                  "tBodyGyroMag.std.."                  
[41] "tBodyGyroJerkMag.mean.."              "tBodyGyroJerkMag.std.."              
[43] "fBodyAcc.mean...X"                    "fBodyAcc.mean...Y"                   
[45] "fBodyAcc.mean...Z"                    "fBodyAcc.std...X"                    
[47] "fBodyAcc.std...Y"                     "fBodyAcc.std...Z"                    
[49] "fBodyAcc.meanFreq...X"                "fBodyAcc.meanFreq...Y"               
[51] "fBodyAcc.meanFreq...Z"                "fBodyAccJerk.mean...X"               
[53] "fBodyAccJerk.mean...Y"                "fBodyAccJerk.mean...Z"               
[55] "fBodyAccJerk.std...X"                 "fBodyAccJerk.std...Y"                
[57] "fBodyAccJerk.std...Z"                 "fBodyAccJerk.meanFreq...X"           
[59] "fBodyAccJerk.meanFreq...Y"            "fBodyAccJerk.meanFreq...Z"           
[61] "fBodyGyro.mean...X"                   "fBodyGyro.mean...Y"                  
[63] "fBodyGyro.mean...Z"                   "fBodyGyro.std...X"                   
[65] "fBodyGyro.std...Y"                    "fBodyGyro.std...Z"                   
[67] "fBodyGyro.meanFreq...X"               "fBodyGyro.meanFreq...Y"              
[69] "fBodyGyro.meanFreq...Z"               "fBodyAccMag.mean.."                  
[71] "fBodyAccMag.std.."                    "fBodyAccMag.meanFreq.."              
[73] "fBodyBodyAccJerkMag.mean.."           "fBodyBodyAccJerkMag.std.."           
[75] "fBodyBodyAccJerkMag.meanFreq.."       "fBodyBodyGyroMag.mean.."             
[77] "fBodyBodyGyroMag.std.."               "fBodyBodyGyroMag.meanFreq.."         
[79] "fBodyBodyGyroJerkMag.mean.."          "fBodyBodyGyroJerkMag.std.."          
[81] "fBodyBodyGyroJerkMag.meanFreq.."      "angle.tBodyAccMean.gravity."         
[83] "angle.tBodyAccJerkMean..gravityMean." "angle.tBodyGyroMean.gravityMean."    
[85] "angle.tBodyGyroJerkMean.gravityMean." "angle.X.gravityMean."                
[87] "angle.Y.gravityMean."                 "angle.Z.gravityMean."   

The processing of these variable names consists of 

1. Removing any "_"
2. Removing any "."
3. Changing lower case "mean" to "Mean"
4. Changing lower case "std" to "StdDev"
5. Replacing a "t" at the beginning of a word to "time"
6. Replacing a "f" at the beginning of a word to "freq", short for "frequency"
7. Replacing any occurrence of "BodyBody" by "Body".
8. Replacing any non-initial occurence of "tBody" by "Body"

This then gives us the following 'cleaned' variable names.

 [1] "subject"                          "activity"                        
 [3] "timeBodyAccMeanX"                 "timeBodyAccMeanY"                
 [5] "timeBodyAccMeanZ"                 "timeBodyAccStdDevX"              
 [7] "timeBodyAccStdDevY"               "timeBodyAccStdDevZ"              
 [9] "timeGravityAccMeanX"              "timeGravityAccMeanY"             
[11] "timeGravityAccMeanZ"              "timeGravityAccStdDevX"           
[13] "timeGravityAccStdDevY"            "timeGravityAccStdDevZ"           
[15] "timeBodyAccJerkMeanX"             "timeBodyAccJerkMeanY"            
[17] "timeBodyAccJerkMeanZ"             "timeBodyAccJerkStdDevX"          
[19] "timeBodyAccJerkStdDevY"           "timeBodyAccJerkStdDevZ"          
[21] "timeBodyGyroMeanX"                "timeBodyGyroMeanY"               
[23] "timeBodyGyroMeanZ"                "timeBodyGyroStdDevX"             
[25] "timeBodyGyroStdDevY"              "timeBodyGyroStdDevZ"             
[27] "timeBodyGyroJerkMeanX"            "timeBodyGyroJerkMeanY"           
[29] "timeBodyGyroJerkMeanZ"            "timeBodyGyroJerkStdDevX"         
[31] "timeBodyGyroJerkStdDevY"          "timeBodyGyroJerkStdDevZ"         
[33] "timeBodyAccMagMean"               "timeBodyAccMagStdDev"            
[35] "timeGravityAccMagMean"            "timeGravityAccMagStdDev"         
[37] "timeBodyAccJerkMagMean"           "timeBodyAccJerkMagStdDev"        
[39] "timeBodyGyroMagMean"              "timeBodyGyroMagStdDev"           
[41] "timeBodyGyroJerkMagMean"          "timeBodyGyroJerkMagStdDev"       
[43] "freqBodyAccMeanX"                 "freqBodyAccMeanY"                
[45] "freqBodyAccMeanZ"                 "freqBodyAccStdDevX"              
[47] "freqBodyAccStdDevY"               "freqBodyAccStdDevZ"              
[49] "freqBodyAccMeanFreqX"             "freqBodyAccMeanFreqY"            
[51] "freqBodyAccMeanFreqZ"             "freqBodyAccJerkMeanX"            
[53] "freqBodyAccJerkMeanY"             "freqBodyAccJerkMeanZ"            
[55] "freqBodyAccJerkStdDevX"           "freqBodyAccJerkStdDevY"          
[57] "freqBodyAccJerkStdDevZ"           "freqBodyAccJerkMeanFreqX"        
[59] "freqBodyAccJerkMeanFreqY"         "freqBodyAccJerkMeanFreqZ"        
[61] "freqBodyGyroMeanX"                "freqBodyGyroMeanY"               
[63] "freqBodyGyroMeanZ"                "freqBodyGyroStdDevX"             
[65] "freqBodyGyroStdDevY"              "freqBodyGyroStdDevZ"             
[67] "freqBodyGyroMeanFreqX"            "freqBodyGyroMeanFreqY"           
[69] "freqBodyGyroMeanFreqZ"            "freqBodyAccMagMean"              
[71] "freqBodyAccMagStdDev"             "freqBodyAccMagMeanFreq"          
[73] "freqBodyAccJerkMagMean"           "freqBodyAccJerkMagStdDev"        
[75] "freqBodyAccJerkMagMeanFreq"       "freqBodyGyroMagMean"             
[77] "freqBodyGyroMagStdDev"            "freqBodyGyroMagMeanFreq"         
[79] "freqBodyGyroJerkMagMean"          "freqBodyGyroJerkMagStdDev"       
[81] "freqBodyGyroJerkMagMeanFreq"      "angleBodyAccMeangravity"         
[83] "angleBodyAccJerkMeangravityMean"  "angleBodyGyroMeangravityMean"    
[85] "angleBodyGyroJerkMeangravityMean" "angleXgravityMean"               
[87] "angleYgravityMean"                "angleZgravityMean" 