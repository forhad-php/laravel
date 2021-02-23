- Start a new project with Jetstream `laravel newProjectName test --jet`
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



##  Create a menu with dashboard:
- Suppose we creat a link named `Exam`
- Adding the line `Route::Resource('exam', App\Http\Controllers\TaskController::class);` into `routs > web.php`
- Go ot `resources > views > navigation-menu.blade.php` → dublicate the code below and replace the dashboard with `exam`
```
<!-- Navigation Links -->
<div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
    <x-jet-nav-link href="{{ route('dashboard') }}" :active="request()->routeIs('dashboard')">
        {{ __('Dashboard') }}
    </x-jet-nav-link>
</div>
```
- Run the command `php artisan make:model Exam -mc --resource`

