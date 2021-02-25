# Workflow --

#0. Start With Composer
- Download and install composer if dont have
- Visit https://laravel.com/docs/8.x#the-laravel-installer
- Run the command `composer global require laravel/installer` to install the Laravel installer
- Run the command `laravel new example-app` to create a Laravel app
- Run the command `cd example-app` to entering the app directory
- Run the command `php artisan serve` to start development server and visit the porvided link


#1. Create and connect the database
- First we need https://chocolatey.org/install to install MySQL in Windows
- So click Start and search "powershell"
- Right-click Windows Powershell and choose "Run as Administrator"
- Run the command from https://chocolatey.org/install to install Chocolatey
- Now we need https://chocolatey.org/packages/mysql to install MySQL via Chocolatey
- So run the command `choco install mysql` on PowerShell
- During install the MySQL, type `all` to permiting install all script.
- Donwload TablePlus from https://tableplus.com/ and Install it to manage database
- Open TablePlus > Create a new connection > MySQL > Create
Name: Example
Host: localhost
User: root
- Click test > if connction is OK > Connect
- To create a new database, click on the database icon > Database Name > OK > Open
- To set database name in Laravel > .env > DB_DATABASE=databasename


#2. Create a page and show it
- Go to routes > web.php
- Duplicate the existing code and replace the welcome to your page name. Be sure with URL. For example I want to create a page named `hello` then url should be `/hello`
- Now go to resources > views > duplicate and rename the welcome page as `hello.blade.php`
- Now visit the link supose `http://127.0.0.1:8000/hello`
- Writ the command `php artisan make:model Hello -mc --resource` in Cmder to create Model, Controller and Resource of Hello page. The following files will be found here →
    1. Database > Migrations > 2021_02_19_112725_create_hellos_table.php
    2. App > Models > Hello.php
    3. App > HTTP > Controllers > HelloController.php


#3. Creating Tables and Showing
- First we need to create a table and input some data. So go to database > migrations > 2021_02_19_112725_create_hellos_table.php
- Write below code →
```php
Schema::create('hellos', function (Blueprint $table) {
    $table->increments('id');
    $table->string('full_name');
    $table->integer('age');
    $table->string('email')->unique();
    $table->string('father_name');
    $table->string('mother_name');
    $table->string('present_address');
    $table->string('permanent_address');
    $table->string('school_name');
    $table->string('phone_number')->unique();
    $table->date('date_of_birth');
    $table->string('profile_picture');
    $table->timestamps();
});
```
> Note: To see available column types `https://laravel.com/docs/8.x/migrations#available-column-types`
- Run the command `php artisan migrate` 
> Note: I've faced with an error because of older version of PHP. So be sure with PHP latest version or compatible with MySQL version.
- Tables will create in TablePlus automatically.
> Note: If there is a problem in table or need change someting, we can try with this command `php artisan migrate:fresh` to delete all tables and migration again.
- Now input some data in the Hello table with TablePlus
- Write this code `Route::get('/hello', 'App\Http\Controllers\HelloController@index');` into routs > web.php . To redirect the Hello page to Controller. Because we do not access the databse without controller.
- Write the below code in `app > Http > Controllers` and create a view named `projects`
```PHP
public function index()
{
    // Get all data from Project table
    $projects = Hello::latest()->get();

    // return $prjects;
    return view('projects', ['projects' => $projects]);
}
```
- If you want to fetch jetstream users, use below code instead of upper code
```PHP
public function index()
{
    $users = \DB::table('users')->select('*')->get();

    return view('Student')->with('users', $users);
}
```
- Now setup a view page in `resources > views > projects.blade.php` and write the below code to view data
```
<ul>
    @foreach($projects as $project)

    <li><strong>Name: </strong>{{$project->name}}</li>
    <li><strong>Body Name: </strong>{{$project->body}}</li>

    @endforeach
</ul>
```
- Now visit the http://127.0.0.1:8000/hello page and see result
- See how to show data in single page → https://github.com/forhad-php/laravel/blob/main/show-data-in-single-page.md
