# API Management using API Manager and API Portal


In this lab, you will perform some tasks that will help you to get yourself familiar with some of the important features of API Manager and API Portal.



## Learning Objectives

At the end of this lab, you will be able to 
* Provide a bulleted list of learning objectives. Try to adhere to Bloom's taxonomy.
* Expose and publish an API from API Manager
* Manage a community of users with API Manager
* Consume an API as an Application Developer from the API Portal

## Scenario

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





## High level instructions for completing this lab

1. Expose the API
    
    Virtualize the REST API so that it can be made available to a community of developers for testing.

2. Publish the API

    Update documentation, security, and implementation so that the API can by used by external partners.

3. Community management

    Show how a community allows to quickly manage the enrollment of application developers.

4. Application developer point of view

    As an application developer, interact with the API Portal to search for relevant APIs, obtain API keys and manage the application usage.


## Detailed solution steps

### Virtual Machine Environment

#### Login / password

If you are disconnected, click on the username “Axway”:

 ![Alt text](image.png)

Enter “axway” in the field “Password”.
Click on the button “Unlock” 
 
![Alt text](image-1.png){:centered}

#### Start Server Components
If products are not started (you can check with the command “statusAll” anywhere from a terminal), double click the following desktop shortcut:
* “Start API Management”
* “Start Backend Services”

![Alt text](image-2.png)



#### API Manager access
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

### Lab solution steps

#### API Virtualization

The following points explain the virtualization process:
* The “Consumer” (on the left) calls a service “Supplier” (on the right) through the “API Management” solution.
* There are 2 connections to access the virtualized service / API
    * From the consumer to the API Management solution: “Frontend API”
    * From the API Management solution to the backend service: “Backend API”

![Alt text](image-6.png)

The virtualization of a service with the API Manager consists of creating the Backend and Frontend APIs.

**Creation of the Backend API**

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

**Creation of a public _Frontend_ API**

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

#### Publishing the API

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

