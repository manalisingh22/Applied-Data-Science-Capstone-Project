<p style="text-align:center">
    <a href="https://skills.network/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDS0321ENSkillsNetwork865-2023-01-01">
    <img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png" width="200" alt="Skills Network Logo"  />
    </a>
</p>

<h1 align=center><font size = 5>Assignment: SQL Notebook for Peer Assignment</font></h1>

Estimated time needed: **60** minutes.

## Introduction
Using this Python notebook you will:

1.  Understand the Spacex DataSet
2.  Load the dataset  into the corresponding table in a Db2 database
3.  Execute SQL queries to answer assignment questions 


## Overview of the DataSet

SpaceX has gained worldwide attention for a series of historic milestones. 

It is the only private company ever to return a spacecraft from low-earth orbit, which it first accomplished in December 2010.
SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars wheras other providers cost upward of 165 million dollars each, much of the savings is because Space X can reuse the first stage. 


Therefore if we can determine if the first stage will land, we can determine the cost of a launch. 

This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.

This dataset includes a record for each payload carried during a SpaceX mission into outer space.


### Download the datasets

This assignment requires you to load the spacex dataset.

In many cases the dataset to be analyzed is available as a .CSV (comma separated values) file, perhaps on the internet. Click on the link below to download and save the dataset (.CSV file):

 <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/data/Spacex.csv" target="_blank">Spacex DataSet</a>



**Navigate to the Go to UI screen** 

* Refer to this insruction in this <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20Sign%20up%20for%20IBM%20Cloud%20-%20Create%20Db2%20service%20instance%20-%20Get%20started%20with%20the%20Db2%20console/instructional-labs.md.html">link</a> for viewing  the   Go to UI screen. 


* Later click on **Data link(below SQL)**  in the Go to UI screen  and click on **Load Data** tab.  



* Later browse for the downloaded spacex file.



<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/images/browsefile.png" width="800">


* Once done select the schema andload the file.  


 <img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/images/spacexload3.png" width="800">
 



If you are facing a problem in uploading the dataset (which is a csv file), you can follow the steps below to upload the .sql file instead of the CSV file:

* Download the file <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/datasets/Spacex%20.sql">Spacex.sql</a>

* Later click on **SQL** in the  **Go to UI Screen**.

* Use the **From file** option to browse for the **SQL** file and upload it.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/images/sqlfile.png">

* Once you upload the script,you can use the **Run All** option to run all the queries to insert the data.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/images/runall.png">

    



```python
!pip install --force-reinstall ibm_db==3.1.0 ibm_db_sa==0.3.3
!pip install sqlalchemy==1.3.24
!pip uninstall ipython-sql -y
!pip install ipython-sql==0.4.1
```

    Collecting ibm_db==3.1.0
      Using cached ibm_db-3.1.0-cp310-cp310-linux_x86_64.whl
    Collecting ibm_db_sa==0.3.3
      Using cached ibm_db_sa-0.3.3-py3-none-any.whl
    Collecting sqlalchemy>=0.7.3
      Using cached SQLAlchemy-2.0.9-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.7 MB)
    Collecting greenlet!=0.4.17
      Using cached greenlet-2.0.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (613 kB)
    Collecting typing-extensions>=4.2.0
      Using cached typing_extensions-4.5.0-py3-none-any.whl (27 kB)
    Installing collected packages: ibm_db, typing-extensions, greenlet, sqlalchemy, ibm_db_sa
      Attempting uninstall: ibm_db
        Found existing installation: ibm-db 3.1.0
        Uninstalling ibm-db-3.1.0:
          Successfully uninstalled ibm-db-3.1.0
      Attempting uninstall: typing-extensions
        Found existing installation: typing_extensions 4.5.0
        Uninstalling typing_extensions-4.5.0:
          Successfully uninstalled typing_extensions-4.5.0
      Attempting uninstall: greenlet
        Found existing installation: greenlet 2.0.2
        Uninstalling greenlet-2.0.2:
          Successfully uninstalled greenlet-2.0.2
      Attempting uninstall: sqlalchemy
        Found existing installation: SQLAlchemy 1.3.24
        Uninstalling SQLAlchemy-1.3.24:
          Successfully uninstalled SQLAlchemy-1.3.24
      Attempting uninstall: ibm_db_sa
        Found existing installation: ibm-db-sa 0.3.3
        Uninstalling ibm-db-sa-0.3.3:
          Successfully uninstalled ibm-db-sa-0.3.3
    Successfully installed greenlet-2.0.2 ibm_db-3.1.0 ibm_db_sa-0.3.3 sqlalchemy-2.0.9 typing-extensions-4.5.0
    Collecting sqlalchemy==1.3.24
      Using cached SQLAlchemy-1.3.24-cp310-cp310-linux_x86_64.whl
    Installing collected packages: sqlalchemy
      Attempting uninstall: sqlalchemy
        Found existing installation: SQLAlchemy 2.0.9
        Uninstalling SQLAlchemy-2.0.9:
          Successfully uninstalled SQLAlchemy-2.0.9
    Successfully installed sqlalchemy-1.3.24
    Found existing installation: ipython-sql 0.4.1
    Uninstalling ipython-sql-0.4.1:
      Successfully uninstalled ipython-sql-0.4.1
    Collecting ipython-sql==0.4.1
      Using cached ipython_sql-0.4.1-py3-none-any.whl (21 kB)
    Requirement already satisfied: prettytable<1 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (0.7.2)
    Requirement already satisfied: ipython>=1.0 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (8.4.0)
    Requirement already satisfied: ipython-genutils>=0.1.0 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (0.2.0)
    Requirement already satisfied: sqlalchemy>=0.6.7 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (1.3.24)
    Requirement already satisfied: six in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (1.16.0)
    Requirement already satisfied: sqlparse in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython-sql==0.4.1) (0.4.3)
    Requirement already satisfied: pexpect>4.3 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (4.8.0)
    Requirement already satisfied: matplotlib-inline in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (0.1.6)
    Requirement already satisfied: decorator in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (5.1.1)
    Requirement already satisfied: backcall in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (0.2.0)
    Requirement already satisfied: setuptools>=18.5 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (65.6.3)
    Requirement already satisfied: prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (3.0.20)
    Requirement already satisfied: stack-data in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (0.2.0)
    Requirement already satisfied: jedi>=0.16 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (0.18.1)
    Requirement already satisfied: traitlets>=5 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (5.1.1)
    Requirement already satisfied: pickleshare in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (0.7.5)
    Requirement already satisfied: pygments>=2.4.0 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from ipython>=1.0->ipython-sql==0.4.1) (2.11.2)
    Requirement already satisfied: parso<0.9.0,>=0.8.0 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from jedi>=0.16->ipython>=1.0->ipython-sql==0.4.1) (0.8.3)
    Requirement already satisfied: ptyprocess>=0.5 in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from pexpect>4.3->ipython>=1.0->ipython-sql==0.4.1) (0.7.0)
    Requirement already satisfied: wcwidth in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0->ipython>=1.0->ipython-sql==0.4.1) (0.2.5)
    Requirement already satisfied: executing in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from stack-data->ipython>=1.0->ipython-sql==0.4.1) (0.8.3)
    Requirement already satisfied: asttokens in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from stack-data->ipython>=1.0->ipython-sql==0.4.1) (2.0.5)
    Requirement already satisfied: pure-eval in /opt/conda/envs/Python-3.10/lib/python3.10/site-packages (from stack-data->ipython>=1.0->ipython-sql==0.4.1) (0.2.2)
    Installing collected packages: ipython-sql
    Successfully installed ipython-sql-0.4.1


### Connect to the database

Let us first load the SQL extension and establish a connection with the database



```python
%load_ext sql
```




**DB2 magic in case of  UI service credentials.**



<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/images/servicecredentials.png" width="600">  

* Use the following format.

* Add security=SSL at the end

**%sql ibm_db_sa://my-username:my-password@my-hostname:my-port/my-db-name?security=SSL**



```python
%sql ibm_db_sa://mdr04626:289Pj0V7hVe6QYUE@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb?security=SSL
```

## Tasks

Now write and execute SQL queries to solve the assignment tasks.

### Task 1




##### Display the names of the unique launch sites  in the space mission



```python
%sql Select Distinct Launch_Site from Spacey
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>launch_site</th>
    </tr>
    <tr>
        <td>CCAFS LC-40</td>
    </tr>
    <tr>
        <td>CCAFS SLC-40</td>
    </tr>
    <tr>
        <td>KSC LC-39A</td>
    </tr>
    <tr>
        <td>VAFB SLC-4E</td>
    </tr>
</table>




### Task 2


#####  Display 5 records where launch sites begin with the string 'CCA' 



```python
%sql select * from Spacey where Launch_Site like 'CCA%'
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>DATE</th>
        <th>time__utc_</th>
        <th>booster_version</th>
        <th>launch_site</th>
        <th>payload</th>
        <th>payload_mass__kg_</th>
        <th>orbit</th>
        <th>customer</th>
        <th>mission_outcome</th>
        <th>landing__outcome</th>
    </tr>
    <tr>
        <td>04-06-2010</td>
        <td>18:45:00</td>
        <td>F9 v1.0  B0003</td>
        <td>CCAFS LC-40</td>
        <td>Dragon Spacecraft Qualification Unit</td>
        <td>0</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Failure (parachute)</td>
    </tr>
    <tr>
        <td>08-12-2010</td>
        <td>15:43:00</td>
        <td>F9 v1.0  B0004</td>
        <td>CCAFS LC-40</td>
        <td>Dragon demo flight C1, two CubeSats, barrel of Brouere cheese</td>
        <td>0</td>
        <td>LEO (ISS)</td>
        <td>NASA (COTS) NRO</td>
        <td>Success</td>
        <td>Failure (parachute)</td>
    </tr>
    <tr>
        <td>22-05-2012</td>
        <td>07:44:00</td>
        <td>F9 v1.0  B0005</td>
        <td>CCAFS LC-40</td>
        <td>Dragon demo flight C2</td>
        <td>525</td>
        <td>LEO (ISS)</td>
        <td>NASA (COTS)</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>08-10-2012</td>
        <td>00:35:00</td>
        <td>F9 v1.0  B0006</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-1</td>
        <td>500</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>01-03-2013</td>
        <td>15:10:00</td>
        <td>F9 v1.0  B0007</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-2</td>
        <td>677</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>03-12-2013</td>
        <td>22:41:00</td>
        <td>F9 v1.1</td>
        <td>CCAFS LC-40</td>
        <td>SES-8</td>
        <td>3170</td>
        <td>GTO</td>
        <td>SES</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>06-01-2014</td>
        <td>22:06:00</td>
        <td>F9 v1.1</td>
        <td>CCAFS LC-40</td>
        <td>Thaicom 6</td>
        <td>3325</td>
        <td>GTO</td>
        <td>Thaicom</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>18-04-2014</td>
        <td>19:25:00</td>
        <td>F9 v1.1</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-3</td>
        <td>2296</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Controlled (ocean)</td>
    </tr>
    <tr>
        <td>14-07-2014</td>
        <td>15:15:00</td>
        <td>F9 v1.1</td>
        <td>CCAFS LC-40</td>
        <td>OG2 Mission 1  6 Orbcomm-OG2 satellites</td>
        <td>1316</td>
        <td>LEO</td>
        <td>Orbcomm</td>
        <td>Success</td>
        <td>Controlled (ocean)</td>
    </tr>
    <tr>
        <td>05-08-2014</td>
        <td>08:00:00</td>
        <td>F9 v1.1</td>
        <td>CCAFS LC-40</td>
        <td>AsiaSat 8</td>
        <td>4535</td>
        <td>GTO</td>
        <td>AsiaSat</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>07-09-2014</td>
        <td>05:00:00</td>
        <td>F9 v1.1 B1011</td>
        <td>CCAFS LC-40</td>
        <td>AsiaSat 6</td>
        <td>4428</td>
        <td>GTO</td>
        <td>AsiaSat</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>21-09-2014</td>
        <td>05:52:00</td>
        <td>F9 v1.1 B1010</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-4</td>
        <td>2216</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Uncontrolled (ocean)</td>
    </tr>
    <tr>
        <td>10-01-2015</td>
        <td>09:47:00</td>
        <td>F9 v1.1 B1012</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-5</td>
        <td>2395</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Failure (drone ship)</td>
    </tr>
    <tr>
        <td>11-02-2015</td>
        <td>23:03:00</td>
        <td>F9 v1.1 B1013</td>
        <td>CCAFS LC-40</td>
        <td>DSCOVR</td>
        <td>570</td>
        <td>HEO</td>
        <td>U.S. Air Force NASA NOAA</td>
        <td>Success</td>
        <td>Controlled (ocean)</td>
    </tr>
    <tr>
        <td>02-03-2015</td>
        <td>03:50:00</td>
        <td>F9 v1.1 B1014</td>
        <td>CCAFS LC-40</td>
        <td>ABS-3A Eutelsat 115 West B</td>
        <td>4159</td>
        <td>GTO</td>
        <td>ABS Eutelsat</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>14-04-2015</td>
        <td>20:10:00</td>
        <td>F9 v1.1 B1015</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-6</td>
        <td>1898</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Failure (drone ship)</td>
    </tr>
    <tr>
        <td>27-04-2015</td>
        <td>23:03:00</td>
        <td>F9 v1.1 B1016</td>
        <td>CCAFS LC-40</td>
        <td>Turkmen 52 / MonacoSAT</td>
        <td>4707</td>
        <td>GTO</td>
        <td>Turkmenistan National Space Agency</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>28-06-2015</td>
        <td>14:21:00</td>
        <td>F9 v1.1 B1018</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-7</td>
        <td>1952</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Failure (in flight)</td>
        <td>Precluded (drone ship)</td>
    </tr>
    <tr>
        <td>22-12-2015</td>
        <td>01:29:00</td>
        <td>F9 FT B1019</td>
        <td>CCAFS LC-40</td>
        <td>OG2 Mission 2  11 Orbcomm-OG2 satellites</td>
        <td>2034</td>
        <td>LEO</td>
        <td>Orbcomm</td>
        <td>Success</td>
        <td>Success (ground pad)</td>
    </tr>
    <tr>
        <td>04-03-2016</td>
        <td>23:35:00</td>
        <td>F9 FT B1020</td>
        <td>CCAFS LC-40</td>
        <td>SES-9</td>
        <td>5271</td>
        <td>GTO</td>
        <td>SES</td>
        <td>Success</td>
        <td>Failure (drone ship)</td>
    </tr>
    <tr>
        <td>08-04-2016</td>
        <td>20:43:00</td>
        <td>F9 FT B1021.1</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-8</td>
        <td>3136</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success (drone ship)</td>
    </tr>
    <tr>
        <td>06-05-2016</td>
        <td>05:21:00</td>
        <td>F9 FT B1022</td>
        <td>CCAFS LC-40</td>
        <td>JCSAT-14</td>
        <td>4696</td>
        <td>GTO</td>
        <td>SKY Perfect JSAT Group</td>
        <td>Success</td>
        <td>Success (drone ship)</td>
    </tr>
    <tr>
        <td>27-05-2016</td>
        <td>21:39:00</td>
        <td>F9 FT B1023.1</td>
        <td>CCAFS LC-40</td>
        <td>Thaicom 8</td>
        <td>3100</td>
        <td>GTO</td>
        <td>Thaicom</td>
        <td>Success</td>
        <td>Success (drone ship)</td>
    </tr>
    <tr>
        <td>15-06-2016</td>
        <td>14:29:00</td>
        <td>F9 FT B1024</td>
        <td>CCAFS LC-40</td>
        <td>ABS-2A Eutelsat 117 West B</td>
        <td>3600</td>
        <td>GTO</td>
        <td>ABS Eutelsat</td>
        <td>Success</td>
        <td>Failure (drone ship)</td>
    </tr>
    <tr>
        <td>18-07-2016</td>
        <td>04:45:00</td>
        <td>F9 FT B1025.1</td>
        <td>CCAFS LC-40</td>
        <td>SpaceX CRS-9</td>
        <td>2257</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success (ground pad)</td>
    </tr>
    <tr>
        <td>14-08-2016</td>
        <td>05:26:00</td>
        <td>F9 FT B1026</td>
        <td>CCAFS LC-40</td>
        <td>JCSAT-16</td>
        <td>4600</td>
        <td>GTO</td>
        <td>SKY Perfect JSAT Group</td>
        <td>Success</td>
        <td>Success (drone ship)</td>
    </tr>
    <tr>
        <td>15-12-2017</td>
        <td>15:36:00</td>
        <td>F9 FT  B1035.2</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-13</td>
        <td>2205</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success (ground pad)</td>
    </tr>
    <tr>
        <td>08-01-2018</td>
        <td>01:00:00</td>
        <td>F9 B4 B1043.1</td>
        <td>CCAFS SLC-40</td>
        <td>Zuma</td>
        <td>5000</td>
        <td>LEO</td>
        <td>Northrop Grumman</td>
        <td>Success (payload status unclear)</td>
        <td>Success (ground pad)</td>
    </tr>
    <tr>
        <td>31-01-2018</td>
        <td>21:25:00</td>
        <td>F9 FT  B1032.2</td>
        <td>CCAFS SLC-40</td>
        <td>GovSat-1 / SES-16</td>
        <td>4230</td>
        <td>GTO</td>
        <td>SES</td>
        <td>Success</td>
        <td>Controlled (ocean)</td>
    </tr>
    <tr>
        <td>06-03-2018</td>
        <td>05:33:00</td>
        <td>F9 B4 B1044</td>
        <td>CCAFS SLC-40</td>
        <td>Hispasat 30W-6  PODSat</td>
        <td>6092</td>
        <td>GTO</td>
        <td>Hispasat  NovaWurks</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>02-04-2018</td>
        <td>20:30:00</td>
        <td>F9 B4  B1039.2</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-14</td>
        <td>2647</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>18-04-2018</td>
        <td>22:51:00</td>
        <td>F9 B4 B1045.1</td>
        <td>CCAFS SLC-40</td>
        <td>Transiting Exoplanet Survey Satellite (TESS)</td>
        <td>362</td>
        <td>HEO</td>
        <td>NASA (LSP)</td>
        <td>Success</td>
        <td>Success (drone ship)</td>
    </tr>
    <tr>
        <td>04-06-2018</td>
        <td>04:45:00</td>
        <td>F9 B4  B1040.2</td>
        <td>CCAFS SLC-40</td>
        <td>SES-12</td>
        <td>5384</td>
        <td>GTO</td>
        <td>SES</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>29-06-2018</td>
        <td>09:42:00</td>
        <td>F9 B4 B1045.2</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-15</td>
        <td>2697</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>22-07-2018</td>
        <td>05:50:00</td>
        <td>F9 B5B1047.1</td>
        <td>CCAFS SLC-40</td>
        <td>Telstar 19V</td>
        <td>7075</td>
        <td>GTO</td>
        <td>Telesat</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>07-08-2018</td>
        <td>05:18:00</td>
        <td>F9 B5 B1046.2</td>
        <td>CCAFS SLC-40</td>
        <td>Merah Putih</td>
        <td>5800</td>
        <td>GTO</td>
        <td>Telkom Indonesia</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>10-09-2018</td>
        <td>04:45:00</td>
        <td>F9 B5B1049.1</td>
        <td>CCAFS SLC-40</td>
        <td>Telstar 18V / Apstar-5C</td>
        <td>7060</td>
        <td>GTO</td>
        <td>Telesat</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>05-12-2018</td>
        <td>18:16:00</td>
        <td>F9 B5B1050</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-16</td>
        <td>2500</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Failure</td>
    </tr>
    <tr>
        <td>23-12-2018</td>
        <td>13:51:00</td>
        <td>F9 B5B1054</td>
        <td>CCAFS SLC-40</td>
        <td>GPS III-01</td>
        <td>4400</td>
        <td>MEO</td>
        <td>USAF</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>22-02-2019</td>
        <td>01:45:00</td>
        <td>F9 B5 B1048.3</td>
        <td>CCAFS SLC-40</td>
        <td>Nusantara Satu, Beresheet Moon lander, S5</td>
        <td>4850</td>
        <td>GTO</td>
        <td>PSN, SpaceIL / IAI</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>04-05-2019</td>
        <td>06:48:00</td>
        <td>F9 B5B1056.1</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-17, Starlink v0.9</td>
        <td>2495</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>24-05-2019</td>
        <td>02:30:00</td>
        <td>F9 B5 B1049.3</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink v0.9, RADARSAT Constellation</td>
        <td>13620</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>25-07-2019</td>
        <td>22:01:00</td>
        <td>F9 B5 B1056.2</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-18, AMOS-17 </td>
        <td>2268</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>06-08-2019</td>
        <td>23:23:00</td>
        <td>F9 B5 B1047.3</td>
        <td>CCAFS SLC-40</td>
        <td>AMOS-17, Starlink 1 v1.0 </td>
        <td>6500</td>
        <td>GTO</td>
        <td>Spacecom</td>
        <td>Success</td>
        <td>No attempt</td>
    </tr>
    <tr>
        <td>11-11-2019</td>
        <td>14:56:00</td>
        <td>F9 B5 B1048.4</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 1 v1.0, SpaceX CRS-19 </td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>05-12-2019</td>
        <td>17:29:00</td>
        <td>F9 B5B1059.1</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-19, JCSat-18 / Kacific 1 </td>
        <td>2617</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS), Kacific 1</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>17-12-2019</td>
        <td>00:10:00</td>
        <td>F9 B5 B1056.3</td>
        <td>CCAFS SLC-40</td>
        <td>JCSat-18 / Kacific 1, Starlink 2 v1.0 </td>
        <td>6956</td>
        <td>GTO</td>
        <td>Sky Perfect JSAT, Kacific 1</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>07-01-2020</td>
        <td>02:33:00</td>
        <td>F9 B5 B1049.4</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 2 v1.0, Crew Dragon in-flight abort test </td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>29-01-2020</td>
        <td>14:07:00</td>
        <td>F9 B5 B1051.3</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 3 v1.0, Starlink 4 v1.0 </td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>17-02-2020</td>
        <td>15:05:00</td>
        <td>F9 B5 B1056.4</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 4 v1.0, SpaceX CRS-20</td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Failure</td>
    </tr>
    <tr>
        <td>07-03-2020</td>
        <td>04:50:00</td>
        <td>F9 B5 B1059.2</td>
        <td>CCAFS SLC-40</td>
        <td>SpaceX CRS-20, Starlink 5 v1.0 </td>
        <td>1977</td>
        <td>LEO (ISS)</td>
        <td>NASA (CRS)</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>04-06-2020</td>
        <td>01:25:00</td>
        <td>F9 B5 B1049.5</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 7 v1.0, Starlink 8 v1.0</td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX, Planet Labs</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>13-06-2020</td>
        <td>09:21:00</td>
        <td>F9 B5 B1059.3</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 8 v1.0, SkySats-16, -17, -18, GPS III-03 </td>
        <td>15410</td>
        <td>LEO</td>
        <td>SpaceX, Planet Labs</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>30-06-2020</td>
        <td>20:10:46</td>
        <td>F9 B5B1060.1</td>
        <td>CCAFS SLC-40</td>
        <td>GPS III-03, ANASIS-II</td>
        <td>4311</td>
        <td>MEO</td>
        <td>U.S. Space Force</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>20-07-2020</td>
        <td>21:30:00</td>
        <td>F9 B5 B1058.2</td>
        <td>CCAFS SLC-40</td>
        <td>ANASIS-II, Starlink 9 v1.0</td>
        <td>5500</td>
        <td>GTO</td>
        <td>Republic of Korea Army, Spaceflight Industries (BlackSky)</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>18-08-2020</td>
        <td>14:31:00</td>
        <td>F9 B5 B1049.6</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 10 v1.0, SkySat-19, -20, -21, SAOCOM 1B </td>
        <td>15440</td>
        <td>LEO</td>
        <td>SpaceX, Planet Labs, PlanetIQ</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>30-08-2020</td>
        <td>23:18:00</td>
        <td>F9 B5 B1059.4</td>
        <td>CCAFS SLC-40</td>
        <td>SAOCOM 1B, GNOMES 1, Tyvak-0172</td>
        <td>3130</td>
        <td>SSO</td>
        <td>CONAE, PlanetIQ, SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>24-10-2020</td>
        <td>15:31:34</td>
        <td>F9 B5 B1060.3</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 14 v1.0, GPS III-04  </td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>05-11-2020</td>
        <td>23:24:23</td>
        <td>F9 B5B1062.1</td>
        <td>CCAFS SLC-40</td>
        <td>GPS III-04 , Crew-1</td>
        <td>4311</td>
        <td>MEO</td>
        <td>USSF</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
    <tr>
        <td>25-11-2020</td>
        <td>02:13:00</td>
        <td>F9 B5 B1049.7</td>
        <td>CCAFS SLC-40</td>
        <td>Starlink 15 v1.0, SpaceX CRS-21</td>
        <td>15600</td>
        <td>LEO</td>
        <td>SpaceX</td>
        <td>Success</td>
        <td>Success</td>
    </tr>
</table>



### Task 3




##### Display the total payload mass carried by boosters launched by NASA (CRS)



```python
%sql SELECT SUM(PAYLOAD_MASS__KG_) FROM SPACEY
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>619967</td>
    </tr>
</table>



### Task 4




##### Display average payload mass carried by booster version F9 v1.1



```python
%sql SELECT AVG(PAYLOAD_MASS__KG_) FROM SPACEY WHERE BOOSTER_VERSION like 'F9 v1.1%'
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>1</th>
    </tr>
    <tr>
        <td>2534</td>
    </tr>
</table>



### Task 5

##### List the date when the first successful landing outcome in ground pad was acheived.


_Hint:Use min function_ 



```python
%sql Select Min(Date) from spacey
```

### Task 6

##### List the names of the boosters which have success in drone ship and have payload mass greater than 4000 but less than 6000



```sql
%%sql 
SELECT BOOSTER_VERSION FROM SPACEY 
WHERE MISSION_OUTCOME='Success (drone ship)' 
and PAYLOAD_MASS__KG_ BETWEEN 4000 and 6000
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>booster_version</th>
    </tr>
</table>



### Task 7




##### List the total number of successful and failure mission outcomes



```python
%sql select mission_outcome, count(mission_outcome) as SUM from spacey group by mission_outcome
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>mission_outcome</th>
        <th>SUM</th>
    </tr>
    <tr>
        <td>Failure (in flight)</td>
        <td>1</td>
    </tr>
    <tr>
        <td>Success</td>
        <td>99</td>
    </tr>
    <tr>
        <td>Success (payload status unclear)</td>
        <td>1</td>
    </tr>
</table>



### Task 8



##### List the   names of the booster_versions which have carried the maximum payload mass. Use a subquery



```python
%sql select booster_version from spacey where payload_mass__kg_ = (select max(payload_mass__kg_) from spacey)
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>booster_version</th>
    </tr>
    <tr>
        <td>F9 B5 B1048.4</td>
    </tr>
    <tr>
        <td>F9 B5 B1049.4</td>
    </tr>
    <tr>
        <td>F9 B5 B1051.3</td>
    </tr>
    <tr>
        <td>F9 B5 B1056.4</td>
    </tr>
    <tr>
        <td>F9 B5 B1048.5</td>
    </tr>
    <tr>
        <td>F9 B5 B1051.4</td>
    </tr>
    <tr>
        <td>F9 B5 B1049.5</td>
    </tr>
    <tr>
        <td>F9 B5 B1060.2</td>
    </tr>
    <tr>
        <td>F9 B5 B1058.3</td>
    </tr>
    <tr>
        <td>F9 B5 B1051.6</td>
    </tr>
    <tr>
        <td>F9 B5 B1060.3</td>
    </tr>
    <tr>
        <td>F9 B5 B1049.7</td>
    </tr>
</table>



### Task 9


##### List the failed landing_outcomes in drone ship, their booster versions, and launch site names for in year 2015



```python
%sql select booster_version, landing__outcome, launch_site from spacey where landing__outcome ='Failure (drone ship)'
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>booster_version</th>
        <th>landing__outcome</th>
        <th>launch_site</th>
    </tr>
    <tr>
        <td>F9 v1.1 B1012</td>
        <td>Failure (drone ship)</td>
        <td>CCAFS LC-40</td>
    </tr>
    <tr>
        <td>F9 v1.1 B1015</td>
        <td>Failure (drone ship)</td>
        <td>CCAFS LC-40</td>
    </tr>
    <tr>
        <td>F9 v1.1 B1017</td>
        <td>Failure (drone ship)</td>
        <td>VAFB SLC-4E</td>
    </tr>
    <tr>
        <td>F9 FT B1020</td>
        <td>Failure (drone ship)</td>
        <td>CCAFS LC-40</td>
    </tr>
    <tr>
        <td>F9 FT B1024</td>
        <td>Failure (drone ship)</td>
        <td>CCAFS LC-40</td>
    </tr>
</table>



### Task 10

##### Rank the count of landing outcomes (such as Failure (drone ship) or Success (ground pad)) between the date 2010-06-04 and 2017-03-20, in descending order



```python
%sql select landing__outcome, count(landing__outcome) as LO from spacey group by landing__outcome order by LO desc 
```

     * ibm_db_sa://mdr04626:***@9938aec0-8105-433e-8bf9-0fbb7e483086.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:32459/bludb
    Done.





<table>
    <tr>
        <th>landing__outcome</th>
        <th>lo</th>
    </tr>
    <tr>
        <td>Success</td>
        <td>38</td>
    </tr>
    <tr>
        <td>No attempt</td>
        <td>22</td>
    </tr>
    <tr>
        <td>Success (drone ship)</td>
        <td>14</td>
    </tr>
    <tr>
        <td>Success (ground pad)</td>
        <td>9</td>
    </tr>
    <tr>
        <td>Controlled (ocean)</td>
        <td>5</td>
    </tr>
    <tr>
        <td>Failure (drone ship)</td>
        <td>5</td>
    </tr>
    <tr>
        <td>Failure</td>
        <td>3</td>
    </tr>
    <tr>
        <td>Failure (parachute)</td>
        <td>2</td>
    </tr>
    <tr>
        <td>Uncontrolled (ocean)</td>
        <td>2</td>
    </tr>
    <tr>
        <td>Precluded (drone ship)</td>
        <td>1</td>
    </tr>
</table>



### Reference Links

* <a href ="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20String%20Patterns%20-%20Sorting%20-%20Grouping/instructional-labs.md.html?origin=www.coursera.org">Hands-on Lab : String Patterns, Sorting and Grouping</a>  

*  <a  href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20Built-in%20functions%20/Hands-on_Lab__Built-in_Functions.md.html?origin=www.coursera.org">Hands-on Lab: Built-in functions</a>

*  <a  href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20Sub-queries%20and%20Nested%20SELECTs%20/instructional-labs.md.html?origin=www.coursera.org">Hands-on Lab : Sub-queries and Nested SELECT Statements</a>

*   <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Module%205/DB0201EN-Week3-1-3-SQLmagic.ipynb">Hands-on Tutorial: Accessing Databases with SQL magic</a>

*  <a href= "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Module%205/DB0201EN-Week3-1-4-Analyzing.ipynb">Hands-on Lab: Analyzing a real World Data Set</a>




## Author(s)

<h4> Lakshmi Holla </h4>


## Other Contributors

<h4> Rav Ahuja </h4>


## Change log
| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2021-10-12 | 0.4 |Lakshmi Holla | Changed markdown|
| 2021-08-24 | 0.3 |Lakshmi Holla | Added library update|
| 2021-07-09 | 0.2 |Lakshmi Holla | Changes made in magic sql|
| 2021-05-20 | 0.1 |Lakshmi Holla | Created Initial Version |


## <h3 align="center"> © IBM Corporation 2021. All rights reserved. <h3/>

