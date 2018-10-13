Responsive Labs Project Management System
=======

RLPMS is an application to provide a user story based backlog management
system for agile development teams. Based off of Fulcrum



![Fulcrum Screenshot](https://github.com/MikeRuby/fulcrumapp/blob/master/doc/screenshot.png)

Goals
-----

RLPMS is a clone of [Pivotal Tracker](http://pivotaltracker.com/).  It will
almost certainly never surpass the functionality, usability and sheer
awesomeness of Pivotal Tracker, but aims to provide a usable alternative.

Installation
------------

First up, your system will need the
[prerequisites for running Ruby on Rails installed](http://rubyonrails.org/download)

Install QT in Mountail Lion with Homebrew 
[View the QT install page](https://github.com/thoughtbot/capybara-webkit/wiki/Installing-Qt-and-compiling-capybara-webkit)

    $ brew update
    $ brew install qt

Once you have these:

    # Checkout the project
    $ git clone git@github.com:MikeRuby/fulcrumapp.git
    $ cd fulcrum

    # Install the project dependencies
    $ gem install bundler
    $ bundle install

    # Set up the development database
    $ bundle exec rake fulcrum:setup db:setup

    # Start the local web server
    $ rails server

You should then be able to navigate to `http://localhost:3000/` in a web browser.
You can log in with the test username `test@example.com`, password `testpass`.


Heroku setup
------------

To deploy it to Heroku, make sure you have a local copy of the project; refer
to the previous section for instructions. Then:

    $ gem install heroku

    # Create your app. Replace APPNAME with whatever you want to name it.
    $ heroku create APPNAME --stack cedar

    # Set APP_HOST heroku config so outbound emails have a proper host
    # Replace APPNAME below with the value from `heroku create`
    $ heroku config:set APP_HOST=APPNAME.herokuapp.com

    # Define where the user emails will be coming from
    # (This email address does not need to exist)
    $ heroku config:set MAILER_SENDER=noreply@example.org

    # Allow emails to be sent
    $ heroku addons:add sendgrid:starter

    # Deploy the first version
    $ git push heroku master

    # Set up the database
    $ heroku run rake db:setup

Once that's done, you will be able to view your site at
`http://APPNAME.herokuapp.com`.

Translating
-----------

Below is an example of how you might go about translating RLPMS to German.

* Find the name of your locale, in this case we are using `de`
* Copy the `config/locales/en.yml` file to `config/locales/de.yml`
* Edit the file and update all the translated strings in quotes on the right
  hand side.
* Add your new locale to `config.i18n.available_locales` in
  `config/application.rb`
* Run `rake i18n:js:export` to build the Javascript translations.
* Run `rake i18n:missing_keys` for finding any missing language keys.

Colophon
--------

RLPMS is built with the following Open Source technologies:

* [Ruby on Rails](http://rubyonrails.org/)
* [Backbone.js](http://documentcloud.github.com/backbone/)
* [jQuery](http://jquery.com/)
* [Tango Icon Library](http://tango.freedesktop.org/Tango_Icon_Library)
* [Jasmine](https://jasmine.github.io/)
* [Sinon](http://sinonjs.org/)
* [Fulcrum](http://wholemeal.co.nz/projects/fulcrum.html)
