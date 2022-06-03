##### final-project-twitter
# Dashboard Service of Targeted Sentiment Analysis on Trending Twitter Topics
Group Members: 
<br>. Emily Yeh: Set up Lambda Function streaming tweet search result on AWS via Tweepy package, Case Study on the key word "Abortion Rights" 
<br>. Fiona Lee: Create S3 buckets to store the tweet raw data and RDS db to store select tweet data including sentiment analysis results, chain user input and data into pipeline
<br>. Helen Yap: Set up Lambda function to perform sentiment analysis on tweets and upsert tweet data to RDS 
<br>. Yutai Li: Build the dashboard to analyze and visualize the descriptive statistics and sentiment classification results 

## Introduction
We propose a workflow for analyzing the sentiments surrounding trending topics on Twitter. We will first stream the Twitter API to the AWS services, and provide analytical data upon keyword queries. By conducting content analysis tasks such as sentiment classification on those tweet conversations and organizing the descriptive information on a dashboard, our pipeline could allow users to gain the insights of how a specified topic is led and discussed by opinion leaders. 

Given the vast growth in social media usage and reliance for news and information, developing a large-scale method to collect and analyze Twitter data as described above would help inform how users feel and perceive the information that can then potentially inform downstream decision-making behaviors.  

## User Interface
Because the target users of our pipeline tool are social science researchers who may not have advanced knolwedge and skills or enough time to build up a whole pipeline including tweets scraping, data storage, sentiment analysis and visualization, we hope to incapsulate all technical details in a downlodable repository. By entering parameters for tweets data, the pipeline takes in user-specified requirements and scrapes the corresponding data for analysis. Users do not need to run any code or upload any files manually onto AWS; the only prerequisite on the user end is have an AWS personal account available, and by sending parameters into the pipeline, databases with tweets data and visualizations of tweets' sentiment are ready to be accessed. Social science researchers can thus work with large-scaled social media data even without sufficient computational resources and advanced skills. 

## Deploying Tweet Data

## Parallelization Design
The current pipeline leverages the 10 allowed invocations of Lambda functions to parallelize sentiment analysis and RDS upsert. A stepfunction is used to pass 10 batches of tweet data to the Lambda function carrying the boto3 client call to AWS Comprehend and RDS. Parallelism on sentiment analysis and writing into database allows a significant decrease in time; the shorter waiting time and the smaller possibility of timeout in processing twitter data are the main advantages of our parallelization design.

## Cloud Storage
Unlike local storages that take up space in disk, cloud databases free up local storage space and provide easy access to large amount of data. In this project, our choice of AWS S3 bucket allows a complete backup for twitter data used in the sentiment analysis, and thus users can always refer back to the raw data, conduct more analyses, and draw different conclusions from the same dataset. Our design of using RDS for processed tweets data enables quick query of sentiment analysis results, and downstream statistical analyses and visualization based on the processed data can be easily performed and customized for every user. With the cloud nature of these two databases, research that utilizes our pipeline tool is no more limited by the local computational resources and storage space; moreover, these databases in the AWS ecosystem prevent any incompatibility between our data processing pipeline and data storage. 

## Dashboard Interface

## Case Study: Abortion Rights

## Prospects of scalability
Our data pipeline is scalable on multiple fronts: 
* **SQS queue:** AWS's SQS queue already has high throughput allowing for even bigger streams of data than we currently have (and are limited by Twitter APIs). If needed, throughput can be further increased by horizontally scaling up SQS by: increasing the number of threads per client, adding more clients
and or increasing the number of threads per client. 

* **Lambda functions:** We are currently limited to 10 invocations of Lambda by AWS Academy. To scale up to potentially 10,000 Lambda functions, we recommend switching to a personal AWS account, which can provide more resources for larger-scale parallelization.

* **RDS:** If greater storage capacity is needed, it is possible to modify the instance type of the current RDS db. If there is uncertainty regarding future workload size, it is also possible to set RDS to automatically scale. 




## References
* https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-throughput-horizontal-scaling-and-batching.html 
* https://aws.amazon.com/blogs/database/scaling-your-amazon-rds-instance-vertically-and-horizontally/


