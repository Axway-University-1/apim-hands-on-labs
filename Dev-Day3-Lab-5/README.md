# Policy Studio Lab - Mashup

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, 

## Learning objectives

At the end of this lab, you will be able to design and create an API based on the mashup of many services.


## Introduction

A mashup (or Web Service Composition) is a combination of existing Web Services to create a new service with added value.

A mashup is a key concept in Service Oriented Architecture (SOA) and Digitalization.

Today, Order Management System **OMS v1** provides a `follow order` method
This service is not optimized. OMS status is updated by batch every night, but users need data in real time. They need more information about the order; has it been paid? is it in stock? and was it shipped?

### Task

* Create a new version of API **OMS v2**

The new version will do the following :
* Validate the customer purchase (Billing backend service). If the customer has paid for the order, the service will acknowledge it
* Indicate the stock availability (OMS backend service). The service indicates if the order is in stock
* Show the delivery status (Shipping mockup service). If the order has been shipped, it will return the status OK
* Merge the 3 services and provide a status with all information

Users will try the new service with **API Portal** and **OAuth** authentication

![Alt text](images/image01.png)

### Instructions

* Create a new version of OMS API to provide an instant follow order

* New method must implement the following algorithm
```
1. Check Billing status is “OK”
2. If not, report status and a message: “Payment status is not correct”
3. Check OMS status is “OK”
4. If not, report status and a message: “Payment is OK, availability issue” 
5. Check Shipping status is “OK”
6. If not, report status and a message: “Payment and availability OK, shipping in progress”
7. If yes, report status OK, paymentDate, deliveryDate and message “Everything OK!”
```

### Some advice

This exercise uses many features we have seen, and some new features
* Think about error management from the beginning.
* Using prepared request message is the simplest solution for composition.
* Look at **Connect to URL** filter documentation to know how to make a call with TLS and HTTP Basic.
* Create a business service to import the new service into API Manager.
* Protect OMS with OAuth and test service through **API Portal**.

### Solution principles: sub-policies

There are 3 big steps to create the new service:
1. Call Billing service : use service virtualized in API Manager, lab “Policy Studio - Lab - From policy to API”
2. Call OMS backend service : 
    * **Host** : `api-env`
    * **Port** :  `5080`
    * **Path** : `/mockup/oms/v1/order`
    * **Parameter** : `orderId` as a query string, as a 9-digit number
    * **Protocol** : `HTTP`
3. Call Shipping mockup service. Use the service created in the lab titled **Policy Studio - Lab - My first mockup**

Let’s create one policy for each step (even if there is only one filter for each)

*Best practice:*
- Start main policy name with 0, to display it first
- It makes sense to prefix other policies 1, 2, 3... but only if these steps are clearly identified
- Sub-policy defined at logical level will simplify maintenance later

### Solution principles: attributes

According to specifications, the following variables are used during the process
* `status`
* `message`
* `deliveryDate`
* `paymentDate`

Let’s create a variable for each one
* `order.status`
* `order.message`
* `order.deliveryDate`
* `order.paymentDate`

*Best practice:* 
* List variables you are using when developing
* If it is not a standard attribute, use a prefix to avoid collision

### Solution principles: error management

* Policy will be designed with attributes and sub-policies
* If one sub-policy returns false, this must be sent as an error message
* Fault Handler will return a simple message using
    * `order.status`
    * `order.message`
    * `Id` (transaction id)

* Attributes used in error message need to be initialized

*Best practice:* 
* Think of error management from the beginning.
* Sending too much information is a security risk. Providing transaction Id will simplify support, without giving information about the solution

### Expected result

* A main policy calling 3 policies

* A REST business service declared in API Manager

* Test the API with API key in **API Portal**


![Alt text](images/image34.png)

## Solution



## Conclusion

