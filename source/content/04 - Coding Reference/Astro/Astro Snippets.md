>[!code] Using frontmatter props
>```js
>// The frontmatter prop gives access to frontmatter and other data such as title, author, and date
>
>const { frontmatter } = Astro.props;
>```


>[!code] Typing frontmatter props
>```ts
>import type {MarkdownLayoutProps} from 'astro';
>
>type Props = <MarkdownLayoutProps>{
>	title: string;
>	author: string;
>	date: string;
>	postNumber: number;
>};
>```

> [!code] Fragments can be useful to avoid wrapper elements when adding [`set:*` directives](https://docs.astro.build/en/reference/directives-reference/#sethtml), as in the following example:
> ```jsx
> ---
> const htmlString = '<p>Raw HTML content</p>'
> ---
> <Fragment set:html={htmlString} />
> ```

