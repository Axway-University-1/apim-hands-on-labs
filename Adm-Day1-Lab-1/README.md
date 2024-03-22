# APIM Installation Lab 

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, 

## Learning objectives

At the end of this lab, you will be able to 
* Install APIM solution with **QuickStart** and understand what it implies
* Use some basic commands like start, stop, status

## Introduction

### Installation mode

#### Attended

With UI or command line

![Alt text](images/image16.png)


#### Unattended

With command line, used for automation

![Alt text](images/image17.png)


* Lab scope is the following
    * Dev environment
    * On Linux, with default rights, no firewall
    * Done by yourself, in the next few minutes!

* Concretely it means using **QuickStart**. 
    * So, it is not production ready. We keep it simple for now.
    * See HA installation module at the end of this course 

### Lab pre-requisites

* User:   
`axway/axway`

* Installation kit:
    * Installer : `/home/axway/Desktop/APIGateway_7.7.<releasedate>_Install_linux-x86-64_BN<buildnumber>.run`
    * License(s) : `/home/axway/Desktop/ReadyTech/Inbox/API_7.7_Temp.lic`

* Installation folder:  
`mkdir -p /home/axway/install/quickstart`

* Execution rights:  
`chmod +x /home/axway/Desktop/APIGateway_7.7.<releasedate>_Install_linux-x86-64_BN<buildnumber>.run`

* Components: 
    * Admin Node Manager 
    * Cassandra
    * API Gateway
    * Server
    * QuickStart Tutorial
    * API Manager
    * Policy Studio
    

## Attended installation

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


## Unattended installation

* Use “--help” to display all options


* Copy, modify (marked parts) and execute:  
```
/home/axway/Desktop/APIGateway_7.7.<releasedate>_Install_linux-x86-64_BN<buildnumber>.run --mode unattended --enable-components nodemanager,cassandra,apigateway,qstart,apimgmt,policystudio,configurationstudio --disable-components packagedeploytools,analytics --setup_type advanced --licenseFilePath /home/axway/Desktop/ReadyTech/Inbox/API_7.7_Temp.lic --apimgmtLicenseFilePath /home/axway/Desktop/ReadyTech/Inbox/API_7.7_Temp.lic --prefix /home/axway/install/quickstart --cassandraInstalldir /home/axway/install/quickstart --cassandraJDK /home/axway/install/quickstart/apigateway/platform/jre --acceptGeneralConditions yes
```

**Example with 7.7.20220228:**
```
/home/axway/Desktop/APIGateway_7.7.20220228_Install_linux-x86-64_BN02.run --mode unattended --enable-components nodemanager,cassandra,apigateway,qstart,apimgmt,policystudio,configurationstudio --disable-components packagedeploytools,analytics --setup_type advanced --licenseFilePath /usr/local/readytech/Inbox/API_7.7_Temp.lic --apimgmtLicenseFilePath /usr/local/readytech/Inbox/API_7.7_Temp.lic --prefix /home/axway/install/quickstart --cassandraInstalldir /home/axway/install/quickstart --cassandraJDK /home/axway/install/quickstart/apigateway/platform/jre --acceptGeneralConditions yes
```

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

### Wait, this is not production installation!

* QuickStart simplifies creation of development environment and should not be used for production

* A realistic production installation will be done in `Installation - API Manager HA` module, in this very training.

* Some other modules are needed before, especially
    * Topology
    * Deployment
    * Cassandra

### How do I do API Manager installation without QuickStart? 

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

### Patching

* Patches contain non-cumulative bugfixes 

* Issued for a specific product release (ex : 7.7.20210830 Patch XXXXX)

![Alt text](images/image21.png)

* Installation instructions available in **Readme** file

![Alt text](images/image22.png)


### Basic operations



### Post installation steps


### Installation validation


### Containerized installation


## Conclusion

