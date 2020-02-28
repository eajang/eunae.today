---
description: 25. Sep. 2019
---

# Handling User Input

{% embed url="https://developer.apple.com/tutorials/swiftui/handling-user-input" %}

![Demo](../../../.gitbook/assets/screenshot-favoritebutton.gif)

## Filter the List View - Approach 1. by @State property

{% code title="LandmarkList.swift" %}
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
{% endcode %}

1. `@State` property: add a state to a view
2.  Add a toggle to interact with user
   * `$` prefix: access a binding to a state variable or one of its properties.
3. Filter the list using state variables

   * A nested ForEach
     * Combining two or more different groups of dynamic views
     * Combining static and dynamic views in a list 

## Filter the List View - Approach 2. Using an Observable Object for Storage

> To prepare for the user to control which particular landmarks are favorites, you will first store the landmark data in a **observable** object.

{% code title="UserData.swift" %}
```swift
import SwiftUI
import Combine

final class UserData: ObservableObject {
    @Published var showFavoritesOnly = false
    @Published var landmarks = landmarkData
}
```
{% endcode %}

### ObservableObject protocol from Combine framework

SwiftUI ...

* subscribes to the observable object
* updates any views that need refreshing when the data changes.

An observable object ... 

* needs to **publish** by `@Publisched` ****any changes to its data.
* The changes can be picked up by the subscribers

{% tabs %}
{% tab title="LandmarkList.swift" %}
```swift
struct LandmarkList: View {
    @EnvironmentObject var userData: UserData    // Use environmentObject
    
    var body: some View {
        NavigationView {
            List {
                Toggle(isOn: $userData.showFavoritesOnly) {
                    Text("Favorites only")
                }
                ForEach(userData.landmarks) { landmark in
                    if !self.userData.showFavoritesOnly || landmark.isFavorite {
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
        LandmarkList()
            .environmentObject(UserData())
    }
}
```
{% endtab %}

{% tab title="LandmarkDetail.swift" %}
```swift
struct LandmarkDetail: View {
    @EnvironmentObject var userData: UserData    // Use environmentObject
    var landmark: Landmark
    
    // Use landmarkIndex when accessing or updating the landmark's favorite status,
    // so that you're always accessing the correct version of that data.
    var landmarkIndex: Int {
        userData.landmarks.firstIndex(where: { $0.id == landmark.id })!
    }
    ...
```
{% endtab %}
{% endtabs %}

### `@EnvironmentObject`

* Shares the model property anywhere in the app.
* Automatically updated when the data is changed.
* It should be supplied by the ancester view
* Simple to use with `ObservableObject`

## Create a Favorite Button and make it works!

{% code title="LandmarkDetail.swift" %}
```swift
...
HStack {
    Text(landmark.name)
        .font(.title)
            
    Button(action: {
        self.userData.landmarks[self.landmarkIndex].isFavorite.toggle()
    }) {
            if self.userData.landmarks[self.landmarkIndex].isFavorite {
                Image(systemName: "star.fill")
                    .foregroundColor(.yellow)
            } else {
                Image(systemName: "star")
                    .foregroundColor(.gray)
            }
        }
    }
...        
```
{% endcode %}

