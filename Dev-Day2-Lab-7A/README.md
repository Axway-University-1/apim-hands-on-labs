# Policy Studio Lab - Quota System

In this lab, 

## Learning objectives

At the end of this lab, you will be able to 


## Introduction

### Scenario

Web Services and service-oriented architectures (SOA) form an integral part of business information systems. This is the case for the Roboulot Group, a group of businesses equipped to tackle the increasingly important question of globalization.

At the Information Systems Division of the group, Peter Smith is an architect, designer, developer, debugger, and security manager. He is also a "modder" but that's another story.

To put applications in place more quickly, Peter Smith must allow existing Web Services to be used for a greater number of purposes and by a greater number of applications, and of course users, of the Roboulot Group.
The problem Peter encounters is to some extent the price of success: the web services are working so well that the number of users is constantly increasing.

Peter must now find a solution to avoid deterioration of the quality of service and the overloading of his servers.

The solution is simple: he will adapt the flow rate to the absorption capacity of the available servers. He can limit the overall number of requests per unit of time, but this will have a negative effect on the quality of service for all his users. This is perhaps an excessively dramatic solution; some users will not appreciate it. Peter Smith wishes to fine-tune the solution. He should be able to adapt the flow rate to the types of use, the applications, and the organization of the Group (and he must serve the head office first if he wants to retain his budgets).

And as always, it must be possible to develop the solution quickly and easily to be implemented in order to adapt to the available resources.

The challenges for Peter lie in the following points:
* "How to implement this efficiently without jeopardizing the existing architecture?" 
* "Given that we know how to implement quotas, is it possible to distinguish them by user profile? With what level of detail?"

Do you know how to use the API Gateway available to you to help Peter with his management, guaranteeing optimum operation, while at the same time preserving his budget.

### Tasks

We propose the "Quota System" policy. This production involves three stages, thus offering three variants on the policy.

#### Task 1: Implementation of quotas
This is the quota management policy in its basic state. We will produce the policy which restricts access to any service to one request every 5 seconds.

#### Task 2: Quota policy based on authentication
In this second version of the policy, we will add authentication. If the user is recognized by the platform, they can access the service as many times as they wish. However, if the user is not recognized, the quota policy is applied, based on the restrictions described below.

#### Task 3: Quota policy based on membership of a group
A user may belong to different groups. These groups may have limited access rights to certain services. 
To simulate this partitioning, we will develop the policy to take into account three levels of authorization to access the services:
* Gold level: Unlimited access;
* Silver level: Access Limited to 5 requests every 5 seconds;
* Bronze level: 1 request every 5 seconds that is the default policy for an unauthenticated user.


## Solution

### Virtual machine environment

* If you are disconnected, click on the username `Axway`

![Alt text](images/image005.png)

* Enter `axway` in the field **Password**.
* Click on the button **Unlock**

![Alt text](images/image006.png)

* If API Management is not started (you can check with the command `statusAll` anywhere from a terminal)
    * Double click the following desktop shortcut **Start API Management** 

![Alt text](images/image007.png)

* Policy Studio is the tool to configure the API Gateway.
    * Open the policy design interface by double-clicking the **Policy Studio** icon on the desktop

![Alt text](images/image008.png)

QuickStart is a way to quickly explore the API Management solution. It is based on a standard configuration with good documentation for beginners.

Let’s open the **QuickStart** project and add modifications to the configuration.

In **Policy Studio**, you will open and modify the **QuickStart** project.

* Click **QuickStart**

![Alt text](images/image009.png)

In the menu that will pop up, click **OK**, to specify no passphrase.

![Alt text](images/image010.png)

The **Policy Studio** shows the following screen

![Alt text](images/image011.png)



### Task 1: Quota system

By the end of this section, you will have implemented restrictions on usage per unit of time: the quotas. The policy that you are going to create will limit the number of requests to the API Gateway to a single request every 5 seconds.

This is the policy that you are going to implement:

![Alt text](images/image012.png)

If you respect the quota, you will see the message `Access to service authorized`.   
You will receive an error message, `Access to service denied`, if you are exceeding your quota.





