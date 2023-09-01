# migration

Azure:

- create resource group for migration
- create ADF
- create an Azure SQL Database (already had a server created for personal projects, used that one)

Database:
- download SSMS, SSDT
- import WideWorldImportersDW on SSMS (through  Restore Detabase, device, add .bak file)
- create connections in SSDT for both on-premise database and Azure SQL Database
- import project in solution explorer
- commented out some rows in different files which wouldn't allow be to later rebuild the project
- rebuild the project after I have no errors
- publish, generate script, check which tables will be created
- deployed the project to Azure SQL DatabasE (I got an error ("'MEMORY_OPTIMIZED tables' is not supported in this service tier of the database. See Books Online for more details on feature support in different service tiers of Azure SQL Database.") and couldn't deploy the entire project, but I managed to deploy all the tables. couldn't deploy the SPs)

ADF:
- download Integration Runtime so you can create a connection between ADF and on-premise SQL Server
- in IAM on Blob Storage, give ADF blob storage contributor role. This way ADF can read from the Blob Storage (through a Linked Service)
- create linked services and datasets
- create 1 pipeline with 1 copy activity that copies FactSales to Blob Storage under the migration container, then  another Copy Activity to move the data from Blob Storage to Azure SQL Database, under the FactSales table.
- do the same thing from DimCustomer
- create a master pipeline which will delete all files under the migration container from Blob Storage, then execute Dim pipeline and Fact Pipeline


What could be done better:
- parametrize it more, especially where I have keys on connections. These should be kept in Azure Key Vault. Any sensitive data should be kept in Azure Key Vault
- parametrize more the pipelies , creating a single connection for OnPremise and AzureSQL, and then add parameters (schema_name, table_name) to pick the desired table
