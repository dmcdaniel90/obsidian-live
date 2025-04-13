---
tags:
  - tailwindcss
---

## Objective
> Understand how to use Tailwind classes to style content

## Key Criteria
- Set up a basic configuration file
- Use in frameworks including React and Astro
- Have a workflow for quickly recalling attribute names
## Results
- Create/convert a project to Tailwind styles
- Create a reusable configuration file

## Resources
- [Documentation](https://tailwindcss.com/docs/installation)
- [Github Repo](https://github.com/tailwindlabs/tailwindcss)
- [Tailwind Play](https://play.tailwindcss.com/)
- [Tailwind Blog](https://tailwindcss.com/blog)

---

## Getting Started

>[!terminal] Install and create a config file
> `npm install -D tailwindcss`
> `npx tailwindcss init`

>[!code] Add the paths to your files
>```js
>/** @type {import('tailwindcss').Config} */
>module.exports = {
>	content: ["./src/**/*.{html,js}"],
>	theme: {
>		extend: {},
>	},
>	plugins: []
>}
>```

>[!code] Add Tailwind directives to your CSS
>`@tailwind base;`
`@tailwind components;`
`@tailwind utilities;`

>[!terminal] Start the CLI build process
>`npx tailwindcss -i ./src/input.css -o ./src/output.css --watch`

### Common Setup Tasks

>[!info] Installing and setting up the Prettier plugin
>`npm install -D prettier-plugin-tailwindcss`
>
>Then, add 'prettier-plugin-tailwindcss' to your `prettier.config.js`
>
>See additional config setup [here](https://github.com/tailwindlabs/prettier-plugin-tailwindcss)



---
## Directory
- [[Tailwind Core]]
---
## Videos
