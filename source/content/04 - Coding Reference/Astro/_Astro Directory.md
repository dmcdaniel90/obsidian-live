## Key parts of Astro
- Understand island architecture
- Learn html directives
- Improve knowledge of Markdown
- Learn how to extend Astro
- Understand how to use slots
- Learn the Astro API
- Extend to a CMS

---
## Getting Started

>[!terminal] Create from official template
`npm create astro@latest -- --template <example-name>`

>[!terminal] Create from template from Github repo
`npm create astro@latest -- --template <github-username>/<github-repo>`

>[!terminal] Common project structure

``` dirtree
- public/
- src/
	- components/
		- Header.astro
		- Gallery.jsx
	- layouts/
		- BaseLayout.astro
	- content/ /* used for content collections only */
	- pages/
		- index.astro
		- about.astro
		- posts/
			- post-1.md
			- post-2.md
			- post-3.md
	- styles
		- global.css
- package.json
- tsconfig.json
- astro.config.mjs
```
> ### Common Setup Tasks
> > [!info] Integrating Prettier and ESLint
> See [here](https://patheticgeek.dev/blog/astro-prettier-eslint-vscode) for configuration setup
---

## References
- [Documentation](https://docs.astro.build/en/getting-started/)
- [Github Repo](https://github.com/withastro/astro)
- [Blog](https://astro.build/blog/)
- [Adding and sharing React state](https://youtu.be/R3N_zg7Lz6Q?si=jDrgUET964q4MuPn)
- [Working with data](https://youtu.be/aS5id2273gY?si=cytRxwjR0dun0VH3)
- [CodingInPublic - Tutorial](https://youtube.com/playlist?list=PLoqZcxvpWzzeRwF8TEpXHtO7KYY6cNJeF&si=jj6-Ku5W4uDE1KXA)



