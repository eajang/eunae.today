---
description: >-
  These are my notes of keywords that I have learned from the course iOS
  Application Development '17 by RWTH Aachen University in iTunes.
---

# Lecture 05. SpriteKit, Protocols, App and ViewController LifeCycles

 [iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)​

## Lecture 5-1. Sprite Kit

### App Architecture with Sprite Kit

<table>
  <thead>
    <tr>
      <th style="text-align:center"></th>
      <th style="text-align:center"></th>
      <th style="text-align:center"></th>
      <th style="text-align:center"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">
        <p>2D Graphics</p>
        <p>and Imaging</p>
      </td>
      <td style="text-align:center">
        <p>Standards-Based</p>
        <p>3D Graphics</p>
      </td>
      <td style="text-align:center">
        <p>High Efficiency</p>
        <p>GPU Access</p>
      </td>
      <td style="text-align:center">Scene Graphs</td>
    </tr>
    <tr>
      <td style="text-align:center">
        <p>Core Animation</p>
        <p>Core Image</p>
        <p>Core Graphics</p>
      </td>
      <td style="text-align:center">Open GL ES</td>
      <td style="text-align:center">Metal</td>
      <td style="text-align:center">
        <p><b>SpriteKit</b>
        </p>
        <p>SceneKit</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:center">GPU</td>
      <td style="text-align:center"></td>
      <td style="text-align:center"></td>
      <td style="text-align:center"></td>
    </tr>
  </tbody>
</table>### Sprite Kit

* 2D gaming engine
* Object-oriented

### 3 major elements

* Objects
* Actions
* Physics

### Root Object: SKScene

* SKView
  * all of the rendering group including all information of trigger for events
  * create SKScene
* SKScene: game scene
  * SKNodes: upper level of SKScene, includes SKShapeNode, SKEffectNode, SKCropNode, ...
  * apply actions and physics to SKNodes
  * every scene has their own physicsWorld\(e.g. gravity\)
* SKPhysicsBody
  * every SKNodes has the property physicsBody which has nil. 

### Implementation \(by demo\)

```swift
override func didMove(to view: SKView) {
    // Set background
    // Add the element with SKNode and set name, position, scale, child ect.
    // Add animations (in the demo used SKEmitterNode for adding thrust)
    // Set Basic Physics parameters
    // ...
}

// Touch Input
override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) { }

// Render Loop
override func update(_ currentTime: TimeInterval) { }

// Function for creating an object which is created in the game by some event.
func createSomething() {
    let something = SKSpriteNode.init()
    ...
    // Give actions to something(object)
    // For example: 
    let moveAction = SKAction.move(by: CGVector.init(dx: 0, dy: -self.size.height), duration: 5)
    let removeAction = SKAction.removeFromParent()
    // Connect actions to something(object)
    something.run(SKAction.sequence([moveAction, removeAction]))
}
```

## Lecture 5-2. Swift Protocols and Extensions

### Protocols

* a blueprint of functionality \(similar to Interface in Java\) e.g. `CustomStringConvertible`, `Equatable`, `Comparable`, ...         \(can define my own print command using protocol\)
* Example of `Equatable`

```swift
struct Employee: Equatable {
    var firstName: String
    var lastName: String
    var jobTitle: String
    // Implement my own equals-function
    static func == (lhs: Employee, rhs: Employee) -> Bool {
        return lhs.firstName == rhs.firstName &&
                lhs.lastName == rhs.lastName &&
                lhs.jobTitle == rhs.jobTitle
    }
}
```

* creating Protocol

```swift
protocol FullyNamed {
    var fullName: String { get } // get is property: readable-value
    func sayFullName()
}
// usage
struct Person: FullyNamed {
    var firstName: String
    var lastName: String
    
    var fullName: String {
        return "\(firstName) \(lastName)"
    }
    func sayFullName() {
        print(fullName)
    }
}
```

### Delegation

* Design pattern that delegates functionality an instance of a class or structure
* Implemented using Protocols
* Commonly used in UIKit
  * UITableViewDelegate, UIPickerViewDelegate
* Often provide optional protocol requirements \( != normal protocol\)

### Extensions

* Add **functionality** to types that are already defined as follows:

```swift
// UIColor: basic class which represents color for ios 
extension UIColor {
    static var favoriteColor: UIColor {
        return UIColor(red: 0.5, green: 0.1, blue: 0.5, alpha: 1.0)
    }
}
```

* Affects to the entire project overall
* Cannot add properties. It means that it cannot increase the size of the object \(memory\)

## Lecture 5-3. App and ViewController LifeCycles

### UIView Controllers

* Tab Bar Controller
  * Each tab is completely independent \(not connected to each other\)

### ScrollView

* UIScrollView
  * Parent of UITableView
* `.frames` property
  * Where is the ScrollView on the screen?
* `.contentSize` property
  * How large is the scrollable area?
  * Setting the contenSize: the size of SubView.frame
* ScrollView with StackView
* Content Insets
  * define the padding of scroll view `let contentInsets = UIEdgeInsetsMake(0.0, 0.0, 300, 0.0) self.theScrollView.contentInset = contentInsets self.theScrollView.scrollIndicatorInsets = contentInsets` 
* UIScrollViewDelegate

### View Controller Life Cycle

![Life Cycle of View Controller](../../.gitbook/assets/grafik.png)

> [https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/WorkWithViewControllers.html](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/WorkWithViewControllers.html)

### App Life Cycle

```text

```

![Life Cycle of Application](../../.gitbook/assets/grafik%20%281%29.png)

> [https://developer.apple.com/documentation/uikit/app\_and\_environment/managing\_your\_app\_s\_life\_cycle](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle)

* Foreground
  * Launch Screen UI\(Inactive\) and App UI\(Active\)
* Background
  * storing, managing network connection ... 
* Application delegate
  * You can acess or get notification of different states in Application delegate

![AppDelegate.swift](../../.gitbook/assets/grafik%20%282%29.png)

### MVC in iOS

#### View

* Storyboard
* updated by controller
* delivers 'User action' to controller

#### Model

* Model Classes
* Persistent Storage
* updated by controller
* notify to controller

#### Controller

* ViewController
* ModelController

