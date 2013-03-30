tornado-rest-handler
====================

A simple Python Tornado handler that manage Rest requests automatically

* [Basic Example of Usage](#basic-example-of-usage)
* [Installation](#installation)

Basic Example of Usage
------------------------

# Routes

One handler for every Rest routes

* GET    /animals index      display a list of all animals
* GET    /animals/new        new return an HTML form for creating a new animal
* POST   /animals create     create a new animal
* GET    /animals/:id show   show an animal
* GET    /animals/:id/edit   return an HTML form for editing a photo
* PUT    /animals/:id        update an animal data
* DELETE /animals/:id        delete an animal

```python
    (r'/animals/?', AnimalHandler), # GET, POST
    (r'/animals/new/?', AnimalHandler), # GET
    (r'/animals/([0-9a-fA-F]{24,})/?', AnimalHandler), # GET, PUT, DELETE
    (r'/animals/([0-9a-fA-F]{24,})/edit/?', AnimalHandler), # GET
```


# Handler implementation

```python
from tornardo_rest_handler import CrudHandler

class AnimalHandler(CrudHandler):
    document = Animal
```

# Templates

You must create your own template. It must have the names list.html, show.html and edit.html.

* animal/list.html
* animal/show.html
* animal/edit.html

By default, the directory is the document name in lower case. You may change the directory though:

```python
class AnimalHandler(CrudHandler):
    document = Animal
    template_path = 'my_dir'
```

Customization
-------------

By default, the list page will show all documents of that type. You can change this behavior through the 'query' attribute:

```python
class AnimalHandler(CrudHandler):
    document = Animal
    query = Animal.objects.filter(...)
```


Installation
------------

```
pip install tornado-rest-handler
```

#### or

```
1. Download zip file
2. Extract it
3. Execute in the extracted directory: python setup.py install
```

#### Development version

```
pip install -e git+git@github.com:paulocheque/tornado-rest-handler.git#egg=tornado-rest-handler
```

#### requirements.txt

```
tornado-rest-handler==0.0.1
# or use the development version
git+git://github.com/paulocheque/tornado-rest-handler.git#egg=tornado-rest-handler
```

#### Upgrade:

```
pip install tornado-rest-handler --upgrade --no-deps
```

#### Requirements

* Python 2.6 or 2.7
* Tested with Tornado 2.4.1


TODO
-------------

* Handlers for another ORMs (other than MongoEngine).
* Pagination
* Send valiation errors to forms
* Use fields and exclude to facilitate auto-generate forms:

```python
class AnimalHandler(CrudHandler):
    document = Animal
    fields = []
    exclude = []
```