# Lecture 03. Swift & UIKit

 [iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)

## Lecture 3-1. Swift

### Variables with nil

Use `nil` when the value is undefined or there is no information about the variable yet.

### Optionals

* Optionals contains two sets; nil or value of other types\(including custom-type\).
* force-upwrap operator **`!`**
  * ⚠ Before unwrapping an optional we need to check if the value is not nil⚠

```swift
if optionalVariable != nil { 
   let unwrappedVariable = optionalVariable!
   // do something
} 
// shorter version
if let unwrappedVariable = optionalVariable {
   // do something
}
```

* Unwrapping multiple optionals by `nested if` or concatenation by `,`
* [Unwrapping nested optionals](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html#ID247)
* possible to use in functions as parameters or return type
* Failable initializers \(e.g. file-loading\)

```swift
init?() {
    return nil
}
```

### Type Casting

* `as?` :boolean statements
* `as!`: force cast. Use only when you are certain that the specific type is correct.

### The Any Type

* represent an instance of **any** type - usually used for array of different types of elements
* **AnyObject**: represent **any** **class** within Swift \(not structure\)

### The Guard Command

```swift
guard condition else {
    // false: execute some code
}
// true: execute some code
```

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

### Gesture Recognizers

* touch gestures
* can be included using the interface builder and code
* custom touch input by basic three events; touch began/touch moved/touch ended

```swift
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) { }
override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) { }
override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) { }
```

