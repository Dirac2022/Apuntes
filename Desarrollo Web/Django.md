
Aditional resources:

- [Django official website](https://www.djangoproject.com/start/overview/ "Django official website")
- [Django documentation](https://docs.djangoproject.com/en/4.1/ "Django documentation page")


# Introduction to Django

## Project Structure

A Django project is a Python package containing the database configuration used by various sub-modules (Django calls them apps) and other Django-specific settings

Use the startproject command of `django-admin` as follows

```sh
(djenv) C:\djenv>django-admin startproject demoproject
```

The startproject is Django’s default project template. It creates the following file structure in the Python environment:

```text
│   manage.py 
│ 
└───demoproject 
        asgi.py 
        settings.py 
        urls.py 
        wsgi.py 
        __init__.py 
```


The manage.py script inside the outer demoproject has the same role as the django-admin utility. 

You can use it to perform various administrative tasks. In that sense, it is a local copy of the django-admin utility

### `manage.py`

The `manage.py` script can perform everything that the `django-admin` utility does but is more straightforward, especially if your are required to work on a single project.

> [!tip] If you have multiple projects, use `django-admin` and specify the settings.

The general usage of `manage.py` is as follows:

```sh
python manage.py <command>
```


<h5>startapp</h5>

As mentioned above, a Django project folder can contain one or more apps. An app is also represented by a folder of a specific file system. The command to create an app is:

```django
python manage.py startapp <name_of_app>
```


<h5>makemigrations</h5>

Django manages the database operations with the ORM technique. Migration refers to generating a database table whose structure matches the data model declared in the app.

```django
python manage.py makemigrations
```

<h5>migrate</h5>

This command option of manage.py synchronizes the database state with the currently declared models and migrations.

```django
python manage.py migrate
```


<h5>runserver</h5>

This command starts Django’s built-in development server on the local machine with IP address 127.0.0.1 and port 8000

```django
python manage.py runserver
```



<h5>shell</h5>

This command opens up an interactive Python shell inside the project. This is useful when you are required to perform some quick interactive operations.

```django
python manage.py shell
```

> [!note] Django prefers **IPython** if it is installed over the standard Python shell



### Project package


The `startproject` command option of the Django-admin utility creates the folder of the given name, inside which there is another folder of the same name.

```django
django-admin startproject demoproject
```


In addition, the `startproject` template places four more files in the package folder.

<h5>settings.py</h5>

Django configures specific parameters with their default values and puts them in this file.

The django-admin utility and `manage.py` script use these settings while performing various administrative tasks.


<h5>urls.py</h5>

This script contains a list of object **urlpatterns**. Every time the client browser requests a URL, the Django server looks to match its pattern and routes the application to the mapped view.

The default structure of urls.py contains a view mapped to the project’s Admin site.


```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
	path('admin/', admin.site.urls).
]
```

<h5>asgi.py</h5>

This file is used by the application servers following the ASGI standard to serve asynchronous web applications.


<h5>wsgi.py</h5>

Many web application servers implement the WSGI standard. This script is the entry point for such WSGI-compatible servers to serve your classical web application.


#### `settings.py`

This file defines the attributes that influence the function of a Django application. The startproject template assigns some default values to these attributes. They may be modified as per requirement during the use of the application.

<h6>INSTALLED_APPS</h6>
Each string represents the path of an app inside the parent project folder. The `startproject` template installs some apps by default.

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

This list must be updated by adding its name whenever a new app is installed.

```django
python manage.py startapp demoapp
```

We must update the list:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'demoapp'
]
```


<h6>Databases</h6>
Specifies the configuration of one or more databases to be used by the current Django application. By default, Django uses the SQLite database. Hence, this setting has a pre-defined configuration for it.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

The default name of the SQLite database is `db.sqlite3`, which is created in the parent project folder.

In place of SQLite, you may choose to use any other. For example, for MySQL, the database settings could be as follows:

```python
DATABASES = {   
    'default': {   
        'ENGINE': 'django.db.backends.mysql',   
        'NAME': 'djangotest',   
        'USER': 'root',   
        'PASSWORD': 'password',   
        'HOST': '127.0.0.1',   
        'PORT': '3306',            
    }   
} 
```


<h6>DEBUG = True</h6>

By default, the development server runs in debug mode. This helps develop the application as the server picks up changes in the code and the output can be refreshed without restarting. However, it must be disabled in the production environment.


<h6>ROOT_URLCONF</h6>
This setting is a string pointing toward the urls.py module in which the project’s URL patterns are found. In this case, it would be

```python
ROOT_URLCONF = 'demoproject.urls'
```


<h6>STATIC URL</h6>
This setting points to the folder where the static files, such as JavaScript code, CSS files and images, are placed. Usually, it is set to 'static/' corresponding to the folder of this name in the parent project folder.

```python
STATIC_URL = 'static/'
```


### Test the installation

After creating the project, to verify that it is built correctly, start the development server with the following command while remaining in the project’s parent folder:

```django
python manage.py runserver
```

If you get this output, the project has been created successful


## App structures

A Django project is a web application that may consist of one or more sub-modules called apps

<h5>What is a Django app</h5>
An app is responsible for performing one single task out of the many involved in the complete web application, represented by the Django project.

For example, a trading organization website may have one app for managing customer data, another for suppliers, and another for stock management. However, the important feature of the Django app is that it is reusable.

When a Django project is created with the `startproject` command, it creates a container folder. Django puts a `manage.py` script and the project package folder in the outer folder.

The `startapp` command option of the `manage.py` script creates a default folder structure for the app of that name.

Here's how to create a `demoapp` in the `demoproject` folder

```django
python manage.py startapp demoapp
```

A folder with the app's name is created inside the parent folder. It has a few Python scripts.

```text
demoproject/
│   db.sqlite3
│   manage.py
│
├───demoapp
│   │   admin.py
│   │   apps.py
│   │   models.py
│   │   tests.py
│   │   views.py
│   │   __init__.py
│   │
│   ├───__pycache__
│   └───migrations
│           __init__.py
│
└───demoproject
    │   asgi.py
    │   settings.py
    │   urls.py
    │   wsgi.py
    │   __init__.py
    │
    └───__pycache__
```


### `views.py`

In Django, a view is a user-defined function that’s called when Django’s URL dispatcher identifies the client’s request URL and matches it with a URL pattern defined in the urls.py file.

The auto-created views file is empty at the beginning.

Let's add a view function called index() in it by saving the following snippet.

```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
    return HttpResponse('Hello, world. This is the index view of Demoapp')
```


<h5>urls.py</h5>
The project package has a file of this name that defines the URL patterns for the project. 

On similar lines, you need to provide the URL routing mechanism for the app. 

>[!tip] Important
>The `urls.py` file can be configured at both the project and app level. In the example below, the urls.py will be configured at both the project and app-level. 

The app folder doesn’t have a file of this name when created. Hence, you have to create one.

Save the following snippet as urls.py in the **demoapp** folder.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index')
]
```

Next, you need to update the urlpatterns list in the project folder’s urls.py and include the app’s URL configurations.

The updated `demoproject/urls.py` should look like this:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('demo/', include('demoapp.urls')),
    path('admin/', admin.site.urls),
]
```


<h5>Update settings.py </h5>

Lastly, you need to update the list of `INSTALLED_APPS` in the project’s setting file. This list already contains some pre-installed apps. Add the name of `demoapp` so that it looks like this:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'demoapp'
]
```

### `models.py`

The data models required for processing in this app are created in this file. It is empty by default. A data model is a Python class based on `django.db.modelsclass`. All the models present here are migrated to the database tables


