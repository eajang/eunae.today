# Observables

## Observables Introduction

Observables can model the three common actions;

* Events
* Async Server Requests
* Animations

## Event Subscription

#### Observable.forEach

* Event handler: `event, error, ()`

```javascript
var observableObj = Observable.fromEvent(element, "mousemove");

// subscribe
var subscription = observableObj.forEach(
    // next data
    event => console.log(event),
    // error(optional)
    error => console.error(error),
    // completed(optional) - no argument(no more data)
    () => console.log("done"));

// unsubscribe
subscription.dispose(); 
```

* with Observer obj⤵

```javascript
// subscribe
var subscription = observableObj.forEach({
    // next data
    onNext: event => console.log(event),
    // error(optional)
    onError: error => console.log(error),
    // completed(optional)
    onCompleted: () => console.log("done")
});

// unsubscribe
subscription.dispose(); 
```

=&gt; Observable pushes data into Observer by extension of callbacks

#### Converting DOMEvents to Observables

```javascript
Observable.fromEvent = function(dom, eventName) {
    // returning Observable object
    return {
        forEach: function(observer) {
            var handler = (e) => observer.onNext(e);
            // hook up the handler
            dom.addEventListener(eventName, handler);
            
            // returning Subscription object
            return {
                dispose: function() {
                    // unhook
                    dom.removeEventListener(eventName, handler);
                }
            }
        }
    }
```

## takeUntil

ref: [https://rxjs.dev/api/operators/takeUntil](https://rxjs.dev/api/operators/takeUntil)

* Two Observables
  * Source collection
  * Stop collection
* Unsubscription source until stop observable is omitted.

## mergeAll

* first come first merged

## switchLatest

* switch on the Observable which comes at latest. -&gt; If the new Observable is arrived, the old Observable is cancelled out to be listened.

## Netflix Search









#### 



