- First clear the cache of routes using. Execute the command `php artisan route:cache` in cmder
- Now use the command `composer require laravel/jetstream` to require jetstream in laravel
- command `php artisan jetstream:install livewire` to install jetstream
> Note: Now we see some new directory in our project like `App > Action > Fortify & Jetstream`, `Resources > Views > Auths` etc.
- Now migrate the migrations using command `php artisan migrate`
> Note: After all we see some new tables in the database like users, sessions, password_resets etc.



- Please execute "npm install && npm run dev" to build your assets. 
