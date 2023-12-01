# Composer Cheat Sheet

## Introduction

Composer is a dependency management tool for PHP. It simplifies the process of managing and autoloading PHP packages and libraries.

## Installation

To install Composer globally:

```
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

## Basic Usage

```
composer init: Initialize a new Composer project.
composer require package-name: Install a package.
composer install: Install project dependencies based on composer.json.
composer update: Update all or specific packages.
composer remove package-name: Remove a package.
```

## composer.json

The composer.json file defines project dependencies and settings.

```
{
    "require": {
        "vendor/package": "1.0.0"
    }
}
```

## Autoloading

Composer provides autoloading for your project's classes.

```
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

## Composer Commands

```
composer dump-autoload: Regenerate the autoloader.
composer show: Show information about installed packages.
composer licenses: Show licensing information for packages.
composer validate: Validate composer.json and composer.lock files.
composer self-update: Update Composer to the latest version.
```

## Scripts

Define custom scripts in composer.json for automation.

Example:

```
{
    "scripts": {
        "test": "phpunit"
    }
}
```

Run custom scripts with composer run script-name.

## Version Constraints

^1.0.0: Allows updates to the most recent minor version (1.0.x).

~1.0.0: Allows updates to the most recent patch version (1.0.0).

> =1.0.0 <2.0.0: Specifies a range of acceptable versions.

1.0.0|2.0.0: Allows either version 1.0.0 or 2.0.0.

## Packagist

Packagist (https://packagist.org/) is the default package repository for Composer.

## Lock File

Composer generates a composer.lock file to lock dependencies to specific versions.

## Composer Global

Use composer global require package-name to install packages globally.
Ensure the Composer global bin directory (~/.composer/vendor/bin) is in your system's PATH.

## Troubleshooting

Use composer diagnose to check common issues.
Clear the Composer cache with composer clear-cache.
Check PHP version compatibility with your dependencies.
This Composer cheat sheet provides essential commands and tips for managing PHP dependencies and packages in your projects.
