# Policy Studio Lab - Quota System

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

Welcome to today's session on API Gateway management! In this hands-on lab, we'll delve into the dynamic world of API access control and resource restriction using Axway's API Gateway. Throughout this session, you'll learn how to design and implement policies that authenticate users, enforce access quotas based on user groups, and monitor traffic effectively. By the end of this session, you'll have gained valuable insights into managing API access securely and efficiently.

In this lab, we'll start by configuring authentication policies to verify user identities using HTTP Basic filters. Next, we'll explore how to set up quota systems to limit access based on user groups, such as Gold, Silver, and Bronze. Through a series of practical exercises, you'll deploy policies that dynamically adjust access restrictions, ensuring seamless user experiences while maintaining security. Get ready to unlock the power of API Gateway management and take control of your API resources like never before!

## 1. Learning objectives

**Remembering:**
   - Recall the steps involved in configuring authentication policies, such as HTTP Basic filters, within API Gateway.
   - Recognize the significance of setting authentication policies as the initial step in controlling API access and ensuring security.

**Understanding:**
   - Explain the concept of authentication policies and their role in verifying user identities before granting access to API resources.
   - Interpret the relationship between authentication policies and access control mechanisms, such as quotas, in maintaining API security and integrity.

**Applying:**
   - Utilize the provided instructions to configure authentication policies, including HTTP Basic filters, within API Gateway.
   - Demonstrate the application of authentication policies in restricting access to API resources based on user credentials and group memberships.

**Analyzing:**
   - Evaluate different scenarios where authentication policies are essential for enforcing access control and preventing unauthorized access to APIs.
   - Assess the impact of authentication policies on API performance, scalability, and overall security posture within an API management environment.

**Creating:**
   - Design a customized authentication strategy tailored to specific organizational requirements, considering factors such as user authentication methods and access control mechanisms.



## 2. Introduction

### 2.1. Scenario

Web Services and service-oriented architectures (SOA) form an integral part of business information systems. This is the case for the Roboulot Group, a group of businesses equipped to tackle the increasingly important question of globalization.

At the Information Systems Division of the group, Peter Smith is an architect, designer, developer, debugger, and security manager. He is also a "modder" but that's another story.

To put applications in place more quickly, Peter Smith must allow existing Web Services to be used for a greater number of purposes and by a greater number of applications, and of course users, of the Roboulot Group.
The problem Peter encounters is to some extent the price of success: the web services are working so well that the number of users is constantly increasing.

Peter must now find a solution to avoid deterioration of the quality of service and the overloading of his servers.

The solution is simple: he will adapt the flow rate to the absorption capacity of the available servers. He can limit the overall number of requests per unit of time, but this will have a negative effect on the quality of service for all his users. This is perhaps an excessively dramatic solution; some users will not appreciate it. Peter Smith wishes to fine-tune the solution. He should be able to adapt the flow rate to the types of use, the applications, and the organization of the Group (and he must serve the head office first if he wants to retain his budgets).

And as always, it must be possible to develop the solution quickly and easily to be implemented in order to adapt to the available resources.

The challenges for Peter lie in the following points:
* "How to implement this efficiently without jeopardizing the existing architecture?" 
* "Given that we know how to implement quotas, is it possible to distinguish them by user profile? With what level of detail?"

Do you know how to use the API Gateway available to you to help Peter with his management, guaranteeing optimum operation, while at the same time preserving his budget.

### 2.2. Tasks

We propose the "Quota System" policy. This production involves three stages, thus offering three variants on the policy.

#### 2.2.1. Task 1: Implementation of quotas
This is the quota management policy in its basic state. We will produce the policy which restricts access to any service to one request every 5 seconds.

#### 2.2.2. Task 2: Quota policy based on authentication
In this second version of the policy, we will add authentication. If the user is recognized by the platform, they can access the service as many times as they wish. However, if the user is not recognized, the quota policy is applied, based on the restrictions described below.

#### 2.2.3. Task 3: Quota policy based on membership of a group
A user may belong to different groups. These groups may have limited access rights to certain services. 
To simulate this partitioning, we will develop the policy to take into account three levels of authorization to access the services:
* Gold level: Unlimited access;
* Silver level: Access Limited to 5 requests every 5 seconds;
* Bronze level: 1 request every 5 seconds that is the default policy for an unauthenticated user.


## 3. Solution

### 3.1. Virtual machine environment

* If you are disconnected, click on the username `Axway`

![Alt text](images/image005.png)

* Enter `axway` in the field **Password**.
* Click on the button **Unlock**

![Alt text](images/image006.png)

* If API Management is not started (you can check with the command `statusAll` anywhere from a terminal)
    * Double click the following desktop shortcut **Start API Management** 

![Alt text](images/image007.png)

* Policy Studio is the tool to configure the API Gateway.
    * Open the policy design interface by double-clicking the **Policy Studio** icon on the desktop

![Alt text](images/image008.png)

QuickStart is a way to quickly explore the API Management solution. It is based on a standard configuration with good documentation for beginners.

Let’s open the **QuickStart** project and add modifications to the configuration.

In **Policy Studio**, you will open and modify the **QuickStart** project.

* Click **QuickStart**

![Alt text](images/image009.png)

In the menu that will pop up, click **OK**, to specify no passphrase.

![Alt text](images/image010.png)

The **Policy Studio** shows the following screen

![Alt text](images/image011.png)



### 3.2. Task 1: Quota system

By the end of this section, you will have implemented restrictions on usage per unit of time: the quotas. The policy that you are going to create will limit the number of requests to the API Gateway to a single request every 5 seconds.

This is the policy that you are going to implement:

![Alt text](images/image012.png)

If you respect the quota, you will see the message `Access to service authorized`.   
You will receive an error message, `Access to service denied`, if you are exceeding your quota.

In the tree view on the left of the screen
* Expand **Policies**
* Right-click on the **TechLabs** container (*if it doesn’t exists Add Container “TechLabs” before adding the policy*)
* Select **Add Policy**

![Alt text](images/image013.png)

In the window that appears,
* For the **Name** field, enter `Quota System`
* Click **OK**.

![Alt text](images/image014.png)

To implement quota checks, you will use a filter which reacts based on a limit of use per unit of time: **Throttling**.

In the search zone, located at the right top, start entering **thro**

The **Throttling** filter appears in the **Content Filtering** section

* Drag and drop this filter on the main canvas

![Alt text](images/image015.png)

The default configuration for this filter authorizes processing one message every second.

We will configure the filter to accept the processing of one message every 5 seconds.
* Choose **Floating Time Window** as the **Rate Limit Algorithm**
* Replace the value `1` in the **every** zone with the value `5`

![Alt text](images/image016.png)

* Click **Finish**.

* To specify that this stage is the first in the sequence, right-click on the **Throttling** filter and select **Set as Start**

![Alt text](images/image017.png)

You have the following:

![Alt text](images/image018.png)

Now that the "Throttling" filter is in place, we will set the result of the request based on the current quota. 

To do this, we will use the **Set Message** and **Reflect Message** filters.
* The **Set Message** filter is used to initialize the format and the content of a message.
* The **Reflect Message** filter is used to return the message of the request. 

We will now set the content of the message in the eventuality that the quota is not reached
* Start entering **Set Message** in the search bar at the top-right hand corner.
* Select the **Set Message** filter 
* Drag and drop this filter on the **Throttling** filter.

![Alt text](images/image019.png)

In the **Configure a new 'Set Message' filter** window,
* For the **Name** field, enter `Set Message OK`
* For the **Content-Type** field, enter `text/html`
* For the **Message Body** field, enter 
```
<html>
	<body>
		Access to service authorized
	</body>
</html>
```
* Click on the **Finish** button


![Alt text](images/image020.png)

* Start entering **Reflect Message** in the search bar in the top-right.
    * Select the **Reflect Message** filter 
* Drag and drop this filter on the **Set Message OK** filter.

![Alt text](images/image021.png)

In the **Configure a new 'Reflect Message' filter** window, 
* For the **Name** field, add `Reflect Message 200`
* For the **HTTP response code status** field, enter `200`
* Click on the **Finish** button

![Alt text](images/image022.png)

We will now put in place the processing of an error message informing that the quota has been reached.
* Start entering **Set Message** in the search zone in the top-right.
* Select the **Set Message** filter 
* Drag and drop this filter on top of the **Throttling** filter.

As the **Throttling** filter already has a success path (green arrow), adding another filter will create a failure path (a red arrow).

![Alt text](images/image023.png)

In the **Configure a new 'Set Message' filter** window,
* For the **Name** field, enter `Set Message KO`
* For the **Content-Type** field, enter `text/html`
* For the **Message Body** field, enter 
    ```
    <html>
	    <body>
		    Access to service denied
	    </body>
    </html>
    ```
* Click on the **Finish** button


![Alt text](images/image024.png)

* Start entering **Reflect Message** in the search zone in the top-right.
* Select the **Reflect Message** filter
* Drag and drop this filter on top of the **Set Message KO** filter.

![Alt text](images/image025.png)

* In the **Configure a new 'Reflect Message' filter** window, 
* In the **Name** field, enter `Reflect Message 500`
* In the **HTTP response code status** field, enter `500` 
* Click on the **Finish** button

![Alt text](images/image026.png)

The **Set Response Status** filter is used to explicitly add a message in the Monitoring displays. 

If this policy proceeds correctly, it will by default be considered positive (whether or not the quota is reached).

However, if the quota is reached, the result of the policy must be an error situation in order to be highlighted in the Monitoring displays (logical and non-technical error). 

We will therefore use the **Set Response Status** filter, to raise this error result, when the **Throttling** filter detects that the quota has been reached.
* Start entering the policy name **Set Response Status** in the search zone in the top-right.
* Select the **Set Response Status** filter 
* Drag and drop this filter on top of the **Reflect Message 500** filter.

![Alt text](images/image027.png)

* In the **Configure a new 'Set Response Status' filter** window, 
* For the **Name** field, enter `Set Response Status fail`
* For the **Response Status** field, select the `Fail` radio button
* Click on the **Finish** button

![Alt text](images/image028.png)

You obtain the following result:

![Alt text](images/image029.png)


For the service to be operational, the listener of the service must be defined.

There is a shortcut to expose a policy to **Default Services** (an HTTP listener).

Click the **Add relative path** icon at bottom of the screen:

![Alt text](images/image030.png)

* For the **When a request arrives that matches the path** field, enter `/TechLabs/quota`
* Uncheck the Global policy options
* Then click **OK**

![Alt text](images/image031.png)

*Note:* the created relative path can be seen in the **Default Services** listener. Path resolvers are managed from this menu.

![Alt text](images/image032.png)

The environment is now ready to be deployed.  
To do this, you have two possibilities:
* Press **F6**.
or
* Click on the deployment icon in the top menu  

The window **Deploy** appears. You connect to the system by identifying yourself: 
* Enter `changeme` in the field **Password**
* Click **Next**

![Alt text](images/image033.png)

* In the field **Group**, select `QuickStart Group`
* Click **Next**

![Alt text](images/image034.png)

* Once the configuration has been deployed, click **Finish**

![Alt text](images/image035.png)

#### 3.2.1. Test the quota system

* To proceed with the tests, use your Firefox browser. 
* In the browser, enter the URL: `http://localhost:8080/TechLabs/quota`

![Alt text](images/image036.png)

![Alt text](images/image037.png)

* Click several times on the refresh button to simulate successive requests.

![Alt text](images/image038.png)

**Expected result:**

On the first request, the service returns a positive response. The request submitted has been accepted by the **Throttling** filter.

If the number of requests is less than one every 5 seconds, the responses returned will be `Access to service authorized`.

If the number of requests is greater than one every 5 seconds, the responses will be negative: `Access to service denied`.

![Alt text](images/image039.png)

The API Gateway Manager is the web console for the administration of the API Gateway server. It is a monitoring tool and helps API developers:
* Open a new tab by clicking **+**, then click **API Gateway Manager** shortcut.

![Alt text](images/image040.png)

* If authentication is prompted,  
Enter `admin` in the field **Username**   
Enter `changeme` in the field **Password**

![Alt text](images/image041.png)

The **Dashboard** tab displays:
* The statistics for traffic on the platform.
* The deployment topology for nodes, instances and their associated states.
* The top 5 most-used services on the server.

The **Dashboard** tab displays the total number of messages processed by the API Gateway platform. This corresponds to the total number of clicks made to simulate calls to the **Quota System** policy.

![Alt text](images/image042.png)

The positive responses are listed in **Messages passed** and the negative ones listed in **Messages Failed**.

The **Monitoring** tab offers:
* A real-time view of the statistics of the API Gateway server activity.
* These statistics are grouped into categories: System / API Services / API Methods/ Clients / Remote Hosts.

![Alt text](images/image043.png)


The **Traffic** tab is an interface dedicated to developers and administrators in order to view the details of a specific request. 

In the **Traffic** tab, it is possible to identify the requests which have been accepted (`Status: 200 OK`) and those which have been rejected (`Status: 500 Internal Server Error`)

![Alt text](images/image044.png)


### 3.3. Task 2: Quota system based on user authentication

In this scenario, we will modify the behavior of the previously created policy.
* If the user is not recognized by the API Gateway platform, the quotas rule is applied automatically.
* Otherwise, the quotas rule is not applied.
This is how the policy will look like when implemented.

![Alt text](images/image045.png)

#### 3.3.1. Create a new **Authentication** policy

We are going to isolate the identification part in an independent Policy. At the same time, you will test the reuse of policies.

We are therefore going to create a new policy named **Authentication**. This policy will authenticate the user using basic authentication (use of an identifier / password pair) when logging in.
* Return to the **Policy Studio** interface 

* Right click on the **TechLabs" container in the Axway Policy Studio explorer, on the left-hand section of the interface.

* Click on the **Add Policy**

![Alt text](images/image047.png)

In the window which appears, 
* For the **Name** field, enter `Authentication`
* Click on **OK**

![Alt text](images/image048.png)

The **HTTP Basic** filter is used to manage the basic user authentication.
* In the search zone, located at the top of the right-hand column, enter **http**
* Select the **HTTP Basic** filter
* Drag and drop this filter on the main canvas

![Alt text](images/image049.png)

Using this filter, the user authentication will be performed against a user store located on the API Gateway.

In the **Configure 'http Basic'** window, 
* Select the following in the respective fields:  
`Credential Format:` `User Name`
`Repository Name:` `Local User Store`
* Leave the **Allow client challenge** option checked
* Click **Finish**

![Alt text](images/image050.png)

* To define the start of the Policy, right-click on the **HTTP Basic** filter and select **Set as Start**.

![Alt text](images/image051.png)

You obtain the following policy, which will succeed or fail depending on whether or not the identifiers provided are valid.

![Alt text](images/image052.png)

We are now going to return to the **Quota System** policy and use the **Authentication** policy which has just been created.
* Click on the **Quota System** tab

![Alt text](images/image053.png)

* Select the **Authentication** policy in the explorer on the left.
* Drag and drop the **Authentication** policy to the canvas.

![Alt text](images/image054.png)

* In the **Configure a new 'Policy Shortcut' filter** window which appears, check that the **Authentication** policy is selected.
* Leave the default values and click **Finish**

![Alt text](images/image055.png)

We are now going to define the **Call 'Authentication'** filter as the start filter.

* Right-click on the **Call 'Authentication'** filter and select **Set as Start** in the pop-up menu. 

![Alt text](images/image056.png)

* If the authentication succeeds, there are no limits to apply, and we therefore pass directly to the positive processing of the message. In the right-hand column, select the green **Success Path** arrow, corresponding to the correct execution of the filter 
* Click on the **Call 'Authentication'** filter to position the start of the arrow, then click on the **Set message OK** filter to indicate the end of the arrow.

![Alt text](images/image057.png)

* In the right-hand column, select the red **Failure Path** arrow

* Connect the **Call 'Authentication'** filter to the **Throttling** filter in the same way.


![Alt text](images/image058.png)

The final policy diagram should look similar to the following picture.

![Alt text](images/image059.png)

The second version of the policy is now ready to be deployed
* Deploy the new configuration using the **F6** key on the keyboard.
* Use `password: changeme`

#### 3.3.2. Test the policy

* In the Internet browser, enter the URL: `http://localhost:8080/TechLabs/quota`

On the first request, the service returns an authentication request.
 
In the "Authentication Required" window,
* For the **User Name** field, enter `user1`
* For the **Password** field, enter `axway`
* Click **OK**

![Alt text](images/image060.png)

* Click several times on the "Firefox" refresh button to simulate successive requests.

![Alt text](images/image061.png)

*Expected result:*  
As the **user1** user is included in the list of users recognized by API Gateway, the **Throttling** filter does not apply to this user. Therefore, whatever the frequency of the requests, the acknowledgements returned will always be positive.

Test with an unrecognized user: test
* Close the browser and open it again to start a new session. Alternatively, open a private window
* In the Firefox browser, enter the URL: `http://localhost:8080/TechLabs/quota`
* In the **Authentication Required** window, enter the following in the respective fields:  
`User Name`: `test`
`Password`: `test`
* Click **OK**

![Alt text](images/image062.png)

* Click several times on the "Firefox" refresh button to simulate successive requests.

*Expected result:*  
As the **test** user is not included in the list of users recognized by API Gateway, the **Throttling** filter therefore applies to this user in the same way as in the previous exercise. The service returns one positive response per 5 second period, successive requests during this period will be rejected.

#### 3.3.3. Monitoring

* If necessary, run the **Firefox** browser and open the **API Gateway Manager** by clicking on the corresponding link:
* If authentication is requested, enter:  
User Name: `admin`  
Password: `changeme`
* Click **OK** 

![Alt text](images/image063.png)

We obtain three types of messages:
* Messages that passed
* Messages that failed
* Messages that caused an exception

* Click on the **Traffic** tab. The activity of the server is displayed.

![Alt text](images/image064.png)

* Select a line for which the **status** of the request is **500 Internal Server Error**, by clicking on it.
It is possible to consult the progress of the policy which has been implemented:
    1.	Authentication with the **test** user - failed
    2.	Application of the **Throttling** filter - quota exceeded
    3.	Result of the request: Access to service denied.
* In the lower part of the page, you can find the HTTP request and response information and the messages from a trace file that correspond to the failed request. Your screen should look similar to the following.

![Alt text](images/image065.png)

* Click on **Back** to return to the list of traffic

* Click a line with the **status** of the request equal to **401 Authentication Required**.


![Alt text](images/image066.png)

This result corresponds to the messages for which the request has generated a **Messages caused an exception** exception. 

An exception has been raised since the request sent by the browser to API Gateway did not have the username / password identification elements.

This behavior is identified: during the first request, the **Quota System** policy is run twice:
1.	FireFox requests the `api-env:8080/TechLabs/quota` service. The **HTTP Basic** filter reports the need for a login and a password. The policy ends by raising an exception.
2.	The **Allow client challenge** option, checked by default in the **HTTP Basic** filter, authorizes FireFox to offer the default connection window. Once you have entered the login and the password, the policy is run a second time with the identification data.


### 3.4. Task 3: Quota restriction based on the membership of a group

The objective is to develop the policy to take into account three levels of authorization for access to the services:
* `Gold` level: Unlimited access;
* `Silver` level: Access limited to 5 requests every 5 seconds;
* `Bronze` level: 1 request every 5 seconds, default right for an unrecognized user.

Close Firefox if it has not already been closed, and return to the **Policy Studio**, to the **Quota System** policy.

For the requirements of the exercise, the `Gold` and `Silver` groups have been created.

Here are the new elements of the policy (on the light background) that you are going to implement.

![Alt text](images/image067.png)

Following authentication, once the user is identified, their group must be determined. The **Check Group Membership** filter is used to check whether a user belongs to a certain group.
* In the search zone, located at the top of the right-hand column, enter **check**.
* Click on the **Check Group Membership** filter
* Then click on the green arrow connecting the **Call 'Authentication'** filter to the **Set Message OK** filter
* The **Check Group Membership** filter will then be inserted on the selected arrow.

![Alt text](images/image068.png)

In the **Configure a new 'Check Group Membership' filter** window, 
* For the `Name` field, enter `Check Group Membership Gold`
* For the `User` field, leave the pre-configured value.
* For the `Group` field, enter `Gold`
* Click `Finish`

![Alt text](images/image069.png)


* Select the **Check Group Membership** filter  
Drag and drop this filter on the **Check Group Membership Gold** filter created previously. This will create an error management branch (red arrow).

![Alt text](images/image070.png)

In the **Configure a new 'Check Group Membership' filter** window, 
* For the **Name** field, enter `Check Group Membership Silver`
* For the **User** field, leave the pre-configured value.
* For the **Group** field, enter `Silver`
* Click **Finish**

![Alt text](images/image071.png)

* In the search zone, located at the top of the right-hand column, enter **set**.  
Select the **Set Attribute Filter** filter  
Drag and drop this filter to the **Check Group Membership Silver** filter.

![Alt text](images/image072.png)

The **Set Attribute Filter** filter is used to assign a value to a variable. Here we will allocate the value corresponding to the maximum number of transactions authorized per unit of time. In the **Configure a new 'Set Attribute Filter' filter** window:
* For the **Name** field, enter `Set Attribute Limit (5)`
* For the **Attribute Name** field, enter `Limit` (be sure to respect upper/lower case)
* For the **Attribute Value** field, enter `5`
* Click on **Finish**

![Alt text](images/image073.png)

* Select the **Set Attribute Filter** filter  
Drag and drop this filter on the **Check Group Membership Silver** filter. This will create an error management branch (red arrow). If the requester identified does not belong to the Silver group, they form part of the Bronze group and are entitled to one request every 5 seconds.

![Alt text](images/image074.png)

In the **Configure a new 'Set Attribute Filter' filter** window, 
* For the **Name** field, enter `Set Attribute Limit (1)`
* For the **Attribute Name** field, enter `Limit` (be sure to respect upper/lower case)
* For the **Attribute Value** field, enter `1`
* Click **Finish**

![Alt text](images/image075.png)

* Select the green **Success Path** arrow.  
Connect the **Set Attribute Filter (1)** filter to the **Throttling** filter

![Alt text](images/image076.png)

* Select the green **Success Path** arrow.  
Connect the **Set Attribute Filter Limit (5)** filter to the **Throttling** filter

![Alt text](images/image077.png)

* Click at the top of the right-hand column on **Select** to be able to select filters on the main frame.
* Double-click on the **Throttling** filter to open its properties window.
* In the **Configure "Throttling"** window, change the value of the **Allow** field to `${Limit}` (be sure to respect upper/lower case).
* Click **Finish**

![Alt text](images/image078.png)


You will move the red **Failure Path** arrow, which starts from the **Call 'Authentication'** filter, to connect it to the **Set Attribute Filter (1)** filter
To do this:
* Click on the red arrow connecting **Call 'Authentication'** and **Throttling** filter.  

Its two ends show small black squares.
* Select the end with the arrow, and move it to the **Set Attribute Limit (1)** filter
* Your policy should look like the following.


![Alt text](images/image079.png)

The policy is now ready to be deployed.
* Press the **F6** key (`password`: `changeme`).
* Click on the **Finish** button once the deployment is completed.

#### 3.4.1. Testing

For the test requirements of this exercise, we have pre-configured in our virtual machine: 
* The following list of users

![Alt text](images/image080.png)

* And, the following groups

![Alt text](images/image081.png)

* The following users are part of the **Gold** group:

![Alt text](images/image082.png)

* The following users are part of the **Silver** group:

![Alt text](images/image083.png)

* To proceed with the tests, run a new session of the Web browser. Remember to close the previous session if it is still open, in order to reset the cache of the browser. Or, use a private window.
* Enter the URL: `http://localhost:8080/TechLabs/quota`
* On the first request, the service returns an authentication request.
* In the **Authentication Required** window, enter the following in the respective fields:  
**User Name:** `Garry` (with two “r”s)  
**Password:** `axway`

![Alt text](images/image084.png)

* Click **OK**
* Press the **F5** button several times to send successive requests.

*Expected result:* 
As the user **Garry** belongs to the **Gold** group, the **Throttling** filter does not apply. Therefore, whatever the frequency with which requests are sent, positive responses will always be returned.

* Exit the browser to reset the cache, and open a new session.
* In the browser, enter the URL: `http://localhost:8080/TechLabs/quota`
* In the **Authentication Required** window, enter the following in the respective fields:  
**User Name:** `Sarah`  
**Password:** `axway`
* Press the **F5** button several times to send successive requests.

*Expected result:* 
As the user **Sarah** belongs to the **Silver** group, the **Throttling** filter applies with the limit of 5 requests authorized per 5 second period. Therefore, if requests are sent more frequently than this, the responses returned will be negative.

* Exit the browser to reset the cache, and open a new session.
* In the **Authentication Required** window, enter the following in the respective fields:  
**User Name:** `user1`  
**Password:** `axway`
* Click **OK**

*Expected result:*
The **user1** user does not belong to the groups with privileges. They are only entitled to one request per 5 second period.

#### 3.4.2. Monitoring

* Run the **Firefox** browser and open the **API Gateway Manager** by clicking on the corresponding link:
* If authentication is requested, enter:  
**User Name:** `admin`  
**Password:** `changeme`

![Alt text](images/image085.png)

* Click on the green graph, for **Passed** transactions.  
Select a transaction in the list with subject **Garry**, for the user Garry. He is a **Gold** subscriber.  All responses are positive.


![Alt text](images/image086.png)

Delete the filter **Transaction status** to see all transactions. 

Select a transaction in the list with subject **Sarah**, for the user Sarah. She is a **Silver** subscriber. Response is negative when more than 5 requests have been submitted in the authorized time period.

![Alt text](images/image087.png)

Select a transaction in the list with subject **user1**, for the user1. He is not a subscriber. Response is negative when more than 1 request has been submitted in the authorized time period.

![Alt text](images/image088.png)

Select a transaction in the list with subject **test**, for the user test. He is an unknown user. Response is negative when more than 1 request has been submitted in the authorized time period.

![Alt text](images/image089.png)


Go to the **Traffic** tab.  
Select an element corresponding to a test with the **user1** user and for which the result has raised an exception.

![Alt text](images/image090.png)

It is possible to consult the progress of the application of the policy which has been implemented:
* 1- The result of the **Check Group Membership Gold** filter --> failed
* 2- The result of the **Check Group Membership Silver** filter --> failed
* 3- Application of the **Throttling** filter --> quota exceeded
* 4- Result of the request: Access to service denied.

![Alt text](images/image091.png)

* You can also take a look at the corresponding traces:

![Alt text](images/image092.png)

* Go to the **Events** tab  
The **Transaction** tab lists the filters for which the result has led to an exception. The **Check Group Membership** and **Throttling** exceptions following the tests with the **user1** user are clearly visible:


![Alt text](images/image093.png)

## 4. Conclusion

Congratulations! In just a few minutes, using the API Gateway, you have been able to restrict access to your resources in a simple, customized, and dynamic way, reusing elements of your existing solution.
























































