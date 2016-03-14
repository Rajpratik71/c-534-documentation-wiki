**<a href="http://app.c-534.io" target="_blank">c-534.io</a> is an Integration Platform as a Service to easily connect systems using REST API.**

# Basic Concepts
##Microservice 
Microservice is a main part of the **<a href="http://app.c-534.io" target="_blank">c-534.io</a>** platform. Can connect to almost any REST API available. Basically a Microservice consists of 3 main parts: **Input Connector**, **Transformation** and **Output Connector**. Look at the diagram below to grasp a basic understanding:
![](https://github.com/C-534/documentation/blob/master/images/02_microservice_diagram.png)

##Input connector
It's the mechanism used to receive or send the data to the external system (e.g. using REST API). Data returned by external system API is available in the **Transformation** as the "in_dict" variable.

##Transformation
Transformation is conversion **Input Connector** data to the **Output Connector** data using Python code. Below is an example of a simple transformation:
```Python
servicenow_notification = in_dict.get('data')

out_dict = {
  "Title": servicenow_notification.get('short_description'),
  "Description": servicenow_notification.get('description'),
  "TypeId": 246277520,
  "Priority": 1 
}
```

##Output connector
It's the mechanism used to send the data to the external system. Source of the data to send is an "out_dict" variable from the **Transformation**.