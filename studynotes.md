# mysite

# if an app has not been installed in the past 2 years than choose something else to utilize your project. 

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

Views/urls are tied togather. 
MODELS/INSTALLEDAPPS are tied togather


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
2. use model_name.objects.all()-> or for the polls app-> Question.objects.all() to retrieve all of the question you have created. at this point it should be 0 QuerySet
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

If you’re interested, you can also run python manage.py check; this checks for any problems in your project without making migrations or touching the database.



from django.db import models
models.Model-> use this in the parameter argument to make  it a parameter. 
Here, each model is represented by a class that subclasses django.db.models.Model. Each model has a number of class variables, each of which represents a database field in the model.

MODELS/INSTALLEDAPPS are tied togather. down the line you will need to tell the admin that the question objects have an admin interface. 

change your models/ run python manage.py makemigrations/ run python manage.py migrate.

A QuerySet represents a collection of objects from your database. It can have zero, one or many filters. Filters narrow down the query results based on the given parameters. In SQL terms, a QuerySet equates to a SELECT statement, and a filter is a limiting clause such as WHERE or LIMIT.


part 3 

if I see a %s that is a placeholder for whatever value I put in after the % sign the next time I use it. 

%s string
%d is a decimal, number, or integer. 
%f will print loats
%g is a generic number 
% itself is just a variable. 
{$ url $} and name are connected 

detail() 

loader ()

context are used in {{ }} context is information stored in a dictionary.
{{}} once you bring this context through it will become static. 
nothing came through-> I must have mislabeld something. 
if python comes through it was a bracket problem. 

{% %} template tag -> takes in a request, operates functions on them, and than returns back to the place it was called. like a rotating door 
{# ignore this #}
{{ context we want to bring through }}
{ | filter } there are roughly 35 filters you can use. 
include()

app_name = has two features. it is a label for the programmers to see what urls they are looking at. AND
app_name is used by the url dispatcher/searcher and will use the app name as a reference for the search.
in the html template tag you can use the (app_name variable:name= value or path name) to reference the path you want in the tag. 
and 

request() -> the users submitted action to the web page which. 
Research what is contained in HTTP request. 

render()
-> has to have a request, it needs the address of an html file or template. context -> variables that you have saved in the project.
context can be an empty dictionary or it can be a dictionary filled with variables that you have made.  
The context is a dictionary mapping template variable names to Python objects.

Raising 404 error-> 
do not change urls in templates. change them in urls.py. have the name= value be the same in urls.py as the template name=

get_object_or_404()
tries to get the information requested and than if it fails it raises the 404. get is always looking for a one object. 

reverse() go to the url conf and fetch a url. its for redirects. you can send it context. look at django.urls utility functions. 
reverse grabs information from urls.py. it works like a formatted f string.


if I am looking for multiple things get_list_or_404(). 
input output 
what does this view do? -> .... 
listing something, doing something. 
1. project outline 
2. idea journal and build out application ideas->

django <-> python are connected so if I cannot find the answer in 
- django template system uses dot lookup syntax to access variable attributes. It does a search for a dictionary in the object, than by the attribute and than by a list-index lookup.

- {% for %}: This tag is used to iterate over a collection, such as a list or queryset. It allows you to loop through the elements and perform actions for each item.

- we know that the name= function is used by django so that it can find the correct url path to use. 
However, different apps and projects exists and name clashing can happen. app_name = -> is where we specify the application namespace.

- {% url %}: The {% url %} tag is used to generate URLs for named URL patterns in your Django application. It takes the name of the URL pattern and any necessary arguments or keyword arguments.

part 4 forms:
form.legal_name
under the write a minimal form 
according to the django tutorial you can use the for loop code. 
or you can use the mike shortcut and use div tags in div tags. 

reverse() see prior notes in part 3

Queryset is a group of objects. 
we can use for loops on a query set to go over the attributes (variables) of objects. and than 

class based views have a lot of functionality but they come with drawbacks. one object at a time, classed based views are great.
multiple objects-> harder for class based views to work with. 
people want customizable actions on their projects.

does it fit my use case? class based views vs class based views.

always try to write for your apps with expandablity. -> more abstract things. not as simple, everything is always expandable, 

choice_set.all-> 

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

