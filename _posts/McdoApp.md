---
layout: post
title: MCDO Candidate Subscription Service
permalink: /MCDO/
---

Inline with the incoming election, we have created a web application hosted on Bluemix, which aids in the dissemination of news, issues, and information regarding the candidates to the citizens of the Philippines.

MCDO is a Candidate Subscription service which integrates the Twilio and PostgreSQL services. Its targeted users are the Public and Campaign Managers.

Public Users
The Public first go to the Web Application hosted by Bluemix. Then they register and choose which candidates they want to subscribe to. Subscribing to a candidate includes the user into a list of people who will be notified with news updates regarding the candidate whenever there is a news blast.

Campaign Managers
Campaign managers are registered and are certified to represent their corresponding candidates. They register on the web application and include which candidate they are managing. Through the web application, they have the ability to send information about their candidate to the public users who have subscribed to the candidate.

This application targets the candidates, campaign managers, and the voters. It enables a platform for the candidates and their campaign managers in order to update their audience with their current happenings e.g. campaign schedules, important press releases, and other messages. It also targets the voters because they get to follow the chosen candidates.

We believe that this will be an eficient way for voters to subscribe to their candidates because of the lack of good internet connection in the country. With this application, the voters would only need to use the system to register and subscribe to the candidates. After this, all updates will be sent through text message and not an internet connection.

Download MCDO Powerpoint Presentation [here](https://github.com/kurtcoder/twitterinsightsresources/blob/master/Insights-For-Twitter-Ley.pptx?raw=true)



In this tutorial you will deploy a MCDO: Candidate Subscription Web App in Bluemix.


#### Copy MCDO Sample application from Github
Copy the repository that contains the application that you will deploy.

1. Create the directory MCDOapp, then go to the created directory.

```text		
>mkdir MCDOapp
>cd MCDOapp
```

2. Clone the Github Repository with the MCDOapp from [https://github.com/kurtcoder/insights-for-twitter](https://github.com/kurtcoder/insights-for-twitter)

```text		
>git clone https://github.com/ongj/Candidatesupdate
```

3. Go to the directory containing the project.

```text		
>cd foldername
```

#### Create the Web Application using Gradle and deploy it in Bluemix using the CF tool

1. Make sure you are in the project directory
2. Use gradle to solve library dependencies and create the web application.

```text		
>gradle assemble
```

3. Login to your bluemix account to use the CF tool

```text		
> cf login -a https://api.ng.bluemix.net -s dev
```

4. Deploy  it to bluemix

```text		
> cf push MCDOapp-<yourname> -m 512M -p build/libs/twil.war
```


5. Go to the [Bluemix] (https://console.ng.bluemix.net) Website and Login.
6. Go to the `Dashboard` Tab and click the widget of your application `MCDOapp-<yourname>`
7. Click `Add a Service or API`
8. In the Catalog page look for the `Twilio` service and click it.
9. Rename the Service name to `Twilio - <yourname>` . You have to login using your Twilio account. Enter the Account SID and Auth Token.
10. Click `Create`
11. You do not need to Restage the Application when prompted because we will be adding another service.
12. Go back and click `Add a Service or API` again. 
13. In the catalog page scroll down until you see the Bluemix Labs Catalog link, click it.
14. Look for `postgresql` and click it.
15. Rename the Service to  `postgresql - <yourname>`
16. Click `Create`
17. When asked to restage the application, click the `Restage` button.

You have successfully deployed your MCDO Application

####End of Tutorial

