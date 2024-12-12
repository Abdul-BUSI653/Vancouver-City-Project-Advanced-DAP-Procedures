# Vancouver-City-Project-Advanced-DAP-Procedures
A project which explain on the Data Enriching, Protection, Governance and Observability.


* In previous part I discussed about the stages involved till ETL pipeline design.
* Now we will move on to the parts post the ETL pipeline creation.
* Below picture “2210112 DAP Design” depicts the various components of design used by him.
![image 000](https://github.com/user-attachments/assets/12bd1f50-9a97-4c89-a5d4-42d4e9057154)<br>
* Previously we stored the information of the ETL outputs in the “vrpr-tfm-abdul” bucket. WE now retrieve that and use it for further processes.
* This step involves the 4 major steps namely:
#### Step 1: Data Enriching
* Data enrichment in data management is all about augmenting raw data with relevant context and information that provides more value for analytical purposes.
* This cleanses the data and transforms it to provide meaningful insights, which again are useful to make better decisions.
* This is where we can make the data available in a more informative way using external tools or services.
* For instance we can use ‘Athena’ service or other SQL services to make data available in a table format so it is easy to understand.
![image 001](https://github.com/user-attachments/assets/c245da6f-5692-44c9-b142-8559c540f04f)>br>
* We can achieve this by creating a database named “vprp_parks_info_db_abdul” and a table called “vprp_parks_info_table_abdul” as shown above.
* The next step is where we can access the above created tables or databases for our analysis.
![image 002](https://github.com/user-attachments/assets/e0196d80-e134-4648-ad25-71eba483ad44)<br>
* This is shown above where we access all the information from the table “vprp_parks_info_table_abdul” using SQL commands.
* The other way we can enrich our data is by making it available in form of reports.
* To make these report available we can use web servers and general servers.
* Before we do that we need a few other configurations to be made.
* For instance we should have our own setup of vpc and other network related things.
![image 003](https://github.com/user-attachments/assets/32edac0d-cf70-41d7-a95e-102fe0147bbf)<br>
* Above image shows the information of “vprp-vpc-abdul-vpc” created for this instance.
![image 004](https://github.com/user-attachments/assets/00597481-6b80-4524-9118-4d1e07644b70)<br>
* Above image shows the information of subnets “vprp-vpc-abdul-subnet-public-1-us-east-1a” and “vprp-vpc-abdul-subnet-private-1-us-east-1b” respectively.
![image 005](https://github.com/user-attachments/assets/51f0439f-330c-4280-a637-27913f6ffa3f)<br>
* Above image shows the information of network route tables created.
![image 006](https://github.com/user-attachments/assets/ecd686e5-3938-4a04-a4fc-54c3bb356acb)<br>
* Above image shows the information of “vprp-vpc-abdul-igs” internet gateway created for access to web and general servers and network respectively.
![image 007](https://github.com/user-attachments/assets/f3d2b4f0-d434-4c00-ad2a-98d876c93978)<br>
* Above image shows the information of “vprp-vpc-abdul-nat-public1-us-east-1a” NAT gateway created for access to web servers and network only.
![image 008](https://github.com/user-attachments/assets/5dc050cf-1356-48f9-9184-c59220712681)<br>
* Above image shows the information of security groups created for web servers (vprp-web-server-sg-abdul) and general (vprp-general-server-sg-abdul) servers respectively.
![image 009](https://github.com/user-attachments/assets/9ec785da-ee48-46e9-b79c-39888e266d93)<br>
* Above image shows the information of the EC2 servers created for web servers (vprp-web-server-abdul) and general servers (vprp-general-server-abdul) respectively.
![image 010](https://github.com/user-attachments/assets/7971849a-7ed7-42c0-a7d7-f87c961a0d6f)<br>
*  Above image shows the information of successful installation of Web Server role in web servers (vprp-web-server-abdul).
![image 011](https://github.com/user-attachments/assets/3f6ba7e1-322f-4334-8217-55fdeda76aaa)<br>
*  Above image shows the information of IIS page in web servers (vprp-web-server-abdul).
![image 012](https://github.com/user-attachments/assets/ca855517-66c2-4a83-946f-ce15d53c4046)<br>
*  Above image shows the iis page access via public ip address of web servers (vprp-web-server-abdul).
*  These are two primitive ways using which we can enrich our data and make it available for end-users.
#### Step 2: Data Protection
* In AWS, one can protect sensitive data by encrypting it to protect its confidentiality and security.
* AWS KMS provides a centralized control point for encryption keys so that users can create, manage, and use them to perform encryption and decryption automatically and with control over access to the keys using IAM policies.
* It improves data protection to be compliant with security standards.Next comes the protection this can be done in multiple ways.
* We have chosen to do it in 2 major ways.
* First is where we can use ‘KMS’ key which can be used to both encrypt and decrypt the data when using it. This provides more security.
* Also instead of using the default key provided by Amazon am creating one new key named “KMS-abdul”.
![image 013](https://github.com/user-attachments/assets/16cf1b32-de74-4a5c-b047-b59d81a2ade1)<br>
* Above image shows the “KMS-abdul” key information
* I will be using this key for multiple purposes like when encrypting the buckets or other instances.
* Before we go and enable the encryption we should also enable the bucket versioning. This is an added layer of protection.
![image 014](https://github.com/user-attachments/assets/86c8042b-d3da-440e-8919-dc231912d2a5)<br>
* Above image shows the information of enabling the default encrypting and bucket versioning.
* I will also create backup buckets “vprp-tfm-abdul-backup” to store information of transformed data buckets created to store the parks information as extra protection.
![image 015](https://github.com/user-attachments/assets/5ab4cb91-a67b-478f-a94d-630c315cfc09)<br>
* Above image shows the backup buckets creation and creating a replication rule to ensure data backup.
#### Step 3: Data Governance 
* Data governance is the discipline for establishing, implementing, and maintaining the structure for data across the enterprise.
* This means defining data quality, privacy, security, and compliance with regulatory standard policies, roles, and procedures.
* Starting with creating access controls, auditing data usage, enabling encryption capabilities for your data, and using features such as AWS Glue Data Catalog for managing and cataloging metadata, data governance in AWS is a combination of setup, management, and maintenance.
![image 016](https://github.com/user-attachments/assets/b6eed7c7-a9a4-4e01-830f-130e48240a26)<br>
* Above image shows the data catalog created.
* Here we need to first access the data we obtained via AWS Glue ETL pipeline designed in the first part.
* We then detect and find any information relevant to customers and clients and then protect it by using some protective ways like replacing the information with “****” or other such sequences.
* We can also evaluate the data quality like in our case we did for the completeness to be more than 95% and uniqueness of data be above 0.75.
* This ensure the data is complete and and unique based on our requirements.
* Once this is achieved we can use the conditional router to separate the data that passed and failed respectively.
* The passed data is stored inside the “Passed” folder created in the “vprp-tfm-abdul” bucket and the failed data is stored in “Failed” folder created in the “vprp-tfm-abdul” bucket.
![image 016-1](https://github.com/user-attachments/assets/0b71e3ae-f475-4c7e-9ecd-b49c74c89a95)<br>
* Above image shows the information of the “dc-vprp-abdul” job run details for the data catalogue.
![image 016-2](https://github.com/user-attachments/assets/050ef7ac-1ee3-4bfa-a003-e2a3a5ec76a7)<br>
* Above image shows the information of Failed folder and respective information stored in it.
![image 016-3](https://github.com/user-attachments/assets/61825c5e-f210-40df-8fbf-52aba3138bd0)<br>
* Above image shows the information of Passed folder and respective information stored in it.
* In this manner we can provide data governance for all the information we are going to use in the DAP of “Vancouver City Parks”.
#### Step 4: Data Observability 
* The real-time performance and health of the data platform in the Parks, Recreation, and Pets (PRP) domain is visualized using the data observability dashboard displayed in AWS CloudWatch.
* A customized dashboard tracks key metrics, including bucket storage utilization, number of objects in buckets, and associated estimated charges, giving a full view of data operations.
* We often face issues related to the data access or budgets or usages and others.
* To avoid this we can customize our own dashboard where we can see all these information at a glance.
* For instance if we are not sure on the S3 data storage and the buckets information is within project limit or not then we can add them to the dashboard shown below.
* Similarly for instance the lab limit is 50$ for us I do not want to exceed 12$ in a day then I can even have the respective alarms designed for that.
* I can even have the resorce sage. For instance we are using the AWS Glue for more time so we can setup an usage report in dashboard which says how much percentage that service is being used.
* The below picture depicts the various information related widgets added in the dashboard.
![image 017](https://github.com/user-attachments/assets/22c98324-0431-4c6d-bb20-4e904ebe1e58)
* Above image shows the information of “vprp-dashboard-abdul” dashboard created.
