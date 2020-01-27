# Building Blocks

## Basic JavaScript

* `forEach()`
  * **consume** the data inside of stream
* `map()`
  * not change the original array
  * make a new result array -&gt; **produce** a stream
  * "replacing"
* `filter()`
  * test every single value
  * create a new array which includes only data that passed the test -&gt; **produce** a stream
  * not change the original array
* `concatAll()`
  * is not JS basic function
  * not recursively flatten
  * 3 dim -&gt; 2 dim, 2 dim -&gt; 1 dim

```javascript
/** Top-rated Movies collection **/
var getTopRatedFilms = user => 
    user.videoLists.
        map(videoList => 
            videoList.videos.
                filter(video => video.rating === 5.0)).
        concatAll();

getTopRatedFilms(user).forEach(film => console.log(film));
```

* `takeUntil()`
  * is not JS basic function
  * Subscribe the stream until the event

```javascript
/** Mouse Drags Collection **/
var getElementDrags = elmt => 
    elmt.mouseDowns.
        map(mouseDown => 
            document.mouseMoves.
                takeUntil(document.mouseUps)).
        concatAll();

getElementDrags(image).forEach(pos => image.position = pos);

```

## Iterator 

```javascript
var iterator = [1, 2, 3].iterator();
console.log(iterator.next())
> {value: 1, done: false}            // current pointed value and true if there is no more value.
```

* `Map`, `Filter` and `ConcatAll` can be implemented using an `Iterator`.
* Consumer pull the data out from producer

## Observer Pattern

* Producer push one item to consumer at a time
* Different semantic from Iterator
* Focus on Use Cases \(UI Event\)

### Observable

{% hint style="info" %}
Observable === collection + Time
{% endhint %}



