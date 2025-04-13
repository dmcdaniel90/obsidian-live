---
tags:
  - astro/content-collections
  - astro/typescript
---
**Tags**: [[astro#content collections]]

> A content collection is any top-level directory inside of the reserved `src/content` directory. Common collections ma include `src/content/authors` or `src/content/posts`. Only content collections are allowed inside of this directory. The files within each content collection are called **collection entries**. These can be in `.md`, `.mdx`, `.yaml`, or `.json` format.

>[!tip] Excluding files
>You can exclude files in a collection from being built by prefixing the name with an `_`

>[!note] The .astro directory
>This directory automatically stores metadata for your collections whenever you run `astro dev` or `astro build`. It can be updated manually by running `astro sync`. Also, it is advised to add this directory to your `.gitignore` file.

## Folder structure

> Use different collections for different types of content. This is important, because frontmatter validation and [[astro#typescript| Typescript]] type-safety require entries in a collection to follow a similar structure (see [schemas]).
> 
> You can also use subdirectories in your collections for further organisation. An example of this would be to have subdirectories for i18n translations inside of a `docs` collection. When you query this collection, you can then filter each language using the file path.

## Defining Collections

>[!code] Collections are defined inside of a `src/content/config.ts` file
>
>```jsx
>import { defineCollection } from 'astro:content';
>
>const blogCollection = defineCollection({ ... });
>const authorsCollection = defineCollection({ ... });
>
>export const collections = {
>	'blog': blogCollection,
>	'authors': authorsCollection,
>}
>```

### Setting up [[astro#typescript|Typescript]] with Astro

>[!code] Setup a `src/content/config.ts` file and a `tsconfig.json` file
>```jsx
>import { defineCollection } from ‘astro:content’
>const blogCollection = defineCollection({ /*  */ })
>export const collections = {
>	‘blog’: blogCollection,
>}

> [!important] [[Zod]] is used in Astro Content Collections to validate frontmatter and provide automatic Typescript types.
> [See Zod README](https://github.com/colinhacks/zod)




