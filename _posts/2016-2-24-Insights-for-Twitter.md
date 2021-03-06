---
layout: post
title: Insights for Twitter
permalink: /insights-for-twitter/
---

The Insights for Twitter service allows us to query Twitter to incorporate Twitter content to our applications.

Download Insights for Twitter Powerpoint Presentation [here](https://github.com/kurtcoder/twitterinsightsresources/blob/master/Insights-For-Twitter-Ley.pptx?raw=true)



In this tutorial you will deploy a sample Insights for Twitter Application in Bluemix through the use of the Devops Delivery Pipeline. You will also familiarize yourself with the service


#### Fork a Github Repository
Fork the repository that contains the application that you will deploy using the Devops Delivery Pipeline.

1. Go to [GitHub](https://github.com) and Login.

2. Go to the Github Repository [https://github.com/kurtcoder/insights-for-twitter](https://github.com/kurtcoder/insights-for-twitter)

3. Click the `Fork` button to make your own copy of the repository.

<br>

#### Create a Bluemix DevOps Project based on the Github Repository 

1. Open another tab in your web browser and login to [Bluemix DevOps] (https://hub.jazz.net)

2. Click  `Create Project` 
	
3. Name your project `insights-for-twitter`.
	
4. Click `Link to an existing GitHub repository`.  

5. Select the repository `<username>/insights-for-twitter`

6. Ensure the following options are chosen:

	||||
	|---|---|---|
	| **Private Project** | checked |
	| **Add features for Scrum development** | checked |
	| **Make this a Bluemix Project** | checked |
	| **Region** | IBM Bluemix US South |
	| **Organization** | you may leave the default selection |		
	| **Space** | dev |

	<br>

7. Click the `CREATE` button and wait for your project to be created.

#### Create a Build Stage

1. Click the `BUILD & DEPLOY` button.

2. Click the `Add Stage` button. 

3. Set the name from `My Stage` to `Build Stage`

4. On the `Input` Tab, set the following values

	||||
	|---|---|---|
	| **Input Type** | SCM Repository |
	| **Git URL** | https://github.com/your_name/insights-for-twitter.git |
	| **Branch** | master |
	| **Stage Trigger** | Run jobs whenever a change is pushed to Git |

	<br>

5. Go to the `Jobs` Tab and click `Add Job` and set `Build` as the Job type.

6. Rename `Build` to `Gradle Assemble`

7. Set the following values

	||||
	|---|---|---|
	| **Builder Type** | Gradle |		
	| **Build Shell Command** | `#!/bin/bash`<br>`gradle assemble`  |	
	| **Stop running this stage if this job fails** | checked |

	<br>

8. Click the `Save` Button.	

#### Create a Deploy Stage

1. Click the `Add Stage` Button

2. Rename `MyStage` to `Deploy Stage`

3. On the `Input` Tab, set the following values

	||||
	|---|---|---|
	| **Input Type** | Build Artifacts |
	| **Stage** | Build Stage |
	| **Job** | Gradle Assemble |
	| **Stage Trigger** | Run jobs when the previous stage is completed |

	<br>
	
4. On the `Jobs` Tab Click `Add Job` and select `Deploy`

5. Rename `Deploy` to `Cloud Foundry Push to Dev Space`.

6. Set the following values:

	||||
	|---|---|---|
	| **Deployer Type** | Cloud Foundry |		
	| **Target** | IBM Bluemix US South - https://api.ng.bluemix.net |		
	| **Organization** | you may leave the default selection |		
	| **Space** | dev |	
	| **Application Name** | blank |		
	| **Deploy Script** | `#!/bin/bash`<br> `cf push insights-for-twitter-<your_name> -m 256M -p build/libs/twitterinsights.war` |	
	| **Stop running this stage if this job fails** | checked |

	<br>

7. Click `Save`

You have created a delivery pipeline.

#### Deploy The application

1. Click the `Run Stage` icon of the `Build Stage`

	>Make sure all the stages pass before proceeding to the next step.

2. Go to the [Bluemix] (https://console.ng.bluemix.net) Website and Login.

3. Go to the `Dashboard` Tab and click the widget of your application `insights-for-twitter-<yourname>`

4. Click `Add a Service or API`

5. In the Catalog page look for the `Insights for Twitter` service and click it.

6. Rename the Service name to `Insights for Twitter - <yourname>` . Select the `Free Plan` Option in the `Selected Plan` Dropdown.

7. Click `Create`

8.  When prompted to Restage Application, press `Restage`

You have successfully deployed your Insights for Twitter Application

#### Using the Application

1. On a new tab, access your new application using the url `http://insights-for-twitter-<yourname>.mybluemix.net`

2. The first operation that the web application can do is to count the number of tweets, given a keyword e.g. `#ibm` or `binay`


Input #ibm in the textfield of `Counting # of Tweets`. The results will look like this:

```
	 {"related":{"search":{"href":"https://cdeservice.mybluemix.net:443/api/v1/messages/search?q=%23ibm"}},"search":{"results":198618}} 
```

This output which is in `JSON` format, shows the url that we used to access the Insights for Twitter Service

```
	 {"related":{"search":{"href":"https://cdeservice.mybluemix.net:443/api/v1/messages/search?q=%23ibm"}}
```

As well as the results of the query, which was to count how many tweets included the keyword

```
"search":{"results":198618}} 
```

3. The next operation that the web application can do is to search for tweets using a keyword. e.g. `#Duterte` and specifiying how many tweets regarding the keyword you want to see `1`

4. For the first text field enter `#Duterte` , for the second text field enter `1`

	>This will search for tweets which include #Duterte in its content, and display only 1.

The Result for the Query will look like this

```
{"search":{"results":6799,"current":1},"tweets":[{"cde":{"author":{"gender":"unknown","parenthood":{"isParent":"unknown","evidence":""},"location":{"country":"","city":"","state":""},"maritalStatus":{"isMarried":"unknown","evidence":""}},"content":{"sentiment":{"evidence":[{"polarity":"NEGATIVE","sentimentTerm":"NOT trust"},{"polarity":"NEGATIVE","sentimentTerm":"puppet"}],"polarity":"NEGATIVE"}}},"message":{"postedTime":"2014-12-23T03:03:18.000Z","verb":"post","link":"http://twitter.com/ericarreza/statuses/547225910999384065","inReplyTo":{"link":"http://twitter.com/iAmMomiRhay/statuses/547154097283923968"},"generator":{"displayName":"Twitter Web Client","link":"http://twitter.com"},"body":"@iAmMomiRhay @inquirerdotnet I don't trust 2 those NPA & other leftist they're puppet to Commie China #duterte should execute them. 😡😤","favoritesCount":0,"objectType":"activity","actor":{"summary":"Buy Baybayin.PH tshirt by clicking #baybayinph","image":"https://pbs.twimg.com/profile_images/511434104382844929/E6s8ZSX0_normal.jpeg","statusesCount":10121,"utcOffset":"-32400","languages":["en"],"preferredUsername":"ericarreza","displayName":"Baybayin Retro","postedTime":"2009-05-10T02:10:15.000Z","link":"http://www.twitter.com/ericarreza","verified":false,"friendsCount":2001,"twitterTimeZone":"Alaska","favoritesCount":4588,"listedCount":3,"objectType":"person","links":[{"rel":"me","href":"http://facebook.com/r1210designers"}],"location":{"displayName":"Pearl of The Orient Sea","objectType":"place"},"id":"id:twitter.com:38975279","followersCount":434},"provider":{"displayName":"Twitter","link":"http://www.twitter.com","objectType":"service"},"twitter_filter_level":"medium","twitter_entities":{"urls":[],"hashtags":[{"indices":[106,114],"text":"duterte"}],"user_mentions":[{"indices":[0,12],"screen_name":"iAmMomiRhay","id_str":"248089128","name":"rhay garcia","id":248089128},{"indices":[13,28],"screen_name":"inquirerdotnet","id_str":"15448383","name":"Inquirer Group","id":15448383}],"trends":[],"symbols":[]},"twitter_lang":"en","id":"tag:search.twitter.com,2005:547225910999384065","retweetCount":0,"gnip":{"language":{"value":"en"}},"object":{"summary":"@iAmMomiRhay @inquirerdotnet I don't trust 2 those NPA & other leftist they're puppet to Commie China #duterte should execute them. 😡😤","postedTime":"2014-12-23T03:03:18.000Z","link":"http://twitter.com/ericarreza/statuses/547225910999384065","id":"object:search.twitter.com,2005:547225910999384065","objectType":"note"}}}],"related":{"next":{"href":"https://cdeservice.mybluemix.net:443/api/v1/messages/search?q=%23Duterte&from=1&size=1"}}}

```

This output which is in `JSON` format, shows information regarding the user who tweeted the tweet and information regarding the tweet

```
{"search":{"results":6799,"current":1},"tweets":[{"cde":{"author":{"gender":"unknown","parenthood":{"isParent":"unknown","evidence":""},"location":{"country":"","city":"","state":""},"maritalStatus":{"isMarried":"unknown","evidence":""}},"content":{"sentiment":{"evidence":[{"polarity":"NEGATIVE","sentimentTerm":"NOT trust"},{"polarity":"NEGATIVE","sentimentTerm":"puppet"}],"polarity":"NEGATIVE"}}},"message":{"postedTime":"2014-12-23T03:03:18.000Z","verb":"post","link":"http://twitter.com/ericarreza/statuses/547225910999384065","inReplyTo":{"link":"http://twitter.com/iAmMomiRhay/statuses/547154097283923968"},"generator":{"displayName":"Twitter Web Client","link":"http://twitter.com"},"body":"@iAmMomiRhay @inquirerdotnet I don't trust 2 those NPA & other leftist they're puppet to Commie China #duterte should execute them. 😡😤","favoritesCount":0,"objectType":"activity","actor":{"summary":"Buy Baybayin.PH tshirt by clicking #baybayinph","image":"https://pbs.twimg.com/profile_images/511434104382844929/E6s8ZSX0_normal.jpeg","statusesCount":10121,"utcOffset":"-32400","languages":["en"],"preferredUsername":"ericarreza","displayName":"Baybayin Retro","postedTime":"2009-05-10T02:10:15.000Z","link":"http://www.twitter.com/ericarreza","verified":false,"friendsCount":2001,"twitterTimeZone":"Alaska","favoritesCount":4588,"listedCount":3,"objectType":"person","links":[{"rel":"me","href":"http://facebook.com/r1210designers"}],"location":{"displayName":"Pearl of The Orient Sea","objectType":"place"},"id":"id:twitter.com:38975279","followersCount":434},"provider":{"displayName":"Twitter","link":"http://www.twitter.com","objectType":"service"},"twitter_filter_level":"medium","twitter_entities":{"urls":[],"hashtags":[{"indices":[106,114],"text":"duterte"}],"user_mentions":[{"indices":[0,12],"screen_name":"iAmMomiRhay","id_str":"248089128","name":"rhay garcia","id":248089128},{"indices":[13,28],"screen_name":"inquirerdotnet","id_str":"15448383","name":"Inquirer Group","id":15448383}],"trends":[],"symbols":[]},"twitter_lang":"en","id":"tag:search.twitter.com,2005:547225910999384065","retweetCount":0,"gnip":{"language":{"value":"en"}},"object":{"summary":"@iAmMomiRhay @inquirerdotnet I don't trust 2 those NPA & other leftist they're puppet to Commie China #duterte should execute them. 😡😤","postedTime":"2014-12-23T03:03:18.000Z","link":"http://twitter.com/ericarreza/statuses/547225910999384065","id":"object:search.twitter.com,2005:547225910999384065","objectType":"note"}}}],


```

The output also shows the url that we used to access the Insights for Twitter Service

```
"related":{"next":{"href":"https://cdeservice.mybluemix.net:443/api/v1/messages/search?q=%23Duterte&from=1&size=1"}}}


```

#### Analyzing how the Application Works

In this tutorial, we were able to create an Insights for Twitter application which uses the operations provided by the
Insights for Twitter service.

First, in order for the application to access the service it needs to use the credentials of the service. You must login using your service credentials. It will use the credentials listed for insights-for-twitter in VCAP_SERVICES which is seen in Bluemix

````
                    JSONObject creds = (JSONObject) service.get("credentials");
                    String username = (String) creds.get("username");
                    String password = (String) creds.get("password");
                    String host = (String) creds.get("host");
                    Long port = (Long) creds.get("port");
                    String url = (String) creds.get("url");

````

To access the Insights for Twitter service, we use Endpoint URLS

	>The url given by VCAP_SERVICES looks like this
	> "url": "https://f517f432-e185-41b5-a362-145612499823:3IavoFP6dV@cdeservice.mybluemix.net"

For the count operation, this is the URL we generate

````
		String input_query = (String) request.getParameter("tQuery");
		
		String urlstring = connector.getUrl() + "/api/v1/messages/count?q=" + URLEncoder.encode(input_query, "UTF-8");
````

`input_query` refers to the value you entered in the text field.

`URLEncoder.encode` is a function which allows symbols e.g. #, (space), $ to be converted into a format that can be transmitted over the internet

`/api/v1/messages/count?q=`will be appended to the url, it specifies that we will be using the `count` operation

For the search operation, this is the URL we generate

````
		String input_query = (String) request.getParameter("tQuery");
		String input_size = (String) request.getParameter("tSize");
		
		String urlstring = connector.getUrl() + "/api/v1/messages/search?q=" + URLEncoder.encode(input_query, "UTF-8") + "&size=" + input_size;

````

`input_query` and `size` are the parameters which you entered in the text field.

	>input_query refers to a keyword you want to search
	
	>size refers to how many tweets you want displayed

`URLEncoder.encode` is a function which allows symbols e.g. #, (space), $ to be converted into a format that can be transmitted over the internet

`/api/v1/messages/search?q=` will be appended to the url, it specifies that we will be using the `search` operation


To use the Insights for Twitter service, we need to authenticate ourselves

````
String userandpass = connector.getUsername() + ":" + connector.getPassword();
		
		String basicAuthorization = "Basic " + javax.xml.bind.DatatypeConverter.printBase64Binary(userandpass.getBytes());
		
		
		 URL finalurl = new URL(urlstring);
         URLConnection urlconnection = finalurl.openConnection();
 
         urlconnection.setRequestProperty ("Authorization", basicAuthorization);

````

In order to authenticate ourselves, we use Client side Basic access authentication

An example of how it looks like is this

	> Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l

We do this by getting the username and password credentials in the VCAP Services and combining them together into one string seperated by a colon

```` String userandpass = connector.getUsername() + ":" + connector.getPassword(); ````
	
We then encoded this string using the RFC2045-MIME variant of Base64 and specify the authorization method, `Basic`

```` String basicAuthorization = "Basic " + javax.xml.bind.DatatypeConverter.printBase64Binary(userandpass.getBytes()); ````

Lastly, we request for access from the url which has the results of our query.


```` 
	URL finalurl = new URL(urlstring);
        URLConnection urlconnection = finalurl.openConnection();
 
        urlconnection.setRequestProperty ("Authorization", basicAuthorization);
	
````

####End of Tutorial

