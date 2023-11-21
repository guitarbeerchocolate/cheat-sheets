# Yii Framework Cheat Sheet

## Introduction to Yii

- **What is Yii?** Yii is a high-performance, component-based PHP framework for building web applications. It follows the Model-View-Controller (MVC) architecture.

## Yii Basics

- **Installation:** Install Yii using Composer or download the Yii application template.

- **Configuration:** Configure the application in the `config` directory.

- **Command-Line Tools:** Use Yii console commands for tasks like migrations and code generation.

## MVC Architecture

- **Model:** Represents the data and business logic.

- **View:** Displays data and handles user interface.

- **Controller:** Handles user requests, processes input, and interacts with models and views.

## Yii Components

- **Widgets:** Reusable UI elements like grids, forms, and menus.

- **Validators:** Validate user input and model attributes.

- **Data Providers:** Provide data to widgets and views.

- **Extensions:** Extend Yii functionality with third-party libraries.

## Routing

- **URL Rules:** Define custom URL rules for routing.

- **Pretty URLs:** Configure clean and user-friendly URLs.

## Database Access

- **Active Record:** Yii's implementation of the Active Record pattern for database access.

- **Database Migrations:** Manage database schema changes.

- **Query Builder:** Build database queries programmatically.

## Authentication and Authorization

- **User:** Implement user authentication and authorization.

- **RBAC:** Role-Based Access Control for fine-grained permissions.

## Forms and Validation

- **Form Models:** Create form models for handling user input.

- **Form Widgets:** Use widgets for form elements.

- **Validation Rules:** Define validation rules for model attributes.

## Caching

- **Data Caching:** Cache data to improve application performance.

- **Fragment Caching:** Cache parts of views.

## Error Handling

- **Error Pages:** Customize error pages for different HTTP status codes.

- **Logging:** Configure application logging.

## Internationalization (i18n)

- **Translations:** Translate application messages and content.

- **Localization:** Format numbers, dates, and times for different locales.

## Yii2 Advanced Template

- **Frontend and Backend:** Divide your application into frontend and backend modules.

- **API:** Build RESTful APIs with the provided template.

- **User Management:** Includes user registration and management.

## Security Best Practices

- **Cross-Site Scripting (XSS) Prevention:** Use the `Html::encode()` method.

- **Cross-Site Request Forgery (CSRF) Protection:** Enable CSRF tokens.

- **SQL Injection Prevention:** Use parameterized queries and Active Record.

## Yii Resources

- [Yii Framework Official Website](https://www.yiiframework.com/): Official documentation and resources.

- [Yii2 Documentation](https://www.yiiframework.com/doc/guide/2.0/en): Comprehensive documentation for Yii2.

- [Yii2 Extensions](https://www.yiiframework.com/extensions): A collection of Yii2 extensions.

## When to use:

### Modules

Shared Functionality: If you have a set of features that need to be shared among different parts of your application, such as authentication, user management, or API integration, creating a Yii2 module can help centralize and standardize that functionality. This ensures consistent implementation across different sections of your application.

Independent Development and Maintenance: Yii2 modules allow multiple developers to work on different parts of an application independently. Each module can have its own directory structure, models, controllers, and views, making it easier to manage the development process. This also allows for easier maintenance and updates as changes within a module won't affect other parts of the application.

Third-Party Integration: If you need to integrate external libraries, plugins, or components into your Yii2 application, creating a module can provide a clean and organized way to incorporate and manage those integrations. By encapsulating the integration logic within a module, you can easily enable or disable the functionality without affecting the rest of your application.

### Filters

Authorization and Access Control: If you need to enforce access control rules or perform authorization checks before executing controller actions, creating a Yii2 filter can be beneficial. Filters can intercept requests, check user permissions, and deny access if necessary. This helps ensure that only authorized users can access specific actions or resources.

Input Validation and Sanitization: If you want to validate and sanitize user input before it reaches the controller actions, filters can be used to intercept the request and perform validation checks. For example, you can create a filter to check if the submitted form data is valid or if certain parameters meet specific criteria. This helps ensure that the input is clean and valid, reducing the risk of security vulnerabilities or errors.

Logging and Auditing: If you need to log or audit certain actions or events within your application, creating a Yii2 filter can be useful. Filters allow you to intercept requests or responses and log relevant information, such as user actions, timestamp, IP address, or any other custom data you want to track. This helps in debugging, monitoring, and maintaining the application.

Response Modification: If you need to modify the response before it is sent back to the client, filters provide a convenient way to intercept the response and make necessary changes. For example, you can create a filter to compress the response, add headers, or modify the content of the response based on certain conditions. This allows you to customize the response behavior without modifying the controller action itself.

Caching: If you want to implement caching for specific controller actions, creating a Yii2 filter can simplify the caching process. Filters can intercept requests and check if the response is already cached. If so, the filter can return the cached response without executing the controller action. This helps improve performance and reduce the load on the server.

### Widgets

Reusability: If you have a UI component that is used across multiple views or pages within your application, creating a Yii2 widget can help encapsulate and reuse that component. Widgets allow you to define the rendering logic, configuration options, and any associated behavior in a self-contained and reusable package.

Complex UI Elements: If you need to render complex UI elements, such as calendars, charts, grids, or file uploaders, creating a Yii2 widget can simplify the implementation and provide a clean interface for using those elements. Widgets abstract the complexity of the underlying HTML, CSS, and JavaScript code, making it easier to integrate and customize such elements in your views.

Encapsulation of Logic: If you have a piece of code that involves both backend and frontend logic, creating a Yii2 widget can help encapsulate that logic. Widgets allow you to define both the server-side and client-side code in a single component. This improves code organization, maintainability, and reusability.

Customization and Configuration: If you want to provide a configurable UI component that can be customized in various ways, creating a Yii2 widget is a suitable approach. Widgets can expose configuration options that allow developers to customize the behavior, appearance, or data source of the component. This provides flexibility without the need for duplicating code or modifying the widget implementation directly.

Promoting Consistency: If you want to ensure consistency in the UI elements across your application, creating Yii2 widgets can help enforce a unified style and behavior. By centralizing the rendering and logic of common UI components into widgets, you can ensure that they are consistently used and maintained throughout your application.
