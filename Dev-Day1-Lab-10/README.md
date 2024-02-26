# API Testing using API Portal

In this lab, you will explore some of the basic features of API Portal in detail. 

**Task**:  
Test API `Stockquote v2`` with API Portal and user gabriel
* Modify the application Gabriel’s shop to use Stockquote
Test API Stockquote v2 with:
    * symbol=GOOG
    * date=01/01/2018

**Task**:
Observe HTTP error responses

**Task**:
Observe CURL example

**Task**:
Download the API Swagger definition

## Solutions

* Connect to the API Portal with user gabriel
* Enter `gabriel@demo.axway.com` in the field `Login Name`
* Enter `Techlabs99*` in the field `Password`
* Click **Sign In**

![Alt text](images/image22.png)

* Edit the application `Gabriel’s shop` and add API `Stockquote v2`
* Click **Save** to apply changes

![Alt text](images/image23.png)


* From the **APIs** tab, test the API for **Stockquote v2**
* Select an API Key and test the API 
    * with `symbol=GOOG`
    * `date=01/01/2018`

![Alt text](images/image25.png)

* See the result of the call: `200 OK`

![Alt text](images/image26.png)

* Look at the explanation of HTTP responses

![Alt text](images/image28.png)

* See the corresponding `CURL` command

![Alt text](images/image27.png)

* Download the API Swagger definition


![Alt text](images/image29.png)





