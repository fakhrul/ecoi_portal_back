# ECOI PORTAL API

## Install database in production

1. Install database

```
sudo apt-get install postgresql
```

2. To connect to PostgreSQL using the postgres role, you switch over to the postgres account on your server by typing:

```
sudo -i -u postgres
psql
postgres=#

to quit
postgres=# \q
postgres@ubuntu-dev:~$ exit
```

## Flask Installation

- Install [Python](https://www.python.org/downloads/), [Pipenv](https://docs.pipenv.org/) and [Postgres](https://www.postgresql.org/) on your machine
- Clone the repository 
- Change into the directory
- Create the project virtual environment with `$ pipenv --three` command
- Activate the project virtual environment with `$ pipenv shell` command
- Install all required dependencies with `$ pipenv install`
- Rename .env.sample to .env and edit variables

  ```
  FLASK_ENV=development
  FLASK_PORT=5005
  DATABASE_URL=postgres://user:pass@localhost:5432/bd
  JWT_SECRET_KEY=pass_salt_phrase
  PAYPAL_ID=
  PAYPAL_SECRET=
  MAIL_SERVER=mail.server.com
  MAIL_PORT=465
  MAIL_USERNAME=user
  MAIL_PASSWORD=pass
  ```

  - To know where to get your paypal id & secret got to https://conectika.tech/blog/conectika-tech-1/post/como-obtener-el-id-de-cliente-y-la-clave-secreta-de-paypal-15

- Create database blog
  ```
  $ sudo su - postgres -c "createuser -s ecoi_portal" 2> /dev/null || true
  $ psql
  # ALTER USER ecoi_portal WITH ENCRYPTED PASSWORD 'qwe123';
  # CREATE DATABASE blog WITH TEMPLATE template0;
  # ALTER DATABASE blog OWNER TO ecoi_portal;
  ```
- Due to a bad flask relation please Comment line 5 from UserModel before Migrate
  ```
  1 # src/models/UserModel.py
  2 from marshmallow import fields, Schema
  3 import datetime
  4 from . import db
  5 #from ..app import bcrypt #after  python manage.py db upgrade uncomment to execute python run.py
  ```
- `$ python manage.py db init`
- `$ python manage.py db migrate`
- `$ python manage.py db upgrade`
- it should look like this

  ```
  1 # src/models/UserModel.py
  2 from marshmallow import fields, Schema
  3 import datetime
  4 from . import db
  5 from ..app import bcrypt #after  python manage.py db upgrade uncomment to execute python run.py
  ```

- Start the app with `python run.py`
- File BACKBLOGGIE.postman_collection.json its a Postman collection just import for test your backend
- standalone_html_paypal_test_button.html its a html file to test the paypal button with the backend and update items_paid column in user using the button

## Where should I host My web app?

The ideal VPS for open community web apps in M??xico https://conectika.tech/standar-vps
