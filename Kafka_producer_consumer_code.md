# getstream data ssl
  
  ```
  val kafkaDF: DataFrame = spark.readStream
        .format("kafka")
        .option("kafka.bootstrap.servers", <broker details>)
        .option("kafka.security.protocol", <>)
        .option("kafka.ssl.truststore.location", <>)
        .option("kafka.ssl.truststore.password", <>)
        .option("startingOffsets", <>)
        .option("subscribe", <>)
        .option("maxOffsetsPerTrigger", <>)
        .option("kafka.ssl.keystore.location", <>)
        .option("kafka.ssl.truststore.password", <>)
        .option("kafka.ssl.endpoint.identification.algorithm", "")
        .option("failOnDataLoss", failOnDataLoss)
        //.option("isolation.level", "read_committed")
        //.option("kafkaConsumer.pollTimeoutMs",400000) //512
        //.option("fetchOffset.numRetries",5)//3
        //.option("fetchOffset.retryIntervalMs",20)
        // .option("spark.streaming.receiver.writeAheadLog.enable",true)
        // .option("enable.auto.commit",true)
        .load()
  kafkaDF.select("value"))
 ```
 # getstream data non-ssl
  
  ```
  val kafkaDF: DataFrame = spark.readStream
        .format("kafka)
        .option("kafka.bootstrap.servers", config.getString(Constants.APP_KAFKA_BROKER))
        .option("startingOffsets, config.getString(Constants.APP_KAFKA_STARTINGOFFSETS))
        .option("subscribe", config.getString(Constants.APP_KAFKA_TOPICNAME))
        .option("maxOffsetsPerTrigger", maxRecords)
        .option("kafka.ssl.endpoint.identification.algorithm", "")
        .option("failOnDataLoss", <"true/false">)
        //.option("isolation.level", "read_committed")
        s//        .option("spark.streaming.receiver.writeAheadLog.enable",true)
        //        .option("enable.auto.commit",true)
        .load()
  ```

# sinkstream data
  ```
  val kafkaWriter: StreamingQuery = kafkaDF
        .selectExpr(
          "CAST(key AS STRING)",
          "CAST(value AS STRING)",
          "CAST(partition AS INTEGER)",
          "CAST(offset AS LONG)",
          "CAST(timestamp AS STRING)",
          "CAST(timestampType AS INTEGER)",
          "CAST(topic AS STRING)"
        )
        .withColumn("load_date", date_format(current_timestamp, "yyyyMMddHHmm"))
        .coalesce(10)
        .writeStream
        .option("checkpointLocation", <>)
        .option("path", <>)
        .partitionBy("load_date")
        .trigger(if (triggerSeconds > 0) {
          <...>
        } else Trigger.Once())
        .format("Json")
        .outputMode(OutputMode.Append()) //csv,orc,parquet
        .start()

      kafkaWriter.awaitTermination
  ```
  
  Screenshot 2021-07-03 at 2.50.50 PM<img width="1250" alt="Screenshot 2021-07-03 at 2 50 50 PM" src="https://user-images.githubusercontent.com/32897934/124349672-1bdc3000-dc0e-11eb-8c2b-608e1fada515.png">
