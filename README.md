<p  align="center">
<img  width="900px"  height = "300px"  src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/28eea43e-5f03-41df-b5cc-524d7f1f947a"/>
</p>

 <p  align="center"><b>Business Analytics Team Project in ITM Major</b></p>

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
### 1.Pair Plot
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/94adcace-0c62-4a74-ae59-f728e020da12">
</p>
<br>
This data set is a data set after removing all data points with a Final Exam score of less than 42 points. It can be seen that even if the Final Exam score is 42 points or more, there are many people who fail the final selection, and the ratio is almost equal to the number of people in the PASS.

### 2.Statistics
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/b095b45c-75ae-4ecb-a13e-216589cb381a">
</p>

### 3.Box Plot
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/e0485e5c-93c8-498a-a3f0-4ff52a19751c">
</p>
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/fa608dac-a68f-4c63-b37e-4690e2aa4d57">
</p>
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/b813653b-1231-45e7-9c58-525df685960b">
</p>

### 4.Correlation Matrix
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/1755d261-1bcd-47a3-8864-f592b6b5e03a">
</p>

### 5.Pie Chart for PASS/FAIL Distribution
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/1be48b99-bda0-42ba-98f3-328b0a105b8e">
</p>

### 6.Bar Chart for distribution of other variables
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/173c1c81-a74a-4fed-9649-a78cbc64290e">
</p>
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/aab669c8-a0ee-4b2d-a589-f50fbf0dd730">
</p>
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/4abe355c-1478-4598-ad1b-7b3bf0a8ef55">
</p>

### 7.Bubble Chart for Peer Reviews and Result of the Exam
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/eb716d32-bfbe-4176-b7a0-2e9e52178489">
</p>

### 8. C Piscine Levels and Scaled Passed Ratio
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/78c03afd-8729-4c09-b47e-fed896f89d52">
</p>

## 💻 Main Data Mining Process
### Pipelining
<p align="center">
<img src ="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/be1b7aaf-c802-40c6-a4ce-26a031e0024f">
</p>


##  🚏 Post-Processing
### Feature Importance
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/cf814448-cd9b-4e3d-b951-f3700b78fcc6)
### ROC Curve
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/f4d58721-7c11-42ea-ba14-3d87c192797f)
### Confusion Matrix
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/3f555bd2-51a3-4324-b35b-ce1dcc52eee8)

### Conclusion
In conclusion, The original name of our project was 'what is important'. We thought there must be a reason why 42 Academy emphasizes the importance of the learning process and peer learning to la-piscine students over the results of the problem. Therefore, we believed that there would be elements more important than the scores of assignments and exams in this test. The outcome of the project indicates that the importance of peer evaluation is more significant than anything else. Through this project, we were able to quantitatively prove that enjoying knowledge through mutual learning and teaching, rather than the amount of individual study, is the core value that 42 Academy emphasizes.​

More importantly, by comparing and analyzing data from 42 distributed and global schools, we were able to recognize data differences and prioritize important factors through modeling.​ This will not only guide a participant to learn in the right direction by recognizing his or her passing probability, but will also be an important tool for quality assurance for the 42 School management.​
​
### Shortcomings
In the data extraction part, it was disappointing that we couldn’t extract data from other campuses due to the long duration of crawling. We also regretted not being able to extract detailed data like campus popularity polls. Additionally, unlike in Korea, France was passing a considerably larger number of participants. Therefore, despite sampling, the data imbalance made it difficult to find a well-performing model.


## 👪 Team Information

- Jeongmin Oh(jeongmino1207@gmail.com), Github Id: jeongmino 
- Kangmin Kim (rkdals0203@gmail.com), Github Id: rkdals0203 
- Aleksandra Kaniewska (@gmail.com), Github Id: alekann009 
- Eonseon Park (eonpark@gmail.com), Github Id: eonpark 
