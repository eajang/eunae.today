---
description: Home office
---

# Day 10. Dive into Code! and Learning JS

```javascript
/**
 * Tagged Template Exercise
 */
function upper(strings,...values) {
  var ret = "";
  for (let i = 0 ; i < strings.length; i++) {
    if (i > 0) {
      ret += String(values[i-1].toUpperCase());
    }
    ret += strings[i];
  }
  return ret;
}


var name = "Eunae",
    twitter = "ejang",
    topic ="JS Study Parts";

console.log(
  upper `Hello ${name} (@${twitter}), welcome to ${topic}!` ===
  "Hello EUNAE (@EJANG), welcome to JS STUDY PARTS!"
);
```

```javascript
/**
 * Declarative pattern which is expected to receive 
 * from getSomeRecords() api
 */
var [
    {
        name: firstName,
        email: firstEmail = "default@email.com"
    },
    {
        name: secondName,
        email: secondEmail = "default@email.com"
    }
] = getSomeRecords();
```

