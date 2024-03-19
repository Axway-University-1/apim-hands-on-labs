# Authentication Lab 

| Average time required to complete this lab | 30 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, 

## Learning objectives

At the end of this lab, you will be able to 
* Integrate an authentication Policy to API Manager
* Implement a simple example of Identity Management policy

## Introduction

A company uses API Manager for app authentication
* There is no user authentication
* User authentication depends on integration

The following are the goals to be achieved:
* Continue to use API Key as before
* Have authentication with HTTP Basic on a LDAP repository


## Instructions

* Create a simple policy with two filters
    * **Authenticate API Key**
    * **HTTP Basic**

* Declare the policy in **API Manager** as an invoke policy to protect **OMS** API

* Test it with **CURL** commands


## Expected result

* A simple authentication policy

* Call the authentication policy from **API Manager**

![Alt text](images/image24.png)





## Solution

* Open **Policy Studio**

![Alt text](images/image25.png)

* Open **QuickStart** project

![Alt text](images/image26.png)

* Create a policy

![Alt text](images/image27.png)

* Add **Authenticate API Key** filter

![Alt text](images/image28.png)

* Edit filter configuration as per the screenshot below.

* Click **Finish**

![Alt text](images/image29.png)

* Add **HTTP Basic** filter on the previous filter

![Alt text](images/image30.png)

* Edit filter configuration as per the screenshot below.

* Click **Finish**

![Alt text](images/image31.png)

* Set the start filter

![Alt text](images/image32.png)


* Make the policy available to **API Manager**

![Alt text](images/image33.png)

* Deploy the policy

![Alt text](images/image34.png)

![Alt text](images/image35.png)

![Alt text](images/image36.png)

* Connect to **API Manager**  
`apiadmin/changeme`

![Alt text](images/image37.png)

* Virtualization - create a Backend with Swagger

![Alt text](images/image38.png)

* Virtualization - create a Frontend

![Alt text](images/image39.png)

* Click **Save**

![Alt text](images/image40.png)

* Select authentication mechanism and save  
If the invoke policy does not appear, refresh the browser 

![Alt text](images/image41.png)

* Create an application

![Alt text](images/image42.png)

![Alt text](images/image43.png)

![Alt text](images/image44.png)

![Alt text](images/image45.png)

![Alt text](images/image46.png)

* Add the User **Anna** in the Sharing tab

![Alt text](images/image47.png)

### Test it!

* `curl -k  https://api-env.demo.axway.com:8065/mockup/oms/v1/oms/v1/order/123123`

* `curl -k  https://api-env.demo.axway.com:8065/mockup/oms/v1/oms/v1/order/123123?KeyId=MY_KEY`

* `curl -k -u anna:anna https://api-env.demo.axway.com:8065/mockup/oms/v1/oms/v1/order/123123`

* `curl -k -u anna:anna https://api-env.demo.axway.com:8065/mockup/oms/v1/oms/v1/order/123123?KeyId=MY_KEY`


![Alt text](images/image48.png)

![Alt text](images/image49.png)

### Troubleshooting

![Alt text](images/image50.png)



## Conclusion

* API Management solution allows to implement many authentication protocols with:
    * API Manager - a simple management interface
    * Policy Studio for a lot of flexibility, with easy-to-use predefined filters