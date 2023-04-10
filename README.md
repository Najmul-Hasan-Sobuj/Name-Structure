# Name-Structure



What is the actual structure of how to name a route, side-bar, model-migration-controller, function, etc.? I'm not saying that my structure is best written this way. You can write as you wish. But it is better to create or follow a structure to increase the productivity of writing code.

Now I teach you some basic name structure:

I will give three examples to make it easier for you to understand. For this I will use `User`, `User Profile` and `User Profile Manage`.

### Structure of Route:

To define a route named "user.*" in Laravel, you can use the `name()` method on your route definition:

If you have created a custom folder for the controller, you must use that path after the controller, for example: 

- Example 1: `use App\Http\Controllers\Admin\UserController;`
- Example 2: `use App\Http\Controllers\Frontend\UserController;`
- Example 3: `use App\Http\Controllers\Admin\UserProfileController;`
- Example 4: `use App\Http\Controllers\Frontend\UserProfileController;`
- Example 5: `use App\Http\Controllers\Admin\UserProfileManageController;`
- Example 6: `use App\Http\Controllers\Frontend\UserProfileManageController;`

```php
use App\Http\Controllers\UserController;
// user route 

Route::get('user', [UserController::class, 'index'])->name('user.index');
Route::get('user/create', [UserController::class, 'create'])->name('user.create');
Route::post('user', [UserController::class, 'store'])->name('user.store');
Route::get('user/{id}/edit', [UserController::class, 'edit'])->name('user.edit');
Route::put('user/{id}', [UserController::class, 'update'])->name('user.update');
Route::get('user/{id}', [UserController::class, 'show'])->name('user.show');
Route::delete('user/{id}', [UserController::class, 'destroy'])->name('user.destroy');
```

```php
use App\Http\Controllers\UserProfileController;
// user profile route 

Route::get('user-profile', [UserProfileController::class, 'index'])->name('user.profile.index');
Route::get('user-profile/create', [UserProfileController::class, 'create'])->name('user.profile.create');
Route::post('user-profile', [UserProfileController::class, 'store'])->name('user.profile.store');
Route::get('user-profile/{id}/edit', [UserProfileController::class, 'edit'])->name('user.profile.edit');
Route::put('user-profile/{id}', [UserProfileController::class, 'update'])->name('user.profile.update');
Route::get('user-profile/{id}', [UserProfileController::class, 'show'])->name('user.profile.show');
Route::delete('user-profile/{id}', [UserProfileController::class, 'destroy'])->name('user.profile.destroy');
```

```php
use App\Http\Controllers\UserProfileManageController;
// user profile manage route 

Route::get('user-profile-manage', [UserProfileManageController::class, 'index'])->name('user.profile.manage.index');
Route::get('user-profile-manage/create', [UserProfileManageController::class, 'create'])->name('user.profile.manage.create');
Route::post('user-profile-manage', [UserProfileManageController::class, 'store'])->name('user.profile.manage.store');
Route::get('user-profile-manage/{id}/edit', [UserProfileManageController::class, 'edit'])->name('user.profile.manage.edit');
Route::put('user-profile-manage/{id}', [UserProfileManageController::class, 'update'])->name('user.profile.manage.update');
Route::get('user-profile-manage/{id}', [UserProfileManageController::class, 'show'])->name('user.profile.manage.show');
Route::delete('user-profile-manage/{id}', [UserProfileManageController::class, 'destroy'])->name('user.profile.manage.destroy');
```

### Structure of Side-Bar:

As usual sidebar name is written `upper first` for
- Example 1: `User`
- Example 2: `User Profile`
- Example 3: `User Profile Manage`   


### Structure of Model || Migration || Controller:

To create a Laravel model, migration and controller, you need to follow the following steps:

1. Laravel Model, Migration, Controller create at a same time: 
To create a new model with migration (`{m}`) and controller (`{r}`) `r` mean resource controller in Laravel, run the following command:
if you use `c` then it means a normal controller
```
php artisan make:model ModelName -m
```
Replace "ModelName" with the name of your model.
- For Example 1: 

```
php artisan make:model User -mc
```
- For Example 2: 

```
php artisan make:model UserProfile -mc
```
- For Example 3: 

```
php artisan make:model UserProfileManage -mc
```

2. If you are create a single Laravel Migration:
To create a new migration in Laravel, run the following command:
```
php artisan make:migration create_table_name --create=table_name
```
Replace "create_table_name" with a name that describes the purpose of the migration and "table_name" with the name of the table you want to create.
must be includes the `s` name of the table you want to create. 
- For Example 1: 

```
php artisan make:migration create_users_name --create=table_name
```
- For Example 2: 

```
php artisan make:migration create_user_profiles_name --create=table_name
```
- For Example 3: 

```
php artisan make:migration create_user_profile_manages_name --create=table_name
```

3. If you are create a single Laravel Controller:
To create a new controller in Laravel, run the following command:
```
php artisan make:controller ControllerName
```
Replace "ControllerName" with the name of your controller.

If you want to create a custom folder for your controller, you can use the following command:

```
php artisan make:controller path/to/ControllerName
```
- For Example 1: 

```
php artisan make:controller path/to/UserController
```
- For Example 2: 

```
php artisan make:controller path/to/UserProfileController
```
- For Example 3: 

```
php artisan make:controller path/to/UserProfileManageController
```


Once you've created your controller, you can define your custom resource route in your `web.php` file like this:

```php
Route::resource('resource-name', 'App\Http\Controllers\CustomFolder\ControllerName');
```


### Structure of Model || Migration || Controller:


```php
     public static function singleFileUpload($mainFile)
     {
         $fileExtention    = $mainFile->getClientOriginalExtension();
         $fileOriginalName = $mainFile->getClientOriginalName();
         $file_size        = $mainFile->getSize();
         $currentTime      = Str::random(17);
         $fileName         = $currentTime . '.' . $fileExtention;

         $mainFile->storeAs('public/files', $fileName);

         $output['status']             = 1;
         $output['file_name']          = $fileName;
         $output['file_original_name'] = $fileOriginalName;
         $output['file_extention']     = $fileExtention;
         $output['file_size']          = $file_size;

         return $output;
     }
```

```php
    Helper::singleFileUpload($mainFile);
```

In this example, we are defining a dynamic parameter (`{mainFile}`) to match any value provided in the argument. 
noted the function name always use camelCase like this: `singleFileUpload`


Hope this helps!
