# Real_time_stock_market_Analysis

## Overview

we'll be simulating real time stock market analysis using python generated data will be pushed from python application using a producer  via kafka broker
Kafka will be installed in our EC2 machine in AWS

Next we'll write a consumer to consume the daa and put in AWS S3

then glue crawler will used to crawl the schema from different files and build the glue catalog which will help us query data in different files.
and the querying part will be done by AWS Sthena


![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/Architecture.jpg)


## Prerequisites:

Knowledge in python,kafka,glue,athena,sql,s3,EC2
aws account 



## step1:

Spin up a Ec2 instance using your AWs acoount use free tier T2.micro so that charges are not incurred
login using ssh credentials
also if there is an permission error type chmod ".pem file" --> to allow permission

## step2:

Install Kafka in EC2 machine using the steps mentioned in file 
[kafka_installation_EC2](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/kafka_installation_EC2)
after installing and launch zookeeper,server, create topic,producer and consumer and verify working.
Note:follow all steps in above mentioned file!!

## step3:
Install kafka in jupyter notebook and create python producer adn cross check working in terminal where we created the producer

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p2_checking_producer_working.png)

next write consumer code in another jupyter notebook and check working

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p3_checking_producer_consumer_working.png)

## step4:

create a python script to simulate stock api using dataset provided and randomly pick data,loop and feed it to producer we can see that the data is generated

while checking the randomly genereated data in producer and consumer in terminal, make sure that
you run only for few seconds since we have a EC2 server with low resource 1 node and 1 broker thus terminate immediately 
else zookeeper,server,producer and consumer will shut down/stop.
incase of shut down restart  zookeeper,server,producer and consumer 

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p4_checking_python%20data%20genereated_in_kafka.png)

## step 6:

Now we need to create an s3 bucket and upload the data generated in consumer to s3
for this we need to install a package called s3fs
also need to configure aws

go to IAM create a user and create access key for cli usage
and dowload the credentials as a csv file and do not share crdentials


for configuring aws we need to  install aws cli in your system
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#cliv2-linux-install

configure aws in terminal using 'aws configure' now u are all set


## step 7:

sample o/p for the logic and server working confirmation

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p5_check_records.png)

running consumer first then producer and refreshing s3 bucket which dumps records in json format

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p6_running_producer_consumer_5sec_inserting_s3.png)

## step 8:

once data is in s3 we'll crawl using glue crawler the entire schema from our s3 files and query on top of it using athena.
create crawler and add s3 path also create IAM role for glue to access s3 bucket.
select glue and give admin access which gives full access to aws services and resources.

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p7_glue_crawler.png)

## step 9:

after IAM role is set for glue create a database
after creating databse add it to crawler and run
then use aws athena to query through the table created from database

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p8_querying_in_athena.png)

## step 10:

now inorder to make it streaming we can set a sleep(1) to create a delay so as to not make server crash in the kafka producercode in jupyter
and run again to see data getting streamed into the s3 and we can verify using athena.

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p9_live_streaming1.png)

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p10_live_streaming2.png)

![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/p11_live_streaming3.png)

we can see records changing while checking count since we are streaming data into s3 from kafka using s3



CREDITS : Ths real time project was done with the help of DARSHIL PARMAR 
          His Youtube channel :-- https://www.youtube.com/@DarshilParmar
