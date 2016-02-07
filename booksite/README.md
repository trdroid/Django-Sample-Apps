### Creating the project

> droid@droidserver:~/onGit/Django$ source /home/droid/scratchpad/Django/vir_env/bin/activate

    (vir_env) droid@droidserver:~/onGit/Django$ 

> (vir_env) droid@droidserver:~/onGit/Django$ django-admin startproject booksite

> (vir_env) droid@droidserver:~/onGit/Django$ ls

    booksite  documentsite  _misc

### Project structure

<img src="_misc/project%20structure.png"/>

### Create tables in the database

Run the <i>migrate</i> command

> (vir_env) droid@droidserver:~/onGit/Django$ cd booksite

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py migrate

    Operations to perform:
      Apply all migrations: contenttypes, admin, sessions, auth
    Running migrations:
      Rendering model states... DONE
      Applying contenttypes.0001_initial... OK
      Applying auth.0001_initial... OK
      Applying admin.0001_initial... OK
      Applying admin.0002_logentry_remove_auto_add... OK
      Applying contenttypes.0002_remove_content_type_name... OK
      Applying auth.0002_alter_permission_name_max_length... OK
      Applying auth.0003_alter_user_email_max_length... OK
      Applying auth.0004_alter_user_username_opts... OK
      Applying auth.0005_alter_user_last_login_null... OK
      Applying auth.0006_require_contenttypes_0002... OK
      Applying auth.0007_alter_validators_add_error_messages... OK
      Applying sessions.0001_initial... OK

The <i>migrate</i> command looks at the "INSTALLED_APPS" setting in <i>booksite/booksite/settings.py</i> as shown below and creates tables according to the database settings in <i>booksite/booksite/settings.py</i> and the database migrations of the app. 

It looks at the models in each app and creates tables for the ones that do not already exist in the database.

INSTALLED_APPS settings in <i>booksite/booksite/settings.py</i>

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',    
]
```

<img src="_misc/after%20migrate%20command.png"/>

### Looking at the contents of the database

https://www.sqlite.org/cli.html

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ sqlite3

	SQLite version 3.8.2 2013-12-06 14:53:30
	Enter ".help" for instructions
	Enter SQL statements terminated with a ";"
	sqlite> .open db.sqlite3
	sqlite> .schema
	CREATE TABLE "django_migrations" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "app" varchar(255) NOT NULL, "name" varchar(255) NOT NULL, "applied" datetime NOT NULL);
	CREATE TABLE "auth_group" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "name" varchar(80) NOT NULL UNIQUE);
	CREATE TABLE "auth_group_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "group_id" integer NOT NULL REFERENCES "auth_group" ("id"), "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id"));
	CREATE TABLE "auth_user_groups" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id"), "group_id" integer NOT NULL REFERENCES "auth_group" ("id"));
	CREATE TABLE "auth_user_user_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id"), "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id"));
	CREATE UNIQUE INDEX "auth_group_permissions_group_id_0cd325b0_uniq" ON "auth_group_permissions" ("group_id", "permission_id");
	CREATE INDEX "auth_group_permissions_0e939a4f" ON "auth_group_permissions" ("group_id");
	CREATE INDEX "auth_group_permissions_8373b171" ON "auth_group_permissions" ("permission_id");
	CREATE UNIQUE INDEX "auth_user_groups_user_id_94350c0c_uniq" ON "auth_user_groups" ("user_id", "group_id");
	CREATE INDEX "auth_user_groups_e8701ad4" ON "auth_user_groups" ("user_id");
	CREATE INDEX "auth_user_groups_0e939a4f" ON "auth_user_groups" ("group_id");
	CREATE UNIQUE INDEX "auth_user_user_permissions_user_id_14a6b632_uniq" ON "auth_user_user_permissions" ("user_id", "permission_id");
	CREATE INDEX "auth_user_user_permissions_e8701ad4" ON "auth_user_user_permissions" ("user_id");
	CREATE INDEX "auth_user_user_permissions_8373b171" ON "auth_user_user_permissions" ("permission_id");
	CREATE TABLE "django_admin_log" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "object_id" text NULL, "object_repr" varchar(200) NOT NULL, "action_flag" smallint unsigned NOT NULL, "change_message" text NOT NULL, "content_type_id" integer NULL REFERENCES "django_content_type" ("id"), "user_id" integer NOT NULL REFERENCES "auth_user" ("id"), "action_time" datetime NOT NULL);
	CREATE INDEX "django_admin_log_417f1b1c" ON "django_admin_log" ("content_type_id");
	CREATE INDEX "django_admin_log_e8701ad4" ON "django_admin_log" ("user_id");
	CREATE TABLE "django_content_type" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "app_label" varchar(100) NOT NULL, "model" varchar(100) NOT NULL);
	CREATE UNIQUE INDEX "django_content_type_app_label_76bd3d3b_uniq" ON "django_content_type" ("app_label", "model");
	CREATE TABLE "auth_permission" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "content_type_id" integer NOT NULL REFERENCES "django_content_type" ("id"), "codename" varchar(100) NOT NULL, "name" varchar(255) NOT NULL);
	CREATE UNIQUE INDEX "auth_permission_content_type_id_01ab375a_uniq" ON "auth_permission" ("content_type_id", "codename");
	CREATE INDEX "auth_permission_417f1b1c" ON "auth_permission" ("content_type_id");
	CREATE TABLE "auth_user" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "password" varchar(128) NOT NULL, "last_login" datetime NULL, "is_superuser" bool NOT NULL, "first_name" varchar(30) NOT NULL, "last_name" varchar(30) NOT NULL, "email" varchar(254) NOT NULL, "is_staff" bool NOT NULL, "is_active" bool NOT NULL, "date_joined" datetime NOT NULL, "username" varchar(30) NOT NULL UNIQUE);
	CREATE TABLE "django_session" ("session_key" varchar(40) NOT NULL PRIMARY KEY, "session_data" text NOT NULL, "expire_date" datetime NOT NULL);
	CREATE INDEX "django_session_de54fa62" ON "django_session" ("expire_date");
	sqlite> 


	sqlite> .tables
	auth_group                  auth_user_user_permissions
	auth_group_permissions      django_admin_log          
	auth_permission             django_content_type       
	auth_user                   django_migrations         
	auth_user_groups            django_session   
	
	sqlite> .exit	

### Creating an app

Create an app called "books"

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py startapp books

### App structure

The following snapshot shows the structure and contents of the generated app directory

<img src="_misc/app%20structure.png"/>

### Designing Models

Create "Author" and "Book" models in <i>booksite/books/models.py</i>

```python
from django.db import models

# Create your models here.
class Author(models.Model):
	name = models.CharField(max_length=50)

	def __str__(self):
		return self.name

class Book(models.Model):
	title = models.CharField(max_length=100)
	content = models.TextField()
	published_on = models.DateField()

	author = models.ForeignKey(Author, on_delete=models.CASCADE)

	def __str__(self):
		return self.title
```

### Activating Models

<b> Install app </b>

Let the project know that the "books" app is installed by including the string 'books.apps.BooksConfig' in the INSTALLED_APPS setting in <i>booksite/booksite/settings.py</i>. With this, Django knows to include the "books" app in the project.

```python
INSTALLED_APPS = [
    'books.apps.BooksConfig', #<----- refers to the 'books' app
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',    
]
```

Instead of specifying the name of the app "books" directly in INSTALLED_APPS, specify it using 'books.apps.BooksConfig' which specifies the name of the app as follows:

<i>booksite/books/apps.py</i>

```python
from django.apps import AppConfig


class BooksConfig(AppConfig):
    name = 'books'  # <----------
```

<b>Make Migrations</b>

Specify Django about changes to the models (in this case, the addition of new models, "Author" and "Book") by running <i>makemigrations</i>. 

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py makemigrations books

	Migrations for 'books':
	  0001_initial.py:
	    - Create model Author
	    - Create model Book

Django saves the changes to the models, and therefore to the database schema under \<project\>/\<app\>/migrations directory. In this case, the migrations are saved in:

<img src="_misc/after%20running%20makemigrations.png"/>

<i>booksite/books/migrations/0001_initial.py</i>

```python
# -*- coding: utf-8 -*-
# Generated by Django 1.9.2 on 2016-02-07 03:59
from __future__ import unicode_literals

from django.db import migrations, models
import django.db.models.deletion


class Migration(migrations.Migration):

    initial = True

    dependencies = [
    ]

    operations = [
        migrations.CreateModel(
            name='Author',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('name', models.CharField(max_length=50)),
            ],
        ),
        migrations.CreateModel(
            name='Book',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('title', models.CharField(max_length=100)),
                ('content', models.TextField()),
                ('published_on', models.DateField()),
                ('author', models.ForeignKey(on_delete=django.db.models.deletion.CASCADE, to='books.Author')),
            ],
        ),
    ]
```

<b> Check SQL that would be executed when the migration is run </b>

First, check to see what SQL the migration would run:

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py sqlmigrate books 0001

	BEGIN;
	--
	-- Create model Author
	--
	CREATE TABLE "books_author" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "name" varchar(50) NOT NULL);
	--
	-- Create model Book
	--
	CREATE TABLE "books_book" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(100) NOT NULL, "content" text NOT NULL, "published_on" date NOT NULL, "author_id" integer NOT NULL REFERENCES "books_author" ("id"));
	CREATE INDEX "books_book_4f331e2f" ON "books_book" ("author_id");
	
	COMMIT;


<b> Run Migration </b>

Running a migration reflects the changes done to the models in the database schema i.e. it has the affect of synchronizing the changes done to the models (which in this case is the addition of two models, "Author" and "Book") with the database schema (which in this case is by creating two tables).

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py migrate

	Operations to perform:
	  Apply all migrations: sessions, books, auth, admin, contenttypes
	Running migrations:
	  Rendering model states... DONE
	  Applying books.0001_initial... OK


Django keeps track of the migrations it applies using a special table in the database called "django_migrations". The "migrate" command runs all the unapplied migrations against the database, synchronizing changes made to the models with the database schema.

<b> Check the database for new tables </b>

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ sqlite3

	SQLite version 3.8.2 2013-12-06 14:53:30
	Enter ".help" for instructions
	Enter SQL statements terminated with a ";"
	sqlite> .open db.sqlite3
	sqlite> .tables
	auth_group                  books_author              
	auth_group_permissions      books_book                
	auth_permission             django_admin_log          
	auth_user                   django_content_type       
	auth_user_groups            django_migrations         
	auth_user_user_permissions  django_session   

Notice the tables: books_author & books_book

### Interacting with Models

<b> Launch Interactive Python Shell </b>

> $ (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py shell

	Python 3.4.3 (default, Oct 14 2015, 20:28:29) 
	[GCC 4.8.4] on linux
	Type "help", "copyright", "credits" or "license" for more information.
	(InteractiveConsole)
	>>> from books.models import Author, Book
	>>>

This command sets the DJANGO_SETTINGS_MODULE environment variable, which makes the Python import path to "booksite/settings.py" available to Django.

Alternatively, to start by using a plain Python shell

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ export DJANGO_SETTINGS_MODULE=booksite.settings

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python3

	Python 3.4.3 (default, Oct 14 2015, 20:28:29) 
	[GCC 4.8.4] on linux
	Type "help", "copyright", "credits" or "license" for more information.
	>>> import django
	>>> django.setup()
	>>> from books.models import Author, Book
	>>> 

<b>Interacting with Models</i>

