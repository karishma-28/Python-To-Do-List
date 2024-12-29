# Python-To-Do-List

It’s a very popular app which helps to manage the tasks. Most of us do have it on our phones. We will be able to develop our own to-do list project in Python by the end of this article.

About to do list

To do list helps a user to perform tasks without chaos. Sometimes, there are many things we need to do in a day due to which we forget some of those or do the least important work first. This is a real world problem that can be solved with the help of our project. Let’s start the to-do list python project.

To do list Project in Python

The user can enter the tasks he/she needs to perform and also the time at which the tasks need to be done. After completion of the task the user can click on the checkbox to mark it as complete or delete that task.

Project Prerequisites

Before starting the Python To Do List project, install django. You need to have good knowledge of django and python. You also need to have a sound knowledge of Html and CSS to design the frontend of the project.



Project File Structure

1. Install Django
2. Create an app and a project
3. Settings.py
4. Models.py file
5. Admin.py file
6. Urls.py file
7. Views.py file

1. Install Django :

Django is an open source framework which is used for rapid web development. This framework is written in python. Secure websites are developed with the help of Django. It is mandatory to install django in order to begin the project. To install, run the command given below on cmd or terminal window.

pip install django
2. Create an app and a project:

The next step is to create an app and a project. Create a project named ToDoList and an app home. To store all the html files, create templates folder. Create a template and static folder. Html files are stored in the template folder and all the images and css files are stored in the static folder. To create an app and a project run the command given below on cmd or your terminal window.

django -admin startproject ToDoList
python manage.py startapp home
3. Setting.py:

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'home.apps.HomeConfig'
]
Add home.apps.Homeconfig in the settings.py file. Registration of app is necessary.

4. Models.py file:

from datetime import timezone
from django.db import models
import datetime
# Create your models here.
class NewTask(models.Model):
    AddTask=models.CharField(max_length=30)
    time=models.TimeField(auto_now=False, auto_now_add=False)
Code Explanation:
Models.py will help a person in the database connectivity.
a. timezone:It helps to store datetime information in UTC in the database.
b. Datetime: It’s a module that comes with django and helps to access the classes related to date and time.
c. CharField: It stores small and large sized strings in the database.
d. TimeField:It stores time in the database.
To create models you need to run migrations. Write the following command
given below.

Python manage.py makemigrations
python manage.py migrate
5. Admin.py file:

from django.contrib import admin
from .models import NewTask
 
class NewTaskAdmin(admin.ModelAdmin):
    list_display=("AddTask","time")
admin.site.register(NewTask,NewTaskAdmin)
Admin.py will help to register the models in the database which can be
Seen by the user.
Code Explanation:
a. list_display:It is a list which will be displayed in the database with the column names given in the parentheses.
b. register:It will register the model in the database.
Creation of a superuser is necessary to access the database. After running
the command given below users will be asked to enter the username, email
and password. After entering these details superuser will be created successfully.

Python manage.py createsuperuser
6. Urls.py file:

from django.contrib import admin
from django.urls import path
from . import views
urlpatterns = [
    path('', views.saveinfo, name='saveinfo'),
    path('saveinfo/', views.saveinfo, name='saveinfo'),
    path('index/', views.index, name='index'),
    path('Delete/<int:id>',views.Delete,name='Delete'),
]
Code Explanation:
a. path(): It defines the path which can be accessed by the user. The paths other than these will give errors.
b. Views: All the views from views.py file are imported.

7. Views.py file:

from django.shortcuts import render,redirect
from .models import NewTask
def saveinfo(request):
    if request.method == "POST":
        AddTask=request.POST['addtask']
        time=request.POST['time']
        add=NewTask(AddTask=AddTask,time=time)
        add.save()
    Add = NewTask.objects.all()
    return render(request,"index.html",{'Add':Add})
def index(request):
    Add = NewTask.objects.all()
    return render(request,"index.html",{'Add':Add})
def Delete(request,id):
        New = NewTask.objects.get(id=id)
        New.delete()
        return redirect('/')
Code Explanation:
a. saveinfo:This function helps to save the information of the task and time in the database.
b. index: This function redirects a user to the home page.
c. Delete:This function will delete the row which a user wants to delete.
d. save(): Object changes are saved with the help of save().
e. delete(): It is used to delete the object.
