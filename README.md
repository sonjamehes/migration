# migration

Azure:

- create resource group for migration
- create ADF
- create an Azure SQL Database (already had a server created for personal projects, used that one)

- download SSMS, SSDT
- import WideWorldImportersDW on SSMS through  Restore Detabase, device, add .bak file)
- create connections in SSDT for both on-premise database and Azure SQL Database
- import project in solution explorer
- commented out some rows in different files which wouldn't allow be to later rebuild the project
- rebuild the project after I have no errors
- publish, generate script, check which tables will be created
- deployed the project to Azure SQL Database
