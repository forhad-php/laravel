
Previusly we used the below code in `App > Http > Controllers > NoticeController.php`

```PHP
public function index()
{
    // Get all data from Project table
    $notices = Notice::latest()->get();

    // return $notices into view page as a 'notices' object
    return view('/notices.index', ['notices' => $notices]);
}
```

And we need to view same data in `welcome` page. So add this `View::share('welcome', $notices);` single line in the existing code. The final code below,

```PHP
public function index()
{
    // Get all data from Project table
    $notices = Notice::latest()->get();

    // return $notices into view page as a 'notices' object
    return view('/notices.index', ['notices' => $notices]);

    View::share('welcome', $notices);
}
```

And in `welcome.blade.php` we just write below code to display the data

```PHP
@foreach($notices as $notice)
    <tr>
        <th>{{$notice->say}}</th>
    </tr>
@endforeach
```

After all we just query the table and pass into the welcome page. So we need to go `routes > web.php` and paste below code,

```PHP
Route::get('/', function () {

    $notices = DB::table('notices')->get();

    return view('welcome', ['notices' => $notices]);

});
```

I just show last single data from the table. So I wrote the below code,

```PHP
Route::get('/', function () {

    $notices = DB::table('notices')->latest()->take(1)->get();

    return view('welcome', ['notices' => $notices]);

});
```
