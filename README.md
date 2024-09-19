# Project 2: Data Quality Control Initiative for the City of Vancouver 311 Inquiry Volume Dataset.
# Project Description 
The Data Quality Control Initiative for the City of Vancouver 311 Inquiry Volume dataset guarantees that all the inquiry data information collected via phone and chat is reliable, accurate, and secure. Data governance is applied at each stage of data management through validation, encryption, and data quality, and this initiative ensures the data is constantly analyzed, secured from breaches, and kept for decision-making and operations to the highest standards.
# Objective  
This project aims to enforce rigorous data quality control measures of the 311 Inquiry Volume to maintain integrity, accuracy, and security and avoid any data loss or penetration by unauthorized personnel. This project seeks to preserve the integrity of the data to provide reliable and trustworthy data for analyzing public services and ensure data availability and accuracy over time.
# Background  
The data of Inquiry Volume 311 is collected by phone calls and chats that citizens of Vancouver make to the 311 services of the city. Concerning the augmentation in the volume and relevance of the data, it is crucial to maintain its quality components, such as accuracy, reliability, and security. Sometimes, a series of errors can lead to wasted information in a dataset, or more particularly, missing data, wrong entries, and even a compromise on security. This project responds to the following challenges through data encryption technologies, data governance, data replication, and monitoring in real-time.
 # Scope
- Implement encryption protocols to secure sensitive data within the dataset.
- Validate and clean data to ensure completeness and accuracy.
- Set up replication and backup systems to safeguard data in case of disasters.
- Monitor data pipelines for performance and detect any anomalies or issues.
- Store validated data in a Trusted Zone for downstream analysis and reporting.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/Project2_Draw.io.jpg?raw=true)


# Methodology
## 1. Data Encryption and Protection
AWS KMS stands for Key Management Service, a service through which users can create encryption keys and use them to protect their data across AWS Services. Data protection is achieved through encryption at rest and in transit, and there are additional layers of security through a combination of security access keys, frequent rotation of keys, and records of activities via AWS CloudTrail. KMS works closely with other AWS services, such as Amazon S3, RDS, and Amazon Elastic Block Store; data is encrypted with Customer Master Keys (CMKs) accrued by the user. This makes it easier to secure, manage, and put into compliance any keys or data that are sensitive.

SSE-KMS stands for Server-Side Encryption with AWS KMS, an extension of the encryption support provided for Amazon S3. In SSE-KMS, data is encrypted by default as they are saved in S3, and the encrypted data remains locked unless the users privileged with KMS permissions attempt to retrieve it. More features, such as crucial access and automatic key management, are integrated with monitoring tools that allow easy critical access and compliance tracking. The SSE-KMS data from the S3 is well protected; no unauthorized person can open and modify the data without permission.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/encryption.png?raw=true)

AWS Backup further complements this by providing automated data backup in S3, ensuring data availability in case of failures or data corruption. KMS, SSE-KMS, and AWS Backup provide robust data protection, encryption, and recovery solutions that secure sensitive datasets like the City of Vancouver's 311 Inquiry Volume, ensuring data integrity and security across AWS environments. AWS Backup will be used to create regular backups of the data to maintain data availability. 

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/S3%20Backup.png?raw=true)

The primary bucket's backup has been established. It is clear from the convention of naming. Versioning and encryption are enabled using the same "lab role" key in my primary bucket.

Data replication is duplicating data across multiple locations to ensure high availability, reliability, and disaster recovery. In the context of AWS, S3 Cross-Region Replication (CRR) allows the automatic copying of data from one Amazon S3 bucket to another in a different AWS region. This ensures that if data is lost, corrupted, or inaccessible in one area, a replica in another region can be restored. 

CRR enhances disaster recovery by providing geographical redundancy, which is especially important for organizations that must protect their data from regional failures, such as natural disasters or infrastructure outages. It also improves data availability, ensuring that users in different locations can access data quickly from the nearest region. 

The setup for replicating the 311 Inquiry Volume dataset across AWS regions is shown, safeguarding the data and ensuring it remains available even during regional failures.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/Replication.png?raw=true)

## 2. Data Governance
Data governance is a rigorous process of overseeing data management in a lifecycle manner to optimize the data's quality, security, availability, and compliance. Some of these are verifying the quality of the data and checking if the data is correct and has all the attributes needed for the intended use. Data governance also entails controlling sensitive information like PII through encryption, masking, or redacting privacy standards.

Besides the verification and certification of data, managers, and custodians of data apply the principles of data management in the area of data processing and sanitization in a way that helps to eliminate unwanted and redundant information in the systems, which are recognized as trusted. This includes sorting out information that may be useless and enhancing the quality of information that shall be processed or used. 

Automation becomes a core aspect of modern data governance, where the defined workflows and jobs are executed periodically to perform data management tasks such as validation, transformation, and updating. In this way, by continuing such processes, organizations will guarantee their data's credibility, security, and compliance with standards and legal requirements. 

In a nutshell, AWS Glue Data Brew will be used to clean and transform the dataset and ensure the available data is sufficient, trustworthy, legitimate, and safeguarded from any illicit use.
Several Components used in designing the ETL process are: 
-	Detect Sensitive Data: The process starts with identifying and masking Canadians' data restricted from being shared in different processes. From the feature, seven forms of sensitive data are masked, depicted by replacing the information with "*. ". 
-	Evaluate Data Quality: A completeness check was carried out on the "Mechanical System Type" column of the data. This meets the validity of the data being gathered, hence readiness to take it to the next level of processing. 
-	Conditional Router: The valid data was filtered to pass through a router check to endorse only the sound data to proceed to the following stages. 
-	Change Schema: Some extra columns not used in the analysis were dropped; thus, the schema was changed. 
-	Trusted Zone: The final transformed data are written in the secure folder and stored under the primary S3 bucket. 

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/ETL.png?raw=true)

- Validated data will be stored in a secure Trusted Zone in AWS S3, serving as the final destination for analysis-ready data.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/Trusted.png?raw=true)

## 4. Monitoring and Alerts
In the 311 Inquiry Volume project context, AWS CloudWatch monitors the health and performance of the data pipelines that process and store inquiry data. It tracks key metrics, such as data processing times, pipeline throughput, and system resource utilization, ensuring the pipeline functions efficiently without bottlenecks or failures.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/monitoring%20and%20controlling.png?raw=true)

We could track and trace the expenses for every task completed during the project using monitoring dashboards.

CloudWatch Alarms are configured to trigger notifications when certain thresholds are exceeded, such as unusual spikes in data volume or processing delays. For example, if there is an unexpected increase in data processing time, an alarm would notify the team to investigate and resolve the issue. This ensures that the data pipeline remains reliable and any performance issues are addressed promptly.

In the event of excessive spending or strange activity, alarms were designed to sound.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/Alarm.png?raw=true)

AWS CloudTrail will be used to log and audit all API calls and access to the dataset for security purposes.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/cloudtrail.png?raw=true)

CloudTrail automatically creates an S3 bucket to store logs that contain information about who accessed the data, what actions were performed, and who modified or deleted data. This ensures integrity and security, and the alarm configuration triggers alerts if suspicious activities are identified and ensures compliance with standards.
5. Data Quality Validation
The dataset will undergo rigorous validation checks to meet the highest data quality standards. A 100% completeness score will be achieved and validated through AWS Glue.
We may examine the final dataset's quality via the data quality tab. For me, the quality was perfect.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/QRPR.png?raw=true)

Automated ETL jobs will ensure that the data remains up-to-date and accurate.

In the 311 Inquiry Volume project, the workflow automates the entire data pipeline, from data ingestion to final storage in the Trusted Zone. The workflow uses AWS Glue to extract data from various sources and transform it by cleaning, validating, and loading it into Amazon S3. Each step will run automatically at regular intervals, ensuring the dataset remains current and accurate. This automated workflow minimizes manual intervention, reduces errors, and guarantees that the processed data is always ready for analysis. By scheduling tasks, the project achieves efficient, consistent data processing.

![Data Discovery](https://github.com/Vijaya397/Project-2/blob/main/images_project2/workflow.png?raw=true)

Workflow automates the process from data extraction to data storage in the Trusted Zone by scheduling each task regularly.
# Tools and Technologies
- AWS Key Management Service (KMS): This encrypts sensitive data and ensures secure storage.
- AWS S3 (Simple Storage Service): Store the dataset in stages (Landing, Raw, Curated, Trusted).
- AWS S3 Cross-Region Replication: This is for disaster recovery and high availability by replicating the dataset across regions.
- AWS Glue: To automate ETL processes and ensure the data is transformed, validated, and cataloged for use.
- AWS Glue DataBrew: Clean, profile, and transform the dataset before storage.
- AWS CloudWatch: To monitor data pipelines and set alarms for performance issues or anomalies.
- AWS CloudTrail: To track API activities, ensuring security and auditing.
- AWS Backup: Ensure the dataset is regularly backed up and available.
- Python (Pandas): This is used to manipulate and prepare the data for further use.
# Deliverables
- Encrypted and Secured Dataset: The dataset will be encrypted using AWS KMS, ensuring it is securely stored and protected from unauthorized access.
- Validated Data in Trusted Zone: A fully validated and cleaned dataset will be stored in the Trusted Zone, ready for further analysis.
- Data Quality Reports: Reports detailing the data quality checks and validation, including a 100% completeness score.
- Monitoring and Alerting System: Fully configured AWS CloudWatch Alarms and CloudTrail Logs for real-time monitoring and auditing of the dataset and API activities.





