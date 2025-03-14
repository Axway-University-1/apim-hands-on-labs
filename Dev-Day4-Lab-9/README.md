# OAuth Lab 

| Average time required to complete this lab | 20 minutes |
| ---- | ---- |
| Lab last updated | Feb 2025 |
| Lab last tested | Feb 2025 |

In this lab, we will navigate the roles of key components such as the Resource Server (API Manager), Authorization Server (API Gateway), and Client Application (API Portal). By immersing ourselves in a hypothetical scenario of a company providing an API to external developers, we will unravel the steps involved in virtualizing APIs and configuring OAuth authentication settings. Get ready to embark on a journey that will equip you with the skills and knowledge to effectively implement OAuth authentication within API Management environments.


## 1. Learning objectives


1. **Remembering:**
   - Recall the fundamental components of OAuth authentication within API Management solutions, including the Resource Server, Authorization Server, and Client Application.
   - Identify the steps involved in configuring OAuth authentication settings, such as virtualizing APIs and granting access rights to external developers.

2. **Understanding:**
   - Explain the concept of OAuth authentication and its significance in securing API access for external developers.
   - Interpret the relationship between API Gateway, API Manager, and API Portal in the context of OAuth authentication.

3. **Applying:**
   - Utilize the provided guidelines to configure OAuth authentication settings within API Manager and API Gateway.
   - Demonstrate the ability to connect to API Portal as a Client Application and consume APIs using OAuth authentication.

4. **Analyzing:**
   - Evaluate different scenarios where OAuth authentication may be preferable over other authentication methods within API Management solutions.
   - Assess the implications of OAuth authentication settings on the security and accessibility of APIs for external developers.

5. **Creating:**
   - Design a customized OAuth authentication strategy tailored to specific organizational requirements within an API Management environment.
   - Develop a comprehensive documentation or guide outlining best practices for implementing OAuth authentication within API Management solutions.

These learning objectives encompass a range of cognitive levels, from basic recall to higher-order thinking skills, providing you with a holistic understanding of OAuth authentication in API Management.

## 2. Introduction

Let's look at a high-level example of how OAuth works with API Management solution.

![Alt text](images/image21.png)

* API  Manager as a Resource Server

* API Gateway as an Authorization Server

* API Portal as a Client Application

![Alt text](images/image22.png)

* Resource Server & Authorization Server: API Gateway & API  Manager

* Client Application to access services: API Portal



## 3. Exercise

A company wants to provide an API (called OMS) to external app developers with OAuth authentication

*Goal:* Virtualize the API and give access via OAuth to external developers with API Management products

* Virtualize the API with **API manager** with OAuth authorization
    * Use **API Manager** as the resource server
    * Use **API Gateway** as the authorization server

* Connect as an external developer to **API Portal** and consume API
    * Use **API Portal** as the Client Application

The API Administrator virtualizes the API via OAuth authentication with **API Manager** and shares rights to Organization Partners

Dave is an application developer belonging to **Partners** Organization. He browses the API Catalog, finds an interesting API (called OMS) requiring OAuth and tests it with API Portal

It is easy. Try it before looking at the solution!



## 4. Solution

### 4.1. API Manager – Inbound Authentication

* Connect to API Manager `https://api-env.demo.axway.com:8075/` as `apiadmin/changeme` 

* Use the existing `OMS V1.1` API.   
You can get some help to virtualize an API thanks to Amplify API Management demo guide

* Configure the Frontend API, Inbound tab, to use Oauth. In the popup, keep all options as default.

![Alt text](images/image24.png)

### 4.2. API Manager - Outbound Authentication

* Configure the Frontend API, outbound tab, with no authentication, then save

![Alt text](images/image25.png)

### 4.3. API Manager - Publish the API

![Alt text](images/image26.png)

### 4.4. API Manager - Access Rights

* Grant API access to the organization **Partners**

![Alt text](images/image27.png)

![Alt text](images/image28.png)

### 4.5. API Portal - Application creation

* Connect to API Portal `https://api-env.demo.axway.com` as `dave/dave` and create an application to access the API

![Alt text](images/image29.png)

* Add **OAuth** credentials in the Application **Authentication** section


![Alt text](images/image30.png)

### API Portal - Test the OMS API

* Go to **API Catalog**, using **APIs** menu item and choose OMS V1.1

![Alt text](images/image31.png)

* Click on **Methods** tab and choose Authorize.
![Alt text][images/image31.2.png]

Choose **select all** and **Authorize**

![Alt text](images/image31.2.png)

*  Select **Get** and **Try it out** and enter 123123 in the order id field and choose **Execute**
* 
![Alt text](images/image31.3.png)

* Congratulations, you have obtained the resource!

![Alt text](images/image33.png)


## 5. Fine scope management (Optional exercise)

### 5.1. API Manager – Scope configuration (Read)

* Control the scope of authorized resources with Security Profiles.

* Unpublish the API, then add new Security Profiles for READ and WRITE resources

![Alt text](images/image34.png)

### 5.2. API Manager – Scope configuration (Write)

![Alt text](images/image35.png)


### 5.3. API Manager – Scope methods

* In the **Inbound** tab, click on Advanced/Simple, and add two per-method overrides for read and submit

* Save, publish and grant access to **Partners** organization

![Alt text](images/image36.png)


### 5.4. API Portal – Check application API rights

* Connect to the **API Portal** with `dave/dave`

* Check **OMS v1** API for the use of the OMS application (unpublishing the API revokes rights for the application)

*Note : if an internal server error appears, recreate the application*

![Alt text](images/image37.png)

### 5.5. API Portal – Scope testing

* Test the API. If Dave authorizes READ resources, he will only have access to “read” method and will get a “401” “scope not valid” error for the “submit” method.

* Choose Flow: clientCredentials and select resource.READ. Dave authorizes READ resource, he will only have access to "read" method and will get an error for "write" method.
  
![Alt text](images/image39.png)
![Alt text](images/image38.png)

* If Dave authorizes WRITE resources, he will only have access to "write" method and will get a “401” “scope not valid” error for the "get" method.
* Choose Flow: clientCredentials and select resource.WRITE.Dave authorizes WRITE resources, he will only have access to “submit” method and will get an error for “read” method.

![Alt text](images/image40.png)
![Alt text](images/image41.png)



## 6. Conclusion

API Management solution allows  to easily use OAuth authentication, with API Gateway, API Manager and API Portal


[images/image31.2.png]: images/image31.1.png