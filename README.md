# FOLIO Reporting SIG - Project: Build a directory of extracted and derived tables

## Project description
https://wiki.folio.org/display/RPT/Build+a+directory+of+extracted+and+derived+tables

| Type | Description |
|:-----|:------------|
| Extracted tables | Tables that LDP creates. |
| Derived tables | Tables created by the community and located in the folio-analytics repository. |

## Dependencies
* Python 3
* Python modules
  *  cryptography
  *  csv
  *  io
  *  os
  *  pandas
  *  psycopg2
  *  requests
  *  tabulate

## Directories
* ```/data```
  * ```/csv```: Contains a CSV file that can used to create additional data for each derived table for enrichment.
  * ```/mermaid```: Here you can create text files for each derived table. In these text files you can type in mermaid syntax. The content is used to generate an er diagram in the output.
* ```/Output```: Contains the output files. In this repository you can find sample outputs.
* ```/python```
  *  ```data_pipeline.py```: The main script wich has to be used.
  *  ```key_generator.py```: Script to create a KEY-FILE and an encrypted file with login credentials.
  *  ```/pkg_output```: Contains local modules to create different outputs.
* ```/sql```
  *  ```/derived_tables```: Contains the query for querying information about derived tables from the PostgresSQL database catalog.

## Usage

* The Python script is written for Python 3 and tested for metadb. 
* It can be necessary to install additional modules (see [Dependencies](#Dependencies)). 
* It assumes that derived tables exist in metadb.

### Preparation
1\. Download the repository.

2\. Database login credentials: You need login credentials for your database. 
* The login credentials can be directly entered in the script ```/python/data_pipeline.py```. 
* **Optional:** You can create an KEY-FILE to connect with the database with the script ```/python/key_generator.py```. At first create a csv file with the name ```credentials.csv```. In this file enter your login credentials. Schema: hostname,database,username,pwd,port_id . Save this file in the subdirectory ```/python```. After that run the script ```/python/key_generator.py```. The script creates a file with the name ```enc_credentials.csv``` and a file with the name ```config.key```. Now you can delete the file ```credentials.csv```. The login credentials are now encrypted in the file ```enc_credentials.csv``` and can only decrypted with the KEY-FILE ```config.key```.

3\. **Optional:** Fill out the CSV file in the subdirectory ```/data/csv```. The data to be added to the data from the database is stored in the CSV file. In the CSV file, the "table" and "attributeName" columns must be filled out as they are stored in the database. A matching takes place later via these attributes. You can check the information beforehand using the SQL query in the ```/sql/derived_tables``` subdirectory.

4\. **Optional:** You can create a text file in the subdirectory ```/data/mermaid``` if you would like create an er diagram for a derived table. Inside the text file you only have to enter the mermaid syntax. The text file name must match the name of the derived table.

### Run the program
You can run the program by using the file ```/python/data_pipeline.py```.

### Output
The generated output files with the documentation have been created in the ```/Output``` directory.
