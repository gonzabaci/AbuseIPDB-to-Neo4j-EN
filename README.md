# AbuseIPDB-to-Neo4j-EN
Project that uses the AbuseIPDB API to extract information from IPs that have performed some type of attack in the last 90 days, generating a CSV file with the IPs, the dates of the attacks, and the corresponding categories. This file can be subsequently loaded into Neo4j to generate a graph diagram.
* Para leer el proyecto en español, visite https://github.com/gonzabaci/AbuseIPDB-to-Neo4j-ES
# Contents
* in.txt: Text file where a maximum of 100 IP addresses should be entered, one below the other.
* main.py: Python script that allows connecting to the AbuseIPDB API.
* out.csv: Output file that will contain the results of the query.
* requirements.txt: File that contains a list of dependencies required to run the script.
  
# System requirements
* Python 3
* Neo4j
* AbuseIPDB API Key

# Installation and usage (Windows)
These instructions provide a guide to download and run the data extraction script, as well as to load the results into Neo4j. I hope they are useful for you!

1. Clone or download this repository.
2. Obtain an AbuseIPDB API Key.
3. Install the requirements with "pip install -r requirements.txt".
4. Enter your AbuseIPDB API key in main.py (line 19).
5. Enter the IP addresses in the in.txt file. Remember that the maximum allowed per day by AbuseIPDB is 100 IP addresses.
6. Run the script through the terminal using the command "python.exe main.py". The query results will be displayed in the out.csv file.
7. Download and install Neo4j from https://neo4j.com/download/.
8. Run Neo4j and create a new project. Select "New" and then "Create project".
9. Add a database to the project by clicking on "Add" and then "Local DBMS". Enter a name and password for the database and click "Create".
10. Navigate to the folder ``` "C:\Users\<user>\.Neo4jDesktop\relate-data\dbmss" ``` and copy the csv file "out.csv" into the latest created database, in the folder named "import". The full path would be ``` "C:\Users\<user>\.Neo4jDesktop\relate-data\dbmss\<your dbms>\import" ```.
11. Start the database from Neo4j. Click "open" to open the database.
12. Run the following command in the Neo4j terminal:

```
load csv with headers from "file:///out.csv" as row
FIELDTERMINATOR ","
merge (IP:ip{ip:row.IP})
merge (CATEGORIES:categories{categories:row.CATEGORIES})
merge (IP)-[:HAS_CATEGORY {relation_date:row.DATE}]->(CATEGORIES)
```
# Example
![Example graph diagram](https://i.imgur.com/hepYpGi.jpeg)

