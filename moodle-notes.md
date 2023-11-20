# Moodle Cheat Sheet

## Introduction to Moodle

What is Moodle? Moodle is an open-source Learning Management System (LMS) used to deliver online courses, manage content, and facilitate communication between students and instructors.

Key Features: Moodle offers features like course management, quizzes, forums, file sharing, grading, and more.

## User Roles

- Administrator: Manages the entire Moodle site.
- Teacher/Instructor: Manages courses, content, and assessments.
- Student: Enrolls in courses and participates in activities.

## Course Management

- Create a Course: As an administrator or teacher, navigate to "Site administration" > "Courses" > "Manage courses and categories" to create a new course.
- Enroll Students: Add students to a course by using enrollment methods like manual enrollment, self-enrollment, or LDAP enrollment.

## Adding Content

- Resources: Add resources like files, folders, URLs, labels, and pages to your course.
- Activities: Include interactive activities like quizzes, assignments, forums, surveys, and more.

## Grading

- Gradebook: Use the Moodle gradebook to set up and manage grading for assignments, quizzes, and other assessments.
- Grading Scales: Define custom grading scales or use predefined scales.
- Rubrics: Create rubrics to assess and grade student work.

## Communication

- Forums: Create discussion forums for students to communicate and collaborate.
- Announcements: Post course announcements to inform students about important updates.
- Messaging: Use the messaging system to send messages to students or other users.

## Quizzes and Assessments

- Create a Quiz: Build quizzes with various question types, including multiple-choice, true/false, short answer, and essay questions.
- Randomize Questions: Randomly select questions from a question bank to create unique quizzes.
- Grading Options: Choose different grading methods for quizzes, such as highest grade, average grade, or last attempt.

## Customization

- Themes: Customize the appearance of your Moodle site with themes or create custom themes.
- Plugins: Extend Moodle's functionality by installing and configuring plugins.

### Creating a basic moodle theme

Create a Custom CSS File
Create a custom CSS file (e.g., custom.css) where you will define the styles for your Moodle theme.

In your custom.css, define the colors and styles based on your color scheme. For example:

```
/* Primary color for headings and links */
h1, h2, h3, h4, h5, h6, a {
  color: #800080;
}

/* Secondary color for backgrounds and text */
body {
  background-color: #ffffff;
  color: #333333;
}

/* Custom styles for buttons */
button, .btn {
  background-color: #800080;
  color: #ffffff;
  border: none;
}

/* Additional custom styles for various Moodle elements */
/* Add your styles here */
```

#### Upload Your Custom Theme

Log in to your Moodle site as an administrator.

Navigate to "Site administration" > "Plugins" > "Themes" > "Theme selector."

Under "Theme selector," click on "Upload a new theme."

Upload the custom theme folder containing your custom.css and other theme files.

#### Configure Moodle to Use Your Custom Theme

After uploading the theme, you should see it listed in the theme selector.

Select your custom theme from the list and click "Save changes."

Moodle will now use your custom theme, and you should see the purple color scheme applied to your Moodle site.

## Creating a basic moodle plugin

### Set Up Your Development Environment

Before you begin, make sure you have a development environment set up for Moodle plugin development. You'll need a Moodle installation, a code editor, and PHP development tools.

### Create the Plugin Directory

Inside the blocks directory of your Moodle installation, create a new directory for your custom block plugin. Name it, for example, hello_username.

Inside the hello_username directory, create a version.php file to define plugin metadata:

```
<?php
$plugin->version = 2023111600; // The current version of your plugin.
$plugin->requires = 2019052000; // The minimum Moodle version required.
$plugin->component = 'block_hello_username'; // The unique plugin identifier.
```

### Create the Block Files

Inside the hello_username directory, create a db directory and a blocks.php file:

```
<?php
$plugin->version = 2023111600;
$plugin->requires = 2019052000;
$plugin->component = 'block_hello_username';

defined('MOODLE_INTERNAL') || die();

$plugin->cron = 0; // Disable cron for this block.
```

Inside the db directory, create a install.php file to define the database tables and settings:

```
<?php
function xmldb_block_hello_username_install() {
    // No database changes required for this block.
}
```

Now, create the main block PHP file, block_hello_username.php, inside the hello_username directory:

```
<?php
class block_hello_username extends block_base {
    public function init() {
        $this->title = get_string('pluginname', 'block_hello_username');
    }

    public function get_content() {
        if ($this->content !== null) {
            return $this->content;
        }

        $this->content = new stdClass();
        $this->content->text = 'Hello ' . fullname($USER);
        $this->content->footer = '';

        return $this->content;
    }
}
```

### Define Language Strings

Inside the hello_username directory, create a lang directory.

Inside the lang directory, create a language file (e.g., en/block_hello_username.php) with the following content:

```
<?php
$string['pluginname'] = 'Hello Username'; // Your block name.
```

### Install and Enable the Plugin

Log in to your Moodle site as an administrator.

Go to "Site administration" > "Notifications" to install and upgrade your plugin.

### Add the Block to a Course

Navigate to a course where you want to add the "Hello Username" block.

Turn editing on.

In the "Add a block" section, select "Hello Username" from the list of available blocks.

The "Hello Username" block should now appear on your course page, displaying the "Hello" message followed by the username of the logged-in user.

## Backup and Restore

- Backup Courses: Regularly back up course content and settings to prevent data loss.
- Restore Courses: Restore courses from backup files when needed.

## Security and Privacy

- User Authentication: Configure authentication methods like LDAP, CAS, or email-based self-registration.
- Data Protection: Comply with data protection regulations by setting privacy options and policies.

## Troubleshooting

- Logs: Check logs for errors and troubleshooting information.
- Community Support: Seek help and advice from the Moodle community and forums.
