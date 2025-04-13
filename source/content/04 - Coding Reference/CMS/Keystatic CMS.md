>[!info] Use cases
>-Need to support Markdoc or MDX
>-Require a Typescript API
>-Do not need a static admin route
>-Working with Astro Content Collections, Next.js, or Remix

>[!faq] [Documentation](https://keystatic.com/docs/content-organisation)
## Getting Started

>[!terminal] Starting a new project that will use Next.js or Astro
>`npm create @keystatic@latest`

## Astro Integration Guide

>[!terminal] Install dependencies to Astro
>`npx astro add react mdx`
>`npm install @keystatic/core @keystatic/astro`

>[!code] Update the Astro config
>```jsx
>// astro.config.mjs
>import { defineConfig } from 'astro/config'
>
>import react from '@astrojs/react'
>import mdx from '@astrojs/mdx'
>import keystatic from '@keystatic/astro'
>
>export default defineConfig({
>	integrations: [react(), mdx(), keystatic()],
>	output: 'hybrid'
>})

>[!code] Create the Keystatic config
>```jsx
>// keystatic.config.ts
>import { config, fields, collection } from '@keystatic/core'
>
>export default config({
>	storage: {
>		kind: 'local' //or cloud
>	},
>	collections: {
>		posts: collection({
>			label: "Posts",
>			slugField: 'title',
>			path: 'src/content/posts/*',
>			format: { contentField: 'content' },
>			schema: {
>				title: fields.slug({ name: { label: 'Title' } }),
>				content: fields.document({
>					label: 'Content',
>					formatting: true,
>					dividers: true,
>					links: true,
>					images: true
>				})
>			}
>		})
>	}
>})

>[!note] Visit `http://127.0.0.1:4321/keystatic` to see the Keystatic Admin UI running.

>[!important] Because Keystatic needs to run serverside code and use Node.js APIs, you will need to add an [Astro adapter](https://docs.astro.build/en/guides/server-side-rendering/#adding-an-adapter) to deploy your project.

>[!caution] When using the `local` strategy, you may want to disable access to the `/keystatic` routes in production.
>
>```jsx
>export default defineConfig({
>	integrations: [react(), markdoc(), ...(process.env.SKIP_KEYSTATIC ? [] : [keystatic()])],
>	output: 'hybrid'
>})
>```
>
>Remember to add your environment variables to your deploy environment



## Keystatic Cloud

> Keystatic Cloud allows for cloud collaboration and live editing without a Github account or creating a local deployment. It also allows for opt-in cloud image storage, optimisation, and delivery.

>[!code] Configuring your project for Keystatic Cloud
>
>```jsx
>// keystatic.config.ts
>import { config } from '@keystatic/core'
>
>export default config({
>	storage: {
>		kind: 'cloud'
>	},
>	cloud: {
>		project: '[TEAM_NAME]/[PROJECT_NAME]' // from your Keystatic Cloud account
>	}
>})
>```

### Cloud Images

>[!note] Optimising images via URL query parameters
>	**fit** - scale-down, contain, cover, crop
>	**format (f)** - png, avif, webp, jpeg (else auto)
>	**quality (p)** - range(1 - 100)
>	**height (h)** - range (1 - 10240)
>	**width (w)** - range (1 - 10240)
>	
>>[!example] https://[IMAGE_URL]?width=240&height=480&fit=crop

>[!note] Keystatic provides a [`cloudImage` field](https://keystatic.com/docs/fields/cloud-image), which can be used instead of the [regular image field](https://keystatic.com/docs/fields/image) if Keystatic is running in cloud mode, and the Image Library is enabled for the project.

>[!note] Keystatic also provides a `CloudImage` component block, which can be used within the flow of a [document field](https://keystatic.com/docs/fields/document). **Coming soon**

