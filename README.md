# Tech Task FELD M
This repository contains my solutions for the tech task provided by [FELD M](https://www.feld-m.de/en/).

## Table of Contents
* [Project Description](#project-description)
* [Installation Guide](#installation-guide)
* [utils Module](#utils-module)
* [Task 1 to 4](#task-1-to-4)
* [Task 5 and transactions Module](#task-5-and-transactions-module)


## Project Description
This project contains the following files: <br/>

```
* utils.py: contains utility functions used in the tasks 1, 2, 3 and 4.
* task1.py: contains solution script for task 1.
* task2.py: contains solution script for task 2.
* task3.py: contains solution script for task 3.
* task4.py: contains solution script for task 4.
* task5.py: contains solution script for task 5.
* transactions.py: a module contains a utility class used in task 5. 
* README.md: This file.
* transactions.db: sqlite database provided by FELD M.
* transactions.csv: csv file generated by task3.py script
* eurofxref-hist-90d.xml: xml file containing the exchange rates provided by FELD M.
```

## Installation Guide
Please make sure that a python version >= 3.5 and pip are installed in your machine. <br />
if not, you can download them from this link : [https://www.python.org/downloads/](https://www.python.org/downloads/). <br/>
In task 5 we used the external library psycopg2, you can install it, by running the following command in a terminal (or cmd for windows): <br />

`pip install psycopg2`

In <b> task 5 </b> an installation of <b> PostgreSQL </b> server is required. 
According to your operating system, follow the provided link for installation instructions : <br/>

* <b> [Windows](https://www.postgresqltutorial.com/postgresql-getting-started/install-postgresql/) </b>
* <b> [Linux ](https://www.postgresqltutorial.com/install-postgresql-linux/)</b>
* <b> [Mac OS ](https://www.postgresqltutorial.com/install-postgresql-macos/)</b>

## utils Module

In order to avoid code duplication and centralize used functions in multiple tasks, I created the module utils wich contains the following functions :<br/>
```
def connect_and_execute_query(sql_query: str) -> list: 
```
This function will connect to the provided SQLite database and execute the sql query passed in parameters. <br/>

The function will return a list containing the result of the sql query execution. <br/>

```
def extract_exchange_rates(file=EUROFXREF_XML, currency='USD') -> dict:
```
Function used in task 2 in order to extract exchage rates from the provided xml file. <br/>

```
def find_day_with_most_revenue(result: list) -> tuple:
```
Function used in task 2, it will process the result of a sql query in order to find the day with most revenue created by mobile phone users.<br/>

## Task 1 to 4

Each script contains a solution for the given tasks. 

E.g task1.py contains a function named task1_solution() wich contains the script to solve the task. <br/>

To run each script, use following command in a terminal from the project directory :

```
Python task1.py
```


## Task 5 and transactions Module

The standard DB-API for interacting with relational databases is defined in a standard interface for Python database access modules. It is documented in [PEP 249 Python Database API specification V2.0 ](https://peps.python.org/pep-0249/). 

Modules, such as **sqlite3** and **psycopg**, are available for most of the popular relational databases, and a number of non-relational databases as well.

The Python DB-API specifies a way to connect to databases and issue commands to them. This gives the advantage that there is a standard way to write code that deals with a database using connections and cursors.

This was the main idea behing my solution for task 5 in order to add support to other DBMS; I created a class that abstract the database manipulation: connection, disconnection, sql execution, etc. 

The class **TransactionsDBManager** constructor takes into parameters the database type : 'sqlite' or 'postgres' in our case.

After that, the class will allow the user to manage the two databases in the same manner.

In order to demostrate the utility of the class TransactionsDBManager, I used it in task5.py to do the following tasks : <br/>

1/ Copy the transactions sqlite database into a postgres database. <br/>

2/ Solve task 1 with postgresql and sqlite databases using two objects of the class TransactionsDBManager. <br/>
