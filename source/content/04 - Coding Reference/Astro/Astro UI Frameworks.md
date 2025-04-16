---
tags:
  - astro/hydration
  - astro/ui
  - astro/component
  - react/astro
---
**Tags**: [[astro#component]], [[react#astro]]
## Official UI Frameworks

>[!note] These frameworks are officially supported by Astro
>- [AlpineJS](https://docs.astro.build/en/guides/integrations-guide/alpinejs/)
>- [Lit](https://docs.astro.build/en/guides/integrations-guide/lit/)
>- [Preact](https://docs.astro.build/en/guides/integrations-guide/preact/)
>- [React](https://docs.astro.build/en/guides/integrations-guide/react/)
>- [SolidJS](https://docs.astro.build/en/guides/integrations-guide/solid-js/)
>- [Svelte](https://docs.astro.build/en/guides/integrations-guide/svelte/)
>- [Vue](https://docs.astro.build/en/guides/integrations-guide/vue/)
>>[!tip] Visit [astro.new](astro.new) to test any of these frameworks out

## Using Framework Components

> Framework components can live in the `/src/components` directory alongside your Astro components or organised in any other way. You can import them into your Astro components and use them as you would normally. By default, they are rendered only on the server as static HTML.

## Hydrating Interactive Components

>[!code] Make framework components interactive by using the `client:*` directives
>
>```jsx
>---
>import Button from '../components/Button.jsx'
>import Counter from '../components/Button.jsx'
>import Sidebar from '../componetns/Sidebar.jsx'
>import Modal from '../components/Button.jsx'
>---
><!-- JS imports on page load -->
><Button client:load />
>
><!-- JS loads after initial load and client is idle (requestIdleCallback event fired) -->
><Counter client:idle />
>
><!-- JS loads when component is visible -->
><Counter client:visible />
>
><!-- JS loads when specified margin enters the viewport -->
><Counter client:visible={{rootMargin: "200px"}} />
>
><!-- JS loads when a certain CSS media query is met -->
><Sidebar client:media="(max-width: 50em)" />
>
><!--  JS renders on the client -->
><Modal client:only="react" />
>```

>[!tip] `.astro` components can use components from multiple frameworks

## Passing props

>[!code] React, Preact, and Solid use the `children` prop, while Svelte and Vue use the `<slot/>` element
>
>```jsx
>---
>import ReactSidebar from '../components/ReactSidebar.jsx'
>---
>
><ReactSidebar>
>	<p>Text</p>
><ReactSidebar />
>```

>[!code] You can also use Named Slots. This also works with React, Preact, and Solid
>
>```jsx
>export default function ReactSidebar(props) {
>	return(
>		<aside>
>			<header>{props.title}</header>
>			<main>{props.children}</main>
>			<footer>{props.socialLinks}</footer> 
>			// Note the transform from kebab-case to camelCase in React
>		</aside>
>	)
>}
>
><ReactSidebar>
>	<h2 slot="title">Menu</h2>
>	<p>Some text</p>
>	<ul slot="social-links">
>		<li><a href="...">Link 1</a></li>
>		<li><a href="...">Link 1</a></li>
>	</ul>
></ReactSidebar> 
>```


>[!important] You can mix framework components and nest them within each other, but only is `.astro` files, not in framework files themselves. You can also use Astro components nested in between frameworks components.

>[!warning] Using the `client:` modifiers on an Astro component results in an error.
>Astro components have no client-side runtime, so you will need to write client side `<script>` tags


## FAQ

>[!faq] How do I use React Hook Forms with Preact and Astro?
>[See here](https://stackoverflow.com/questions/75274026/using-astro-js-with-preact-and-react-hook-forms)

