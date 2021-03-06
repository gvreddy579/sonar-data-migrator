sonar-data-migrator
===================

Utility to migrate data from one Sonar instance to other ones.

This tool is for the case where you are managing sonar instance and then decide to merge it to another sonar instance which already have many projects. 
In this case you can't import dump (you know ids can't be duplicated and other referential data need change as per new autogenerated id in new DB). 
This tool let you migrate all/project wise data to another sonar instance.

To use it, follow below steps.

1.  Run maven install on the project, it will create bineries zip under target/assemly folder. 
2.	Extract zip on machine from where you have access to both sonar server DB.
3.	Do sonar analysis on both source and target sonar with same code.
4.	configure source and target db details in database.properties file
5.	run init.sql on target sonar db, it will create temporary tables to store migrated data details
6.	set proper java path in script.bat file (you can use script.sh for executing on linux) .

Usage

* run the bat/sh script passing users as argument for migration of users
* run the bat/sh script passing data as first argument and project key as per "Key" value in sonar report as second argument. If key is not passed, it will work for all projects in db.

Note that script is idempotent meaning that running it multiple times doesn't create any issue as data already migrated won't migrate again. This script will migrate below things

1.	Users (default sonar-users role is assigned to all migrated users)
2.	Action plans associated to the project
3.  All changes to issue like assignee,severity,status,action plan and resolution
4.	All reviews/comments added to issue
5.	All false positive data