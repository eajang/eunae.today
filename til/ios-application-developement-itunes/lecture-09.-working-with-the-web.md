---
description: >-
  These are my notes of keywords that I have learned from the course iOS
  Application Development '17 by RWTH Aachen University in iTunes.
---

# Lecture 09. Working with the web

[iOS Application Development WS17/18 by RWTH Aachen University](https://itunes.apple.com/jm/course/ios-application-development-ws17-18/id1288558355)

## Lecture 09. Working with the web

### Create an URL

```swift
let url = URL(string: "https://www.apple.com")!
```

* `!` for the case of invalid url

### Create a data task and the request

* Fetching all of the data that is on the url:

```swift
let task = URLSession.shared.dataTask(with: url) {  // runs on a background thread
    (data, response, error ) in    
    // do something - for example:
    if let data = data {
        if let string = String(data: data, encoding: .utf8) {
            print(string)
        }
    }
}
task.resume()
```

* `task.resume()` ⚠important⚠ 
  * After create the task, you must start the task by calling **`resume()`**.

### Working with an API

{% code-tabs %}
{% code-tabs-item title="URL" %}
```swift
extension URL {
    func withQueries(_ queries: [String: String]) -> URL? {
        var components = URLComponents(url: self, resolvingAgainstBaseURL: true)
        components?.queryItems = queries.compactMap{
            URLQueryItem(name: $0.0, value: $0.1)
        }
        return components?.url
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```swift
let baseURL = URL(string: "https://api.nasa.gov/planetary/apod")!
        
let query: [String: String] = [
    "api_key": "API_KEY",
    "date": "2019-09-23"
]
        
let url = baseURL.withQueries(query)!
let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
    if let data = data, let string = String(data: data, encoding: .utf8) {
        print(string)
    }
}
task.resume()
```

{% code-tabs %}
{% code-tabs-item title="response" %}
```bash
{
 "copyright":"Tun\u00e7 TezelTWAN",
 "date":"2019-09-23",
 "explanation":"Today is an equinox, a date when day and night are equal.  Tomorrow, and every day until the next equinox, the night will be longer than the day in Earth's northern hemisphere, and the day will be longer than the night in Earth's southern hemisphere. An equinox occurs midway between the two solstices, when the days and nights are the least equal. The featured picture is a composite of hourly images taken of the Sun above Bursa, Turkey on key days from solstice to equinox to solstice. The bottom Sun band was taken during the north's winter solstice in 2007 December, when the Sun could not rise very high in the sky nor stay above the horizon very long.   This lack of Sun caused winter. The top Sun band was taken during the northern summer solstice in 2008 June, when the Sun rose highest in the sky and stayed above the horizon for more than 12 hours.  This abundance of Sun caused summer. The middle band was taken during an equinox in 2008 March, but it is the same sun band that Earthlings see today, the day of the most recent  equinox.   Browser-Enhanced APOD: Google Chrome extensions (free, user created and maintained)",
 "hdurl":"https://apod.nasa.gov/apod/image/1909/seasons_tezel_1080.jpg",
 "media_type":"image",
 "service_version":"v1",
 "title":"Equinox: The Sun from Solstice to Solstice",
 "url":"https://apod.nasa.gov/apod/image/1909/seasons_tezel_1080.jpg"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Multi Threading in iOS

* Slow or expensive -&gt; background
* free the main thread -&gt; responds to the UI
* Synchronous
  * task 1 --&gt; task 2 --&gt; task 3 --&gt; ...
  * Ties up the main thread
* Asynchronous
  * multiple tasks simultaneously on multiple threads
  * background queue
  * frees up the main thread
* Grand Central Dispatch
  * Allows multi threads on your app
  * Assigns tasks to "dispatch queues" and priority
  * **Main queue**
    * Created when app launches
    * Highest priority
    * update/respond UI
  * **Background queue**
    * Lower-prioriry
    * long-running operations
  * Structure `DispatchQueue.global(qos: .background).async {     // Do some background work     DispatchQueue.main.async {         // Update the UI to indicate the work has been completed     }    }` 

