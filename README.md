Introduction
-------------
Sparkify is a startup company which provides music streaming service to the users through their app. The song information (song id, song name, artist etc.) and the user activity data (user id, user action, etc.) from the app are currently collected and stored in the form of JSON files.

For querying the JSON data to find the meaningful insights, Sparkify should create a database to analyze the JSON files and run their analytical queries to identify different user patterns and provide recommendations to their users.

One of the most efficient way Sparkify can use to design their database is STAR schema with n number of dimensional tables connected to one fact table. Using this approach will help in fast query execution, analysis and aggregations for reporting as well as implementing complex business rules.
In this project, I have implemented the STAR schema approach for database creation and ETL using python for processing the Sparkify data (JSON files) into the database to run analytical queries for song play analysis of Sparkify users.

Tool Stack used
---------------
Database: Postgres
Programming Language: Python 3

Prerequisites
-------------
Python Libraries:
•	psycopg2 - To connect to Posgres database rom python 
•	pandas – To perform ETL using dataframes

Libraries can be installed using the below command.
pip install LibraryName

Database
--------
    
STAR Design
------------

Dimension Tables
-----------------

o	users - users in the app   
    
    Schema: user_id, first_name, last_name, gender, level
    
o	songs - songs in music database 
    
    Schema: song_id, title, artist_id, year, duration
    
o	artists - artists in music database 

    Schema: artist_id, name, location, latitude, longitude

o	time - timestamps of records in songplays broken down into specific units 

    Schema: start_time, hour, day, week, month, year, weekday

Fact Table
----------

o	songplays records in log data associated with song plays

    Schema: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

Database Process
----------------
•	Generate the tables using the python script

ETL Process
-----------
•	Read the song and log datasets
•	Load songs, artists dimension tables from songs_data JSON files
•	Load users, time dimension tables from log_data JSON files
•	Load the songplays fact table from dimension table 

Scripts
--------

1.	sql_queries.py
This script contains SQL queries to drop and create the dimension and fact tables for the project 

2.	create_tables.py
This script contains the python commands to execute the SQL queries defined in the sql_queries.py to generate the tables. Functions used in this script are:
o	create_database: Drop and creates the database 
o	drop_tables: Drops the dimension and fact tables 
o	create_tables: Creates the dimension and fact tables

3.	etl.ipynb

This python jupyter notebook reads a single file from song_data and log_data and extracts and transforms the columns required for the tables and load that data into your tables. 

4.	etl.py
This python script reads all files from song_data and log_data and extracts and transforms the columns required for the tables and load that data into your tables. Functions used in this script are:
o	process_song_file: Read and process the songs dataset to load songs and artists tables
o	process_log_file: Read and process the logs dataset to load users, time and songplays tables
o	process_data: Read the all file paths of songs and logs dataset and provide them to process_song_file and process_log_file as a parameter to process data into tables

5.	test.ipyb:
This is test script to check if data is loaded into the dimension and fact tables


Project Execution
-----------------
Execute the scripts in the below order to generate the database tables and perform ETL

1.	create_tables.py

    Command: python create_tables.py

2.	etl.ipynb or etl.py
    Command: python etl.py

3.	test.ipynb
