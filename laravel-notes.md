# Laravel Framework Cheat Sheet

## Introduction to Laravel

- **What is Laravel?** Laravel is a powerful PHP web application framework known for its elegant syntax, developer-friendly tools, and robust features.

## Laravel Basics

- **Installation:** Install Laravel using Composer by running `composer create-project laravel/laravel project-name`.

- **Configuration:** Configure the application settings in `.env` and `config` files.

- **Artisan CLI:** Use the Artisan command-line tool for various tasks like migrations, seeding, and generating code.
## Launch your Laravel project

Open a terminal in the directory of your project, and type:
```
php artisan serve
```
You will then be given URL that the server is running on.

## Create a new controller

```
php artisan make:controller MyController
```

## MVC Architecture

Model: Represents the application's data and business logic.

```
// Example User model
class User extends Model {
    protected $table = 'users';
}
```

View: Handles the presentation layer and UI.

Controller: Processes user requests, interacts with models, and renders views.

```
// Example controller method
public function index() {
    $users = User::all();
    return view('users.index', compact('users'));
}
```

## Laravel Components

Eloquent ORM: Laravel's built-in ORM for database access.

Blade Templates: Blade is a templating engine for creating dynamic views.

blade.php

```
<!-- Blade template example -->
@foreach ($users as $user)
    <p>{{ $user->name }}</p>
@endforeach
```

Middleware: Middleware handles HTTP requests before they reach the application.

```
// Example middleware
public function handle($request, Closure $next) {
    // Perform actions before the request is handled
    return $next($request);
}
```

Routing: Define routes and controllers for handling HTTP requests.

```
// Example route definition
Route::get('/users', 'UserController@index');
```

Validation: Validate user input with Laravel's validation rules.

```
// Example validation
$validatedData = $request->validate([
    'name' => 'required|max:255',
    'email' => 'required|email|unique:users',
]);
```

## Database

Migration: Create and manage database tables using migrations.

### Create a new migration

```
php artisan make:migration create_users_table
```

Seeder: Populate the database with sample data using seeders.

### Create a new seeder

```
php artisan make:seeder UsersTableSeeder
```

Query Builder: Build database queries using Laravel's query builder.

```
// Example query
$users = DB::table('users')->where('active', 1)->get();
```

## Authentication and Authorization

Authentication: Easily implement user authentication.

```
// Example authentication routes
Auth::routes();
```

Authorization: Define access control policies with Laravel's gate feature.

```
// Example authorization gate
Gate::define('update-post', function ($user, $post) {
    return $user->id === $post->user_id;
});
```

## Forms and Requests

Forms: Create and handle HTML forms with Laravel's form builder.

Request Validation: Validate incoming HTTP requests with custom rules.

CSRF Protection: Laravel provides built-in CSRF protection for forms.

blade.php

```
<!-- Example form in Blade template -->
<form method="POST" action="/profile">
    @csrf
    <!-- Form fields -->
</form>
```

Middleware
Custom Middleware: Create custom middleware for handling specific tasks in the request-response cycle.

Middleware Groups: Group and apply middleware to routes.

## API Development

API Routes: Create routes specifically for API endpoints.

Resource Controllers: Use resource controllers for RESTful API development.

API Authentication: Implement API authentication using tokens or OAuth.

## File Storage

File Uploads: Handle file uploads with Laravel's built-in features.

File Storage: Use Laravel's file storage system for managing uploaded files.

## Testing

PHPUnit Integration: Laravel includes PHPUnit for testing.

Testing Database: Use an in-memory SQLite database for testing.

Test Factories: Create factories for generating test data.

## Laravel Resources

[Laravel Official Documentation: Comprehensive documentation and guides](https://laravel.com/docs/).

[Laracasts: Video tutorials and screencasts for learning Laravel](https://laracasts.com/).

[Packagist Laravel Packages: A collection of Laravel packages](https://packagist.org/search/?query=Laravel).
