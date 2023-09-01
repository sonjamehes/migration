# migration

Azure:

- create resource group for migration
- create ADF
- create an Azure SQL Database (already had a server created for personal projects, used that one)

Database:
- download SSMS, SSDT
- import WideWorldImportersDW on SSMS through  Restore Detabase, device, add .bak file)
- create connections in SSDT for both on-premise database and Azure SQL Database
- import project in solution explorer
- commented out some rows in different files which wouldn't allow be to later rebuild the project
- rebuild the project after I have no errors
- publish, generate script, check which tables will be created
- deployed the project to Azure SQL DatabasE (I got an error and couldn't deploy the entire project, but I managed to deploy the 2 relevant tables I need)

ADF:
- download Integration Runtime so you can create a connection between ADF and on-premise SQL Server
- create linked services and datasets
- create 1 pipeline with 1 copy activity that copies FactSales to Blob Storage under the migration container, then  another Copy Activity to move the data from Blob Storage to Azure SQL Database, under the FactSales table.
- do the same thing from DimCustomer
- create a master pipeline which will delete all files under the migration container from Blob Storage, then execute Dim pipeline and Fact Pipeline
