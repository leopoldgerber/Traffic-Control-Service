# Traffic Control Service

The repository contains scripts for working with the platform. A complex task is the collection of reports for a selected period to analyze competitor traffic, which will help the company to determine the place for expansion, as well as provide an opportunity to analyze the marketing strategy of other companies. 

## Functions performed by scripts:

### 3 - DB Upload

Responsible for loading data from the collected reports into the database. Includes connection to the database, processing of column names and types (for proper loading into the database).

Required external files: 
- <code>database_config.json</code> - to connect to the desired database.
- <code>exception_list.json</code> - for exception columns, because not all columns with string values must be processed. Manual input is possible if there is no file.

Both files can be created using the scripts in the depository [additional files](#additional-files)
