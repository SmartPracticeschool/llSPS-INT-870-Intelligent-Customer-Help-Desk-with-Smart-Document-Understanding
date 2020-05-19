# Intelligent Customer Help Desk with Smart Document Understanding

## Category : Artificial  Intelligence

In this project, we go through a working example of a web ui that utilises multiple Watson services to create a better customer care experience.

Using the Watson Discovery Smart Document Understanding (SDU) feature, we will enhance the Discovery model so that queries will be better focused to only search the most relevant information found in a typical owner's manual. When a customer question involves operation of a product, the Assistant dialog will communicate with the Discovery service using a webhook.

The webhook will be created by defining a web action using IBM Cloud Functions.

### What is SDU ?

SDU - Smart Document Understanding. SDU trains Watson Discovery to extract custom fields in your documents. With SDU, you annotate fields within your documents to train custom conversion models. As you annotate, Watson is learning and will start predicting annotations. 

### What is Webhook ?

A webhook is a mechanism that allows you to call out to an external program based on something happening in your program. When used in a Watson Assistant dialog skill, a webhook is triggered when the Assistant processes a node that has a webhook enabled. The webhook collects data that you specify or that you collect from the user during the conversation and save in context variables. The URL that receives the webhook is the listener. 

In our example, the webhook will communicate with an IBM Cloud Functions web action, which is connected to the Watson Discovery service.

### Flow

![Capture](https://user-images.githubusercontent.com/64901867/81792927-55dc0580-9526-11ea-9339-8c817ecac130.PNG)

step-1: The  data  source  from  external  is  annotated  by  using  Watson  Discovery Smart  Document  Understanding.

step-2: The  user  interacts  with  the  back-end  server  through  the  application  user  interface. The  front-end  app  user  interface  is  a  chatbot  that  engages  the  user  in  a  conversaton.

step-3: Dialog  between  the  user  and  back-end  server is  coordinated  using  a  Watson  Assistant  dialog  skill.

step-4: If  the  user  asks  a  question  that  falls  outside  of  the  scope  of  the  pre-determined  question  set, then  a  search  query  is  issued  to  the  Watson  Discovery  service  through  a  Watson  Assistant  search  skill.

### Steps :

i) Create IBM Cloud services.

ii) Configure  Watson  Discovery.

iii) Create IBM Cloud Functions action

iv) Configure  Watson  Assistant.

v) Create the flow in Node-RED and Run the application.

### Configure Watson Discovery

#### Import the document

Launch the Watson Discovery tool and create a new data collection by selecting the Upload your own data option. Give the data collection a unique name. When prompted, select and upload the ecobee3_UserGuide.pdf file located in the data directory of the local repo.

Before applying SDU to the document, lets do some simple queries on the data so that we can compare it to results found after applying SDU.

![Capture](https://github.com/IBM/watson-discovery-sdu-with-assistant/blob/master/doc/source/images/disco-collection-panel-pre.png)

### 6. Project  Deliverables :

Requirement  specification (Document) - Initial  briefing  report.

User  interface

Backend  Development

Set up of Test System

User Training  session

Project Report

### 7. Project  Team:

Individual  project

Name : G.Bhavya

### 8. Project  Schedule : (19  days)

Project  Planning  & Kickoff - 1day

Setup  the  Development  Environment - 1 day

Create IBM  Cloud  Account - 0.5 day

Create  a  Node_RED  Starter  Application - 1 day

Explore  IBM  Watson  Usecases - 0.5  day

Introduction  to  Watson  Assistance - 2 days

Introduction  to  Watson  Discovery- 2 days

Getting  Started  with  IBM  Cloud  Functions - 1 day

Create  necessary  IBM  Cloud  services - 1 day

Configure  Watson  Discovery  Service - 1 day

Create  cloud  functions  action - 1 day

Configure  Watson  Assistant - 1 day

Build  Node-RED  flow  to  integrate  all  services - 2 days

Build  a  web  dashboard - 1 day

Test  the  Bot  and  capture  the  results - 1 day

Prepare  the  project  report  and  upload  the  Node_RED  flow  to  GitHub - 1 day

Create  a  project  Demo  Video  and  upload  to  youtube - 1 day
