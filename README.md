# University-Student-Financial-Enterprise-Model

## Executive Summary
Every year it is observed that 10 million students fly to foreign countries to pursue their higher studies. The application process starting from choosing a university, loan process and graduating from the university from a good job in hand is a tedious process. There are many applications in the industry that focus on one aspect of students i.e., either on their application process or choosing a financial organization for their education loan or helping a student to find a good job. For example, applications like yocket focus on finding the best university to the student, applications like WemakeScholars help students take education loans from the
best financial organizations and applications like LinkedIn, Glass door helps student land in a good job. But there is no single application that can handle the student data from the application stage to his employment stage. This combined data helps us to draw many insights that are otherwise impossible with single application dealing with only one section of data. The database was modelled considering all the data that the application process, loan process and employment process of a student involves in. The tables were populated based on real time data. EER and UML diagrams were modelled and these conceptual data was mapped to relational model to populate the tables with the data. Primary and Foreign key constraints were stipulated across the relational model and database implementation in MySQL using all the tables were shown. To have an illustration in No SQL database, Neo4j database is queried using Cypher with 8 nodes out of 11 available. The SQL and NoSQL database implementation worked well and was able to fetch data as expected. The database efficiency and working is tested by connecting the database to Python language. Python’s Seaborn library is used to visualize the output of SQL queries. The queries and the Visualization results matched and provided the correct output as expected. As technical expectations of any project has no boundaries and always there is a scope to improve. There are few aspects that we can improve technically to include few more features and provide better suggestions to the students.
## 1. Business Problem Definition and Requirement :
The current data model focuses on gathering data from the students in two different phases of their career. This data helps organizations like banks, NBFC’s to make efficient decisions in disbursing loans to the students of a particular university and also helps students with accurate and proper information about their study in abroad. Therefore, we can consider it as a complex collection of data from different phases that a student passes through in his career right from applying to foreign universities to repaying loans after landing in a job. This model also helps banks to evaluate student profiles based on the university they got admit to and provide with better loan schemes. From the perspective of students this model provides them with a clear view about the financial and academicals planning they need to arrange before they start with their university education. People with similar interests can form groups to co-ordinate on different steps in the process of reaching to a different country. Once the students are aware of the rules and protocols of different academic standards before they start with the academics it allows them to prepare from the university perspective. The data model helps universities to find out the major companies that hire fresh graduates and the major locations that students from the university work in. This database helps universities to build strong connections with the companies that hire frequently and also prepare
curriculums with respective to industry standards. From the perspective of banks, our data model provides them with a statistical evidence on the success rate of different types of loans disbursed to students who wish to continue their studies across different countries  The following are the rules to be followed while implementing the data model.
  1. The Applicant entity has an attribute fee range which has to match with the university fee range while recommending the universities.
  2. One student can apply to different departments under the same university but can be admitted to only department of a university
  3. One student receives loan from one or zero banks while one bank can grant loans to any number of students.
  4. One student as one employer while one employer can employee any number of students.
  5. The employment table here in the model denotes the first job that a student joins after the graduation.
  6. Banks cannot provide loan more than 80% of the value of the collateral property of the student.
  7. The Rate of interest for collateral loans should be less than non – collateral loans in the same bank.
  8. Financial organisation has to grant loans only to students parents having eligible credit score
  9. A university can be in multiple locations and multiple departments. Departments can offer multiple courses. Each course can have multiple students. Each course      has onecourse requirement.
## Design of the database
To create a database for the business we identify the tables as Applicant, University, Department, Course, Student, Financial Organisation, Address, and Employment
Organisation. Each Applicant can apply to ‘n’ universities for ‘n’ courses provided by ‘n’ departments. Student will accept admission from only one university. Financial Organizations can provide loan to ‘n’ students based on the Credit score and collateral value of the student. Student works in the organization after their graduation. The Repayment of loans by the students is calculated once they start earning at the respective organization. One organization can employee ‘n’ students from the university while one student can be employed by ‘one’ organization. The address of the financial organizations, Company University and students are recorded so that universities can better predict the locations from which geographical locations students majorly come from and where they land in jobs after the graduation. We have used Navicat, Excel and Gitmind for developing data model for the business case

## 2. Entity Relationship Diagram (ER model)
The EER diagram for the model
![image](https://user-images.githubusercontent.com/84727716/173187270-7986a95f-df03-4456-91da-319d9655d085.png)

Unified Modelling Language (UML) Class diagram The UML Class diagram for the data model is shown below.
![image](https://user-images.githubusercontent.com/84727716/173187285-6a846676-f118-4409-b7bb-d05fd3711968.png)

Relational Model (All Primary keys are underlined and are NOT NULL. All the Foreign keys are NOT NULL) 

ApplicantScore (User_ID, UnderGrad CGPA, Higher Education, Secondary Education,
TOEFL/IELTS, GRE Score) User_ID is primary key and is NOT NULL

Applicant (User_ID, last name, First name, Fee Range, Address_ID)
User_ID is the primary key and is NOT NULL
Address_ID is the foreign key refers to Address table

Address (Address_ID, Address Line 1, City, State, country, Phone Number)
Address_ID is the primary key and is NOT NULL

Application (Applicant_ID, University_ID, Course_ID, User_ID)
Applicant_ID is the primary key and is NOT NULL
University_ID is the foreign key refers to University Table
Course_ID is the foreign key refers to Course table
User_ID is the foreign key refers to Applicant Table

University (University_ID, University Name, Department_ID, Address_ID)
University_ID is the primary key and is NOT NULL
Department_ID is the foreign key refers to Department table
Address ID is the foreign key refers to Address table

Department (Department ID, Department Name, Course_ID)
Course_ID is the foreign key refers to course table

Course (Course ID, Course Name, Course_Req_ID, Fees)
Course_Req_ID is the foreign key refers to Course_Req table

Course_Req (Course_Req_ID, UnderGrad CGPA, Higher Education, Secondary Education,
TOEFL/IELTS, GRE Score)
Course_Req_ID is the primary key and is NOT NULL

Financial Organization( Loan_ID, Rate of Interest, Amount, Years of Repayment, Loan
Closing Date, Applicant Credit Score, Loan Starting Date, Branch Code, Address_ID,
Collateral Value, Loan Type)
Address_ID is the foreign key and is NOT NULL

Student (Student_ID, Applicant_ID, Loan_ID, LinkedIn)
Applicant_ID is the foreign key refers to Application Table
Loan_ID is the foreign key refers to financial organization

Employment (Employee_ID, Student_ID, Organisation_Name, Role, Address_ID, Salary
Range)
StudentID is the foreign key refers to Student table and is NOT NULL
Address_ID is the foreign key refers to Address table and is NOT NULL

![image](https://user-images.githubusercontent.com/84727716/173187357-005acc30-4861-4dfe-bc55-9a35a3b77a7c.png)

## 3. Implementation of Relational Model Using MySQL
MySQL Connection
Query1: Count of Students who applied for different courses
This Result helps to find out the preference of students to different majors
Select Course_name,count(*) 'C' from application A join Course C on A.Course_ID =
C.Course_ID group by Course_name order by C DESC limit 10

![image](https://user-images.githubusercontent.com/84727716/173187361-694960ae-df7f-485c-a2f0-6290c5f82537.png)

Query2: Cities of Financial Organizations that offered highest number of loans
This result helps us to find out the bank branches that give preference to educational
loans
select A.City,count(S.Student_ID) as nnumber
from org O join student S on O.Loan_ID =S.Loan_ID
join Address A on A.Address_ID=O.Address_ID
group by City order by nnumber desc limit 5;
![image](https://user-images.githubusercontent.com/84727716/173187368-8662f50a-1eec-4a50-94d3-925dc7908fcb.png)


Query3: Average Requirement of Each Course
This helps students to choose courses based on average requirement for each course
Select Course_Name, avg(UnderGradCPGA),avg(TOFEL_IELTS),avg(GRE) from course C
join course_req CR on C.Course_Req_ID =CR.Course_Req_IDgroup by Course_Name
![image](https://user-images.githubusercontent.com/84727716/173187373-780f1e8e-a04e-484d-8268-a77581ac26c4.png)

Query4: Students who applied to Northeastern University
This query helps to find out the students who applied to a specific university so that they can
form groups to discuss about housing, academic discussions.
Select Lastname, Firstname from applicant where user_id in (Select user_id from university
U join application A on U.University_ID = A.University_ID where University_Name
='Northeastern University')
![image](https://user-images.githubusercontent.com/84727716/173187383-d3b62d00-586f-4a27-a71b-78098d823522.png)

Query5: Students who have qualified to course offered by the university based on the
requirements stated
Based on the Average requirements we filter out the applicants who are eligible for each
course
Select Ap.Applicant_ID,X.User_Id, U.University_Name from applicant A
join applicantscore X on A.User_Id = X.User_Id join application Ap on Ap.user_id =
A.User_id join course C on C.Course_id = Ap.Course_ID join course_req Cr on
Cr.Course_Req_ID =C.Course_Req_ID join University U on Ap.university_ID
=U.university_ID where X.TOFEL_IELTS >= Cr.TOFEL_IELTS and X.UnderGradCPGA
>= Cr.UnderGradCPGA and X.GRE >= Cr.GRE

![image](https://user-images.githubusercontent.com/84727716/173187388-ea5bb457-b626-4859-9d38-4854f56acaf2.png)

## 4. Implementation of Relational Model using NO SQL

![image](https://user-images.githubusercontent.com/84727716/173187406-a482b626-9487-430f-8cd2-9263e92a1595.png)

Query1: Number of Applications to Northeastern University
Match (n:Application)-[:Applied_university]-(u:University)
where u.University_Name= 'Northeastern University'
return count(n.Applicant_Id)
Query2: Top 5 courses in Northeastern University based on the Fee Range
Match(c:Course)-[:offers]-(d:Department)-[:Has]-(u:University)
return count(c.Course_Name) as number,u.University_Name
order by number desc
Query3: Number of Courses offered by a University
Match(c:Course)-[:offers]-(d:Department)-[:Has]-
(u:University) where u.University_Name= 'Northeastern University'
return c.Course_Name order by c.Fees Limit 5
5. Accessing Database Using Python
Python’s Seaborn library was used to visualize the output of SQL Queries. The graphs data
matched with the output of SQL queries.
Mysql Database is connected to python using Mysql.Connector and mycursor.execute and
mycursor.fetchall() is used to fetch the query outputs. Seaborn package is used to visualize
the query outputs.
Graph1: Intake of Students to different countries
Graph2: Average Salary of students place for every company in a university
6. Summary and Recommendation
The Students database in My SQL helps students to choose universities based on their profile
and observe the trends in the companies that hire students from the universities. Based on the
intake of students to the universities and their pay range financial organizations can prioritize
educational loans to the students. Python Seaborn package is used to analyse and visualize
Number of students to different countries, average salary range of students graduating from
each university. All the data imported and populated is real data which helps in drawing
better insights. The data is also analysed and visualized using Neo4j graph database. Cypher
language is used to query the Neo4j database.
One improvement in the database model that we observed after designing the database is
there can be few GPA Centric and Research Centric colleges that give preference to students
having achievements in these respective fields. By calculating the percentile of each student
among all other students for a particular intake we can determine the highest percentile value
of a student among GRE Scores, GPA, and Research Work. These statistics can be leveraged
to provide better university suggestions to the students. Also the Veracity of data is a concern
to be noted. As there are many organizations that try to take an advantage of these type of
applications by introducing fake student profiles which would change the accuracy of the
model and affect its efficiency. Taking inputs from only valid international students by
introducing a feature of mentioning passport Number or Mobile Number to use this
application would answer this security concern.
