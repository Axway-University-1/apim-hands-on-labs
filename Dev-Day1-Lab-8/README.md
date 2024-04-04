# API lifecycle management using API Manager

Welcome, learners, to today's lab session focused on API lifecycle management using API Manager. In this lab, we will delve into the intricate process of managing the lifecycle of an API, a crucial aspect of modern software development and integration. Throughout this session, you will gain hands-on experience in maneuvering through the stages of API development, testing, publication, deprecation, and retirement.

As technology evolves rapidly, organizations must adapt by efficiently managing their APIs to meet consumer demands and industry standards. Through this lab, you will navigate real-world scenarios where a company aims to enhance its existing API, Stockquote, to cater to consumer requirements for retrieving historical stock quotes. By understanding the API lifecycle management process, you will be equipped with the skills necessary to orchestrate seamless transitions between API versions and ensure continued accessibility and functionality for end-users. Let's embark on this journey to master API lifecycle management and elevate your proficiency in API development and governance.

## Learning objectives

**Remembering:**
   - Recall the steps involved in managing the lifecycle of an API in API Manager.
   - List the different states an API can be in during its lifecycle, such as Develop/Configure/Test, Published, Deprecated, and Retired.

**Understanding:**
   - Explain the significance of API lifecycle management in the context of software development and integration.
   - Interpret the differences between unpublished and published APIs and understand the implications of deprecating and retiring APIs.

**Applying:**
   - Utilize API Manager to test APIs with specific users and validate their access rights.
   - Demonstrate the process of creating a new version of an API and providing access rights to internal and external users.

**Analyzing:**
   - Evaluate the access rights of different users to APIs based on their organizational roles.
   - Assess the impact of upgrading access to newer API versions on user permissions and testing capabilities.

**Creating:**
   - Design a comprehensive API lifecycle management strategy tailored to the organizational requirements of a given scenario.
   - Develop a documentation outlining best practices for API versioning, access management, and lifecycle transitions within API Manager.


## Scenario introduction

A company is exposing an API, `Stockquote v1`. The API returns the quote of a given company on the market.

API consumers would like to get the quote for a given date in addition to a given company. The company has created a new version  `Stockquote v2` and wants to expose it, with a new parameter: the quote date
<table>
    <thead>
        <tr>
            <th>Anna</th>
            <th>Dave</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Anna</b> is an internal developer, and is part of the **API Developer** Organization </td>
            <td>**Dave** is an external application developer, and is part of the **Partner** Organization</td>
        </tr>
        <tr>
            <td><img src="images/image23.png" style="text-align:center"></td>
            <td><img src="images/image24.png" style="text-align:center"> </td>
        </tr>
    </tbody>
</table>


* Both Anna and Dave have access to `Stockquote v1`, and they are both interested in using `Stockquote v2`

* Let’s see how to create a new version of Stockquote API and how to provide rights to `Stockquote v2`, to internal and external users


## Creation of an API

### API Lifecycle

![Alt text](images/image01.png)
<p style="text-align: center;">An unpublished API corresponds to the state Develop/Configure/Test</p>

**Task:**
* Test `Stockquote v1` with API Manager, with users `anna/anna` and `dave/dave`
    * Validate that Anna and Dave can test `Stockquote v1`

**Task:**
* Connect to API Manager with administrator user `apiadmin/changeme`
    * Create Backend
        * Import **Stockquotev2.json** swagger file from **/home/axway/demo/data/api_library** into the **API Development** Organization
    * Create Frontend
        * Expose the API on path `/stockquote/v2` (exposing is in the inbound tab)  
	    Best practice: always add the version to the path, to manage versions correctly
    * In the API tab, add the image **Stockquote** to the API, from **Home > demo/data/images/Stockquote.jpg**
    * Do not add any security (meaning pass through)

**Task:**
* Test `Stockquote v2` with the following parameters and user/password `anna/anna` and `dave/dave`.
    * `symbol=GOOG`
    * `date=01/01/2018`
* What happens? Why?

### Live and scheduled end-of-life

![Alt text](images/image02.png)
<p style="text-align: center;">A published API corresponds to a live API
</p>

**Task:**
* Connect to API Manager with administrator user
* First, add the security (API Key) to `Stockquote v2`
* Publish `Stockquote v2`
* Select `Stockquote v1` and Upgrade access to the newer API `Stockquote v2`
    * Deprecate `Stockquote v1`
    * Retire `Stockquote v1` in two years

**Task**
* Test `Stockquote v2` with user `dave/dave`
    * `symbol=GOOG`
    * `date=01/01/2018`
* Is Dave now able to test the API? Why?

## Solutions

* Connect to API Manager with `apiadmin/changeme`

* Go to **API > Backend API**
    * Select **New API > Import Swagger API**
    * Select the file from **/home/axway/demo/data/api_library/Stockquotev2.json**
    * Select **Organization** as **API Development**
    * Click **Import**


![Alt text](images/image25.png)

* Go to **API> Frontend API**
    * Select **New API > New API from backend API**
    * Select **Stockquote v2**, click Ok
    * In the inbound tab
        * Change `resource path` to `/stockquote/v2`
        * Select `Inbound security` as `Pass Through`
    * Click **Save**


![Alt text](images/image26.png)

* Go to the API tab
    * Change the API name to `Stockquote v2`
    * Click on **add image** and add the stockquote image from `Home > demo/data/images/Stockquote.jpg`
    * Click **Save**

![Alt text](images/image27.png)

* Go to **API> API Catalog**
    * Click on **Stockquote v2**
    * Try the method **GetQuote** with
        * `symbol=GOOG`
        * `date=01/01/2018`
    * Click **Try method**

![Alt text](images/image28.png)

The testing works with Anna, but not with Dave. Why?  
* Because a user can consume any API of his or her Organization, without any granted access

Anna and Stockquote APIs (v1 and v2) belong to the same **API Development** Organization, so it works

Dave belongs to the Organization **Partner**. So, he needs a grant access to use an API of another Organization. 

Let’s grant him access!

* Login into API manager with `apiadmin/changeme`
* Select `Stockquote v2`
* Click `Manage selected`
* Select `Grant access`
* Grant API access to `The following organizations`
* Click on `+` to add Partners organization to which **Dave** belongs

* Logout as **apiadmin**
* Login as **Dave** and check that he now has access to **Stockquote v2**

![Alt text](images/image29.png)

* Connect to API Manager with `apiadmin/changeme`
* Go to **API > Frontend API**. Open `Stockquote v2`, go to the `Inbound` tab and add `API Key` as `Inbound security`. Click **Save**
* Select `Stockquote v2` by checking the box. 
* Click on **Manage Selected** and then click **Publish**.

![Alt text](images/image30.png)

* Select `Stockquote API`

* Click **Manage selected**

* Select **Upgrade access to newer API**


![Alt text](images/image31.png)


* This opens a new window **Grant API access**. Upgrade the API to `Stockquote v2`

* Deprecate and retire `Stockquote v1` API in two years

* Click **Upgrade**

![Alt text](images/image32.png)

* Connect to API Manager with `dave/dave`
* Go to **APIs > API Catalog** and click on `Stockquote v2`
* Click `Try it` for API method `GetQuote`

![Alt text](images/image33.png)


* Select the **Stockquote application** and **KeyId** that was created for `Stockquote v1`
* Add `GOOG` for the `symbol`
* Add `01/01/2018` for the `date`
* Click **Try method**

> It works!  When upgrading access to a newer API, the solution grants the same rights for the new version than for the previous version. Dave is now allowed to test without creating a new application and credentials

![Alt text](images/image34.png)


## Conclusion

* API Manager allows to manage the full life cycle of APIs from creation - with multiple versions - to end of life
* The available status are 
    * Unpublished for development
    * Published, for live
    * Deprecated, to warn users of the end of life
    * Retired, to stop access to the API - with a rollback possibility

* API Manager is able to copy rights from one API version to another: a user doesn’t have to create a new application and credentials to use a new version of the same API




