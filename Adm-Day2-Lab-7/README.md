# Testing and Troubleshooting Lab 

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, 

## Learning objectives

At the end of this lab, you will be able to 
* Understand a project build process using the `projpack` tool
* Explore Environmentalization techniques
* Understand the deployment process using the `projdeploy` tool
* Understand the API promotion process using the `apimanager-promote` tool



## Introduction

The lab explores two scenarios:
1. Package and deploy three Policy Studio projects
    * You will understand how you can externalize parameters and variable, so you can dynamically change them for each target environment
    * You will build and deploy a package to a target environment using command line tools
2. Use the apimanager-promote tool to promote an API collection to a target environment

Both scenarios targets DevOps and how you can automate build and deployment steps in your pipeline.


![Alt text](images/image.png)

### Scope of the lab

You work with:
* Policy Studio to make your projects suitable for deploying to multiple environments
* API Management scripts – projpack/projdeploy/apimanager-promote – to understand the build and deploy/promote processes

### Accelerating your deployment process

Sample scripts are in  
`/opt/Axway/APIM/apigateway/samples/scripts/environmentalize/`

![Alt text](images/image15.png)

And

`/opt/Axway/APIM/apigateway/samples/scripts/certs`

![Alt text](images/image16.png)



Here are some details about the *environmentalize* scripts

<table>
<tbody>
<tr>
<td>addEnvSettings.py</td>
<td>Downloadsa deployment package (.fed) from an API Gateway. Marks the <b>Traffic HTTP Interface</b> port field to be environmentalized. Creates an environment settings entry for the port, and sets it to <code>7878</code>.</td>
</tr>
<tr>
<td>getEnvSettings.py</td>
<td>Connects to an API Gateway and lists all the fields that have been marked for environmentalization. the associated values in environment settings are output.</td>
</tr>
<tr>
<td>mergeEnvSettings.py</td>
<td>Offline script that does not connect to an API Gateway. Merges a policy package (.pol) from downstream with an environment package (.env) from upstream, and merges them to create a deployment package (.fed).</td>
</tr>
<tr>
<td>removeEnvSettings.py</td>
<td>Downloads a deployment package (.fed) from an API Gateway. Removes the <b>Traffic HTTP Interface</b> port field from being environmentalized (opposite of the <code>addEnvSettings.py</code> script).</td>
</tr>
</tbody>
</table>




<hr style="background-color:blue;"></hr>

Here are some details about the *certs* scripts

<table>
<tbody>
<tr>
<td>addCertFromFile.py</td>
<td>Connect to a target Admin Node Manager and add a new certificate to the certificate store from a referenced file</td>
</tr>
<tr>
<td>addCert.py</td>
<td>A utility script with the methods used by other 3 scripts to manipulate certificates</td>
</tr>
<tr>
<td>addCertsFromSSL.py</td>
<td>Connect to a target Admin Node Manager and add a new certificate downloaded from an SSL server</td>
</tr>
<tr>
<td>addFromP12File.py</td>
<td>Connect to a target Admin Node Manager and add a new certificate and key from a P12 file to the certificate store</td>
</tr>
</tbody>
</table>







## Conclusion

* Well thought deployment process and tooling are critical to the overall success of DevOps

* You have explored some of the available options for automating your DevOps for Axway API Management

* Axway API Management REST APIs along with demonstrated command line tools provide a flexible environment for integrating the product with almost any existent DevOps
