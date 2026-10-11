# kawa-design

The kawa design system as plain CSS, shared by [kawa-studio](https://github.com/kawa-platform/kawa-studio) and
[kawa-docs](https://github.com/kawa-platform/kawa-docs) so both look like one product. No build step, no runtime.

## Theming

Dark is the default (`:root`) and `html[data-theme='dark']`; light is `html[data-theme='light']`. Set the attribute on
`<html>` to switch. Docusaurus uses the same attribute, so the docs switch with it.

## Fonts and icons

The tokens name Geist (headings and body), JetBrains Mono and the Phosphor duotone icons, but this package does not
load them: a remote `@import` only works at the very top of a stylesheet, which bundlers do not guarantee. Add them to
the page `<head>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600&family=JetBrains+Mono:wght@400;500;600&display=swap">
<link rel="stylesheet" href="https://unpkg.com/@phosphor-icons/web@2.1.1/src/duotone/style.css">
```

## Using it

Depend on a tagged release:

```json
"@kawa/design": "github:kawa-platform/kawa-design#v1.0.0"
```

```js
import '@kawa/design/index.css';     // everything (kawa-studio)
import '@kawa/design/tokens.css';    // tokens only, map them onto your own components (kawa-docs)
```

## Releasing

1. Change the CSS, bump `version` in `package.json`, commit.
2. Tag it: `git tag v1.1.0 && git push --tags`.
3. In each consumer, bump the `#v…` in its `package.json` and run `npm install`.

A token rename is a breaking change for consumers that reference the token directly (kawa-docs maps several onto
Docusaurus): release it as a new major version.
