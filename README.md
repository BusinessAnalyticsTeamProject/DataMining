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
Our team was launched to solve this situation using **Business Analytics** techniques.

## 😎 Purpose 
![image](https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/9a84dce6-be7a-47cc-8a37-71e7ed831954)
### 1. Predict the probability that an applicant will be Passed/Failed
### 2. Identify important factors that affect the final selection results of trainees
### 3. Compare the selection criteria of 42 Seoul and Ecole 42 to identify the differences in selection factors

  
## 📚 Data Collection
### Overall Collecting Process
<img src = "https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/746067b3-c5ca-4ded-afdb-921510f0a43b"/>

### 1. User Raw Data: API
<img width="497" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/f9f06468-4366-4639-b437-1fae2b5088f8">
<br>
By calling /v2/campus/:/campus_id/users, we could separately collect raw data for all users of Seoul 42 Campus and Ecole 42 Campus, and the campus_ids for each are 29 and 1.

<img width="502" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/edc8c355-4c62-44be-8c33-f641b188d40e">
<br>
This is what user raw data looks like.

### 2. Feedback and Evaluation Data: API with Python Code for Processing
<img width="524" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/d5e704a7-a048-4adf-b334-618766aa9c7a">
<br>
By calling /v2/users/:user_id/scale_teams/as_corrector and /v2/users/:user_id/scale_teams/as_corrected, we were able to obtain data in json format with items for events in which a user participated as a correcter and correction recipient.
<img width="1231" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/43896369-4652-49b2-ac09-6cbf052d7be5">
<br>
This is the sample data structure of as_corrected data. By counting item named with corrcected, we've figured out how many evaluations they gave (corrector) and feedback they received(corrected).
<br>

### 3. Level​, Group Assignments​, Penalty​, Highest La-picsine​, Final Exam Score: Crawling with Python Code
<img width="735" alt="image" src="https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/45c6d1da-eaeb-4f2e-b178-b395ca3d9b94">
In 42 School, each user has their own personal page. From there, we could retrieve statistical information about users. So, data is collected through crawling by accessing each user's page.
Level​: Overall progress that can be made through assignments, and midterm exams
Group Assignments: Optional group assignments
Penalty​
Highest La-picsine​
Final Exam Score




## 🛣 EDA
### 1.Pie Chart for PASS/FAIL ratio
<p  align="center">
<img src = "https://github.com/BusinessAnalyticsTeamProject/DataMining/assets/111236793/234bb13b-a287-4914-915c-21b80849eda0"/>
</p>
This data set is a data set after removing all data points with a Final Exam score of less than 42 points. It can be seen that even if the Final Exam score is 42 points or more, there are many people who fail the final selection, and the ratio is almost equal to the number of people in the PASS.


## 💻 Main Data Mining Process
<p  align="center">
<img width = "250px" height = "500px" src="https://user-images.githubusercontent.com/76484900/227690312-6296bc19-ab94-418b-ac83-76dc9fdfb836.png"/>
<img width = "250px" height = "500px" src="https://user-images.githubusercontent.com/76484900/227690317-f8f6294e-3d75-4ba4-8a95-1464a2609397.png"/>
<img width = "250px" height = "500px" src="https://user-images.githubusercontent.com/76484900/227690318-78d17535-1bae-4940-bb0f-5b8bda74ab26.png"/>
</p>


##  🚏 Conclusion
Beyond self-study proctoring, we will collaborate with other large-scale education platforms to provide learning content. As a result, more users will be attracted, and more efficient and effective learning will be achieved through our project's technology.

We are also deploying the service using AWS EC2 cloud service. Therefore, scaling up based on the size of users can be easily performed and expansion can be prepared by dynamically increasing servers according to demand.



 

## ⚙️Tech Stack


### 🚏 `Server - APP(BE)`

|service|version|
|--|--|
|**NodeJS**|v16.x|
|**EXPRESS**|v4.x|
|**REDIS**|v3.0.x|
|**MySQL**|5.7.x|

  

### 📱 `FE - APP`

|service|version|
|--|--|
|**Android Studio**|v4.2|
|**Figma**|web_service|
|**webRTC**|open-source|

  

### 💻 `ML - embedded`

|service|version|
|--|--|
|**python**|v3.11.2|
|**Yolov5**|v5|

  


## 👪 Team Information

- Jeongmin Oh(@gmail.com), Github Id: lopahn2 
- Kangmin Kim (rkdals0203@gmail.com), Github Id: rkdals0203 
- Aleksandra Kaniewska (@gmail.com), Github Id: alekann009 
- Eonseon Park (eonpark@gmail.com), Github Id: eonpark 
