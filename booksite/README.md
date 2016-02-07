### Creating the project

> droid@droidserver:~/onGit/Django$ source /home/droid/scratchpad/Django/vir_env/bin/activate

    (vir_env) droid@droidserver:~/onGit/Django$ 

> (vir_env) droid@droidserver:~/onGit/Django$ django-admin startproject booksite

> (vir_env) droid@droidserver:~/onGit/Django$ ls

    booksite  documentsite  _misc

### Project structure

<img src="_misc/project%20structure.png"/>

### Creating an app

Create an app called "books"

> (vir_env) droid@droidserver:~/onGit/Django/booksite$ python manage.py startapp books

### App structure

The following snapshot shows the structure and contents of the generated app directory

<img src="_misc/app%20structure.png"/>

### Create tables in the database

Run the <i>migrate</i> command

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

The <i>migrate</i> command reads the available models and creates tables for the ones that do not already exist in the database.

<img src="_misc/after%20migrate%20command.png"/>

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


### Interacting with Models

