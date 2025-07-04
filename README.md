# Linkedin Job Postings <img src="https://github.com/user-attachments/assets/db0a41d5-d211-4066-9853-1b93d96c938d" alt="Descripción de la imagen" width="50" height="50">

👥 Team Contributions


Ashutosh Khadse:
Led the initial phases of the project, focusing on data extraction and transformation. He was instrumental in setting up the PostgreSQL database using SQLAlchemy, ensuring efficient data loading and management.
Also, Focused on automation, visualization, and data cleaning. He developed Apache Airflow DAGs to automate the ETL pipeline, conducted data cleaning operations, and created comprehensive dashboards in both Power BI Desktop and Power BI Cloud to visualize the processed data.

Abhijeet Sushir:
Specialized in data preprocessing tasks. He handled the imputation of missing values, standardization of data formats, and removal of duplicates, contributing significantly to the integrity of the dataset.

Hardik Kelotra:
Managed the integration of external data sources through APIs. He was responsible for fetching additional job postings via RapidAPI, performing exploratory data analysis, and incorporating the new data into our existing PostgreSQL schema.

## Overview
In this project, we are going to analyze, manipulate and visualize data about job postings in Linkedin, as part of an ETL project. We used SQLAlchemy as an Object-Relational Mapping (ORM) tool connected to PostgreSQL, and we will generate visual representations using PowerBI.

## Tools used

- Python
    
- Pandas
    
- PowerBI
    
- SQLAlchemy
    
- PostgreSQL
    
- Jupyter Notebook

## Repository Organization:
Our repository has a folder called Data, which is where the datasets in xlsx format that we use for the development of the project are. It also has the notebook where all the code and functionalities of the project were created except for the visualizations that were created with Power BI. In the repository there is also the README of the project and the requirements.txt

## Dataset used
For this project, we used 3 datasets, extracted from Kaggle, the first of which was: It contains 28 columns and 33246 rows that correspond to some works published on Linkedin.
The columns names of “job_postings.csv” before data transformation are:

1. job_id: The job ID as defined by LinkedIn

2. company_id: Identifier for the company associated with the job posting (maps to companies.csv)

3. title: Job title.

4. description: Job description.

5. max_salary: Maximum salary

6. med_salary: Median salary

7. min_salary: Minimum salary

8. pay_period: Pay period for salary (Hourly, Monthly, Yearly)

9. formatted_work_type: Type of work (Fulltime, Parttime, Contract)

10. location: Job location

11. applies: Number of applications that have been submitted

12. original_listed_time: Original time the job was listed

13. remote_allowed: Whether job permits remote work

14. views: Number of times the job posting has been viewed

15. job_posting_url: URL to the job posting on a platform

16. application_url: URL where applications can be submitted

17. application_type: Type of application process (offsite, complex/simple onsite)

18. expiry: Expiration date or time for the job listing

19. closed_time: Time to close job listing

20. formatted_experience_level: Job experience level (entry, associate, executive, etc)

21. skills_desc: Description detailing required skills for job

22. listed_time: Time when the job was listed

23. posting_domain: Domain of the website with application

24. sponsored: Whether the job listing is sponsored or promoted.

25. work_type: Type of work associated with the job

28. currency: Currency in which the salary is provided.

29. compensation_type: Type of compensation for the job.

The second data set that we use is called "job_industries" and has 2 columns (job_id and industry_id) where each job is related to an id of an industry. We use this dataset later (section 3) as well as our third dataset (industries). The columns names of “job_industries” before data transformation are:

1. job_id: The job_id column corresponds to the job_id's found in our first dataset
2. industry_id: The industry_id column corresponds to an id assigned to each industry to be related to each job later.

The third data set that we used is called "industries" and has 2 columns (industry_id and industry_name ) where the industry_id is the id corresponding to each industry and the industry_name column is the name associated with that industry_id. The columns names of "industries" before data transdormation are:

1. industry_id: Id assigned to each industry
2. industry_name: Industry name

## Requirements

- Python 3x 

- PostgreSQL 16x (psycopg2)
  
- Openpyxl
  
- Matplotlib
  
- PowerBI desktop
  
- SQLAlchemy
  
- JSON credentials file (keys.json) with the next format:
```json
{
"user": "your_user",
"password": "your_password",
"port": "your_postgres_number_port",
"server": "your_server_address",
"db": "your_database_name"
}
```
## Project Setup

1. Clone de repository:
```bash
```
2. Go to the project directory:
```bash
cd linkedin_job_postings_etl
```
3. Create a virtual environment:
```bash
python -m venv env
```
4. Activate virtual environment:
```bash
.\venv\Scripts\activate
```
5. Install libraries:
```bash
pip install -r requirements.txt
```
6. Create a database in PostgreSQL
7. The project have an Jupyter Notebook, "eda.ipynb" and this notebook is divided into 4 sections :
- We recommend you start with section #1: Import the modules, make the connection to the database, and load the data into it.
    ##### Note: In this section, you must change the name of the JSON file to the name of the JSON file that you need to create to be able to make the connection to the database. In our case the name of my file was `keys.json`. If you decide to name your file the same way, remember to change the values specified in the `Database Configuration` field located in the README.
- The second step is to execute section 2, which is where the exploratory analysis carried out on the 3 tables with which we initially worked is located.
- The third step is to run section 3, which is where the merge, imputing & standardization
- The fourth step is to run section 4, which was where we created the new table (our final table) in postgreSQL
  
8. Go to Power BI:

  
8.1 Create a new dashboard.

8.2 Select the option Get/Import data and search PostgresSQL Database


8.3 Insert your PostgreSQL server and your database name and accept:



8.4 If you manage to connect to the database the following will appear:


##### Note: For our analysis and the creation of our visualizations we used the LinkedinSalary table since this table was where the entire imputation, filtering and standardization procedure was carried out. Basically it is our final table

8.6 Congrats!, you can now select the table you want to work with, you can upload it to the dashboard and make your own dashboard

## Our Dashboard
Here is our dashboard: [Our Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNjM2ZTg5NGItMDUwZi00YmRlLTg4M2UtNDRmNjEyZDMwYTU1IiwidCI6IjY5M2NiZWEwLTRlZjktNDI1NC04OTc3LTc2ZTA1Y2I1ZjU1NiIsImMiOjR9)

# Linkedin Job Postings - ETL - Part # 2 :chart_with_downwards_trend: :open_file_folder:

## Overview
To carry out the second part of our project, we make our dimensional model from our dataset resulting from the first part of the project. Subsequently, we look for an API to make queries to bring data about more job postings and to be able to further expand our original dataset taking into account its columns. For this second part, we used the same tools used for the development of the first part, only a new one was added, which was Rapid Api, which was where we found the API to bring more job postings.
We also updated the structure of our project by organizing it by folders and added an additional Jupyter Notebook "API_eda" which was where the eda was done to the results of the API, the structural creation of the table in Postgres and finally the insertion of the data into the table

## Dimensional Model

To create our dimensional model we used Power BI and the process was as follows:

1. Verify that you already have the table created (in Postgres) with the transformations
##### Remember: The table with the transformations is the same one that you select to perform the visualizations in step 8.6 in the first part

2. Repeat steps 8, 8.1, 8.2 and 8.3 of the first part, when you have connected to postgres you select the table that was mentioned in the previous step
##### Note: In order to connect to your database you must take into account the json file that you created at the beginning of the project, since there you defined the username, password, port, server (where postgres will run) and the name of the database that are you going to use

3. When selecting the table and loading it, you will right click on it to duplicate it, in our case we made 4 different tables, since we took out our fact table, and 3 dimensions connected to it

4. Having the 4 different tables, what we did was select the columns that each dimension was going to have, including the fact table

Leaving our dimensional model like this:



5  Finally, we only make our visualizations by selecting the columns or items of each dimension that we would use to make the graphs.

##### Note: The relationships were made through job_id between the fact table and the dimensions

## API

For the API part it is necessary to have a Google account preferably, it is also worth noting that in order to use an API you have to subscribe to it and take into account the number of requests/queries that it allows you to make to that API from the basic plan (that means free), additionally, some credentials are necessary, which the application gives you once you register to be able to make requests to the API


In our case, we had to create several Google accounts to be able to make several requests, then we had to save those results in a csv to be able to perform the exploratory analysis and based on that analysis, perform the respective transformations from a Jupyter Notebook.

Some transformations were:

- Removal of duplicate data
- Standardization of columns with abbreviated data such as location or type of work
- Salary Outliers (imputing)
- Delete the “remote_ratio” column

Subsequently, the table structure for postgres was created and the transformed data was inserted into the aforementioned table.

We connect to postgres like this in steps 8, 8.1, 8.2 and 8.3, we select the table with the name we gave it when creating it

And now we can make the graphs. This is our API dashboard: [Our API Dashboard](Visualizations/dimensional_model_visual.pdf)


# Linkedin Job Postings - ETL - Part #3 (Final Part)

## Overview
To carry out the third and final part of our project, we include new tools and processes such as Apache Airflow for the automation of our project and the tasks that will be shown later. Additionally, the Apache Kafka "tool" was implemented to stream the data through a topic that was created to be able to stream the data through a producer and be received by a consumer to be sent to a Power BI real-time dashboard. Finally in this final stage of our project, we added Great Expectations to our project. This process allowed us to perform a thorough validation, ensuring that the data meets predefined standards and criteria. Through Great Expectations, we verify crucial aspects such as consistency, integrity, validity and accuracy of our data sets. This included checking consistency between different fields, identifying outliers or null values, as well as validating data formats and ranges.

We use the following expectations:

- Expect Column Values to not be Null: This expectation ensures that none of the rows in a specific column contain null values (or None in Python).

- Expect Column Values to be Greater than: This expectation checks that all values in a column are greater than a specific value.

- Expect Column Values to match Regex: This expectation checks that the values in a column match a specific regular expression (regex).

- Expect Column Values to Match Strftime format: This expectation checks that the values in a column match a specified date and time format using the strftime format.

##### Note: For the final part of our project we decided to do it on a virtual machine with Ubuntu operating system as an alternative to Docker to run Airflow and Kafka.


## Tools Finally Used

- Python
    
- Pandas
    
- PowerBI (Desktop for part 1 & 2 and Cloud for Final Part)
    
- SQLAlchemy
    
- PostgreSQL
    
- Jupyter Notebook

- Apache Kafka

- Apache Airflow

- Great Expectations

- VM with Ubuntu System for Final Part


## Project Workflow
This is the project workflow:


## How to run this project:

First of all, to be able to run the project and later kafka, you need to have kafka installed in the virtual machine and kafka-python within the virtual environment and Apache Airflow. Here are the steps to run the project:


Once Kafka is installed, a Kafka folder should be created where you have downloaded it and subsequently extracted it.


1. Create a database in PostgreSQL
2. The project have an Jupyter Notebook, "eda.ipynb" and this notebook is divided into 4 sections :
- We recommend you start with section #1: Import the modules, make the connection to the database, and load the data into it.
  
    ##### Note: In this section, you must change the name of the JSON file to the name of the JSON file that you need to create to be able to make the connection to the database. In our case the name of my file was keys.json. If you decide to name your file the same way, remember to change the values specified in the Database Configuration field located in the README.
  
- The second step is to execute section 2, which is where the exploratory analysis carried out on the 3 tables with which we initially worked is located.
- The third step is to run section 3, which is where the merge, imputing & standardization
- The fourth step is to run section 4, which was where we created the new table (our final table) in postgreSQL


#### Note: If you still have doubts, you can review section 1 and 2 of the readme to understand well and replicate the steps for creating the tables.


3. Running airflow

Once the tables are created in postgres you can start airflow

3.1 Airflow Standalone
The first step now is to do the following command in a different terminal but not from vscode, preferably a cmd of the operating system and inside the project directory:

```bash
export AIRFLOW_HOME=$(pwd)
```

Once the command is done, you can do the command from Visual Studio Code but in this way:
```bash
export AIRFLOW_HOME=${pwd}
```


Once that command is done the next command is:
```bash
airflow standalone
```

Once the airflow command is done it will start running


3.2 Airflow Login
Once airflow has started running, the password to access airflow will appear in the console as follows:



Then, you will access the url localhost:8080 where you will be greeted with a login menu like this:

You will set the user admin and the password that appeared in the console (In any case, at the root of the project a file standalone_admin_password.txt will be created) where the password will be for the user and be able to enter airflow

Once you have logged in, the created dag will appear and you will be able to access it and it will look something like this:

Now you can start running the dag, once the entire dag has been run you should see something like this:


#### Considerations: Just when the dag goes through the task (transform_db_task) I recommend you go to a cmd of the operating system and do the following:

```bash
cd Folder_Where_Kafka_Has_Been_Extracted
```

```bash
cd kafka
```

And we recommed you to open 3 differents terminals and that within the 3 terminals you are inside kafka (cd kafka).

once inside the kafka folder, this command will be done in the first terminal:
```bash
./bin/zookeeper-server-start.sh config/zookeeper.properties
```

In the second terminal, you will do the following command:
```bash
./bin/kafka-server-start.sh config/server.properties
```

In the third terminal, you will do the following command:

```bash
./bin/kafka-topics.sh --delete --topic linkedin.streaming --bootstrap-server localhost:9092
```

Finally, you will go to the consumer.py file (which is located inside the dags/dags_connections folder) and you will run the consumer file, the producer does not need to run it because it will be done automatically when the dag reaches the producer task

#### Note: You should keep in mind that the process may take a little while because there are several tasks and the process is somewhat delayed and slow.

Once the data has been sent, you will go to power BI, in our case Power BI cloud and you will do the following:



Select the Dashboard option or in Spanish "Panel"


Select Edit option and then add icon:



Select "Datos de transmision personalizados"



And there you can add a new set of transmission data


The API option is selected:


Once you select the API, you will be asked to enter the columns that you will use for the transmission and their respective data type. Once this is completed, the url of the dashboard will appear in real time like this:


Once you create the new set, a blank canvas will open where you can put the graphs and the data will arrive and complete the dashboard like this:


In our case, once the data arrived, this is how the dashboard looked like:



## Thanks:
This is how our project ends, once the dashboard has run you can check pgadmin where you will see the dimensions and the fact table that was created during the load task.

Thank you for visiting our repository


