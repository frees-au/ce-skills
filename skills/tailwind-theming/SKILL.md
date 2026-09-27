---
name: tailwind-theming
author: Si Hobbs
description: Build or adjust custom themes using Tailwind CSS 4 while respecting existing theme structure, asset libraries, and project-specific theming boundaries. Includes stubs for Shopify and Drupal.
metadata:
  short-description: Tailwind 4 theming best practice
---

# Tailwind Theming

Use this skill when the user asks for a new Drupal theme with Tailwind integration, ideally Tailwind 4 on a new Drupal or Shopify theme, or the Drupal theme in the project has Tailwind integration.

## Do not apply skill when

There are circumstances where this skill may not be appropriate, check with operator:

- Project is not a Drupal or Shopify project (although it applies equally well to other frameworks).
- target theme has an upstream, eg Drupal.org, "Are you we sure you want to modifying this theme and diverge from the upstream theme?"
- target theme has existing CSS tooling: "You're already using Bootstrap|SASS, are you should you want to combine this with Tailwind?"

## Philosophy being applied

There may be a conversation with the operator about this skill and how it fits into other skills and strategies.

Tailwind is a popular choice of theme and this skill is not a full Tailwind skill, but is intended to augment the skill or strategy employed by the project.

Over time and versions, different patterns emerge and recede. This skill (more specificialy  the stub themes in the stubs folder) provide a harness for how you will see Tailwind configured. In many cases no reference is made to a specific configuration strategy where there is no opinion.

Pixel-perfection is not a goal of this skill, and should be addressed with the operator.

## Anti-patterns

### Separating style and markup

Tailwind provides a means of co-locating style and markup and can make projects easy to maintain for this reason when there is already and established pattern of re-usable templates (eg Drupal and Shopify).

The anti-pattern that LLMs should avoid is reusable classes, where the class is defined in CSS and used in the HTML. When there is a tendency to reuse a class:

- Can Tailwind classes be applied cleanly inline?
- Is there an opportunity to abstract the templates to avoid repetition of the styles?
- Can a custom tag be used? Is there reference to TAC (Tag, Attribute, Class) methodology in this project or available skills?

### Using arbitrary tailwind classes

Custom classes like `lg:top-[344px]` are a code smell, they add cognitive load and open LLM to do more of this type of style. This guidance might conflict with "pixel-perfect" HTML styling.

- Is this an opportunity to create a variable (eg. in the case of color)?
- Is there a custom spacing/margin/padding/sizing increment that can be applied in the @theme config?
- What happens if a standard class is used? Does the pixel difference actually matter to the person observing?

## References

- `stubs/drupal-theme`
- `stubs/shopify-theme`
