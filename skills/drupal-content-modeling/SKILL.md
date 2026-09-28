---
name: drupal-site-building
author: Simon Hobbs
description: Analyze and change Drupal content models using config/sync, entity displays, field storage, permissions, and migrations with a semantic approach to naming and using the Drupal config as the source of truth.
metadata:
  short-description: Drupal content modeling
---

# Drupal Content Modeling

Use this skill when a Drupal task involves content types, fields, paragraphs, media, taxonomy, entity references, form displays, view displays, permissions, generated content, or config-driven site structure.

## Discovery

- Inspect `config/sync` first. Field labels, descriptions, required flags, storage types, target bundles, widget settings, formatter settings, and dependencies are often more reliable than rendered UI.
- Map the content model from the config objects before editing:
  - `node.type.*`
  - `field.storage.*`
  - `field.field.*`
  - `core.entity_form_display.*`
  - `core.entity_view_display.*`
  - `taxonomy.vocabulary.*`
  - `media.type.*`
  - `paragraphs.paragraphs_type.*`
  - `user.role.*`
- Cross-check code consumers of fields before renaming or deleting anything. Search for machine names in custom modules, themes, migrations, tests, and seed/generator commands.

## Change Strategy

- Preserve machine names unless the user explicitly asks to rename them.
- Prefer small, reversible model changes. Avoid broad config rewrites when the task only needs a field, display, or permission adjustment.
- If the repo has a Drupal runtime available, prefer generating or exporting config through `drush` or `dr`, then review the YAML diff.
- If config is edited directly, validate with the project's config status/import workflow before claiming it is ready.
- When beginning work, config should be Validatable (see ## Validation).
- Assume the operator (eg the human) will make changes through the UI, so will need clear messaging about when config is valid and committed to the repo.

## Field Decisions

- Choose field types for editorial behavior, querying needs, and future migrations, not only for the current display.
- Use entity reference fields when the referenced item has independent lifecycle, permissions, reuse, or reporting value.
- Use paragraphs or layout components when editors need ordered, repeatable structured sections.
- Keep computed or integration-only values out of editorial fields unless editors need to see or override them.

## Semantic naming and re-use

When creating a new entity type or field, follow these guidelines:

- Do not prefix the field with `field_` or any other prefix.
- Avoid underscores in field or entity machine names.
- The field may already exist (eg. `summary`, so prefer to reuse it.
- Request clarification for possible re-use of a field.
- Refer to [references/sample-model.md](references/sample-model.md).

## Validation

Config is considered valid when:

- Config import and export is idempotent
- git workspace is clean (especially in the /config directory)
