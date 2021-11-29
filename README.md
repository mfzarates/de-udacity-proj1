Project summary:
----------------
Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. 
Objective: To create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project

How it works:
-------------
Primary analytics is to understand what songs users are listening to.
Step 1:
- To create a start schema with songs as the main target variable.

sql_queries.py: containts the SQL queries to build the tables, to insert rows and a SELECT query to find song_id and artist_id based on the song name, artist name and song length. 

create_tables.py: connects to the database and builds a sparkify database if doesn't exists. Once the database is created, this fils executes the SQL queries in sql_queries.py to build tables in the schema.

etl.py: processes the JSON files containing song, artist, user and songplay data into the tables. It also uses pandas library to perform some aspects of the ETL

etl.ipynb: implements the same script as etl.py, but on a single song file and log file.

test.ipynb: contains a number of SQL query to test the contents of the various tables after the ETL has been performed


How to use the scripts:
-----------------------
To build the schema(or to drop the tables and rebuild them)
python create_tables.py

To execute the ETL to load data into the tables:
```
python etl.py
```
Some queries used to test the results of the ETL using test.ipynb:

to combine artist name and song title:
```
%sql SELECT name, title FROM songs NATURAL JOIN artists LIMIT 5;
```

to view rows that appear on all 5 tables:
```
%sql SELECT * \
FROM songplays JOIN songs ON songplays.song_id = songs.song_id \
JOIN artists ON songplays.artist_id = artists.artist_id \
JOIN time ON songplays.start_time =  time.start_time \
JOIN users ON songplays.user_id = users.user_id \
LIMIT 5;
```

to check which rows have a song_id:
```
%sql SELECT * FROM songplays WHERE song_id != 'None' LIMIT 5;
```
