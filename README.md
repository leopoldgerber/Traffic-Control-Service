# Traffic Control Service

The repository contains scripts for working with the platform. A complex task is the collection of reports for a selected period to analyze competitor traffic, which will help the company to determine the place for expansion, as well as provide an opportunity to analyze the marketing strategy of other companies. 

## Functions performed by scripts:

### 1 - Download Data

Main parser

### 2 - Data Preprocessing

### 3 - DB Upload

Responsible for loading data from the collected reports into the database. Includes connection to the database, processing of column names and types (for proper loading into the database).

Required external files: 
- <code>database_config.json</code> - to connect to the desired database.
- <code>exception_list.json</code> - for exception columns, because not all columns with string values must be processed. Manual input is possible if there is no file.

Both files can be created using the scripts in the depository [additional files](additional%20files/)


A script for downloading reports for a selected period, for selected domains. 
Emulates downloading a person, to bypass account blocking. Contains random values for the height of the scroll in both directions, making pauses between transitions and pauses before and after pressing buttons.
Passes through each domain in turn with the reporting categories selected for it. The storage location of the downloaded reports is set by the user. The selected location will be used for further assembly of all reports, including the processing of these reports.

NOTE: The best solution is to use scripts 1 and 2 in tandem in one run, since the variables from script 1 contain the lists of domains by category. Modification is possible to display the list of processed domains by category in separate files. 

<br>

<details close>
<summary>Read more about domains by category</summary>
<br>
Since downloadable reports, in most cases, do not have a domain in the name, it is necessary to consider the result of the download. In addition to the division by month (1 month - 1 report), there are also subcategories that form 1 category (1 subcategory - 1 report).
  
### There are three results of downloads: 
1 - the report was successfully downloaded and contains all the data.
2 - the report was downloaded, but does not contain data (no data from the platform side).
3 - the report cannot be downloaded, because the platform has not updated the data for you
</details> 

<br>


Скрипт для скачивания отчетности за выбранный период, по выбранным доменам. 
Эмулирует скачивание человека, для обхода блокировки аккаунта. Содержит рандомными значениями для высоты скролла в обе стороны, совершение пауз между переходами и пауз до и после нажатий кнопок.
Проходится поочередно по каждому домену с выбранными для него категориям отчетностей. Место хранения скаченных отчетов задает пользователь. Выбранное место будет использоваться для дальнейшей сборки всех отчетности, в том числе и обработки этих отчетов.

NOTE: Наилучшим решением будет использовать скрипт 1 и 2 в связки в одном запуске, так как переменные из скрипта 1 содержат списки доменов по категориям. 
Подробнее о доменах по категориям: Так как скачиваемые отчеты, в большинстве случаев, не имеют в названии домен, то необходимо учитывать результат скачивания. Помимо разделения по месяцам (1 месяц - 1 отчет), существуют еще подкатегории, которые формируют 1 категорию (1 подкатегория - 1 отчет). 

Существует три результат скачиваний: 
1 - отчет был удачно скачен и содержит все данные.
2 - отчет был скачен, но не содержит данные (нет данных со стороны платформы).
3 - отчет невозможно скачать, так как платформа не обновила данные за выбранный период.
