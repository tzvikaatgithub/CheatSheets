# ===  Introduction to PostgreSQL Psycopg2 ===

# We will use the same script as the sqlite.py (see above) but we will modify it to make it work with PostGreSQL

# first we have to change the package that handles the database from sqlite3 to psycopg2


# Install Python package for PostgreSQL
# psycopg2 must be installed

# in addition postgresql must also be installed
https://postgresql.org/download
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib

# see more about the installation and usage on digital ocean
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04
# you can install Visual Studio or a pre-compiled python library for psycopg2 a .whl file
# below is a comprehansive installation of psycopg2 instructions for Ubuntu16.04
https://www.fullstackpython.com/blog/postgresql-python-3-psycopg2-ubuntu-1604.html

sudo apt-get install postgresql libpq-dev postgresql-client postgresql-client-common
sudo -H pip3 install psycopg2



# Access PostgreSQL from CLI and create database etc
# access without switching account
sudo -u postgres psql

# quit
\q

# create new database
sudo -u postgres createdb <dbname>

# create new user
# it doesn't need to be a supersuer to crud database
sudo -u postgres createuser --interactive

# or if you login
sudo -u postgres psql
CREATE DATABASE height_collector;
CREATE USER tester WITH PASSWORD 'test_password';

# if username and db match then user will be able to access the db
# otherwise you need to login as superuser and grant it priveledges
GRANT ALL PRIVILEGES ON DATABASE "<dbname>" to <username>;
