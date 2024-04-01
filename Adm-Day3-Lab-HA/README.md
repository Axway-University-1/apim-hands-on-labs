# High Availability Installation of API Manager

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, you will learn how to exercise routine administration operations on the platform.




## Learning objectives

At the end of this lab, you will be able to 
* Install API Manager in High Availability
* Do a reasonably secure installation
* Check that the installation is working properly

## Introduction

* Installation is based on an architecture definition

* Some of the common constraints:
    * Security requirement
    * Network
    * Team coordination

* And each company has its own unique constraints

### Scope of this lab

* API Manager HA
    * API Manager monitoring not used, ie no DB

* Installation done by you

* Secured installation
    * No default certificate
    * Default password changed: Axway123
        * For all
    * TLS internal connections

* 5 servers
    * 2 in “Process zone”, highly secured
    * 3 in “Data zone”, LAN

* Technical pre-requisites already met
    * VMs delivered
    * Credentials and roles provided
    * Ports opened

### Target architecture

![Alt text](images/image01.png)

### API call 1 - flow

![Alt text](images/image02.png)

### API call 2

![Alt text](images/image03.png)

### Internal connections

![Alt text](images/image04.png)

Why 3 ANMs in the exercise?

* There is the need for 3 Cassandra nodes for HA
* But, only 2 ANMs are required for HA
* 3 ANMs are used in the exercise to have consistent configuration across all 3 servers in Data zone.

Could I do installation differently?

* Yes, in your Information System! 
* Performing different installations is one of the flexibility provided by the Axway solution
* Note minimum number of servers is 3 (due to Cassandra). 
* 7 servers installation could make sense too. And adding components (API Portal, Embedded Analytics) can affect the number of servers used


For now, let’s focus on our 5 servers installation!

## Installation preparation

* Similar to single server installation

* Be careful to review your requirement/dependency with other teams

* Pay particular attention to 
    * Logins with appropriate permissions
    * Whether the ports are opened
    * Whether the load balancers are factored in

### Checklist

-[x] Login for all servers, with right credentials
-[x] Port listed and opened
In and out
Load-balancer configured
Licenses reviewed and uploaded to API Gateway servers
Installer downloaded from support site and uploaded to all required servers
Check patches, select which to install (by default the latest) and upload to all required servers 


## Installation