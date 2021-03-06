# Overview

Current project demonstrate how to build a talend job which will manipulate data coming from an Heroku Postgres Database.

Different kind of job have been built.

- UC, M_UC and H_UC : Used for data transformation from an input table to an output table
- BULK_LOAD_TO_SF : Used to demonstrate how to cal Bulk API V2 Talend component to upload data from an input table to Salesforce
- TEST_CHRONO_AND_SENDING : used to demonstrate how to chronometer job processment and send it to Salesofrce through LOG_DURATION subjob

# Prerequisites

- Have a Heroku Postgres Plan with some available Tables.
- Have Talend Open Studio 7.1
- For Bulk Job, have a developer edition with a configured connected app (JWT Flow)

# Guide Line to Install and Deploy Talend Jobs into Heroku App

1) With you text editor, Create a property file with the name of you choice with all these value setted properly according to the type of talend job you want to launch
```
	DB_PG_Login=
	DB_PG_Server=
	DB_PG_Password=
	DB_PG_AdditionalParams=
	DB_PG_Database=
	DB_PG_Port=
	DB_PG_Schema=
	DB_DESCR=
	DB_COMMIT_EVERY=
	SF_LOGIN=
	SF_PWD=
	SF_JWT_ISSUER=
	SF_JWT_AUDIENCE=
	SF_BULK_FILE_PATH=
	SF_LOG_URL=
	SF_LOG_CLIENTSECRET=
	SF_LOG_CLIENTID=
	SF_LOG_CL_SECRET=
	TLD_TMP_FILE=
	TLD_CONFIG_FILE=
	TLD_ROOT_PATH=
```

2) Clone Project

3) Open Project with Talend Open Studio. You will find different kind of job which can be executed in a Heroku Dyno in interaction with a Heroku-Postgres Database

4) Go into the context of the project and set the proper value of TLD_CONFIG_FILE value according to your property filename

5) Export Project to your file system

6) Unzip project exported and add your property file created on step 1) in the folder at the root

7) Compress folder and Rename zip extension with jar

8) Deploy jar on your Heroku app
	```
	heroku deploy:jar <your jar> --app <your heroku app name>
	```
9) To test, open a bash session on your app, uncompress the jar	and execute job sh
	```
	heroku run bash -a <your heroku app name> -s <dyno plan>
	```
Exemple : 
		```
		heroku run bash -a myapp -s performance-l
		```

10) Eventually log your activity : 
		```
		heroku logs --tail -a <your heroku app name>
		```
