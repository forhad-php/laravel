- Upload entire app folder out of `public_html`
- Move the folder `public` into `public_html` directory
- Edit the file `index.php` and add the app folder name into URL like below
```php
require __DIR__.'/../example-app/vendor/autoload.php';
$app = require_once __DIR__.'/../example-app/bootstrap/app.php';
```
- If not enter into the website paste the below code into `routes/web.php`
```php
Route::get('/clear', function() {
    Artisan::call('cache:clear');
    Artisan::call('config:cache');
    Artisan::call('view:clear');
    return "Cleared!";
});
```
- Go to `www.example.com/clear` to clear the cacsh!
- Now again test..
- Now we fix the database and go to `example-app-name/.env` and set DB name, user, pass
- Done!
> Note: If again shows an error with previous access, Go to `www.example.com/clear` to clear the cacsh and try again.

## 404 Page Not Found
- Go to `public_html/.htaccess` and paste below code
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
```
- And Go to `app/Providers/AppServiceProvider.php` and paste below code under the `boot()` method
```PHP
$this->app->bind('path.public', function() {
return base_path().'/../public_html';
```
