# i18n

### Resources

Read or watch:

- [Flask-Babel](https://intranet.alxswe.com/rltoken/fBpGjDt2BFuBFiz-jwublQ)
- [Flask i18n tutorial](https://intranet.alxswe.com/rltoken/RtGz7pI7TKnYqrMMG9rWMg)
- [pytz](https://intranet.alxswe.com/rltoken/7rrCz4pkpqAn4FfRZ2Vsvw)

### Learning Objectives

- Learn how to parametrize Flask templates to display different languages
- Learn how to infer the correct locale based on URL parameters, user settings or request headers
- Learn how to localize timestamps

task 0
First you will setup a basic Flask app in 0-app.py. Create a single / route and an index.html template that simply outputs “Welcome to Holberton” as page title (<title>) and “Hello world” as header (<h1>).

task 1: Basic Babel setup.  
Then instantiate the Babel object in your app. Store it in a module-level variable named babel.

In order to configure available languages in our app, you will create a Config class that has a LANGUAGES class attribute equal to ["en", "fr"].

Use Config to set Babel’s default locale ("en") and timezone ("UTC").

Use that class as config for your Flask app.

task 2: get locale from request.  
Create a get_locale function with the babel.localeselector decorator. Use request.accept_languages to determine the best match with our supported languages.

3. Parametrize templates
   Use the \_ or gettext function to parametrize your templates. Use the message IDs home_title and home_header.

Create a babel.cfg file containing

```
[python: **.py]
[jinja2: **/templates/**.html]
extensions=jinja2.ext.autoescape,jinja2.ext.with_
```

Then initialize your translations with

```
$ pybabel extract -F babel.cfg -o messages.pot .
```

and your two dictionaries with

```
$ pybabel init -i messages.pot -d translations -l en
$ pybabel init -i messages.pot -d translations -l fr
```

4. Force locale with URL parameter

In this task, you will implement a way to force a particular locale by passing the locale=fr parameter to your app’s URLs.

In your get_locale function, detect if the incoming request contains locale argument and ifs value is a supported locale, return it. If not or if the parameter is not present, resort to the previous default behavior.

Now you should be able to test different translations by visiting http://127.0.0.1:5000?locale=[fr|en].

Visiting http://127.0.0.1:5000/?locale=fr should display this level 1 heading:
Bonjour monde!
