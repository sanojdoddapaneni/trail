# AKHILA MORA

**Introduction** –  
In this project, pdf of incident summary report is downloaded from the given link of norman.gov website. These incidents are stored in 5 columns in pdf. Our goal of the project is to read the content of the incidents from the pdf and create a database and then return the total number of incidents sorted numerically in decending order and the name of incidents in alphabetical order. This project is developed in Ubuntu in GCP using python.

**Sources** –   
*URL considered - https://www.normanok.gov/sites/default/files/documents/2022-03/2022-02-28_daily_incident_summary.pdf  
Sources for Regular Expressions –   
re.sub() – https://docs.python.org/3/library/re.html  
re.split() – https://stackoverflow.com/questions/41220172/regex-to-splitstring-on-date-and-keep-it  
pandas DataFrame for separating and inserting into the table (incidents) – https://www.geeksforgeeks.org/python-pandas-dataframe/  
sqlite3 source and execution – https://docs.python.org/3.8/library/sqlite3.html*  

**Installation directions** –  
In this project, packages urllib, pypdf, tempfile, re, sqlite3 and argparse are used where urllib, argparse and tempfile packages are inbuilt with python and remaining packages can be installed using commands –  
```pipenv install <package name>```  

A Pipfile is generated and provided in the repository which will install all the libraries nd requirments with the command ```pip .```  

**Project Description** –   

**main.py file** –  
This file is created in the directory project0 which call the functions of project0.py by importing the project0 directory and its functions and execute then by using command –  
```pipenv run python project0/main.py –incidents <url>``` (followed by URL of PDF without the # symbol).  

**project0.py** –  
This python file consists of code for the functions that are called in the main file.  

Firstly, the packages required are imported which are mentioned in Installation directions.

**fetchincidents(url)** –  
This function is used to read the data from the url of the pdf using urllib package and returns the pdf to be unsed by other functions.

**extractincidents()** –  
This function first collects the data from fetchincidents() and then stores it into temporary file using tempfile package. Now, the package pypdf package is used to read the pdf pages and its data accordingly. Package re (regular expressions) is used to parse the information collected in the string form using re.sub() and re.split() methods and then, split the data from 0 to the end of string into 5 columns according to the pdf which can be fed to database.

**createdb()** –  
This function is used to create database normanpd.db and then create the table incidents in the database with the columns incident_time, incident_number, incident_location, nature and incident_ori using SQL commands. Initially, connection is established to the database using sqlite3 package and then we execute the drop table command to clean any previous table created as incidents and then execute create table command. SQL commands are executed using execute() method. This only creates the table incidents and does not process or take any actions on the data extracted in extractincidents() function.

**populatedb()** –  
This function is used to insert our data extracted in extractincidents() into the incidents table created in created(). We use insert into command of SQL using sqlite3 package and insert the processed data into the incidents table.

**status()** –  
This function is used to print the desired output which is nature of incidents according to its count.
**Test cases** – 

We have created a new directory called tests and then created a file called test_download.py which contains different functions of test cases for each function in project0.py. Each test case in the file is explained below accordingly.

Firstly, we import the packages sys to execute test file for all the directories of the project and provide the path accordingly and then import project0 folder and project0.py within the folder and then finally we should import package pytest to run testcases accordingly. Pyest modules works on pytest framework and can be installed using pipenv install pytest command.

We declare a url which we considered for project0 and write the tests accordingly.

**test_fetchincidents()** –  
Here, we call the functions fetchincidents() from project0.py and check it with our own url and arrest true accordingly using if statement.

**test_extractincidents()** –  
In this function, we take output of extractincidents() from project0.py and assert not None.

**test_createdb()** –  
This function take the db from createdb() function from project0.py and compare it to the db in test case. Using if condition if the createdb() has normanpd.db the test case will be passed.

**test_populatedb()** –  
Here, we run the popuatedb() function from project0.py and assert true for test case to be passed.

**test_status()** –  
Here, we check for not None condition of output which calls status() function from project0.py and the test is passed accordingly.

**Possible Bugs** - 

In test_download.py we run test cases for each function considering the URL declared in the test_download.py and the normanpd.db database. Any changes to this database name or URL will result in failed test cases for the test functions. Further, when using pandas, dataFrames should be associated to their columns and same column names should be given in intert SQL command in populatedb() function. It will result in error when the column declaration is removed.

At the end, these files are added, committed and pushed into git hub using git commands accordingly for each file.
