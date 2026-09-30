---
name: drupal-auto-dev
author: Simon Hobbs
description: Multi-modal strategies for building a Drupal website, which ranges from using PHP/Drush, editing config files, computer use, and validating results. Assumes operator monitoring.
metadata:
  short-description: Drupal website building.
---

# Drupal website building

Use this skill when the operator is building Drupal functionality (may be working in tandem). At minimum needs access to the Drupal UI and, `./vendor/bin/drush`, and `git` can be accessed.

## Asking the operator

The following will stop progress.

- Need a new module or theme name
- Unclear project root
- Being on a feature branch that doesn't correlate with the current task
- Can't access drush
- Can't access website
- Can't access git
- Unresolveable git status

## Git management

Before and after each feature:

- Must be a git repo (alert operator if not)
- Be on `main`, `dev`, `develop`, `staging` or `agent` branch unless otherwise instructed
- `git status` should be clean. Commit changes as needed.
- Drush config import/export should be clean.
- phpunit and phpcs should be clean.
- Run `git fetch` (or `git pull --rebase` in case of upstream changes) and `git push`
- Never create a feature branch.
- Never work on more than one feature at a time.

## Upstream code

Never edit files referenced in .gitingore, eg:

- vendor
- web/core
- web/libraries
- modules/contrib
- themes/contrib
- node_modules

## Hosting

If the site has an sqlite connection, assume it can be started with `./vendor/bin/drush runserver` or `./vendor/bin/dr server`.

If there is a mariadb/mysql database connection and no instruction to run ddev or similar, the plan is to run a local version of the site with just php and SQLite. If necessary, add a sites/default/agents.settings.php (include it from settings.php by detecting an env variable or host) and setup sqlite to live in ./site/default/database/. Install the site, then if there is existing config, updated the UUID as needed, and import the existing config.

Whenever installing, always make these files writable if not already:
```
web/sites/default/settings.php: Permission denied
web/sites/default/default.settings.php: Permission denied
web/sites/default/files: Permission denied
web/sites/default/default.services.yml: Permission denied
```

Run the server locally using the default 8888. If the port is taken, verify if you can access the site already because it is running (the operator maybe running it), try using computer use to do so.

Alert the operator what is happening through this process.

## PHP and debugging

- Add full doxygen (pass phpcs)
- Do not put inline comments.
- Inspect logs with watchdog, drush

## Testing

Only test code which being changed.

- vendor/bin/phpunit
- vendor/bin/phpcs

Monitor logs with drush

## Javascript

Use modern DOM APIs like querySelector, addEventListener, fetch, etc.

Never add jQuery as a dependency or use jQuery in any form. Use vanilla JavaScript or modern web APIs instead. This includes:
* Never importing jQuery via CDN, npm, or composer
* Never using $ or jQuery() functions
* Never suggesting jQuery-based solutions

## PHP and debugging strategy

When writing code or debugging Drupal errors, create php scripts in .scripts/agent/ and execute them with `drush php:script .scripts/agent/foobar.php` to actually test content, entities, the functionality of classes, just like setup() might occur in a phpunit test.

To understand how to instantiate and use services and classes: read the phpunit static/functional tests, read all the files named *.api.php, service.yml's and class constructors.
