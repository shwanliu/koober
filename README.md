Koober
----------------

An uber data pipeline sample app.  Play Framework, Akka Streams, Kafka, Flink, Spark Streaming, and Cassandra.


Start Kafka:

    ./sbt kafkaServer/run

Web App:

1. Obtain an API key from [mapbox.com](https://www.mapbox.com/)
1. Start the Play web app: `MAPBOX_ACCESS_TOKEN=YOUR-MAPBOX-API-KEY ./sbt webapp/run`

Try it out:

1. Open the driver UI: [http://localhost:9000/driver](http://localhost:9000/driver)
1. Open the rider UI: [http://localhost:9000/rider](http://localhost:9000/rider)
1. In the Rider UI, click on the map to position the rider
1. In the Driver UI, click on the rider to initiate a pickup

Start Flink:

1. `./sbt flinkClient/run`
1. Initiate a few pickups and see the average pickup wait time change (in the stdout console for the Flink process)

Start Cassandra:

    ./sbt cassandraServer/run

Start the Spark Streaming process:

1. `./sbt kafkaToCassandra/run`
1. Watch all of the ride data be micro-batched from Kafka to Cassandra

Setup PredictionIO Pipeline:

1. Setup PIO
    (base) liuxiaoyingdemacbook pro:.git liuxiaoying$ pio status
     
    [INFO] [Management$] PredictionIO 0.14.0 is installed at /Users/liuxiaoying/PredictionIO-0.14.0
    [INFO] [Management$] Inspecting Apache Spark...
    [INFO] [Management$] Apache Spark is installed at /Users/liuxiaoying/PredictionIO-0.14.0/vendors/spark-2.1.1-bin-hadoop2.6
    [INFO] [Management$] Apache Spark 2.1.1 detected (meets minimum requirement of 2.0.2)
    [INFO] [Management$] Inspecting storage backend connections...
    [INFO] [Storage$] Verifying Meta Data Backend (Source: PGSQL)...
    [INFO] [Storage$] Verifying Model Data Backend (Source: PGSQL)...
    [INFO] [Storage$] Verifying Event Data Backend (Source: PGSQL)...
    [INFO] [Storage$] Test writing to Event Store (App Id 0)...
    [INFO] [Management$] Your system is all ready to go.
    
2. Set the PIO Access Key:

        export PIO_ACCESS_KEY=<YOUR PIO ACCESS KEY>

3. Start the PIO Pipeline:

        ./sbt pioClient/run

Copy demo data into Kafka or PIO:

For fake data, run:

    ./sbt "demoData/run <kafka|pio> fake <number of records> <number of months> <number of clusters>"
    
For New York data, run:

    ./sbt "demoData/run <kafka|pio> ny <number of months> <sample rate>"

Start the Demand Dashboard

    PREDICTIONIO_URL=http://asdf.com MAPBOX_ACCESS_TOKEN=YOUR_MAPBOX_TOKEN ./sbt demandDashboard/run
