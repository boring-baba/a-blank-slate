## Twitter Bot which tweets Mars Photos

Hi! In this article, we will build a simple Twitter bot with Python, which will use NASA Open source API to tweet Mars Image every 1 hour. I have built this Bot and hosted it on Heroku and it's online for the past few months. You can view it here [Mars Image Bot](https://twitter.com/ImageMars). So, follow along, as I detail below the entire process.

**Step 1: Getting Credentials from NASA Open API**

As we are going to pull our Images from NASA Open source API, which in turn gets these Images from Mars Rover. So, let's first visit https://api.nasa.gov/, Here we have to enter few details, and it will give us an API Key to access its APIs. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633268342669/T15bU5RoL.png)

After entering all details, you should see the below screen, where API Key will be shown, please note this carefully, we will need it.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633268600733/kMnKk5-5B.png)

Now, from the menu, select Browse APIs and enter Mars in the search box, you should see all mars related APIs.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633268715422/RUXdBFtaq.png)

Now, we are going to use the below API, which sends us random Image Data every time we change the SOL number.

https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=12&api_key=DEMO_KEY

Replace the DEMO_KEY with your API Key.

This Endpoint returns a Photos Array, which contains all information. we will be traversing it and finding the Image Endpoint. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633268891214/LWD78mWGA.png)

Okay, So we have all the info which we needed from NASA.

**Step 2: Code our Python Bot**

We will first get the Twitter API keys, for that go to this URL  [Developer Portal](https://developer.twitter.com/en/portal/dashboard) and follow the process, which is self-explanatory. In the end, you should have your Access Key and Consumer Key. (Do let me know in the comments if you face any issues.)

Let's start coding. 😈

First Lets import the **tweepy** and other libraries, and set the Twitter keys in a variable. I have used config variables, as I am going to deploy it to a Server Later on, you can directly assign the values, for local development.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633269617128/_LTNx7tKQ.png)

Now, try to make a connection with Twitter, If all goes well you should see the "Connection Done!" message, in the terminal.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633269088073/HhLW4UY__.png)

Now, as we are connected to Twitter, let's try to pull the Image from NASA API, which we are going to use. First, we are getting the current date and time, and printing it out. Next, we are trying to fetch a random Integer, if you remember in NASA API, we need to pass a random SOL. So, we will add this number in the API Url, and make a get request. If the request code is 200, we will start reading the response, or else will print an error message. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633270094814/LsSzSeA-h.png)

As our Image URL is in the photos array, we will save this array in photos_array, and as you can see in the response, there are multiple images object in the array, so let's pick a random object from the array by again using the random library. 
Once we found the Image, pass the message and image to another function, from where we will actually update the Twitter status.



![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633270528687/-ScuqlJlN.png)


This function is very simple, it makes a web call to the Image URL and then pulls it. Further, it uses the below method of tweepy library to update Twitter status.

```
api.update_with_media(filename, status=message)
``` 

Now, if you have followed all these steps and call the **get_random_image_from_nasa** function, you should be able to tweet an image, but let's schedule it to run every one hour.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633270965994/ulTzWYp89.png)


Here, we are using, schedule library, to run the above function every hour. 


Congrats!, now your bot is working.

Let me know if you want me to write about how to host this bot to Heroku and run free for life. 🐶

Github Repo URL - https://github.com/a-blank-slate/mars-image-tweeting-bot/blob/main/tweet.py


Thanks! for reading this. 



