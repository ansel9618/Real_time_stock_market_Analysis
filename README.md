# Real_time_stock_market_Analysis

## Overview

we'll be simulating real time stock market analysis using python
Next the generated data will be pushed from python application using a producer  via kafka broker
Kafka will be installed in our EC2 machine in AWS

Next we'll write a consumer to consume the daa and put in AWS S3

then glue crawler will used to crawl the schema from different files and build the glue catalog
which will help us query data in different files

and the querying part will be done by AWS Sthena


![My Image](https://github.com/ansel9618/Real_time_stock_market_Analysis/blob/main/images/Architecture.jpg)



















CREDITS : Ths real time project was done with the help of DARSHIL PARMAR 
          His Youtube channel :-- https://www.youtube.com/@DarshilParmar
