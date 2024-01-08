# azure-database-migration475
Comtemts
1. Project Overview
2. File Structure

Milestone 2
1. Provisioned a Windows Virtual Machine using Microsoft Azure
2. Connected to the VM using Remote Desktop Connection on my Windows machine
3. SQL Server and SSMS installed on the VM
4. Production Database 'AdventureWorks2022' set up from the backup file provided.

Milestone 3
1. Set up an Azure SQL database with the name 'AdventureWorks2022' ready for migration
2. Azure Data Studio installed on the VM
3. Connect to both the local database and Azure database on Azure Data studio
4. Schema migration from the local database to the Azure database ready for data to be migrated.
5. Data migration completed to the Azure database from the local database

Milestone 4
1. Created a backup file of my database on the local VM machine
2. Uploaded this file to blob storage on Microsoft Azure
3. Created the new VM for the development environment and restored the database to this.
4. In SSMS created an automated backup to run weekly on a Sunday at 12:00AM

Milestone 5
1. Mimic dataloss in a production environment. To replcate the dataloss I deleteded the following two tables from the production environment:
  1 - Person.PersonPhone
   2 - Sales.PersonCreditCard
2. Using Azure Data Studio restored the version from the most recent backup. Check this to see that it contained the tables that were missing as a result of the dataloss

Milestone 6
1. Created a secondary server in a different geographical location from the previous one
2. Then set this up as a geo-replication for the production Azure SQL Database
3. Created the failover to the secondary server with different geographical location
4. Tested the failover and the role of the servers successfully swapped
5. Performed a failback and the returned to their original roles.

Milestone 7
1. Went into the securtiy settings of the primary server and set up myself as an admin
2. Created a new user account in Microsoft Entra ID
3. Using the admin credentials then assigned the db_datareader role to the newly created user
4. Tested out the new permissions to check the user could only read from the database and not make any changes
