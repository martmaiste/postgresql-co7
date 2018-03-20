dockerfiles-centos-postgres
===========================

Dockerfile to build PostgreSQL on CentOS 7
Meant for porting or migrating PostgreSQL databases from CentOS 7 servers to Docker enviroment


Setup
-----

To build the image
```
git clone https://github.com/martmaiste/postgresql-co7
docker build --rm -t postgresql-co7 postgresql-co7
```

Launching PostgreSQL
--------------------

#### Quick Start (not recommended for production use)
```
docker run --name=postgresql -d -p 5432:5432 martmaiste/postgresql-co7
```

Creating a database at launch
-----------------------------

You can create a postgresql superuser at launch by specifying `DB_USER` and
`DB_PASS` variables. You may also create a database by using `DB_NAME`. 
```
docker run --name postgresql -d \
-p 5432:5432 \
-v /var/lib/pgsql:/var/lib/pgsql \
-e 'DB_USER=username' \
-e 'DB_PASS=ridiculously-complex_password1' \
-e 'DB_NAME=my_database' \
martmaiste/postgresql-co7
```

To connect to your database with your newly created user:
```
psql -U username -h $(docker inspect --format {{.NetworkSettings.IPAddress}} postgresql-co7)
```