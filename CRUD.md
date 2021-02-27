- First we need to login if the jetstream installed. Otherwise an error can occoure.
- First we create a route `Route::get('/notices', 'App\Http\Controllers\NoticeController@index');` in `routes > web.php`
- And create a file in `Resource > views > notices.blade.php`
- After all execute the command `php artisan make:model Notice -mc --resource`
- Now we have -
1. Database > Migrations > 2021_02_19_112725_create_notices_table.php
2. App > Models > Notice.php
3. App > HTTP > Controllers > NoticeController.php
 
    
    

