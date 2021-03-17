First we need "Intervention Image" which is a PHP image handling and manipulation library. So execute the command - `composer require intervention/image`


Open config/app.php file and scroll down below in `'providers' => [...]` array add the below line of code.
```PHP
Intervention\Image\ImageServiceProvider::class
```


Next is to add the facade of this package to the `'aliases' => [...]` array, just below the providers array list.
```PHP
'Image' => Intervention\Image\Facades\Image::class
```


Now execute the command `php artisan make:migration add_post_thumbnail_to_posts_table --table=posts` to create a new table in the database.

Now go to the file `database/migrations/[DATE]_add_post_thumbnail_to_posts_table.php` and paste the code below -
```PHP
/**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('posts', function (Blueprint $table) {
            $table->string('post_thumbnail')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('posts', function (Blueprint $table) {
            $table->dropColumn('post_thumbnail');
        });
    }
```


Now run the migration - `php artisan migrate`
