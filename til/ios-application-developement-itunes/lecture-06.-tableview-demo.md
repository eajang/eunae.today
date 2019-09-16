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

![Main.storyboard](../../.gitbook/assets/grafik%20%284%29.png)

### Step 2. Add Reaction

#### Tap-Event: Implementation method from the delegate-protocol

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

#### Rearrange the cells

![Demo for rearranging](../../.gitbook/assets/screencast-2019-09-16-18-41-06.gif)

{% code-tabs %}
{% code-tabs-item title="EmojiTableViewController.swift" %}
```swift
...
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Uncomment the following line to preserve selection between presentations
        // self.clearsSelectionOnViewWillAppear = false

        // Uncomment the following line to display an Edit button in the navigation bar for this view controller.
        self.navigationItem.leftBarButtonItem = self.editButtonItem
    }

...
    // indexPath: description of the cell that you want to display in each row
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        ...
        // enable to reorder the cells
        cell.showsReorderControl = true
        
        return cell
    }
...
    // Override to support rearranging the table view.
    override func tableView(_ tableView: UITableView, moveRowAt fromIndexPath: IndexPath, to: IndexPath) {
        let movedEmoji = emojis.remove(at: fromIndexPath.row)
        emojis.insert(movedEmoji, at: to.row)
        tableView.reloadData()
    }
    
    // Remove the minus button on the leftside in editing mode
    override func tableView(_ tableView: UITableView, editingStyleForRowAt indexPath: IndexPath) -> UITableViewCell.EditingStyle {
        return .none
    }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Step 3. Add remove function in editing mode

![Demo for removing](../../.gitbook/assets/screencast-2019-09-16-20-28-51.gif)

{% code-tabs %}
{% code-tabs-item title="EmojiTableViewController.swift" %}
```swift
...
    // Override to support editing the table view.
    override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        if editingStyle == .delete {
            // Delete the row from the data source
            emojis.remove(at: indexPath.row)
            tableView.deleteRows(at: [indexPath], with: .fade)
        }
    }
...
    // Remove the minus symbol on the leftside in editing mode
    override func tableView(_ tableView: UITableView, editingStyleForRowAt indexPath: IndexPath) -> UITableViewCell.EditingStyle {
        return .delete
    }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Step 4. Edit and Add an Emoji

![Demo for editing and adding](../../.gitbook/assets/screencast-2019-09-16-21-25-41.gif)

![Main.storyboard \(making sagues with static table view\)](../../.gitbook/assets/grafik%20%281%29.png)

{% code-tabs %}
{% code-tabs-item title="EmojiTableViewController.swift" %}
```swift
...
    // MARK: - Navigation

    // In a storyboard-based application, you will often want to do a little preparation before navigation
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // Get the new view controller using segue.destination.
        // Pass the selected object to the new view controller.
        
        if segue.identifier == "EditEmoji" {
            let indexPath = tableView.indexPathForSelectedRow!
            let emoji = emojis[indexPath.row]
            
            let navigationController = segue.destination as! UINavigationController
            let addEditEmojiTableViewController = navigationController.viewControllers.first as! AddEditEmojiTableViewController
            
            addEditEmojiTableViewController.emoji = emoji
        }
    }
 
    @IBAction func unwindToEmojiTableViewController(segue: UIStoryboardSegue) {
        guard segue.identifier == "saveUnwind" else {
            return
        }
        
        // Where the segue started
        let sourceViewController = segue.source as! AddEditEmojiTableViewController
        
        if let emoji = sourceViewController.emoji {
            // Check whether the emoji edited or created
            if let selectedIndexPath = tableView.indexPathForSelectedRow {
                // Edited emoji
                emojis[selectedIndexPath.row] = emoji
                tableView.reloadRows(at: [selectedIndexPath], with: .none)
            } else {
                // Created emoji
                let newIndexPath = IndexPath(row: emojis.count, section: 0)
                emojis.append(emoji)
                tableView.insertRows(at: [newIndexPath], with: .automatic)
            }
        }
    }

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="AddEditEmojiTableViewController.swift" %}
```swift
...
    @IBOutlet weak var symbolTextField: UITextField!
    @IBOutlet weak var nameTextField: UITextField!
    @IBOutlet weak var descriptionTextField: UITextField!
    @IBOutlet weak var usageTextField: UITextField!
    
    @IBOutlet weak var saveButton: UIBarButtonItem!
    
    var emoji: Emoji?
    
    override func viewDidLoad() {
        super.viewDidLoad()

        if let emoji = emoji {          // unwrapping optionals
            symbolTextField.text = emoji.symbol
            nameTextField.text = emoji.name
            descriptionTextField.text = emoji.description
            usageTextField.text = emoji.usage
        }
        
        updateSaveButtonState()
        
        ...
    }
    
    // Enable save button if all of the textfield is not empty
    func updateSaveButtonState() {
        let symbolText = symbolTextField.text ?? ""
        let nameText = nameTextField.text ?? ""
        let descriptionText = descriptionTextField.text ?? ""
        let usageText = usageTextField.text ?? ""
        
        saveButton.isEnabled = !symbolText.isEmpty &&
            !nameText.isEmpty &&
            !descriptionText.isEmpty &&
            !usageText.isEmpty
    }
    
    // When the text field in state editing changed
    @IBAction func textEditingChanged(_ sender: UITextField) {
        updateSaveButtonState()
    }
...
    // MARK: - Navigation

    // In a storyboard-based application, you will often want to do a little preparation before navigation
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // Get the new view controller using segue.destination.
        // Pass the selected object to the new view controller.
        
        guard segue.identifier == "saveUnwind" else {
            return
        }
        
        let symbol = symbolTextField.text!
        let name = nameTextField.text!
        let description = descriptionTextField.text!
        let usage = usageTextField.text!
        
        emoji = Emoji(symbol: symbol, name: name, description: description, usage: usage)
    }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

