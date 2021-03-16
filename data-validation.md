### Laravel 8 Validation Rules List → https://laravel.com/docs/8.x/validation#available-validation-rules

#### Note: Previusly I using `nullable` to escape the Email field when a user register with Jetstream. The code from `/database/migrations/2014_10_12_000000_create_users_table.php` look like below -

```PHP
public function up()
{
    Schema::create('users', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->string('age');
        $table->string('email')->unique()->nullable();
        $table->timestamps();
    });
}
```

> Note: See the `$table->string('email')->unique()->nullable();` means this field can nullable..

#### And ofcourse if you want any column to accept null values you will need to allow this in your migration or Go to phpMyAdmin > User Table > Email Column and Tick the box named Null

#### Also check `/app/Actions/Fortify/CreateNewUser.php` code

```PHP
Validator::make($input, [
    'name' => ['required', 'string', 'max:255'],
    'age' => ['required', 'string', 'max:2'],
    'email' => ['nullable', 'string', 'email', 'max:255', 'unique:users'],
    'password' => $this->passwordRules(),
    'terms' => Jetstream::hasTermsAndPrivacyPolicyFeature() ? ['required', 'accepted'] : '',
])->validate();
```

> Note: See the `'email' => ['nullable', 'string', 'email', 'max:255', 'unique:users'],` means this field can nullable..

And finally check `/resources/views/auth/register.blade.php` is there any `required` property available here

```HTML
<x-jet-input id="age" class="block mt-1 w-full" type="number" name="age" :value="old('age')" required />
<x-jet-input id="email" class="block mt-1 w-full" type="email" name="email" :value="old('email')" />
```

> Note: See the defferent of two line above? The email input field has no `required`
