# Real-Time_Custmer_Segmentation_Scala-Spark

Real-Time Telecome Operator Customer Segmentation based on their usage according to specific criteria that exist in SEGMENT.csv, and RULES.csv. It uses Scala-Spark to listen to a Spooling Directory that the streamed data is generated inside of it.

## Installation

Build the project to get the fat jar (scala-spark-assembly-0.1.jar)

```bash
sbt assembly
```


## Usage

### Generate Data and Stream
```bash
java -jar DataGen.jar Segment '/segment_dir_path'
java -jar DataGen.jar Rules '/rules_dir_path'
java -jar DataGen.jar Data '/stream_dir_path'
```

- RULES.csv  
Contains the rules which defines the rules for sending a notification per service
identifier/application. Fields are ordered as the following:  
i. Service Identifier: Id for the service/application  
ii. Service Description : Service/application name  
iii. Start time : the lower bound of usage tracking window  
iv. End time : the upper bound of usage tracking window  
v. Total volume : the volume amount that needs to be exceeded to mark a valid rule to send the notification  

- SEGMENT.csv  
Contains list of dials X Company interested to track their usage

- DATA_yyyyMMddHHmm.csv  
Contains a data record per line indicating one session. Field are ordered as the following:  
i. Msisdn: customer dial  
ii. Service Identifier: Id for the service/application  
iii. Traffic Volume: amount of download traffic used in the session  
iv. Timestamp : timestamp of the transaction  

Note: Customer dials are generated randomly from DataGen.jar, which exist in data directory.

### Process and Segment the Stream
```bash
java -jar scala-spark-assembly-0.1.jar
java -jar scala-spark-assembly-0.1.jar /stream_dir_path' '/segment_dir_path' '/rules_dir_path' '/output_dir_path'
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
