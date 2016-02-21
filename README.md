# MediaKeyTap.swift

## Usage

Create a MediaKeyTap:
```swift
@NSApplicationMain
class AppDelegate: NSObject, NSApplicationDelegate {
    ⋮

    var mediaKeyTap: MediaKeyTap?

    func applicationDidFinishLaunching(aNotification: NSNotification) {
        mediaKeyTap = MediaKeyTap(delegate: self)
        mediaKeyTap?.start()
    }

    ⋮
}
```

and implement MediaKeyTapDelegate's 1 method:
```swift
func handleMediaKey(mediaKey: MediaKey, event: KeyEvent) {
    switch mediaKey {
    case .PlayPause:
        print("Play/pause pressed")
    case .Previous, .Rewind:
        print("Previous pressed")
    case .Next, .FastForward:
        print("Next pressed")
    }
}
```

You can also access the `KeyEvent` to access the event's underlying `Keycode`, `KeyFlags` and `KeyRepeat` values.

The MediaKeyTap initialiser allows the keypress behaviour to be specified:
```swift
    MediaKeyTap(delegate: self, on: .KeyDown) // Default
    MediaKeyTap(delegate: self, on: .KeyUp)
    MediaKeyTap(delegate: self, on: .KeyDownAndUp)
```

## Requirements

* In order to capture key events globally, your application cannot be sandboxed or you will not receive any events.

## Installation

### CocoaPods

Add `pod 'MediaKeyTap.swift'` to your `Podfile` and run `pod install`.

Then `import MediaKeyTap`.