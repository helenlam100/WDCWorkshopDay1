Introduction

Format of workshop: 6-7 projects total over two full-time days. 
Focus: Bring clarity to all of the Watson APIs, and (i) be able to demo through NodeRed; (ii) utilize the APIs and understand the documentation; (iii) and fork and clone existing applications made available through Watson Developer Cloud for internal discussions and client facing discussions. 

Prep:
Open Bluemix and request Alchemy API key. 

Agenda – DAY 1
9:15 a.m. – 9:30 a.m. Coffee and refreshments. 
9:30 a.m. – 10 a.m. Introduction. Verify set up environment, C9 registration and Bluemix registration, should be done before class. 30 minutes. 
10:00 a.m. – 10:45 a.m. Introduction to Bluemix GUI, Jazzhub, the cognitive APIs, Watson APIs. Provision Alchemy Service, get key for 2nd day (takes up to 48 hours to receive key). 
10:45 a.m. – 11:30 a.m. Project 1 part 1 – Language Translation, Text-to-Speech, Speech-to-Text App 
11:30 a.m. – 12:15 p.m. Project 1 part 2
12:15 p.m. – 1:15 p.m. Lunch – catered
1:15 p.m. – 2:45 p.m. Project 2 Personality Insights App
2:45 p.m. – 4:15 p.m. Project 3 Visual Image App 

Overview of Bluemix
Cloud Foundry 
Cloud Foundry is an open source platform as a service (PaaS) that lets you quickly create and deploy applications on the cloud. 

References
(i)	https://console.ng.bluemix.net/docs/starters/install_cli.html
(ii)	https://www.ibm.com/developerworks/cloud/library/cl-bluemixfoundry/
(iii)	http://www-03.ibm.com/certify/tests/eduC5050-285.shtml
  Study_Guide_C5020_285.pdf  

NodeRed 
“Node-RED is a visual tool for wiring the Internet of Things. It is easy to connect devices, data and api’s (services). It can also be used for other types of applications to quickly assemble flows of services. Node-RED is available as open source and has been implemented by the IBM Emerging Technology organization. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range of nodes in the palette. Flows can be then deployed to the runtime in a single-click. While Node-Red is based on Node.js, JavaScript functions can be created within the editor using a rich text editor. A built-in library allows you to save useful functions, templates or flows for re-use.”
References and link to intro lab: https://github.com/watson-developer-cloud/node-red-labs/tree/master/introduction_to_node_red
NodeJS
“Node.js is an open-source, cross-platform runtime environment for developing server-side Web applications. Although Node.js is not a JavaScript framework,[3] many of its basic modules are written in JavaScript.
Node.js has an event-driven architecture capable of asynchronous I/O. These design choices aim to optimize throughput and scalability in Web applications with many input/output operations, as well as for real-time Web applications (e.g., real-time communication programs and browser games).”
Since Node.js can process much more requests in parallel using the single threaded I/O event loop.”
References: https://en.wikipedia.org/wiki/Node.js
Project 1 – Language Translator 
We learn how to make REST calls to an API using Postman as our REST client.
1.	Check out the demo @ https://language-translator-demo.mybluemix.net/
a.	Look at the REST call and response in the demo (Rest API and JSON tabs)
b.	We will recreate the same call and response by using Postman and the API explorer for Language translation
c.	Leave this page open, we will go back to it to get the developer documents (documentation link at the top - http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/language-translation/)
2.	Provision a Watson Language Translation Node with trainable plan (not standard), do not bind to an application (https://console.ng.bluemix.net/catalog/services/language-translation/)
a.	Click on Service Credentials, copy user name, password and url into a text document
b.	Go to API explorer (http://www.ibm.com/watson/developercloud/language-translation/api/v2/)
c.	Recreate examples from API explorer in Postman
d.	Explain how training works for custom models
3.	http://watsonttslab.mybluemix.net
a.	We can then build on this, first we can add a text box + button to the page so we do not have to go to the node-red editor to send a string to be spoken
b.	Create HTTP POST route called speak, parses request body for var called speak and sets that as msg.payload to be translated and connected to the previous flow
c.	Create HTTP POST route called translate, does the same as above excepts sends string to translate service, then sends to another TTS node configured for French, before sending to websocket
d.	Modify HTML in template, add two input fields and buttons for speak and translate, add Jquery event handlers for both buttons
 
 







Project 2 – Personality Insights App
1.	Fork and Deploy personality insights app
2.	Go through API Explorer, Use API with Postman
3.	Discuss programming models (http://www.ibm.com/watson/developercloud/doc/getting_started/gs-develop.shtml)
4.	Discuss use cases
Project 3 – Visual App
1.	Instantiate the “Internet of Things Platform Starter” Boilerplate under “catalogue”, if you haven’t already. Name your app “Node Red Apps.” This boilerplate has the latest updated Watson Service nodes in the Node Red app. 
2.	Bind the “Visual Recognition” API to your app. 
3.	Follow the instructions in this lab, use “Visual Recognition” v3, not the deprecated node. 
https://github.com/watson-developer-cloud/node-red-labs/blob/master/basic_examples/visual_recognition/README.md
 
4.	EXCEPT: 
Don’t use “Extra img URL” for 3rd node, add the function node and enter the following: 
msg.payload = msg.payload.imageurl;
return msg;
5.	
Change report node to the following: 
<h1>Visual Recognition</h1>
<p>Analyzed image: {{#result}}{{#images}}{{resolved_url}}<br/><img src="{{resolved_url}}" height='100'/></p>{{/images}}{{/result}}
<table border='1'>
    <thead><tr><th>Name</th><th>Score</th></tr></thead>
    {{#result}}
      {{#images}}
        {{#classifiers}}
          {{#classes}}
      <tr><td><b>{{class}}</b></td><td><i>{{score}}</i></td></tr>
          {{/classes}}
        {{/classifiers}}
      {{/images}}
    {{/result}}
</table>
<form  action="{{req._parsedUrl.pathname}}">
    <input type="submit" value="Try again"/>
</form>

6.	Deploy the application. 
7.	Copy and paste the URL your node red app in a new window, remove “/red” and add “/reco” to the end. 
8.	Use this image URL: http://animal-dream.com/data_images/tiger/tiger8.jpg
9.	Look under “debug” and you should see “tiger” show up. 
To view JSON: http://jsonviewer.stack.hu/
Why, When, and How
“Visual Recognition allows users to understand the contents of an image or video frame, answering the question: “What is in this image?” Submit an image, and the service returns scores for relevant classifiers representing things such as objects, events and settings. What types of images are relevant to your business? How could you benefit from understanding and organizing those images based on their contents? With Visual Recognition, users can automatically identify subjects and objects contained within the image and organize and classify these images into logical categories. Need to train Visual Recognition on specific or custom content? Easily train a new classifier by sending examples and voila! Custom image recognition!
Intended use
Need to figure out what is contained in many images, but don’t have the man-power to manually go one-by-one?
•	Organize image libraries into categories
•	Segment user interests from social media pictures
•	Find great images with specific content faster
•	Recognize custom content from images”
References: https://www.ibm.com/watson/developercloud/visual-recognition.html











