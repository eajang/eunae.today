# Basic Javascript

## Notation

### The spread syntax\(...\)

Expand an iterable\(e.g. array\)

```javascript
console.log(...[1, 2, 3]);  // 1, 2, 3
console.log(...'Hello');    // H e l l o
```

```javascript
var arr = ['C', 'D'];
var arr2 = ['A', 'B', arr, 'E', 'F'];

console.log(arr2);        // ['A', 'B', ['C', 'D'], 'E', 'F']
```

```javascript
var arr = ['C', 'D'];
var arr2 = ['A', 'B', ...arr, 'E', 'F'];

console.log(arr2);        // ['A', 'B', 'C', 'D', 'E', 'F']
```

{% hint style="info" %}
Reference  
-  [https://codeburst.io/javascript-es6-the-spread-syntax-f5c35525f754](https://codeburst.io/javascript-es6-the-spread-syntax-f5c35525f754)
{% endhint %}

