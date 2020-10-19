# Dataset 
This project uses the dataset of "Cambridge Police Department crash" to apply key information design concepts, demonstrate the function and best form of data visualization. There are 11 variables with 10,335 records in the dataset. The dashboards and charts are made in TABLEAU and QLIK SENSE

# Steps to execution
1.	Define your questions: we will be defining each problem in the next page of the document with an explanation.
2.	Set clear measurement priorities: our priorities are Number of Records, Days of the Week and Date Time
3.	Collect Data: Data is nothing but the Cambridge Police Crash Dataset
4.	Analyze the Data: Explained each research questions in a detailed way under the questions
5.	Interpret the Results by Visualization: Explained each visualization in a broadway under each research question.	

# Business Questions
Are the average traffic conditions of each day on weekends are more than the average on each day on weekends?
On what time does the higher number of accidents occur?
What are the trends in the crashes? 




## Event Hub Streaming Architecture
Event Hub Streaming application is designed to reveal the insight data from event hub as elaborated below:
***Batch Processing: Training Data*** Data is train using Spark ML library. Data got pull from TS/Blobstore for training and save to model back to Predix Blobstore, bellow is the Regression Pipeline model in Batch Training.
Flow iin snapshot bellow: 
<img src="img/Batch Processing.png">
***Stream Processing Data*** Streaming load the ML Model from Predix Blobstore. 
Streaming Flow using Event-Hub Connectors pull data from event-hub broker. Data go through cleaning/cleansing before cleansing dataframe feed to Pipeline prediction to genereate the prediction insight output.
Flow Diagram:
<img src="img/Stream Processing.png">  
## Predix-Insight Setup: 
###Set up the predix insight job with flow template and flow 
***Setup Flow Template: Bellow is the sample of Predix Insight Flowtemplate
<img src="img/PI-stream-flow-setup.png">
***Set up flow: Predix insight flow set up as bellow snapshot configuration.
<img src="img/PI-stream-flow-setup.png">
## Usage:
1. **Building application**: I recommend starting with the print flow template, a simple basic java code.  
   1a.Start add the code in java class file : PrintFlowTemplate.java. For example, start make change under method: 
   ```
   public static void processMessage(Message message){
      System.out.println("process message");
      String messageFromEventHub = new String(message.getBody().toByteArray(), StandardCharsets.UTF_8); 
      System.out.println(messageFromEventHub);
    } 
   ```    
   1b.Build flow-template java app using maven command: mvn clean isntall    
   
2. **Running application on local/ native spark cluster**: 
   1b. Run locally using the command (see in the note:
     ```
       spark-submit --jars flow-template/lib/spark-streaming-event-hub-assembly-1.0.jar,flow-template/lib/hadoop-aws-2.7.4.jar,flow-template/lib/aws-java-sdk-1.7.4.jar --class com.ge.predix.insights.flowtemplate.StreamProcessingFlowTemplate spark-streaming-event-flow-template-1.0-SNAPSHOT.jar   
