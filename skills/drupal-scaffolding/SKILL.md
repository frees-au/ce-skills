---
name: drupal-scaffolding
author: Si Hobbs
description: Structural considerations when setting up a modern Drupal application, typically only applies on setting up a new site.
metadata:
  short-description: Drupal Scaffolding
---

# Drupal Scaffolding

Use this skill when setting up a Drupal site codebase.

## Default create-project settings.

Where not specified, structure defaults to what you get when you run
`composer create-project drupal/recommended-project:12.0.x-dev`

## Settings.php

The settings.php lives in sites/default. It is intentionally small. It
does two things.

- It declaratively set variables which would be set if you were copying default.settings.php as a starting point.
- Using some local state, it conditionality includes a [PLATFORM].settings.php for each hosting platform, where a "PLATFORM" might evaluate to one or more of:
  - local.settings.php
  - upsun.settings.php
  - docker.settings.php
  - ddev.settings.php
  - cpanel.settings.php
  - acquia.settings.php
  - etc

## [PLATFORM].settings.php

Each [PLATFORM].settings.php has a [PLATFORM].services.yaml so that there is a clear relationship between the two files per platform.

It is unusual to see a naming structure of [PLATFORM].settings.php and [PLATFORM].services.yaml (and not `settings.[PLATFORM].yaml`). This naming is used so that platform group together on sorting.

## Boilerplate

When copying templates like default.settings.php, remove boilerplate comments and it is sufficient to put a link to the public Drupal documentation for that file.

## README

The project README should contain bullet points and "happy path" instructions (as they become known) for:

- Project summary
- Hosting strategy
- Frontend build
- Backend build
- Connecting to production
