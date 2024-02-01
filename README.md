# SSubdomain

SSubdomain is a Django package for managing subdomains.

## Features

- Subdomain routing
- User role-based access control
- Flexible configuration

## Usage

### Install from PyPI

```bash
pip install ssubdomain
```

```bash
python manage.py migrate
```

### Add to INSTALLED_APPS

```python
# settings.py

INSTALLED_APPS = [
    ...
    'SSubdomains'
]
```

### Add to MIDDLEWARE

```python
# settings.py

MIDDLEWARE = [
    ...
    'SSubdomains.middleware.SubdaomainsManagerMiddleware'
]
```

### Define subdomains

```python
# settings.py

SSUBDOMAINS_CONFIG = {

    'SUBDOMAIN_URLCONFS': {
        'www': 'project.urls.www',
        'blog': 'project.urls.blog'
    },

    'ROLE_FIELD': 'role',

    'ALLOWED_SUBDOMAINS_BY_ROLE': {
        'editor': ['blog']
    },

    'DISABLED_SUBDOMAINS_BY_ROLE': {
        'guest': ['blog']
    },
    'USE_MODEL': True,  # if you want to use model for subdomains, set this to True
    'MODEL': 'SSubdomains.Subdomain',
    # if you want to use custom  model for subdomains you must extend SubdomainBase model

}
```

### Set up urlconfs

#### `project/urls/www.py`



```python
from django.urls import path

# www url patterns 
urlpatterns = [
    ...
]
```

#### `project/urls/blog.py`

```python
from django.urls import path

# blog url patterns
urlpatterns = [
    ...
]
```

### Access via subdomains

```http
http://www.example.com 
http://blog.example.com
```

## Summary

SSubdomain provides a clean way to manage multiple subdomains in a Django project. User role-based access control makes
it easy to restrict parts of a site.
