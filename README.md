# SaySo Backend: Flask

## Overview

A functioning hobby project to bring my Python and Flask skills up to date. The is the Microservice half of a single-page blogging platform.

This project has:

* **MicroService API** - Backed by SQLite. Functions:
  * **Login**
  * **Logout**
  * **Signup**
  * **User Profile CRUD**
  * **Post CRUD**
  * **Comments CRUD**

[Frontend is in this repo](https://github.com/iq9/say-so-frontend-vanilla).

## Technologies

* **Python 3.7 on Flask 1.1.2**
* **SQLite** - Easy to connect PostgreSQL on Production. Vagrantfile will spin up a Postgres VM.
* **SQL Alchemy** - ORM
* **Alembic** - Migrations
* **JWT Auth** - For authentication between front and back.
* **PipEnv** - Python dependency management fixed. It behave like Bundler and NPM. Deterministic builds!

## Setup: MacOS

### Auth

Set the Secret that the JWT authentication will use, eg:
add this line to `.zshrc`, `.bashrc` or `.bash_profile`.

```bash
    export APP_SECRET='secret-key'
```

### Python

Set PyEnv to a 3.7 variant.

```bash
pyenv global 3.7.2
```

### Flask

Set the ``FLASK_APP`` and ``FLASK_DEBUG`` env var:

```bash
    export FLASK_APP=autoapp.py
    export FLASK_DEBUG=1
```

### Dependencies

If you haven't already:

`brew install pipenv`

CD into this app's root directory and:

```bash
    pipenv --python 3.7.4 # Change to your python version. Sets up Virt Env.
    pipenv sync --dev     # Best to install only what's in pipfile.lock.
                          # Those are the versions that work.
    pipenv run db init
    pipenv run db migrate
    pipenv run db upgrade
```

Start the web server:

```bash
    pipenv run flask run --with-threads
```

The frontend makes REST calls to this and expects Port 5000.

* Service should now be requestable via CURL or HTTPie at: http://localhost:5000

## Screenshots

coming

## Deployment

On Prod, make sure `FLASK_DEBUG` env var is unset or is set to `0`,
so that `ProdConfig` is used. Also, set `DATABASE_URL` to your Postgres
URI for example `postgresql://localhost/example`.

## Shell

Interactive Shell. Good for debugging:

```bash
    pipenv run shell
```

You will have access to the Flask `app` object and Models.

## Tests

```bash
    pipenv run test
```

## Migrations

When a new migration needs to be applied:

```bash
    pipenv run db migrate
```

This will generate a new migration script. Then run:

```bash
    pipenv run db upgrade
```

To apply the migration.

Full migration commands: `pipenv run db --help`.
