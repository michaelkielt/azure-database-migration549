# Project README: Azure Database Migration

## Overview

This project focuses on architecting and implementing a cloud-based database system on Microsoft Azure, showcasing hands-on expertise in cloud engineering. The project is divided into the following parts:

1. **Establishing a Production Environment Database:**
   - Set up and connect to an Azure Virtual Machine.
   - Install SQL Server and SQL Server Management Studio (SSMS) on the virtual machine.
   - Create a production database on SSMS using a backup file (`.bak`).

2. **Migrating to Azure SQL Database:**
   - Set up an Azure SQL Database using the Azure Portal, allowing SQL login and specifying the VM's IP address in firewall rules.
   - Install Azure Data Studio on the VM to manage connections to the local SQL Server and Azure SQL Database.
   - Use the SQL Server Schema Compare extension in Azure Data Studio to compare and migrate the schema from the on-premise database to Azure SQL Database.
   - Install the Azure SQL Migration extension in Azure Data Studio to migrate data from the on-premise database to Azure SQL Database.
   - Validate the migration success by inspecting data, schema, and configurations, ensuring adherence to the principles of data integrity.

3. **Secure Database Backups on Azure Blob Storage and Development Environment Setup**
   - Generate a full backup of the production database and securely store it on Azure Blob Storage.
   - Provision a new Azure Virtual Machine for development and replicate the production environment.
   - Restore the production database in the development environment using the generated database backup.
   - Configure a maintenance plan for weekly full backups of the development database to Azure Blob Storage, enhancing data security and availability.
  
4. **Disaster Recovery Simulation:**
   - Simulate intentional data loss in the production environment and execute the disaster recovery process to restore the database to a point before the data loss       
     occurs. This step ensures the robustness of the system's recovery mechanisms and validates the effectiveness of having a disaster recovery strategy.

5. **Geo-Replication and Failover:**
   - Implement geo-replication for the restored production Azure SQL Database, creating a synchronised replica of the primary database.
   - Orchestrate a planned failover to the secondary region, simulating real-world challenges.
   - Test the failover functionality and perform a tailback to revert to the primary region.

6. **Microsoft Entra Directory Integration:**
   - Enable Microsoft Entra ID authentication for the SQL server hosting the Azure production database.
   - Set up an admin account and test admin privileges in Azure Data Studio.
   - Create a DB reader user in Microsoft Entra ID and grant the user the `db_reader` role in Azure Data Studio.
   - Test read-only privileges for the DB reader user by running SELECT queries and validating access denial for UPDATE queries.

     
## Part 1: Establishing a Production Environment Database

### Prerequisites:
- Microsoft Azure account
- Azure Virtual Machine provisioned
- SQL Server and SSMS installed on the virtual machine
- Backup file (`.bak`) for the production database

### Objective:
Establish a production database by provisioning an Azure Virtual Machine, installing SQL Server, and configuring SQL Server Management Studio (SSMS). Create the production database using SSMS and a backup file (.bak), ensuring a secure and well-configured environment.

### Steps:
1. **Azure VM Setup:**
   - Provision an Azure Virtual Machine.
   - Configure the VM using appropriate credentials and firewall rules.
   - Connect to the VM using RDP (Remote Desktop Protocol) and Microsoft Remote Desktop.

2. **SQL Server Installation:**
   - Install SQL Server on the Azure VM.

3. **SSMS Installation:**
   - Install SQL Server Management Studio on the VM.

4. **Database Creation:**
   - Use SSMS to create the production database on the VM, utilising the backup file that corresponds
     to the renowned Microsoft SQL Server database known as 'AdventureWorks'.

## Part 2: Migrating to Azure SQL Database

### Prerequisites:
- Azure SQL Database created using the Azure Portal
- Azure Data Studio installed on the VM
- SQL Server Schema Compare extension and Azure SQL Migration extension installed in Azure Data Studio

### Objective:
Migrate to Azure SQL Database by creating an instance using the Azure Portal. Allow SQL login, specify the VM's IP address in firewall rules, and install Azure Data Studio on the VM. Use the SQL Server Schema Compare and Azure SQL Migration extensions in Azure Data Studio to migrate schema and data from the on-premise database to Azure SQL Database. Validate the migration's success by inspecting data, schema, and configurations.

### Steps:
1. **Azure SQL Database Setup:**
   - Create an Azure SQL Database using the Azure Portal.
   - Allow SQL login and specify the VM's IP address in firewall rules.

2. **Azure Data Studio Configuration:**
   - Install Azure Data Studio on the VM.

3. **Connection Establishment:**
   - Use Azure Data Studio to establish connections to the local SQL Server and Azure SQL Database.

4. **Schema Migration:**
   - Install the SQL Server Schema Compare extension in Azure Data Studio.
   - Compare and migrate the schema from the on-premise database to the Azure SQL Database.

5. **Data Migration:**
   - Install the Azure SQL Migration extension in Azure Data Studio.
   - Migrate data from the on-premise database to Azure SQL Database.

6. **Validation:**
   - Inspect data, schema, and configurations in Azure Data Studio.
   - Ensure the migration adheres to principles of data integrity.
  
## Part 3: Secure Database Backups on Azure Blob Storage and Development Environment Setup

### Prerequisites:
- Azure Virtual Machine for production
- Production database successfully set up
- Azure Blob Storage account created
- New Azure Virtual Machine provisioned for development
- SQL Server and SSMS installed on the development VM

### Objective:
Securely back up the production database on Azure Blob Storage by generating a full backup and uploading it to a configured container. Provision a new Azure Virtual Machine for development, install SQL Server and SSMS, and restore the production database using the generated backup. Set up a maintenance plan for weekly full database backups to Azure Blob Storage, ensuring data security and availability. Confirm the successful execution of the maintenance plan for periodic backups.

### Steps:

1. **Secure Database Backup on Azure Blob Storage:**
   - Generate a full backup of the production database hosted on the production VM.
   - Store the backup file in the SQL Server Backup folder on the production VM.
   - Configure an Azure Blob Storage account to serve as a secure online repository for database backups.

2. **Upload Backup to Azure Blob Storage:**
   - Upload the full generated backup file to the configured blob storage container.

3. **Development Environment Provisioning:**
   - Provision a new Azure Virtual Machine to serve as the development environment.

4. **SQL Server and SSMS Installation on Development VM:**
   - Install SQL Server and SQL Server Management Studio (SSMS) on the development VM to replicate the production environment.

5. **Restore Database on Development Environment:**
   - Use the backup file generated previously to restore the database onto the new "sandbox" development environment using SSMS.

6. **Maintenance Plan for Periodic Backups:**
   - Create a maintenance plan in SSMS on the development VM.
   - Set up a periodic weekly full database backup to the Azure Blob Storage container.
   - Configure SQL Server Credentials to connect to the Azure Blob Storage.
   - Provide the Azure Storage account name and secret access key for secure access.

7. **Validation:**
   - Confirm that the maintenance plan executes periodic backups to the Azure Blob Storage container.

## Part 4: Disaster Recovery Simulation

### Objective:
Simulating a disaster scenario to test the robustness of the system's recovery process. In this simulation, intentional data loss was induced in the production environment, and the recovery process was executed to restore the system to a point before the data loss occurred.

### Steps:

1. **Simulating Data Loss:**
   - Connect to the production SQL database using SQL Server Management Studio (SSMS).
   - Execute SQL statements to remove foreign key (FK) constraints within the `Person.Address` table.
   - Utilise a DELETE statement to remove the top 1000 records from the `Person.Address` table.
   - Confirm the success of the data loss by reviewing the results in Azure Data Studio.

2. **Initiating Database Restore:**
   - Access the Azure portal and navigate to the homepage of the Azure SQL Database.
   - Select the 'restore' option to initiate the database restoration process.

3. **Choosing a Restore Point:**
   - Choose a restore point that precedes the simulated data loss by selecting a time approximately 2 hours before the incident occurred.

4. **Configuring Restored Database:**
   - Specify a new database name for the restored database by appending '-restored' to the original database name.
   - Deploy the newly restored database using the selected restore point.

5. **Validation of Restoration:**
   - Use Azure Data Studio to inspect the restored database's `Person.Address` table.
   - Confirm that the entries previously deleted during the simulation have been successfully restored.

## Part 5: Geo-Replication and Failover

### Objective:
Implementing geo-replication to enhance database availability and simulate real-world challenges by orchestrating a planned failover to a secondary region. This part demonstrates the establishment of a synchronised replica of the primary database and validates the failover capabilities to ensure system resilience.

### Steps:

1. **Setting Up Geo-Replication:**
   - Navigate to the Azure portal and access the SQL server hosting the primary production database.
   - Create a synchronised replica (geo-replica) of the primary database.
   - Configure the new SQL server to be geographically distant, in this case by selecting a region such as US East.
   - Choose SQL authentication as the authentication method and deploy the geo-replica.

2. **Simulating Real-World Challenges - Planned Failover:**
   - Go to the SQL server page on the Azure portal.
   - Create a new failover group for the primary server hosting the production database.
   - Select the newly provisioned geo-replica server as the server in the failover group.
   - Deploy the failover group successfully.

3. **Testing Failover:**
   - Validate the failover by selecting the resource (failover group) and choosing 'failover.'
   - Confirm that the secondary database is now promoted to the primary database.

4. **Functional Validation:**
   - Test the functionality of the failover by connecting to the database.
   - Run queries on Azure Data Studio to ensure that the secondary database is operational and functions correctly.

5. **Tailback for Reversion to Primary Region:**
   - After validating the failover, perform another failover to initiate a tailback.
   - Revert the system to the primary region, making the original primary database the active one again.

## Part 6: Microsoft Entra Directory Integration

### Objective:
Integrate Microsoft Entra Directory with the Azure SQL Database setup to enhance access management and security. This section focuses on enabling Microsoft Entra ID authentication for the SQL server hosting the Azure production database and managing user roles effectively.

### Steps:

1. **Enabling Microsoft Entra ID Authentication:**
   - Navigate to the SQL server page on the Azure portal.
   - Under the security section, select Microsoft Entra ID.
   - Select 'Set admin' and set an admin account for Microsoft Entra ID authentication.

2. **Testing Admin Privileges:**
   - Validate admin privileges by connecting to the primary database in Azure Data Studio.
   - Run queries to ensure the admin account can perform administrative tasks.

3. **Creating a DB Reader User:**
   - Go to the Microsoft Entra ID page on the Azure portal.
   - Create a new user with the username 'project-db-reader'.

4. **Assigning DB Reader Role:**
   - In Azure Data Studio, execute a statement in the primary database
     using the credentials of the newly created user to grant the user the db-reader role.

5. **Testing Read-Only Privileges:**
   - Reconnect to the primary database with the db_reader role credentials in Azure Data Studio.
   - Run SELECT queries to confirm read privileges.
   - Attempt UPDATE queries to verify that write access is denied.

### Conclusion
In the culmination of this comprehensive Azure Database Migration project, we have successfully navigated through multiple key phases, demonstrating a robust and well-architected cloud-based database system on Microsoft Azure. The project's structured approach has covered critical aspects of database management, migration, disaster recovery, geo-replication, and integration with Microsoft Entra Directory. Each part of the project has contributed to the overall goal of establishing a resilient and efficient database ecosystem.

