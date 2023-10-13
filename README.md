# Azure-Database-Migration

# Milestone 2 Set up the Production Environment:

1. Provision a Windows Virtual Machine

- Before creating a VM, we need to create a Resource group that will later contain all the infrastructure needed for this project

![Screenshot 2023-10-11 at 11 42 10](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/8cee047a-aab3-40d9-9967-3da11aa54679)

- VM is created, here we name & configure the image as Windows 10, size Standard_B2ms will provide all the resources needed
  
![Screenshot 2023-10-11 at 12 01 48](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/611e3285-371d-489d-9902-a11703b8fd8c)

- Resource is created using Admin authentication, if user makes a Linux shell this will be done VIA SSH, for inbound ports RDP for Windows image & SSH for Linux image

- With a Windows image we will need to accept the licencing also
  
![Screenshot 2023-10-11 at 12 01 57](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f4cef0b0-dee7-4e2c-9801-19795f18916b)

- Review & create image, this will take a few minutes then we can view the VM in Azure

![Screenshot 2023-10-11 at 12 07 50](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/166a6540-6886-41c2-8dfc-e5cc5ff9a4ca)

2. Connect to the Windows Virtual Machine

- Click the 'Connect' icon at the top right of the resource
  
![Screenshot 2023-10-11 at 12 16 39](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/15c39cb4-7937-443f-91ae-fb808efe9101)

- This brings you to a page where we can download the RDP file to add the VM

![Screenshot 2023-10-11 at 12 18 06](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c7708431-9217-4472-ae2b-a5350d4459dc)

![Screenshot 2023-10-11 at 12 18 23](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/e03dad7e-5c7d-425a-8cae-63d4328b788c)

- Find Windows Remote Desktop on the app store download this application, once open we can drag & drop the .rdp file to access the VM

- Open the Virtual Machine: DO NOT ALLOW PUBLIC CONNECTIONS on first boot up

<img width="693" alt="Screenshot 2023-10-11 at 12 21 54" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/67dfb943-5a1c-4b9f-9dc0-710f889821d6">

<img width="352" alt="Screenshot 2023-10-11 at 12 22 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7c0cf0e2-306a-4d9d-b3d3-afac9f3ea692">

3. Install SQL Server & SSMS

- Follow this link on your remote desktop browser https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb to install SQL Server & select Basic for the installation type

- At end of instillation you will have the option to also install SSMS, the link can also be found here https://aka.ms/ssmsfullsetup

- Once both are installed, lets open SSMS, we should be greeted by this window & just click connect

<img width="1655" alt="Screenshot 2023-10-12 at 10 49 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/24e92f75-05a6-4584-92e9-0e7ae6365483">


4. Create the Production Database

- Install the file linked here https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak

- Right-click on 'database' on SSMS, then 'restore`, note here that restore will look in a specific MSSQL folder for backup .bak files as pictured below, we should move the .bak folder from downloads into this MSSQL backup folder, screenshot below shows filepath to it

<img width="355" alt="Screenshot 2023-10-12 at 11 47 10" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/52c7d567-9f2b-4325-b394-ec25374af2d3">

- We should now see the AdventureWorks2022 Table in out list of databases

# Milestone 3 Migrate to Azure SQL Database

- Firstly in Azure, find SQL server, which we will host the database on

![Screenshot 2023-10-13 at 15 42 23](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b37c8da5-6fe6-41b9-b83b-a8791c6efe7c)
