# Dough.js Template Project

This is a simple template project for creating new [Dough.js](https://github.com/rharter/dough.js) web applications.

# The Project Structure

Until generation scripts are created, you are required to make your project structure by hand.

    - Root
      + app
		    + controllers
		    + views
		  + config
		  + lib
		    + resources
		    + vendor
		  + public

## app/controllers

Your web application controllers live in the `app/controllers` directory.  Controllers are Javascript files that generally contain all of the request handler functions pertaining to a given section of your app.

## app/views

The standard templating language for Dough.js is [Mustache](http://mustache.github.com/).  Mustache template files live in subdirectories inside the `app/views` directory.  The names of the subdirectories are arbitrary, but should correlate to the controller names for organizational purposes.  For instance, all templates related to a `user.js` controller should live in `app/views/users/`.

## config

The `config` directory is not currently heavily used, but will be in the near future.  Currently, your `routes.js` file lives here.

## lib/resources

The `lib/resources` directory is where you'll put all of your custom Javascript helper files, along with any jar files that you want included in your project. Custom helper files should live directly in this folder, and any custom plugins (usually Javascript and jar files) will go in subdirectories named for the plugin.

## lib/vendor

This is where third party plugins reside.  Third party distributable plugins have a specific structure like so:

    - plugin_name
      + jars
      + resources

The root directory is named after the plugin is contains for ease of identification.  The `jars` directory contains any required jar files, and the `resources` directory is for the Javascript files that the plugin will access.

## public

All static resources live in the `public` directory.  These will be served based on the request URL using the `public` directory as the root.  If a static resource exists, it will override any routes that might have matched.

# Routes

Routes define which controller function handles each request.  The `public` directory will be searched first and, if no static resource is found, the router will be queried to handle the request.

Routes can be filtered by URI and HTTP method.  You can define a basic route like so:

    dough.router.register('/users', controllers.users.index, 'GET');

This tells the router that any `GET` request to `http://hostname:8080/users` should be handled by the `controllers.users.index` function.

The first parameter is the URI that should be matched. You can define request parameters in the URI for a truly RESTful service.

    dough.router.register('/users/:id', controllers.users.index, 'GET');

These parameters will be resolved at request time and passed to your handler function in the `request.params` hash.

You can also pass an array for the third parameter to make a route resolve multiple HTTP methods.  For instance:

    dough.router.register('/users', controllers.users.index, ['GET', 'POST']);
