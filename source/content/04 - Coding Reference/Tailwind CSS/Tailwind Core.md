---
tags:
  - tailwindcss
  - css
---

## Utility-First vs Inline

> Instead of writing CSS, Tailwind lets you style elements using pre-existing utility classes directly in your HTML.
> 
> Unlike inline CSS, utility classes have the benefits of:
> - Pre-written class names
> - Constraints from a predefined design system
> - Responsive utilities (media queries) for creating responsive designs
> - State variants for targeting pseudo-classes such as `focus` and `hover`
> - More control over inheritance
> - Works with PostCSS plugins, such as PurgeCSS
> - Can declare multiple properties at once, such as `.sr-only`

## State Variants

>[!code] Declaring a hover modifier on a class name
>```html
><button class="bg-sky-500 hover:bg-sky-700">Save Changes</button>
>```

>[!info] Example modifiers
>- Pseudo-classes :FasArrowRight: `:hover`, `:focus`, `:first-child`, `:required`
>- Pseudo-elements :FasArrowRight: `::before`, `::after` `::placeholder`, `::selection`
>- Media and feature queries :FasArrowRight: `prefers-reduced-motion`
>- Attribute selectors :FasArrowRight: `[dir="rtl"]`, `[open]`

## Responsive Design

>[!info] All Tailwind classes can be applied conditionally at different breakpoints, of which Tailwind has five by default

| Breakpoint prefix | Min-width | CSS                         |
| ----------------- | --------- | --------------------------- |
| `sm`              | 640px     | `@media (min-width: 640px)` |
| `md`              | 768px     | `@media (min-width: 640px)` |
| `lg`              | 1024px    | `@media (min-width: 640px)` |
| `xl`              | 1280px    | `@media (min-width: 640px)` |
| `2xl`             | 1536px    | `@media (min-width: 640px)` |
>[!code] Setting a responsive width on an element
>```html
><!-- width of 16 by default, 32 for medium, 48 for large screens and up -->
><img class="w-16 md:w-32 lg:w-48" src="...">
>```

>[!caution] Don't use `sm:` to target mobile devices
>Use unprefixed utilities first, which target all devices, then use `sm:{utility-name}` to target all devices above 640px


## Dark Mode

>[!code] Add the `dark:` prefix to make a style apply only in dark mode
>```html
><div class="bg-white dark:bg-slate-800 ..."></div>

>[!info] Manually toggle dark mode
>By default, dark mode follows the `prefers-color-scheme` CSS media feature. You can set your Tailwind config to `darkMode: 'selector'` to set it manually. You can then use JS functionality to toggle the `dark` class in your main `<html>` element.

## Reusing Styles

>[!tip] Reusing Tailwind classes basics
>- Use your editor's multi-cursor to edit instances of the same class simultaneously.
>- Utilise iteration functions, such as `Array.map`
>- Create reusable components (such as in React)

>[!code] Composing custom classes
>```css
>@tailwind base
>@tailwind components
>@tailwind utilities
>
>@layer components {
>	.btn-primary {
>		@apply py-2 px-5 bg-violet-500 text-white font-semibold rounded-full
>	}
>}
>```
>
>>[!attention] Avoid using `@apply` just to make things look cleaner. By using apply, you end up basically writing CSS by coming up with class names, jumping between files, potentially making breaking changes to global CSS, and making your CSS bundle size larger.
>>

## Custom Styles

>[!example] Add customisations in the `theme` section of your `tailwind.config.js`.
>[See Example](https://tailwindcss.com/docs/adding-custom-styles#customizing-your-theme) 
>[See Documentation](https://tailwindcss.com/docs/theme)

### Arbitrary values, properties, and variants

>[!code] List of examples 
>```html
><div class="top-[117px]"></div>
><div class="top-[117px] lg:top-[344px]"></div>
><div class="bg-[#bada55] text-[22px] before:content-['Festivus']"></div>
><div class="bg-[--my-color]"></div> <!--no var() needed-->
><div class="[my-property:value] hover[my-property:value2]"></div> <!--can use modifiers-->
><div class="[--scroll-offset:56px] lg:[--scroll-offset:44px]"></div> <!--modify css variables-->
>
><!--Variants allow for on-the-fly selector modification-->
>
><ul role="list">{map a list of items}<li class="lg:[&:nth-child(3)]:hover:underline">{item}</li></ul>

### CSS and @layer styles

#### Base styles

> You can declare classes in your `<html>` or `<body>` element style tags to set base styles or you can `@apply` styles in an `@layer base` in your CSS file. 

#### Component styles

> Use the `@layer components` for when you need more complicated styles, but still want to be able to override them with utility classes, if needed. Also useful, for custom styles for third-party components.
> 
> >[!tip] Using `theme`
> >You can also use the defined theme from your Tailwind config by setting a property to `background-color: theme('colors.white');` or `padding: theme('spacing-6');` for example

#### Utility styles

> Useful for when there is a CSS feature that is not supported by Tailwind such as `.filter-grayscale`

>[!tip] Removing unused CSS
>Rules with an `@layer` directive will not be included in the rendered HTML if the class is not used. To always include it, remove the directive and place it above your `@tailwind utilities` directive to ensure you can still override your class with Tailwind utilities

### Functions

>[!code] Use the `theme()` function to access your Tailwind config values using dot notation.
>```css
>.content-area {
>	height: calc(100vh - theme(spacing.12));
>}
>.btn-blue {
>	background-color: theme(colors.blue.500 / 75%);
>}
>```

>[!code] The `screen()` function allows you to create media queries that reference your breakpoints by name instead of duplicating their values in your own CSS.
>```css
>@media screen(sm) {
>	/* Instead of saying min-width: 640px */
>}
>```
