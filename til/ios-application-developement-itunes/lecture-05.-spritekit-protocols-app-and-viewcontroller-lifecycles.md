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
        <p>SpriteKit</p>
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

### Lecture 05. SpriteKit, Protocols, App and ViewController LifeCycles

###  <a id="strings"></a>

* 
