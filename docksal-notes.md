# Docksal Cheat Sheet

## Installation

Use Docksal's Installation Guide at https://docs.docksal.io/getting-started/setup/

## Getting Started

Initialize a Project: Navigate to your project folder and run the following command to initialize Docksal for your project:

```
fin init
```

Start the Stack: Start the Docksal stack with:

```
fin start
```

Access Project: Visit your project at http://projectname.docksal.

## Docksal CLI

List Available Commands: List all available Docksal commands:

```
fin
```

Version: Check Docksal version:

```
fin version
```

Stop the Stack: Stop the Docksal stack:

```
fin stop
```

## Services Management

List Services: List all running services:

```
fin ps
```

Start/Stop Service: Start or stop a specific service:

```
fin start <service>
fin stop <service>
```

Restart Service: Restart a specific service:

```
fin restart <service>
```

## Project Configuration

Configure Project: Edit .docksal/docksal.env to configure your project settings.

Customize Services: Customize services by editing .docksal/docksal.yml.

## Database Management

Access Database: Access the database using:

```
fin db
```

Database Import/Export: Import or export a database dump:

```
fin db import <file.sql>
fin db export <file.sql>
```

## Site Configuration

Customize Apache/Nginx: Customize webserver settings by editing .docksal/etc/nginx or .docksal/etc/apache.

Configure Hosts: Add domain aliases by editing /etc/hosts on your host machine.

## Project Cleanup

Remove Project: To remove a project, use:

```
fin project remove
```

Remove Docksal: To uninstall Docksal, refer to the uninstallation guide at https://docs.docksal.io/getting-started/setup/#uninstall
