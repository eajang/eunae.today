# Observable

### Observable

**lazy** Push collections of multiple values

### Pull vs Push

protocol; describes the way to communicate btw a data _**Producer**_ and a data _**Consumer**_

#### Pull

* Consumer decides when to receive data from producer
* Producer doesn't know the timing
* Single return value from producer

#### Push

* Producer decides when to send data to consumer
* Consumer doesn't know the timing
* Single return value from producer
* Observables\(producer\) - a push system; a producer of multiple values, pushing them to Observers\(consumers\)

### Observables as generalizations of functions

* Available to deliver values either synchronously or asynchronously

#### Creating Observables

```javascript
import { Observable } from 'rxjs';

const observable = new Observable(function subscribe(subscriber) {
  const id = setInterval(() => {
    subscriber.next('hi')
  }, 1000);
});
```

* creation functions; like, of, interval, from, etc.

#### Subscribing to Observables

```javascript
observable.subscribe(x => console.log(x));
```

* `subscribe` - simply start "Observable execution"

#### Executing Observables

#### Disposing Observables Executions







