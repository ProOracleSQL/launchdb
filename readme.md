SpaceDB v2.0.1
==============

SpaceDB is a data set that contains all orbital and suborbital launches, all satellites, and related information.  It's based on data from the JSR Launch Vehicle Database, 2017 Dec 28 Edition.

The goals of SpaceDB are to provide a data set that is:

1. **Simple** - The data can be easily loaded into an Oracle database.  And it can be easily understood.  There are 20 tables but almost all of the tables and columns are obvious and do not require a lot of domain knowledge.
2. **Small** - The entire data set can be downloaded in 3 megabyte zip file.  You can install this on almost any system without going over your disk quota.
3. **Interesting** - I assume that most people who use a database have at least some appreciation for space flight.
4. **Real** - The data is not an imaginary.  If you spend time querying this data you will also learn something about the real world.

This data set will be used in my upcoming book, Pro Oracle SQL Development.  I'm tired of every SQL example using `EMPLOYEES` or `PARTS`.


Examples
--------

Count the number of launches per category:

	select launch_category, count(*)
	from launch
	group by launch_category
	order by count(*) desc;


How to Install
--------------

**Oracle Instructions:**

1. Download and unzip oracle_create_space.sql.zip.
2. CD into the directory with that file.
3. Set the command line to work with a UTF8 file.  In Windows this should work:

		C:\space> set NLS_LANG=American_America.UTF8

	In Unix this should work:

		setenv NLS_LANG American_America.UTF8

4. Start SQL\*Plus as a user who can either create another schema or load tables and data into their own schema.
5. Either use your existing schema, or create a new one like this:

		SQL> create user space identified by "enterPasswordHere#1" quota unlimited on users;

6. Run these commands to install the tables and data.  It should only take a minute.

		SQL> alter session set current_schema = space;
		SQL> @oracle_create_space.sql

**Postgres Instructions:**

1. Download and unzip csv_files.zip.
2. Download postgres_create_space.sql.
3. Modify postgres_create_space.sql to reference the correct directory that contains the CSV files.
4. Start psql and run this command:

		postgres=# \i postgres_create_space.sql


**Other Database (Partial) Instructions:**

1. Download and unzip csv_files.zip.
2. Load each of the 20 CSV files.


Schema Description
------------------

Below is a simple text description of the tables, roughly ordered by their importance and their relationships.

	LAUNCH
		LAUNCH_PAYLOAD_ORG
		LAUNCH_AGENCY

	SATELLITE
		SATELLITE_ORG

	ORGANIZATION
		ORGANIZATION_ORG_TYPE

	PLATFORM

	SITE
		SITE_ORG

	LAUNCH_VEHICLE
		LAUNCH_VEHICLE_MANUFACTURER
		LAUNCH_VEHICLE_FAMILY

	STAGE
		STAGE_MANUFACTURER

	PROPELLANT

	ENGINE
		ENGINE_MANUFACTURER
		ENGINE_PROPELLANT

	LAUNCH_VEHICLE_STAGE


License
-------

This data set and the code to load it are licensed under the LGPLv3.
