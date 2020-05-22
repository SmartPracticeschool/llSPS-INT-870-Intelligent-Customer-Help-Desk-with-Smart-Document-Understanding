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

Click the Build your own query [1] button.

Enter queries related to the operation of the thermostat and view the results. The results are not very useful, and in some cases, not even related to the question.

#### Annotate with SDU 

Now let's apply SDU to the document to see if we can generate some better query responses.

From the Discovery collection panel, click the Configure data button to start the SDU process.

The goal is to annotate all of the pages in the document so Discovery can learn what text is important, and what text can be ignored.

i) Select text and assign it a label like subtitle, text, footer, etc.,

ii) Submit the page to Discovery.

As we go though the annotations one page at a time, Discovery is learning and should start automatically updating the upcoming pages. Once we get to a page that is already correctly annotated, we can stop, or simply click Submit. The more pages you annotate, the better the model will be trained.

Once we click the Apply changes to collection button, we will be asked to reload the document. Choose the same manual .pdf document as before.

Next, click on the Manage fields tab.

Here is where we tell Discovery which fields to ignore. Using the on/off buttons, turn off all labels except subtitles and text. Tell the Discovery to split the document apart, based on subtitle. Submit the changes. Once again, you will be asked to reload the document.

![Capture](https://github.com/IBM/watson-discovery-sdu-with-assistant/blob/master/doc/source/images/disco-collection-panel.png)

Return to the "Build your own Query" and we will see how much better the results look like.

### Create IBM Cloud Functions action

Start the IBM Cloud Functions service by selecting Create Resource from the IBM Cloud dashboard. Enter functions as the filter, then select the Functions card

From the Functions main panel, click on the Actions tab. Then click on Create.

From the Create panel, select the Create Action option.

On the Create Action panel, provide a unique Action Name, keep the default package, and select the Node.js 10 runtime. Click the Create button to create the action.

Once your action is created, click on the Code tab. Modify the Code as per your application.

Select the Parameters tab. Add the following keys in the Parameter : url, environment_id, collection_id, iam_apikey

Now that the credentials are set, return to the Code panel and press the Invoke button again. Now we should see actual results returned from the Discovery service.

Next, Go to the Endpoints tab, Click the checkbox for Enable as Web Action. This will generate a public endpoint URL . Take note of the URL value, as this will be needed by Watson Assistant.

### Configure Watson Assistant

Launch the Watson Assistant tool and create a new dialog skill. Select the Use sample skill option as the starting point. 

#### Add new intent

Create a new intent that can detect when the user is asking about operating the Ecobee thermostat.

Create the Intents tab and Click the Create intent button.

Name the intent #Product_Information, and enter the following example questions to train the Watson.

i) How to set the timer?

ii) How to set the furnace?

iii) How to turn on the heater?

#### Create new dialog node

Now we need to add a node to handle the newly added intent. Click on the Dialog tab, select the Add node below option. 

Name the node "Queries about product" and assign it the newly added intent. This means that if Watson Assistant recognizes a user input such as "how do I set the time?", it will direct the conversation to this node.

#### Enable Webhook from Assistant

click on Customize, and enable Webhooks for this node. Click Apply.

The dialog node should have a Return variable set automatically to $webhook_result_1. This is the variable name you can use to access the result from the Discovery service query. We need to pass in the users question via the parameter input. The key needs to be set to the value "<?input.text?>"

#### Test in Assistant Tooling

From the Dialog panel, click the Try it button and Enter some user input and test the bot if it is giving the accurate result.

### Create the flow in Node-RED 

Go to Cloud Foundary App in the IBM Cloud Dashboard and go to the Visit the app url. This will direct us to the NOde-RED software, now click on Go to the Node-RED flow editor

Now Install the Node-RED dashboard from the "Manage Pallet". Now Create the flow shown below in the flow editor. (Images are given in the reference in git. Please refer that)

Now click on Assistant and make sure you enter the correct credentials (Workspace ID) that we have created earlier. Otherwise it gives an error like "Resource Not Found". Now Deploy the flow. If everything is correct, then it will be deployed successfully.

Now copy the url till ./net and add ui to the url now you can see the user interactive ui. Test the bot and check if it is giving the accurate results. Images have been provided for the reference.

## License

This project is licensed under the MIT License.

## Learn more

Artificial Intelligence Code Patterns: https://developer.ibm.com/technologies/artificial-intelligence/

With Watson: Want to take your Watson app to the next level? Join the With Watson program to leverage exclusive brand, marketing, and tech resources to amplify and accelerate your Watson embedded commercial solution. https://www.ibm.com/watson/with-watson/

Kubernetes on IBM Cloud: Deliver your apps with the combined the power of Kubernetes and Docker on IBM Cloud- https://www.ibm.com/cloud/container-service

## Links

Demo on Youtube : https://youtu.be/pd57ehoLOv0

Node-RED flow link : https://ishubot.eu-gb.mybluemix.net/red/#flow/7764455e.d3d65c

Node-RED UI link : https://ishubot.eu-gb.mybluemix.net/ui/#!/0?socketid=ofDza2eEa-D9GUboAAAB


