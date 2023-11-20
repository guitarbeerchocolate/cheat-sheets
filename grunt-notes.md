# Grun cheat sheet

## Introduction to Grunt

What is Grunt? Grunt is a JavaScript task runner that automates common tasks in your development workflow.

Why Grunt? Grunt simplifies repetitive tasks, like minification, compilation, unit testing, and more, making your development process more efficient.

## Getting Started

Installation: Install Grunt globally using npm (Node Package Manager):

```
npm install -g grunt-cli
```

Project Setup: Create a package.json file and add Grunt as a development dependency:

```
npm init
npm install grunt --save-dev
```

Create a Gruntfile: Create a Gruntfile.js in your project root to define tasks and configurations.

## Gruntfile Basics

Load Grunt Plugins: Use grunt.loadNpmTasks('plugin-name') to load Grunt plugins.

Configuration: Configure tasks using the `grunt.initConfig({})` method.

Register Tasks: Register tasks with `grunt.registerTask('task-name', ['task1', 'task2'])`.

Common Grunt Tasks
Linting: Use Grunt for code linting with plugins like grunt-contrib-jshint or grunt-eslint.

Concatenation: Combine multiple files into one with grunt-contrib-concat.

Minification: Minify JavaScript and CSS files with grunt-contrib-uglify and grunt-contrib-cssmin.

Sass/LESS Compilation: Compile Sass or LESS files into CSS using grunt-contrib-sass or grunt-contrib-less.

File Watch: Automatically run tasks when files change with grunt-contrib-watch.

Testing: Run tests with plugins like grunt-contrib-qunit or grunt-contrib-jasmine.

Live Reload: Use grunt-contrib-connect and grunt-contrib-livereload for live-reloading during development.

## Sample Gruntfile.js

```
module.exports = function(grunt) {
  // Load Grunt plugins
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-uglify');

  // Configure tasks
  grunt.initConfig({
    jshint: {
      files: ['src/**/*.js'],
      options: {
        esversion: 6,
        globals: {
          jQuery: true
        }
      }
    },
    uglify: {
      my_target: {
        files: {
          'dist/output.min.js': ['src/**/*.js']
        }
      }
    }
  });

  // Register tasks
  grunt.registerTask('default', ['jshint', 'uglify']);
};
```

## Running Grunt

Run All Tasks: Execute all registered tasks by running `grunt`.

Run Specific Task: Run a specific task with `grunt task-name`.

Watch: Use `grunt watch` to watch for file changes and run tasks automatically.
