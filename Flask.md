# Flask 

## Flask app

initialize flask app

```python
from flask import Flask, render_template
app = Flask(__name__)

#in terminal write this 
export FLASK_APP=main.py
export FLAK_DEBUG=1 #for debug 
```



##Routing

```python
@app.route('/')
def home():
  return '<h1>hello world</h1>'
```

## Dynamic Routes

```python
@app.route('/user/<user<')
def user_page():
  return '<p>hello</p>'.format(name)
```

## Routing Arguments

```python
@app.route('/user/<name>', methods=['GET', 'POST'] )
def user(name):
  pass
```



## Rendering templates

create a folder called templates containing all html files

```python
from flask import Flask, render_template
app = Flask(__name__)


@app.route('/')
def index():
    return render_template('index.html')
    
@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)
```

## Error handling

```python
@app.errorhandler(404)
def page_not_found(e):
	return render_template('404.html'), 404

@app.errorhandler(500)
def internal_server_error(e):
	return render_template('500.html'), 500
```

PS: render template can take a second argument which is the response code usually 200 for success and 404 for errors 



## Dynmic links url_for()

```python
url_for('user', name='john',
_external=True) would return http://localhost:5000/user/john
```

## Static files

create a directory called static containing css files and all static files such as images etc..

```python
{% block head %}
{{ super() }}
<link rel="shortcut icon" href="{{ url_for('static', filename='favicon.ico') }}"
type="image/x-icon">
<link rel="icon" href="{{ url_for('static', filename='favicon.ico') }}"
type="image/x-icon">
{% endblock %}
```

##super() 

used to preserve the original contents of the block defined in the base templates

## flask-moment

to manage local date and time 

```bash
pip install flask-moment
```

using the lib

```python
from flask_moment import Moment
moment = Moment(app)
```

import the moment library(in base.html template)

```pytho
{% block scripts %}
{{ super() }}
{{ moment.include_moment() }}
{% endblock %}
```

## Web forms

```bash
pip install flask-wtf
```

unlike other flask packages this does not need to be initialized , yet it needs a secret key (unique secret key ) as follow

```python
app.config['SECRET_KEY'] = 'hard to guess string
```

using web forms

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired
```



### Available forms input

- BooleanField
- DateField
- DateTimeField
- DecimalField
- FileField
- HiddenField
- MultipleFileField
- FieldList
- FloatField
- FormField
- IntegerField
- PasswordField
- RadioField
- SelectField
- SelectMultipleField
- SubmitField
- TextAreaField

### arguments

these form takes a label and an optional argument that is a validator

### Validators

- DataRequired
- Email
- EqualTo
- InputRequired
- IPAddress
- Length
- MacAddress
- NumberRange
- Optional
- Regexp
- URL
- UUID
- AnyOf
- NoneOf

### example

```python
@app.route('/user/<name>', methods=['GET', 'POST'] )
def user(name):
    name = None
    form = NameForm()
    if form.validate_on_submit():
        name = form.name.data
        form.name.data = ''
    return render_template('user.html', form=form, name=name)

  class NameForm(FlaskForm):
    name = StringField('What is your name?', validators=[DataRequired()])
    submit = SubmitField('Submit')
    
 
```

in the html file

```html
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}

{% block title %}Flasky{% endblock %}

{% block page_content %}
<div class="page-header">
<h1>Hello, {% if name %}{{ name }}{% else %}Stranger{% endif %}!</h1>
</div>
{{ wtf.quick_form(form) }}
{% endblock %}
```

### forms functions

- validate_on_submit() 
  - returns true when form is submitted

## User Session

first we need to import it and use the redirect as follow

```python
from flask import Flask, render_template, session, redirect, url_for

@app.route('/user', methods=['GET', 'POST'] )
def user():
    form = NameForm()
    if form.validate_on_submit():
        session['name'] = form.name.data
        return redirect(url_for('user'))
    return render_template('user.html', form=form, name=session.get('name'))

```

## Flashing messages with flash

import flash

```python
from flask import Flask, render_template, session, redirect, url_for, flash

@app.route('/user/test', methods=['GET', 'POST'])
def user_test():
    form = NameForm()
    if form.validate_on_submit():
        old_name = session.get('name')
        if old_name is not None and old_name != form.name.data:
            flash('Looks like you have changed your name!')
            session['name'] = form.name.data
            return redirect(url_for('user_test'))
    return render_template('user.html',form = form, name = session.get('name'))

class NameForm(FlaskForm):
    name = StringField('What is your name?', validators=[DataRequired()])
    submit = SubmitField('Submit')

```

this is not enough to display the message we need to add the get_flashed_messages() in the html file as follow

```html
{% block content %}
<div class="container">
{% for message in get_flashed_messages() %}
<div class="alert alert-warning">
<button type="button" class="close" data-dismiss="alert">&times;</button>
{{ message }}
</div>
{% endfor %}
{% block page_content %}
{% endblock %}
</div>
{% endblock %}
```



## app config

The app.config dictionary is a general-purpose place to store configuration variables

used by Flask, extensions, or the application itself. Configuration values can be added

to the app.config object using standard dictionary syntax

# Jinja

templating engine super powerful

## rendering variables (including lists dictionaries etc...)

```jinja2
{{ var_name }}
```

## If else

```jinja2
{% if user %}
	hello {{ user }}
{% else %}
	hello, guest
{% endif %}
```

## for loop

```jinja2
<ul>
{% for comment in comments %}
	<li>{{ comment }}</li>
{% endfor %}
</ul>
```



## Macros

```jinja2
{% macro render_comment(comment) %}
	<li>{{ comment }}</li>
{% endmacro %}

<ul>
{% for comment in comments %}
	{{ render_comment(comment) }}
{% endfor %}
</ul>

```

## Importing and reuse into jinja2

```jinja2
{% import 'macros.html' as macros %}

<ul>
{% for comment in comments %}
	{{ macros.render_comment(comment) }}
{% endfor %}
</ul>
```

## Inheritence and reuse

```jinja2
<html>
<head>

{% block head %}
	<title>
	{% block title %}{% endblock %}
	</title>
{% endblock %}
</head>

<body>
{% block body %}
{% endblock %}
</body>
</html>
```

in the other html jinja2 file inherit

```jinja2
{% extends "base.html" %}
	{% block title %}Index{% endblock %}
	
{% block head %}
{{ super() }}
<style>
</style>
{% endblock %}

{% block body %}
<h1>Hello, World!</h1>
{% endblock %}
```



# Flask-Bootstrap

## installation

```bas
pip install falsk-bootstrap
```

![](/Users/bounasrnour/Documents/Blog/Screen Shot 2021-08-08 at 10.05.02 PM.png)

custom css file

```jinja2
{% block styles %}
{{super()}}
<link rel="stylesheet"
      href="{{url_for('.static', filename='mystyle.css')}}">
{% endblock %}
```

custom javascript

```jinja2
{% block scripts %}
<script src="{{url_for('.static', filename='myscripts.js')}}"></script>
{{super()}}
{% endblock %}
```



# Database

## SQL Database

A relational database stores data in tables, each table consists of columns and rows, for example a table can have columns such as name, family_name, address. While the rows represent the actual data

Primary key is a special solumn that holds a unique identifier for each row stored in the table

Foreign key, reference the primary key of a row in the same or another table, these links are called relationship and is the foundation of databases



## NoSQL

Databases that do not follow the relatioal model of the SQL are refered to as NoSQL. It uses collections instead of tables and documents instead of records. Joining tables are difficult due to the structure of the data 

## Python Database Framework

## Flask Alchemy

```bash
pip install flask-sqlalchemy
```

in SQLAlchemy databases are specified as URLs

| MySQL              | mysql://username:pass@hostname/database      |
| ------------------ | -------------------------------------------- |
| Postgres           | postgresql://username:pass@hostname/database |
| SQLite(linux, mac) | sqlite:///absolute/path/to/database          |
| SQLite(win)        | sqlite:///c:/absolute/path/to/database       |



> Note: SQLite database do not have a server, so hotname, username and password are omitted and database is the filename on disk for the database

Initialize as follow

```python
import os
from flask_sqlalchemy import SQLAlchemyapp 
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] ='sqlite:///' + os.path.join(basedir, 'data.sqlite')
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)

```



## Models

```pyth
 class Role(db.Model):
	__tablename__ = 'roles'
	id = db.Column(db.Integer, primary_key=True)
	name = db.Column(db.String(64), unique=True)
	def __repr__(self):
		return '<Role %r>' % self.name
		
class User(db.Model):
	__tablename__ = 'users'
	id = db.Column(db.Integer, primary_key=True)
	username = db.Column(db.String(64), unique=True, 				index=True)
	def __repr__(self):
		return '<User %r>' % self.username

```



Types of columns

- Integer, 32bits
- SmallInteger 16bits short int
- BigInteger, long unlimited precision int
- Float 
- Numeric, fixed point number
- String
- Text, optimized for large or unbounded lenght
- Unicode
- UnicodeText, optimized for large unicode
- Boolean
- Date
- Time
- DateTime
- Interval, time interval
- Enum
- PickleType
- LargeBinary



### Other arguments

- primary_key,  True/False
- unique , no duplicate value for this column
- index 
- nullable, if true allow empty values
- default, define default value for the column

### __repr__()

```python
def __rep__():
  pass
```

For representing data for debug purposes 

## Relationship

```python
class Role(db.Model):
    users = db.relationship('User', backref='role')
class User(db.Model):
    role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))

```



### relationship options

- backref , add back reference in the other model in the relationship
- primaryjoin, specify join condition between 2 models explicitly
- lazy , how related items are loaded 
  - select, on demand the first time they are accessed
  - immediate, when the source object is loaded
  - joined, immediately but as a join
  - subquery, but as a subquery
  - noload, items are never loaded
  - dynamic , give a query instead of loading the item
- uselist , if false use a scalar
- order_by, ordering
- secondary, specify name of the association table to use in many to many relationship
- secondaryjoin, the secondary join condition for many to many 



## Creating table

python shell

```bash
flask shell
>>> from main import db
>>> db.create_all()
>>> db.drop_all() 
```

now a new file called data.sqlite is created, drop_all to delete all tables and data



## Inserting rows

```python
>>> from main import Role, User
>>> admin_role = Role(name='Admin')
>>> mod_role = Role(name='Moderator')
>>> user_role = Role(name='User')
>>> user_john = User(username='john', role=admin_role)
>>> user_susan = User(username='susan', role=user_role)
>>> user_david = User(username='david', role=user_role)
```



## Db Session

To add changes to the database we need to add them to the db session then commit 

```shell
>>> db.session.add(admin_role)
>>> db.session.add(mod_role)
>>> db.session.add(user_role)
>>> db.session.add(user_john)
>>> db.session.add(user_susan)
>>> db.session.add(user_david)
```

or

```shell
>>> db.session.add_all([admin_role, mod_role, user_role,
... user_john, user_susan, user_david])
```

commit changes to db

```shel
>>> db.session.commit()
```

## Deleting rows

```shell
>>> db.session.delete(mod_role)
>>> db.session.commit()
```

## Querying Rows

```shell
>>> Role.query.all()
```

Filtering by

```shell
>>> User.query.filter_by(role=user_role).all()
```

Get first

```shell
>>> user_role = Role.query.filter_by(name='User').first()
```

### Query filters

- filter(), 
- filter_by()
- limit() , limit number of results
- offset(), offset to the result
- order_by()
- group_by()

### Query executors

- all(), return all results
- first()
- first_or_404(),  abort and send 404 it no result
- get(), return row that matches primary key, none if no match
- get_or_404()
- count(), count the result of query
- paginate(), return a Pagination obj









https://www.youtube.com/watch?v=RBSGKlAvoiM&t=16s



https://www.youtube.com/watch?v=nTeuhbP7wdE



















