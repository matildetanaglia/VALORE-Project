# VALORE-Project
A docker-compose file of a Docker Application aimed at the multidimensional data analysis. 

The docker-compose file contains all the images needed for the creation and the support of the Data Warehouse Level and ANalysis/User Level of a Data Warehouse.

1. redis (image: redis:4.0.5-alpine)    
2. notebooks (implemented by the dockerfile) -> creation and population of postgreSQL database
3. postgres (image: clkao/postgres-plv8)
4. pgadmin (image: dpage/pgadmin4) -> visualization of the database
5. bi_server (image: kmnrstzaiou/pentaho-bi-saiku) -> visualization of the data mart content and OLAP operations


## Requirements:

- docker (https://docs.docker.com/desktop/)
- java (java 8)
- schema workbench (https://sourceforge.net/projects/mondrian/files/schema%20workbench/3.6.1-stable/psw-ce-3.6.1.zip) 
- PostreSQL library for schema workbench: https://jdbc.postgresql.org/download.html -> “PostgreSQL JDBC 4.2 Driver , 42.2.18”. 
  Drag this file inside the schema-workbench directory "drivers".

##  Installation of the Docker Application: 
                                                
N.B.1 choose a **password** for the pgAdmin and Postgres environment section in the docker-compose file and save the changes.

N.B.2 we assume that the data source are csv files.


### Instruction:

1. Enter in the terminal and go in the path where you save the docker-compose file and the Dockerfile (they must be in the same directory)
    a. run the command: docker-compose up
       this command will install all the needed images (if not already installed) and open all the connections to the localhost ports.
       If everything is well done, docker creates three directories _notebooks_, _postgres-data_, _redis-data_ .
       Do **not quit** from the terminal until you want to exit from the application.
       
2. open the browser and go to: localhost:5050
   In this port is present PgAdmin. We use this port to establish the connection and visualize the database content.
   
   a. create a new server ("Add New Server")
   b. compile the server settings (as written in the docker-compose file)
      - Name: user@domain.com
      - Host name/address: postgres
      - Port: 5432
      - Maintenance database: postgres
      - Username: postgres
      - Password: *******
       
2. open the browser and go to: localhost:8888
   In this port is present Jupyter Notebook. 
   
   a. Create a file _.ipynb_ for the creation and population of the database. We suggest supporting the population phase of the database with the code. 
      This will be helpful for the reproducibility of the operations and for the sharing phase (everyone that uses your docker application will have 
      exactly the same database).
      
      You will find an example of this in the _Create_DB_example.ipynb_. For the correct execution of this file you have to:
      - change all the passwords with the correct one;
      - change db_name and schema_name with the correct ones;
      - create within the _notebooks_ directory of this application a directory named "CSV" in which you put all the csv files of your database;
      - create within the _notebooks_ directory of this application a postgres_create_tables.sql file with the _create table_ command of all your database tables   
        (the corresponding csv files);
      - create within the _notebooks_ directory of this application the _source_model.rb_ file and import it.
      
   b. Create a file _.ipynb_ for the data mart tables creation (actually, in this project we use the ROLAP approach). We suggest supporting the population phase of 
      the data mart with the code. This will be helpful for the reproducibility of the operations and for the sharing phase (everyone that uses your docker 
      application will have exactly the same data mart tables).
      - fact table implementation e population;
      - dimention tables implementation e population.
      
3. open the browser and go to: localhost:8080
   In this port is present Pentaho with the Saiku extension.
   
   a. Insert the access credential:
      - Username: admin
      - Password: password
   
   b. create the connection with the Postgres database:
      Follow these instructions:
      - Manage Data Sources -> New Data Source
        • Data source name: user@domain.com
        • Source Type: Database Table(s)
        Press the **+** symbol
      - Connection Name: user@domain.com
        Database Type: PostgreSQL
        Access: Naive (JDBC)
        Settings:
          Host Name: postgres
          Database Name: db_name
          Port Number: 5432
          Username: postgres
          Password: ******
        Press **Test** (the connection should have success)
      
4. open another terminal and enter in the _schema-workbench_ directory 
   - run the command: ./workbench.sh
     Then the application will open.
   - press Option -> Connection...
   - Connection Name: user@domain.com
        Database Type: PostgreSQL
        Access: Naive (JDBC)
        Settings:
          connection name: user@domain.com
          Host name: localhost
          Database name: db_name
          Port Number: 8890
          Username: postgres
          Password: ******
         Press **Test** (the connection should have success)
         Press **Ok**
    - Create a new schema for the desired data mart
    - Publish the schema through the connection

5. reload the browser page: localhost:8080
   - Press Create New -> Saiku Analytics -> Create New Query
   - Select your data mart

6. Multidimensional Analysis with Saiku
   
   
   
   
   
   
   
   
   
   
   
   
