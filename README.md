# PlainPing

This is a repackaged version of [naptics/PlainPing](https://github.com/naptics/PlainPing)
## Usage

To run the example project, clone the repo, and run `pod install` in the Example directory first.

### PlainPing interface

There is one class function in PlainPing, call `PlainPing.ping(hostname, completionBlock)`.
Arguments:
* `hostName`: use a name or an IP
* `completionBlock`: will return the elapsed time in ms and an error, if there is one
* `withTimeout`: (optional), define how long we wait for an answer in seconds, default 3s


#### Example:
```swift
PlainPing.ping("www.google.com", withTimeout: 1.0, completionBlock: { (timeElapsed:Double?, error:Error?) in
    if let latency = timeElapsed {
        self.pingResultLabel.text = "latency (ms): \(latency)"
    }

    if let error = error {
        print("error: \(error.localizedDescription)")
    }
})
```

#### Example 2:
Ping several hosts one-by-one.
```swift
var pings:[String] = []

@IBAction func pingButtonPressed(_ sender: UIButton) {
    pings = ["www.google.com", "www.naptics.ch"]
    pingNext()
}

func pingNext() {
    guard pings.count > 0 else {
        return
    }

    let ping = pings.removeFirst()
    PlainPing.ping(ping, withTimeout: 1.0, completionBlock: { (timeElapsed:Double?, error:Error?) in
        if let latency = timeElapsed {
            print("\(ping) latency (ms): \(latency)")
        }
        if let error = error {
            print("error: \(error.localizedDescription)")
        }
        self.pingNext()
    })
}
```

## Installation

PlainPing is available via SPM or Cocoapods at [naptics/PlainPing](https://github.com/naptics/PlainPing)

## Author

Jonas Schoch, jonas.schoch@naptics.ch

## License

PlainPing is available under the MIT license. See the LICENSE file for more info.