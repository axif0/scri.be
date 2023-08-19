# Style Guidelines for scri.be

Thank you for following our style guide! The team asks that you familiarize yourself with this guide and follow it for any contributions. Doing so makes PRs and general code collaboration much more effective :)

We'll also link to this document in cases where these guidelines have not been followed. If that's what brought you here, no stress! Thanks for your interest and your drive to contribute to open-source and Scribe in particular! ❤️

If you have questions or would like to communicate with the team, please [join us in our public Matrix chat rooms](https://matrix.to/#/#scribe_community:matrix.org). We'd be happy to hear from you!

<a id="contents"></a>

## **Contents**

- [Vue and Nuxt](#vue-and-nuxt)
- [TypeScript](#typescript)
- [Tailwind](#tailwind)
- [Common styles](#common-styles)
- [Formatting](#formatting)
- [Colors](#colors)
- [Font](#font)
- [Text size](#text-size)
- [Tab size](#tab-size)
- [Icons](#icons)
- [Padding](#padding)

<a id="vue-and-nuxt"></a>

## Vue and Nuxt [`⇧`](#contents)

The frontend for Scribe is written in the framework [Vue.js](https://vuejs.org/) and specifically the meta-framework [Nuxt.js](https://nuxt.com/). The team chose Vue because of its broad usage across the development industry as well as relative ease of use and adoption for new contributors. Most of all we appreciate the structure that Vue adds to a project by leveraging the order of HTML and adding scripting and styling on top. Nuxt expands on Vue seamlessly and includes many [modules](https://nuxt.com/modules) to make development much easier.

Vue files (`.vue`) are Single-File Components that have `<template>`, `<script>` and `<style>` blocks. Conventions for writing Vue for Scribe include:

- `<template>` blocks should come first, `<script>` second and `<style>` last
- The Vue [Composition API](https://vuejs.org/guide/introduction.html#composition-api) should be used in all cases
- [TypeScript](https://www.typescriptlang.org/) should be used where ever possible within `<script>` blocks with `defineProps`
- Self-closing components (`<Component />`) should be used for any component that doesn't have content
  - This style is [strongly recommended in Vue](https://vuejs.org/guide/essentials/component-basics.html#dom-template-parsing-caveats)
  - Generally if a component has a `<slot>` then this would imply that it would normally have content and thus require a closing tag

<a id="typescript"></a>

## TypeScript [`⇧`](#contents)

PRs are always welcome to improve the developer experience and project infrastructure!

Currently `typescript.strict` and `typescript.typeCheck` in `nuxt.config.ts` are not enabled. This may change in the future. Strict type checks are not enabled to allow building the app outside `Docker`. Local and Netlify builds proceed despite TS errors with strict checks disabled.

> [!NOTE]\
> For VS Code users: it is recommended to install these extensions to enable in-editor type-checking:
>
> - [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
> - [Volar TS](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin)

### Vue Single File Component (.vue file) Guidelines

- Create general frontend types in the [frontend/types](https://github.com/scribe-org/scri.be/tree/main/frontend/types) directory
- When typing Arrays, use `arrayElementType[]` rather than the generic type `Array<T>` unless [extending](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#arrays):

```ts
const strArray: string[] = ["Thank", "you", "for", "contributing!"];
```

- Scribe uses the [Composition API](https://vuejs.org/guide/extras/composition-api-faq.html), so please implement `<script setup lang="ts">` and use `defineProps` with the generic type argument.

```typescript
const props = defineProps<{
  foo: string;
  bar?: number;
}>();
```

- Please also use `withDefault` when types require [default values](https://vuejs.org/guide/typescript/composition-api.html#props-default-values)

See [Vue and TypeScript docs](https://vuejs.org/guide/typescript/composition-api.html#typing-component-props) for more information about typing component props.

There is a limited set of package types that are available in the global scope. The current list can be found in `frontend/tsconfig.json` under `"compilerOptions.types"`, with this list being modified as the project matures.

Before opening a new PR, it is recommended to first generate the current types, then manually check those types:

1. cd into `frontend`
2. run `yarn run postinstall` to generate types in `frontend/.nuxt`
3. run `yarn nuxi typecheck`

Within VS Code TS errors are visible, however, running these commands will help to ensure the new code does not introduce unintended TS errors at build time. Existing TS errors may be ignored. PRs are always welcome to address these errors!

<a id="tailwind"></a>

## Tailwind [`⇧`](#contents)

Scribe uses [Tailwind CSS](https://tailwindcss.com/) for CSS styling and [Headless UI](https://headlessui.com/) unstyled, accessible components for more complex page elements like dropdowns and popups. Tailwind styles are applied via space-separated `class="STYLE"` attributes on HTML elements in Vue `<template>` blocks. The following sections will detail the specific styles that are used throughout the codebase.

Please note that as Scribe uses Tailwind, this means that `<style>` blocks are often times not used within Vue Single-File Components. `<style>` blocks should only be used in cases where including the styles within the `<template>` block would be overly complex or if Tailwind does not support a certain style parameter. The team understands that Tailwind at times can lead to very long style classes, but because of this we make use of the custom classes [below](#common-styles) to combine commonly used elements into consistent, responsive drop-in attributes.

<a id="common-styles"></a>

## Common styles [`⇧`](#contents)

The following are custom Tailwind classes from [frontend/assets/css/tailwind.css](https://github.com/scribe-org/scri.be/blob/main/frontend/assets/css/tailwind.css) that are consistently used within the Scribe frontend codes:

- `focus-brand`

  - Creates a custom brand styled orange ring around an element when it is focussed for both light and dark mode
  - Should be used on all elements that the user can focus (buttons, links, dropdowns, menu items, etc)

- `link-text`

  - Color and hover color are defined for links for both light and dark mode

> [!NOTE]\
> There's also custom styles available to make development easier such as `bg-breakpoint-test` that changes the background of the element it's applied to based on the current breakpoint.

<a id="formatting"></a>

## Formatting [`⇧`](#contents)

For the frontend Scribe uses [Prettier](https://prettier.io/) to format the code and [Headwind](https://github.com/heybourn/headwind) to sort Tailwind CSS classes. We'll eventually set it up so that code is autoformatted within the PR flow, and generally the team isn't worried about formatting as it's done on save locally as we work.

<a id="colors"></a>

## Colors [`⇧`](#contents)

The file [frontend/tailwind.config.ts](https://github.com/scribe-org/scri.be/blob/main/frontend/tailwind.config.ts) defines all colors within the `colors` section of the `theme` configuration. All brand colors are split first by `light` and `dark` mode in their names and then the general usage of the color followed by qualifiers such as `hover`. The reason for this naming criteria is to avoid repeat styling keywords like `text-text-light` that might lead to confusion or leaving it as just `text-light` rather than applying the usage and then the color. The prior style would correctly be applied via `text-light-text`.

Note that for all colors we need to apply both the light and dark mode variants. In Tailwind this is done by placing the `dark:` prefix before a class. An example of this is the following where we'll set the background of an element to the header color for both light and dark mode:

```html
<!-- This div has a background that reacts to the color mode. -->
<div class="bg-light-header dark:bg-dark-header"></div>
```

Note further that Tailwind allows for alpha components for opacity to be applied to colors directly within the class declaration. We thus do not need to save versions of colors with transparency unless they are inherently used with an alpha less than one. An example of a color that has an inherent non-one alpha is `light-text` (`"rgba(0, 0, 0, 0.85)"`). To apply an alpha component to a color in Tailwind you follow it with a slash and the alpha that should be used as in the following example:

```html
<!-- The background of this div has 40% opacity. -->
<div class="bg-light-cta-orange/40"></div>
```

<a id="font"></a>

## Font [`⇧`](#contents)

The fonts for Scribe are [Red Hat Text and Red Hat Display](https://www.redhat.com/en/about/brand/standards/typography) as defined in [frontend/tailwind.config.ts](https://github.com/scribe-org/scri.be/blob/main/frontend/tailwind.config.ts). `Red Hat Text` is applied throughout the website and `Red Hat Display` is used for all headers by applying `font-display`. As headers are generally defined by `responsive-h#` custom classes that include `font-display`, it will be rare that you'll need to apply it directly. See the next section for more details.

<a id="text-size"></a>

## Text size [`⇧`](#contents)

[frontend/assets/css/tailwind.css](https://github.com/scribe-org/scri.be/blob/main/frontend/assets/css/tailwind.css) defines custom combinations of default and Scribe defined Tailwind header sizes. Responsive header classes all have `font-display` applied to them. The naming criteria of these headers follows that of HTML headers so that the team remembers that when a `responsive-h#` tag is used that it should be applied to a coinciding `<h#>` tag for accessibility. Note that headers should generally have a `bold` style applied to them as well, with for example page headers being defined as follows:

```html
<!-- The size and weight styles for page headers. -->
<h1 class="font-bold responsive-h1">Page Header</h1>
```

<a id="tab-size"></a>

## Tab size [`⇧`](#contents)

Codes on the frontend for Vue (`<template>`, `<script>` and `<style>` blocks), TypeScript, CSS and other related files should use two spaces for tabs.

<a id="icons"></a>

## Icons [`⇧`](#contents)

Scribe uses [nuxt-icon](https://github.com/nuxt-modules/icon) for all icons. Icons are defined via `<Icon name="ICON_NAME"/>` components, with [Icônes](https://icones.js.org/) being a good place to look for [Iconify](https://iconify.design/) based files to import. The `<Icon/>` component also has a `size` argument that `em` based arguments can be passed to. There's also a `color` argument, but colors are handled with Tailwind CSS via the `text-COLOR` class argument.

Custom icons for Scribe can further be found in the [Icon directory of the frontend components](https://github.com/scribe-org/scri.be/tree/main/frontend/components/Icon). These icons can also be referenced via the `<Icon>` component via their file name (ex: `<Icon name="IconSupport">` for the grasped hands we use). For Tailwind coloration note that we need to use `fill-COLOR` for the custom Scribe icons rather than `text-COLOR`.

<a id="padding"></a>

## Padding [`⇧`](#contents)

There are a few custom padding classes that can be used for `px` and `py` styling as defined in [frontend/assets/css/tailwind.css](https://github.com/scribe-org/scri.be/blob/main/frontend/assets/css/tailwind.css). Please use consistent custom padding classes to assure that elements move together at different breakpoints.
