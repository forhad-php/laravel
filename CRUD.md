## First we view the data from database

> Remember: We need to login if the jetstream installed. Otherwise an error can occoure.
- First we create a route `Route::get('/notices', 'App\Http\Controllers\NoticeController@index');` in `routes > web.php`
- Create a folder `notices` in `resources > viwes` and also create three files `index.blade.php`, `create.blade.php`, and `edit.blade.php`
- After all execute the command `php artisan make:model Notice -mc --resource`
- Now we have →
1. Database > Migrations > 2021_02_19_112725_create_notices_table.php
2. App > Models > Notice.php
3. App > HTTP > Controllers > NoticeController.php
- Now we create a schema in `database > migrations > 2021_02_27_040045_create_notices_table.php` through below code
```
Schema::create('notices', function (Blueprint $table) {
    $table->id();
    $table->string('say');
    $table->timestamps();
});
```
- Execute the command `php artisan migrate`
- Now we are going to `App > Http > Contorllers > NoticeController.php` and write the code below
```
public function index()
{
    // Get all data from Project table
    $notices = Notice::latest()->get();

    // return $notices into view page as a 'notices' object
    return view('/notices.index', ['notices' => $notices]);
    // Because we create a folder named `notices` and the `.index` mean `index.blade.php` file
}
```
- Finally we view the data into `resources > views > notices > index.blade.php` through below code
```
<ul>
    @foreach($notices as $notice)

    <li><strong>Notice: </strong>{{$notice->say}}</li>

    @endforeach
</ul>
```
> Note: If any error faces, Execute the command `php artisan route:cache` first



## Now we start CRUD oparation
- Go to `routs > web.php` and add the line `Route::get('/create-notice', 'App\Http\Controllers\NoticeController@create');`
- Go to `create()` method into `App > Http > Controllers > NoticeController.php` and write `return view('notices.create');`
- Now visit the URL `http://127.0.0.1:8000/create-notice` and show `create.blade.php`
- Now we create a submit form into `resources > views > projects > create.blade.php`
