# Setting up the development environment for Django applications

installing the virtual environment
```bash
pip install virtualenv
```

Creating the virtual environment

```bash
python -m venv venv
```
activating environment

```bash
venv\scripts\activate
```
stop the environment

```bash
deactivate
```

upgrade pip

```bash
python -m pip install --upgrade pip
```

install django and core tools

```bash
pip install django python-decouple
```

python-dotenv load environment variables from .env

creating a requirement

```bash
pip freeze > requirements.txt
```

to install the existing project with requirement 

```bash
pip install -r requirement.txt
```

start the django project 

```bash
django-admin startproject config . # . this dot avoind nested folder
```

create .gitignore in the root and list secret folders and file to avoid them from exposed in github repo

create .env in the root for secret

```python
DEBUG=True
SECRET_KEY=my-secret-key-here

DATABASE_NAME=my=database-name

OPENAI_API_KEY=api_key_here
WHATSAPP_API_KEY=meta_api

```

On the top of the settings.py make the basic import

```python

import os
from pathlib import path
from decouple import config

# then after replace the default with the following 

SECRET_KEY = config("SECRET_KEY")

DEBUG = config("DEBUG") == "TRUE"

# THEN NOW DATABASE

DATABASE = {
    'default' : {
        'ENGINE' :
'django.db.backends.sqlite3',
        'NAME' : BASE_DIR / 
os.getenv("DATABASE_NAME"),
    }
}

```

split the settings (base / dev / prod)

from settings.py you spit what chages for testing and for production


What goes in base.py
If this changes per environment, it does NOT belong here.

```python
INSTALLED_APPS
MIDDLEWARE
TEMPLATES
AUTH_PASSWORD_VALIDATORS
LANGUAGE_CODE
TIME_ZONE
STATIC_URL
```


What goes in dev.py
Development is for you.

```python
from .base import *

DEBUG = True

ALLOWED_HOSTS = []

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

#Also:

# console email backend

# verbose logging

# debug tools

```

what goes in prod.py
Production is for real users.

```python
from .base import *

DEBUG = False

ALLOWED_HOSTS = ['yourdomain.com']

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config("DB_NAME"),
        'USER': confidg("DB_USER"),
        'PASSWORD': config("DB_PASSWORD"),
        'HOST': config("DB_HOST"),
        'PORT': config("DB_PORT"),
    }
}

# Also:

# security settings

# HTTPS

# caching

# real email backend
```


set django setting module

``` powershell
setx DJANGO_SETTINGS_MODULE config.settings.dev
```

run migrations 
```bash
python manage.py makemigration
python manage.py migrate
```


start the project apps

```bash
python manage.py startapp appname
```

introduce the app in settings.py

# configuring the settings.py file

First install the psycopg2 package, a postgreSQL adapter for python
```bash
pip install psycopg2
```

1. configure the DATABASE

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_database_name',
        'USER': 'your_database_user',
        'PASSWORD': 'your_database_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

#With the .env file
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config("DB_NAME"),
        'USER': config("DB_USER"),
        'PASSWORD': config("DB_PASSWORD"),
        'HOST': config("DB_HOST"),
        'PORT': config("DB_PORT"),
    }
}
```

2. Managing static files

```python
STATIC_URL = '/static/'
MEDIA_URL = '/media/'
```

setting up the location where those files are stored is required
```python
MEDIA_ROOT = BASE_DIR / "media"
```
integrate email functionality for error logging
``` python
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBacked'
```

3. Specify the allowed host
```python
ALLOWED_HOST = ['*']
```



# Setting up the DRF if needed

```bash
pip install djangorestframework
pip freeze > requirements.txt
```

register DRF

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

# Setting up postgressql 

logging to postgres and creating database
```bash
psql -u postgres

CREATE DATABASE myproject_db;
CREATE USER myproject_user WITH PASSWORD 'strongpassword123';
ALTER ROLE myproject_user SET client_encoding TO 'utf8';
ALTER ROLE myproject_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE myproject_user SET timezone TO 'Africa/Johannesburg';

GRANT ALL PRIVILEGES ON DATABASE myproject_db TO myproject_user;
```

confirm user exist
```bash
\du
```
exit
```bash
\q
```

logging in using the user 
```bash
psql -U myproject_user -d myproject_db
```