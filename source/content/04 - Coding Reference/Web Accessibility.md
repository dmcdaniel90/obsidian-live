---
tags:
  - web-accessibility
  - html
  - aria
---


>[!info] [Web.Dev Learn Accessibility](https://web.dev/learn/accessibility/)

> Digital accessibility, commonly abbreviated a11y, is about designing and building websites and web apps that disabled people can interact with in a meaningful and equivalent way.

|Types of Impairments|Examples|Tools Commonly Used|Pain Points|
|---|---|---|---|
|Vision|blindness, low vision, colour blindness|screen readers, screen magnification, Braille output devices|Screen reader software incompatibility, no pinch to zoom on mobile, complex graphs and charts differentiated by colours alone, text colour contrasts|
|Mobility|arthritis, paralysis, seizure disorders|Adaptive switches, eye tracking devices, mouth/head sticks, speech input|Elements that are only designed to work with the use of a mouse.|
|Hearing|deafness, hard of hearing, hearing impaired|hearing aids, captions, transcripts, sign language|Audio content without text transcripts, video with no synchronized captions|
|Cognitive|Down's syndrome, autism, ADHD, dyslexia, etc|screen readers, text highlighting, text prediction, abstractive summarization tools|Busy interfaces that make it overly complicated to focus on the task at hand, big walls of words with little whitespace, justified text, and small or hard-to-read fonts.|
|Seizure and vestibular|Epilepsy, vertigo, dizziness, balance|OS settings to reduce motion|Videos that autoplay, extreme flashing or strobing of visual content, parallax effects, or scroll-triggered animations.|
|Speech|apraxia, dysarthria, stuttering|Augmentative and alternative communication, speech-generating devices|Voice-activated technology such as smart home devices and apps.|

>[!info] A fourth of the world's population is made up of persons with disabilities. It is one of the world's largest emerging markets, with many modern products the result of accessibility research and corporate lawsuits regarding the lack of accessible features.  


## Measuring digital accessibility

>[!info] The standard recommendation to follow is provided by the [Web Content Accessibility Guidelines (WCAG)](https://web.dev/learn/accessibility/measure?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2F%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Fmeasure#wcag)

>[!tip] See [Conducting an Accessibility Audit](https://www.w3.org/WAI/test-evaluate/)

![[WCAG Success Criteria.png]]

### The Four Principles

>[!tip] [W3 Accessibility Principles](https://www.w3.org/WAI/fundamentals/accessibility-principles/)

- **Perceivable** - Users must be able to perceive all essential information on the screen, and it must be conveyed to multiple senses
- **Operable** - Users must be able to operate the digital product's interface. The interface cannot require interaction that a user cannot perform.
- **Understandable** - Users must understand the information and the operation of the user interface
- **Robust** - As devices and user agents evolve, the digital product supports and continues to support assistive technologies.

## ARIA and HTML

> ARIA is not a true programming language but a set of attributes you can add to HTML elements to increase their accessibility. These attributes communicate role, state, and property to assistive technologies via accessibility APIs found in modern browsers. This communication happens through the accessibility tree.

>[!quote] "[WAI-ARIA](https://www.w3.org/WAI/standards-guidelines/aria/), the Accessible Rich Internet Applications Suite, defines a way to make web content and web applications more accessible to people with disabilities. It especially helps with dynamic content and advanced user interface controls developed with HTML, JavaScript, and related technologies."
>
>[The WAI group](https://www.w3.org/WAI/)

>[!info] The Accessibility Tree
>The accessibility tree is created by the browser and based on the DOM. It corrects markup based up the user's assistive technology preferences. Think of it as a copy of the DOM that ARIA interacts with.
>
>See more: [Accessibility Tree - Chrome Dev Tools](https://developer.chrome.com/blog/full-accessibility-tree)

### ARIA Features

The three main features of ARIA are
- *Roles* - define what an element is or does on the page
```html
<div role="button">Self-Destruct</div>
```
- *Properties* - express characteristics or relationships to an object
```html
<div role="button" aria-describedby="more-info">Self-Destruct</div>
<div id="more-info">This page will self destruct in 10 seconds</div>
```
- *States/values* - define the current conditions or data values associated with the element
```html
<div role="button" aria-describedby="more-info" aria-pressed="false">Self-Destruct</div>
<div id="more-info">This page will self-destruct in 10 seconds</div>
```
### ARIA Rules

1. Don't use ARIA unless an HTML element does not have accessibility support built in. Elements and attributes such as `<nav>` and `<required>` do not require ARIA as they are accessible-ready, so it is preferred to use Semantic HTML elements.
2. Don't add unnecessary ARIA, such as adding a role to an `<h2 role="tab">` tag. If it is for interactivity, it would be better to wrap the `<h2>` tag in a `<div role="tab"></div>`
3. Always support keyboard navigation. Add a `tabindex="0"` attribute to any element that needs to be focusable and doesn't normally receive it.
4. Don't hide focusable elements
5. Use accessible names for interactive elements. Accessible names can be the text between a link tag, an image between a link tag with an `alt` attribute, or the `<label>` element.

### More ARIA + HTML tips

- Use the correct roles. Use an `aria-label` to describe a link, instead of `role`
```html
<a role="heading">Read more</a> <!--Dont do this! -->
<a aria-label="Read more about some awesome artice title">Read More</a>
```
- Avoid redundant roles, such as `role="list"` on a `<ul>` or `<ol>` element
- Avoid unintended side effects
>[!code]
>```html
><details>
<summary role="button">More Information</summary> <!-- UH OH -->
</details>

## Content Structuring

> One of the most important aspects of digital accessibility is the underlying structure of the page. When you build your website or app using [structural elements](https://www.w3.org/WAI/tutorials/page-structure/) instead of relying on styles alone, you give critical context to people using assistive technologies (AT), such as screen readers.
> 
> Structural elements serve as an outline of the content on the screen, but they also act as anchor points to allow for easier navigation within the content.

>[!info] [MDN HTML Element Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) 

### Landmarks

> Landmarks provide AT users detail about the page's layout. It is preferable to use the newer HTML elements, however you can use/combine with the ARIA role. `<form>` and `<section>` require the `name` attribute in order to be accessible, with `<section>` needing to be [[#ARIA Rules | accessibly named.]]

| HTML landmark element                                                        | ARIA landmark role                                                                                  |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [`<header>`](https://developer.mozilla.org/docs/Web/HTML/Element/header)     | [banner](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/banner_role)               |
| [`<aside>`](https://developer.mozilla.org/docs/Web/HTML/Element/aside)       | [complementary](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/complementary_role) |
| [`<footer>`](https://developer.mozilla.org/docs/Web/HTML/Element/footer)     | [contentinfo](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/contentinfo_role)     |
| [`<nav>`](https://developer.mozilla.org/docs/Web/HTML/Element/nav)           | [navigation](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/navigation_role)       |
| [`<main>`](https://developer.mozilla.org/docs/Web/HTML/Element/main)         | [main](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/main_role)                   |
| [`<form>`](https://developer.mozilla.org/docs/Web/HTML/Element/form) 1       | [form](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/form_role)                   |
| [`<section>`](https://developer.mozilla.org/docs/Web/HTML/Element/section) 1 | [region](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Roles/region_role)               |
> [See examples](https://web.dev/learn/accessibility/structure?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2F%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Fstructure#landmarks)
### Headings