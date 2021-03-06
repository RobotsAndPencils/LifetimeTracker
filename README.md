# LifetimeTracker

![Demo](Resources/demo.gif)

LifetimeTracker can surface retain cycle / memory issues right as you develop your application, and it will surface them to you immediately, so you can find them with more ease.

Instruments and Memory Graph Debugger are great, but too many times developers forget to check for issues as they close the feature implementation.

If you use those tools sporadicaly many of the issues they surface will require you to investigate the cause, and cost you a lot of time in the process.

## Installation

### CocoaPods

Add `pod 'LifetimeTracker'` to your Podfile.

### Carthage

Add `github "krzysztofzablocki/LifetimeTracker"` to your Cartfile.

## Integration
To Integrate visual notifications simply add following line at the start of `AppDelegate(didFinishLaunchingWithOptions:)`:

```swift
#if DEBUG
  LifetimeTracker.setup(onUpdate: LifetimeTrackerDashboardIntegration().refreshUI)
#endif
```

## Tracking key actors

Usually you want to use LifetimeTracker to track only key actors in your app, like ViewModels / Controllers etc. 

You conform to `LifetimeTrackable` and call `trackLifetime()` at the end of your init functions:

```swift
class SectionFrontViewController: UIViewController, LifetimeTrackable {
    static var lifetimeConfiguration: LifetimeConfiguration = (identifier: "VC", maxCount: 1)

    override init(nibName nibNameOrNil: String?, bundle nibBundleOrNil: Bundle?) {
        super.init(nibName: nibNameOrNil, bundle: nibBundleOrNil)
        /// ...
        trackLifetime()
    }
}
```

When you have more than `maxCount` items alive, the tracker will let you know.

## License 
LifetimeTracker is available under the MIT license. See [LICENSE](LICENSE) for more information.

## Attributions

I've used [SwiftPlate](https://github.com/JohnSundell/SwiftPlate) to generate xcodeproj compatible with CocoaPods and Carthage.
