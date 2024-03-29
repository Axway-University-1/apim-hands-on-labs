# Policy Studio Lab - My first mockup

In this lab, 

## 1. Learning objectives

At the end of this lab, you will be able to 
* Use Policy Studio interface and explore the various filters
* Create policies using Policy Studio
* Create a mockup service

## Introduction
### What is a mockup?

* In manufacturing and design, a mockup is a model of a design or device, used for teaching, demonstration, design evaluation, promotion, etc.

* In API context, it is used to describe a server emulating a back-end behavior

* It is often used in development to avoid technical or organizational impacts

### Scenario

* The goal of the whole exercise suite is to improve the way Company orders are followed

* The shipping partner provides an order shipping status via API

* To avoid test impact during development phase, we will simulate the partner server response: by creating a mockup

#### What the company is trying to achieve?

![Alt text](images/image01.png)

#### How we are going to test partner services without impact?

![Alt text](images/image02.png)


## Tasks

### Instructions to develop an API

* Create an API (Policy) that implements a specific logic

* Associate a path to the policy

* Deploy the configuration

### Service definition - request/response

* The mockup is hosted in API Management solution
    * In this case, in the same API Gateway instance

* Request :
    * Request to shipping partner: 	`GET /supplier/delivery`
    * If there are additional parameters to the request, the service will not take them into account and will provide the same response  
	For example : `GET /supplier/delivery?id=${id}`, with **id** for the **order id**

* Response :
    * Response from shipping partner:
    ```json 
    {  "status" : "OK",
        "deliveryDate" : "Jan 1, 2016 0:00:01 AM"}

Before looking at solution in next section, try to think about what is required for a mockup
* Expose a service
* Accept a request
* Provide a consistent response

*Hint:* The simplest mockup policy requires only 2 filters

### Step-by-step instructions

* Create an API (Policy) that implements a specific logic
* Create a container called **Training**
* Create a sub container called **Shipping**
* Create a policy called **ShippingMockup**
* Add 2 filters to the policy (see next slide for complete path and policy implemented)
    * 1 filter to create the response body
    * 1 filter to set the HTTP response code to `200`
* Associate a path to the policy to accept requests

* Deploy the configuration

* Test the new service with a curl or a web browser

### Expected result

* A simple service with a predefined response

![Alt text](images/image35.png)

## Solution

### Open QuickStart project

* Open Policy Studio
    * Double click the Policy Studio icon on the desktop
* Open the **QuickStart** project
    * Under **Recent Projects**, click on the **QuickStart** project
    * Click **OK** on the **Passphrase** popup box, leaving the Passphrase blank.

![Alt text](images/image36.png)
![Alt text](images/image37.png)

### Create containers and policies

* Create container named **Training**
    * Right-click on **Policies**
    * Select **Add container** and name it **Training**

* Create sub-container named **Shipping**
    * Right-click on the new **Training** container
    * Select **Add container** and name it **Shipping**

* Create policy **ShippingMockup**
    * Right-click on new container
    * Select **Add policy** and name it **ShippingMockup**
    * Leave the category and description as is

![Alt text](images/image38.png)


### Create filters

* Open policy by double-clicking
* Type `set` to search for filter `Set Message`
* Click on **Set Message** and drag in center of policy
* Drop it on the policy canvas

![Alt text](images/image39.png)

### Set message

* Type content type `application/json`

* Copy paste the JSON message below in **Message Body**
```json 
{
 "status":"OK,
 "deliveryDate":"Jan 1, 2021 0:00:01 AM"
}
```

* Click on **Finish**

![Alt text](images/image40.png)

### Reflect message

* Type **refl** to search for filter **Reflect Message**
* Click on **Reflect Message** and drag and drop on top of filter **Set Message**
* Drop it on top of the **Set Message** filter to link it automatically

![Alt text](images/image41.png)

* Set response code to `200`

* Click on **Finish**

![Alt text](images/image42.png)

### Set as start

* Select **Set Message** filter and right-click

* Execute **Set as Start**

![Alt text](images/image43.png)


### Expose the service

* Expose service by clicking on **Add relative path**

* On new panel use the path `/supplier/delivery`

* Uncheck Global policies links

* Click **OK**

![Alt text](images/image44.png)

![Alt text](images/image45.png)

### Deploy the configuration

* Deploy either by
    * Clicking on deploy button, or
    * Using F6 shortcut

![Alt text](images/image46.png)

* Add default username and password: `admin/changeme`
* Click **Next**

![Alt text](images/image47.png)

* Click **Next** to deploy on default group (QuickStart)

![Alt text](images/image48.png)

* After successful deployment, click on **Finish**

![Alt text](images/image49.png)


### Testing

From your favorite browser, call the newly created API with a URL similar to the following:

`http://api-env:8080/supplier/delivery?id=123123`



![Alt text](images/image50.png)

## Conclusion

* This is a perfectly valid mockup…

* … but not a good API
    * No business logic; content is static
    * It accepts parameters but does not check it or use it
    * No concern about identity or protection
    * No documentation

* Keep mockup simple: main purpose is for testing

* Policy Studio allows to create simple services with preconfigured filters
You created a mockup service with just 2 filters!







