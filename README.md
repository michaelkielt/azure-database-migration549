# Project README: Azure Database Migration

## Overview

This project focuses on architecting and implementing a cloud-based database system on Microsoft Azure, showcasing hands-on expertise in cloud engineering. The project is divided into the following parts:

1. **Establishing a Production Environment Database:**
   - Set up and connect to an Azure Virtual Machine.
   - Install SQL Server and SQL Server Management Studio (SSMS) on the virtual machine.
   - Create a production database on SSMS using a backup file (`.bak`).

2. **Migrating to Azure SQL Database:**
   - Set up an Azure SQL Database using the Azure Portal, allowing SQL login and specifying the VM's IP address in firewall rules.
   - Install Azure Data Studio on the VM for managing connections to both the local SQL Server and Azure SQL Database.
   - Use the SQL Server Schema Compare extension in Azure Data Studio to compare and migrate the schema from the on-premise database to Azure SQL Database.
   - Install the Azure SQL Migration extension in Azure Data Studio to migrate data from the on-premise database to Azure SQL Database.
   - Validate the migration success by inspecting data, schema, and configurations, ensuring adherence to the principles of data integrity.

## Part 1: Establishing a Production Environment Database

### Prerequisites:
- Microsoft Azure account
- Azure Virtual Machine provisioned
- SQL Server and SSMS installed on the virtual machine
- Backup file (`.bak`) for the production database

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

### Steps:
1. **Azure SQL Database Setup:**
   - Create an Azure SQL Database using the Azure Portal.
   - Allow SQL login and specify the VM's IP address in firewall rules.

2. **Azure Data Studio Configuration:**
   - Install Azure Data Studio on the VM.

3. **Connection Establishment:**
   - Use Azure Data Studio to establish connections to both the local SQL Server and Azure SQL Database.

4. **Schema Migration:**
   - Install the SQL Server Schema Compare extension in Azure Data Studio.
   - Compare and migrate the schema from the on-premise database to Azure SQL Database.

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
   - Set up a periodic weekly full backup of the database to the Azure Blob Storage container.
   - Configure SQL Server Credentials to connect to the Azure Blob Storage.
   - Provide the Azure Storage account name and secret access key for secure access.

7. **Validation:**
   - Confirm that the maintenance plan executes periodic backups to the Azure Blob Storage container.


