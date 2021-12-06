# Udacity_EvaluateHumanBalance

#### Project Overview
You work for the data science team at STEDI, a small startup focused on assessing balance for seniors. STEDI has an application that collects data from seniors during a small exercise. The user logs in and then selects the customer they are working with. Then the user starts a timer and clicks a button with each step the senior takes. When the senior has reached 30 steps, their test is finished. The data transmitted enables the application to monitor seniors’ balance risk.


#### A New Product Feature
Your product manager has requested a graph that shows fall risk (will they fall and become injured?) for recent assessments. The development team has built a graph, which is ready to receive risk information from Kafka:

#### The Data
The STEDI data science team has configured some real-time data sources using Kafka Connect. One of those data sources is Redis. When a customer is first assessed in the STEDI application, their record is added to a sorted set called Customer in Redis. Redis is configured as a Kafka source and whenever any data is saved to Redis (including Customer information), a payload is published to the Kafka topic called redis-server.

#### The Challenge
The application development team has programmed certain business events to be published automatically to Kafka. Whenever a customer takes an assessment, their risk score is generated, as long as they have four or more completed assessments. The risk score is transmitted to a Kafka topic called stedi-events as a JSON object with this format:

{"customer":"Jason.Mitra@test.com","score":7.0,"riskDate":"2020-09-14T07:54:06.417Z"}
The application development team was not able to complete the feature as the graph is currently not receiving any data. Because the graph is currently not receiving any data, you need to generate a new payload in a Kafka topic and make it available to the STEDI application to consume.

#### Related Topic
redis-server Topic: Write one spark script sparkpyrediskafkastreamtoconsole.py to subscribe to the redis-server topic, base64 decode the payload, and deserialize the JSON to individual fields, then print the fields to the console. The data should include the birth date and email address. You will need these.
stedi-events Topic: Write a second spark script sparkpyeventskafkastreamtoconsole.py to subscribe to the stedi-events topic and deserialize the JSON (it is not base64 encoded) to individual fields. You will need the email address and the risk score.
stedi-score Topic: Write a spark script sparkpykafkajoin.py to join the customer dataframe and the customer risk dataframes, joining on the email address. Create a JSON output to the newly created kafka topic you created for STEDI to subscribe to that contains at least the fields below:

#### Project Structure
'''
Evaluate Human Balance
|____Guide.ipynb
|____sparkpyrediskafkastreamtoconsole.py    # Spark streaming script
|____sparkpyeventskafkastreamtoconsole.py   # Spark streaming script
|____sparkpykafkajoin.py                    # Spark streaming script
|____submit-redis-kafka-streaming.sh
|____submit-event-kafkastreaming.sh
|____submit-event-kafkajoin.sh
|
|____stedi-application
| |____application.conf                     # Set up customized Kafka topic
| |____stop.sh
| |____start.sh
|
|____Spark
| |____logs                                 # Result logs
| | |____redisstream.log
| | |____eventstream.log
| | |____kafkajoin.log
| | |____spark--org.apache.spark.deploy.master.Master-1-53eda89c49aa.out
| | |____spark--org.apache.spark.deploy.worker.Worker-1-53eda89c49aa.out
|
|____screenshots                            # Application working screenshots
| |____screenshot 2.jpg
| |____screenshot 1.jpg
'''
