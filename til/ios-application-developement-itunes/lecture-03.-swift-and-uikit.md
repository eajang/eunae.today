# Lecture 03. Swift & UIKit

[iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)

## Lecture 03. Swift & UIKit

### Xcode Debugging

{% tabs %}
{% tab title="Command usage in terminal" %}
`po sender`: show information about the current sender \(e.g. the button I pressed\)  
`po (sender as UIButton).titleLable.text`: inspect more detail
{% endtab %}

{% tab title="Edit breakpoints" %}
We can make a condition, ignoring-counts or actions with po in terminal.
{% endtab %}
{% endtabs %}

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
* Property observers

```swift
struct StepCounter {
    var totalSteps: Int = 0 {
        willSet {
            print("About to set totalSteps to \(newValue)")
        }
        didSet {
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
```

