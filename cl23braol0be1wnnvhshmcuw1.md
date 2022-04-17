## Fetch Unread Emails to Slack using Slash Commands Bot

Slack is one of the most popular messaging tools. In this article, we will connect our free slack account with Gmail using Slash commands and Google Scripts to pull our unread emails. Many times we face situations where Gmail is blocked because of security in some workplaces and machines. Using this we will be able to view our emails directly in Slack. 

## Slack Account

You need to have a slack account to follow this tutorial, you can create a free account from here [Join Slack](http://slack.com/intl/en-in/)

Once we create or log in to the slack workspace, we need to get an email address where we can forward the unread emails from Gmail. 

Follow the steps from this [slack article](https://slack.com/intl/en-in/help/articles/206819278-Send-emails-to-Slack#h_01F4WE06MBF06BBHQNZ1G0H2K5)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650198597684/dOIA6ehgU.png)

## Google Script Account 

As we are going to use google script API to pull emails, please log into your google account and then go to [Google Script](https://script.google.com/home/start). 
Click on **New Project** on the top left screen.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650197124960/i9xDA2ahC.png)

A new script editing window will open, remove the dummy code and paste the below code. Save the script, and provide a name to the project. 

```
function fetchUnreadGmailAndSendToSlack() {
  var threads = GmailApp.search('is:unread');
    for (var i = 0; i < threads.length; i++) {
        console.log("found message with subject :: "+threads[i].getMessages()[0].getSubject());
        threads[i].getMessages()[0].forward('email-id-from-slack@team-name.slack.com');
        threads[i].getMessages()[0].markRead();
        console.log("Mail forwareded to slack.");
    }
   console.log("finished.");
}

function doPost(request){
  fetchUnreadGmailAndSendToSlack();
  console.log(request);
  var responseContent = '{"text": "Message Received, Bots are Working On ! "}';
  var response = ContentService.createTextOutput(responseContent);
  response.setMimeType(ContentService.MimeType.JSON);
  return response;
}
``` 

On line number 5, please change the email id to your slack email id received from the above step. 

In this code there are two methods, as Slack makes a POST request, we have created one doPost() which will receive the request and call the fetchUnreadGmailAndSendToSlack() method. It will also reply back in the slack chat with a success message, which will indicate the request is processed successfully.
fetchUnreadGmailAndSendToSlack this method will search for the unread emails using Gmail APP API. Once it finds the list, it will iterate through those emails and forward them to provided slack mail-id and then mark them as read.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650198896777/xUQrM-2xw.png)

 Now, that we are done with coding, we need to deploy this script and get the URL using which we can execute it.
Click on the Deploy button on the top right, then select New deployment. Here as it's our first deployment, we need to tell google which kind of script is this, so select the type as Web app. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650199251199/w2-A2NY_y.png)

Then write some description, select your email id in the Execute as an option, this will make sure, whenever this script is run it will use your access, and in the last drop-down select anyone under "Who has access". Click Deploy, and then authorize. 
It will ask you to then select your google account, a warning will pop up, click on advanced, and then click on your project name. 

A similar screen should come up, copy the Web app URL. Anyone with this endpoint can trigger your script. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650199653033/OVpSD1S8Q.png)

## Head Back to Slack

As we have our script which will pull the unread email, we need to create an app on Slack to access this script using our slash commands. 
 Go to this [Slack APP URL](https://api.slack.com/apps?new_app=1), click on the **Create New App** Button, select from scratch, enter details and click create.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650199965775/yiWAE0em9.png)

Now, we need to set slash commands, which will invoke our google script. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650201848845/GVP33awok.png)

Click on **Create New Command** and fill details. Text which you enter in the command box will be used to invoke this app, whereas in the Request URL enter your Google Web app Deployment URL. Add short description and hit save.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650200078746/FBzIUlFw5.png)

One Last Step is to install this app in your workspace. Under Settings, select Install App, authorize the app by selecting the workspace.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650200578753/vDq7gB1Cj.png)

Now, we are all set to pull our unread emails directly in slack. So, go to slack chat and invoke this app by typing / and then your command entered above in any chat window. In my case its **/supermanfetchemails** 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650200741022/2ZJZK-xV9.png)

You should see a message in the chat as **Message Received, Bots are Working On! **
and unread emails must have arrived from the slack bot chat.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650201368978/cAJs1QoGU.png)

Now whenever you need to find your un-read emails from Gmail, you call your own superman bot. Further customization can be done in google script, as Gmail APP Api provides multiple functions. 

**That's a wrap. Let me know your feedback on this.**


