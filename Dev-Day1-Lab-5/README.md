# API Testing

| Average time required to complete this lab | 30 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

Welcome to the API Testing lab! In this session, we will delve into the essential aspects of API testing using API Manager and API Portal. This hands-on experience will equip you with the knowledge and skills necessary to effectively test APIs, a crucial aspect of modern software development. Throughout this lab, you will not only learn how to test APIs using API Management interfaces but also explore other common methods such as browser testing, and command-line testing.

By the end of this session, you will have a solid understanding of how to test APIs from various platforms and interfaces. Whether you're testing from the API Portal, API Manager, your browser, or the command line, you will gain valuable insights into each method's advantages and limitations. Additionally, you will discover how API Gateway Manager can be utilized to monitor transactions and troubleshoot any issues that may arise during API testing. Get ready to dive into the world of API testing and enhance your skills as a developer!

## 1. Learning Objectives

**Remembering:**
   - Recall the steps involved in testing APIs from various platforms and interfaces, including API Portal, API Manager, browser, and command line.
   - Remember the syntax and options for using CURL commands to test APIs, including HTTP verbs, headers, data payloads, and security options.

**Understanding:**
   - Explain the significance of API testing in the software development lifecycle and its role in ensuring the reliability and functionality of APIs.
   - Understand the purpose and function of API Gateway Manager in monitoring transactions and troubleshooting issues related to API testing.

**Applying:**
   - Utilize the provided guidelines to create applications and define rights for API testing within API Portal and API Manager interfaces.
   - Apply the knowledge gained to connect to API Portal and API Manager as a user and perform API testing tasks, such as testing the Stockquote API.

**Analyzing:**
   - Evaluate the effectiveness of different API testing methods, including their advantages and limitations, in ensuring the quality and performance of APIs.
   - Analyze transaction data in API Gateway Manager to identify patterns, trends, and potential issues in API usage and performance.

**Creating:**
   - Design a comprehensive API testing strategy tailored to specific project requirements and constraints, considering factors such as resource availability, time constraints, and project scope.


## 2. Test from API Management interfaces

### 2.1. Try-out API method - from API Portal and API Manager

StockQuote is a trading API providing the value of a company stock

**Task**: Test the GET method of Stockquote, for the company Google, meaning with parameter `symbol = GOOG`. Get a positive response
* Note : Stockquote is running on the Backend Server, backend services must be started

#### 2.1.1 With API Portal

* Connect with `anna/anna` to API Portal and test Stockquote API

#### 2.1.2. With API Manager

* If API Portal is not present, you have to know how to use API Manager
* It works exactly like API Portal
* Connect with `anna/anna` to API Manager and test Stockquote API

## 3. Test from Postman

**Task**: Test the Stockquote API with Postman.

* Open Postman 
* Invoke `https://api-env.demo.axway.com:8065/stockquote/rest?symbol=GOOG`
* Set the header `KeyId=<API key from API Manager or Portal>`

![Alt text](images/image22.png)

![Alt text](images/image23.png)

## 4. Test from your browser

The API Gateway has an API to test the connection to an API Gateway instance called healthcheck.

**Task**: Test the healthcheck API with the following parameters
* **Method:** `GET`
* **Security:** `HTTP`
* **Host:** `api-env`
* **Port:** `8080`
* **Path:** `healthcheck`

## 5. Test from the command line

* Syntax : `curl [options] url`
* Options :
    * **-X HTTP verb:** GET, POST PUT, DELETE
    * **-H "--header: header"** e.g. `-H “keyId: YTphB”`
    * **-u `<user:password>`**: send user and password over HTTP Basic
    * **-d data payload**. Prefix by @ to load a file. Use `--data-binary` if required
    * **-k --insecure**:  validates any HTTPS certificate
    * **-v -- verbose**: used for debugging purposes

* Type `man curl` in the terminal for more info

**Task**: Test the healthcheck API with a CURL command and the following parameters
* **Method:** `GET`
* **Security:** `HTTP`
* **Host:** `api-env`
* **Port:** `8080`
* **Path:** `healthcheck`


**Task**: Test the Stockquote API with a CURL command and the following parameters
* **Method:** `GET`
* **Security:** `HTTPS`
* **Host:** `api-env`
* **Port:** `8065`
* **Path:** `/stockquote/rest`
* **Parameter:** `symbol=GOOG`
* **KeyId:** `<get the apikey from an application in API Portal or API>`Manager

**Task**: Test the Stockpurchase API with a CURL command and the following parameters
* **Method:** `POST`
* **Security:** `HTTP`
* **Host:** `api-env`
* **Port:** `5080`
* **Path:** `/mockup/stockpurchase/rest`
* **Parameter:** `symbol=GOOG`
* **Data to provide in the request body:**  `{“buyStockSymbol” : ”1”}`


## 6. Activity troubleshooting 

* Connect to API Gateway Manager to follow transactions  
    `https://api-env.demo.axway.com:8090/` with user/password : `admin/changeme`
* Look at the dashboard and see traffic overview: which are the calls?
* Click on the messages in the graph to see transaction details
    * Click on a request and see HTTP request and response

![Alt text](images/image26.png)

![Alt text](images/image25.png)

## 7. Solutions

### 7.1. Test from API Management interfaces - API Portal

* Connect to API Portal with `anna/anna`: `https://api-env.demo.axway.com/`
* In Applications tab, create an application to define rights for API Stockquote called `Stockquote app`
* Select Stockquote API and click **Next**

![Alt text](images/image27.png)

* Scroll down to **Authentication**
* Under API Keys, click **Generate**
* Click **Save**

![Alt text](images/image28.png)

* Go to the APIs tab. 
* From the API Catalog, test the API from the **Methods** tab

![Alt text](images/image29.png)

* From the **Security method** dropdown, select the Stockquote app key that you generated previously.

![Alt text](images/image30.png)

* Click on **Try it out** under the **GET** method
* Add the query parameter **GOOG** for the symbol and execute the Get method

![Alt text](images/image31.png)

* See the `200 OK` result, and the response headers and body. 

If the result is not 200 OK, check that backend services have been started.

![Alt text](images/image32.png)

### 7.2. Test from API Management interfaces - API Manager

* Connect to API Manager with `anna/anna`: `https://api-env.demo.axway.com:8075/`

* Go to **Clients > Applications** and create a new application named  **Stockquote application**

* Add API access for **Stockquote** by checking the checkbox

* Click **Create** to save the application

![Alt text](images/image33.png)

* Go to the **Authentication** tab
* Click on **New API Key**
* Click on **Edit**
* Add `*` for javascript origins
* Click **Save**

![Alt text](images/image34.png)

* Go to **API > API Catalog** and click on **Stockquote**
* Click **Try it** for API method **GetQuote**

![Alt text](images/image35.png)

* Select the **Application** and **KeyId** you have just created
* Add **GOOG** for the symbol
* Click **Try method**

![Alt text](images/image36.png)

### 7.3. Test from a browser

* Type `http://api-env:8080/healthcheck` in a browser

![Alt text](images/image37.png)

### 7.4. Test from the command line

* Type `curl http://api-env:8080/healthcheck` in the terminal

    * You should see the result:  
    `<status>ok</status>`

* Type `curl -k -H "KeyId:<API_Key>" https://api-env.demo.axway.com:8065/stockquote/rest?symbol=GOOG` in the terminal

    * You should see the result:
    ![Alt text](images/image38.png)

* Type `curl -k -H "Content-Type: application/json" -X POST --data '{“buyStockSymbol” : ”1”}' http://api-env.demo.axway.com:5080/mockup/stockpurchase/rest?symbol=GOOG` in the terminal

    * You should see the result:  
    `{"OrderResult": "Stockquote purchased",
  "Stock": “GOOG"}`


## 8. Conclusion

You now know how to test the APIs using API Portal and API Manager. You can also now use CURL commands for unit testing or automation of testing.

API Gateway Manager can be used to monitor dashboards and troubleshoot issues.








