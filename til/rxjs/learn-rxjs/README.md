---
description: 'https://www.learnrxjs.io + https://rxjs-dev.firebaseapp.com/guide/overview'
---

# Learn RxJS

## Introduction

{% hint style="info" %}
Learning RxJS with the [guide](https://rxjs-dev.firebaseapp.com/guide/overview) and [Learn RxJS](https://www.learnrxjs.io)
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

