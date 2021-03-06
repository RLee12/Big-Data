# Big-Data
This repo is my experience and code with big data technologies, including Kafka, Cassandra, Spark, ElasticSearch, Node.js, Redis, Bootstrap,jQuery,D3.js. All the code is written in Python. Kafka as the high volume data transmitter, Cassandra as the NoSQL database, Spark can do streaming process, ElasticSearch as the fast search engine, node.js as the server.

# What did I do?
Firstly, I get stock data from google finance and transmitted the data by Kafka; Then utilized spark streaming processed the raw data from KafkaBroker and computed the average price of stock of every timestamp; Pushed the data to redis hub for server to read; Finally, displaying the real-time dynamic data using Bootstrap，jQuery and D3.js. 
<br><img src="https://github.com/Dukecat0613/Big-Data/blob/master/ImagesSet/Screen%20Shot%202017-02-16%20at%2011.21.24%20AM.png"></br>
# How to run?
Suppose your docker virtual machine ip is 192.168.99.100, first run flask-data-producer (include port, kafka_broker ip, kafka topic in your dev.cfg)
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


# Final Results
UI Interface:
<br><img src='https://github.com/Dukecat0613/Big-Data/blob/master/ImagesSet/Screen%20Shot%202017-02-14%20at%2010.21.32%20PM.png'></br>

Backend data pipeline:
<br><img src='https://github.com/Dukecat0613/Big-Data/blob/master/ImagesSet/Screen%20Shot%202017-02-14%20at%2010.23.00%20PM.png'></br>
