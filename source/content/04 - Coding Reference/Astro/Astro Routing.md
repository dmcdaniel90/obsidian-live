---
tags:
  - astro/routing
---

> Pages are located in the `src/pages/` directory. Use standard `<a>` tags to navigate between routes. Subroutes are mapped based on the filesystem structure at build time. For instance, you can either use a `src/pages/about.astro` file or `src/pages/about/index.astro` to declare a new route at `mysite.com/about`


### Dynamic Routing
> An Astro page file can specify dynamic route parameters in its filename to generate multiple, matching pages. For example, `src/pages/authors/[author].astro` generates a bio page for every author on your blog. `author` becomes a _parameter_ that you can access from inside the page.

 > [!Caution] Note
 In Astro’s default static output mode, these pages are generated at build time, and so you must predetermine the list of `author`s that get a corresponding file. In SSR mode, a page will be generated on request for any route that matches.

#### Static (SSG) Mode

> Because routes must be determined at build time for static sites, you can use the `getStaticPaths()` function to generate an array of objects holding the dynamic parameters.
```jsx
{/*src/pages/dogs/[dog].astro*/}
---
export function getStaticPaths() {
  return [
    {params: {dog: 'clifford'}},
    {params: {dog: 'rover'}},
    {params: {dog: 'spot'}},
  ];
}

const { dog } = Astro.params;
---
<div>Good dog, {dog}!</div>
```
> You can use rest parameters spread deep nested routes
```jsx
{/*src/pages/[path].astro*/}
---
export function getStaticPaths() {
	return [
		{params: {path: 'one/two/three'}},
		{params: {path: 'four'}},
		{params: {path: undefined }
	]
}
const { path } = Astro.params;
---
```
> A more practical use that mixes rest parameters with named parameters
```jsx
{/* filename: /[org]/[repo]/tree/[branch]/[...file] 
request made for: /withastro/astro/tree/main/docs/public/favicon.svg
*/}
```
```jsx
---
export function getStaticPaths() {
	return [
		{params: {
			org: 'withastro',
			repo: 'astro',
			branch: 'main',
			file: 'docs/public/favicon.svg'
			}
		}
	]
}
const { path } = Astro.params;
---
```
#### Another Example
> Uses a destructured `[...slug]` to set routes, and also sets incoming props for each route
```jsx
---
export async function getStaticPaths() {
	const pages = [
		{
			slug: undefined,
			title: "Astro Store",
			text: "Welcome to the Astro store!",
		},
		{
			slug: "products",
			title: "Astro products",
			text: "We have lots of products for you",
		},
		{
			slug: "products/astro-handbook",
			title: "The ultimate Astro handbook",
			text: "If you want to learn Astro, you must read this book.",
		},
	];

	return pages.map(({ slug, title, text }) => {
		return {
			params: { slug },
			props: { title, text },
		};
	});
}

const { title, text } = Astro.props;
---

<html>
	<head>
		<title>{title}</title>
	</head>
	<body>
		<h1>{title}</h1>
		<p>{text}</p>
	</body>
</html>
```
>[!important] For Server-Side Rendering SSR Mode
>Do not use the `getStaticPaths` function. Simply declare the array of route objects in `pages` and instead of mapping over the pages, use the `slug` to find the requested page on the server
>```jsx
>const { slug } = Astro.params;
>const page = pages.find((page) => page.slug === slug);
>if (!page) return Astro.redirect("/404");
>const { title, text } = page;
>```


### Redirects
> Direct configuration works for static routes, but also for dynamic routes as long as they contain the same parameters
```node
import { defineConfig } from 'astro/config';

export default defineConfig({
  redirects: {
    '/old-page': '/new-page'
  }
});

{/* Using SSR or an adaptor lets you set status codes */}
export default defineConfig({
	redirects: {
		'/old-page': {
		status: 302,
		destination: '/new-page'
		}
	}
});
```
> You can use the `Astro.redirect` method to dynamically redirect
```jsx
---
import { isLoggedIn } from '../utils';

const cookie = Astro.request.headers.get('cookie');

// If the user is not logged in, redirect them to the login page
if (!isLoggedIn(cookie)) {
  return Astro.redirect('/login');
}
---
<html>
  <!-- Page here... -->
</html>
```


