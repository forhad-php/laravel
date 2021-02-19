# Workflow --

#0. Start With Composer
- Download and install composer if dont have
- Visit https://laravel.com/docs/8.x#the-laravel-installer
- Run the command `composer global require laravel/installer` to install the Laravel installer
- Run the command `laravel new example-app` to create a Laravel app
- Run the command `cd example-app` to entering the app directory
- Run the command `php artisan serve` to start development server and visit the porvided link


#0. Create a page and show it
- Go to routes > web.php
- Duplicate the existing code and replace the welcome to your page name. Be sure with URL. For example I want to create a page named `hello` then url should be `/hello`
- Now go to resources > views > and duplicate the welcome page
- Now visit the link supose `http://127.0.0.1:8000/hello`


#0. Create and connect the database
- Donwload TablePlus from https://tableplus.com/ and Install it
- Open TablePlus > Create a new connection > MySQL > Create
