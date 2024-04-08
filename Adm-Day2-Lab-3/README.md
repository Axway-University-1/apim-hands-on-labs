# Testing and Troubleshooting Lab 

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

Welcome to the Testing and Troubleshooting Lab! In this session, we'll delve into the critical aspects of testing and debugging APIs within the Axway API Management ecosystem. Throughout this lab, you'll gain hands-on experience in conducting various types of tests and troubleshooting techniques to ensure the reliability and functionality of APIs.

Through interactive exercises and real-world scenarios, you'll explore how to test and receive responses from different services, including StockQuote APIs, using both API Portal and API Manager interfaces. Additionally, you'll master the art of testing APIs directly from a browser and through command-line tools like Curl, equipping you with valuable skills for both manual and automated testing practices. Let's dive in and uncover the essential strategies for ensuring the seamless performance of APIs within your API Management environment!

## 1. Learning objectives

**Remembering:**
   - Recall the steps involved in testing APIs, including accessing API Management interfaces and using CURL commands.
   - Remember the parameters required for testing APIs, such as HTTP method, security settings, host, port, and path.

**Understanding:**
   - Explain the significance of testing APIs for ensuring their functionality and reliability within an API Management ecosystem.
   - Understand the differences between testing APIs from API Portal and API Manager interfaces and through command-line tools like Curl.

**Applying:**
   - Apply the provided guidelines to test the Stockquote API using both API Portal and API Manager interfaces.
   - Demonstrate the ability to conduct API testing from a browser and through Curl commands, applying the appropriate parameters.

**Analyzing:**
   - Evaluate the results of API testing to identify potential issues or discrepancies in API performance.
   - Analyze the transaction details in API Gateway Manager to troubleshoot and resolve API-related issues effectively.

**Creating:**
   - Design a comprehensive API testing strategy tailored to specific organizational requirements, considering factors such as security, performance, and scalability.
   - Develop documentation outlining best practices for API testing and troubleshooting within an API Management environment.

## 2. Exercise

### 2.1. API testing

#### 2.1.1. Test from API Management interfaces

**StockQuote** is a trading API providing the value of a company stock

Test the `GET` method of **StockQuote**, for the company Google, meaning with parameter `symbol = GOOG`. Get a positive response

*Note*: Stockquote is running on the Backend Server. Backend services must be started

**With API Portal**

* Connect with `anna/anna` to **API Portal** and test **Stockquote** API

**With API Manager**

* If **API Portal** is not present, you have to know how to use **API Manager**
* It works exactly like **API Portal**
* Connect with `anna/anna` to **API Manager** and test Stockquote API


#### 2.1.2. Test from a browser

The **API Gateway** has an API to test the connection to an API Gateway instance called `healthcheck`.

Test the `healthcheck` API with the following parameters
* Method: `GET`
* Security: `HTTP`
* Host: `api-env`
* Port: `8080`
* Path: `healthcheck`


#### 2.1.3. Test using Curl from command line

Curl basics for HTTP

* Syntax : curl [options] url

Options :
* `-X`/--request HTTP verb: GET, POST PUT, DELETE
* `-H`/--header  : header, e.g. `-H “keyId: YTphB”`. Multiple authorized
* `-u`/--user  `<user:password>`: send user and password in HTTP Basic
* `-d`/--data: payload. Prefix by @ to load a file. Use --data-binary if required
* `-k`/--insecure:  validates any HTTPS certificate
* `-v`/-- verbose: more talkative for debugging purposes

See `man curl` for more info.

**Task**

Test the healthcheck API with a CURL command and the following parameters
* Method: `GET`
* Security: `HTTP`
* Host: `api-env`
* Port: `8080`
* Path: `healthcheck`

**Task**

Test the Stockquote API with a CURL command and the following parameters
* Method: `GET`
* Security: `HTTPS`
* Host: `api-env`
* Port: `8065`
* Path: `/stockquote/rest`
* Parameter: `symbol= GOOG`
* KeyId: get the apikey from an application in API Portal or API Manager

**Task**

Test the Stockpurchase API with a CURL command and the following parameters
* Method: `POST`
* Security: `HTTP`
* Host: `api-env`
* Port: `5080`
* Path: `/mockup/stockpurchase/rest`
* Parameter: `symbol = GOOG`
* Data to provide in the request body: `{“buyStockSymbol” : ”1”}`



### 2.2. Activity troubleshooting

* Connect to **API Gateway Manager** to follow transactions
    * `https://api-env.demo.axway.com:8090/` with user/password: `admin/changeme` 

* Look at the dashboard and see traffic overview: which are the calls?

* Click on the messages in the graph to see transaction details

* Click on a request and see HTTP request and response

![Alt text](images/image23.png)

![Alt text](images/image24.png)

## 3. Solutions

### 3.1. Test from API Management interfaces - API Portal

* Connect to **API Portal** with `anna/anna`:   
`https://api-env.demo.axway.com/`

* In **Applications** tab, create an application to define rights for API Stockquote called **Stockquote app**

* Select **Stockquote API** and click **Next**

* Click **Save**

![Alt text](images/image25.png)

![Alt text](images/image26.png)

* Open and edit the application you just created

* In the authentication tab, generate an API Key

* Go to the API tab. From the **API Catalog**, test the API

![Alt text](images/image27.png)

![Alt text](images/image28.png)

* Add the query parameter `GOOG` for the `symbol` and execute the Get method 

![Alt text](images/image30.png)


* See the 200 OK result, and the response headers and body. 

*If the result is not 200 OK, check that backend services are started*

![Alt text](images/image31.png)

![Alt text](images/image32.png)

### 3.2. Test from API Management interfaces - API Manager

* Connect to **API Manager** with `anna/anna`:  
`https://api-env.demo.axway.com:8075/`

* Go to **Clients --> Applications** and create a new application called **Stockquote application**

* Add API access for `Stockquote`

* Click **Create** to save the application

![Alt text](images/image33.png)

* Go to the **Authentication** tab

* Click on **New API Key**

* Add `*` for javascript origins

![Alt text](images/image34.png)

* Go to **API --> API Catalog** and click on **Stockquote**

* Click **Try it** for API method `GetQuote`

![Alt text](images/image35.png)

* Select the application and **keyId** you have just created

* Add `GOOG` for the symbol

* Click **Try method**

![Alt text](images/image36.png)

### 3.3. Test from your browser

* Type `http://api-env:8080/healthcheck` in a browser


![Alt text](images/image39.png)


### 3.4. Test using Curl from command line

#### 3.4.1. Healthcheck
```
curl http://api-env:8080/healthcheck
```

Result:
```
<status>ok</status>
```

#### 3.4.2. Stockquote

```
curl -k -H "KeyId:e315a8b5-45f6-4f96-b20a-0b586a2a96c6" https://api-env.demo.axway.com:8065/stockquote/rest?symbol=GOOG
```

Result:
![Alt text](images/image40.png)



## 4. Conclusion

We used the following to test APIs:
    * CURL commands for unit testing or automation
    * **API Portal** and **API Manager** with interfaces to try APIs

**API Gateway Manager** offers monitoring dashboards and precious troubleshooting information
