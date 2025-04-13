---
tags:
  - astro/images
---

## Storing Images

> Images stored in `src/` are automatically optimised by Astro, whereas images in `/public` are served or copied into the build folder as-is, without optimising. Images can also be served from a CMS or other similar platform, however the [source must be specified in your configuration](https://docs.astro.build/en/guides/images/#authorizing-remote-images). Finally, images can also be fetched from an API or a full URL path.

>[!important] Local images must be imported to be used, unlike remote and `public` images
>

## Images Astro

### In .astro files
> The `<Image />` component is built in to Astro and allows for images to be automatically optimised. You can use an `<img>` HTML tag, but this will skip image processing. The `<Image/>` element also infers image dimensions to avoid Cumulative Layout Shift (CLS), adds lazy loading, and async decoding. 
> >[!code] The `<Image />` component
> >```js
> >---
> >import { Image } from 'astro:assets';
> >import localBirdImage from '../../images/subfolder/localBirdImage.png'
> >---
> ><Image src={localBirdImage} alt="A bird sitting on a nest of eggs" width="50" height="50" />
> 


>[!tip] Click [here](https://docs.astro.build/en/recipes/dynamically-importing-images/) for instructions on Dynamic Importing Images

>[!note] Special attributes of the `<Image/>` component
> - [densities](https://docs.astro.build/en/guides/images/#densities)
> - [widths & sizes](https://docs.astro.build/en/guides/images/#widths)
> - [quality](https://docs.astro.build/en/guides/images/#quality)
> - [inferSize](https://docs.astro.build/en/guides/images/#infersize)
> 
> >[!attention] You cannot currently set default values for all `<Image/>` components. As an alternative, wrap the `<Image/>` component in a custom component.
> >
> >```jsx
> >---
> >import { Image } from 'astro:assets';
> >const {src, ...attrs} = Astro.props;
> >---
> ><Image src={src} {...attrs} />
> ><style>....</style>
> >


## Images in Markdown and MDX

> Use the standard `![alt](src)` syntax for `.md` files. This works with the [Image Service API](https://docs.astro.build/en/reference/image-service-reference/) to optimise your images. `.mdx` files allow for you to use the `<Image/>` component and JSX `<img />` tags.

## Images in Content Collections

> In addition to the methods used for Markdown and MDX files, in Content Collections, you can also set a cover image and alt text by setting the `cover` and `coverAlt` attributes in the post frontmatter.

>[!code] Validating image metadata
>The `image` helper, along with the built in [Zod] integration, lets you validate image metadata in your content collection schema.
>
>```ts
>import { defineCollection, z } from "astro:content";
>
>const blogCollection = defineCollection({
>	schema: ({ image }) => z.object({
>		title: z.string(),
>		cover: image().refine((img) => img.width >= 1080, {
>			message: "Cover image must be at least 1080 pixels wide!"
>		}),
>		coverAlt: z.string()
>	})
>});
>export const collections = {
>	blog: blogCollection
>}
>```

## Images in UI Frameworks

>Use the framework's standard syntax for rendering images. Astro components will not work here, but you can wrap the `<Image />` component in a UI framework component or in a [[Astro Components#The slot element | named `<slot />`]].


