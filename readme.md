# Microsoft Azure Architect Technologies for Cloud 

I have created this repository as my go-to self reference for Azure Architecht technologies certifications

## Powershell

- It is a command line interface for administrating Azure environment

- **Azure PowerShell** is an extended version of Microsoft-extended Powershel - Allows you to interact with Azure Environment via **Azure Modules**. These azure modules are a set of commands that configure a certain task such as configuring a virtual network, subnet etc. The convenience is that you can run a specific Azure Module through powershell and it will automatically configure it. 

- The requirements for installing Azure Powershell is that you have the latest versions of win basic powershell and .NET Framework- See below to check which versions you have

- Check which default version is available for powershell in windows by opening it and typing `$PSVersionTable` in the terminal. This commands give a bunch of details. You can be even more specific with `$PSVersionTable.PSVersion`. Keep powershell up to date- current version is 5.1. If you need to install use [Latest Powershell version](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.1#powershell-core)

- You should also have the updated version of **.NETframework** - It is a webapp framework that is used to build online software. You can use powershell to check the version with the following commnd:

- `(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802`  where `-ge` is greater than or equal to. This is like going to the registry with `regedit` and then navigating to the path and locating the version. 394802 corresponds with .NET Framework version 4.6.2 or later and is the release key. Each version has its own release key, for example 528040 is the release key for .NET Framework 4.8. A version of 4.72 or later is preferred. If you need to install use [Latest .NET framework version](https://docs.microsoft.com/en-us/dotnet/framework/install/)

- Below are the comparison operators in powershell

- `-eq`	Equal
- `-ne`	Not Equal
- `-gt`	Greater than
- `-ge`	Greater than or equal to
- `-lt`	Less than
- `-le`	Less than or equal to
- `-like`	Checks if part of string matches (Wildcard comparison)
- `-notlike`	Checks if part of a string doesn’t matches (Wildcard comparison)
- `-match`	RegEx comparison
- `-notmatch`	RegEx comparison
- `-contains`	Containment Operator
- `-notcontains`	Non-Containment Operator
- `-In`	In Operator
- `-notIn`	Non In Operator
- `-Replace`	Replaces a string pattern

## Azure Architect technologies 

It can be grouped into the following components:

- Azure infrastructure  
    - Storage accounts
    - Deploying virtual machines
    - Building virtual networks
    - Security, using the network security groups
    - VPN connections
    - Multifactor authentication
    - Using resource manager
    - Active Directory

- Implementing security solutions
    - Using Azure Migrate
    - Using Azure site recovery
    - Load balancer
    - Application gateway
    - Application manager
    - Firewall
    - Role based access
    - Key Vault
    - Encryption

- Azure Webservices
    - Using the Web App Service
    - Deploying an application
    - Deployment from github
    - Azure Docker and Kubernetes

- Data Management
    - MySQL
    - CosmosDB

- Azure Moniroting and Diagnostics
    - Connecting machines to log analytics workspace
    - Log analytics - setting up queries and alerts
    - Diagnostics of virtual machines and storage accounts

## Azure Storage Accounts

- 4 basic types of features: Blob (sharing videos, images and objects), table (storing data), queue (for sending and receiving messages), file(creating file shares)

- Select storage accounts from dashboard and create a new storage account
    - **Basics tab**
    - Assign a resource group
    - Assign a new storage account name - ***This name must be unique and will be part of the URL linking to specific objects inside the container***
    - Select region
    - You can choose between standard or premium performance option. 
                    - The *standard is a general purpose account* (blob, table, queue,file sharing)
                    - Premium is more specific for each of the individual subtypes and has low latency
    - Choose redundancy- It relates to availability, for extra availability you have more options, but the basic option is (locally redundant storage)
    - **Advanced tab**
    - You can keep the default settings
    - **Networking**
    - Keep the default setting
    - **Data Protection**
    - Keep the soft delete blob checked - A deleted object will remain in place for 7 days untill when it can be recovered
    - **Tags**
    - No changes
    - **Review+Create**
- Once a storage account is created, you can access it under resources and locating it by its name and it will have options of Containers, file shares, tables and queues - each consistent with the 4 basic types of features

**Services inside the storage account**

- **Blob Service** : This service gives the ability to upload objects- you can access this service by ***clicking the containers inside the storage account***

    - Create a container (typicaly this is how its done for a blob service)
    - Assign a name such as 'data' and select public level access as private(no anonymous access)- the latter is an additional security feature
    - Once you click a container named 'data', then you can upload an object to it such as a file which can be an image file or a text based file
    - You can also modify the file by clicking edit while inside the container
    - The text files can also be viewed in various formats such as javascript etc
    - A unique URL will be available for each of the objects uploaded inside the container
    - If you type in this URL into the browser, you will be able to access this object if the ***Public Access level for the 'data' container is NOT set to private***
    - The access level can be changed by clicking on the container and then clicking "change access" level - selecting Blob(anomymous read access for blobs only) will allow public read only access. This will be applied to blob only, while an alternative option can also be selected for changing access level to container level as well
    - You can create a folder inside the container by selecting the advanced option when uploading the file. Under "upload to folder" you can type in the folder name

    - An example: A company can have an application that uploads videos, those videos can then be uploaded onto a container using the blob service. Each video will have its unique URL. The app can be linked to the storage account. This allows complete separation between the storage account and the application

- **File Share Service** This is when you want to share a file across multiple users or virtual machines- It gives you the ability to map a drive onto a container- this is not ideal with a blob service.  The difference with blob is that the file there is stored as an object and has a unique URL and the file cannot be maped across multipe users and VMs. You can access the file share service by ***clicking the file share inside the storage account**

    - Create a new file share inside the storage account
    - Assign a name such as 'data' and Set a quota- size limit, can select 1 Gib
    - Then you can open this file share named 'data' as it shows in the storage account
    - You can then create a directory inside this fileshare
    - You can also upload a file into fileshare or inside the directory you have created
    - When you upload a file, a unique file URL will also be created - but the link will not work for public access- This URL is a link to the fileshare which will only work after successful mapping
    - Instead you can connect to the fileshare. This can be done by selecting your OS e-g Windows and then copy the code for connection. The code contains a password. Then you can 1) Either use powershell and copy this code 2) Use windows mapping feature and manually paste the password. This will create a new drive in my computer