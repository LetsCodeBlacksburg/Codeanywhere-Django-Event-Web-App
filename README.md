# Codeanywhere-Django-Event-Web-App
 Pro Series - Web Framework Django/python workshop Let's Code Blacksburg! Tuesday, December 13, 2016 from 5:30 PM to 8:00 PM (EST) Blacksburg, VA

	1. Slide:
		○ Overall Goal of this session:
			§ Demonstrate the value Django can bring inside your organization
				□ By showing how fast and easy it is to spin up a DB driven website
				□ By showing off the autogenerated admin console 
				□ Why Django might be better than a typical CMS (WordPress, Drupla, Joomla, etc)
					® Basically all CMS's will need a programmer to extend and customize and you are still left with a messy customization
					® Django start with a developer and get exactly what you need.
						◊ More quickly get to market window
						◊ Less of what you don't need
			§ Django major features:
				□ Amazing Documentation
				□ Python is easy language to learn and is clean (DRY, TDD, PEP08, etc)
				□ Virtualenv (via python)
				□ Auto generated Admin console
				□ ORM built in (and easy to use)
				□ TDD
	2. Slide:
		○ We only have 2 hours so we will be using Codeanywhere
			§ Allows us to skip python & django installation
		○ We will rely heavily on github repo sample pre-built before the class for code snippets
	3. Slide:
		○ Create codeanywhere.com account and login
		○ Create a new project (Named whatever you want) "LCBB Event Web App"
		○ Open/Create new container for newly created project
			§ Choose Django with Ubuntu 14.04
			§ Name it whatever you want "LCBB Event Web App Container"
		○ Click the "Run Project" (play) button
		○ Copy bottom link from Info tab and paste into new tab 
			§ Swap out "XX" in the url with port number "8000"
	4. Slide:
		○ Describe Codeanywhere.com Editor
			§ Where to start new SSH Terminal
			§ Where to open "Info" if accidentally closed
			§ Folder structure on left side
			§ On to the console
	5. Slide:
		○ SSH Terminal:
			§ %> source django/bin/activate
			§ %> cd projectname
			§ %> python manage.py startapp appname
			§ %> cd projectname
	6. Slide:
		○ Discuss manage.py
		○ Discuss difference in Projects and Apps in Django
		○ Initial project already created but if you needed to create it use this command:
			§  django-admin.py startproject projectname
		○ Create Events app
			§ %> python manage.py startapp events
		○ SEE branch: release-one-projectapp-creation
	7. Slide:
		○ Discuss MVC vs TMV
			§ Django is not true MVC, but it is equally as optimal
			§ If I had to compare the two:
				□ Template is view
				□ View is controller
				□ Model is model
				□ Urls.py maps the route
	8. Slide:
		○ Connect events app to project
			§ Add the below line to the "INSTALLED_APPS" section of the settings.py file
				□ 'events.apps.EventsConfig'
			§ Create events/urls.py:
				from django.conf.urls import url
				from . import views
				app_name = 'events'
				urlpatterns = [
				    url(r'^$', views.index, name='index'),
				    # url(r'^(?P<event_id>[0-9]+)/$', views.detail, name='detail'),
				]
			§ Connect projectname/urls.py to projectname/events/url.py
				from django.conf.urls import include, url
				url(r'^events/', include('events.urls')),
				
	9. Slide:
		○ Create basic "Hello World" in views.py
			def index(request):
			  return HttpResponse('Hello World')
		○ SEE branch: release-2-projectapp-view
	10. Slide:
		○ Create Models:
			§ Event(models.Model)
				□ Name
				□ Date_time
				□ Description
				□ Enabled
			§ Person
				□ Name
				□ Email
			§ Attendance
				□ Person
				□ Event
		○ See: https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/models.py
	11. Slide:
		○ Discuss ORM
			§ %> python manage.py makemigrations
			§ %> python manage.py migrate
			§ %> python manage.py migrate 0003 (targeted migration "roll back")
		○ Look at migrations folder
			§ Review 00001_initial.py file it created
		○ SEE branch: release-3-projectapp-models
	12. Slide: 
		○ Discuss shell
			§ %> python manage.py shell
			§ >>> from events.models import Event, Person, Attendance
			§ >>> Event.objects.all() 
			§ >>> e = Event(name='event one', description='this is the description')
			§ >>> e.save() 
			§ >>> e.date_time
			§ >>> e = Event(name='event two', description='this is the description for event two')
			§ >>> e.save()
			§ >>> Event.objects.filter(name__endswith='two')  
			§ Cntl Z      <- to quit
	13. Slide:
		○ Create Templates and connect to view:
			§ Discuss why duplication of app name in template folder
			§ events/templates/events/index.html
				□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/templates/events/index.html
			§ events/templates/base.html
				□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/templates/base.html
			§ Template inheritance via {% block name %} [% endblock %}
			§ Events/static/events/starter-template.css
				□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/static/events/starter-template.css
	14. Slide:
		○ Connect view.py to templates:
			§ Add linked code to view.py {Just the function "def index"
				□ https://github.com/atuggle/Codeanywhere-Django-Event-Web-App/blob/release-4-projectapp-templates/projectname/events/views.py
		○ SEE branch: release-4-projectapp-templates
	15. Slide:
		○ Discuss Forms:
		○ Create "RegisterForm(forms.Form)" 
			§ Create events/forms.py file
				□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/forms.py
	16. Slide:
		○ Create form and detail.html:
		○ Events/templates/events/details.html
			□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/templates/events/detail.html
		○ Uncomment line un urls.py so details route will work
		○ Update views.py to look like this:
			□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/views.py
		○ Use the form to create one or more attendance records in db
		○ SEE branch: release-5-projectapp-forms
	17. Slide:
		○ What about the autogenerated admin you talked about?
		○ First we must create a super user in the db:
			□ %> python manage.py createsuperuser
				□ Follow prompts
			□ Navigate to your app /admin:
				□ http://port-8000.lcbb-event-web-app-container-allentuggle503110.codeanyapp.com/admin
				□ Notice there is already "Groups" & "Users"
		○ Register models in admin.py that you want to show In the admin:
			□ Edit events/admin.py:
				□ https://github.com/atuggle/Events-Project-Codeanywhere/blob/master/projectname/events/admin.py
			□ Refresh admin 
			□ Discuss Admin consoles
		○ SEE branch: release-6-projectapp-templates
	18. Slide:
		○ Q & A
		○ What next:
		○ Resources:
			□ https://www.djangoproject.com/
				□ View both the tutorial & overview
Book: "Two Scoops of django" by Daniel Greenfeld and Audrey Roy
