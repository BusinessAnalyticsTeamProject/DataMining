## 📄 Background
### 1. Increasing competition rate​ & Unclear passing criteria
 
<p  align="center">
<img src = "https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/d09c150a-2b0e-479c-8486-b5ee902e987c">
</p>
<br>
42 School is rapidly gaining global recognition as a prestigious educational institution, particularly in Korea, where the competition rate is an astonishing 44 to 1. 
However, a significant challenge arises during the month-long testing period, as the nature of crucial activities remains shrouded in secrecy, posing a concern for prospective students and their preparation strategies.​
<br>

### 2. Globalized Campus of 42 school
<p  align="center">
<img src = "https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/0b359730-dcf7-4c31-9c64-af0634b30af0">
</p>
<br>
There are 50 number of 42 campus and this education system is originated from 42 Ecole, which is the first campus of 42 school.
42 As schools become increasingly global, cracks will inevitably appear in their operating policies and educational standards.​
It is unclear whether the students at 42 School are being evaluated according to the standards of 42 Ecole, which has originality.​
Our team was launched to solve this situation using Business Analytics techniques.

## 😎 Purpose 
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/9a84dce6-be7a-47cc-8a37-71e7ed831954)
### 1. Build a model that can predict the probability that an applicant will be Passed/Failed
### 2. Identify important factors that affect the final selection results of participants
### 3. Compare the selection criteria of 42 Seoul and Ecole 42 to identify the differences in educational priority and operating policies

  
## 📚 Data Collection
### Overall Collecting Process
<img src = "https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/746067b3-c5ca-4ded-afdb-921510f0a43b"/> <br>
We completed the data collection process by following these five steps. We created raw data through API calling, merged the crawled data, and deleted unnecessary columns.


### 1. User Raw Data: API
<img width="497" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/f9f06468-4366-4639-b437-1fae2b5088f8"><br>
By calling /v2/campus/:/campus_id/users, we could separately collect raw data for all users of Seoul 42 Campus and Ecole 42 Campus, and the campus_ids for each are 29 and 1.

<img width="502" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/edc8c355-4c62-44be-8c33-f641b188d40e"><br>
To get the raw data, we found the campus IDs of the Seoul and Ecole campuses and retrieved the data through API requests. This is what user raw data looks like.

### 2. Feedback and Evaluation Data: API with Python Code for Processing
<img width="524" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/d5e704a7-a048-4adf-b334-618766aa9c7a"> <br>
By calling /v2/users/:user_id/scale_teams/as_corrector and /v2/users/:user_id/scale_teams/as_corrected, we were able to obtain data in json format with items for events in which a user participated as a correcter and correction recipient.
After calling /v2/users/:user_id/scale_teams/as_corrector and as corrected to add the feedback received by one user and the feedback given by that user to another user as independent variables, the number of items is calculated from each response json format. By counting, we were able to extract data.
<img width="1231" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/43896369-4652-49b2-ac09-6cbf052d7be5"> <br>
This is the sample data structure of as_corrected data. By counting item named with corrcected, we've figured out how many evaluations they gave (corrector) and feedback they received(corrected).
<br>

### 3. Level​, Group Assignments​, Penalty​, Highest La-picsine​, Final Exam Score: Crawling with Python Code
<img width="735" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/45c6d1da-eaeb-4f2e-b178-b395ca3d9b94"> <br>
In 42 School, each user has their own personal page. From there, we could retrieve statistical information about users. So, data is collected through crawling by accessing each user's page. <br>
Level​: Overall progress that can be made through assignments, and midterm exams <br>
Group Assignments: Optional group assignments <br>
Penalty​: How many times cheated; each time a user get caught, 42 points will be deducted from assignment score <br>
Highest C-picsine​: In assignments using the C language, the highest level of assignment completed (0~13) <br>
Final Exam Score: as it is.<br>

### 4. Merge all of files from API and crawled file.
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/0a41f4d3-2e87-40f8-b6cd-2a4c793c92af)
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/051d35b9-3830-4713-950d-a1f76ecc3260)
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/9e1e1d6e-9a56-4221-900c-825dcb24d83a)
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/1aac28a6-35d4-4c11-ab5e-f98f908ad9dc)
<br>
Files created through API calls and crawling include CSV files and a plain text file recording assignments and exam scores. From the plain text file, I extracted the Highest C Piscine, Final Exam Score, and the Number of Group Assignments. I then summed these scores and divided them by a certain value to derive a level that closely resembles the actual level, and created a CSV file from this data.
Subsequently, we performed an inner join on each CSV file using the 'id' and 'login' information. All dummy data was filtered out based on the level and generation.
This is how the final data  looks like. Since the participants whose score is under 42 will automatically be failed, we could know almost ¼ student could not be passed in final exam.

## 🛣 EDA
### 1. Pair plot
#### 42Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/pairplot.png">
</p>
<br>
This data set is a data set after removing all data points with a Final Exam score of less than 42 points. It can be seen that even if the Final Exam score is 42 points or more, there are many people who fail the final selection, and the ratio is almost equal to the number of people in the PASS.

### In 42Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/de4226ce-61e4-435f-aa25-f077a1ef38e4)


### 2.Statistics
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/statistics.png">
</p>

#### 42Ecole
<img width="792" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/3892748b-7b76-452e-8ea6-7ccf40638038">


### 3.Box Plot
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/boxplots%201.png">
</p>
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulboxplot%202.png">
</p>
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulboxplot%203.png">
</p>

#### 42Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/ac370ec3-e830-455d-883f-73f1cedca1b9)



### 4.Correlation Matrix
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/correlationmatrix.png">
</p>

#### 42 Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/85436d3c-1ddc-458d-b511-4c8fa07a8ad8)


### 5.Pie Chart for PASS/FAIL Distribution
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulpiechart.png">
</p>

#### 42 Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/b887ae0b-9f23-4b4c-8c66-b1a42465c94c)


### 6.Bar Chart for distribution of other variables
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulbarchat1.png">
</p>
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulbarchart2.png">
</p>
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoulbarchart3.png">
</p>

#### 42 Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/01c2246c-5b4c-4b39-937b-b9ba17ae9902)


### 7.Bubble Chart for Peer Reviews and Result of the Exam
#### 42 seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoul%20bubble%20chart.png">
</p>

#### 42 Ecole
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/6558e724-5e4e-4c4e-b4a5-3a28d1b3daa2)


### 8. C Piscine Levels and Scaled Passed Ratio
#### 42 Seoul
<p align="center">
<img src ="https://github.com/alekann009/Business-Analytics-final/blob/main/assets/seoul%20polar%20chart.png">
</p>

#### 42 Ecole 
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/dbed7ac8-cd73-42a3-8a63-fef689ac4f1e)





## 💻 Main Data Mining Process
### Split the data into train set and test set
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/27084d5a-6d59-4920-8945-dd6d2745a648)

### Pipelining in 42Seoul
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/be1b7aaf-c802-40c6-a4ce-26a031e0024f">
</p>

### Pipelining in 42Ecole
<img width="733" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/bbf2fc70-af6e-4e91-8432-7510fe8b5552">


##  🚏 Post-Processing
### Feature Importance
#### in 42Seoul
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/cf814448-cd9b-4e3d-b951-f3700b78fcc6)
#### in 42Ecole

<img width="910" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/ed756698-816a-4e21-8f10-33d5b1328b62">

### ROC Curve
#### In 42Seoul
<img width="427" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/807b9418-3e5d-451d-a7e7-3dec312502b4">

#### In 42Ecole
<img width="460" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/afccbc6a-6469-44c4-9793-3ef9715f8920">


### Confusion Matrix
#### In 42Seoul
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/3f555bd2-51a3-4324-b35b-ce1dcc52eee8)
#### In 42Ecole
<img width="484" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/532f1c99-abab-436a-a79e-a5eb52f4aef1">


#### Accuracy score
<img width="959" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/64fdd946-d2ca-44e7-83dd-78c3302c60d4">

### Is high Accuracy better?
<img width="964" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/65460400/474c31dc-939b-4485-8f8e-46733b19fdf4">


### Conclusion
In conclusion, The original name of our project was 'what is important'. We thought there must be a reason why 42 Academy emphasizes the importance of the learning process and peer learning to la-piscine students over the results of the problem. Therefore, we believed that there would be elements more important than the scores of assignments and exams in this test. The outcome of the project indicates that the importance of peer evaluation is more significant than anything else. Through this project, we were able to quantitatively prove that enjoying knowledge through mutual learning and teaching, rather than the amount of individual study, is the core value that 42 Academy emphasizes.​

More importantly, by comparing and analyzing data from 42 distributed and global schools, we were able to recognize data differences and prioritize important factors through modeling.​
This not only guides a participant to learn in the right direction by recognizing his or her passing probability, but also serves as an important tool for quality assurance for the global 42 School management team.​
By utilizing this model and collecting and analyzing data from more campuses, the likelihood of running a good program that guarantees consistent quality will increase.
​
### Shortcomings
In the data extraction part, it was disappointing that we couldn’t extract data from other campuses due to the long duration of crawling. We also regretted not being able to extract detailed data like campus popularity polls. Additionally, unlike in Korea, France was passing a considerably larger number of participants. Therefore, despite sampling, the data imbalance made it difficult to find a well-performing model.


## 👪 Team Information

- Jeongmin Oh(jeongmino1207@gmail.com), Github Id: jeongmino 
- Kangmin Kim (rkdals0203@gmail.com), Github Id: rkdals0203 
- Aleksandra Kaniewska (@gmail.com), Github Id: alekann009 
- Eonseon Park (pocva6243@gmail.com), Github Id: eonpark 
