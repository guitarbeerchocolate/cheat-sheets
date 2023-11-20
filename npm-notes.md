# NPM (Node Package Manager) Cheat Sheet

## Introduction to NPM

What is NPM? NPM is the default package manager for Node.js, used to install, manage, and distribute JavaScript packages and libraries.

Key Features:

- Access to a vast ecosystem of open-source packages.
- Dependency management for Node.js projects.
- Command-line interface for package management.

## NPM Commands

Initialize a New Project: Create a package.json file to manage project dependencies.

```
npm init
```

Install a Package Locally: Install a package and add it as a project dependency.

```
npm install package-name
```

Install a Package Globally: Install a package globally to make it accessible in your command line.

```
npm install -g package-name
```

Install a Package as a Development Dependency: Install a package for development purposes only.

```
npm install --save-dev package-name
```

Update All Dependencies: Update all packages listed in package.json to their latest versions.

```
npm update
```

Install Packages from package.json: Install all project dependencies listed in package.json.

```
npm install
```

Uninstall a Package: Remove a package from your project.

```
npm uninstall package-name
```

Search for Packages: Search the npm registry for packages.

```
npm search package-name
```

View Package Information: Display detailed information about a package.

```
npm info package-name
```

List Installed Packages: List all installed packages in your project.

```
npm ls
```

Run Scripts Defined in package.json: Execute custom scripts defined in the scripts section of package.json.

```
npm run script-name
```

Publish a Package: Publish your own package to the npm registry.

```
npm publish
```

Authenticate with a Registry: Log in to a specific npm registry.

```
npm login
```

Logout: Log out from the current npm registry.

```
npm logout
```

## package.json File

The package.json file is used to manage project metadata and dependencies.

To create or update package.json, run npm init and follow the prompts.

Dependencies and devDependencies are listed in the dependencies and devDependencies sections, respectively.

```
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "My Node.js project",
  "dependencies": {
    "express": "^4.17.1",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "eslint": "^7.32.0",
    "mocha": "^9.1.1"
  },
  "scripts": {
    "start": "node index.js",
    "test": "mocha"
  },
  "author": "Your Name",
  "license": "MIT"
}
```

## NPM Registry

The default NPM registry is https://registry.npmjs.org.

You can configure NPM to use custom registries if needed.
