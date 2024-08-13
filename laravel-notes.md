# Laravel Framework Cheat Sheet

## Introduction to Laravel

- **What is Laravel?** Laravel is a powerful PHP web application framework known for its elegant syntax, developer-friendly tools, and robust features.

## Laravel Basics

### Start using laravel commands

```
composer global require laravel/installer
```

- **New project:** Install Laravel using Composer by running:

```
laravel new project-name
```

- **Configuration:** Configure the application settings in `.env` and `config` files.

- **Artisan CLI:** Use the Artisan command-line tool for various tasks like migrations, seeding, and generating code.

## Launch your Laravel project

Open a terminal in the directory of your project, and type:

```
php artisan serve
```

You will then be given URL that the server is running on.
At this stage, you should also make use of the npm packages. Open another terminal and run:

```
npm i
```

Once those packages have been install, you can run the npm dev environment, thus:

```
npm run dev
```

This includes the Vite server which listens for asset changes in files such as JS and CSS. To have blade content automatically update in the browser when saved...

In the HTML->HEAD tag of your blade template file add the vite directive, thus:

```
@vite(['resources/css/app.css', 'resources/js/app.js'])
```

As a results changes are seen immediately in the web browser. You may need to re-run `npm run dev` for this to take effect.

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

### Laravel Breeze

Installing Laravel Breeze starter kit provides all the authentication features, including balde templates styled with Tailwind CSS.

```
composer require laravel/breeze
php artisan breeze:install
npm run dev
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

### Tailwind

Tailwind should automatically be available in your Laravel project. If not, just add it to `postcss.config.js`, thus:

```
export default {
    plugins: {
        tailwindcss: {},
        autoprefixer: {},
    },
};
```

## Steps for creating a new functionality

Before we go too far, remember this. Eloquent cleverly makes associations between elements of your application.

In addition to the steps below, you'll probably want to add the laravel debug bar through composer, thus:

```
composer require barryvdh/laravel-debugbar --dev
```

### 1. Create the files

```
php artisan make:model <Yourmodelname> --all
```

Will generate a migration, seeder, factory, policy, resource controller, and form request classes for the model:

A model within app/Models/

A Factory within database/factories/

A Migration within database/migrations/

A Seeder within database/seeders/

A Store Request within app/Http/Requests/

An Update Request within app/Http/Requests/

A Controller within app/Http/Controllers/

A Policy within app/Policies/

### 2. Add some routes

You can begin by adding, just the routes like this:

```
Route::get('/yourfunctionality', function () {
    return 'Basic index get';
});
Route::get('/yourfunctionality/create', function () {
    return 'Basic create';
});
Route::post('/yourfunctionality', function () {
    return 'Basic store';
});
Route::get('/yourfunctionality/{yourfunctionalityitem}', function () {
    return 'Basic show';
});
Route::get('/yourfunctionality/{yourfunctionalityitem}/edit', function () {
    return 'Basic edit';
});
Route::patch('/yourfunctionality/{yourfunctionalityitem}', function () {
    return 'Basic update';
});
Route::delete('/yourfunctionality/{yourfunctionalityitem}', function () {
    return 'Basic destroy';
});
```

Then gradually, start adding items returned from your controller, like this:

```
Route::get('/yourfunctionality', [YourController::class, 'index']);
Route::get('/yourfunctionality/create', [YourController::class, 'create']);
Route::post('/yourfunctionality', [YourController::class, 'store'])->middleware('auth');
Route::get('/yourfunctionality/{yourfunctionalityitem}', [YourController::class, 'show']);
Route::patch('/yourfunctionality/{yourfunctionalityitem}', [YourController::class, 'update']);
Route::delete('/yourfunctionality/{yourfunctionalityitem}', [YourController::class, 'destroy']);
```

While we're at it, let's make associated routes more readable by grouping them thus:

```
Route::Controller(YourController::class)->group(function()
{
    Route::get('/yourfunctionality', 'index');
    Route::get('/yourfunctionality/create', 'create');
    Route::post('/yourfunctionality', 'store')->middleware('auth');
    Route::get('/yourfunctionality/{yourfunctionalityitem}', 'show');
    Route::patch('/yourfunctionality/{yourfunctionalityitem}', 'update');
    Route::delete('/yourfunctionality/{yourfunctionalityitem}', 'destroy');
});
```

Before proceeding, test that these work.

### 3. Develop our migrations

You should have some idea about what data you want to use with your class. Even if it's not fully formed, you should create something and improve it later.

To create a new migration use:

```
php artisan make:migration
```

To push your migration to the database use:

```
php artisan migrate
```

If you make changes to your migration and wish to push them to your database use:

```
php artisan migrate:fresh
```

To see all options:

```
php artisan
```

and look for migrate.

### 4. Develop our model

Now that we have our migration, we can develop our model a little.
When we created the files in step 1, a factory was one of them. As a result, the new model contains a refence to it through `use HasFactory;`
, thus:

```
class YourModel extends Model {
    use HasFactory;
}
```

Laravel by default, assumes that this model will be used to work with a table called your_model, as described in the migration.

You can make sure of this through an override such as:

```
class JobListing extends Model {
    use HasFactory;
    protected $table = 'your_model';
}
```

$fillable is an array containing all table fields that can be mass-assigned through the create and update methods.

$guarded is an array of fields that should not be mass-assigned. By default, it contains all model attributes, acting as a blacklist.

When using the create or update methods, Laravel checks if the incoming data only contains the fields listed in the $fillable array or if it doesn't contain the fields listed in the $guarded array. If not, it will throw a MassAssignmentException. This helps ensure that only intended fields are updated, protecting your application from unwanted modifications.

```
class YourModel extends Model {
    use HasFactory;
    protected $table = 'job_listing';
    protected $fillable = ['title','salary'];
}
```

The created_at, and updated_at fields are automatically created and updated by laravel.

### 5. Develop the factory

A factory is used to create example (or "fake") data for your database.

Match the items returned from the `function definition()` to your migration.

Foreign keys can be added by adding the mode to which they refer e.g.

```
'user_id' => User::factory()
```

### 6. Develop a seeder for your factory

Open the seed file created in step 1.
Develop the function run thus:

```
public function run(): void
{
    YourModel::factory(200)->create();
}
```

When this seeder is run it will create 200 records according to the definitions of its factory. To run all the seeders:

```
php artisan db:seed
```

To run just 1 seeder:

```
php artisan db:seed --class=YourSeederName
```

### 7. Develop relationships within models

Imagine we have a model for Job, and another model for Employer.
Each Job belongs to an employer, i.e. a Job can only have one employer. You can therefore create a function for employer within the Job model, thus:

```
public function employer()
{
    return $this->belongsTo(Employer::class);
}
```

In this example, an employer can have many jobs and so we can apply a similar function for jobs within the employer model, thus:

```
public function jobs()
{
    return $this->hasMany(Job::class);
}
```

### 8. Develop pivot tables (optional)

Imagine you have 2 tables. 1 table contains jobs, the other contains tags. You might need a third table to connect the 2, so that you can have a record of all the tags for a job. This is called a pivot table.

You can add the migration code to either the job or tag migrations, but it's useful to name the pivot table with the 2 related tables e.g. job_tag. Therefore the migration code would look like this:

```
Schema::create('job_tag', function (Blueprint $table) {
    $table->id();
    $table->foreignIdFor(\App\Models\Job::class, 'job_id')->constrained()->cascadeOnDelete();
    $table->foreignIdFor(\App\Models\Tag::class, 'tag_id')->constrained()->cascadeOnDelete();
    $table->timestamps();
});
```

In this example, `$table->foreignIdFor(\App\Models\Job::class, 'job_id')` creates a foreign key column `'job_id'` that references the primary key of the `'jobs'` table.

The `constrained()` method adds a foreign key constraint, and `cascadeOnDelete()` ensures that when a job is deleted, all related records in the 'job_tag' table are also deleted.

`$table->foreignIdFor(\App\Models\Tag::class, 'tag_id')` creates a foreign key column `'tag_id'` that references the primary key of the `'tags'` table. Similar to the `'job_id'` column, it adds a foreign key constraint and cascades deletes.

`$table->timestamps()` creates two timestamp columns `'created_at'` and `'updated_at'` to store the creation and update timestamps for each record.

This migration creates a **many-to-many** relationship table for the `'jobs'` and `'tags'` tables, allowing jobs to have multiple tags and vice versa.

We also have work to do in our Job model, and Tag model to support this. In the Job model apply a function tags, thus:

```
public function tags()
{
    return $this->belongsToMany(Tag::class);
}
```

In the Tag model apply a function job, thus:

```
public function jobs()
{
    return $this->belongsToMany(Job::class);
}
```

### Queues (optional)

The database table which supports queues is called `'jobs'`. It's quite common to change this and give it a more meaningful name such as `'queue_jobs'`. To do this go to the `config/queue.php` file and set the new names there. You will then need to change the job migrations to reflect these changes and refresh them as described earlier.

Conceptually, queues look like this:

1. A job is dispatched to a queue. This job could be an email which is about to be sent, or really any kind of function.
2. The job sits on the queue until a worker can pick it up.
3. A worker removes the job from the queue and executes it.

A code example for this would be the following:

```
Mail::to($job->employer->user)->queue(
    new JobPosted($job)
);
```

In the example above, the method `send` is replaced by `queue` i.e. the job is being sent to the queue and a worker will send the mail.

To get workers to take jobs from the queue, run the command:

```
php artisan queue:work
```

## Laravel Resources

[Laravel Official Documentation: Comprehensive documentation and guides](https://laravel.com/docs/).

[Laracasts: Video tutorials and screencasts for learning Laravel](https://laracasts.com/).

[Packagist Laravel Packages: A collection of Laravel packages](https://packagist.org/search/?query=Laravel).
