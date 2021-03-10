- Previously I've found an error like below,
```
ErrorException
Trying to get property 'profile_photo_url' of non-object (View: C:\xampp\htdocs\mrta2020\teaching-academy\resources\views\navigation-menu.blade.php)
```
> Then I've also found the solution that put `@auth` at the top of the file and put also `@endauth` at the bottom of the file that solve the problem. Basically we must call `@auth` and `@endauth` when we are using `{{ Auth::user()->profile_photo_url }}`
