### Installing the App

- [Install the Postgres RDBMS](https://www.postgresql.org/download/)

- Install Python 3.6

- Create a virtual environment, install the requirements, and activate the virtual environment:
```
$ python3.6 -m venv env
$ source env/bin/activate
$ pip install -r requirements.txt
$ source env/bin/activate
```

- Switch to the postgres user and enter the Postgres shell:
```
$ sudo su - postgres
$ psql
```

- Create development and test databases:
```
postgres=# create database bitcoin_acks;
postgres=# create database bitcoin_acks_test;
```

- Set password for the `postgres` user:
```
postgres=# \password
postgres=# \q
```

- [Create GitHub API token](https://github.com/settings/tokens/new) 
  The token must have the `public_repo` permission scope.

- Export the following variables to your environment.
```
GH_PGDATABASE=bitcoin_acks
TEST_GH_PGDATABASE=bitcoin_acks_test
PGUSER=postgres
PGPASSWORD=<your password>
PGHOST=127.0.0.1
PGPORT=5432
GITHUB_USER=<you-github-username>
GITHUB_API_TOKEN=<your-github-api-token>
```

- Create database tables:
```
$ python src/bitcoin_acks/database/createdb.py
```

- Populate the database
```
$ python src/bitcoin_acks/github_data/pull_requests_data.py
```

### Running the App

- Poll the Github API to keep the database up to date:
```
$ python src/bitcoin_acks/github_data/pull_request_events.py
```

- Run the web server:
```
$ python src/bitcoin_acks/webapp/run.py
```

### Upgrading

- Run migrations:
```
$ alembic --config src/bitcoin_acks/migrations/alembic.ini upgrade head
```


### Running the tests
```
$ python setup.py test
```
