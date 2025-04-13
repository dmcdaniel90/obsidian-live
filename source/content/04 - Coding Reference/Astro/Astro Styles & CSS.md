---
tags:
  - astro/css
---

> Astro officially supports [Tailwind CSS](https://docs.astro.build/en/guides/integrations-guide/tailwind/), but has many other community plugins that are useful for styling and optimising.

## Adding styles

> Simply use `<style>` tags in your component or page template. You can write css (or SASS) between the tags, or write inline CSS in standard or JSX format.

>[!important] Styles are automatically scoped to the local component by default, not globally. It's common to use a `src/styles/global.css` file and to use scoped stylesheets for individual components. Global styles are useful for applying styles to content from outside of Astro, such as blog posts. See more about global styles [here](https://docs.astro.build/en/guides/styling/#global-styles)

## Dynamic classes

> Use the `class:list` utility attribute
```jsx
---
const { isRed } = Astro.props;
---
<!-- If `isRed` is truthy, class will be "box red". -->
<!-- If `isRed` is falsy, class will be "box". -->
<div class:list={['box', { red: isRed }]}>
	<slot />
</div>

<style>
  .box { border: 1px solid blue; }
  .red { border-color: red; }
</style>
```

## CSS variables

> Try defining CSS variables in your frontmatter, then access them by declaring them in the `define:vars` attribute in the `<style>` tag.
```jsx
---
const foregroundColor = "rgb(221 243 228)";
const backgroundColor = "rgb(24 121 78)";
---
<style define:vars={{ foregroundColor, backgroundColor }}>
  h1 {
    background-color: var(--backgroundColor);
    color: var(--foregroundColor);
  }
</style>
<h1>Hello</h1>
```
## Passing classes to children

> Although the class attribute does not automatically pass down and class is a reserved keyword in JS, you can accept a class *prop* and the `data-astro-cid-*` attribute.
```jsx
---
const { class: className, ...rest } = Astro.props;
{/* ...rest contains the data-astro-cid-* */}
---

<div class={className} {...rest}>
	<slot/>
</div>

---
import MyComponent from "../components/MyComponent.astro"
---
<style>
	.red {
		color: red;
	}
</style>

<MyComponent class="red">This will be red!</MyComponent>
```

## External styles
> For external global stylesheets, you can either import them into your frontmatter (note that styles will be scoped relative to the importing component) or import from an NPM package. You can also import stylesheets as you would normally for UI frameworks such as React

>[!caution] Importing styles from npm packages
> See [here](https://docs.astro.build/en/guides/styling/#import-a-stylesheet-from-an-npm-package) for additional config possibly needed

>[!info] `<link>` Tags
>You *could* use link tags to load a static stylesheet (from the `public/` directory), however, you would miss out on the CSS processing, bundling, and optimisations provided by Astro. Better to use `import`! 

## Integrations

>[!terminal] Sass and SCSS
>Use `<style lang="scss">` or `<style lang="sass">` in `.astro` files. 
>```
>npm install sass

>[!terminal] TailwindCSS
>See [here](https://docs.astro.build/en/guides/integrations-guide/tailwind/) for configuration details
>See [[Tailwind Directory]]
>```
>npx astro add tailwind


>[!code] PostCSS
>Create a `postcss.config.cjs` file at the project root
>```js
>module.exports = {
>	plugins: [
>		require('autoprefixer'),
>		require('cssnano')
>	]
>}

>[!code] React/Preact
> `.jsx` files support global CSS and CSS Modules.
> ```jsx
> import './global.css'; // include global CSS
import Styles from './styles.module.css'; // Use CSS Modules (must end in `.module.css`, `.module.scss`, or `.module.sass`!)
