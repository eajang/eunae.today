---
description: '28. Sep. 2019, 05. Oct. 2019'
---

# Animating Views and Transitions

{% embed url="https://developer.apple.com/tutorials/swiftui/animating-views-and-transitions" %}

{% tabs %}
{% tab title="HikeView.swift" %}
```swift
...
extension AnyTransition {
    static var moveAndFade: AnyTransition {
        var insertion = AnyTransition.move(edge: .trailing)
            .combined(with: .opacity)
        var removal = AnyTransition.scale
            .combined(with: .opacity)
        return .asymmetric(insertion: insertion, removal: removal)
    }
}

struct HikeView: View {
    var hike: Hike
    @State private var showDetail = false
    
    var body: some View {
        VStack {
            HStack {
                HikeGraph(hike: hike, path: \.elevation)
                    .frame(width: 50, height: 30)
                    .animation(nil)
                
                VStack(alignment: .leading) {
                    Text(verbatim: hike.name)
                        .font(.headline)
                    Text(verbatim: hike.distanceText)
                }
                
                Spacer()

                Button(action: {
                    withAnimation {
                        self.showDetail.toggle()
                    }
                }) {
                    Image(systemName: "chevron.right.circle")
                        .imageScale(.large)
                        .rotationEffect(.degrees(showDetail ? 90 : 0))
                        .scaleEffect(showDetail ? 1.5: 1)
                        .padding()
                }
            }
            if showDetail {
                HikeDetail(hike: hike)
                    .transition(.slide)
            }
        }
    }
}
...
```
{% endtab %}
{% endtabs %}

* `func animation(_ animation: Animation?) -> some View` : animates any changes to animatable properties\(color, opacity, rotation, size ... \) of the view.
* basic animations
  * predefined or custom easing
  * spring
  * fluid animations
* `func withAnimation<Result>(_ animation: Animation? = .default, _ body: () throws -> Result) rethrows -> Result` : returns the result of recomputing the view's body with the provided animation.

### View Transitions

* defualt: on/offscreen by fading in/out
* `func transition(_ t: AnyTransition) -> some View` : gives a transition to a view
  * _identity_: returns the unmodified input view as the output view
  * _opacity_: insertion and removal by controlling transparency and opaqueness
  * _scale_
  * _slide_
* `func combined(with other: AnyTransition) -> Any Transition` : combines transition with another, returning a new combined transition
* `static func asymmtric(insertion: AnyTransition, removal: AnyTransition) -> AnyTransition` : provide diff. transitions for when the view appears and disappears.





