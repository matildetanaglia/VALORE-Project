# VALORE-Project
A docker-compose file of a Docker Application aimed at the multidimentional data analysis. 

The docker-compose file contains all the images needed for the creation and the support of the Data Warehouse Level and ANalysis/User Level of a Data Warehouse.

1. redis (image: redis:4.0.5-alpine)    
2. notebooks (implemented by the dockerfile) -> creation and population of postgreSQL database
3. postgres (image: clkao/postgres-plv8)
4. pgadmin (image: dpage/pgadmin4) -> visualization of the database
5. bi_server (image: kmnrstzaiou/pentaho-bi-saiku) -> visualization of the data mart content and OLAP operations


# Requirements:

- docker (https://docs.docker.com/desktop/)
- java (java 8)
- schema workbench (https://sourceforge.net/projects/mondrian/files/schema%20workbench/3.6.1-stable/psw-ce-3.6.1.zip) 
- PostreSQL library for schema workbench: https://jdbc.postgresql.org/download.html -> “PostgreSQL JDBC 4.2 Driver , 42.2.18”. 
  Drag this file inside the schema-workbench directory "drivers".

                                                ############################################
                                                #  Installation of the Docker Application: #
                                                ############################################
                                                
N.B.1 choose a **password** for the pgAdmin and Postgres enviroment section in the docker-compose file and save the changes.
N.B.2 the pentaho **credential** are: user = admin and password = password.


# Instruction:

1. Enter in the terminal and go in the path where you save the docker-compose file and the Dockerfile (they must be in the same directory)
    a. run the command: docker-compose up
       this command will install all the needed images (if not already installed) and open all the connections to the local host ports. 
       Do not quit from the terminal until you want to exit from the application.
       
2. open the browser and go to: localhost:5050
   In this port is present PgAdmin. We use this port for enstamblish the connection and visualize the database content.
   
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
   
   a. Create the file for the creation and population of the database. We suggest to support the population phase of the database with the code. 
      This will be helpfull for the reproducibility of the activities and for the sharing phase (every one that use your docker application will have exactly the        
      same database).
   
   
   
   
   
   
   
   
   
   
   
   
   
   
