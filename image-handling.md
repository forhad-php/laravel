- First we need "Intervention Image" which is a PHP image handling and manipulation library. So execute the command - `composer require intervention/image`
> Note: Package Documentation: http://image.intervention.io/getting_started/installation and a tutorial here https://www.youtube.com/watch?v=h0EwH5Jjctk
- Open config/app.php file and scroll down below in `'providers' => [...]` array add the below line of code.
```PHP
Intervention\Image\ImageServiceProvider::class
```
- Next is to add the facade of this package to the `'aliases' => [...]` array, just below the providers array list.
```PHP
'Image' => Intervention\Image\Facades\Image::class
```
- Now we create a route in `Routs > web.php`
```PHP
Route::get('/img', function()
{
    $img = Image::make('wordpress-code-poetry.jpg')->resize(300, 200);

    return $img->response('jpg');
});
```
- An image named `wordpress-code-poetry.jpg` exist in `Project-Name > Public` folder.
- Execute `php artisan route:cache` command and Visit: http://127.0.0.1:8000/img and see the result.

> Note: Full Blog Creating Tutorial =
> https://www.ryansutana.name/2017/07/how-to-create-a-blog-with-laravel-5-part-1-file-structure-templating/ (Blog series 5 parts)
> https://www.ryansutana.name/2017/08/how-to-upload-image-for-blog-post-in-laravel-5/ (Only for thumbnail image)
