---
tags:
  - astro/component
  - astro/slot
---
**Tags**: [[astro#component]]
## Components

> Use Astro or framework components, import and fetch data, pass and use props, use [[JSX]] syntax

``` jsx
---
import SomeAstroComponent from '../components/SomeAstroComponent.astro';
import SomeReactComponent from '../components/SomeReactComponent.jsx';
import someData from '../data/pokemon.json';

// Access passed-in component props, like `<X title="Hello, World" />`
const { title } = Astro.props;
// Fetch external data, even from a private API or database
const data = await fetch('SOME_SECRET_API_URL/users').then(r => r.json());
---
<!-- Your template here! -->
```
``` jsx
<h1>{title}</h1>
<SomeAstroComponent pokemonList={someData}/>

{
data.map(user => {
  return <SomeReactComponent client:load user={user} />
  })
}
```

### The [[astro#slot|slot]] element

> Allows you to create a wrapper around a set of elements or components

```html
<!—- a component called Container —->

<div class=“container”>
  <slot /> <!—- Children go here —>
</div>

<div class=container”>
  <slot />
</div>

<!—- Import ‘Container.astro’ —>

<Container>
  <h1>Hello World</h1>
  <SomeComponent />
  <AnotherComponent />
</Container>

<!—- Named Slots —->

<div id="content-wrapper">
  <Header />
  <slot name="after-header" />  <!--     children with the `slot="after-header"` attribute will go here -->
  <Logo />
  <h1>{title}</h1>
  <Footer />
  <slot name="after-footer" />
</div>

<Fragment slot=“after-header”>
  <h1>Header in a fragment</h1>
</Fragment>

<slot>
  <p>Fallback content if no slot </p>
</slot>
```

