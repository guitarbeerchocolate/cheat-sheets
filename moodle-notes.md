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

  - **User Journey:** An administrator logs in, goes to the "Site administration" section, and creates a new course by providing course details, such as course name, description, and enrollment methods.

- Enroll Students: Add students to a course by using enrollment methods like manual enrollment, self-enrollment, or LDAP enrollment.
  - **User Journey:** A teacher logs in, accesses the course, and enrolls students by specifying their usernames or using a self-enrollment method.

## Adding Content

- Resources: Add resources like files, folders, URLs, labels, and pages to your course.

  - **User Journey:** A teacher adds a PDF resource to the course module by uploading the file and providing a description for students to access.

- Activities: Include interactive activities like quizzes, assignments, forums, surveys, and more.
  - **User Journey:** A teacher creates a quiz activity with multiple-choice questions and sets the due date and grading options.

## Grading

- Gradebook: Use the Moodle gradebook to set up and manage grading for assignments, quizzes, and other assessments.

  - **User Journey:** A teacher accesses the gradebook, sets up categories, and assigns grades to students based on their quiz performance.

- Grading Scales: Define custom grading scales or use predefined scales.

  - **User Journey:** An administrator configures a custom grading scale for specific courses, such as "Excellent," "Good," "Satisfactory," etc.

- Rubrics: Create rubrics to assess and grade student work.
  - **User Journey:** A teacher creates a rubric for an assignment, specifying criteria and scoring levels for evaluation.

## Communication

- Forums: Create discussion forums for students to communicate and collaborate.

  - **User Journey:** A teacher creates a discussion forum within the course, and students can post and reply to discussions.

- Announcements: Post course announcements to inform students about important updates.

  - **User Journey:** A teacher posts an announcement on the course homepage to notify students of an upcoming assignment submission deadline.

- Messaging: Use the messaging system to send messages to students or other users.
  - **User Journey:** A student sends a private message to a classmate for clarification on an assignment.

## Quizzes and Assessments

- Create a Quiz: Build quizzes with various question types, including multiple-choice, true/false, short answer, and essay questions.

  - **User Journey:** A teacher creates a quiz with multiple-choice questions, defines time limits, and sets quiz availability.

- Randomize Questions: Randomly select questions from a question bank to create unique quizzes.

  - **User Journey:** A teacher configures the quiz to draw questions randomly from a question bank, ensuring each student gets a different set of questions.

- Grading Options: Choose different grading methods for quizzes, such as highest grade, average grade, or last attempt.
  - **User Journey:** A teacher selects "Highest grade" as the grading method for a quiz to consider only the highest score achieved by each student.

## Customization

- Themes: Customize the appearance of your Moodle site with themes or create custom themes.
  - **User Journey:** An administrator creates a custom theme with a unique color scheme and applies it to the Moodle site.
- Plugins: Extend Moodle's functionality by installing and configuring plugins.
  - **User Journey:** An administrator installs a plugin for integrating with an external learning resource, enhancing the platform's capabilities.

### Creating a basic moodle theme

#### Create a Custom CSS File

1. Create a custom CSS file (e.g., custom.css) where you will define the styles for your Moodle theme.

2. In your custom.css, define the colors and styles based on your color scheme.

   ```css
   /* Primary color for headings and links */
   h1,
   h2,
   h3,
   h4,
   h5,
   h6,
   a {
     color: #800080;
   }

   /* Secondary color for backgrounds and text */
   body {
     background-color: #ffffff;
     color: #333333;
   }

   /* Custom styles for buttons */
   button,
   .btn {
     background-color: #800080;
     color: #ffffff;
     border: none;
   }

   /* Additional custom styles for various Moodle elements */
   /* Add your styles here */
   ```

3. Upload Your Custom Theme

- **User Journey:** Log in to your Moodle site as an administrator.

  Navigate to "Site administration" > "Plugins" > "Themes" > "Theme selector."

  Under "Theme selector," click on "Upload a new theme."

  Upload the custom theme folder containing your custom.css and other theme files.

4. Configure Moodle to Use Your Custom Theme

- **User Journey:** After uploading the theme, you should see it listed in the theme selector.

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

- **User Journey:** Go to "Site administration" > "Notifications" to install and upgrade your plugin.

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
