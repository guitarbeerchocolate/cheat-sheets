# Totara Development Cheat Sheet

This cheat sheet provides an overview of common tasks and tools for Totara development, organized by key areas such as environment setup, module development, and theme customization.

---

## Table of Contents

- [Environment Setup](#environment-setup)
- [Folder Structure](#folder-structure)
- [Module Development](#module-development)
  - [Create a New Module](#create-a-new-module)
  - [Database Migrations](#database-migrations)
  - [Event Handlers](#event-handlers)
  - [Cron Jobs](#cron-jobs)
- [Theme Development](#theme-development)
  - [Customizing Themes](#customizing-themes)
- [API References](#api-references)
  - [User API](#user-api)
  - [Course API](#course-api)
  - [Enrolment API](#enrolment-api)
- [Tips and Best Practices](#tips-and-best-practices)

---

## Environment Setup

1. **System Requirements**

   - PHP 7.2+
   - MySQL or PostgreSQL
   - Apache or Nginx
   - Git for version control

2. **Setting Up Totara LMS**

   - Clone Totara from the repository:
     ```bash
     git clone https://github.com/totara/totara.git
     cd totara
     ```
   - Set up database and adjust the `config.php` file accordingly.
   - Install dependencies:
     ```bash
     composer install
     ```
   - Install Totara by navigating to the installation URL in your browser.

3. **Enabling Developer Mode**
   - In `config.php`:
     ```php
     $CFG->debug = (E_ALL | E_STRICT);
     $CFG->debugdisplay = 1;
     $CFG->debugging = 'DEVELOPER';
     ```

---

## Folder Structure

- **`/admin`**: Administrative functionality and scripts.
- **`/auth`**: Authentication plugins.
- **`/blocks`**: Block plugins, UI elements that display content.
- **`/course`**: Course-related code.
- **`/mod`**: Modules (activities and resources).
- **`/theme`**: Theme files for UI customization.
- **`/totara`**: Totara-specific plugins, e.g., HR features.
- **`/local`**: Custom local plugins.
- **`/lang`**: Language files.

---

## Module Development

### Create a New Module

1. **Folder Structure**: Inside `/mod/yourmodule`:

   - `version.php`: Version info for the module.
   - `lib.php`: Main library file for the module.
   - `mod_form.php`: Module settings form.
   - `index.php`: Entry point for the module.
   - `view.php`: View logic for the module.

2. **version.php**:

   ```php
   $plugin->component = 'mod_yourmodule'; // Full plugin name
   $plugin->version   = 2024100600;       // YYYYMMDDXX
   $plugin->requires  = 2018051700;       // Required Moodle version
   ```

3. **Install XMLDB schema:** Define the database schema in `db/install.xml`.

4. **Capabilities:** Define permissions in `db/access.php`:

```
$capabilities = [
    'mod/yourmodule:view' => [
        'riskbitmask' => RISK_XSS,
        'captype' => 'read',
        'contextlevel' => CONTEXT_MODULE,
        'archetypes' => ['student' => CAP_ALLOW],
    ],
];
```

### Database Migrations

- Use `db/upgrade.php` for database migrations.
- Example:
  ```php
  if ($oldversion < 2024100600) {
      // Define a new table.
      $table = new xmldb_table('yourmodule');
      $table->add_field('id', XMLDB_TYPE_INTEGER, '10', XMLDB_UNSIGNED, XMLDB_NOTNULL, XMLDB_SEQUENCE);
      upgrade_mod_savepoint(true, 2024100600, 'yourmodule');
  }
  ```

### Event Handlers

- Define event handlers in `db/events.php`:

  ```php
  $observers = [
      [
          'eventname' => '\core\event\course_completed',
          'callback' => 'mod_yourmodule_observer::course_completed',
      ],
  ];
  ```

### Cron Jobs

- Define cron tasks in `db/tasks.php`:

  ```php
  $tasks = [
      [
          'classname' => 'mod_yourmodule\task\yourmodule_cron_task',
          'blocking' => 0,
          'minute' => '*/15',
          'hour' => '*',
          'day' => '*',
          'dayofweek' => '*',
          'month' => '*',
      ],
  ];
  ```

## Theme Development

### Customizing Themes

1. **Creating a new theme**:

   - Copy an existing theme (like Boost).
   - Modify `theme/yourtheme/config.php`:

     ```php
     $THEME->name = 'yourtheme';
     $THEME->sheets = ['custom'];
     ```

2. **SCSS Customization**:

   - Add custom SCSS to `scss/yourtheme.scss`.

3. **Mustache Templates**:

   - Custom HTML templates in `/templates`.
   - Example template logic:

     ```mustache
     <div class="custom-class">{{{output.content}}}</div>
     ```

---

## API References

### User API

- **Create a user**:

  ```php
  $user = new stdClass();
  $user->username = 'jdoe';
  $user->email = 'jdoe@example.com';
  $user->id = user_create_user($user);
  ```

### Course API

- **Create a course**:

  ```php
  $course = new stdClass();
  $course->fullname = 'Sample Course';
  $course->shortname = 'SAMP001';
  $course->category = 1; // Category ID
  $course->id = create_course($course);
  ```

### Enrolment API

- **Enrol a user in a course**:

  ```php
  $enrol = enrol_get_plugin('manual');
  $instance = enrol_get_instances($courseid, true);
  $enrol->enrol_user($instance->id, $userid);
  ```

## Tips and Best Practices

- **Use Coding Guidelines**: Follow [Moodle coding style](https://moodledev.io/general/development/policies/codingstyle).
- **Security**: Always validate user inputs and escape outputs.
- **Debugging**: Enable developer mode and use logging:

  ```php
  error_log('Debug message here');
  ```
