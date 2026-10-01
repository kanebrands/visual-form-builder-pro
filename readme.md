# Visual Form Builder Pro PHP Modernization

This repository contains a modernization pass for the legacy Visual Form Builder Pro WordPress plugin. The intent of this project is to keep the original plugin behavior intact while updating the PHP code so it can run cleanly on modern PHP versions, with PHP 8.3 as the minimum supported runtime.

The current work focuses on compatibility fixes: reducing PHP warnings, notices, deprecations, and fatal errors caused by older PHP idioms while avoiding broad rewrites of the plugin architecture.

## Original Plugin Credit

Visual Form Builder Pro was originally authored by Matthew Muro. The original plugin site is available at [https://vfbpro.com](https://vfbpro.com).

## Requirements

- PHP 8.3 or newer.
- WordPress installed and configured.
- A database supported by the target WordPress version.
- A web server capable of running WordPress plugins, such as Apache, nginx with PHP-FPM, or a comparable local development server.
- WordPress administrative access to install, activate, and configure the plugin.
- File permissions that allow WordPress to load plugin PHP files and plugin assets.

## WordPress Compatibility Notes

This codebase is a legacy WordPress plugin and still depends on WordPress APIs and conventions, including:

- WordPress plugin loading through `visual-form-builder-pro.php`.
- WordPress database access through `$wpdb`.
- WordPress admin screens, AJAX hooks, shortcodes, widgets, and capabilities.
- WordPress helper functions such as `maybe_unserialize()`, `is_serialized()`, `wp_mail()`, `wp_die()`, `esc_html()`, and related sanitization helpers.

Because of those dependencies, the plugin should be tested inside a real WordPress installation rather than executed as standalone PHP.

## Optional Runtime Features

Some plugin features depend on site configuration or external services:

- Email delivery requires a working WordPress mail configuration.
- Legacy reCAPTCHA support requires configured reCAPTCHA keys in the plugin settings.
- Akismet spam checks require Akismet to be installed and active.
- PHP sessions are optional and controlled by the existing `VFB_USE_PHP_SESSIONS` constant. The default database-backed session behavior is still supported.

## Validation

The PHP files in this repository were checked with PHP 8.3.35 using `php -l`. The lint pass completed without syntax errors or PHP 8.3 lint-time deprecation output.

Functional testing should still be performed in WordPress for the major plugin flows:

- Creating and editing forms.
- Rendering forms on the front end.
- Submitting forms.
- Sending notification emails.
- Viewing and editing entries.
- Exporting entries.
- Using conditional field rules and email rules.
- Testing any enabled CAPTCHA, Akismet, PayPal, or add-on integrations.

## Project Scope

This project is not a feature rewrite. The compatibility pass intentionally keeps the original structure and behavior wherever possible. Changes should remain narrowly focused on modern PHP compatibility, runtime stability, and WordPress-safe handling of legacy saved data.
