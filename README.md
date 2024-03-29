# i18n engine for Django Framework
[![pypi version](https://badge.fury.io/py/django-i18n.svg)](https://pypi.org/project/django-i18n/)

## Installation

Use the package manager [pip](https://pypi.org/) to install django-i18n

```bash
pip3 install django-i18n
```

## Setup
Before using library, you need setup some things in your django project, please follow this steps
1. Setup all required variables in your settings.py
  ```python
  LOCALE = 'es' # Mandatory
  LOCALE_FALLBACK = 'en' # Optional, default =  'en'
  LOCALES = ['es'] # Mandatory
  LOCALES_PATH = os.path.join(BASE_DIR, 'locales') # Optional, default path './locales' folder

  INSTALLED_APPS = [
    ...
    'django_i18n',
    ...
  ]
  ```

2. After that, you need create a locales folder (Setted in LOCALES_PATH variable in your settings.py), inside your folder you need some yml files with **EXACT** names as you setted in LOCALES variable, next you can see an example
  ```yaml
  en:
    my:
      title: "An incredible title"
      content: "Hello %{name}"
  ```
## Usage in python files

```python
from django_i18n.tools import translate, set_locale, handle_orm_errors

translate("my.title")
# OR
translate('my.content', name='World')

# Set locale
set_locale(locale="en", fallback="es") # Fallback is optional, default value is 'en'

# Handle ORM errors
form = MyForm(data)
handle_orm_errors(list_errors=form.errors, as_json=False)
# List errors is a Django forms errors
#as_json return dict as json string
```

## Usage in template
```jinja2
{% load t from django_i18n %}

<html>
  <head>
    <title>{% t 'my.title' %}</title>
  </head>
  <body>
    <h1>{% t 'my.content' name='World' %}</h1>
  </body>
</head>
 ```
## Fallback response
If you have setted a fallback, each translation may be return
```python
translate('my.locale')
#> Fallback: An incredible title
```

If that key doesn't exists in your locale and your fallback, this is the response
```python
translate('my.locale2')
#> Translation missin my.locale2
```

## To Do
1. Forms complete support handler
2. Default messages for Django forms
3. Other supported formats

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)