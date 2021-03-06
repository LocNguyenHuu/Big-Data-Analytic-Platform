# Big Data Analytic Platform
   This repo is the implementation of a data pipeline infrastructure built with Apache big data technologies, including Kafka, Cassandra, Spark, Redis. Kafka as the high volume data transmitter, Cassandra as the NoSQL database, Spark can do streaming process, ElasticSearch as the fast search engine, node.js as the server. The platform was designed to have high performance and ability to scale easily. If you are interested in learning more, start playing with each component by following the guide from READMEs under their folders!

# Overview 
   First, the stock data was retrieved from real-time stock dataset and ingested by Kafka cluster; next spark streaming was utilized to processe the raw data from Kafka brokers and compute the average value of the stock prices within a time period; then the processed data was pushed to redis hub for server to fetch; finally, there will be a simple dashboard UI developed using Bootstrap, D3.js, etc. to display the real-time price trends. 
<br><img src="https://github.com/Dukecat0613/Big-Data/blob/master/ImagesSet/Screen%20Shot%202017-02-16%20at%2011.21.24%20AM.png"></br>

# Dependency 
Please follow [this](https://docs.google.com/document/d/1d-ggqJGTdizkEO9sPjitKJksexe0vWE_9_O_zy8JH-s/edit?usp=sharing) guide to check and install software components required to run this program in your dev environment.

# Usage
Assuming your docker virtual machine ip is 192.168.99.100, first run flask-data-producer (include port, kafka_broker ip, kafka topic in your dev.cfg)
```
export ENV_CONFIG_FILE=`pwd`/config/dev.cfg
``` 
```
python flask_data_producer.py
```

Run redis_publisher
```
python redis_publisher.py `your kafka topic` 192.168.99.100:9092 `your redis channel` 192.168.99.100 6379
```

Run spark streaming, please include spark-streaming-kafka-0-8-assembly_2.11-2.0.0.jar in your spark classpath
```
spark-submit pyspark_streaming.py `your kafka producer topic` `another kafka topic you send to after processing data` 192.168.99.100:9092
```
Start server
```
node index.js --port=3000 --redis_host=192.168.99.100 --redis_port=6379 --subscribe_topic=`kafka topic you send to after processing data`
```


