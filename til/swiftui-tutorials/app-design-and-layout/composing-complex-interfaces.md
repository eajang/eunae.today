---
description: 05. Oct. 2019
---

# Composing Complex Interfaces

{% embed url="https://developer.apple.com/tutorials/swiftui/composing-complex-interfaces" %}

![](../../../.gitbook/assets/screenshot01.gif)

{% tabs %}
{% tab title="Home.swift" %}
```swift
...
struct CategoryHome: View {
    var categories: [String: [Landmark]] {
        Dictionary(
            grouping: landmarkData,
            by: { $0.category.rawValue }
        )
    }
    
    var featured: [Landmark] {
        landmarkData.filter { $0.isFeatured }
    }
    
    @State var showingProfile = false
    
    var profileButton: some View {
        Button(action: { self.showingProfile.toggle() }) {
            Image(systemName: "person.crop.circle")
                .imageScale(.large)
                .accessibility(label: Text("User Profile"))
                .padding()
        }
    }
    
    var body: some View {
        NavigationView {
            List {
                FeaturedLandmarks(landmarks: featured)
                    .scaledToFill()
                    .frame(height: 200)
                    .clipped()
                    .listRowInsets(EdgeInsets())
                ForEach(categories.keys.sorted(), id: \.self) { key in
                    CategoryRow(categoryName: key, items: self.categories[key]!)
                }
                .listRowInsets(EdgeInsets())
                
                NavigationLink(destination: LandmarkList()) {
                    Text("See All")
                }
            }
            .navigationBarTitle(Text("Featured"))
            .navigationBarItems(trailing: profileButton)
            .sheet(isPresented: $showingProfile) {    // Use modal
                Text("User Profile")
            }
        }
    }
}

struct FeaturedLandmarks: View {
    var landmarks: [Landmark]
    var body: some View {
        landmarks[0].image.resizable()
    }
}
...
```
{% endtab %}

{% tab title="CategoryRow.swift" %}
```swift
...
struct CategoryRow: View {
    var categoryName: String
    var items: [Landmark]
    
    var body: some View {
        VStack(alignment: .leading) {
            Text(self.categoryName)
                .font(.headline)
                .padding(.leading, 15)
                .padding(.top, 5)
            
            ScrollView(.horizontal, showsIndicators: false) {
                HStack(alignment: .top, spacing: 0) {
                    ForEach(self.items) { landmark in
                        NavigationLink(
                            destination: LandmarkDetail(
                                landmark: landmark
                            )
                        ) {
                            // **
                            CategoryItem(landmark: landmark)
                        }    
                    }
                }
            }
            .frame(height: 185)
        }
    }
}

struct CategoryItem: View {
    var landmark: Landmark
    var body: some View {
        VStack(alignment: .leading) {
            landmark.image
                .renderingMode(.original)    // ***
                .resizable()
                .frame(width: 155, height: 155)
                .cornerRadius(5)
            Text(landmark.name)
                .foregroundColor(.primary)    // ***
                .font(.caption)
        }
        .padding(.leading, 15)
    }
}

struct CategoryRow_Previews: PreviewProvider {
    static var previews: some View {
        CategoryRow(
            categoryName: landmarkData[0].category.rawValue,
            items: Array(landmarkData.prefix(4))
        )
    }
}
```
{% endtab %}
{% endtabs %}

> In Xcode 11 beta 6, if you nest a `ScrollView` inside a `List` and that `ScrollView` contains a `NavigationLink`, the links won’t navigate to the destination when tapped by the user.

### Dictionary

A collection with key-value pairs. A dictionary is type of hash table

* Fast access to the entries
* Key is a hashable type such as string or number.
* Value can be any object.
* `init(grouping:by:)`: Generic Initializer, keying off the property
  * Parameters
    * grouping values: A sequence of values to group into a dictionary
    * by keyForValue: A closure that returns a key for each element in values.

### Button

* `init(action:label:)` : Initializer
  * Parameters
    * action: to perform when self is triggered 
    * label: a view that describes the effect of calling on Trigger

### NavigationLink

A button that triggers a navigation presentation when pressed.

* `init(destination:label:)` : Initializer
  * \(\*\*\) **CategoryItem** itself is the label for the button.
  * \(\*\*\*\) Text as label renders using environment's accent color and images may render as template images.



