# azure-database-migration475
Comtemts
1. Project Overview
2. Project Description

1. Project Overview
The following README is a description of an implementaion of a database migration using the various tools and sotwares provided by the Microsoft Azure cloud computing services

Such tools provide end-users ease of use and highly documented advanced tooling and are a focal point of the following description.

2. Project Description
Milestone 2
1. Provisioned a Windows Virtual Machine using Microsoft Azure
The first step in this project, involved the migration of a database from an on-site system to using Azure cloud computing services and to use these services to set up a vm.

The resource group for the vm to be attached to (and the rest of the project) is selected - production-vm. A region for the VM to be hosted was selected as UK South to minimize latencies as it is close. 

Windows 11 Pro was chosen as the image for the VM as a standard size for this sort of migration.

2. Connected to the VM using Remote Desktop Connection on my Windows machine
3. SQL Server and SSMS installed on the VM
SQL Server Management Studio (SSMS) is a database management tools developed by Microsoft. SSMS is a Windows-only tool that is used to manage SQL Server databases, while Azure Data Studio is a cross-platform tool that can be used to manage SQL Server, PostgreSQL, and MySQL databases 12.
These tools are vital for database management and migration using Azure Cloud Services.
5. Production Database 'AdventureWorks2022' set up from the backup file provided.

Milestone 3
1. Set up an Azure SQL database with the name 'AdventureWorks2022' ready for migration
   <!-- TODO: how did you connect to the SQL database? What is a firewall rule? -->
Using the Azure portal a Azure SQL database can be created by selecting the Azure SQL database resource from the create a resource option from the home portal. A linked SQL server can be generated and SQL login is chosen for the authentication method. Firewall settings are updated so that on the SQL database so that the VM IP address is added to the new server.

2. Azure Data Studio installed on the VM
Azure Data Studio is a cross-platform tool that can be used to manage SQL Server, PostgreSQL, and MySQL databases 12. This allowed me to to create a server connection between Azure data studio and the SQL Server hosted on the VM.
3. Connect to both the local database and Azure database on Azure Data studio
4. Schema migration from the local database to the Azure database ready for data to be migrated.
With connections created using Azure data studio it was now possible to proceed with schema migration. To achieve this the SQL Server Schema Compare extension had to be downloaded through Azure data studios extension marketplace.

Once  installed schema comparison/migration is started on the vm hosted database and selecting the Schema compare option. This create the schema compare GUI with the production-vm database set as the source. The target database is selected as the Azure SQL production database stored on the azure SQL Server. Comparisons can then  be made before migration is confirmed.
5. Data migration completed to the Azure database from the local database
Once the schema is migrated it is then simple to transfer all the appropriate data across. Data validation then takes place through checking and comparing a number of tables in each database to make sure there has been no loss in the transfer.

Milestone 4
1. Created a backup file of my database on the local VM machine
The database can be backed to a .bak file using SSMS. This was achieved by selecting the Adventure works database stored on the Azure vm and selecting to create a full restore backup.
2. Uploaded this file to blob storage on Microsoft Azure
Blob storage is Azure Cloud Based. It allows for storage of a large amount of data.
3. Created the new VM for the development environment and restored the database to this
A development area is incredibly useful for trying anything new before deploying to a production environment. This was created by following the steps of how the other environment was created.
4. In SSMS created an automated backup to run weekly on a Sunday at 12:00AM

Milestone 5
1. Mimic dataloss in a production environment. To replicate the dataloss I deleted the following two tables from the production environment:
  1 - Person.PersonPhone
   2 - Sales.PersonCreditCard
Azure SQL Database provides three high availability architectural models: Remote storage model, Local storage model, and Hyperscale model. Within each of these models, SQL Database supports local redundancy and zonal redundancy options. Local redundancy provides resiliency within a datacenter

2. Using Azure Data Studio restored the version from the most recent backup. Check this to see that it contained the tables that were missing as a result of the dataloss
Recovery of the data was achieved by using azure portal and selecting the Azure Sql database resource. From the databases homepage I selected the Restore option. This opens the Restore database window. Where I selcted to restore the dabase to two hours before as restore point. Finally a name has to be given to the the database which for this project was adventureworksreplica.

Milestone 6
1. Created a secondary server in a different geographical location from the previous one
I chose East US as the region for this secondary server that replicates the original settings of my original server. This allows there to be a powerful disaster recovery feature should something happen in one of the locations.
2. Then set this up as a geo-replication for the production Azure SQL Database
3. Created the failover to the secondary server with different geographical location
4. Tested the failover and the role of the servers successfully swapped
5. Performed a failback and the returned to their original roles.
It is important to test the system using a failover (Switching the workload from primary region to the secondary) and then tailback (the opposite direction)

Milestone 7
1. Went into the securtiy settings of the primary server and set up myself as an admin
2. Created a new user account in Microsoft Entra ID
3. Using the admin credentials then assigned the db_datareader role to the newly created user
The db_datareader is a role that allows the used to view the database and all the information that it contains, but is it gives the user no permission to edit the database. This is useful when someone needs access to 

4. Tested out the new permissions to check the user could only read from the database and not make any changes
