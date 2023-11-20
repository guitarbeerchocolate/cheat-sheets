# Gulp cheat sheet

## Introduction to Gulp

What is Gulp? Gulp is a JavaScript task runner that helps automate repetitive tasks in your development workflow.

Why Gulp? Gulp simplifies tasks such as minification, concatenation, compilation, testing, and more, making your development process more efficient.

## Getting Started

Installation: Install Gulp globally using npm (Node Package Manager):

```
npm install -g gulp-cli
```

Project Setup: Create a package.json file and add Gulp as a development dependency:

```
npm init
npm install gulp --save-dev
```

Create a Gulpfile: Create a gulpfile.js in your project root to define tasks and configurations.

## Gulpfile Basics

Load Gulp Plugins: Use const pluginName = require('gulp-plugin-name') to load Gulp plugins.

Create Tasks: Define tasks using `gulp.task('task-name', () => {})`.

Run Tasks: Run tasks using the gulp command followed by the task name, e.g., `gulp task-name`.

## Common Gulp Tasks

Linting: Use Gulp for code linting with plugins like gulp-eslint or gulp-jshint.

Concatenation: Combine multiple files into one with `gulp-concat`.

Minification: Minify JavaScript and CSS files with `gulp-uglify` and `gulp-cssmin`.

Sass/LESS Compilation: Compile Sass or LESS files into CSS using `gulp-sass` or `gulp-less`.

File Watch: Automatically run tasks when files change with `gulp.watch`.

Testing: Run tests with plugins like gulp-jasmine or gulp-mocha.

Live Reload: Use gulp-connect and a live-reload plugin for live-reloading during development.

## Sample gulpfile.js

```
const gulp = require('gulp');
const eslint = require('gulp-eslint');
const uglify = require('gulp-uglify');

// Lint JavaScript files
gulp.task('lint', () => {
  return gulp.src(['src/**/*.js'])
    .pipe(eslint())
    .pipe(eslint.format())
    .pipe(eslint.failAfterError());
});

// Minify JavaScript files
gulp.task('minify', () => {
  return gulp.src('src/**/*.js')
    .pipe(uglify())
    .pipe(gulp.dest('dist'));
});

// Default task to run both lint and minify
gulp.task('default', gulp.series('lint', 'minify'));
```

## Running Gulp

Run All Tasks: Execute all tasks defined in the default task by running gulp.

Run Specific Task: Run a specific task with `gulp task-name`.

Watch: Use `gulp watch` or `gulp.watch` to watch for file changes and run tasks automatically.
