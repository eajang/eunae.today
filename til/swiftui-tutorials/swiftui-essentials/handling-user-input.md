---
description: 25. Sep. 2019
---

# Handling User Input

{% embed url="https://developer.apple.com/tutorials/swiftui/handling-user-input" %}

## Filter the List View by a property of state

{% code-tabs %}
{% code-tabs-item title="LandmarkList.swift" %}
```swift
import SwiftUI

struct LandmarkList: View {
    @State var showFavoritesOnly = true        // 1. Define state variable
    
    var body: some View {
        NavigationView {
            List {
                Toggle(isOn: $showFavoritesOnly) {      // 2. Add Toggle
                    Text("Favorites only")
                }
                // 3. Filtering the list
                ForEach(landmarkData) { landmark in
                    if !self.showFavoritesOnly || landmark.isFavorite {
                            NavigationLink(destination: LandmarkDetail(landmark: landmark)) {
                            LandmarkRow(landmark: landmark)
                        }
                    }
                }
            }
        .navigationBarTitle(Text("Landmarks"))
        }
    }
}

struct LandmarkList_Previews: PreviewProvider {
    static var previews: some View {
        ForEach(["iPhone SE", "iPhone XS Max"], id: \.self) { deviceName in
            LandmarkList()
                .previewDevice(PreviewDevice(rawValue: deviceName))
                .previewDisplayName(deviceName)
        }
        
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

1. `@State` property: add a state to a view
2.  Add a toggle to interact with user
   * `$` prefix: access a binding to a state variable or one of its properties.
3. Filter the list using state variables

   * A nested ForEach
     * Combining two or more different groups of dynamic views
     * Combining static and dynamic views in a list 

