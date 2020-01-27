---
description: 24. Sep. 2019
---

# Building Lists and Navigation

> [https://developer.apple.com/tutorials/swiftui/building-lists-and-navigation](https://developer.apple.com/tutorials/swiftui/building-lists-and-navigation)

![Demo video of tutorial](../../../.gitbook/assets/screenshot-video.gif)

## Sample Data

{% tabs %}
{% tab title="Landmark.swift" %}
```swift
import SwiftUI
import CoreLocation

struct Landmark: Hashable, Codable, Identifiable {
    var id: Int
    var name: String
    fileprivate var imageName: String
    fileprivate var coordinates: Coordinates
    var state: String
    var park: String
    var category: Category
    
    var locationCoordinate: CLLocationCoordinate2D {
        CLLocationCoordinate2D(
            latitude: coordinates.latitude,
            longitude: coordinates.longitude)
    }
    
    enum Category: String, CaseIterable, Codable, Hashable {
        case featured = "Featured"
        case lakes = "Lakes"
        case rivers = "Rivers"
    }
}

extension Landmark {
    var image: Image {
        ImageStore.shared.image(name: imageName)
    }
}

struct Coordinates: Hashable, Codable {
    var latitude: Double
    var longitude: Double
}

```
{% endtab %}

{% tab title="landmarkData.json" %}
```swift
[
    {
        "name": "Turtle Rock",
        "category": "Featured",
        "city": "Twentynine Palms",
        "state": "California",
        "id": 1001,
        "park": "Joshua Tree National Park",
        "coordinates": {
            "longitude": -116.166868,
            "latitude": 34.011286
        },
        "imageName": "turtlerock"
    },
    {
        "name": "Silver Salmon Creek",
        "category": "Lakes",
        "city": "Port Alsworth",
        "state": "Alaska",
        "id": 4,
        "park": "Lake Clark National Park and Preserve",
        "coordinates": {
            "longitude": -152.665167,
            "latitude": 59.980167
        },
        "imageName": "silversalmoncreek"
    },
    {
        "name": "Chilkoot Trail",
        "category": "Rivers",
        "city": "Skagway",
        "state": "Alaska",
        "id": 5,
        "park": "Klondike Gold Rush National Historical Park",
        "coordinates": {
            "longitude": -135.334571,
            "latitude": 59.560551
        },
        "imageName": "chilkoottrail"
    },
    {
        "name": "St. Mary Lake",
        "category": "Lakes",
        "city": "Browning",
        "state": "Montana",
        "id": 8,
        "park": "Glacier National Park",
        "coordinates": {
            "longitude": -113.536248,
            "latitude": 48.69423
        },
        "imageName": "stmarylake"
    },
    {
        "name": "Twin Lake",
        "category": "Lakes",
        "city": "Twin Lakes",
        "state": "Alaska",
        "id": 11,
        "park": "Lake Clark National Park and Preserve",
        "coordinates": {
            "longitude": -153.849883,
            "latitude": 60.641684
        },
        "imageName": "twinlake"
    },
    {
        "name": "Lake McDonald",
        "category": "Lakes",
        "city": "West Glacier",
        "state": "Montana",
        "id": 6,
        "park": "Glacier National Park",
        "coordinates": {
            "longitude": -113.934831,
            "latitude": 48.56002
        },
        "imageName": "lakemcdonald"
    },
    {
        "name": "Charley Rivers",
        "category": "Rivers",
        "city": "Eaking",
        "state": "Alaska",
        "id": 1,
        "park": "Charley Rivers National Preserve",
        "coordinates": {
            "longitude": -143.122586,
            "latitude": 65.350021
        },
        "imageName": "yukon_charleyrivers"
    },
    {
        "name": "Icy Bay",
        "category": "Lakes",
        "city": "Icy Bay",
        "state": "Alaska",
        "id": 2,
        "park": "Wrangell-St. Elias National Park and Preserve",
        "coordinates": {
            "longitude": -141.518167,
            "latitude": 60.089917
        },
        "imageName": "icybay"
    },
    {
        "name": "Rainbow Lake",
        "category": "Lakes",
        "city": "Willow",
        "state": "Alaska",
        "id": 3,
        "park": "State Recreation Area",
        "coordinates": {
            "longitude": -150.086103,
            "latitude": 61.694334
        },
        "imageName": "rainbowlake"
    },
    {
        "name": "Hidden Lake",
        "category": "Lakes",
        "city": "Newhalem",
        "state": "Washington",
        "id": 7,
        "park": "North Cascades National Park",
        "coordinates": {
            "longitude": -121.17799,
            "latitude": 48.495442
        },
        "imageName": "hiddenlake"
    },
    {
        "name": "Chincoteague",
        "category": "Rivers",
        "city": "Chincoteague",
        "state": "Virginia",
        "id": 9,
        "park": "Chincoteague National Wildlife Refuge",
        "coordinates": {
            "longitude": -75.383212,
            "latitude": 37.91531
        },
        "imageName": "chincoteague"
    },
    {
        "name": "Lake Umbagog",
        "category": "Lakes",
        "city": "Errol",
        "state": "New Hampshire",
        "id": 10,
        "park": "Umbagog National Wildlife Refuge",
        "coordinates": {
            "longitude": -71.056816,
            "latitude": 44.747408
        },
        "imageName": "umbagog"
    }
]

```
{% endtab %}
{% endtabs %}

* `fileprivate`
  * When you want to access your code within the same file from different classes or structs.

## Create the Row View and Customize the Row Preview

{% code title="LandmarkRow.swift" %}
```swift
import SwiftUI

struct LandmarkRow: View {
    var landmark: Landmark
    
    var body: some View {
        HStack {
            landmark.image
                .resizable()
                .frame(width: 50, height: 50)
            Text(landmark.name)
        }
    }
}

struct LandmarkRow_Previews: PreviewProvider {
    static var previews: some View {
        Group {
            LandmarkRow(landmark: landmarkData[0])
            LandmarkRow(landmark: landmarkData[1])
        }
        .previewLayout(.fixed(width: 300, height: 70)) // set the size of a row
    }
}

```
{% endcode %}

* `Group` :a container for grouping view content.
  * XCode renders the group's child views as separate previews in the canvas.

## Create the dynamically-generated List of Landmarks and Set Up Navigation Between List and Detail

{% code title="LandmarkList.swift" %}
```swift
import SwiftUI

struct LandmarkList: View {
    var body: some View {
        NavigationView {    // Use NavigationView
            List(landmarkData) { landmark in
                NavigationLink(destination: LandmarkDetail()) {
                    // Generate dynamically by returning a LandmarkRow
                    LandmarkRow(landmark: landmark)
                }
            }
        .navigationBarTitle(Text("Landmarks"))
        }
    }
}

struct LandmarkList_Previews: PreviewProvider {
    static var previews: some View {
        LandmarkList()
    }
}

```
{% endcode %}

### Identifiable protocol

1. By passing along with the data a key path to property that unizuely identifies each element\(e.g. id\)
2. [By making the data type conform to the Identifiable protocol](building-lists-and-navigation.md#sample-data)



