---
description: 'Working time: 08:00 ~'
---

# Day 02. Set up and learn up

## More about the product

* Getting familiar with the terminogies of the product
* Repository and task board
* Tech stacks

## About Melody - Introduction

{% hint style="info" %}
[https://melody.js.org/documentation/quickstart/intro](https://melody.js.org/documentation/quickstart/intro)
{% endhint %}

* Rendering
  * only if the component is explicitly changed
* Lifecycle
  * Components' State management
    * Using [**reducer**](https://redux.js.org/basics/reducers/) **`(currentState, action) => nextState`**
    * Updated state is returned
  * Lifecycle hook
    * `dispatch`: actions to reducer ➡️ the resources should be free up
* Handling events
  * `ref` for an element Dom node
  * `bindEvents()`: bind event to element

## About RxJS - Overview

{% hint style="info" %}
Learning RxJS with the [guide](https://rxjs-dev.firebaseapp.com/guide/overview)
{% endhint %}

### Purity

* Function -&gt; as pure as possible

### Flow

* Operators for controlling the events flow through the observables

### Values

* Transforming the values passed through the observables

```javascript
import { fromEvent } from 'rxjs';
import { throttleTime, map, scan } from 'rxjs/operators';

fromEvent(document, 'click')
.pipe(
  throttleTime(1000),
  map(event => event.clientX),                   // pass the value
  scan((count, clientX) => count + clientX, 0)   // transform the value
)
.subscribe(count => console.log(count));
```

