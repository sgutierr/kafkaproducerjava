# Kafka Producer/Consumer example in Java
This is an example of a Java producer that sends a random integer to a topic named `total-connected-devices`.
# Prerequisites
This is the software required for running this example:
 - Git 
 - Java Development Kit (JDK) OpenJDK 11
 - Red Hat OpenShift Container Platform CLI 
 - Kafka installlation on Red Hat OpenShift 

# Demo steps:
This application listens for records sent to the `total-connected-devices` topic. Then, run the `producer` application in your other command-terminal and verify that the `viewer` application is receiving the records.
## 0. Preparing certificate 
  1. Extracting the cluster certificate from OCP, example from Kafka namespace:
 **`oc extract secret/my-cluster-cluster-ca-cert --keys=ca.crt `**
 
 2. Generate a `truststore.jks` file with `password` as the store password. Store the KeyStore files in your workspace.
 **`keytool -import -trustcacerts -alias root -file kafka-cluster.crt -keystore truststore.jks -storepass password -noprompt`**
 
## 1. Setting up connection
By using your editor of choice, open the `producer/src/main/java/com/redhat/telemetry/producer/ProducerApp.java` file, and replace these variables by your correspondent environment variables: 
 - "**YOUR_KAFKA_BOOTSTRAP_HOST**"
 - "**YOUR_KAFKA_BOOTSTRAP_PORT**"
 - "**ABSOLUTE_PATH_TO_YOUR_WORKSPACE_FOLDER**" (path where your truststore.jks file is)

## 2. Compile application
In your command-line terminal, navigate to the `kafka-producers/plain` directory. Compile the application.
**`./mvnw clean package`**
## 3. Run the consumer and the producer
### 3.1 Consumer: 
In a new command-line terminal, execute the `viewer` application and leave it open.
**`java -jar viewer/target/viewer-1.0.jar`**

### 3.2 Producer: 
In your other command-line terminal, run the Java executable file for the `producer` application. This application sends several messages to Kafka.
**`java -jar producer/target/producer-1.0.jar`**

Verify that the `viewer` application is receiving the records sent by the `producer` application.
