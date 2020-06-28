# AWS Cloud Data Warehouse

## Background

Sparkify, a music streaming startup, has grown the user base and song database and want to move their data onto the cloud. The data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in the app.

As a data engineer, my role is to build an ETL pipeline that extracts the data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for the analytics team to continue finding insights in what songs that users are listening to, and run queries for testing purposes. 


## Datasets

- Song data: s3://udacity-dend/song_data
- Log data: s3://udacity-dend/log_data
- Log data json path: s3://udacity-dend/log_json_path.json


## Configuration

1. Fill all the fields of `dwh.cfg', except only two fields are left empty: 
 - `HOST` (inside the `DB` configuration section) 
 - And the `ARN` (inside the `IAM_ROLE` configuration section) 

2. Creating a new AWS Redshift Cluster
```sh
python aws_create_cluster.py
```

3. Checking the cluster availability 

- run several times until the cluster becomes available: 

```sh
python aws_check_cluster_available.py
```

4. Destroying the cluster 

- After the ETL process done, destroy it with a single command: 

```sh
python aws_destroy_cluster.py
```

## The ETL Process

 - `python create_tables.py` - create new fact and dimension tables for the star schema in Redshift;
 - `python etl.py` - two principal tasks:
     - load data from S3 into staging tables on Redshift ;
     - translate data from the staging tables to the analytical tables with `INSERT ... SELECT` statements

## Analyzing the results

 - `python analyze.py` 
 return the counting of each analytical table.

