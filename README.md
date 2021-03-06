# flask-project-setup

Flask project setup: TDD, Docker, Postgres and more

- [Part 1](https://www.thedigitalcatonline.com/blog/2020/07/05/flask-project-setup-tdd-docker-postgres-and-more-part-1/)
- [Part 2](https://www.thedigitalcatonline.com/blog/2020/07/06/flask-project-setup-tdd-docker-postgres-and-more-part-2/)
- [Part 3](https://www.thedigitalcatonline.com/blog/2020/07/07/flask-project-setup-tdd-docker-postgres-and-more-part-3/)

## Further Resources

- [Dissecting a Web stack](https://www.thedigitalcatonline.com/blog/2020/02/16/dissecting-a-web-stack/)
- [Click](https://click.palletsprojects.com/en/8.0.x/) - A Python package for creating command line interfaces
- [Python subprocess module](https://docs.python.org/3/library/subprocess.html)
- [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) - A Flask extension to work with SQLAlchemy
- [SQLAlchemy and PostgreSQL](https://docs.sqlalchemy.org/en/13/dialects/postgresql.html) - The Python SQL Toolkit and ORM
- [Flask-Migrate](https://flask-migrate.readthedocs.io/en/latest/) - A Flask extension to handle database migrations with Alembic
- [Useful pytest command line options](https://www.thedigitalcatonline.com/blog/2018/07/05/useful-pytest-command-line-options/)
- [pytest-flask](https://pytest-flask.readthedocs.io/en/latest/) - A plugin for pytest that simplifies testing Flask applications
- [Flask-SQLAlchemy API](https://flask-sqlalchemy.palletsprojects.com/en/2.x/api/)
- [Gunicorn](https://gunicorn.org/) - A Python WSGI HTTP Server

## Flask Configuration

See [./application/config.py](./application/config.py)

Some notes on the variables and the parameters involved in the configuration.

- `FLASK_ENV` and `FLASK_DEBUG` have to be initialised outside the application as the code might misbehave if they are changed once the engine has been started.
- `FLASK_ENV` can have only the two values _development_ and _production_ and the main difference is in performances.
- If `FLASK_ENV` is _development_ then `FLASK_DEBUG` becomes automatically _True_.

Guidelines

- It's pointless to set `DEBUG` and `ENV` in the application configuration, they have to be environment variables.
- Generally you don't need to set `FLASK_DEBUG`, just set `FLASK_ENV` to _development_.
- Testing doesn't need the debug server turned on, so you can set `FLASK_ENV` to _production_ during that phase. It needs `TESTING` set to _True_, though, and that has to be done inside the application.

### Notes

- [Flask configuration documentation](https://flask.palletsprojects.com/en/2.0.x/config/)
- [Flask application factories](https://flask.palletsprojects.com/en/2.0.x/patterns/appfactories/)

## Manage

```
## development
FLASK_CONFIG=development FLASK_ENV=development flask run --host 0.0.0.0
# or
# chmod +x manage.py
./manage.py flask run --host 0.0.0.0
./manage.py compose build web
./manage.py compose up -d
./manage.py compose exec web bash
./manage.py compose down
./manage.py compose exec db psql -U postgres
./manage.py flask db init
./manage.py flask db migrate -m "Some message"
./manage.py flask db upgrade

## flask migrate
./manage.py compose up -d
# if first time
./manage.py create-initial-db
./manage.py flask db migrate -m "Initial user model"
./manage.py flask db upgrade

## check with psql
./manage.py compose exec db psql -U postgres
postgres=# \l
postgres=# \c application
# You are now connected to database "application" as user "postgres".
application=# \dt
application=# select * from alembic_version;
application=# \d users
```

## Pipenv

- [Advanced Usage of Pipenv](https://pipenv-fork.readthedocs.io/en/latest/advanced.html)

```
PIPENV_VENV_IN_PROJECT=true python3.7 -m pipenv install -d
```
