---
tags:
  - astro/viewtransitions
---
**Tags**: [[astro#view transitions]]

>[!documentation] [Documentation](https://docs.astro.build/en/guides/view-transitions/)
## Basics

>[!code] Add the `<ViewTransitions />` element into the `<head>`. Be sure to `import {ViewTransitions} from "astro:transitions`
>``` html
><head>
>	<meta charset="UTF-8" />
>	<title>{title}</title>
>	<ViewTransitions />
></head>


> This adds some default transitions between page routes

## Transition Controls

>[!documentation] [See Transition Directives](https://docs.astro.build/en/guides/view-transitions/#transition-directives)

### Naming transitions

>[!tip] Give common elements on separate pages the same name with the `transition:name={name}` property to enable per component transition control
>By default, elements will 'smart-morph' if they have changed position or sizing in between page routes

### Animation

>[!tip] Use the `transition:animate="none"` on the `<body>` element to remove animations from the page (but keep any per-component transitions.) Then use the `transition:animate="slide"` property, for example, on another component further down (such as a `<slot />` element)

### Persisting

> Transitions triggered by an event listener, such as with a theme toggle, do not work after the listener has been triggered because Astro treats event listeners as modules that only run once on page load.

>[!tip] Use the `transition:persist` property on any elements that you want to have javascript or event listener data to carry over on a new page route.

>[!tip] For event listeners on the `window` object, such as running a function to get a them from local storage on initial page load, you will need to use an event on the `document` object `astro:after-swap` as well in order to persist data between refreshes.

>[!tip] Naming persists
>Combine a `transition:persist` with `transition:name`
>:FasArrowDownLong:
>`transition:persist="navigation"`

### Maintaining State

#### System Flow
> In Astro, the `ViewTransition` flow looks like this:
> 1. User clicks link to new route
> 2. A request is made to the server for the new route
> 3. The server adds a data attribute `<html data-astro-transition="forward/back"` to determine which direction to move (for slide transitions)
> 4. `document.startViewTransition` fires (fallback for non-Chromium)
> 5. Swaps occur
> 	a. `<head>` items such as shared stylesheets, scripts, and `transition:persist`
> 	b. `<body>` replaced (shared `transition:persist` stays)
> 	c. scroll position restored
> 	d. `astro:after-swap` fires on `document`
> 6. Wait for new stylesheets and new scripts
> 7. Show new document, animate elements, and `astro:page-load` fires

>[!caution] Using `<script is:inline>`
>Using this will also cause any scripts to run on each page load. However, it can cause a flash of the default theme before loading the locally stored theme.

## Customisations

### Loading documents

> Problem: With `<ViewTransitions />` enabled on an Astro site, a user attempts to access a link to a PDF that is located in the public folder. The link opens to a page of jumbled letters, numbers, and symbols

>[!check] use `data-astro-reload` attribute
>Use the `data-astro-reload` attribute to force a full page navigation (traditional navigation) 

### Custom animations

>[!code] Pass a custom preferences object to the `transition:animate` attribute to modify an existing animation type
>
>```jsx
>import { fade } from 'astro:transitions'
><header transition:animate={fade({ duration: '0.4s' })} ></header>
>```

>[!code] Create a custom animation :FasArrowRightLong: [See Types](https://docs.astro.build/en/guides/view-transitions/#customizing-animations)
>```jsx
>const anim = {
>	old: {
>		name: 'fadeIn',
>		duration: '0.2s'
>		easing: 'linear',
>		fillMode: 'forwards',
>		}
>		new: {
>		name: 'fadeOut',
>		duration: '0.3s',
>		easing: 'linear',
>		fillMode: 'backwards',
>		}
>	};
>	const myFade = {
>		forwards: anim,
>		backwards: anim,
>	};
>	<header transition:animate={myFade}> ... </header>

