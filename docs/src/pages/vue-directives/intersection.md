---
title: Intersection Directive
desc: Vue directive that uses Intersection Observer API to call a method when user scrolls and brings a component into or out of view.
badge: "v1.3.0+"
related:
  - /vue-directives/scroll-fire
  - /vue-directives/scroll
---

"Intersection" is a Quasar directive that enables a method to be called when the user scrolls and the DOM element (or component) that it is applied to comes into or out of the viewport.

Under the covers, it uses the [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).

::: warning
Not all browsers support the Intersection Observer API. Most [modern browsers](https://caniuse.com/#search=intersection) do, but other browsers, **like IE 11**, do not. If you need to support older browsers, you can install and import (into a boot file) the official W3C [polyfill](https://github.com/w3c/IntersectionObserver).
:::

## Installation

<doc-installation directives="Intersection" />

## Usage

Reading the [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) first will be best in your understanding of how this directive works.

Intersection directive takes either a handler function as an argument or an Object. The Object form looks like this:

```js
{
  handler: /* Function */,
  cfg: {
    // any options from "Intersection observer options"
    // on https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API
    root: null, // DOM Element
    rootMargin: '0px',
    threshold: 0
  }
}
```

When using the Object form, only the `handler` key is mandatory.

The handler Function takes one parameter, which is an [IntersectionObserverEntry](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry).

::: tip
Scroll within the examples below until the observed element is in view. Then scroll it out of view.
:::

### Basic

<doc-example title="Basic" file="Intersection/Basic" />

### Trigger once

The directive can be used with the `once` modifier (ex: `v-intersection.once`). Once the observed element comes into view, the handler Function will be called and the observing will stop. This allows you to control the processing overhead if all you need is to be notified when the observed element starts to be visible on screen.

<doc-example title="Once" file="Intersection/Once" />

### Using an Object

By passing in an Object as the directive's value (instead of a Function), you can control all the options (like threshold) of the Intersection Observer.

<doc-example title="Supplying configuration Object" file="Intersection/ObjectForm" />

### Advanced

Below is a more advanced example of what you can do. The code takes advantage of the HTML `data` attribute. Basically, by setting `data-id` with the index of the element in a loop, this can be retrieved via the passed in `entry` to the handler as `entry.target.dataset.id`. If you are unfamiliar with the `data` attribute you can read more [here](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) about using the `data` attribute.


<doc-example title="Advanced" file="Intersection/Advanced" />

One more advanced example using `v-intersection` to control resources so that only the visible ones are loaded into memory. As the `q-item` becomes intersected the contained `q-card` with associated image is loaded into the DOM and displayed. When the `q-item` is no longer intersected with the container, the associated `q-card` is removed from the DOM. In the example below, a slight delay in loading the `q-card` is added for effect.

<doc-example title="Scrolling Cards" file="Intersection/ScrollingCards" />

## API

<doc-api file="Intersection" />