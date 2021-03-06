---
description: >-
  These are my notes of keywords that I have learned from the course iOS
  Application Development '17 by RWTH Aachen University in iTunes.
---

# Lecture 08.Building Complex Input Screens, Closures, and Animations

 [iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)​

## Lecture 8-1. Building Complex Input Screens

![Demo for what I made with the video](../../.gitbook/assets/screencast-2019-09-17-17-14-13.gif)

> Sources: [https://github.com/eajang/iOS-Example-ComplexInputScreens](https://github.com/eajang/iOS-Example-ComplexInputScreens)

## Lecture 8-2. Closures

### Closures

* self-contained blocks of functionality
* "Anonymous functions"
* make code shorter and more readable
* basic structure `{ (parameters) -> return type in     statements }`
* no return value: use `Void`
* Example

```swift
// Function
func sumFunction(numbers: [Int]) {
    var total = 0
    // Code
    return total
}
// Function usage
let sum = sumFunction(numbers: [4, 24, 45, 12])

// Closure
let sumClosure = { (numbers: [Int]) -> Int in
    var total = 0
    // Code
    return total
}
// Closure usage
let sum = sumClosure([4, 24, 45, 12])
```

### Trailing Closure

* Closure as the only argument:

```swift
let sortedTracks = tracks.sorted { (firstTrack, secondTrack) -> Bool in
    return firstTrack.starRating < secondTrack.starRating
}
```

* Closure as the last argument:

```swift
func performRequest(url: String, response: (Int) -> Void) { }
// Usage
performRequest(url: "https://www.apple.com") { (data) in
    print(data)
}
```

### Simplifying Closures

```swift
let sortedTracks = tracks.sorted { (firstTrack, secondTrack) -> Bool in
    return firstTrack.starRating < secondTrack.starRating
}
// Simplifying - Infer the return type
let sortedTracks = tracks.sorted { (firstTrack, secondTrack) in
    return firstTrack.starRating < secondTrack.starRating
}
// Simplifying - Use placeholder arguments
let sortedTracks = tracks.sorted {
    return $0.starRating < $1.starRating
}
// Simplifying - If the closure has just one statement:
let sortedTracks = tracks.sorted {$0.starRating < $1.starRating}
// Operator Methods
// Two parameters of String, return a value of type Bool
let sortedNames = names.sorted (by: >)
```

### Map

* `map(_:)`  : call the closure expression once for each item in the array.
* Example

```swift
// names is an array of first names
let fullNames = names.map { (name) -> String in
    return name + " Smith"
}
```

### Filter

* `filter(_:)` : call the closure expression once for each item in the array.
* Example

```swift
let numbersLessThan20 = numbers.filter { (number) -> Bool in
    return number < 20
}
```

### Reduce

* `reduce(_:_:)` : returns the result of combining the elements of the sequence

  `reduce(_ initialResult: Result, _ nextPartialResult:(Result, Element) throws  
  -> Result) rethrows -> Result)`

* Example

```swift
let total = numbers.reduce(0) { (currentTotal, newValue) -> Int in
    return currentTotal + newValue
}
// Short version
let total = numbers.reduce(0, {$0 + $1})
```

###  Capturing Values

* A nested function can capture any of its outer function's arguments, constants and variables.

## Lecture 8-3. Practical Animation

### UIView Animations 

```swift
// Animation Closures:
animate(withDuration:animations:)
animate(withDuration:animations:completion:)
animate(withDuration:delay:options:animations:completion:)

// Example 
UIView.animate(withDuration: 2.0) {    // seconds
    aView.alpha = 0.3
}
```

* Example of simple animation

![Simple animation](../../.gitbook/assets/simpleanimationdemo.gif)

```swift
import UIKit
import PlaygroundSupport

let liveViewFrame = CGRect(x: 0, y: 0, width: 300, height: 300)
let liveView = UIView(frame: liveViewFrame)
liveView.backgroundColor = .black
PlaygroundPage.current.liveView = liveView

let smallFrame = CGRect(x: 0, y: 0, width: 100, height: 100)
let square = UIView(frame: smallFrame)
square.backgroundColor = .green
liveView.addSubview(square)

// Animation
UIView.animate(withDuration: 3, animations: {
    square.backgroundColor = .orange
    square.frame = CGRect(x: 100, y: 100, width: 200, height: 200)
})
```

