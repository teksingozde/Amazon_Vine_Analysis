# Amazon Vine Analysis

A customer requested analysis and submission of product reviews written by Vine program members. Here, the expectation of the customer is whether there is any prejudgment in the critiques from the members in the product reviews.

## Resources
### Data Resources:
- Amazon Review Datasets Index.txt
- Amazon_Reviews_ETL.ipynb
- challenge_schema.sql

### Software Resources:
- Python 3. 9. 12
- Pandas 1. 4. 4
- Google Colaboratory
- Hadoop 2. 7
- Spark 3. 2. 3
- pgAdmin4 6. 12
- PostgreSQL 13.1
- DBeaver 22. 3. 1

## Overview of Analysis
It should be noted that Amazon AWS service was used at the beginning of the study. Amazon AWS provides us with an online database service and it is beneficial in terms of increasing the working capacity as the capacity of this work will make it difficult to use our computer. First of all, to talk about RDS, Relational Databases, an RDS is created thanks to AWS and this database provides benefits in terms of cloud storage service.
S3, on the other hand, is a simple storage service and is a cloud storage service that provides the transportation of many files without providing access to any computer, provided that they are received by Google Colaboratory.

Sagemaker, on the other hand, is a SQL platform that we built on AWS. Here, PostgreSQL is selected and the created local host connects to DBeaver and transfers the datasets, namely tables, that we created on Google Colaboratory without the need for a completely local computer. The necessary datasets are exported via DBeaver. In our work, the tables are exported as .csv file via DBeaver. However, you can also do the export in many ways, which are listed below.

<img width="591" alt="Screen Shot 2023-01-12 at 3 34 47 PM" src="https://user-images.githubusercontent.com/26927158/212211245-dbcef4cf-b0e2-4ee2-b596-1a4d49f52caa.png">

At the same time, you can easily access the ER Diagram to examine the relationships between the tables. When the exported tables are complete, connections with RDS are cut.

Google Colaboratory is a completely free and easy-to-use tool for Python analysis. You can perform data analysis by connecting with a database server as in our study, or you can easily perform the necessary analysis by uploading your dataset to the Google Colaboratory environment. There is no need to connect to the local computer to be able to analyze in Google Colaboratory. At the same time, when transferring projects on Github, a copy can be created and a worksheet can be presented by establishing a Github connection via Google Colaboratory.

In order for us to do our analysis in the study, Spark has been started first and Apache Spark provides the PostgreSQL driver to be loaded.
In this study, the URL is used to analyze. With the URL of this dataset, the data is read as Spark DataFrame. Here, a number of data tables are created, which are provided with SparkFiles.

The expectation in the study is to make a vine review analysis. For this, we need the work file that creates the PostgreSQL connection with the name and link of the study that we created while establishing the RDS connection in the system by making the RDS configuration. In order to create this connection, a password is entered and tables can be viewed and exported via DBeaver. Likewise, analysis can be made via Google Colaboratory by uploading the «vine_table.csv» file obtained from Amazon_Review_Analysis to S3. The RDS configuration query is as follows and the transfer of tables to the database is shown.
<img width="1027" alt="Configure RDS for Tables" src="https://user-images.githubusercontent.com/26927158/212211354-75a8511d-9cdd-4f9d-89e9-7a6a88d79a2f.png">

A few filters have been created in the study. These filters are; Reviews with at least twenty votes are those in which at least half of the votes are marked as helpful. Helpful reviews are also filtered among themselves. These filters are; It is in the form of paid and free reviews. Vine reviews are in the category of paid reviews. Vine reviews are also learned with an extra analysis as being 5 star. Because, it is only in this way that it can be understood whether the members of the vine create prejudices while examining.

Additionally, vine_Review_Analysis has been added with the help of pandas library via Google Colaboratory. This is because it shows that the work can be done using both pandas library and SQL, also by connecting to Spark. The studies under the "Vine Review Analysis" folder, Vine_Review_Analysis.ipynb, are the studies that were done entirely with Spark and Hadoop database. “Vine_Review_Analysis.sql” is in the form of a syntax, where the necessary filters are created by transferring the vine_table.csv file. When the vine_table.csv table is transferred to the SQL environment, the necessary analysis results can be obtained with the help of this query. “pandas_Vine_Review_Analysis.ipynb” was created using Google Colaboratory. Vine_table.csv data set was loaded into Google Colab environment and the study was done without connecting to a local computer in that way, and then transferred to Google Colab as Github repository by copying with the path of the study.

## Results

Vine Review Analysis results are as below and screenshots of the results are taken from Google Colaboratory.

#### Table 1. Vine DataFrame
![image](https://user-images.githubusercontent.com/26927158/212211521-0f5ba643-5610-4400-ba70-923e964d7527.png)
In the table above, the first 20 columns usually contain the information of people who are not a vine member. Generally, the scores given are 4 and 5. It is included in the first 20 columns, most of which are unapproved products.

#### Table 2. Total Votes Count DataFrame
![image](https://user-images.githubusercontent.com/26927158/212211627-951b1337-d442-4d26-80c4-e3ec53de3f79.png)
The first filter shows the votes with more than 20 total votes. In terms of each ID, it is seen that the majority of the total votes are considered helpful. However, not all of these first 20 lines are vine members and the majority of them are not endorsed products. The star rating points given also vary a lot.

#### Table 3. New Votes DataFrame 
![image](https://user-images.githubusercontent.com/26927158/212211706-227c616d-28a9-4635-9010-d028dead9b55.png)
The table above shows the DataFrame where helpful votes were selected as helpful more than half of the total votes. However, reviewers of these products are also not vine members, and overall star ratings vary. The products in the first 20 lines are listed as approved and unapproved. The highest total votes is 388 and the lowest is 20 as seen in the table. 370 of the criticism articles, which received 388 votes, were accepted as helpful. This is a very large rate and it can be seen that the person approves the product. Likewise, the critique with a total of 20 votes was approved and received 5 points.

#### Table 4. Unpaid Program Review DataFrame
![image](https://user-images.githubusercontent.com/26927158/212211807-713629c2-ac70-495d-bae8-c39e8f61eedc.png)
Unpaid program review results are the same as in Table 3. Because unpaid people are not vine members and do not pay any fees.

#### Table 5. Paid Program Review DataFrame
![image](https://user-images.githubusercontent.com/26927158/212211901-e1221827-8fd9-48d9-bc98-1dabe748f04e.png)
The analysis of people who are members of Vine is shown in table 5. In general, it is seen that they receive less votes than those who are not members of Vine, and in general, the majority of them are also beneficial. However, voting products are also seen as unapproved. In terms of star rating, there is a medium scoring system.

#### Table 6. Total - Unpaid - Paid Reviews 
![image](https://user-images.githubusercontent.com/26927158/212211987-0bb3118c-0ae9-4079-bc7a-a1571afce6a4.png)
- How many Vine reviews and non-Vine reviews were there?
In Table 6., the total vote of the criticism articles is 740,983.
While 736,202 of these total votes are non-vine members, 4,781 are vine members. According to the above analysis, non-vine members are approximately 154 times higher than vine members.

#### Table 7. Total - Unpaid - Paid Five Star Reviews 
![image](https://user-images.githubusercontent.com/26927158/212212124-0c5030dc-1ded-4d69-90de-a639ee218dad.png)
- How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
Table 7. shows the distribution of the products given 5 points between those with and without vine members. Those with a total of 5 points are 413,293, while those with vine members are 1.604 and those without vine members are 411.689. That is, those who are members of Vine are at very low levels in terms of both the number of criticisms and points.

#### Table 8. Percentage of Five Star Reviews Unpaid - Paid
![image](https://user-images.githubusercontent.com/26927158/212212243-1bf23754-3d2a-4aa3-9d17-cf46b9c69602.png)
- What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
While the 5 star review percentage of Vine members was 33.54%, the 5 star percentage of non-vine members was analyzed as 55.92%. This means that vine membership is in the form that there is no pre-judgment in the voting system and reviews in any way.

## Summary
First, there was not enough data for vine members in the first 20 rows of the dataset. It would be very difficult to comment adequately on this subject.
It is obvious that 5 stars is too many. This clearly shows that the satisfaction with the books is moderate.

It is not possible to make an explanatory comment about the Vine program, with a data set studied. In order to make such comments, homogeneous and normal distribution of the data is expected. However, there are many non-vine members and are not suitable for analysis.

33.54% of Vine members have been analyzed as 5 star reviews. Non-Vine members were also analyzed as 55.92%. If there was a bias in the critiques and scoring of vine members, it would be a higher rate, not 33.54%.
























