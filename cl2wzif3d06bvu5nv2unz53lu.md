## Unlimited Free Email Address using Cloudflare and your Free Custom Domain

We all have faced this issue where we need to provide our email id for registration purposes on different websites. Sometimes we think we can avoid giving our personal or business email addresses as this can result in spam emails. 

Now, on the internet, we know there are many websites that provide free temporary email addresses. No doubt those email addresses will do your job, but there are some disadvantages to them, such as they are temporary addresses so cant be used for the long term, second you need to create those addresses beforehand to fill in the website. Now, as this trick is very well known, many sites block addresses from these websites' domain names. 

There is another way to generate an unlimited Gmail email address by adding a (+) plus sign. for example - **abc+xyz@gmail.com** or **abc+123@gmail.com**, these all will go to **abc@gmail.com**. This method will work on most sites if they don't have a check on plus sign with gmail.com addresses. 

Cloudflare Trick:
We will use the free domain from the freedom website for this tutorial, if you already have a domain name registered with Cloudflare, then go to step 3.

** Step 1:**   **Get Free Domain Name: ** Go to [freenom. com](https://www.freenom.com/), and register for an account. Once login to the website, search for a domain name that is available, then select the **.tk ** option and checkout. This domain is free of cost and valid for 1 year. On the checkout page, you can change the duration from 3 months to 12 months and then proceed for checkout. You will get your free domain name now. 

![freenom.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1651989311235/X7AnSVa7t.gif align="center")

**Step 2:**  Login or create a [Cloudflare](https://dash.cloudflare.com/login) account. Add your domain name to the Cloudflare dashboard. Now, Cloudflare will search for the existing domain name record for this domain and then ask you to modify it to point to Cloudflare name servers. Copy the name servers from Cloudflare, and go to freedom, domain management and replace the name servers. You need to wait for a few minutes till Cloudflare picks the new changes.

![cloudflare-nameservers-change.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1651991340568/gHSypxLDL.gif align="left")

**Step 3:**  Now, go to the email section of Cloudflare, it will show some records are missing, you can click on a skip for now. Click on the Route tab and then click on Enable Email Routing. Cloudflare will show some options you just need to accept those recommendations and apply. Finally, it will give you an "Email Routing is enabled and routing emails." message. 


![enable-email-record.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1651992112199/_0ULGkFs0.gif align="left")

**Step 4:**  All set to create email addresses. Go to the Routes tab and scroll to the destination email address section, add your email address where you want to receive all emails for this domain. Once you verify the destination email address 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651995048178/VwUtoDH5u.png align="left")

Go to the "Catch-all address" section and enable it, click on edit and select send to option and from the next drop down select your email address which you have verified. Click Save. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651995180255/9Ud85Evvq.png align="left")

Now, you are set to use any email address from this domain. Like if you receive an email on hashnode@domainname.tk, devto@domainname.tk, or medium@domainname.tk. These all will land in your primary email address which you verified in cloudflare. 


Now, while signing up on any website, you can add any email address on that website and the email will land on your webmail.


That's a wrap. Let me know your feedback on this. Please follow for more such tricks and tutorials.


