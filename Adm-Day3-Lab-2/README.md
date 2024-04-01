# API Gateway and API Manager Upkeep Lab 

| Average time required to complete this lab | 60 minutes |
| ---- | ---- |
| Lab last updated | March 2024 |
| Lab last tested | March 2024 |

In this lab, you will learn how to exercise routine administration operations on the platform.




## Learning objectives

At the end of this lab, you will be able to 
* Execute some of the maintenance tasks related to backup, recovery, file archiving, and API Gateway audit.


## Tasks

### KPS table upkeep

In this task, you are required to
* Perform a backup of a Quickstart KPS table (*HeroesCharactersRegistry* table)
* Simulate a disaster by manually deleting the table
* Check data is missing in API Gateway Manager
* Restore data

#### Using kpsadmin tool for backup

* In a terminal window switch to:  
    ```
    cd /opt/Axway/APIM/apigateway/posix/bin
    ```

* Run kpsadmin in interactive mode (ID/pwd – admin/changeme):  
    ```
    ./kpsadmin
    ```

* Select option 11 to backup a table

* Pick default options for Group and API Gateway

* Pick QuickStart collection

* Pick default for Table

* Type y  to confirm your selections

![Alt text](images/image12.png)

* Copy and save UUID (see the screenshot below)

![Alt text](images/image13.png)

* Quit the tool

* Find your backed up table in  
`/opt/Axway/APIM/apigateway/groups/group-2/instance-1/conf/kps/backup/`


#### Using kpsadmin tool for restore

* Run kpsadmin tool in interactive mode

* Pick option 10 to clear a table that you’ve just backed up  
`QuickStart_HeroesCharactersRegistry`

* Go to API Gateway Manager UI and confirm that your table is empty

![Alt text](images/image14.png)

* Back in the terminal window, pick option 12 and restore the same table (use saved UUID from back up)

* Verify your data is restored in API Gateway Manager UI 

![Alt text](images/image15.png)


### Cassandra upkeep

In this task, you will
* Understand Cassandra data directory structure
* Identify an API Management keyspace
* Perform a snapshot of one Cassandra keyspace

#### Understand Cassandra data directory structure

* Cassandra data is segregated by keyspace

* Keyspaces are organized by table

* Each table directory contains :
    * Table data (SSTable files)
    * Snapshot data 
    * Incremental backup data 

![Alt text](images/image17.jpeg)

![Alt text](images/image16.png)

#### Identify an API Management keyspace

* In a terminal window switch to  
    ```
    cd /opt/Axway/cassandra/bin
    ```

* Display your keyspaces  
    ```
    ll ../data/data/
    ```

* You should see 6 keyspace directories:
    * System keyspaces: system*
    * API Management keyspaces : x<DOMAIN_ID>_<GROUP_ID>

![Alt text](images/image18.png)


#### Perform a snapshot of one Cassandra keyspace

* Clear all previous snapshots  
    ```
    ./nodetool -h ::FFFF:127.0.0.1 clearsnapshot -- x<DOMAIN_ID>_<GROUP_ID>
    ```
![Alt text](images/image19.png)

* Verify that there is no more snapshots directories  
    ```
    find ../data/data/x<DOMAIN_ID>_<GROUP_ID> -name snapshots
    ```
![Alt text](images/image20.png)

* Take a snapshot of one keyspace  
    ```
    ./nodetool -h ::FFFF:127.0.0.1 snapshot -t NEW_SNAPSHOT -- x<DOMAIN_ID>_<GROUP_ID>
    ```
![Alt text](images/image21.png)

* Verify that the new snapshots directories have been created  
    ```
    find ../data/data/x<DOMAIN_ID>_<GROUP_ID> -name NEW_SNAPSHOT
    ```
![Alt text](images/image22.png)


## Conclusion

* Keeping your API Management healthy requires good planning

* Create an “upkeeping” plan for your installation

* Consult product documentation for additional information and tips

