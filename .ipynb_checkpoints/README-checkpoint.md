# Data Warehouse Modeling in Redshift for Sparkify

## Purpose of database and analytical goals

The startup 'Sparkify' captures its data on songs, artists, users and also records transactions of when a song is played, and this data in stored in S3 buckets in song_data and log_data directories.

Using this data, Sparkify will be able to come up with insights such as:
- Which locations have the highest volume of music usage?
- Which are the most popular artists?
- Are there any seasonal variations? And which are the most common times of day for music usage?

But for doing so, we need to transform this source data into a form that is more easily consumable for analytics. The purpose of the database is to create a star schema model based on this data to enable fast read access.

## Schema design and ETL pipeline

The tables are created using the create_tables.py script, which connects to the Redshift cluster database. After this, the ETL pipeline is used to copy the song_data and long_data files from the S3 bucket to staging tables. The purpose of the staging tables is to replicate the source data, as an intermediate step before inserting values into our fact and dimension tables to make sure we do not mess up the source data. After this, appropriate joins are created for the fact and dimension tables.

The output tables we have are:
- fact_songplay
- dim_user
- dim_artist
- dim_song
- dim_time

Since this is a star schema, this enables for fast read access to fact table for performing advanced analytics.

### Files in repository

sql_queries.py - The script that contains all SQL queries that need to be run for this project - create, drop, copy into staging tables, load values into fact/dimension tables etc.
create_tables.py - Functions to create and drop tables, by pulling in statements from sql_queries.py
etl.py - Functions to load into staging tables, and then into fact/dimension tables.

### How to run this project

- Add credentials to dwh.cfg file
- Run create_tables.py to drop and create tables.
- Run etl.py to load into staging tables and then load into fact and dimension tables.

### References

https://stackoverflow.com
https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-security-groups.html
https://github.com/san089/Udacity-Data-Engineering-Projects/blob/master/Data_Warehouse/sql_queries.py (Line 191 for timestamp conversion)
