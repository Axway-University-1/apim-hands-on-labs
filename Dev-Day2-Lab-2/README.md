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


## Solution


