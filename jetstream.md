https://stackoverflow.com/questions/63827708/how-to-create-a-jetstream-project-via-composer-in-laravel-8
- Start a new project with Jetstream `laravel new projectName --jet`
> stack = livewire or inertia. Livewire using Tailwind CSS and inertia using vue --teams for support team options.
- Follow https://jetstream.laravel.com/2.x/installation.html#installing-jetstream
> If you decide to create a new project with JetStream Authentication then this is the best practice without any issues.
- Adding Jetstream existing project :point_down:
> If you’re using Windows, and you’re using Git-Bash, you might notice that composer is not recognized sometimes, even though you have it installed globally. Just switch to CMD and run the command there. After completion, it’s time to install JetStream with either Livewire or Intertia options.

- So first thing is first, open `run` from windows and type `cmd` to open the `command prompt`
- To run the command in the project location > go to the porject folder > click on addressbar > clear all > write `cmd` and enter
- Now clear the cache of routes using. Execute the command `php artisan route:cache` in cmd
- Use the command `composer require laravel/jetstream` to require jetstream in laravel
- command `php artisan jetstream:install livewire` to install jetstream
> Note: Now we see some new directory in our project like `App > Action > Fortify & Jetstream`, `Resources > Views > Auths` etc.
- Execute `npm install && npm run dev` to build assets
- Now migrate the migrations using command `php artisan migrate`
> Note: After all we see some new tables in the database like users, sessions, password_resets etc.



##  Create a menu link with dashboard and views the data:
- Suppose we creat a link named `purchases`
- Adding the line `Route::Resource('purchases', App\Http\Controllers\PurchasesController::class);` into `routs > web.php`
- Go ot `resources > views > navigation-menu.blade.php` → add this code below under the `<!-- Navigation Links -->` comment and after the Dashboard section
```
<!-- Navigation Links -->
<div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
    <x-jet-nav-link href="/purchases" :active="request()->routeIs('purchases.index')">
        {{ __('Purchases') }}
    </x-jet-nav-link>
</div>
```
- Run the command `php artisan make:model Purchases -mc --resource`
- Go to `App > Http > Controllers > PurchasesController.php` and setup the code below
```php
public function index()
{
    // Get → latest() fetches the most recent set of data from the Database.
    $purchases = Purchases::latest()->get();

    // Passing the $prjects data into purchases view page
    return view('purchases', ['purchases' => $purchases]);
}
```
- Now we duplicate the page `Resources > Views > dashboard.blade.php` and paste the table code form https://tailwindui.com/components/application-ui/lists/tables
```HTML
<div class="py-12">
    <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <!-- Delete the welcome and paste the table code here -->

    </div>
</div>
```



##  Create a new field in registration form:
- First, go to `resources > views > auth > register.blade.php` and create a new age field via below code
```
<div class="mt-4">
    <x-jet-label for="age" value="{{ __('Age') }}" />
    <x-jet-input id="age" class="block mt-1 w-full" type="number" name="age" :value="old('age')" required />
</div>
```
- To create a table in database, go to `database > migrations > 2014_10_12_000000_create_users_table.php` and add this `$table->string('age');` line after any field
- Now go to `App > Models > User.php` and add the age attribute like below
```PHP
protected $fillable = [
    'name', 'email', 'age', 'password',
];
```
- Then go to `App > Actions > Fortify > CreateNewUser.php` and add the line `'age' => ['required', 'string', 'max:2'],` into `Validator::make($input, [` and add another line `'age' => $input['age'],` into `return DB::transaction(function () use ($input) {`
- Finally run the command `php artisan migrate:fresh`



##  Others Customization:
- To customize dashboard `Resources > Views > welcome.blade.php`
- To customize user profile welcome page go to `vendor > laravel > jetstream > resources > views > components > welcome.blade.php`
- To get profile picture feature, comment out the line `Features::profilePhotos(),` into `config > jetstream.php` file
- - To chagne the dashboard logo, Go to `resources > views > navigation-menu.blade.php`
```
<!-- Logo -->
<div class="flex-shrink-0 flex items-center">
    <a href="{{ route('dashboard') }}">
        <img src="https://picsum.photos/10" class="rounded-full h-10 w-10 object-cover" />
    </a>
</div>
```
