# APIM Installation Lab     


| Average time required to complete this lab | 60 minutes    |
| ---- | ---- |
| Lab last updated | January 2025 |
| Lab last tested | January 2025 |

Welcome to the APIM Installation Lab! In this hands-on session, we'll delve into the installation process of the Axway API Management (APIM) solution. By the end of this lab, you'll gain the essential skills to install APIM using the QuickStart method and understand its implications. Whether you're a beginner exploring APIM or aiming to automate installations, this lab provides a foundational understanding that sets the stage for your journey with APIM.

## Index
- [1. Learning Objectives](#1-learning-objectives)
- [2. Introduction](#2-introduction)
- [3. Attended Installation](#3-attended-installation)
- [4. Unattended Installation](#4-unattended-installation)
- [5. Conclusion](#5-conclusion)




## 1. Learning objectives

**Understanding:**
   - Explain the installation modes available for Axway API Management (APIM), distinguishing between Attended and Unattended modes.
   - Interpret the significance of prerequisites such as user credentials, installation kit, and necessary components in the APIM installation process.

**Applying:**
   - Utilize the provided instructions to execute the installation process of APIM using the QuickStart method, either through a graphical user interface or command line interface.
   - Demonstrate proficiency in selecting components and configuring settings during the APIM installation process.

**Analyzing:**
   - Evaluate the suitability of QuickStart for APIM installation in different environments, considering factors such as development versus production setups.
   - Analyze the implications of using QuickStart for APIM installation on post-installation steps and overall system stability.

**Creating:**
   - Design a customized installation strategy for APIM tailored to specific organizational requirements, considering scalability, security, and automation.
   - Develop a comprehensive documentation or guide outlining best practices for APIM installation, including pre-requisites, installation steps, and post-installation checks.

## 2. Introduction

Throughout this session, we'll focus on setting up APIM in a development environment on Linux, emphasizing simplicity and ease of installation. You'll learn how to execute basic commands like start, stop, and check status, crucial for managing APIM components such as Admin Node Manager, API Gateway Instance, and Cassandra. Let's dive in and get started with the installation process, laying the groundwork for your exploration into the world of API Management.

### 2.1. Installation mode

#### 2.1.1. Attended

With UI or command line

![Alt text](images/image16.png)


#### 2.1.2. Unattended

With command line, used for automation

![Alt text](images/image17.png)


* Lab scope is the following
    * Dev environment
    * On Linux, with default rights, no firewall
    * Done by yourself, in the next few minutes!

* Concretely it means using **QuickStart**. 
    * So, it is not production ready. We keep it simple for now.

### 2.2. Lab pre-requisites

* User:   
`axway/axway`

* Installation kit:
    * Installer : `/home/axway/Desktop/APIGateway_7.7.<releasedate>_Install_linux-x86-64_BN<buildnumber>.run`
    * License(s) : `/home/axway/demo/data/licenses/classic`

* Installation folder:  
`mkdir -p /home/axway/install/quickstart`

* Execution rights:  
`chmod +x /home/axway/Desktop/APIGateway_7.7.20240830_Install_linux-x86-64_BN04.run`

* Components: 
    * Admin Node Manager 
    * Cassandra
    * API Gateway
    * Server
    * QuickStart Tutorial
    * API Manager
    * Policy Studio
    

## 3. Attended installation (Skip to unattended installation in Lab environment)

* Execute installer: ``./APIGateway_7.X.Y_Install_linux-x86-64_ZZZ.run`
    * With UI: run it from VM Desktop
    * With command line: from Putty or option `--mode text`

* Accept license

* Use always **Custom**

* Select components checked + Configuration Studio: 
    * Admin Node Manager, Cassandra, API Gateway Server, QuickStart Tutorial, API Manager, Policy Studio, Configuration Studio

* Installation Directory: `/home/axway/install/quickstart`

* API Gateway license: absolute path to license 

* Cassandra Installation Directory: `/home/axway/install/quickstart/Cassandra`

* JRE Location: keep it

* Admin Node Manager credentials : N

* Host Name: `api-env`

* Keep all default ports: `8090`, `8085`, `8080`

* API Manager credentials: N

Launch it!

![Alt text](images/image16.png)


## 4. Unattended installation

* Use “--help” to display all options


* Copy, modify (marked parts) and execute:  

> /home/axway/Desktop/APIGateway_7.7.<releasedate>_Install_linux-x86-64_BN<buildnumber>.run --mode unattended --enable-components nodemanager,cassandra,apigateway,qstart,apimgmt,policystudio,configurationstudio --disable-components packagedeploytools,analytics --setup_type advanced --licenseFilePath /home/axway/Desktop/ReadyTech/Inbox/API_7.7_Temp.lic --apimgmtLicenseFilePath /home/axway/Desktop/ReadyTech/Inbox/API_7.7_Temp.lic --prefix /home/axway/install/quickstart --cassandraInstalldir /home/axway/install/quickstart --cassandraJDK /home/axway/install/quickstart/apigateway/platform/jre --acceptGeneralConditions yes


**Example with 7.7.20240830:**

```
/home/axway/Desktop/APIGateway_7.7.20240830_Install_linux-x86-64_BN04.run --mode unattended --enable-components nodemanager,cassandra,apigateway,qstart,apimgmt,policystudio,configurationstudio --disable-components packagedeploytools,analytics --setup_type advanced --licenseFilePath /home/axway/demo/data/licenses/classic/multiple.lic --apimgmtLicenseFilePath /home/axway/demo/data/licenses/classic/multiple.lic --prefix /home/axway/install/quickstart --cassandraInstalldir /home/axway/install/quickstart --cassandraJDK /home/axway/install/quickstart/apigateway/platform/jre --acceptGeneralConditions yes
```


** Installation takes a few mintues to complete. After issuing the command, there will be no output for a few mintues. 

*Important to remember*

* Do not forget about patches
* Installation only finished once validated (see later)
* If QuickStart is installed, processes started
* Be careful of patches

What you must see as a result of installation?

* In installation folder
    * Log file (troubleshooting)
    * apigateway
    * cassandra
    * configurationstudio
    * policystudio
    * uninstall

* Process started (due to QuickStart)
    * ANM
    * Instance
    * Cassandra

### 4.1. Wait, this is not production installation!

* QuickStart simplifies creation of development environment and should not be used for production

* Some other modules are needed before, especially
    * Topology
    * Deployment
    * Cassandra

### 4.2. How do I do API Manager installation without QuickStart? 

* Cassandra (single or cluster) must be installed

* Without QuickStart, no default domain
    * See in [docs.axway.com](https://docs.axway.com/bundle/axway-open-docs/page/docs/apim_installation/apigtw_install/post_overview/index.html) to create host and instance
    * Or see in Topology module

* Then : 
    * Either use setup-apimanager
        * Modification of running instance
        * Modification of Cassandra
    * Modification of envSettings.props (environment configuration)

```
setup-apimanager --username admin --password changeme --adminName apiadmin --adminPass changeme -g mygroup -n myinstance --update
```

* Or use **Configure API Manager** option from Policy studio
    * Modifications done on local project
    * Needs packaging/deployment to running instance

![Alt text](images/image20.png)

### 4.3. Patching

* Patches contain non-cumulative bugfixes 

* Issued for a specific product release (ex : 7.7.20210830 Patch XXXXX)

![Alt text](images/image21.png)

* Installation instructions available in **Readme** file

![Alt text](images/image22.png)


### 4.4. Basic operations

What are basic operations here?
* Start
* Stop
* Status

What are components that are in scope of this installation?
* Admin Node Manager (ANM)
* API Gateway Instance
* Cassandra

How to achieve it? 
* Command line (for all)
* With API Gateway Manager 
    * Start/stop/status of instances with UI
    * And a UI feature means presence of an API

    ![Alt text](images/image23.png)

#### 4.4.1. Admin Node Manager (ANM)

Context
* ANM embeds API Gateway Manager
* There is one Node Manager (NM) per installation
    * And at least one NM is ANM
* ANM is able to manage instances and groups

Command line

* Executable  
`apigateway/posix/bin/nodemanager`


* Stop  
* `nodemanager -k`
```
/home/axway/install/quickstart/apigateway/posix/bin/nodemanager -k
```
* Start  
`nodemanager -d`
```
/home/axway/install/quickstart/apigateway/posix/bin/nodemanager -d
```

* Status  
`ps -eaf | grep -i "Node Manager"`  
`netstat -an | grep 8090`  
`curl -k https://localhost:8090`

#### 4.4.2. API Gateway Instance, from ANM

*Requires ANM to be started*

URL: `https://myhost:8090`
Default login: `admin/changeme`

![Alt text](images/image24.png)

API (call to ANM)

[Swagger](https://apidocs.axway.com/swagger-ui-NEW/index.html?productname=apigateway&productversion=7.7.0&filename=api-gateway-swagger.json)

#### 4.4.3. API Gateway Instance

Context

* An Instance belongs to a Group

* Names are important
    * Instance logical: `QuickStart Server`
    * Instance internal: `instance-1`
    * Group logical: `QuickStart Group`
    * Group internal: `group-2`

* Command line requires logical name


Command line

* Executable  
`apigateway/posix/bin/startinstance`

* Stop  
`startinstance -n "QuickStart Server" -g "QuickStart Group" -k`
> /home/axway/install/quickstart/apigateway/posix/bin/startinstance -n "QuickStart Server" -g "QuickStart Group" -k

* Start  
`startinstance -n "QuickStart Server" -g "QuickStart Group" -d`
> /home/axway/install/quickstart/apigateway/posix/bin/startinstance -n "QuickStart Server" -g "QuickStart Group" -d

* Status  
`ps -eaf | grep -i "QuickStart Server"`  
`netstat -an | grep 8080`  
`curl http://localhost:8080/healthcheck`

#### 4.4.4. Cassandra

Context
* API Manager repository
* And could be used as KPS
* Cassandra is supported by Axway as part of the solution
* See docs.axway.com here for management documentation  
[Command line](https://docs.axway.com/bundle/axway-open-docs/page/docs/cass_admin/admin_cassandra_classic/cassandra_manage/index.html)


* Executable  
`cassandra/bin/cassandra`

* Start  
`cassandra -f &`  
> `/home/axway/install/quickstart/cassandra/bin/cassandra -f &`

* Stop (cf documentation)  
`kill <<pid>>`

* Status  
`netstat -an | grep 9042`  
`ps -eaf | grep -i cassandra`  

#### 4.4.5. Dependencies

Rules

* ANM and Instances can be run separately
    * No ANM implies no visibility, no deployment

* API Manager requires Cassandra
    * But instance can start without Cassandra

Recommended run order

1. Cassandra
2. ANM
3. Instances

### 4.5. Post installation steps

#### 4.5.1. Refer to docs.axway.com

[Refer to this link](https://docs.axway.com/bundle/axway-open-docs/page/docs/apim_installation/apigtw_install/post_overview/index.html)

![Alt text](images/image26.png)

*Important points*

* Link to start all tools
* Initial configuration, eg create domain
    * No need only with QuickStart
* Run as services
* Run with standard port (80, 443, ...) as non-root user
* Security guidelines


### 4.6. Installation validation

* Check Cassandra, ANM, Instances are started
    * Or start these in this order

* Connect to API Gateway Manager
    * `https://api-env.demo.axway.com:8090`
    * Default login: `admin/changeme`

* Connect to API Manager
    * `https://api-env.demo.axway.com:8075`
    * Default login: `apiadmin/changeme`

* Call healthcheck API
    * `curl http://api-env.demo.axway.com:8080/healthcheck`  


### 4.7. Containerized installation

* Installation resources publicly available from:  
[https://repository.axway.com/home](https://repository.axway.com/home)
    * Documentation

    * Helm charts (AWS, Azure, Google, Openshift, minikube,…)

* [Official documentation](https://docs.axway.com/bundle/axway-open-docs/page/docs/apim_installation/apigw_containers/index.html)


## 5. Conclusion

* Installation requires good preparation and always ends with validation

* Dev environment can be quickly setup with **QuickStart**

* **API Gateway** installation can be done attended with command line or UI, or unattended, very useful for automation