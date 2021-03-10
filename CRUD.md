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



## Now we start CRUD oparation (Create)
- Go to `routs > web.php` and add the line `Route::get('/create-notice', 'App\Http\Controllers\NoticeController@create');`
- Go to `create()` method into `App > Http > Controllers > NoticeController.php` and write `return view('notices.create');`
- Now visit the URL `http://127.0.0.1:8000/create-notice` and show `create.blade.php`
- Now we create a submit form into `resources > views > notices > create.blade.php` through below code
```
<h2>Create a notice</h2>

<form action="/create-notice" method="POST">
    <!-- Laravel automatically generates a CSRF "token" for each active user session managed by the application. -->
    @csrf

    <!-- value="{{old('say')}}" allows to store old value from user of input field. The field doesn't empty though if the value not passed the validation and page reload  -->
    <p>
        <!-- <label for="title">Notice Title: </label>
        <input type="text" name="title" id="title" placeholder="Title" value="{{old('title')}}"> -->
        
        <label for="say"></label>
        <textarea name="say" id="say" placeholder="Your notice.." cols="30" rows="10">{{old('say')}}</textarea></p>
    <br>
    <!-- Show the error message -->
    <span style="color: red">{{$errors->first('say')}}</span>
    <button type="submit">Create</button>
</form>
```
> Note: Example of old value storing on input field = `<input type="text" name="title" id="title" value="{{old('title')}}">`
- Then we create another route into `routs > web.php` called `Route::post('/create-notice', 'App\Http\Controllers\NoticeController@store');`
- Now we work under `store()` method of `app > http > controllers > NoticeController.php` file. Write the below code
```
public function store(Request $request)
{
    // Validation
    request()->validate([
        'say' => 'required'
    ]);

    //Create an object 'Notice'
    $notice = new Notice();
    // String the request of 'say' field into the 'say' properties
    $notice->say = request('say');
    // save the request
    $notice->save();
    // redirect to notices/index.blade.php
    return redirect('/notices');
}
```
- We just need to visit - `http://127.0.0.1:8000/create-notice`



## CRUD oparation (Edit):
- Go to `Resources > Views > Notices` and we just create an Edit link through ID. Just add the below line
```
<a href="/notice/{{$notice->id}}/edit">Edit</a>
```
- Now we create a route for edit another for update. Just add the lines below into `routes > web.php`
```
Route::get('/notice/{id}/edit', 'App\Http\Controllers\NoticeController@edit');
Route::put('/notice/{id}/edit', 'App\Http\Controllers\NoticeController@update');
```
- Add below code into `App > Http > Controllers > NoticeController.php`
```
public function edit(Notice $notice, $id) // $id comes from Routs → web.php → Route::get('/notice/{{id}}/edit'...
{
    // We need all notices from database
    $notice = Notice::findOrFail($id);
    // Return to edit.blade.php page with passing notice data
    return view('notices.edit', ['notice' => $notice]);
}
```
- Paste the below code into `Resources > Views > Notices > edit.blade.php`
```
<h2>Edit a notice</h2>

<form action="/notice/{{$notice->id}}/edit" method="POST">
    <!-- Laravel automatically generates a CSRF "token" for each active user session managed by the application. -->
    @csrf
    @method('PUT')

    <p>
        <label for="say"></label>
        <textarea name="say" id="say" placeholder="Your notice.." cols="30" rows="10">{{$notice->say}}</textarea>
    </p>
    <br>
    <!-- Show the error message -->
    <span style="color: red">{{$errors->first('say')}}</span>
    <button type="submit">Update</button>
</form>
```
- Finaly write the below code into `App > Http > Controllers > NoticeController.php`
```
public function update(Request $request, Notice $notice, $id) // $id must be defined as a parameter
{
    // Validation
    request()->validate([
        'say' => 'required'
    ]);

    // Find all data from database table
    $notice = Notice::findOrFail($id);
    // Request of 'say' field into the 'say' properties
    $notice->say = request('say');
    // save the request
    $notice->save();
    // redirect to notices/index.blade.php
    return redirect('/notices');
}
```



## CRUD oparation (Delete):
- Add the line below into `index.blade.php` file
```
<!-- Create a Delete link through ID -->
<form onSubmit="return confirm('Do you want to delete?')" action="/notice/{{$notice->id}}/delete" method="POST">
    @csrf

    <button type="submit">Delete</button>
</form>
```
- Then add the line `Route::post('/notice/{id}/delete', 'App\Http\Controllers\NoticeController@destroy');` into `web.php` file
> Remenber: Again every time create a route if there any error just execute `php artisan route:cache`
- Finally add the code below into `NoticeController.php` file
```
public function destroy(Notice $notice, $id) // $id must be defined as a parameter
// $id comes from Routs → web.php → Route::get('/notice/{{id}}/edit'...
{
    // Find all data from database table
    $notice = Notice::findOrFail($id);

    // Delete the request
    $notice->delete();

    // redirect to notices/index.blade.php
    return redirect('/notices');
}
```



> Note: Laravel 8 CRUD Tutorial by Example → https://www.techiediaries.com/laravel-8-crud-tutorial/ (Must be check out next time)
