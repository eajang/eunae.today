---
description: >-
  These are my notes of keywords that I have learned from the course iOS
  Application Development '17 by RWTH Aachen University in iTunes.
---

# Lecture 02. Introduction to Swift & Xcode

[iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)

## Lecture 02. Intro into Swift & Xcode

### Swift - Characteristics

* Clean syntax
* Optionals
* Tupels and multiple return values
* Type safety
* Generics
* Structs: support mathods, extensions, and protocols
* Powerful error handling

### Swift \(Language\)

1. Variables and Constants
   * `var`: variables
   * `let`: constants
   * Cannot be changed afterwards
   * Cannot be `nil`
   * Automatic type-casting
   * Explicit specifying is also possible.
2. Optionals

   * Can be `nil`
   * `?`  
   * `!` : implicitly unwrapped optionals

   [&gt;&gt; more about **Optionals**](https://app.gitbook.com/@eajang/s/blog/~/edit/drafts/-Lo_rO5xw1RUvwHTnK3V/til/ios-application-developement-itunes/lecture-03.-swift-and-uikit#optionals)\*\*\*\*

3. Tuples
   * Set of variables
   * Multiple types also possible
   * After defining the values in a tuple, cannot change the value in diff. type

### Xcode \(Environment\)

* Playground --- demo video
  * xcodepoj : all setting for the project
* Xcode Debugging

{% tabs %}
{% tab title="Commands usage in Terminal" %}
`po sender`: show information about the current sender \(e.g. the button I pressed\)  
`po (sender as UIButton).titleLable.text`: inspect more detail
{% endtab %}

{% tab title="Edit breakpoint" %}
We can make a condition, ignoring-counts or actions with po in terminal.
{% endtab %}
{% endtabs %}



