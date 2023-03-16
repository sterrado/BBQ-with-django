<h1>Welcome to the Nacho excercise!</h1>

<h4>Read the instructions very carefully!</h4>

<strong>Consigna:</strong>

You'll prepare an api for a frontendless app to organize asados. In case you want, we'll leave the front end part for a version 2. The main entities to be related are Asado(event), Person(many), Meat(many). There are some bonus tracks. We'll use Django Rest Framework for this.

<strong>Additional things</strong>

<ul>
    <li>Use github to track code versioning. Make commits as you develop, maybe a commit per task or more</li>
    <li>You can use different branches also per task and then do a pull request to the main branch, but this is optional</li>
    <li>You can ask Santiago anything if you get stuck, don't waste too much time when stuck, but google things first.</li>
    <li>We can, and I'd say we should, make code reviews every now and then</li>
    <li>You have to be familiar with how REST protocol works: GET, POST, PUT, PATCH and DELETE methods</li>
    <li>Django and Django rest framework documentation will be your main ally for this</li>
</ul>

<em>Task 1</em>
Download git and python. Clone this repo into a directory in your computer.
Make a virtual environment to install python dependencies (libraries, frameworks, etc). <q>python3 -m venv venv</q>
Activate the environment. <q> source venv/bin/activate</q> <-- for mac.
In vs code select the view tab on the top menu, go to command palette, and type Python: Select Interpreter. Select the python interpreter from your virtual environment you just created.

Note: If you don't activate your environment, or don't select your interpreter correctly you'll install different things in different places and the code may not run correctly.

Pip install django, django admin

Run python django-admin startproject $myprojectname

cd into $myprojectname

run python manage.py startapp $appname --> Start with 'asado'

pip install django-rest-framework

go to $myprojectname>.settings.py , register the app and rest_framework in INSTALLED_APPS. Like, append the string 'asado' and 'rest_framework' to that list

cd .. to root folder and run <q> pip freeze > requirements.txt</q> --> This is the dependencies list for new devs incoming to the project, they'll just run pip install -r requirements.txt and have everything they need installed.

make a .gitignore file in the root folder, add venv there so you don't upload your virtual environment to github. The folder name should be in gray color.

Ok, you have the main structure. You have your django project with its folder with settings, and its linked to your first app 'asado'. You also have rest framework installed correctly.
Time to do a commit... <q> git add . </q> and <q> git commit -m 'added project setup and asado app'</q>. From now on, go ahead with your commits on your own.

<em>Task 2</em>

Make your first endpoint just to test. Go in your app views.py file (where logic lies) and make a function that receives a request and returns 'Hello world'. Make sure to use api_view decorator and to return a Response Object from rest_framework.response.
After you make this function, you need to configure routing. So make an urls.py file in your app, and link the urls.py file from your project urls.py file to this new file in your app.
Run <q>python manage.py runserver</q> from your django project directory and access this endpoint from the browser (http://localhost:8000/$path/)

<em>Task 3</em>

Make a model for asado. After creating the model, run <q>python manage.py makemigrations</q> , your migration files are created. Then run <q> python manage.py migrate</q> to actually migrate. You now created a table for storing and retrieving data for asado model. You also migrated some more django built in tables.

Make a file called serializers.py and make a Model Serializer from rest framework using Asado model as model.

In views.py make two endpoints, one to register an asado, and one to retrieve all asados. One is post request, the other get, this you define in @api_view decorator.
You'll have to read about django ORM. Some examples:

Asado.objects.create()
Asado.objects.all()
Asado.objects.first()
Asado.objects.filter() --> list
Asado.objects.get() --> one object

Notes: If you return a model without serializing, you won't be able to see its data. Serializer turns an object of type <object> to json data.
Also, if you don't return a Response object from django rest framework, it won't work.

<em>Task 4</em>

Now do a viewset in views.py. Learn how to do a ModelViewSet from rest framework, learn how to configure it in the routing (you'll need a simple router or default router from rest framework).

Once you have your viewset, you'll be able to create, get all, get by id (/$path/$id/), delete, etc.

<em>Task 5</em>

Make a new app called person. Do a model, a serializer and a viewset. Make sure this model is related to asado with a many to many (make it null = True). Now you can have multiple people related with multiple asados. Make your migrations.

Try serializing a list of person in the asado's serializer. You can go to the asado serializer, import the person serializer, add a field called people = PersonSerializer(many=True, required=False) and in the Person model, add related_name= 'people' to the many to many field. This is how you link them in the serializer.

So now, when your retrieve an asado or all asados, you'll have the people that attend to them.


<em>Task 6</em>

Make the same task 5 but for meat. So now you can add entraña, lomo, etc to an asado. 

Note: If you're more interested in relations, check fields ForeignKey and OneToOneRelationship, this is to make a OneToOne and OneToMany relationships.



<h3>Bonus tracks</h3>
<ul>
    <li>Dockerize app, see how you can do it on youtube, and run docker-compose up instead of running python manage.py runserver</li>
    <li>Deploy the app on heroku, which is free so that anyone can access your awesome api. Check on google how to deploy a django project on heroku.</li>
</ul>

<h1>Lets goo!</h1>

<img src="https://media.makeameme.org/created/lets-do-this-8829e7bf89.jpg">