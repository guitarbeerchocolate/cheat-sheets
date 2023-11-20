# Craft CMS Cheat Sheet

## Installation and Setup

### Install Craft CMS

1. Download Craft CMS from [craftcms.com](https://craftcms.com/).
2. Extract the downloaded archive to your web server directory.
3. Access the Craft CMS setup via a web browser and follow the installation steps.

### Configuration

- Customize your configuration settings in the `config/` directory, such as `general.php` and `db.php`.

## Craft CMS Control Panel

### Access the Control Panel

- Access the Craft CMS control panel by appending `/admin` to your site's URL (e.g., `https://yourwebsite.com/admin`).

### Dashboard

- The dashboard provides an overview of your site's recent activity and statistics.

### Sections

- Create and manage sections to organize content.
- Define entry types, categories, and tags for each section.

### Entries

- Create, edit, and manage content entries.
- Assign entry types, categories, tags, and custom fields.

### Categories and Tags

- Organize content with categories and tags.
- Create and manage category groups and tag groups.

### Users

- Manage user accounts and permissions.
- Create user groups and assign permissions.

### Assets

- Upload, organize, and manage files and images.
- Use the Asset Indexes to control asset URLs.

### Settings

- Configure site settings, routes, and plugins.
- Set up SEO settings and email settings.

## Templating

### Twig Templates

- Craft CMS uses Twig templating engine for creating templates.
- Templates are located in the `templates/` directory.

### Variables

- Access Craft CMS content and data using template variables.
- Example: `{{ entry.title }}` displays the title of an entry.

### Loops

- Iterate through entries, categories, and other data using `for` loops.

### Conditionals

- Use `if` statements to conditionally display content.
- Example: `{% if entry.author == currentUser %} You are the author {% endif %}`

### Includes

- Include partial templates using `{% include 'template-name' %}`.

### Macros

- Define and use reusable macros within templates.

## Plugins

### Install Plugins

- Install plugins from the Craft CMS Plugin Store or manually by uploading the plugin files.

### Plugin Settings

- Configure plugin settings in the Craft CMS control panel under "Settings."

### Twig Extensions

- Some plugins provide additional Twig extensions and functions for templates.

## Updating Craft CMS

### Update Craft CMS

- Before updating, backup your database and files.
- Update Craft CMS from the control panel or using Composer.

### Plugin Updates

- Check for updates to your installed plugins and update them as needed.

## Security

### Craft CMS Security

- Keep Craft CMS, plugins, and server software up to date.
- Use strong passwords and enable two-factor authentication for users.

### Permissions

- Assign appropriate permissions to users and groups.
- Limit access to the control panel for necessary users only.

### Protect Files and Directories

- Protect sensitive files and directories, including `config/`, `storage/`, and `templates/`.

## Craft CMS CLI

### Craft CLI

- Craft CLI provides various commands for managing Craft CMS via the command line.
- Examples:
  - `./craft migrate/all`: Run database migrations.
  - `./craft clear-caches/all`: Clear caches.

## Debugging

### Debug Toolbar

- Enable the debug toolbar in `config/general.php` for debugging information in the control panel.

### Debugging in Templates

- Use `{% dump %}` to output debug information in templates.

## Useful Resources

- [Craft CMS Documentation](https://craftcms.com/docs): Official documentation for Craft CMS.
- [Craft CMS Stack Exchange](https://craftcms.stackexchange.com/): Community-driven Q&A for Craft CMS.
- [Craft Plugin Store](https://plugins.craftcms.com/): Official repository for Craft CMS plugins.

This Craft CMS cheat sheet provides essential commands, settings, and tips for managing and developing websites with Craft CMS.
