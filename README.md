# Container for pydbtester
This code is used to create a contianer that uses pyodbc that will allow you to test connectivity to a SQL database using a container.  Use the sample yaml file and add the correct args for your database connection string.

1. Connection String: format for pyodbc is "DRIVER={ODBC Driver 17 for SQL Server};SERVER=<serverFQDN>;DATABASE=<database>;UID=<username>;PWD=<password>"
2. <table> Table you want to query
3. <#ofRows> Amount of rows you would like to query

note on the connection string: The image contains the ODBC Driver 17 and must be included in the string for the connection to work.  You may need username@serverFQDN when logging into Azure hosted SQL.

# YAML
```
apiVersion: v1
kind: Pod
metadata:
  name: dbtester
  labels:
    app: dbtester
spec:
  nodeSelector:
    beta.kubernetes.io/os: linux
  containers:
  - name: dbtester
    image: benparker/pydbtester:latest
    imagePullPolicy: Always
    command: ["python3"]
    args: ["-u", "dbtester.py", "DRIVER={ODBC Driver 17 for SQL Server};SERVER=<serverFQDN>;DATABASE=<database>;UID=<username>;PWD=<password>", "<table>", "<#ofRows>"]
```
