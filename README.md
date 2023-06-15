# Traffic Control Service

The repository contains scripts for working with the platform. A complex task is the collection of reports for a selected period to analyze competitor traffic, which will help the company to determine the place for expansion, as well as provide an opportunity to analyze the marketing strategy of other companies. 

## Functions performed by scripts:

### 1 - Download Data

A script for downloading reports for a selected period, for selected domains. 
Emulates downloading a person, to bypass account blocking. Contains random values for the height of the scroll in both directions, making pauses between transitions and pauses before and after pressing buttons.
Passes through each domain in turn with the reporting categories selected for it. The storage location of the downloaded reports is set by the user. The selected location will be used for further assembly of all reports, including the processing of these reports.

<b>NOTE:</b> The best solution is to use scripts 1 and 2 in tandem in one run, since the variables from script 1 contain the lists of domains by category. Modification is possible to display the list of processed domains by category in separate files. 

<br>

<details close>
<summary>Read more about domains by category</summary>
<br>
 
***
 
Since downloadable reports, in most cases, do not have a domain in the name, it is necessary to consider the result of the download. In addition to the division by month (1 month - 1 report), there are also subcategories that form 1 category (1 subcategory - 1 report).

<br>

There are three results of downloads: 
- the report was successfully downloaded and contains all the data.
- the report was downloaded, but does not contain data (no data from the platform side).
- the report cannot be downloaded, because the platform has not updated the data for you

***
 
<br>
</details> 

### 2 - Data Preprocessing

### 3 - DB Upload

Responsible for loading data from the collected reports into the database. Includes connection to the database, processing of column names and types (for proper loading into the database).

Required external files: 
- <code>database_config.json</code> - to connect to the desired database.
- <code>exception_list.json</code> - for exception columns, because not all columns with string values must be processed. Manual input is possible if there is no file.

Both files can be created using the scripts in the depository [additional files](additional%20files/)
