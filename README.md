# dblogs

dblogs is a collection of Helm Charts that setup reverse proxies or
scheduled jobs to collect database logs. The main use case for these
logs is security audit and compliance. 

## Why ?

Online databases do not recommend logging of all activity on the database
because the logging infrastructure may interfere with the performance of 
the database. The recommended solution is a reverse proxy which acts as a
bastion node and captures all the activity.

Data Warehouse and Data Lake Engines do provide ways to capture all activity.
However there is no standard way to capture these logs. This project captures
the best practices to capture activity logs.

## Supported Databases
1. [MySQL](mysqllogs/README.md)
