---
description: >-
  These are my notes of keywords that I have learned from the course iOS
  Application Development '17 by RWTH Aachen University in iTunes.
---

# Lecture 06. TableView Demo

 [iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)​

## Lecture 06. TableView Demo - "Emoji Dictionary"

### Step 1. Make TableView and show the data on the table view

![Demo for first step](../../.gitbook/assets/screencast-2019-09-16-17-14-16.gif)

{% code-tabs %}
{% code-tabs-item title="Emoji.swift" %}
```swift
// Data Model of our app
struct Emoji {
    var symbol: String
    var name: String
    var description: String
    var usage: String
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="EmojiTableViewController.swift" %}
```swift
class EmojiTableViewController: UITableViewController {
    // Example data set
    var emojis: [Emoji] = [
        Emoji(symbol: "😀", name: "Grinning Face", description: "A typical smiley face.", usage: "happiness"),
        Emoji(symbol: "😕", name: "Confused Face", description: "A confused, puzzled face.", usage: "unsure what to think; displeasure"),
        Emoji(symbol: "😍", name: "Heart Eyes", description: "A smiley face with hearts for eyes.", usage: "love of something; attractive"),
        Emoji(symbol: "👮‍♀️", name: "Police Officer", description: "A police officer wearing a blue cap with a gold badge.", usage: "person of authority"),
        Emoji(symbol: "🐢", name: "Turtle", description: "A cute turtle.", usage: "Something slow"),
        Emoji(symbol: "🐘", name: "Elephant", description: "A gray elephant.", usage: "good memory"),
        Emoji(symbol: "🍝", name: "Spaghetti", description: "A plate of spaghetti.", usage: "spaghetti"),
        Emoji(symbol: "🎲", name: "Die", description: "A single die.", usage: "taking a risk, chance; game"),
        Emoji(symbol: "⛺️", name: "Tent", description: "A small tent", usage: "camping"),
        Emoji(symbol: "📚", name: "Stack of Books", description: "Three colored books stacked on each other", usage: "homework, studying"),
        Emoji(symbol: "💔", name: "Broken Heart", description: "A red, broken heart.", usage: "extreme sadness"),
        Emoji(symbol: "💤", name: "Snore", description: "Three blue \'z\'s.", usage: "tired, sleepiness"),
        Emoji(symbol: "🏁", name: "Checkered Flag", description: "A black-and-white checkered flag.", usage: "completion")
        
    ]
    
    ...
    
    override func numberOfSections(in tableView: UITableView) -> Int {
        // one section
        return 1
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        // number of rows in each section
        if section == 0 {
            return emojis.count
        } else {
            return 0
        }
    }

    // indexPath: description of the cell that you want to display in each row
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        // Reuse the cell which is not shown anymore
        let cell = tableView.dequeueReusableCell(withIdentifier: "EmojiCell", for: indexPath)
        
        let emoji = emojis[indexPath.row]
        // Configure the cell...
        cell.textLabel?.text = "\(emoji.symbol) - \(emoji.name)"
        cell.detailTextLabel?.text = emoji.description
        
        return cell
    }
    
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

![Main.storyboard](../../.gitbook/assets/grafik%20%283%29.png)

### Step 2. Add function for tap event.

#### Implementation method from the delegate-protocol

{% code-tabs %}
{% code-tabs-item title="EmojiTableViewController.swift" %}
```swift
...
// tap-event
override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let emoji = emojis[indexPath.row]
        print("\(emoji.symbol) \(indexPath)")        // example output: 😀 [0, 0]
}
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}



