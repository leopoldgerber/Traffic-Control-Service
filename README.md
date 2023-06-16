# Traffic Control Service

The repository contains scripts for working with the platform. A complex task is the collection of reports for a selected period to analyze competitor traffic, which will help the company to determine the place for expansion, as well as provide an opportunity to analyze the marketing strategy of other companies.

NOTE: The repository contains an incomplete script and was created to demonstrate skills. Possible copying with the indication of the author (leopoldgerber).

# Functions performed by scripts:

## 1 - Download Data
<code>[Script](1%20-%20Download%20Data.py)</code>

The main script for downloading reports from an account on the platform. 

Emulates downloading a person, to bypass account blocking. Contains random values for the height of the scroll in both directions, making pauses between transitions and pauses before and after pressing buttons.
Passes through each domain in turn with the reporting categories selected for it. The storage location of the downloaded reports is set by the user. The selected location will be used for further assembly of all reports, including the processing of these reports.

<b>NOTE:</b> The best solution is to use scripts 1 and 2 in tandem in one run, since the variables from script 1 contain the lists of domains by category. Modification is possible to display the list of processed domains by category in separate files. 

Classes and arguments:

<details close>
<summary>scroll</summary>
The arguments can be set by the user, by default, the arguments are passed inside the main class, since the height of the pages by category differs and processing requires the visibility of buttons when using the script.
<br>

Methods:
- <code>.scroll_down</code> Contains 3 (if 'short' was selected) and 7 (if 'long' was selected) repeated actions with fixing the previous random variable. From the beginning of the page to the end or the desired height of visibility of the button.
- <code>.scroll_up</code> Same as .scroll_down, but for the opposite direction.  
 
<br>
</details> 

<details close>
<summary>downloader_prepare</summary>
Launches the driver (the path to the driver is specified by the user himself in the arguments), navigates to the link specified by the user. Authorization to the user's account takes place (login and password must be specified in the arguments), a fake domain search is launched to crawl the page with the primary search (then the domains will be passed to the search bar).
<br>

Arguments:
- <code>login</code> of the account 
- <code>password</code> of the account 
- <code>fake domain</code> (to overcome the first search page, then a search bar will be used)
- <code>driver path</code>
- <code>link</code> to the platform's website (preferably to the authorization page)
- <code>downloaded files path</code> (required for further processing)
 
<br>
</details> 

<details close>
<summary>downloader_main</summary>
The class passes through all categories selected by the user. The arguments are passed a file with domains, the beginning and end of the list of domains (numeric values or string values during modification), the selected categories and enabling notifications about the end of work on the domain (False by default).
<br>
 
Category arguments:
- <code>overview</code> Contains information about organic and inorganic traffic. 
- <code>backlinks</code> Information from where the user came from.
- <code>anchors</code> Anchor texts linking to the domain.
- <code>tbd_visits</code> Trend by devices, subcategory "Visits". Contains information about the number of visits.
- <code>tbd_unique</code> Trend by devices, subcategory "Unique". Contains information about unique users.
- <code>tbd_duration</code> Trend by devices, subcategory "Duration". Contains information about the time of visits.
- <code>tbd_bounce_rate</code> Trend by devices, subcategory "Bounce Rate". Contains information about the bounce rate.
- <code>traffic_sources</code> Traffic source information.
- <code>traffic_journey</code> Information about transitions after visiting the page.
- <code>traffic_countries</code> Traffic information by country.
- <code>status_alert</code> Notification of the end of work on the domain.
  
<br>
</details> 

<br>

<details close>
<summary>Read more about domain list and why it is necessary</summary>
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

## 2 - Data Preprocessing
<code>[Script](2%20-%20Data%20Preprocessing.py)</code>

Processing and combining all reports by category. Uses lists of successfully downloaded reports by domains and collects all reports together.
The method of entering months is manual, it can be modified. It is also possible to upload a file with domains. Domains will be processed (some extra characters will be deleted, the list will be cleared of duplicates).
All methods in the class are equal to categories. It is possible to select the desired categories/methods.

## 3 - DB Upload
<code>[Script](3%20-%20DB%20Upload.py)</code>

Responsible for loading data from the collected reports into the database. Includes connection to the database, processing of column names and types (for proper loading into the database).

<details close>
<summary>Class and Methods</summary>
<br>
 
Methods:
- <code>upload_files</code> Loads all output files from the destination folder of the previous script (where processed and merged reports are stored).
- <code>columns_change_name</code> To correctly assign a name to the fields in the database, you need to correct the name of the columns of the datasets.
- <code>punctuation_search</code> Search for punctuation for correct processing of queries used to load data into the database.
- <code>columns_punctuation</code> Search for punctuation inside each column (by values).
- <code>columns_edit</code> Processing values with punctuation inside the value. Excluding columns in the exclusion list (information will follow).
- <code>db_connect</code> Connecting to the database.
 
Class:
- <code>get_column_type</code> Checking columns for data type to correctly determine the data type of fields in the database.
- <code>create_table</code> Creating a table, the name is determined by the name of the dataframe.
- <code>alter_columns</code> For automation, columns from the dataframe are added alternately.
- <code>insert_rows</code> Adding rows to a table.
  
<br>
</details> 

Required external files: 
- <code>database_config.json</code> - to connect to the desired database.
- <code>exception_list.json</code> - for exception columns, because not all columns with string values must be processed. Manual input is possible if there is no file.

Both files can be created using the scripts in the depository [additional files](additional%20files/)

# License

All Scripts are released under BSD 3-Clause "New" or "Revised" license as found in the [license file](/LICENSE).
