# AppEngine Launching An App

The last technical part of the prework will be to launch an App Engine app so that you can get familiar with the GAE interface and file structure.

##Objectives
* Launch a simple App Engine app
* Add a handler to the app

## Google App Engine Launcher

Managing projects on App Engine is infinitely easier with the GAE Launcher. Click [here](https://cloud.google.com/appengine/downloads#Google_App_Engine_SDK_for_Python) to find the instructions for how to download and install it.

## Creating an app on GoogleAppEngineLauncher
+ Open up GoogleAppEngineLauncher

+ Create a new application by going to the File menu and picking "New Application..."

+ Name your application “appengine-practice”

+ Click the browse button to save the application into the Desktop directory.  

+ Enter 8080 in the port field if it's not already there (Not admin port!)

+ Click Create.

+ Click the green Run button.

+ Open a new Google Chrome browser and put the url: `http://localhost:8080/`

You should see: Hello, world!

CONGRATS you just made MVP app in Google AppEngine.



##What Did AppEngine do for you?

App Engine created two files in the location specified in the 'path' column of the Launcher, in this case, this should be your Desktop. Those two files were a configuration file, app.yaml and the file that instructed the app to display "Hello world!"

### The Configuration - App.yaml
The configuration file, `app.yaml` is used to specify url paths, either to scripts or files. At the top, it also lists information about the application code. This file also is a place to list any libraries that are used in the app.

```yaml
application: appengine-practice #unique application name
version: 1 # version 1 of this application’s code
runtime: python27 # running on python 2.7
api_version: 1 # API version 1
threadsafe: true # how AppEngine processes multiple requests simultaneously

handlers:
- url: /favicon\.ico
  static_files: favicon.ico
  upload: favicon\.ico

- url: .*
  script: main.app

libraries:
- name: webapp2
  version: "2.5.2"
```
### The Controller - Main.py
The main.py file is a file that contains Python code surrounded by a framework called webapp2. This framework helps link the pages the user sees to the logic we want to perform on the backend.

```python
import webapp2 #imports webapp2

class MainHandler(webapp2.RequestHandler):
    def get(self):
        self.response.write('Hello world!')

app = webapp2.WSGIApplication([
    ('/', MainHandler)
], debug=True)
```

In main.py, notice that the webapp2 library is  **imported**. This allows us to route our handlers. Each handler is a class with one method that runs to handle the request and generate a response. The default request to handle is GET.

The last bit of code in main.py is the **route**, which maps the URLs to their handlers.

##Creating a Handler
If you need to create a new handler, there are typically two things to do:

+ Create a new handler class with a unique name
+ Add a new route mapping a URL to that handler.

To demonstrate that these handlers are just Python, we've also added code to the handler that counts to 100 with a for loop. You've seen this code in the previous session when we introduced Google App Engine.

Here's the full code added to the main.py file:

```python
import webapp2

class MainHandler(webapp2.RequestHandler):
    def get(self):
        self.response.write('Hello world!')

class CountHandler(webapp2.RequestHandler):
    def get(self):
        for i in range(1, 101):
            self.response.write(i)

app = webapp2.WSGIApplication([
    ('/', MainHandler),
    ('/count', CountHandler),
], debug=True)
```
You can test this in your browser at `http://localhost:8080/count`. (If your application is running on a different port number, make sure you use the correct one.)
Once again, your screen says: Hello, world!

It also counts to 100 when we change the url to `/count`. Our new handler at work!

## Conclusion
You can continue to add new handlers or play around with the two current ones, MainHandler and CountHandler. This will give you a good foundation as we build our own apps during CSSI training.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/cssi-6.1-gae-launch-app' title='AppEngine Launching An App'>AppEngine Launching An App</a> on Learn.co and start learning to code for free.</p>
