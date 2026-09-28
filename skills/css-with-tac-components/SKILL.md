---
name: css-with-tac-components
author: Brynn Briedis & Simon Hobbs
description: Apply a "TAC" (Tag, Attribute, Class) strategy to create clean semantic html components like `<fs-badge variant="tertiary">` rather than excessive use of divs, spans and classes, and some accessibility and other sugar on top.
metadata:
  short-description: CSS with TAC components technique for web projects
---

# Goals

The goals are:
- highly readable and semantic markup
- the emergence of components like `<fs-badge>` or `<fs-photo-grid>`
- minimal divs and spans
- minimal javascript
- accessibility

## Project decisions/discovery

The project's README.md, especially regarding the styleguide, should resolve the following questions. Answer the questions and update the README, if not already.

1. What is the prefix? (Free Sauce projects default to `fs-`).
2. Should we use `<fs-button variant="cta">` or `<button data-variant="cta">`? (Since `<button variant="cta">` is invalid.)
3. If Tailwind, should the project use native CSS in `@theme` or `@layer components` when it comes to custom elements.

## Examples

Instead of obscuring components behind classes and boilerplate:

```html
<button class="primary btn">
<div class="photo-grid" data-columns="4">
<div class="badge alert">
<div id="faq-list" class="foo-bar accordion baz" data-state="expanded">
```

Use clean HTML like this. Note that data attributes and cu 

```html
<button data-variant="primary"> or <fs-button variant="primary">
<fs-photo-grid columns="4">
<fs-badge variant="alert">
<fs-accordion state="expanded">
```

## Style

Data attributes and custom attributes can be styled.

```css
fs-photo-grid[columns="4"] {
  grid-template-columns: repeat(4, 1fr);
}
```

Custom attributes vs data- attributes are styled similarly.

```css
/* <fs-button variant="alert"> */
fs-button[variant="alert"] {
  background-color: red;
}

/* <button data-variant="alert"> */
button[data-variant="alert"] {
  background-color: red;
}
```

## Application

### Deciding on custom tags/elements

Style the element by its HTML tag before doing anything else.

```css
button { ... }
details { ... }

fs-alert { ... }
fs-card { ... }
```

- Prefer native HTML tags wherever they fit: `button`, `details`, `summary`, `dialog`, `nav`, `main`, `section`, `article`, `form`, `table`, headings, lists, and text elements.
- Custom tags must use the decided namespace prefix (eg `fs-`).
- The tag name should be a clear noun that describes the component: `fs-alert`, `fs-card`, `fs-badge`, `fs-panel`.
- Structural children may also use custom elements when they clarify markup: `fs-card-title`, `fs-shell-sidebar`, `fs-brand-mark`.
- Do not create subtype tags for component variations. Use the base component tag with a `variant` attribute instead: `<fs-card variant="login">`, not `<fs-login-card>` or `<fs-card-login>`.
- Never use `div` or `span` as the public component identity when a native tag or `ac-` custom tag would be clearer.
- Every custom tag must either wrap native semantics or declare the needed `role` and `aria-*` attributes in markup.

### Deciding on variants

Use HTML attributes to define variants, states, and customization.

```html
<button data-variant="primary">
<details data-open>
<fs-card variant="login">
<fs-badge status="ready">
<fs-panel emphasis="alert">
```

```css
button[data-variant="primary"] { ... }
details[data-open] summary::after { ... }
fs-card[variant="login"] { ... }
fs-badge[status="ready"] { ... }
fs-panel[emphasis="alert"] { ... }
```

- Use attributes for variants and states, not extra classes.
- A component subtype is a `variant` on the base tag. For example, use `<fs-panel variant="settings">`, `<fs-grid variant="color">`, or `<fs-card variant="login">` instead of inventing `fs-settings-panel`, `fs-color-grid`, or `fs-login-card`.
- Prefer existing HTML attributes: `disabled`, `hidden`, `open`, `type`, `aria-current`, `aria-invalid`.
- Use boolean attributes for simple on/off states.
- Use lowercase, hyphenated value attributes for named variants: `status="ready"`, `surface="hard"`, `layout="split"`.
- Attribute-based variants are the component API. Keep them stable and intentional.
- If a state is not native, pair the visual attribute with an ARIA state.

## Deciding on classes

Classes are the escape hatch, not the styling mechanism.

- Never use a class to create a component: use a native tag or `fs-` tag.
- Never use a class for a component variant: use an attribute.
- Never use a class for spacing, layout, colors, or typography.

## Design tokens

All style-guide values must be CSS custom properties prefixed with the project prefix (eg `--fs-`).

Global tokens live in `src/app.css` on `:root`.

```css
:root {
  --fs-color-carrot: #f4f1ea;
  --fs-color-carrot-rotton: #fffdf7;

  --fs-font-sans: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  --fs-font-mono: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;

  --fs-duration-fast: 150ms;
  --fs-duration: 260ms;
  --fs-duration-slow: 500ms;
  --fs-ease: ease-out;
}
```

Component-scoped tokens are declared on the component tag and named `--fs-[component]-[property]`.

```css
fs-badge {
  --fs-badge-background: var(--fs-color-steel);
  --fs-badge-color: var(--fs-color-paper);
  --fs-badge-border-color: var(--fs-color-line);

  background: var(--fs-badge-background);
  color: var(--fs-badge-color);
  border: var(--fs-badge-border-width) solid var(--fs-badge-border-color);
}

fs-badge[status="ready"] {
  --fs-badge-background: var(--fs-color-carrot);
}
```

- Never hard-code a design value in a component when a token exists.
- Global tokens use `--fs-[category]-[variant]`: `--fs-color-red`, `--fs-font-sans`.
- Component tokens use `--fs-[component]-[property]`: `--fs-badge-background`.
- Component tokens should reference global tokens.
- Do not redeclare global tokens on component tags. Define component-scoped tokens containing the element name that consume the global tokens.
- Durations, focus rings, borders, spacing, and typography are design values too.


### JavaScript Behavior

Start with native behavior and CSS.

- Use native controls first: `button`, `details`, `summary`, `dialog`, inputs, selects, and forms.
- JavaScript should enhance behavior, not replace styling logic.
- Toggle attributes and let CSS respond.
- Do not write inline styles for component state.
- Do not use JavaScript to recreate platform behavior that already exists.

### File And Scope Organization

The file `src/app.css` is the style-guide entry point. Recommended structure inside `src/app.css`:

```css
@layer reset, base, components, pages;

@layer reset {
  * { box-sizing: border-box; }
}

@layer base {
  :root { ... }
  body { ... }
  button { ... }
  details { ... }
}

@layer components {
  fs-panel { ... }
  fs-badge { ... }
  fs-shell { ... }
}
```

- Base styles for native HTML elements belong in the `base` layer.
- Shared custom tags belong in the `components` layer.

### Naming Conventions

| Thing | Convention | Example |
| --- | --- | --- |
| Custom tag | `fs-[noun]` | `fs-alert`, `fs-card`, `fs-badge` |
| Structural child tag | `fs-[component]-[part]` | `fs-card-title`, `fs-shell-sidebar` |
| Component subtype | base tag plus `variant` | `<fs-card variant="login">` |
| Boolean attribute | lowercase noun/adjective | `disabled`, `open`, `compact` |
| Value attribute | lowercase, hyphenated | `status="ready"`, `variant="primary"` |
| Global design token | `--fs-[category]-[variant]` | `--fs-color-red`, `--fs-font-sans` |
| Component token | `--fs-[component]-[property]` | `--fs-badge-background` |

## Exceptions

### Tailwind

- Do not use Tailwind classes inline in the markup for custom elements unless they are truly local.
- Do not add Tailwind to a project already using this skill, since it has questionable returns.
- It is ok to use CSS and `@apply` in the `@layer components` layer for custom elements. It should come after base styling.

### Svelte

- Page-specific styles may live in a Svelte `<style>` block when they are truly local.

## Accessibility

Tag-first markup supports accessibility because native elements bring keyboard behavior, roles, names, and platform conventions.

- Prefer native elements because they already carry semantics.
- A custom `fs-` tag must not hide semantics. Add `role` and `aria-*` where needed.
- A state attribute must either be native or paired with ARIA.
- Never signal state with color alone. Pair color with text, shape, or iconography.
- Focus styles come from shared `--fs-focus-*` tokens.
- Keyboard navigation must work without custom scripts.
- Do not use positive `tabindex`.
- Reading order should remain DOM order.

## Quick Reference Checklist

1. Is there a native HTML tag for this? Use it.
2. If no native tag fits, is the custom tag named with `fs-`?
3. Are variants and states attributes rather than classes?
4. Is state visible to assistive technology?
5. Are all style values using `--fs-` tokens?
7. Are selectors simple and tag-first?
8. Can the component be reached and operated by keyboard?
