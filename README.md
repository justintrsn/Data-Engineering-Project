# INITIAL ELT PROJECT
This repo is a simple project using Docker and PostgreSQL to demonstrate a simple ELT process. This project is directly taken from [Freecodecamp](https://www.youtube.com/watch?v=PHsC_t0j1dU&t=4654s) for my own learning.

## Repository Structure
1. **`docker-compose.yaml`**: This file contains the configuration for Docker Compose, which is used to orchestrate multiple Docker containers. It defines three services:
- `source_postgres`: The source PostgreSQL database.
- `destination_postgres`: The destination PostgreSQL database.
- `elt_script`: The service that runs the ELT script.

2. `elt_script/Dockerfile`: This Dockerfile sets up a Python environment and installs the PostgreSQL client. It also copies the ELT script into the container and sets it as the default command.

3. `elt_script/elt_script.py`: This Python script performs the ELT process. It waits for the source PostgreSQL database to become available, then dumps its data to a SQL file and loads this data into the destination PostgreSQL database.

4. `source_db_init/init.sql`: This SQL script initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, and inserts sample data into these tables.

## How it works
1. `Docker Compose`: Using the docker-compose.yaml file, three Docker containers are spun up:

- A source PostgreSQL database with sample data.
- A destination PostgreSQL database.
- A Python environment that runs the ELT script.

2. `ELT Process`: The elt_script.py waits for the source PostgreSQL database to become available. Once it's available, the script uses `pg_dump` to dump the source database to a SQL file. Then, it uses `psql` to load this SQL file into the destination PostgreSQL database.

3. `Database Initialization`: The `init.sql` script initializes the source database with sample data. It creates several tables and populates them with sample data.

## Running this Project

1. Install and run `docker` and `docker-compose` on your machine
2. Clone this repo
3. `cd` to this repo and `docker compose up`
4. After the ELT process completes, you can access the source and destination PostgreSQL databases on ports 5433 and 5434, respectively.

