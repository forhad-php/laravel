
Previusly we used the below code in `App > Http > Controllers > NoticeController.php`

```
public function index()
{
    // Get all data from Project table
    $notices = Notice::latest()->get();

    // return $notices into view page as a 'notices' object
    return view('/notices.index', ['notices' => $notices]);
}
```

And we need to view same data in `welcome` page. So add this `View::share('welcome', $notices);` single line in the existing code. The final code below,

```
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

```
@foreach($notices as $notice)
    <tr>
        <th>{{$notice->say}}</th>
    </tr>
@endforeach
```
