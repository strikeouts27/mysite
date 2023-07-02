# mysite
Notes in my own words
learning python has a youtube channel that breaks down how to do this step by step.

Questions for my tutor:
Can you better explain this aspect of the include function? 

Include() function The idea behind include() is to make it easy to plug-and-play URLs. Since polls are in their own URLconf (polls/urls.py), they can be placed under “/polls/”, or under “/fun_polls/”, or under “/content/polls/”, or any other path root, and the app will still work.



tutorial part 1 

it seems that when I exit out of virtual enivornments I have to reinstall everything again otherwise I get the bash error.

to start a project run the following command:
django-admin startproject mysite 

mysite/asgi.py: An entry-point for ASGI-compatible web servers to serve your project. See How to deploy with ASGI for more details.
mysite/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project. See How to deploy with WSGI for more details.

writing views:
from django.http import Http

from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")

1. write the view
2. create a urls.py file. 
3. in the urls.py file include this code 

from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
4. map the view to the urls.py file in the urlpatterns
The include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.
The include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.

part 2 
Set up a datbase, keep track of the models, than migrate the database. 

Process establishing the database:
1. python manage.py migrate-> will apply the 18 unapplied migrations
2. create your models in python in models.py. use models.Model as a parameter so that you can import django's functionality for models. also run the django.db import models at the top so that it will recognize models.Model parameters. 

3. go to the installed_apps in settings.py
4. tell django installed_apps where to pull the information from. 
ou do this by typing out the following syntax: application_folder.python_module_name.model_name. 
by telling django about this app we can than run the migrations to create the database entries. 

Process: How to see what you have in objects in django. 

1. import the models. 
2. use model_name.objects.all()-> or for the polls app-> Question.objects.all() to retrieve all of the question you have created. at this point it should be 0 QuerySet[
3. we need to create questions and that requires two parameters. we know this because in models.py we have two python attributes or django field names. so to create this said question in the API shell we type out a variable name and set it equal to the model_name(attribute1=, attribute2 =)-> in the case of the polls app question_text="Whats new?", pub_date=timezone.now()-> this will put the exact moment in time it was created which satsifes that. By doing this we instantate the python object.
4. Use variable_name.save() to actually save the object. 
5. Use the variablename.id to get the id field for the first value. 
 #app_folder_name.module_name.model_in_file.
6. use question.objects.all() to see all of the objects created under that variable that has the object saved into it. you should see [model: model object (1)]-> Question: Question object(1)
7. if you want it to be more descriptive with the output than use __str__(self): inside of the model that you are accessing information from. return self.question_text.

1. go to models.py and import models from django.db. 
2. switch over to the terminal with make migration command with the name of the command.
3. run the migrate command.
4. after the changes you can use the api to see the changes with 

part 2 Databases 

I worked with mike during a programming session on my google drive to setup PostgresSQL. 
If you wish to use another database, install the appropriate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings:

One of the things that I ran into was object creation with primary keys. it seems to me that if I create an object using the shell terminal in django it establishes a primary key of 1. and if I have the wrong question for the wrong id, it is best to update those values, never delete. for I thought delte() would remove that entry in the database and than when I created values it would slide the other entries down by one when I delete a record. that is NOT the case. It kept incrementing by one and left the empty value as empty. there may be a way to update through this but I have not found it. 


ENGINE – Either 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'. Other backends are also available.
NAME – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file. The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory.

to create a table in django we use the python manage.py migrate command. 

The migrate command looks at the INSTALLED_APPS setting and creates any necessary database tables according to the database settings in your mysite/settings.py file and the database migrations shipped with the app (we’ll cover those later). 

models
Now we’ll define your models – essentially, your database layout, with additional metadata.

A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. Django follows the DRY Principle. The goal is to define your data model in one place and automatically derive things from it.

from django.db import models
models.Model-> use this in the parameter argument to make  it a parameter. 
Here, each model is represented by a class that subclasses django.db.models.Model. Each model has a number of class variables, each of which represents a database field in the model.

To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting. The PollsConfig class is in the polls/apps.py file, so its dotted path is 'polls.apps.PollsConfig'. Edit the mysite/settings.py file and add that dotted path to the INSTALLED_APPS setting. It’ll look like this:



part 3 

- django template system uses dot lookup syntax to access variable attributes. It does a search for a dictionary in the object, than by the attribute and than by a list-index lookup.

- {% for %}: This tag is used to iterate over a collection, such as a list or queryset. It allows you to loop through the elements and perform actions for each item.

- we know that the name= function is used by django so that it can find the correct url path to use. 
However, different apps and projects exists and name clashing can happen. app_name = -> is where we specify the application namespace.

- {% url %}: The {% url %} tag is used to generate URLs for named URL patterns in your Django application. It takes the name of the URL pattern and any necessary arguments or keyword arguments.

part 4 forms:

-

part 5 
part 6 
part 7
part 8 
part 9 
part 10


commands and vocabulary

- a 

- .all() will retrieve all of the objects. it is best used with other commands such as filter and order by. 
- b
- c
- .create() we can create objects or instances in the database by using this method. simply observe the model in models.py that is the object you want to create and than fill in the parameters as attribute.s 

-.count() count how many objects their are. 
- d
- delete() if you want to delete a variable that is holding the objects use the .delete method. probably want to ask a supervisor before deleting data. 

- e
- f
filter()-> we can filter what we search through objects using that command. this will grab multiple values unlike get()
- g
get()-> we can search through objects for one specific one based on unique criteria. 
- h
- i
- include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.
The idea behind include() is to make it easy to plug-and-play URLs. Since polls are in their own URLconf (polls/urls.py), they can be placed under “/polls/”, or under “/fun_polls/”, or under “/content/polls/”, or any other path root, and the app will still work.

- j
- k
- kwargs argument: 
Arbitrary keyword arguments can be passed in a dictionary to the target view. We aren’t going to use this feature of Django in the tutorial.

- l

- m
- max_length=200 -> up to 200 characters per field. 
- migrate apply changes to the database.
- models.Modael -> use this as a parameter to activate django's model functionality for a class. this command is derived from-> from django.db import models.
from django.db import models

- n
- o
objects command: python_module_name.objects.all() see we have an empty query set. 
- on_delete=models.CASCADE - this command tells python or django to delete everything to delete everything attached to the data. 
- p
- path() function is passed four arguments, two required: route and view, and two optional: kwargs, and name. At this point, it’s worth reviewing what these arguments are for.
- q
- r
reverse_name = name in urls and that is what is used to find what page to go. 
- route argument: 
route is a string that contains a URL pattern. When processing a request, Django starts at the first pattern in urlpatterns and makes its way down the list, comparing the requested URL against each pattern until it finds one that matches.
- s 

- save() 
- (shell command python manage.py shell) use this command to activate the api terminal in django.

- sqlmigrate see how ORM used SQL statements to create the table. It shows what will be run when we run the migrate command. It does not run the migration itself.
python manage.py shell command allows us to interact with the database. 
- t 
- u 
- v
- view argument: 
When Django finds a matching pattern, it calls the specified view function with an HttpRequest object as the first argument and any “captured” values from the route as keyword arguments. We’ll give an example of this in a bit.
- w 
- x 
- y 
- z 


QuerySet- a group of objects

