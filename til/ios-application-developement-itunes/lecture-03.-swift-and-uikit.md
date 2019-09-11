# Lecture 03. Swift & UIKit

 [iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)

## Lecture 3-1. Swift

### Strings

* Single characters are also of type String `let a = "a"               // 'a' is a String let b: Character = "b"    // 'b' is a Character`
* `==`: Comparison/Equality
* `isEmpty`

### Functions

* Basic Structure

```swift
func functionName(parameters) -> ReturnType {
    // body of the function
}
```

* Function with multiple parameters 

```swift
func functionName(firstNumber: Int, secondNumber: Int) {
    // body of the function
}
functionName(firstNumber: 10, secondName: 5)    // function call
```

* Default parameter values

```swift
func functionName(parameter: String, parameterWithDefaultValue: Int = 0) {
    // body of the function
}
functionName("functionTest")                    // function call without 2. param.
functionName("functionTest", 100)               // function call with 2. param.
```

* Argument labels
  * Use first part of parameter
  * `_` :  call function without label

```swift
func sayHello(to person: String, and anotherPerson: String) {
    print("Hello \(person) and \(anotherPerson)")
}
sayHello(to: "Eunae", and: "Gyumin")            // function call

func sayHelloWithoutLabel(_ person: String, _ anotherPerson: String) {
    print("Hello \(person) and \(anotherPerson)")
}
sayHello("Eunae", "Gyumin")            // function call
```

### Structs

* String, Int, Double, Bool
* Value types \(not reference types such as **classes**\)
* It is possible to **define functions and initializers**\(e.g. `String.init() or String()`\) in struct
* Property observers \([more details](https://docs.swift.org/swift-book/LanguageGuide/Properties.html#ID262)\)

```swift
struct StepCounter {
    var totalSteps: Int = 0 {
        willSet {
            // willSet is called when the new value of totalSteps is passed.
            print("About to set totalSteps to \(newValue)")
        }
        didSet {
            // didSet is called after the value of totalSteps is updated.
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// call 'willSet' - output: About to set totalSteps to 200
// call 'didSet'  - output: Added 200 steps
stepCounter.totalSteps = 360
// call 'willSet' - output: About to set totalSteps to 360
// call 'didSet'  - outputAdded 160 steps
```

### Classes

* Reference types
* Subclass and overriding functions are possible.
  * ⚠ Do everything first in your class and then call initializer of super class.

### Collections

* Groups of objects
* ⚠Value types ⚠

#### 1. Arrays

```swift
var names: [String] = []
var names: Array[String] = []
var names = [String]()
```

#### 2. Dictionaries

```swift
var myDictionary = [String: Int]()            // type of key : type of value
var myDictionary = Dictionary<String, Int>()
var myDictionary: [String: Int] = [:]

Array(myDictionary.keys)      // get an array of all keys in a dictionary
Array(myDictionary.values)    // get an array of all values in a dictionary

if let myValue = myDictionary["myKey"] {
    // do something if "myKey" exists in myDictionary. -> checking optionals
}
```

## Lecture 3-2. Introduction to UIKit

### Overview of UIView

* foundation class for all visual elements
* Subclasses
  * UILabel
  * UIButton
  * UIImageView
  * UIScrollView 
  * ...

### Connection code to ui

{% tabs %}
{% tab title="Outlet" %}
> An **outlet connection** is created when you need to send a message from **your code to a user interface** object in Xcode’s storyboard.
{% endtab %}

{% tab title="Action" %}
> An **action connection** is created when you need to send a message from **a control in the storyboard to your code**.
{% endtab %}
{% endtabs %}

* Reference : [Gan Chau](https://medium.com/@GanChau?source=post_page-----b5331fb233a1----------------------).\(2015\). Medium, _Outlet vs Action Connections in Xcode_. Retrieved from [https://medium.com/@GanChau/outlet-vs-action-connections-in-xcode-b5331fb233a1](https://medium.com/@GanChau/outlet-vs-action-connections-in-xcode-b5331fb233a1)



