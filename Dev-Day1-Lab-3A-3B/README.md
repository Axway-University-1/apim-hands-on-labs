# API Management using API Manager and API Portal


In this lab, you will perform some tasks that will help you to get yourself familiar with some of the important features of API Manager and API Portal.



## 1. Learning Objectives

At the end of this lab, you will be able to 
* Provide a bulleted list of learning objectives. Try to adhere to Bloom's taxonomy.
* Expose and publish an API from API Manager
* Manage a community of users with API Manager
* Consume an API as an Application Developer from the API Portal

## 2. Scenario

Wherever possible, we use scenarios to make learning more relevant and engaging. You will be using the following scenario for this lab.

A company wants to increase their agility and the speed of application development.

You as a developer is tasked with the following goals
* Easily virtualize an API
* Manage users and API consumption

In today’s world, companies publish APIs to increase their agility and as such the speed with which they develop new applications, thus responding to new demands of existing clients, partners and suppliers.

Gerard Lambert is the architect, designer and responsible of security in the department of system integration of the Roboulot Group. In short, it’s the person to blame if something does not work as it is supposed to (you probably saw this before…).

To optimize their business, the Roboulot Group has launched an ambitious program. The group wants to provide automated services through APIs to the partners and affiliates. The service would allow external parties:
* To process orders more quickly 
* To follow a manufacturing process using their applications

Partners are encouraged to use these services to optimize their own processes. It’s a win-win situation that facilitates commercial relationships by improving margins. 

Gerard is entrusted with the mission to enable such services through APIs. The new APIs accelerate creation of the new applications within the ecosystem of the group and that of its partners (and of course this needs to be done yesterday!). These applications should be able to easily use functionality and services from other applications.

In his role of overseeing the “APIsation” program of the company, he should make sure that the publication of the APIs is easy, and that the usage of these APIs is controlled and that their utilization does not harm the IT systems.

Gerard Lambert needs your expert knowledge to put a Portal in place that allows to expose APIs to the external parties. Ideally, he needs a solution which allows to control the usage of these APIs depending on the type of applications that are using them.

| Current situation without API Management solution | Target state using API Management with API Manager and API Portal|
| ------ | ------ |
| ![Current situation without APIM](images/WithoutAPIM.png) | ![Target state with APIM](images/WithAPIM.png) |
| In the existing system, as shown in the diagram above, consumers directly access the order management system (OMS) backend system. The consumers also do not have any means to follow-up on the order once they have made the order. | Thanks to Axway's API Management solution, the company can now secure the access to the OMS backend system. The consumers will also be able to track their order from a branded API Portal. |





## 3. High level instructions for completing this lab

1. Expose the API
    
    Virtualize the REST API so that it can be made available to a community of developers for testing.

2. Publish the API

    Update documentation, security, and implementation so that the API can by used by external partners.

3. Community management

    Show how a community allows to quickly manage the enrollment of application developers.

4. Application developer point of view

    As an application developer, interact with the API Portal to search for relevant APIs, obtain API keys and manage the application usage.




## 4. Virtual Machine Environment

#### 4.1. Login / password

If you are disconnected, click on the username “Axway”:

 ![Alt text](image.png)

Enter “axway” in the field “Password”.
Click on the button “Unlock” 
 
![Alt text](image-1.png){:centered}

#### 4.2. Start Server Components
If products are not started (you can check with the command “statusAll” anywhere from a terminal), double click the following desktop shortcut:
* “Start API Management”
* “Start Backend Services”

![Alt text](image-2.png)



#### 4.3. API Manager access
Connect to the API Manager:

* Start “Firefox” by double-clicking the icon on the desktop:

![Alt text](image-3.png)

* Click on the shortcut “API Manager” which is available in Firefox (URL: “https://api-env.demo.axway.com:8075/”).
 
![Alt text](image-4.png)

Login as administrator.
Enter the following information in the login screen:
* Enter “apiadmin” in the field “Username”
* Enter “changeme” in the field “Password”
* Click on “Login”.
* Click on the tab “API”


Some APIs are already virtualized. The goal of this scenario is to virtualize the Order Management System (OMS) of the company. 

 ![Alt text](image-5.png)

## 5 Lab solution steps

### 5.1. API Virtualization

The following points explain the virtualization process:
* The “Consumer” (on the left) calls a service “Supplier” (on the right) through the “API Management” solution.
* There are 2 connections to access the virtualized service / API
    * From the consumer to the API Management solution: “Frontend API”
    * From the API Management solution to the backend service: “Backend API”

![Alt text](image-6.png)

The virtualization of a service with the API Manager consists of creating the Backend and Frontend APIs.

#### 5.1.1. Creation of the Backend API

The “Backend API” represents the API provided by the backend system in API Manager. This “Backend API” can be created manually or by importing a file that describes a service contract.  

In this example, we are going to import a file in “Swagger” format provided by the Order Management System and which describes the service.

* Click on the tab **API**, 
* Select **Backend API** in the menu
* Click **New API**
* Select **Import Swagger API**

![Alt text](image-7.png)

You are currently in the menu which allows to create or reference an API that will be managed by the API Manager.  

In the window **Import from**,
* Keep the default value **Swagger definition file** in the field **Source**
* Click **Select file** in the field **File**

![Alt text](image-8.png)

In the menu “File Upload” that opens:
* Click the map **axway** -> **TechLab** -> **TechLabs Resources**  
    Note : Depending on the screen, it is possible that you need to use the vertical scrollbar to show the map
* In the right section, select the file **oms_v1.json** (this file describes the service)
* Click **Open**

![Alt text](image-9.png)

In the window **Import from**:
* Replace the default text with **OMSv1.1** in the field **API Name**
* Select **API Development** in the list **Organization**
* Click **Import**

![Alt text](image-10.png)

You will see a message that the API is successfully imported.
* Click **ok**

![Alt text](image-11.png)

Let’s take a look at the imported API.

Click the **OMSv1.1** API in the list (you may need to select “All” in the “Show” drop-down menu on the right)

![Alt text](image-12.png)

In the first tab **API**, you find all the general information like name, type (REST or SOAP), Base Path URL, Resource Path and a summary.

![Alt text](image-13.png)

The second tab “API Methods” shows all the available API Methods belonging to the API:
* Click **API Methods**. The OMS API provides two methods **read** and **submit**.

![Alt text](image-14.png)

In the next steps, we will use the **read** method to get details of an order.

#### 5.1.2. Creation of a public _Frontend_ API

The public API allows to define the way that the internal resource (“Backend” API) will be exposed so that it can be consumed.

Open the administration console of the API Manager (if you are disconnected, check the instructions in section 3.3)
* Select the tab **API**
* Select the sub-tab **Frontend API**
* Click **New API**
* Select **New API from backend API**

![Alt text](image-15.png)

* Select **OMSv1 1.0** in the list
* Click **OK**

![Alt text](image-16.png)

You will now see a form that allows you to create the public API.

In the tab “Inbound”,
* Select **Pass Through** in the field **Inbound Security**. This allows you to verify if the API is working without having to manage access rights. We will change it later.

![Alt text](image-17.png)

A configuration window **Pass Through Device** appears.
* Keep the default value and click **OK**

![Alt text](image-18.png)

* Click **Save**

![Alt text](image-19.png)

The API is now ready to be tested.
* Open a new tab in Firefox (blue “+” button)
* Enter the URL: `https://api-env.demo.axway.com:8065/mockup/oms/v1/order/123123`
* Hit enter on the keyboard 

![Alt text](image-20.png)

The resource is consumed and returns a value. it works!

### 5.2. Publishing the API

Now that the API has been defined and tested, it can be published.

As you’ve noticed, the virtualization of an API is simple and fast.
Some additional steps are required to allow this API to be shared with the application developers.
* Change the authentication
* Update the documentation
* Change the status of the API
* Share the API with the partners
* Put quotas in place

Let’s go back to the “Frontend API” to change the authentication mechanism:
* Go back to the page **Axway API Manager**
* Select **Frontend API** in the menu **API**
* Type oms in filter API to find it easily

![Alt text](image-21.png)

* Click **OMSv1.1**

![Alt text](image-22.png)

 In the “Inbound” tab,  
 * Select **API Key** for the field **Inbound security**, to indicate that this resource requires an API key

 ![Alt text](image-23.png)

 In a new window, “API Key Device” appears:

 ![Alt text](image-24.png)

 * Click **OK** (Leave the default options, the API key is passed in an http header)

Now we will complete information related to this API. 
* Click the **API** tab.
* Enter **Order Management System** in the field **API Summary**

![Alt text](image-25.png)

* Click **Add image**

![Alt text](image-26.png)

The menu **File Upload** opens:
* Click **Axway -> TechLab -> TechLabs Resources**
* Select **OMS.jpg**
* Click **Open**

![Alt text](image-27.png)

You should have the following screen:

![Alt text](image-28.png)

Tags allow application developers to search for APIs in the API Catalog. Let’s add one:
* At the bottom of the tab **API**, in the section **Tags**, create a new tag by clicking **“+”**  
**Note:** You may need to scroll down to see **Tags**

![Alt text](image-29.png)

* Enter **Type** in the field **Tag** 
* Enter **Corporate OMS** in the field **Values**

![Alt text](image-30.png)

The update of the **Frontend API** is now finished. 

* Click **Save** at the top of the page

![Alt text](image-31.png)

The last step consists of publishing the API from **Manage frontend API**:
* Check the box next to the **OMSv1.1** API

![Alt text](image-32.png)

* In the top menu, click **Manage selected**
* Select **Publish**

Leave the default values in the window **Publish API** that pops ups:
* Click **OK**

![Alt text](image-33.png)

The status of the API becomes **Published**. Your API is now published!

![Alt text](image-34.png)

Every API belongs to an organization. In the current example, **OMSv1** belongs to the organization **API Development**. This organization is only for internal developers.

To make the **OMSv1** API available in the **Partners** organization, we will grant access to it:
* Select a check box next to the **OMSv1** API in the **Manage frontend API** screen
* Click **Manage selected** in the top menu

![Alt text](image-35.png)

* Select **Grant access**

A new window **Grant API access** appears:
* Select **The following organizations** for the field **Grant API access to**
* Click **“+”**
* Select **Partners**
* Click **OK**

![Alt text](image-36.png)

A confirmation window “Grant access” appears:
* Click **ok**

![Alt text](image-37.png)


Now we will set quota to protect our backend servers and allocate resources between the applications. We will configure two types of quota:
* A global system quota: API Manager calculates the total amount of transactions for all the applications.
* A quota per “Application”: API Manager measures the number of transactions per application.

To limit the number of transactions on a system level (100 transactions per second):
* Select from the menu **Clients**
* Click **Default Quotas**
* Click **System**

![Alt text](image-38.png)

* Click **Add API**
* In the list, select **OMSv1.1** (you may start typing in the “Filter” text box for quick selection of an API)

![Alt text](image-39.png)

* Set the number of messages as **100**
* Set the number of seconds as **1**

Note: if these 2 values are not entered, the orange button indicates that there are still invalid fields present.

![Alt text](image-40.png)


* Click outside the field and click **Save**

![Alt text](image-41.png)

To limit the number of transactions per application (In our case, a transaction every 3 seconds):
* Click **Application Default**

![Alt text](image-42.png)

* Click **Add API**
* Select **OMSv1**

![Alt text](image-43.png)

* Set the number of messages as “1” and the number of seconds as “3”
* Click outside the field and click **Save**

![Alt text](image-44.png)

This configuration allows the API Manager to apply the following quota:
* The total amount of calls to the OMSv1 API, for all methods and all consumers, is limited to 100 messages per second. This prevents an overload of the backend system.
* By default, an application can make 1 call every 3 seconds. This allows to allocate resources between all the applications. This is the default behavior and this behavior can be overwritten per application basis.

### 5.3. Manage organizations

Until now, the scenario has been realized with the “apiadmin” account that has all rights. We have virtualized an API and executed the necessary steps to make it accessible to external partners.

Now, we will look at the management of roles with 2 different users:
* In this chapter, Renée, responsible for client relations, would like to propose APIs to the partners
* In the next chapter, we will continue with Gabriel, an external app developer, who is enrolled by Renée

We will connect with the user **Renée**. She has the role of **Organization Manager** of the organization **Partners**. This role provides him the rights to enroll new developers and manage the APIs available to the Partners organization.

Log out as the **apiadmin** user:
* Click on the menu at the top right (cog wheel)
* Click **Sign Out**

![Alt text](image-45.png)

A sign-in window appears:
* Enter **renee** as **Username** 
* Enter **renee** in **Password**
* Click **Sign in**

![Alt text](image-46.png)

* Click on the menu **Clients**

![Alt text](image-47.png)

* Click **Application Developers**.  
    * You can notice that Renée is member of the organization. She will provide a registration code to new developers so that they can enroll in the **Partners** organization. They will enroll using the subscription mechanism of the API Manager:
* Click **Organizations**
* Click on the organization **Partners**

Renée manages the organization, the APIs, the users and the applications that we will see in the following exercise.

![Alt text](image-48.png)

![Alt text](image-49.png)

The available APIs are listed for this organization. We can see the API “OMSv1.1”.  
**Note:** You may need to scroll down to see the APIs.

![Alt text](image-50.png)

Now, we need to create the registration codes that allows application developers to enroll automatically.

* Click **Generate code** in the menu **Registration Codes** with default values selected
* In the window that opens, click **Generate**

![Alt text](image-51.png)

This action creates an auto registration code, as it can be seen in the example below. This code is valid for 10 user registrations over a period of one month (here by example the 29th of June 2019). Past this date, the code will no longer be valid.

![Alt text](image-52.png)

Click in the code box, select all, copy and paste your code somewhere. We will need it later.

You can log out as Renee.


### 5.4. Application developer point of view

Renée has created a registration code.

Following an email campaign, the developers of the “Partners” organization have received an invitation to connect to the API Portal, the developer portal.

Gabriel, an application developer, uses this code to access to the API Portal. The link in his e-mail refers to: `https://api-env.demo.axway.com`.

Gabriel connects using Firefox:
* Open a new tab in Firefox (blue “+” button)
* Click on the “Portal” shortcut available in Firefox (URL: `https://api-env.demo.axway.com`)

![Alt text](image-53.png)

The following screen opens:

![Alt text](image-54.png)

* Click **Sign In**

* Click **Sign up**

In the registration screen of the API Portal:
* Enter **Gabriel** in the field **Full name**
* Enter **gabriel@demo.axway.com** in the field **Email**
* Enter **Techlabs99*** in the field **Password** 
* Enter **Techlabs99*** in the field **Confirm Password**
* In the field **Organization Code (optional)**, use the registration code obtained previously in section 5.3.
* Accept the Terms & Conditions and Privacy Policy by checking the boxes
* Click **Sign up** to register

You will see a message on the top.

![Alt text](image-55.png)

The message indicates that you will receive an activation email for the account. You will consult your email to finalize your registration in the API Portal.

You will use the Webmail interface to read the emails of Gabriel:
* Open a new tab in Firefox (blue “+” button)
* Click the shortcut **Webmail** 
* Enter **gabriel** in the field **Username**
* Enter **gabriel** in the field **Password**
* Click on the front arrow or press Enter 

![Alt text](image-56.png)

In the inbox, you see a new email:
* Click on the mail with the subject: “Registration Request”

![Alt text](image-57.png)

* Click the **Activate Account** link to complete the registration process.

![Alt text](image-58.png)

Your account is activated

Connect to the API Portal:
* Enter **gabriel@demo.axway.com** in the field **Login Name**
* Enter **Techlabs99*** in the field **Password**
* Click **Sign In**

![Alt text](image-59.png)

As you may have noticed, an application developer has fewer rights than an organization administrator or an administrator of the API Manager. The application developer uses the API Portal to:
* Look for APIs and check their documentation: **API Catalog**
* Get identification information for the applications: **Applications** 
* Check the consumption of APIs by his applications: **Monitoring**

First, let’s access the API catalog:
* The menu API Catalog should already be open. Click **APIs** if it is not the case.
* Click the **Documentation** link in **OMSv1.1** for more details

![Alt text](image-60.png)

The documentation allows an application developer to discover the functionality of an API.

The service contract of an API is available in the API Portal in Swagger 2.0 format. You can find this in the **Methods** tab.

![Alt text](image-61.png)

Gabriel wishes to get information on the GET method:
* Click **Get order**  

Looking at the description of the API method, an API key is required. The next step consists of creating one.










## Summary

The API Manager is an easy to use interface to
* Virtualize APIs in just a few steps
* Expose APIs with authentication mechanisms and quotas
* Manage APIs consumers

The API Portal is the interface for consumers to
* Self-register and self-service for user independence
* Search with filters into API Catalog and documentation
* Test API with inline Try-it
* Monitor API usage

