# Azure-Database-Migration

# Milestone 2 Set up the Production Environment:

# 1. Provision a Windows Virtual Machine

- Before creating a VM, we need to create a Resource group that will later contain all the infrastructure needed for this project

![Screenshot 2023-10-11 at 11 42 10](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/8cee047a-aab3-40d9-9967-3da11aa54679)

- VM is created, here we name & configure the image as Windows 10, size Standard_B2ms will provide all the resources needed
  
![Screenshot 2023-10-11 at 12 01 48](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/611e3285-371d-489d-9902-a11703b8fd8c)

- Resource is created using Admin authentication, if user makes a Linux shell this will be done VIA SSH, for inbound ports RDP for Windows image & SSH for Linux image

- With a Windows image we will need to accept the licencing also
  
![Screenshot 2023-10-11 at 12 01 57](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f4cef0b0-dee7-4e2c-9801-19795f18916b)

- Review & create image, this will take a few minutes then we can view the VM in Azure

![Screenshot 2023-10-11 at 12 07 50](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/166a6540-6886-41c2-8dfc-e5cc5ff9a4ca)

# 2. Connect to the Windows Virtual Machine

- Click the 'Connect' icon at the top right of the resource
  
![Screenshot 2023-10-11 at 12 16 39](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/15c39cb4-7937-443f-91ae-fb808efe9101)

- This brings you to a page where we can download the RDP file to add the VM

![Screenshot 2023-10-11 at 12 18 06](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c7708431-9217-4472-ae2b-a5350d4459dc)

![Screenshot 2023-10-11 at 12 18 23](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/e03dad7e-5c7d-425a-8cae-63d4328b788c)

- Find Windows Remote Desktop on the app store download this application, once open we can drag & drop the .rdp file to access the VM

- Open the Virtual Machine: DO NOT ALLOW PUBLIC CONNECTIONS on first boot up

<img width="693" alt="Screenshot 2023-10-11 at 12 21 54" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/67dfb943-5a1c-4b9f-9dc0-710f889821d6">

<img width="352" alt="Screenshot 2023-10-11 at 12 22 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7c0cf0e2-306a-4d9d-b3d3-afac9f3ea692">

# 3. Install SQL Server & SSMS

- Follow this link on your remote desktop browser https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb to install SQL Server & select Basic for the installation type

- At end of instillation you will have the option to also install SSMS, the link can also be found here https://aka.ms/ssmsfullsetup

- Once both are installed, lets open SSMS, we should be greeted by this window & just click connect

<img width="1655" alt="Screenshot 2023-10-12 at 10 49 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/24e92f75-05a6-4584-92e9-0e7ae6365483">

# 4. Create the Production Database

- Install the file linked here https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak

- Right-click on 'database' on SSMS, then 'restore`, note here that restore will look in a specific MSSQL folder for backup .bak files as pictured below, we should move the .bak folder from downloads into this MSSQL backup folder, screenshot below shows filepath to it

<img width="355" alt="Screenshot 2023-10-12 at 11 47 10" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/52c7d567-9f2b-4325-b394-ec25374af2d3">

- We should now see the AdventureWorks2022 Table in out list of databases

# Milestone 3 Migrate to Azure SQL Database

# 1. Set Up Azure SQL Database

- Firstly in Azure, find SQL Database server, which we will host the database on & begin by creating a SQL Satabase Server

![Screenshot 2023-10-13 at 15 42 23](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b37c8da5-6fe6-41b9-b83b-a8791c6efe7c)

- Connect the SQL Database server to your resource group, give it a name & location, then use SQL authentication to create login details

![Screenshot 2023-10-13 at 15 44 11](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/2fbfc7ab-963d-430c-91e3-fc674cef1f76)

- Now lets Create that SQL Database, search SQL Database!

![Screenshot 2023-10-13 at 15 50 54](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/90b183dd-503d-4721-a0b5-4488080633cc)

- IMPORTANT, ON STORAGE SELECT BASIC

![Screenshot 2023-10-13 at 15 51 37](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/1877f556-c9c4-406d-9e2d-8ab103c3a5f3)

- Once created, let's add a firewall rule, set public network access to 'selected networks'

![Screenshot 2023-10-13 at 15 54 16](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/aee3d874-0260-4773-bf81-d278f1a4b8d7)

![Screenshot 2023-10-13 at 15 54 33](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b5d609ba-0b2e-4512-8c15-6cd94d4a637a)

- Go back to your VM & fetch your local IP

![Screenshot 2023-10-13 at 17 50 43](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/ea194e28-9682-4311-a3e5-ccb29a0292d3)

- Now let's add a firewall, have both start and end Ipv4 Address as the IP

![Screenshot 2023-10-13 at 18 00 48](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c1bb6099-0caf-42f2-b110-34a732dc7d45)

# 2. Prepare for Migration

- Install Azure Data Studio on the VM using this link https://go.microsoft.com/fwlink/?linkid=2242848

- During installation tick all boxes

<img width="602" alt="Screenshot 2023-10-17 at 13 12 20" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0a2cf0c9-a990-4eb6-8f6f-501e572b4f83">

- Login to localhost with windows authentication to connect to the local SSMS Server

<img width="1039" alt="Screenshot 2023-10-17 at 13 53 09" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/de8d1401-03ba-4617-863b-844d6730bd3d">

# 3. Connect to Azure SQL Database

- Connect to SQL database using SQL login

<img width="1039" alt="Screenshot 2023-10-17 at 13 22 14" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f46d0f6d-8606-44a5-bed3-7ea73ed8dc68">

# 4. Schema Migration

- Install SQL Server Schema Compare

<img width="1039" alt="Screenshot 2023-10-17 at 14 00 20" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0607c973-3b82-4a77-97f9-d012b7e06b94">

- Right click on localhost, comapre scheme to Azure SQL Database, ensure localhost is source & SQL Database is target, also ensure the target database is the SQL Database we have created

<img width="1039" alt="Screenshot 2023-10-17 at 14 30 08" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/83d53039-ae25-4bda-a350-5730a5ae41f6">

- Start the Schema comparison & Accept all changes

<img width="1039" alt="Screenshot 2023-10-17 at 14 32 49" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/3d827b87-d92b-4e02-b751-461cb435e6df">

- We can now see all of the schemas have been added to our Azure SQL Database

<img width="1039" alt="Screenshot 2023-10-17 at 14 48 19" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/d3093e07-f657-4657-a124-ed4d88b0fc1f">

# 5. Data Migration

- Install SQL Migration Extension

<img width="1039" alt="Screenshot 2023-10-17 at 15 11 10" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/93fc9165-0f85-4f41-aec0-2e14287ca913">

- Click 'Manage on local DB we want to migrate to Azure SQL Database

<img width="1039" alt="Screenshot 2023-10-17 at 15 12 09" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/09538728-1b23-4b03-9413-edd82ac76d2d">

- Click Migrate to Azure SQL under Azure SQL Migration

<img width="1039" alt="Screenshot 2023-10-17 at 15 12 38" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/8ac16b71-0ef1-41f6-9df8-2ba37100ecf5">

- Select Database we want to migrate And press Next

<img width="1039" alt="Screenshot 2023-10-17 at 15 12 49" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/ef96b2eb-cb76-406f-a3bf-7ed292c1c3f4">

- Choose Azure SQL Database as migration choice

<img width="1039" alt="Screenshot 2023-10-17 at 15 15 39" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/34aaa1b5-aade-4729-a79e-31ce22bbcf6e">

- Before continuing, ensure we assess the Database for suitability
  
<img width="1039" alt="Screenshot 2023-10-17 at 15 16 05" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/a89ad2ac-029f-4747-a87a-8c41ee9f2f35">

<img width="1039" alt="Screenshot 2023-10-17 at 15 15 57" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f3e8c735-e96f-4e14-aaa6-539c1401c6ac">

- Now let's select the Azure SQL target, we need the location, resource group, DB Server & our login credentials

<img width="1039" alt="Screenshot 2023-10-17 at 15 17 51" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/fe328bff-74ff-4907-95b2-b5fbbd494876">

- Once we connect we can select the SQL Database target

<img width="1039" alt="Screenshot 2023-10-17 at 15 18 05" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c5b7893c-114a-4931-b606-2be8bd899200">

- Before we continue, we need to add Azure Database Migration Services onto our resource group

![Screenshot 2023-10-17 at 15 19 06](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0cb45e1e-d173-4ceb-9ba2-cf3d4a24ca84)

![Screenshot 2023-10-17 at 15 19 28](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f9fa19ce-7855-4e09-b242-babc937ebc06)

![Screenshot 2023-10-17 at 15 20 02](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0046b0ba-d418-4e59-b63b-19270255be18)

- Now that's all setup, we can refresh the setup wizards & our DB Migration Service

<img width="1027" alt="Screenshot 2023-10-17 at 15 23 12" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/2ed86187-4e2c-4f49-9244-77dd8e924c6c">

- We need to download & install the integration runtime on our VM & copy one of the keys

<img width="1027" alt="Screenshot 2023-10-17 at 16 05 55" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/82594e32-f9ab-41ff-9c4a-6a1d4b641f2a">

- Here just install the newest runtime ( for me was the bottom one)

<img width="1027" alt="Screenshot 2023-10-17 at 16 07 32" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/2dd4675d-58bd-439f-a732-0b384ba94b5f">

- Add the key to the runtime & press register, DO NOT enable remote access

<img width="780" alt="Screenshot 2023-10-17 at 16 12 46" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/6d60103e-d5d8-4448-a307-83da2c9cfd68">

<img width="780" alt="Screenshot 2023-10-17 at 16 14 01" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/4e65a413-91c6-4ded-af94-08d4fe940f42">

- Now let's 'Launch Configuration Manager', which will allow us to move to the 5th step

<img width="780" alt="Screenshot 2023-10-17 at 16 15 32" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/a38a5f8e-fb83-4270-8be0-d8ec28f89a71">

<img width="1020" alt="Screenshot 2023-10-17 at 16 16 10" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/89c4502b-5077-466c-949e-933ca0f6595a">

- Enter our VM credentials & edit the table selection to include all tables

<img width="1020" alt="Screenshot 2023-10-17 at 16 16 59" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/1a067d62-6754-4386-aca7-1a96ae1e9637">

- Before we finish RUN VALIDATION

<img width="1020" alt="Screenshot 2023-10-17 at 16 17 26" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/74a1a48a-a476-4a40-8416-417a83a3f4da">

- Finally, let's START MIGRATION

<img width="1020" alt="Screenshot 2023-10-17 at 16 17 41" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/4c1bf8b7-6f00-448d-8884-9542c38c076c">

- We can check the status of our migration here

<img width="1020" alt="Screenshot 2023-10-17 at 16 18 43" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/6e47cec7-f18c-45c3-9184-d4f77eec87dc">

- Now we wait for the data to migrate :)

# 6. Validate Migration Success

- right click any table & 'select top 1000' to verify the migration

<img width="1020" alt="Screenshot 2023-10-17 at 17 04 10" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/accf08ea-b57b-4ca1-a9ea-16df8011f18b">

# Milestone 4: Data Backup and Restore

# 1. Backup the On-Preminse Database

- On SSMS Connect to the on-premise SQL Server, right-click the database, then tasks & backup

<img width="733" alt="Screenshot 2023-10-19 at 11 22 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b4d9f69f-2ce8-42a3-90c7-6a64ee0997b7">

- Rename the backup to something descriptive

<img width="911" alt="Screenshot 2023-10-19 at 11 37 06" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/42b929f3-6adf-4a7d-8d31-5fd20a803d79">

- Click 'Ok' to backup our database

<img width="911" alt="Screenshot 2023-10-19 at 11 37 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/16494819-73ac-4814-bef5-5e5f9e26580c">

# 2. Upload Backup to Blob Storage

- On the VM, Let's log in to Azure & create a storage account, we need to create this with a unique name (like S3 buckets) & link it to the resource group

<img width="846" alt="Screenshot 2023-10-20 at 13 08 36" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f1d47947-5d86-4bde-bfac-df68a1ab3331">

- Once created click upload

<img width="846" alt="Screenshot 2023-10-20 at 13 13 53" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c15841d0-9820-44be-b3ed-6669e01a68a0">

- We will be required to create a name for the container, this doesn't have to be universally unique, just unique to your storage account

<img width="576" alt="Screenshot 2023-10-20 at 13 14 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/bf4dfe69-f96b-4b8c-9f36-ce925969d069">

- Let's press upload & find our backup file, this will be in the backup folder (will need to find the bak file in MSSQL folder)

<img width="825" alt="Screenshot 2023-10-20 at 13 15 33" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/6347c862-8d41-4551-b17f-63662b575b8d">

# 3. Restore Database on Development Environment

- Let's create a new VM with its own SQL Server & Database, following set up from previous tasks

- Once these are all set up, next step is to reinstall SSMS and Data Studio

- On browser in VM, login to Azure & Access the blob we created in the previous task, if we go into the 'storage browser' and in our container we can find the .bak file to download

<img width="1088" alt="Screenshot 2023-10-20 at 15 18 21" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c6a5f9f2-6f90-44c7-9f70-6d21ffaddc44">

- Let's move the .bak file from our downloads file into the backup folder in our MSSQL folder

<img width="1088" alt="Screenshot 2023-10-20 at 15 20 18" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/912c5097-6132-4f80-acc6-045e38a8bfef">

- On SSMS let's restore database & select our backup file

<img width="1088" alt="Screenshot 2023-10-20 at 15 22 46" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b03a3191-b406-4b67-b91c-958eedf4c935">

<img width="870" alt="Screenshot 2023-10-20 at 15 23 15" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/692f276d-ef3f-4a5e-bf04-e22a0bfad642">

<img width="870" alt="Screenshot 2023-10-20 at 15 23 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/008c51ae-397d-4943-ba5a-0d36ea14c451">

- Now thats backed up, lets connect to localhost on our Data Studio

<img width="1026" alt="Screenshot 2023-10-20 at 15 26 48" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0fcf1a3f-8e93-4400-99a6-b45093ad2cad">

- Once connected, let's query a table to ensure Data Migration Success

<img width="1026" alt="Screenshot 2023-10-20 at 15 27 11" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/432ba380-3084-41b0-87a8-fc0014963238">

<img width="1026" alt="Screenshot 2023-10-20 at 15 27 22" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/fdbc2e98-08b9-4407-8ce5-5615118c7664">

# 4. Automate Backups for Development Database

- The first step is to start the SQL Server Agent, we need the Agent in order to automate backups

<img width="545" alt="Screenshot 2023-10-20 at 18 04 20" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/48a70aa3-6ded-4f9e-9e90-ff6ed0d9b26e">

- Now let's create a new query in our server in order to create credentials to link to our storage account

<img width="545" alt="Screenshot 2023-10-20 at 18 05 56" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c89ec934-ee7a-4bbc-9579-115753f9d01e">

- We need to go into our storage account to get both the account name & the key for our credentials

![Screenshot 2023-10-20 at 18 07 10](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7759096a-d38b-40af-a736-a210196bedb9)

- Now we can create the credentials that will be needed during the maintenance plan

<img width="848" alt="Screenshot 2023-10-24 at 13 58 34" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/05badca8-a806-454f-a0d6-1165fdee1906">

- Now let's create the maintenance plan, right click on maintenance plans

<img width="328" alt="Screenshot 2023-10-24 at 15 04 35" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/da46b0a8-22f8-40eb-bb6d-53bf4949c66a">

- Name the plan,for now, we won't add a schedule, then select the maintanence task we want to perform

<img width="560" alt="Screenshot 2023-10-24 at 13 47 49" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7e9b4d42-b6ad-4c38-a96f-c96090021178">

<img width="664" alt="Screenshot 2023-10-20 at 18 12 21" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/bef1fbe0-387d-45b8-aa31-770f98387773">

- Select the Database to Backup & backup to URL

<img width="573" alt="Screenshot 2023-10-24 at 13 03 30" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/760f9f32-f045-4b4f-a98e-4ad4a28690f6">

- Moving to the destination tab, lets select our credentials & enter the same container as the one we created for our storage account

<img width="560" alt="Screenshot 2023-10-24 at 13 54 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/38100bea-0466-4898-85fd-5dd7889f0ca7">

- Let's finalise the maintenance plan & refresh to get our now plan!

<img width="560" alt="Screenshot 2023-10-24 at 13 27 37" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/a552b356-98a8-4a64-81dc-695acbca46c9">

<img width="560" alt="Screenshot 2023-10-24 at 13 28 00" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0b5c3266-ef95-4608-a17f-2f4f8dc39046">

- Let's execute the new plan, this should succeed!

<img width="560" alt="Screenshot 2023-10-24 at 13 28 12" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/45558526-4ba3-4fc3-ba14-7c277a561c1b">

<img width="472" alt="Screenshot 2023-10-24 at 13 55 45" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/0b239038-0fb9-4a5c-94fa-b37be27ad8e6">

- Finally, let's modify the maintenance task to occur once a week on a Sunday :)

<img width="328" alt="Screenshot 2023-10-24 at 15 23 56" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/143c01e6-e034-40ae-9e22-ad885217ae28">

<img width="670" alt="Screenshot 2023-10-24 at 15 24 07" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/56a374ac-542e-4ce6-a2ca-abed884a1b54">

- We can verify the backup by checking in our container

<img width="1409" alt="Screenshot 2023-10-24 at 14 01 06" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/9799fb55-c360-477e-83de-b0e023ba8a4b">

# Milestone 5: Disaster Recovery Simulation

# 1. Mimic Data Loss in Production Environment

- lets break some stuff ;)

- Lets choose a random table & delete 200 records in Data Studio (Originally had 19972 rows)

<img width="1036" alt="Screenshot 2023-10-26 at 18 41 47" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/3f2ca34e-9ba0-4eff-9239-bc7678402fff">

<img width="1036" alt="Screenshot 2023-10-26 at 18 43 05" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/3b443ac7-5841-4c0f-8115-b2da901bd3e4">

# 2. Restore Database From Azure Database Backup

- In Azure, find the pruduction database & click 'restore'

![Screenshot 2023-10-26 at 18 44 41](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f0735d26-0fe0-4fa9-98cd-568b4fe55721)

- Now Restore from a point in tim ebefore the data loss (a few hours before rows were dropped)

![Screenshot 2023-10-26 at 18 46 27](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/361ab315-8a57-4795-8ca0-239c48fb11fb)

- Now lets go into our SQL server for the Prod Database, here we can find the restored database, lets click on it & connect to it using Data Studio

<img width="1055" alt="Screenshot 2023-10-26 at 19 57 39" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/1c6ddaeb-7f94-43f9-a1dd-e19ef38c7353">

<img width="1055" alt="Screenshot 2023-10-26 at 19 57 51" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/e8d24c50-3cb8-46b0-a5f7-c2aa1983b5fb">

<img width="503" alt="Screenshot 2023-10-26 at 19 58 29" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/88443b73-d2f6-4f25-b1dc-c60ae80b094f">

- If we compare rows now, we can see that The amount of rows is equal to before our mimiced data loss

<img width="1417" alt="Screenshot 2023-10-26 at 20 00 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f79721a7-a386-48dd-b6c6-3a72de045820">

# Milestone 6: Geo Replication and Failover

# 1. Set Up Geo-Replication for the Azure SQL Database

- Move to our restored Database, Select replicas & choose 'Create Replica'

![Screenshot 2023-10-26 at 20 18 04](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/97eef870-0be5-48fd-be5e-7b768a29b2ca)

- now lets create a new SQL server in a different region to begin Geo-Replica in the 'create replica' section

![Screenshot 2023-10-26 at 20 18 58](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/3bb790af-b9fa-48c8-a247-d4b6bac91499)

![Screenshot 2023-10-26 at 20 19 43](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/4d8ec305-1f98-4f38-82e0-43412cff63d2)

- Add the new server & Create the new Geo-Replica SQL Database

![Screenshot 2023-10-26 at 20 20 14](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/45c22919-6f6e-4367-86de-0344da1aacff)

# 2. Test Failover and Failback

- Lets move into the newly created replication server, under failover groups select the new group created

![Screenshot 2023-10-26 at 20 34 54](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/4f65eb53-aae5-4b3e-a3f9-ddab7bf7ac04)

- Lets select 'Failover' to swap the primary & secondary databases, we should see the two servers at the bottom swap icons

![Screenshot 2023-10-26 at 20 35 33](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7ef0f8d3-4d99-459a-bfc0-6b9d5dcdf846)
![Screenshot 2023-10-26 at 20 36 32](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/56a382ae-187d-4020-a632-0cd00896a22e)

- now lets Failback to have our original Database as the primary

![Screenshot 2023-10-26 at 20 36 58](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b3badaae-f82e-4d0d-96e1-0c2a1ba29042)

# Milestone 7: Microsoft Entra Directory Integration

# 1. Configure Microsoft Entra ID for Azure SQL Database

- On Azure navigate to your SQL Server where your Prod Restore is Located, select 'Microsoft Entra ID' on the left-hand side & set admin

<img width="480" alt="Screenshot 2023-10-27 at 12 07 31" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/cf8cf884-a81f-4e28-bc2e-fbeee5199429">

- Select your user as the admin & save admin settings

<img width="959" alt="Screenshot 2023-10-27 at 12 07 42" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/e77dc212-bd20-4296-ac11-bc25dafabe33">

- On Data studio, query a table, then disconnect from the server, then right click -> edit connection

<img width="959" alt="Screenshot 2023-10-27 at 12 08 03" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/cfb3a6df-b0d3-4fc7-8bbe-baafcd11af4b">
<img width="445" alt="Screenshot 2023-10-27 at 12 08 32" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/77a74974-b9bb-40a6-97c1-ba14ef218fe9">

- Edit connection type to be Azure Active Directory, your admin settings should load immediately

<img width="490" alt="Screenshot 2023-10-27 at 12 08 49" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/de8d6047-13f8-4309-b9bb-c121d6db9198">

- Query the same table as before to check you still have access

<img width="992" alt="Screenshot 2023-10-27 at 12 09 21" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/b7296299-d44b-4104-bd29-a3d73f5ba012">


