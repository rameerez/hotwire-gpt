<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [0 Turbo Ios](#0-turbo-ios)
  - [0 README](#0-readme)
    - [Turbo Native for iOS](#turbo-native-for-ios)
  - [1 Quick Start Guide](#1-quick-start-guide)
    - [Quick Start Guide](#quick-start-guide)
  - [2 Overview](#2-overview)
    - [Overview](#overview)
    - [Building Your Turbo Native Application](#building-your-turbo-native-application)
  - [3 Authentication](#3-authentication)
    - [Authentication](#authentication)
  - [4 Path Configuration](#4-path-configuration)
    - [Path Configuration](#path-configuration)
  - [5 Migration](#5-migration)
    - [Migrating from Turbolinks.framework to Turbo.framework](#migrating-from-turbolinksframework-to-turboframework)
  - [6 Advanced](#6-advanced)
    - [Advanced Topics](#advanced-topics)
- [1 Turbo Android](#1-turbo-android)
  - [0 README](#0-readme-1)
    - [Turbo Native for Android](#turbo-native-for-android)
  - [1 INSTALLATION](#1-installation)
    - [Installation](#installation)
    - [Pre-release Builds](#pre-release-builds)
  - [2 OVERVIEW](#2-overview)
    - [Overview](#overview-1)
  - [3 QUICK START](#3-quick-start)
    - [Quick Start Guide](#quick-start-guide-1)
  - [4 PATH CONFIGURATION](#4-path-configuration)
    - [Path Configuration](#path-configuration-1)
  - [5 NAVIGATION](#5-navigation)
    - [Navigate to Destinations](#navigate-to-destinations)
    - [From a TurboFragment](#from-a-turbofragment)
    - [From a TurboActivity](#from-a-turboactivity)
  - [6 ADVANCED OPTIONS](#6-advanced-options)
    - [Advanced Options](#advanced-options)
- [2 Joe Masilotti Hybrid Ios Apps Tutorial](#2-joe-masilotti-hybrid-ios-apps-tutorial)
  - [0 Intro](#0-intro)
- [Hybrid iOS apps with Turbo](#hybrid-ios-apps-with-turbo)
  - [1\. The Turbo framework](#1%5C-the-turbo-framework)
  - [2\. URL routing](#2%5C-url-routing)
  - [3\. Forms and basic authentication](#3%5C-forms-and-basic-authentication)
  - [4\. The JavaScript bridge](#4%5C-the-javascript-bridge)
  - [5\. Native authentication](#5%5C-native-authentication)
  - [6\. Tips and tricks](#6%5C-tips-and-tricks)
  - [1 The Turbo Framework](#1-the-turbo-framework)
- [The Turbo Framework](#the-turbo-framework)
  - [The power of hybrid...](#the-power-of-hybrid)
  - [Getting started with Turbo](#getting-started-with-turbo)
  - [Hybrid app building blocks](#hybrid-app-building-blocks)
  - [2 Url Routing](#2-url-routing)
- [URL routing](#url-routing)
  - [URL routing with Turbo](#url-routing-with-turbo)
  - [But first, a quick refactor](#but-first-a-quick-refactor)
  - [1\. Visit actions](#1%5C-visit-actions)
  - [2\. Path configuration](#2%5C-path-configuration)
  - [Native view controllers](#native-view-controllers)
  - [Error handling with Turbo](#error-handling-with-turbo)
  - [External links](#external-links)
  - [Introduction to forms (and authentication)](#introduction-to-forms-and-authentication)
  - [3 Forms And Basic Authentication](#3-forms-and-basic-authentication)
- [Forms and basic authentication](#forms-and-basic-authentication)
  - [Turbo installation](#turbo-installation)
  - [Basic CRUD](#basic-crud)
  - [Validations and invalid forms](#validations-and-invalid-forms)
  - [Double pushed controllers](#double-pushed-controllers)
  - [Turbolinks form submissions](#turbolinks-form-submissions)
  - [Basic authentication](#basic-authentication)
  - [Up next: The JavaScript bridge](#up-next-the-javascript-bridge)
  - [4 The Javascript Bridge](#4-the-javascript-bridge)
- [The JavaScript bridge](#the-javascript-bridge)
  - [Client → Server](#client-%E2%86%92-server)
  - [Server → Client](#server-%E2%86%92-client)
  - [Looking ahead at Strada](#looking-ahead-at-strada)
  - [Up next: native authentication](#up-next-native-authentication)
  - [5 Native Authentication](#5-native-authentication)
- [Native authentication](#native-authentication)
  - [1\. Unauthenticated requests](#1%5C-unauthenticated-requests)
  - [2\. Initial authentication](#2%5C-initial-authentication)
  - [3\. Authenticated requests](#3%5C-authenticated-requests)
  - [Wrapping up](#wrapping-up)
  - [6 Tips And Tricks](#6-tips-and-tricks)
- [Tips and tricks](#tips-and-tricks)
  - [Developer quality of life improvements](#developer-quality-of-life-improvements)
  - [Make your hybrid app feel more native](#make-your-hybrid-app-feel-more-native)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 0 Turbo Ios

## 0 README

### Turbo Native for iOS

**Build high-fidelity hybrid apps with native navigation and a single shared web view.** Turbo Native for iOS provides the tooling to wrap your [Turbo 7](https://github.com/hotwired/turbo)-enabled web app in a native iOS shell. It manages a single WKWebView instance across multiple view controllers, giving you native navigation UI with all the client-side performance benefits of Turbo.

#### Features

- **Deliver fast, efficient hybrid apps.** Avoid reloading JavaScript and CSS. Save memory by sharing one WKWebView.
- **Reuse mobile web views across platforms.** Create your views once, on the server, in HTML. Deploy them to iOS, [Android](https://github.com/hotwired/turbo-android), and mobile browsers simultaneously. Ship new features without waiting on App Store approval.
- **Enhance web views with native UI.** Navigate web views using native patterns. Augment web UI with native controls.
- **Produce large apps with small teams.** Achieve baseline HTML coverage for free. Upgrade to native views as needed.

#### Requirements

Turbo iOS is written in Swift 5.3 and requires iOS 14 or higher. It supports web apps using either Turbo 7 or Turbolinks 5. The Turbo iOS framework has no dependencies.

**Note:** You should understand how Turbo works with web applications in the browser before attempting to use Turbo iOS. See the [Turbo 7 documentation](https://github.com/hotwired/turbo) for details.

```javascript
import { Turbo } from "@hotwired/turbo-rails"
```

Make sure your web app sets the `window.Turbo` global variable as it's required by the native apps (set automatically by [turbo-rails](https://github.com/hotwired/turbo-rails)).

#### Getting Started

The best way to get started with Turbo iOS to try out the demo app first to get familiar with the framework. The demo app walks you through all the basic Turbo flows as well as some advanced features. To run the demo, clone this repo and open `Demo/Demo.xcodeproj` in Xcode and run the Demo target. See [Demo/README.md](Demo/README.md) for more details about the demo. When you’re ready to start your own application, read through the rest of the documentation.

#### Installation

Add Turbo as a dependency through Xcode or directly to a Package.swift:

```
.package(url: "https://github.com/hotwired/turbo-ios", from: "<latest-version>")
```

You can also integrate the framework manually if your prefer, such as by adding the repo as a submodule, and linking `Turbo.framework` to your project.

#### Documentation

- [Quick Start](Docs/QuickStartGuide.md)
- [Overview](Docs/Overview.md)
- [Authentication](Docs/Authentication.md)
- [Path Configuration](Docs/PathConfiguration.md)
- [Migration](Docs/Migration.md)
- [Advanced](Docs/Advanced.md)

#### Contributing

Read the [contributing guide](/CONTRIBUTING.md) to learn how to set up your development environment.

Turbo iOS is open-source software, freely distributable under the terms of an [MIT-style license](LICENSE). The [source code is hosted on GitHub](https://github.com/hotwired/turbo-ios).
Development is sponsored by [37signals](https://37signals.com/).

We welcome contributions in the form of bug reports, pull requests, or thoughtful discussions in the [GitHub issue tracker](https://github.com/hotwired/turbo-ios/issues).

Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.

---

© 2023 37signals LLC


## 1 Quick Start Guide

### Quick Start Guide

This is a quick start guide to creating the most minimal Turbo iOS application from scratch get up and running in a few minutes. This will support basic back/forward navigation, but will not be a fully functional application.

1. First, create a new iOS app from the Xcode File > New > Project menu and choose the default iOS "App" template. Note: When using XCode >= 12, be sure to choose "Storyboard" under "Interface" and "UIKit App Delegate" under "Lifecycle" in the project creation dialog. 

2. Select your app's main top-level project, go to the Swift Packages tab and add the Turbo iOS dependency by entering in `https://github.com/hotwired/turbo-ios`.

3. Open the `SceneDelegate`, and replace the entire file with this code:
```swift
import UIKit
import Turbo

class SceneDelegate: UIResponder, UIWindowSceneDelegate {
    var window: UIWindow?
    private lazy var navigationController = UINavigationController()

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let _ = (scene as? UIWindowScene) else { return }
        window!.rootViewController = navigationController
        visit(url: URL(string: "https://turbo-native-demo.glitch.me")!)
    }
    
    private func visit(url: URL) {
        let viewController = VisitableViewController(url: url)
        navigationController.pushViewController(viewController, animated: true)
        session.visit(viewController)
    }
    
    private lazy var session: Session = {
        let session = Session()
        session.delegate = self
        return session
    }()
}

extension SceneDelegate: SessionDelegate {
    func session(_ session: Session, didProposeVisit proposal: VisitProposal) {
        visit(url: proposal.url)
    }
    
    func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
        print("didFailRequestForVisitable: \(error)")
    }
    
    func sessionWebViewProcessDidTerminate(_ session: Session) {
        session.reload()
    }
}
```

4. Hit run, and you have a basic working app. You can now tap links and navigate the demo back and forth in the simulator. We've only touched the very core requirements here of creating a `Session` and handling a visit.

5. You can change the url we use for the initial visit to your web app. Note: if you're running your app locally without https, you'll need to adjust your `NSAppTransportSecurity` settings in the Info.plist to allow arbitrary loads.

6. A real application will want to customize the view controller, respond to different visit actions, gracefully handle errors, and build a more powerful routing system. Read the rest of the documentation to learn more.

## 2 Overview

### Overview

There only a few main types in Turbo iOS. The primary ones being the `Session` and `Visitable`.

#### Session

The `Session` class is the central coordinator in a Turbo Native for iOS application. Each `Session` manages a single `WKWebView` instance, and lets your app choose how to handle link taps, present view controllers, and deal with network errors. You can create a `Session` in a few different ways depending on your needs:

##### Creating a Session

```swift
// 1. Create with no parameters - automatically creates a WKWebView with default configuration
let session = Session()

// 2. Create with a custom web view configuration, automatically creates a WKWebView with
// the passed-in configuration, you'll most likely want to do this to set your application's
// custom user-agent
let configuration = WKWebViewConfiguration()
configuration.applicationNameForUserAgent = "MyApplication"
let session = Session(configuration: configuration)

// 3. Finally, if you need full control, such as a WKWebView subclass, you can pass an initialized web view into the session
let webView = WKWebView()
let session = Session(webView: webView)
```

In most cases, you 'll want to use option #2. However you create your session, you need to set the `Session` delegate and implement the required protocol methods:

```swift
session.delegate = self

extension MyObject: SessionDelegate {
    func session(_ session: Session, didProposeVisit proposal: VisitProposal) {
        // Handle a visit proposal
    }

    func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
        // Handle a visit error
    }   
}
```

Turbo iOS calls the `session(_:didProposeVisit:)` method before every [application visit](https://github.com/turbolinks/turbolinks/blob/master/README.md#application-visits), such as when you tap a Turbo-enabled link or call `Turbo.visit(...)` in your web application. Implement this method to choose how to handle the specified URL and action. This is called a *proposal* since your application is not required to complete the visit.

See [Responding to Visit Proposals](#responding-to-visit-proposals) for more details.

```swift
func session(session: Session, didFailRequestForVisitable visitable: Visitable, error: Error)
```

Turbo calls `session:didFailRequestForVisitable:withError:` when a visit’s network request fails. Use this method to respond to the error by displaying an appropriate message, or by requesting authentication credentials in the case of an authorization failure.

See [Handling Failed Requests](#handling-failed-requests) for more details.

#### Visitable

A `Visitable` is a `UIViewController` that can be visited by the `Session`. Each `Visitable` view controller provides a `VisitableView` instance, which acts as a container for the `Session`’s shared `WKWebView`. The `VisitableView` optionally has a pull-to-refresh control and an activity indicator. It also automatically displays a screenshot of its contents when the web view moves to another `VisitableView`.

Visitable view controllers must conform to the Visitable protocol by implementing the following three properties:

```swift
protocol Visitable {
    weak var visitableDelegate: VisitableDelegate? { get set }
    var visitableView: VisitableView! { get }
    var visitableURL: URL! { get }
}
```

Turbo iOS provides a `VisitableViewController` class that implements the `Visitable` protocol for you and provides everything you need out of the box. This view controller displays the `VisitableView` as its single subview.

Most applications will probably need want to subclass `VisitableViewController` to customize its layout or add additional views. For example, the bundled demo application has a [ViewController subclass](../Demo/ViewController.swift) that can display a custom error view in place of the `VisitableView`.

If your application’s design prevents you from subclassing `VisitableViewController`, you can implement the `Visitable` protocol yourself. See the [VisitableViewController implementation](../Source/Visitable/VisitableViewController.swift) for details.

Note: custom `Visitable` view controllers must notify their delegate of their `viewWillAppear` and `viewDidAppear` methods through the `VisitableDelegate`'s `visitableViewWillAppear` and `visitableViewDidAppear` methods. The `Session` uses these hooks to know when it should move the WKWebView from one VisitableView to another.

### Building Your Turbo Native Application

#### Initiating a Visit

To visit a URL with Turbo, first instantiate a `Visitable` view controller. Then present the view controller and pass it to the Session’s `visit` method.

For example, to create, display, and visit using the built-in `VisitableViewController` in a `UINavigationController`-based application, you might write:

```swift
let visitable = VisitableViewController(url: yourAppURL)
navigationController.pushViewController(visitable, animated: true)
session.visit(visitable)
```

#### Responding to Visit Proposals

When you tap a Turbo-enabled link, the visit details make their way from the web view to the Session as a `VisitProposal`. Your Session’s delegate must implement the `session:didProposeVisit:` method to choose how to act on each proposal.

Normally you’ll respond to a visit proposal by creating a view controller with the URL from the visit proposal and simply initiating a visit. See [Initiating a Visit](#initiating-a-visit) for more details.

You can also choose to intercept the proposed visit and display a native view controller instead. This lets you transparently upgrade pages to native views on a per-URL basis. See the demo application for an example.

##### Implementing Visit Actions

Each proposed visit has a `VisitOptions` including an `Action`, which tell you how you should present the `Visitable`.

The default `Action` is `.advance`. In most cases you’ll respond to an advance visit by pushing a Visitable view controller for the URL onto the navigation stack.

When you follow a link annotated with `data-turbo-action="replace"`, the proposed Action will be `.replace`. Usually you’ll want to handle a replace visit by replacing the top-most visible view controller with a new one instead of pushing.

#### Handling Failed Requests

Turbo iOS calls the `session:didFailRequestForVisitable:error:` method when a visit request fails. This might be because of a network error, or because the server returned an HTTP 4xx or 5xx status code. If it was a network error in the main cold boot visit, it will be the `NSError` returned by WebKit. If it was a HTTP error or a network error from a JavaScript visit the error will be a `TurboError` and you can retrieve the status code.

```swift
func session(session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
    if let turboError = error as? TurboError {
        switch turboError {
        case .http(let statusCode):
            // Display or handle the HTTP error code
        case .networkFailure, .timeoutFailure:
            // Display appropriate error messages
        }
    } else {
        // Display the network failure or retry the visit
    }
}
```

HTTP error codes are a good way for the server to communicate specific requirements to your Turbo Native application. For example, you might use a `401 Unauthorized` response as a signal to prompt the user for authentication.

See the demo app’s [SceneController](../Demo/SceneController.swift) for a detailed example of how to present error messages and perform authorization.

#### Setting Visitable Titles

By default, Turbo iOS sets your Visitable view controller’s `title` property to the page’s `<title>`.

If you want to customize the title or pull it from another element on the page, you can implement the `visitableDidRender` method on your Visitable:

```swift
func visitableDidRender() {
    title = formatTitle(visitableView.webView?.title)
}

func formatTitle(title: String) -> String {
    // ...
}
```

#### Changing How Turbo Opens External URLs

By default, Turbo iOS opens external URLs in the default browser. You can change this behavior by implementing the Session delegate’s optional `session:openExternalURL:` method.

For example, to open external URLs in an in-app [SFSafariViewController](https://developer.apple.com/library/ios/documentation/SafariServices/Reference/SFSafariViewController_Ref/index.html), you might write:

```swift
import SafariServices

// ...

func session(session: Session, openExternalURL URL: NSURL) {
    let safariViewController = SFSafariViewController(URL: URL)
    presentViewController(safariViewController, animated: true, completion: nil)
}
```

##### Becoming the Web View’s Navigation Delegate

 When doing the cold boot visit, Turbo will need to take over as the WKWebView’s `navigationDelegate` to know when the page loads. After that, it's likely your application will want to become the `navigationDelegate` so you can have full control over the various methods.
 
 For example, when Turbo ignores a link, that link activation will go through the `func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void)` method. From that method you can decide how to route that URL, possibly through a native view controller or opening in the browser. See the demo for an example of this.

To assign the web view’s `navigationDelegate` property, implement the Session delegate’s optional `sessionDidLoadWebView(_:)` method. Turbo calls this method after every “cold boot,” such as on the initial page load and after pulling to refresh the page.

```swift
func sessionDidLoadWebView(_ session: Session) {
    session.webView.navigationDelegate = self
}

func webView(_ webView: WKWebView, decidePolicyForNavigationAction navigationAction: WKNavigationAction, decisionHandler: (WKNavigationActionPolicy) -> ()) {
    decisionHandler(WKNavigationActionPolicy.Cancel)
    // Handle non-Turbo links
}
```

Once you assign your own navigation delegate, Turbo will no longer invoke the Session delegate’s `session:openExternalURL:` method.

Note that your application _must_ call the navigation delegate’s `decisionHandler` with `WKNavigationActionPolicy.Cancel` for main-frame link activation navigation to prevent external URLs from loading in the Turbo-managed web view.

##### Sharing Cookies with Other Web Views

If you’re using a separate web view for authentication purposes, or if your application has more than one Turbo Session, you can use a single [WKProcessPool](https://developer.apple.com/library/ios/documentation/WebKit/Reference/WKProcessPool_Ref/index.html) to share cookies across all web views.

Create and retain a reference to a process pool in your application. Then configure your Turbo Session and any other web views you create to use this process pool.

```swift
let processPool = WKProcessPool()
// ...
configuration.processPool = processPool
```

## 3 Authentication

### Authentication
There are a number of ways to handle authentication in a Turbo Native iOS app. Primarily, you will be authenticating the user through a web view and relying on cookies. The framework however doesn't provide any auth-specific handling or APIs, that's completely up to each app, depending on their configuration.

#### Cookies
If your app does not need to make any authenticated network requests from native code, you can simply use cookies like in a web browser. When your user authenticates, set the appropriate cookies and make sure they are persistent, not session cookies. `WKWebView` will automatically handle persisting those cookies to disk as appropriate between app launches. All your web and XHR requests will then just work.

#### Native & Web
If you need to make authenticated network requests from both the web and native code, it's a little more complex, and depends on your particular app. You can authenticate natively and somehow hand those credentials to the web view, or authenticate in the web and send those credentials to native. We don't have any particular recommendations there, but can tell you how we decided to handle it in our apps.

##### Basecamp 3 and HEY
For Basecamp 3 and HEY, we perform authentication completely natively, and get an OAuth token back from our API. We then securely persist this token in the user's Keychain. This OAuth token is used for all network requests by setting a header in `URLSession`. This OAuth token is used for all native screens and extensions (share, widgets, today, watch, etc).

For Basecamp 3, when you load a web view for the first time in our app, we get a 401 from the server. We handle that response by making a special request in a hidden `WKWebView` to an endpoint on our server using our OAuth token which sets the appropriate cookies for the web view. When that request finishes successfully, we know the cookies are set and Turbo is ready to go. This only happens the first launch, as the web view cookies will be persisted as mentioned above. The key to this strategy is to create a `URLRequest` using the OAuth header, and use that to load the web view calling `webView.load(request)` for the authentication request. If the web view is different from the Turbo web view, you'll need to also ensure they're using the same `WKProcessPool` so the cookies are shared.

For HEY, we have a slightly different approach. We get the cookies back along with our initial OAuth request and set those cookies directly to the web view and global cookie stores.

## 4 Path Configuration

### Path Configuration

The "path configuration" is a feature that simplifies mapping various urls to "path properties". When possible, it's preferred to get data for a page from the page itself through the DOM or a library like Strada (see [advanced](Advanced.md)). However, certain properties you need to know *before* the page loads. This can be anything you want from the title, the background color, the presentation, or which view controller to load. Using a path configuration is completely optional and not required to use Turbo iOS.

The path configuration itself is a JSON file with the following structure:

```json
{
  "settings": {
    "enable-feature-x": true
  },
  "rules": [
    {
      "patterns": [
        "/new$",
        "/edit$"
      ],
      "properties": {
        "presentation": "modal"
      }
    },
    {
      "patterns": [
        "/sign_in",
      ],
      "properties": {
        "appearance": "dark"
      }
    },
  ]
}
```


You tell the `Session` about the path configuration creating a `PathConfiguration` and setting it on the `Session`:

```swift
let pathConfiguration = PathConfiguration(sources: [
  .file(Bundle.main.url(forResource: "path-configuration", withExtension: "json")!)
])

session.pathConfiguration = pathConfiguration
```

The `PathConfiguration` object can be set on multiple sessions at once and used from your own code.

#### Sources

A path configuration has an array of `sources`. You can configure the source to be a locally bundled file, a remote file available from your server, or both. We recommend always including a bundled version even when loading remotely, so it will be available in case your app is offline.

Providing a bundled file and a server location will cause the path configuration to immediately load from the bundled version and then download the server version. When downloading from a server, it will also cache that latest version locally, and attempt to load it before making the network request. That way you have a chain of configurations available, always using the latest version when available, but falling back to cache or bundle as needed.

```swift
let pathConfiguration = PathConfiguration(sources: [
  .file(Bundle.main.url(forResource: "path-configuration", withExtension: "json")!),
  .server(URL(string: "https://example.com/your-path-config.json")!)
])
```

#### Path Properties

Path properties are the core of the path configuration. The `rules` key of the JSON is an array of dictionaries. Each dictionary has a `patterns` array which is an array of regular expressions for matching on the URL, and a dictionary of `properties` that will get returned when a pattern matches.

You can lookup the properties for a URL by using the URL itself or the `url.path` value. The path configuration finds all matching rules in order, and then merges them into one dictionary, with later rules overriding earlier ones. This way you can group similar properties together.

Given the following rules:

```json
[
    {
      "patterns": [
        "/new$",
        "/edit$"
      ],
      "properties": {
        "presentation": "modal"
      }
    },
    {
      "patterns": [
        "/messages/new$",
      ],
      "properties": {
        "appearance": "dark"
      }
    },
  ]
```

The url `example.com/new` will only match the first rule and return: 

```json
{ 
  "presentation": "modal" 
}
```

The url `example.com/messages/new` however would match both the first and second rule, and return the combined properties of:

```json
{ 
  "presentation": "modal", 
  "appearance": "dark" 
}
```

When the `Session` proposes a visit, it looks up the path properties for the proposed visit url if it has a `pathConfiguration` and it passes those path properties to your app in the `VisitProposal` via `proposal.properties`. This is for convenience, but you can also use the path configuration directly and do the same lookup in your application code.

##### Query String Matching

By default, path patterns only match against the path component of the URL. Enable query string matching via:

```swift
Turbo.config.pathConfiguration.matchQueryStrings = true
```

To ensure the order of query string parameters don't affect matching, a wildcard `.*` before and after the match is recommended, like so:

```
{
  "patterns": [".*\\?.*foo=bar.*"],
  "properties": {
    "foo": "bar"
  }
}
```

#### Settings

The path configuration optionally can have a top-level `settings` dictionary. This can be whatever data you want. We use it for controlling anything that we want the flexibility to change from the server without releasing an update. This might be different urls, configurations, feature flags, etc. If you don't want to use that, you can omit it entirely from the JSON.

It can be accessed like this:

```swift
if let enableFeatureX = pathConfiguration.settings["enable-feature-x"] as? Bool {
  // Do something with `enableFeatureX` boolean value
}
```


## 5 Migration

### Migrating from Turbolinks.framework to Turbo.framework

If you were using the [Turbolinks iOS](https://github.com/turbolinks/turbolinks-ios) framework, we recommend migrating to Turbo. Though Turbo iOS is a new a framework, it is not a major change from the old Turbolinks iOS framework. Most of the code is the same, but has been improved, refactored, and better tested. It is compatible both with Turbolinks 5 and Turbo 7 JS on the server. There are some breaking API changes, but mostly in name.

Follow these steps, and you should be up and running in no time. I was able to update Basecamp 3 and HEY in about 15 minutes to give you an idea of the scope:

1. Update your dependency manager to point to `hotwired/turbo-ios` instead `turbolinks/turbolinks-ios`, see the [installation](Installation.md) doc for more info.
2. Change all your imports from `import Turbolinks` to `import Turbo`. This also would apply if you have any place you're using the full module for a type, like `Turbolinks.Session` would need to change to `Turbo.Session`
3. Try to build, at which point you should start to see a few errors for API changes.
4. `session(_ session: Session, didProposeVisitToURL url: URL, withAction action: Action)` is now `session(_ session: Session, didProposeVisit proposal: VisitProposal)`. The new `VisitProposal` type includes the url and a new `VisitOptions` type. The `VisitOptions` type includes the action.
5. `func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, withError error: NSError)` is now `func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error)`. What was previously an `NSError` is now an `Error`. To access the statusCode from a failure, you can check if the error is a new `TurboError` type like so: `let turboError = error as? TurboError, case .http(let statusCode) = turboError`
6. That should be the major code changes, please test your app first and open an issue if you run into blockers during migration. Note: the old Turbolinks.framework is now deprecated, but you can continue to use it as long as it works for you.


#### Changes from turbolinks-ios
1. Requires iOS 14 and later.
2. Fixed numerous scroll inset issues with the web view. Almost all of these culminated from underlying WebKit bug across versions iOS 10 and iOS 11. It seems they were all fixed in iOS 12, so that's why iOS 12+ is now required. That means we could drop our hacks for getting the correct inset for the web view and rely on the iOS to do it automatically. The web view now sits full under the nav bar/tab bars and works as expected as far as scroll positioning and restoration


#### Whats new in Turbo iOS?
1. Introduced a new `PathConfiguration` concept, documented here - [PathConfiguration](PathConfiguration.md)
2. Support for Turbo 7 apps as well as new `VisitOptions` provided by Turbo 7
3. Support for Swift Package Manager now that as of Swift 5.3 it supports resources
4. Bug fixes and additional tests

## 6 Advanced

### Advanced Topics

#### Multiple Sessions

Each `Session` is 1:1 with a `WKWebView`. This means you can never have two pages active at the same time. You can create as many separate session as you need, though it's recommended to make as few as a possible. Every session you make will require a cold-boot visit which is likely to the be the slowest page load in your app. Each web view also uses additional resources.

One place you'll definitely want multiple sessions is for modals since non full-screen modals don't work out of the box with a single session. The demo shows a way to do this by lazily creating a reusable modal session whenever a modal is used. This is efficient, works well with any modal type, and makes the app feel better since we don't need to alter the main session at all to present/dismiss a modal. 

A `UITabBarController` based app should work with a single session, but you may want to use multiple session there as well. A good rule of thumb is that you'll likely want a separate session for each navigation context you have (most likely a session per `UINavigationController`).

#### Enable Debug Logging
During development, you may want to see what `turbo-ios` is doing behind the scenes. To enable debug logging, you can set the `TurboLog.debugLoggingEnabled` flag to `true`. Debug logging should always be disabled in your production app. For example:

```swift
###if DEBUG
TurboLog.debugLoggingEnabled = true
###endif
```

#### Native <-> JavaScript Integration

You can send messages from your native app to the web view by using `session.webView.evaluateJavaScript()` method. You can receive messages by adding a `WKScriptMessageHandler` to the web view and implementing the required protocols. That allows for two-way async communication. 

Here's a simple sketch of how this works. You can create your session with a `WKWebViewConfiguration` and in that configuration, you can setup your `WKScriptMessageHandler` which will be used to receive messages from the web app through JavaScript. When you receive a message, you can parse it and handle it however you need, optionally sending data back to the web app with the `webView.evaluateJavaScript()` method.

```swift
import Turbo
import WebKit

// WKScriptMessageHandler requires NSObject conformance
class SessionController: NSObject {
    lazy var session: Turbo.Session = {
        let configuration = WKWebViewConfiguration()
        
        // Setup your session with a WKWebViewConfiguration and script message handler
        configuration.userContentController.add(self, name: "nativeApp")
        
        let session = Turbo.Session(webViewConfiguration: configuration)
        session.delegate = self
        
        return session
    }()
}

extension SessionController: WKScriptMessageHandler {
    func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
        // WebView JS sends a message with
        // webkit.messageHandlers.nativeApp.postMessage(message)
        
        // Native app receives message and processes it as needed, maybe pass to another object
        // message.body...
        
        // Native app can call more JS functions as needed
        session.webView.evaluateJavaScript("someReplyMessage()")
    }
}
```

This is fine for simple tasks, but we've found we need something more comprehensive for our apps, which is why we created a new framework called Strada. This is a library in 3 parts (web, iOS, and Android) for integrating Turbo Native apps with their hosted web apps. This is separate and optional, but can dramatically improve the experience of your app. See the Strada repo for details (*coming soon*).

# 1 Turbo Android

## 0 README

### Turbo Native for Android

**Build high-fidelity hybrid apps with native navigation and a single shared web view**. Turbo Native for Android provides the tooling to wrap your [Turbo 7](https://turbo.hotwired.dev/)-enabled web app in a native Android shell. It manages a single WebView instance across multiple Fragment destinations, giving you native navigation UI with all the client-side performance benefits of Turbo.

#### Features
- **Deliver fast, efficient hybrid apps.** Avoid reloading JavaScript and CSS. Save memory by sharing one WebView.
- **Reuse mobile web views across platforms.** Create your views once, on the server, in HTML. Deploy them to [iOS](https://github.com/hotwired/turbo-ios), Android, and mobile browsers simultaneously. Ship new features without waiting on Play Store approval.
- **Enhance web views with native UI.** Navigate web views using native patterns. Augment web UI with native controls.
- **Produce large apps with small teams.** Achieve baseline HTML coverage for free. Upgrade to native views as needed.

#### Requirements

1. Android SDK 26+ is required as the `minSdk` in your `build.gradle.kts` file.
1. This library is written entirely in [Kotlin](https://kotlinlang.org/), and your app should use Kotlin as well. Compatibility with Java is not provided or supported.
1. This library supports web apps using either Turbo 7 or Turbolinks 5.
1. `Turbo` (or `Turbolinks`) is exposed on the `window` object on the WebView page being loaded.

**Note:** You should understand how Turbo works with web applications in the browser before attempting to use Turbo Android. See the [Turbo 7 documentation](https://turbo.hotwired.dev) for details.

#### Getting Started
The best way to get started with Turbo Android is to try out the demo app first to get familiar with the framework. The demo app walks you through all the basic Turbo flows as well as some advanced features. To run the demo, clone this repo, open the directory in Android Studio, and build the `demo` module to your Android device. See [demo/README.md](demo/README.md) for more details about the demo. When you’re ready to start your own application, read through the rest of the documentation.

See the [instructions to build the project yourself](docs/BUILD-PROJECT.md).

#### Documentation

1. [Installation](docs/INSTALLATION.md)
1. [Overview](docs/OVERVIEW.md)
1. [Quick Start](docs/QUICK-START.md)
1. [Path Configuration](docs/PATH-CONFIGURATION.md)
1. [Navigation](docs/NAVIGATION.md)
1. [Advanced Options](docs/ADVANCED-OPTIONS.md)

#### Contributing

Turbo Android is open-source software, freely distributable under the terms of an [MIT-style license](LICENSE). The [source code is hosted on GitHub](https://github.com/hotwired/turbo-android). Development is sponsored by [37signals](https://37signals.com/).

We welcome contributions in the form of bug reports, pull requests, or thoughtful discussions in the [GitHub issue tracker](https://github.com/hotwired/turbo-android/issues).

Please note that this project is released with a [Contributor Code of Conduct](docs/CONDUCT.md). By participating in this project you agree to abide by its terms.

---------

© 2024 37signals LLC

## 1 INSTALLATION

### Installation

#### Gradle

Add the dependency from Maven Central to your app module's (not top-level) `build.gradle.kts` file:

```kotlin
dependencies {
    implementation("dev.hotwire:turbo:<latest-version>")
}
```

[![Download](https://img.shields.io/maven-central/v/dev.hotwire/turbo)](https://search.maven.org/artifact/dev.hotwire/turbo)

See the [latest version](https://search.maven.org/artifact/dev.hotwire/turbo) available on Maven Central.

#### Required `minSdk`

Android SDK 26 (or greater) is required as the `minSdk` in your app module's `build.gradle.kts` file:

```kotlin
compileSdk = 34

defaultConfig {
    minSdk = 26
    targetSdk = 34
    // ...
}
```

#### Internet Permission

In order for a [WebView](https://developer.android.com/reference/android/webkit/WebView.html) to access the Internet and load web pages, your app must have the `INTERNET` permission. Make sure you include this permission in your app's `AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

### Pre-release Builds

Pre-release builds will be published to [GitHub Packages](https://github.com/features/packages).

#### Personal Access Token

If you'd like to use a pre-release version, you'll need to create a [Personal Access Token](https://docs.github.com/en/free-pro-team@latest/packages/learn-github-packages/about-github-packages#authenticating-to-github-packages) in your GitHub account and give it the `read:packages` permission.

Copy your access token to your `.bash_profile` (or another accessible place that's outside of source control):

```bash
export GITHUB_USER='<your username>'
export GITHUB_ACCESS_TOKEN='<your personal access token>'
```

#### Gradle

Add the GitHub Packages maven repository and the dependency to your app module's `build.gradle.kts` file:

```kotlin
repositories {
    maven {
        name = "GitHubPackages"
        url = uri("https://maven.pkg.github.com/hotwired/turbo-android")

        credentials {
            username = System.getenv('GITHUB_USER')
            password = System.getenv('GITHUB_ACCESS_TOKEN')
        }
    }
}

dependencies {
    implementation("dev.hotwire:turbo:<latest-version>")
}
```

See the [latest version](https://github.com/hotwired/turbo-android/releases) available on GitHub Packages.

## 2 OVERVIEW

### Overview
Turbo Android is a native adapter for any [Turbo 7](https://turbo.hotwired.dev)-enabled web app. It enables you to build hybrid (native + web) apps that give you the flexibility to display native screens, `WebView` screens, or a blend of both. It's built entirely using standard Android tools and conventions.

This library has been in use and tested in the wild since June 2020 in the all-new [HEY Android](https://play.google.com/store/apps/details?id=com.basecamp.hey&hl=en_US) app.

#### Structure of Your App
Turbo Android uses Google's [Navigation component library](https://developer.android.com/guide/navigation) under the hood to navigate between destinations. It leverages a single-`Activity` architecture and each navigation destination is a `Fragment` that you'll implement in your app. To take advantage of speed improvements that [Turbo](https://turbo.hotwired.dev) enables for web applications, a single `WebView` instance is swapped between each `TurboWebFragment` destination, so the `WebView` instance and resources don't need to be recreated for each destination.

The structure of your single-`Activity` app will look like the following diagram. The library manages most of the navigation and lifecycle events for you automatically, but you'll need to setup the foundation of your app and each unique `Fragment` destination. We'll walk you through setting up your app in the [Quick Start Guide](QUICK-START.md) instructions.

![Structure of a Turbo App](assets/turbo-app-diagram.png)

## 3 QUICK START

### Quick Start Guide

#### Contents

1. [Create a NavHostFragment](#create-a-navhostfragment)
1. [Create an Activity](#create-an-activity)
1. [Create a Web Fragment](#create-a-web-fragment)
1. [Create a Path Configuration](#create-a-path-configuration)

#### Create a NavHostFragment

A [`NavHostFragment`](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment) is a component available in [Android Jetpack](https://developer.android.com/jetpack) and is primarily responsible for providing "an area in your layout for self-contained navigation to occur."

The Turbo extension of this class, `TurboSessionNavHostFragment`, along with being responsible for self-contained `TurboFragment` navigation, also manages a `TurboSesssion` and a `TurboWebView` instance. You will need to implement a few things for this abstract class:

- The name of the `TurboSession` (this is arbitrary, but must be unique in your app)
- The url of a starting location when your app starts up. Note: if you're running your app locally without HTTPS, you'll need to adjust your `android:usesCleartextTraffic` settings in the AndroidManifest.xml (or use an Android Network security configuration), and target [`10.0.2.2` instead of `localhost`](https://developer.android.com/studio/run/emulator-networking).
- A list of registered activities that Turbo will be able to navigate to (optional)
- A list of registered fragments that Turbo will be able to navigate to
- The location of your `TurboPathConfiguration` JSON file(s) to configure navigation rules

In its simplest form, the implementation of your `TurboSessionNavHostFragment` will look like:

**`MainSessionNavHostFragment`:**
```kotlin
import dev.hotwire.turbo.session.TurboSessionNavHostFragment

class MainSessionNavHostFragment : TurboSessionNavHostFragment() {
    override val sessionName = "main"

    override val startLocation = "https://turbo-native-demo.glitch.me/"

    override val registeredActivities: List<KClass<out AppCompatActivity>>
        get() = listOf(
            // Leave empty unless you have more
            // than one TurboActivity in your app
        )

    override val registeredFragments: List<KClass<out Fragment>>
        get() = listOf(
            WebFragment::class
            // And any other TurboFragments in your app
        )

    override val pathConfigurationLocation: TurboPathConfiguration.Location
        get() = TurboPathConfiguration.Location(
            assetFilePath = "json/configuration.json",
            remoteFileUrl = "https://turbo.hotwired.dev/demo/configurations/android-v1.json"
        )
}
```

See the [Fragment section](#create-a-web-fragment) below to create a `TurboFragment` that you'll register here. See the [Path Configuration documentation](PATH-CONFIGURATION.md) to create your path configuration file(s).

Refer to the demo [`MainSessionNavHostFragment`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/main/MainSessionNavHostFragment.kt) for an example.

#### Create an Activity

It's strongly recommended to use a single-Activity architecture in your app. Generally, you'll have one `TurboActivity` and many `TurboFragments`.

##### Create the TurboActivity layout resource

You need to create a layout resource file that your `TurboActivity` will use to host the `TurboSessionNavHostFragment` that you created above.

Android Jetpack provides a [`FragmentContainerView`](https://developer.android.com/reference/androidx/fragment/app/FragmentContainerView) to contain `NavHostFragment` navigation. In its simplest form, your Activity layout file will look like:

**`res/layout/activity_main.xml`:**
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/main_nav_host"
        android:name="dev.hotwire.turbo.demo.main.MainSessionNavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:defaultNavHost="false" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

Refer to the demo [`activity_main.xml`](../demo/src/main/res/layout/activity_main.xml) for an example.

##### Create the TurboActivity class

A Turbo Activity is straightforward and needs to implement the [`TurboActivity`](../turbo/src/main/kotlin/dev/hotwire/turbo/activities/TurboActivity.kt) interface in order to provide a [`TurboActivityDelegate`](../turbo/src/main/kotlin/dev/hotwire/turbo/delegates/TurboActivityDelegate.kt).

Your Activity should extend Android Jetpack's [`AppCompatActivity`](https://developer.android.com/reference/androidx/appcompat/app/AppCompatActivity). In its simplest form, your Activity will look like:

**`MainActivity.kt`:**

```kotlin
class MainActivity : AppCompatActivity(), TurboActivity {
    override lateinit var delegate: TurboActivityDelegate

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        delegate = TurboActivityDelegate(this, R.id.main_nav_host)
    }
}
```

_Note that `R.layout.activity_main` refers to the Activity layout file that you already created. `R.id.main_nav_host` refers to the `MainSessionNavHostFragment` that you created, hosted in the layout file._

Refer to the demo [`MainActivity`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/main/MainActivity.kt) as an example. (Don't forget to add your Activity to your app's [`AndroidManifest.xml`](../demo/src/main/AndroidManifest.xml) file.)

#### Create a Web Fragment

##### Create the TurboWebFragment class

You'll need at least one web Fragment that will serve as a destination for urls that display web content in your app.

A web Fragment is straightforward and needs to implement the [`TurboWebFragment`](../turbo/src/main/kotlin/dev/hotwire/turbo/fragments/TurboWebFragment.kt) abstract class. This abstract class implements the [`TurboWebFragmentCallback`](../turbo/src/main/kotlin/dev/hotwire/turbo/fragments/TurboWebFragmentCallback.kt) interface, which provides a number of functions available to customize your Fragment.

You'll need to annotate each Fragment in your app with a `@TurboNavGraphDestination` annotation with a URI of your own scheme. This URI is used by the library to build an internal navigation graph and map url path patterns to the destination Fragment with the corresponding URI. See the [Path Configuration documentation](PATH-CONFIGURATION.md) to learn how to map url paths to destination Fragments.

In its simplest form, your web Fragment will look like:

**`WebFragment.kt`:**
```kotlin
@TurboNavGraphDestination(uri = "turbo://fragment/web")
class WebFragment : TurboWebFragment()
```

The library automatically inflates a default `R.layout.turbo_fragment_web` layout to host a `TurboView`. If you'd like to create your own custom layout for your web Fragment, you can override the `onCreateView()` function and inflate your own layout. See the demo [`WebHomeFragment`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/features/web/WebHomeFragment.kt) as an example of of providing your own layout.

You can also provide your own custom progress view or error view by overriding the `createProgressView()` and `createErrorView()` functions in your web Fragment.

Refer to demo [`WebFragment`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/features/web/WebFragment.kt) as an example.

#### Create a Path Configuration

See the documentation to learn about setting up your [path configuration](PATH-CONFIGURATION.md)

#### Navigation

See the documenation to learn about [navigating between destinations](NAVIGATION.md).

#### Advanced Options

See the documentation to [learn about the advanced options available](ADVANCED-OPTIONS.md).

## 4 PATH CONFIGURATION

### Path Configuration
A JSON configuration file specifies the set of rules Turbo will follow to navigate to Fragment destinations and configure options. It has two top-level objects: 

1. Application-level `"settings"`
1. Url path-specific `"rules"`

At minimum, you will need a bundled [`src/main/assets/json/configuration.json`](../demo/src/main/assets/json/configuration.json) file in your app that Turbo can read. We also recommend hosting a [remote configuration file on your server](#remote-path-configuration), so you can update the app's configuration at any time without needing an app update.

In its simplest form, your JSON configuration will look like:

**`assets/json/configuration.json`:**
```json
{
  "settings": {
    "screenshots_enabled": true
  },
  "rules": [
    {
      "patterns": [
        ".*"
      ],
      "properties": {
        "context": "default",
        "uri": "turbo://fragment/web",
        "pull_to_refresh_enabled": true
      }
    }
  ]
}
```

Refer to demo [`configuration.json`](../demo/src/main/assets/json/configuration.json) as an example.

#### Remote Path Configuration

Remote configuration files are fetched (and cached) on every app startup, so the app always has the latest configuration available. The location of these configuration files needs to be set in your [`TurboSessionNavHostFragment.pathConfigurationLocation`](#create-a-navhostfragment). 

```kotlin
class MainSessionNavHostFragment : TurboSessionNavHostFragment() {
    // ...
    override val pathConfigurationLocation: TurboPathConfiguration.Location
        get() = TurboPathConfiguration.Location(
            assetFilePath = "json/configuration.json",
            remoteFileUrl = "https://turbo.hotwired.dev/demo/configurations/android-v1.json"
        )
}
```

Here's some tips for managing path configurations:

- Use different path configuration files, with different URLs, for Android and [iOS](https://github.com/hotwired/turbo-ios).
- Include a version in your path configuration URL (`v1` in the above example). This way if you need to make fundamental changes to your architecture you can be confident you won't break the app for people who haven't updated.
- Try to keep your local and remote path configuration files in sync. When your app starts, Turbo will load your local configuration file, then make a request for your remote file which will override your local file. If the files are different and your server doesn't respond quickly, it's possible to get difficult to debug behaviour. If you're making other changes to your app that will require a new native deployment, that's a good time to update your local file to match the current state of your server.

#### Settings
The `settings` object is a place to configure app-level settings. This is useful when you have a remote configuration file, since you can add your own custom settings and use them as remote feature-flags. Available settings are:
* `screenshots_enabled` — Whether or not transitional web screenshots should be used during navigation. This gives the appearance of a more smooth experience since the session WebView is swapped between web destination Fragments, but does require more performance overhead. 
	* Optional.
	* Possible values: `true`, `false`. Defaults to `true`.
* Any custom app settings that you'd like to configure here

#### Rules
The `"rules"` array defines a list of rules that are processed in order and cascade downward, similar to CSS. The top-most declaration should establish the default behavior for all url path patterns, while each subsequent rule can override for specific behavior.

##### Patterns

The `patterns` array defines Regex patterns that will be used to match url paths (and as a result, which `properties` should be applied for a particular path).

##### Properties

The `properties` object contains a handful of key/value pairs that Turbo Android supports out of the box. You are free to add more properties as your app needs, but these are the ones the framework is aware of and will handle automatically.

* `uri` — The target destination URI to navigate to. Must map to an Activity or Fragment that has implemented the [`TurboNavGraphDestination`](../turbo/src/main/kotlin/dev/hotwire/turbo/nav/TurboNavGraphDestination.kt) annotation with a matching `uri` value.
	* **Required**. 
	* No explicit value options. No default value.
* `context` — Specifies the presentation context in which the view should be displayed. Turbo will determine what the navigation behavior should be based on this value + the `presentation` value. Unless you are specifically showing a modal-style view (e.g., a form, wizard, navigation, etc.), `default` is usually sufficient. 
	* Optional. 
	* Possible values: `default` or `modal`. Defaults to `default`. 
* `presentation` — Specifies what style to use when presenting the given `uri` destination. Turbo will determine what the navigation behavior should be based on this value + the `context` value. In most cases `default` should be sufficient, but you may find cases where your app needs specific behavior. 
	* Optional. 
	* [Possible values](../turbo/src/main/kotlin/dev/hotwire/turbo/nav/TurboNavPresentation.kt): `default`, `push`, `pop`, `replace`, `replace_root`, `clear_all`, `refresh`, `none`. Defaults to `default`.
* `fallback_uri` — Provides a fallback URI in case a destination cannot be found that maps to the `uri`. Can be useful in cases when pointing to a new `uri` that may not be available yet in older versions of the app.
	* Optional.
	* No explicit value options. No default value.
* `title` —  Specifies a default title that will be displayed in the toolbar for the destination. This is most useful for native destinations, since web destinations will render their title from the `WebView` page's `<title>` tag.
    * Optional.
    * No explicit value options. No default value.
* `pull_to_refresh_enabled` — Whether or not pull-to-refresh should be enabled for the given path.
	* Optional.
	* Possible values: `true`, `false`. Defaults to `false`.
  

## 5 NAVIGATION

### Navigate to Destinations

#### From Web Links
Tapping a web link in a `TurboWebFragment` will automatically navigate to the url's corresponding Fragment destination, based on the app's [Path Configuration](PATH-CONFIGURATION.md).

Sometimes, you may want to override this default behavior. For example, if your web app can surface external domain urls, you should open those urls in the device's default browser. The `TurboWebFragment` abstract class implements the `TurbolNavDestination` interface, which provides a `shouldNavigateTo(newLocation: String)` function that can be overridden.

In your web Fragment, this would look like:

**`WebFragment.kt`:**
```kotlin
@TurboNavGraphDestination(uri = "turbo://fragment/web")
class WebFragment : TurboWebFragment() {

    // ...

    override fun shouldNavigateTo(newLocation: String): Boolean {
        return when (newLocation.startsWith(MY_DOMAIN)) {
            true -> {
                // Allow Turbo to follow the navigation to `newLocation`
                true
            }
            else -> {
                // Open `newLocation` in the device's external browser
                launchBrowser(newLocation)
                false
            }
        }
    }

    private fun launchBrowser(location: String) {
        val intent = Intent(Intent.ACTION_VIEW, Uri.parse(location))
        context?.startActivity(intent)
    }
}
```

Refer to demo [`NavDestination`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/base/NavDestination.kt) interface as a more advanced example.

### From a TurboFragment
If you'd like to navigate to a new destination in response to native UI/features, it's easy from any `TurboFragment`. The following navigation APIs are available:

- `navigate(location: String)`
- `navigateUp()`
- `navigateBack()`
- `clearBackStack()`
- `refresh(displayProgress: Boolean)`

Refer to the [`TurboNavDestination`](../turbo/src/main/kotlin/dev/hotwire/turbo/nav/TurboNavDestination.kt) interface for further documentation.

In your Fragment, this would look like:

**`WebFragment.kt`:**
```kotlin
@TurboNavGraphDestination(uri = "turbo://fragment/web")
class WebFragment : TurboWebFragment() {

    // ...

    private fun respondToNativeFeature() {
        // Navigate to a new destination
        navigate(MY_NEW_LOCATION)

        // Navigate up to the previous destination (Toolbar arrow behavior)
        navigateUp()

        // Navigate back to the previous destination (OS back button behavior)
        navigateBack()

        // Clears all Fragment destinations off the backstack, excluding
        // the starting destination of your TurboSessionNavHostFragment
        clearBackStack()

        // Refresh the current destination
        refresh()

        // Refresh the current destination without displaying progress
        refresh(displayProgress = false)
    }
}
```
### From a TurboActivity
If you'd like to navigate to a new destination in response to native UI/features, it's easy from any `TurboActivity`. The following navigation APIs are available from the Activity's `delegate`:

- `delegate.navigate(location: String)`
- `delegate.navigateUp()`
- `delegate.navigateBack()`
- `delegate.clearBackStack()`
- `delegate.refresh(displayProgress: Boolean)`

Refer to the [`TurboActivityDelegate`](../turbo/src/main/kotlin/dev/hotwire/turbo/delegates/TurboActivityDelegate.kt) class for further documentation.

In your Activity, this would look like:

**`MainActivity.kt`:**
```kotlin
class MainActivity : AppCompatActivity(), TurboActivity {

    // ...

    private fun respondToNativeFeature() {
        // Navigate to a new destination
        delegate.navigate(MY_NEW_LOCATION)

        // Navigate up to the previous destination (Toolbar arrow behavior)
        delegate.navigateUp()

        // Navigate back to the previous destination (OS back button behavior)
        delegate.navigateBack()

        // Clears all Fragment destinations off the backstack, excluding
        // the starting destination of your TurboSessionNavHostFragment
        delegate.clearBackStack()

        // Refresh the current destination
        delegate.refresh()

        // Refresh the current destination without displaying progress
        delegate.refresh(displayProgress = false)
    }
}
```

## 6 ADVANCED OPTIONS

### Advanced Options

#### Create a Native Fragment
You don't need to rely on your web app for every screen in your app. Elevating destinations that would benefit from a higher fidelity experience to fully-native is often a great idea. For example, here's how you would create a fully native image viewer fragment:

##### Create the TurboFragment layout resource
You need to create a layout resource file that your native `TurboFragment` will use as its content view.

In its simplest form, your Fragment layout file will look like:

**`res/layout/fragment_image_viewer.xml`:**
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Your layout views here -->

</androidx.constraintlayout.widget.ConstraintLayout>
```

Refer to the demo [`fragment_image_viewer.xml`](../demo/src/main/res/layout/fragment_image_viewer.xml) for an example.

##### Create the TurboFragment class
A native Fragment is straightforward and needs to implement the [`TurboFragment`](../turbo/src/main/kotlin/dev/hotwire/turbo/fragments/TurboFragment.kt) abstract class.

You'll need to annotate each Fragment in your app with a `@TurboNavGraphDestination` annotation with a URI of your own scheme. This URI is used by the library to build an internal navigation graph and map url path patterns to the destination Fragment with the corresponding URI. See the [Path Configuration guide](PATH-CONFIGURATION.md) to learn how to map url paths to destination Fragments.

In its simplest form, your native Fragment will look like:

**`ImageViewerFragment.kt`:**
```kotlin
@TurboNavGraphDestination(uri = "turbo://fragment/image_viewer")
class ImageViewerFragment : TurboFragment() {
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        return inflater.inflate(R.layout.fragment_image_viewer, container, false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        loadImage(view)
    }

    private fun loadImage(view: View) {
        // Load the image into the view using the `location`
    }
}
```

Don't forget to register the `ImageViewerFragment` class in your app's `TurboSessionNavHostFragment` as a Fragment destination.

Refer to demo [`ImageViewerFragment`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/features/imageviewer/ImageViewerFragment.kt) as an example.

#### Display Bottom Sheet Dialogs
Fragment destinations can be dislplayed as bottom sheet dialogs. These are transitional, modal Fragments that can be easily dismissed. Bottom sheet Fragments can be web or native.

##### Create a Web Bottom Sheet Fragment
A web bottom sheet Fragment is straightforward and needs to implement the [`TurboWebBottomSheetDialogFragment`](../turbo/src/main/kotlin/dev/hotwire/turbo/fragments/TurboWebBottomSheetDialogFragment.kt) abstract class. This abstract class implements the [`TurboWebFragmentCallback`](../turbo/src/main/kotlin/dev/hotwire/turbo/fragments/TurboWebFragmentCallback.kt) interface, which provides a number of functions available to customize your Fragment.

In its simplest form, your web bottom sheet Fragment will look like:

**`WebBottomSheetFragment.kt`:**
```kotlin
@TurboNavGraphDestination(uri = "turbo://fragment/web/modal/sheet")
class WebBottomSheetFragment : TurboWebBottomSheetDialogFragment()
```
The library automatically inflates a default `R.layout.turbo_fragment_web_bottom_sheet` layout to host a `TurboView`. If you'd like to create your own custom layout for your web bottom sheet Fragment, you can override the `onCreateView()` function and inflate your own layout.

You can also provide your own custom progress view or error view by overriding the `createProgressView()` and `createErrorView()` functions in your web Fragment.

Refer to demo [`WebBottomSheetFragment`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/features/web/WebBottomSheetFragment.kt) as an example.

#### Fragment Transition Animations
The transition animations when navigating between Fragments can be fully customized. To do this, override the `TurboNavDestination.getNavigationOptions()` interface function (available in all Fragment destinations). Place your custom XML animation resources in the `/res/anim` directory and provide these animations using the AndroidX [`NavOptions`](https://developer.android.com/reference/androidx/navigation/NavOptions) DSL. An example looks like:

```kotlin
override fun getNavigationOptions(
    newLocation: String,
    newPathProperties: TurboPathConfigurationProperties
): NavOptions {
    return navOptions {
        anim {
            enter = R.anim.custom_anim_enter
            exit = R.anim.custom_anim_exit
            popEnter = R.anim.custom_anim_pop_enter
            popExit = R.anim.custom_anim_pop_exit
        }
    }
}
```

Refer to the demo [`NavDestination.kt`](../demo/src/main/kotlin/dev/hotwire/turbo/demo/base/NavDestination.kt) as an example.

#### Using Multiple Activities
You may encounter situations where a truly single-`Activity` app may not be feasible. For example, you may need an `Activity` for logged-out state and a separate `Activity` for logged-in state.

In such cases, you need to create an additional `Activity` that also implements the `TurboActivity` interface. You will need to be sure to register each `Activity` by calling [`TurboSessionNavHostFragment.registeredActivities()`](../turbo/src/main/kotlin/dev/hotwire/turbo/session/TurboSessionNavHostFragment.kt) so that you can navigate between them.

#### Enable Debug Logging
During development, you may want to see what `turbo-android` is doing behind the scenes. To enable debug logging, call `Turbo.config.debugLoggingEnabled = true`. Debug logging should always be disabled in your production app. For example:

```kotlin
if (BuildConfig.DEBUG) {
    Turbo.config.debugLoggingEnabled = true
}
```

#### Native <-> JavaScript Integration

To call native code from JavaScript, use [`addJavascriptInterface`](https://developer.android.com/reference/android/webkit/WebView#addJavascriptInterface(java.lang.Object,%20java.lang.String)). JavaScript interfaces are long lasting, so a good place to do this is your `TurboSessionNavHostFragment` subclass' `onSessionCreated` function.

To call JavaScript code from native, use [`evaluateJavascript`](https://developer.android.com/reference/android/webkit/WebView#evaluateJavascript(java.lang.String,%20android.webkit.ValueCallback%3Cjava.lang.String%3E)). For example, to do this every time a Turbo visit is completed, override `onVisitCompleted` in your `TurboWebFragment` subclass:

```kotlin
class WebFragment : TurboWebFragment() {

    // ...
    
    override fun onVisitCompleted(location: String, completedOffline: Boolean) {
        super.onVisitCompleted(location, completedOffline)
        
        val script = "console.log('hello world')"
        session.webView.evaluateJavascript(script, null)
    }
```

Executing JavaScript directly is fine for simple tasks, but we've found we need something more comprehensive for our apps, which is why we created a new framework called Strada. This is a library in 3 parts (web, iOS, and Android) for integrating Turbo Native apps with their hosted web apps. This is separate and optional, but can dramatically improve the experience of your app. See the Strada repo for details *(coming soon)*.

# 2 Joe Masilotti Hybrid Ios Apps Tutorial

## 0 Intro

Hybrid iOS apps with Turbo
==========================



May 14, 2021

Native apps are hard. They are expensive to build and even more expensive to maintain.

What if that wasn't the case? What if every time you built a new workflow in your Rails app, your mobile app got that feature *for free*?

This is possible with [Turbo](https://github.com/hotwired/turbo-ios/), a small framework from the geniuses at Basecamp. Follow this series of posts to learn how to build a hybrid iOS app from scratch. All you need is a mobile website powered by Ruby on Rails.

Follow along as we build a hybrid iOS from scratch alongside the supporting Rails code.

[1\. The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
----------------------------------------------------------------------------------

This introduction covers the benefits of hybrid apps and how Turbo helps bridge the gap between web and native. It also breaks down the code in the Quick Start guide from the Turbo wiki line by line. A perfect place to start for those new to Turbo or hybrid in general.

[2\. URL routing](https://masilotti.com/turbo-ios/url-routing/)
---------------------------------------------------------------

The second article covers everything related to routing URLs. This includes visit actions (advance vs. replace), path configuration, error handling, and native view controllers. It also touches on how forms work in Turbo iOS and why you might be running into issues with your Rails app.

[3\. Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
-----------------------------------------------------------------------------------------------------

Part 3 covers slightly more advanced topics: forms and basic authentication. Learn how to install Turbo in Rails 6, add custom form handling for the iOS client, and get up and running with web-based authentication.

[4\. The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
-----------------------------------------------------------------------------------

Having all our content in rendered on the web comes with some trade-offs. What if we want a native navigation bar button? Enter the JavaScript bridge, where we can pass messages between client and server without waiting for someone to tap a link.

[5\. Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
-----------------------------------------------------------------------------------

One major limitation of web-only authentication is, well, it's web only. Native authentication, on the other hand, opens up a world of possibilities. It breaks your app out of the web world and enables fully native screens. Meaning, you can integrate native SDKs like location services and push notifications. Or, you can render SwiftUI views for the really important stuff.

[6\. Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)
-----------------------------------------------------------------------

To wrap up the series I'm sharing tips and tricks I've picked up over the years that range from making development easier to making the app feel more native. How to dismiss a modal after submitting a form, fixes for double pushed controllers, disabling link previews (Force Touch), and more.

## 1 The Turbo Framework

The Turbo Framework
=====================================================



February 18, 2021

Native apps are hard. They are expensive to build and even more expensive to maintain. Every time you release a feature on the web, you also need to add it to each of your mobile apps.

What if that wasn't the case? What if every time you built a new workflow in your Rails app, your mobile app got that feature *for free*? And you didn't even need to go through App Store approval?

This is possible with [Turbo](https://github.com/hotwired/turbo-ios/), a small framework from the geniuses at Basecamp -- the same technology that powers [their mobile app](https://apps.apple.com/us/app/id1015603248), [Hey](https://apps.apple.com/us/app/hey-email/id1506603805), and countless other apps.

This is the first post in a series on how to build high-fidelity, hybrid iOS apps with Turbo and Ruby on Rails. It covers the benefits of Turbo-powered hybrid apps and how to get up and running.

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  *Hybrid iOS apps with Turbo -- Part 1: The Turbo framework*
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  [Hybrid iOS apps with Turbo -- Part 6: Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)

The power of hybrid...
--------------------

Basecamp highlights four major benefits of a hybrid approach to your mobile apps. You'll:

1.  Deliver fast, efficient hybrid apps.
2.  Reuse mobile web views across platforms.
3.  Enhance web views with native UI.
4.  **Produce large apps with small teams.**

The first three items are product features that enable the actual value, number four. I've *solely* maintained Turbo iOS apps for Rails applications with hundreds of controllers and models.

This means you don't need to hire a team of iOS developers to build your app. You only need a solid understanding of the Turbo framework and a mobile web experience to build on top of.

##### ...via the magic of Turbo

The magic of Turbo comes from its hands-off approach to rendering. All content is derived from the existing Rails application, instead of being rebuilt natively in Swift.

Very simply, Turbo lets you "wrap" your website in native chrome. It renders the web content inside of a web view with native navigation.

This means that all of the existing mobile web content can be used *immediately* when you create the iOS app. And any new web screens automatically "just work" in the app.

When you're ready to level up a screen to native code, Turbo gives you hooks to set up your own custom view controllers. But this is entirely optional; lots of websites look great as is!

##### Apps powered by Turbo

Like Rails, Turbo was extracted from existing code at Basecamp. The team has been publicly using some form of Turbolinks since 2014. [Basecamp's mobile app](https://apps.apple.com/us/app/basecamp-3/id1015603248) and their new email service, [Hey](https://apps.apple.com/us/app/hey-email/id1506603805), are both powered by Turbo.

> Wait, what's the difference between Turbo and Turbolinks? In the context of *hybrid apps*, not much. Version 7 of Turbolinks was renamed to Turbo when Basecamp consolidated a few products into [Hotwire](https://hotwire.dev). On the web, [lots of new features were added](https://turbo.hotwire.dev).

Outside of official Basecamp apps, there are a number of independent hybrid apps powered by Turbo. I built [BeerMenus](https://apps.apple.com/us/app/beermenus-find-great-beer/id917882057)'s iOS app in 2014 and officially jumped on the hybrid bandwagon. I also actively maintain [Zaarly's iOS app](https://apps.apple.com/us/app/zaarly/id964717947) after building their first version in 2016.

Currently, I'm working with the fine folks at [Hoist](https://www.hoistup.com). They help people build successful home service businesses as quickly and painlessly as possible. A lot of design decisions and best practices expressed in this series were solidified while building this app.

Getting started with Turbo
--------------------------

Enough talk, let's see some code! The Turbo wiki includes a [quick start guide to Turbo](https://github.com/hotwired/turbo-ios/blob/main/Docs/QuickStartGuide.md). Let's build that code snippet from scratch.

The first TestFlight build I uploaded for Hoist didn't look too different from the following code!

##### 1\. Add the Turbo dependency

First, add the Turbo Swift package pointed to `https://github.com/hotwired/turbo-ios`. File -> Swift Packages -> Add Package Dependency... Since the package is technically still in beta, I'm pointing directly to the `main` branch. Feel free to leave the default and fetch up to the latest major release.

![Add the Turbo Swift package](https://masilotti.com/assets/images/turbo-ios/hybrid-apps-with-turbo/add-turbo-swift-package.png)

Add the Turbo Swift package

##### 2\. Create the core navigation

Then, open `SceneDelegate`, create a `UINavigationController`, and assign this to the window's `rootViewController`. This will handle the main navigation of the app.

```
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {
    var window: UIWindow?
    let navigationController = UINavigationController()

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let _ = (scene as? UIWindowScene) else { return }
        window!.rootViewController = navigationController
    }
}

```

At the core of Turbo is the `Session`. This is responsible for making network requests and letting your code know when someone clicks a link or encounters an error.

##### 3\. Wire up the app to Turbo

Import the Turbo framework and create an instance of `Session`. Assign the `SceneDelegate` as the session's delegate to get informed when a link is clicked.

```
import Turbo

class SceneDelegate {
    private lazy var session: Session = {
        let session = Session()
        session.delegate = self
        return session
    }()
}

extension SceneDelegate: SessionDelegate {
    func session(_ session: Session, didProposeVisit proposal: VisitProposal) {}
    func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {}
}

```

We'll get back to these callbacks in a second. For now, create a new helper function to perform a visit. A `Visit` in Turbo is essentially a click on a hyperlink, pretty much a web request.

##### 4\. Perform a `Visit`

This helper takes in a URL and passes it to the creation of a `VisitableViewController`. This comes from the Turbo framework and manages the shared web view, pull to refresh, and other minor details. All you need to know for now is that it renders the page.

Finally, tell the `Session` to visit this controller. Notice that the *controller* is visited, not a URL. This is a key concept in Turbo, where anything that conforms to the `Visitable` protocol can be visited via a `Session`. In this example we are using `VisitableViewController`, but you're free to create your own.

```
class SceneDelegate {
    private func visit(url: URL) {
        let viewController = VisitableViewController(url: url)
        navigationController.pushViewController(viewController, animated: true)
        session.visit(viewController)
    }
}

```

To kick off our first request, call this new helper from `scene(_:, willConnectTo:, options:)`. We are pointing to a demo web app from Basecamp that shows off a few of Turbo's features.

```
class SceneDelegate {
    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        // ...
        visit(url: URL(string: "https://turbo-native-demo.glitch.me")!)
    }
}

```

Build and run the app and you should see the rendered page!

![Turbo Native Demo running in the simulator](https://masilotti.com/assets/images/turbo-ios/hybrid-apps-with-turbo/turbo-native-demo.png)

Turbo Native Demo running in the simulator

However, nothing else seems to work. Try clicking a link. Notice that nothing happens? Let's revisit our `SessionDelegate` and implement those methods.

##### 5\. Implement `SessionDelegate`

```
extension SceneDelegate: SessionDelegate {
    func session(_ session: Session, didProposeVisit proposal: VisitProposal) {
        visit(url: proposal.url)
    }

    func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
        print(error)
    }
}

```

We can leverage the helper we created earlier to visit the new URL when someone clicks a link. Error handling will be explored in a future article.

Relaunch the app and try clicking around. Clicking links from the homepage should push a new controller on to the navigation stack. Just like a native app!

Hybrid app building blocks
--------------------------

Hopefully by now it's clear how powerful Turbo is when backed by a robust mobile web site. Adding a new page to the demo app doesn't require any changes to the client; it all just works.

Remember, the big value of hybrid is only having to make changes once. This is accomplished by moving as much logic as possible to the Rails app.

For example, you might want to present all forms modally. This follows iOS best practices and ties really nicely into Turbo's Path Configuration. The best part is that once configured it doesn't need to be adjusted for new workflows.

We've also built a JavaScript API to dynamically add navigation buttons to any screen in the app. We hook into a custom Stimulus controller and take advantage of SF Symbols on the client side. This gives us flexibility to change portions of the native UI without a client update and App Store review.

## 2 Url Routing

URL routing
===========



February 26, 2021

This is part 2 of a [6-part series on Hybrid iOS apps with Turbo](https://masilotti.com/turbo-ios/). In [part 1](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/) we touched on the basics of the Turbo framework and why hybrid can be a great choice. We went through the [official Quick Start guide](https://github.com/hotwired/turbo-ios/blob/main/Docs/QuickStartGuide.md) line by line and ended up with a working Turbo Native demo.

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  *Hybrid iOS apps with Turbo -- Part 2: URL routing*
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  [Hybrid iOS apps with Turbo -- Part 6: Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)

But a few links were broken and we shoved a bunch of code in the `SceneDelegate`. This week focuses on the different types of routing available in Turbo and how we implement each flavor. It also covers a couple of gotchas that are easy to miss but hard to fix.

Let's dive in!

All the code for this series can be found on my GitHub repository, [Turbo-iOS Demo](https://github.com/joemasilotti/Turbo-iOS-Demo). Each article has a "start" and "complete" branch if you'd like to follow along.

URL routing with Turbo
----------------------

Here are the different types of routing we will cover from the Turbo framework in this piece. Each lines up nicely with a broken link (or two) in the demo.

1.  Visit actions
2.  Path configuration
3.  Error handling
4.  External links
5.  Introduction to forms (and authentication)

But first, a quick refactor
---------------------------

Last week's code example threw all of the Turbo-related code right in the `SceneDelegate`. Let's move that to a new object so we can easily extend the behavior in the future.

##### Introducing the `AppCoordinator`

To start, we can move all of our logic to a coordinator. We won't be diving too deep into the coordinator pattern in this post. For now, think of this as a helper object that orchestrates the "flow" of the app. It will be in charge of bridging the gap between Turbo and the UI.

Pull down my [Turbo-iOS Demo](https://github.com/joemasilotti/Turbo-iOS-Demo) codebase and checkout the `part-2/start` branch. Notice that we moved all of the Turbo-related logic to `AppCoordinator`. Now `SceneDelegate` is left to do one thing: manage the scene.

Next, let's dig into our first broken link.

1\. Visit actions
-----------------

We find our first broken link by tapping "Navigate to another page" then "Replace with another webpage." This navigation should not have *pushed* a new view controller onto the stack. Instead, it should have *replaced* the visible content.

![This should have been a modal.](https://masilotti.com/assets/images/turbo-ios/url-routing/push-or-replace.png)

This should have been a modal.

This introduces a new Turbo concept: visit actions. Each time a link is clicked Turbo exposes the type of action in the `session(_:didProposeVisit:)` delegate callback.

The second parameter is a `VisitProposal`. This encapsulates all the information about the link being clicked. Most of the logic in the app will derive from interpreting the contents of this object.

Note the object hierarchy below. We can determine which action was triggered via: `proposal.options.action`.

```
public struct VisitProposal {
    public let url: URL
    public let options: VisitOptions
    public let properties: PathProperties
}

public struct VisitOptions: Codable, JSONCodable {
    public let action: VisitAction
    public let response: VisitResponse?
}

public enum VisitAction: String, Codable {
    case advance
    case replace
    case restore
}

```

##### `advance` visit action

Advance is the most commonly used action and also the most straightforward. When a link is clicked via the `advance` action a new screen should be *pushed* onto the navigation stack.

##### `replace` visit action

Instead of pushing a view controller onto the stack, `replace` instead...well... replaces it. This gives the impression of the content reloading or updating to reflect a change.

A major benefit is that we can submit a form then replace the form contents with the "show" CRUD action to give the impression of modifying content natively.

##### `restore` visit action

We won't generate `restore` links directly but will need to handle them in the app. These are reserved for revisiting content that should already be cached - for example, navigating back to a previous page.

Moving forward, we will handle `restore` actions the same way as `replace` ones.

##### Handle non-advance Turbo links in the app

Now that we understand how visit actions work, lets implement the changes in our iOS app. We will start at the delegate callback mentioned earlier.

Change the implementation to pass the visit action along with the URL.

```
func session(_ session: Session, didProposeVisit proposal: VisitProposal) {
    visit(url: proposal.url, action: proposal.options.action)
}

```

Next, update `visit(url:)` to accept the new parameter. When we get a non-advance visit, we want to replace the last controller with our new one. As a convenience, we can also default the `action:` parameter to `advance`.

```
private func visit(url: URL, action: VisitAction = .advance) {
    let viewController = VisitableViewController(url: url)
    if action == .advance {
        navigationController.pushViewController(viewController, animated: true)
    } else {
        navigationController.viewControllers = Array(navigationController.viewControllers.dropLast()) + [viewController]
    }
    session.visit(viewController)
}

```

By setting the navigation controller's `viewControllers` property directly, we don't trigger any animations. It all happens at the same time we get a seamless transition into replacing the screen.

2\. Path configuration
----------------------

Tap on that "Load a page modally" link. See how it slides up from the bottom of the screen like a native modal? Oh, what? It doesn't? Ah, silly me. We haven't added routing yet!

Routing, in the context of Turbo, is the translation of links to view controllers and presentation styles. It enables you to render native view controllers, present screens modally, and do all sorts of custom logic.

At its core, routing is based on the URL, allowing specific "type" of URLs to behave differently. For example, you could present all URLs ending in `/new` to be presented modally. Or, you could show a native view controller when the path is `/settings`.

##### `PathConfiguration.json`

Lucky for us, Turbo has taken the hard work out of URL routing. Instead of manually parsing regexes or other custom logic, we can provide a single JSON file to the framework.

This path configuration file maps URLs to behavior via regexes. When a URL is mapped we can pry into the associated rules that were applied via `PathProperties`, accessed via `Proposal.properties`.

Here's a snippet from the [example path configuration file](https://github.com/hotwired/turbo-ios/blob/main/Docs/PathConfiguration.md) from the Turbo-iOS repository. Let's walk through this and cover what each line means.

```
{
  "settings": {
    "enable-feature-x": true
  },
  "rules": [
    {
      "patterns": [
        "/new$",
        "/edit$"
      ],
      "properties": {
        "presentation": "modal"
      }
    }
  ]
}

```

First we have the `settings` section. These are properties that are applied to each and every URL when routed. They are useful for feature flags and toggling other generic behavior.

Next is the `rules` section, the meat of the file. Only one rule is listed but it matches two different patterns. If the routed URL ends in `/new` or `/edit` we want to present this screen modally.

##### Wire up the path configuration

The first step is adding the JSON file to the project and letting `Session` know about it. Under the `Resources` group add a new file named `PathConfiguration.json` with the following content.

```
{
  "rules": [
    {
      "patterns": [
        "/new$"
      ],
      "properties": {
        "presentation": "modal"
      }
    }
  ]
}

```

Then, update the `session` lazy variable to be configured with our local JSOn file.

```
private lazy var session: Session = {
    let session = Session()
    session.delegate = self
    session.pathConfiguration = PathConfiguration(sources: [
        .file(Bundle.main.url(forResource: "PathConfiguration", withExtension: "json")!),
    ])
    return session
}()

```

###### Remote configuration

If you typed this out manually you might notice that `PathConfiguration` takes a few different types of sources. We are only using the local one, but you can also point it directly to a URL on your server.

The local file is loaded first, then the configuration is overridden with the remote one, if given. This enables remote configuration of URLs and routes without updating your app!

##### Route the URL

Now that we've assigned our rules, how do we actually apply the routing? Let's revisit our `SessionDelegate` callback and expose the properties to `visit(url:action:)`.

```
func session(_ session: Session, didProposeVisit proposal: VisitProposal) {
    visit(url: proposal.url, action: proposal.options.action, properties: proposal.properties)
}

```

Now we need to update our `visit` signature to handle the new parameter. Like last time, give it a sane default for when we don't know or care about the properties.

Also, before pushing or replacing our view controller let's check for the presentation property. If its equal to `modal`, then we present the view controller instead of pushing it on the navigation stack.

```
private func visit(url: URL, action: VisitAction = .advance, properties: PathProperties = [:]) {
    let viewController = VisitableViewController(url: url)
    if properties["presentation"] as? String == "modal" {
        navigationController.present(viewController, animated: true)
    } else if action == .advance {
        navigationController.pushViewController(viewController, animated: true)
    }
    /* ...*
}

```

Now the modal link should work as expected. Do note that we haven't handled the "Submit Form" link yet, and tapping it will cause odd things to happen. Rest assured, we will get to forms later in the series.

![Presented as a modal](https://masilotti.com/assets/images/turbo-ios/url-routing/modal.png)

Presented as a modal

##### Dismissing the modal breaks the app!

Uh-oh, looks like we introduced a bug. If you dismiss the modal, you can no longer tap on any links.

This is caused by the way Turbo works under the hood. There's a lot of [magic](https://github.com/hotwired/turbo-ios/blob/ca008e8215c66c2a276862375709b5c819b8b8b8/Source/Visitable/Visitable.swift#L43) going on to make sure each link visit transition occurs smoothly, all out of the scope of this series.

For now, all we need to know is that modals need their own `Session`. This ensures that a) dismissing a modal doesn't break anything and b) we don't create a new session every time someone taps this link.

First, extract the lazy variable to a helper method. Then, create a `modalSession` variable via the new helper.

```
private lazy var session = makeSession()
private lazy var modalSession = makeSession()

private func makeSession() -> Session {
    let session = Session()
    /* ... */
    return session
}

```

Now we only need to `visit()` the correct `session`. Replace the last line of `visit(url:action:properties:)` with the following.

```
if properties["presentation"] as? String == "modal" {
    modalSession.visit(viewController)
} else {
    session.visit(viewController)
}

```

Native view controllers
-----------------------

This approach is not limited to presentation logic; we can also route to different view controllers. Let's piggy-back on the example server's "Intercept with a native view" link to show some native content.

First, add a new rule to `PathConfiguration.json`.

```
{
  "patterns": [
    "/numbers"
  ],
  "properties": {
    "controller": "numbers"
  }
}

```

Next, rework our `visit(url:action:properties)` implementation to dynamically create the controller based on the path properties. Also, make sure to only visit the session if the controller is `Visitable`.

```
private func visit(url: URL, action: VisitAction = .advance, properties: PathProperties = [:]) {
    let viewController: UIViewController

    if properties["controller"] as? String == "numbers" {
        viewController = NumbersViewController()
    } else {
        viewController = VisitableViewController(url: url)
    }

    /* ... */

    if let visitable = viewController as? Visitable {
        if properties["presentation"] as? String == "modal" {
            modalSession.visit(visitable)
        } else {
            session.visit(visitable)
        }
    }
}

```

The implementation of `NumbersViewController` isn't relevant - it could be any native content. For completeness, here's my implementation.

```
class NumbersViewController: UIHostingController<NumbersView> {
    init() {
        super.init(rootView: NumbersView())
    }
}

struct NumbersView: View {
    private let numbers = 1 ... 10

    var body: some View {
        List(numbers, id: \.self) { number in
            Text(String(number))
        }
    }
}

struct NumbersView_Preview: PreviewProvider {
    static var previews: some View {
        NumbersView()
    }
}

```

![A native view controller with Turbo iOS](https://masilotti.com/assets/images/turbo-ios/url-routing/numbers-view-controller.png)

A native view controller with Turbo iOS

###### Refactor imminent...

This method is getting a little ugly, and we are checking the presence of a magic string twice. I'm going to clean this up a bit and extract a helper to check for modal presentation. See you on the [other side](https://github.com/joemasilotti/Turbo-iOS-Demo/commit/6f462dd14c220e6e4b4456aa21dcd14dfb67e569)!

Error handling with Turbo
-------------------------

The next broken link is "Hit an HTTP 404 error." Clicking that shows a spinner, then a blank page. (Or, maybe this is the perfect example of a 404! 😆)

To fix this we need to address the other `SessionDelegate` callback, `session(_:didFailRequestForVisitable:error:)`. Currently, we are doing nothing more than logging the error.

Instead, let's render the error message in a custom view. This example uses SwiftUI, but feel free to drop in any ol' `UIViewController`.

First, create the SwiftUI view. It will be passed the error message as a string. I added this to a new group called "Views."

```
import SwiftUI

struct ErrorView: View {
    let errorMessage: String

    var body: some View {
        VStack(spacing: 12) {
            Image(systemName: "exclamationmark.triangle")
                .resizable()
                .scaledToFit()
                .foregroundColor(.accentColor)
                .frame(height: 40)
            Text("Error loading page")
                .font(.title)
            Text(errorMessage)
        }
    }
}

```

Back in `AppCoordinator`, replace the implementation of the error handling with the following. This creates the `ErrorView`, wraps it in a `UIHostingController`, then positions it as a child view controller of the top view controller.

```
func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
    guard let topViewController = navigationController.topViewController else { return }

    let swiftUIView = ErrorView(errorMessage: error.localizedDescription)
    let hostingController = UIHostingController(rootView: swiftUIView)

    topViewController.addChild(hostingController)
    hostingController.view.frame = topViewController.view.frame
    topViewController.view.addSubview(hostingController.view)
    hostingController.didMove(toParent: topViewController)
}

```

You could also add a button to this view that tries to reload the page. Since we have a reference to the `Session` all we need to do is ask it to refresh via `session.reload()`. This will clear the Turbo cache and revisit the current page.

External links
--------------

Up next is "Follow an external link." Tapping this opens the framework's GitHub repository in Safari. While not technically broken, we can improve this UX by instead by opening an in-app browser.

An external link is any URL that doesn't match Turbo's root URL domain. We kicked off the app pointing to `https://turbo-native-demo.glitch.me`, so anything that doesn't match `turbo-native-demo.glitch.me` is considered "external" by the framework.

##### `WKNavigationDelegate`

The callback for these links happens in a new delegate, `WKNavigationDelegate`. This lives off of the web view provided by Turbo's `Session`.

Add the following to `SessionDelegate`. This makes the coordinator the navigation delegate only when a Turbo request finishes.

```
func sessionDidLoadWebView(_ session: Session) {
    session.webView.navigationDelegate = self
}

```

Then, extend `AppCoordinator` to implement the new delegate. This also requires importing `WebKit` and making the coordinator inherit from `NSObject`.

```
import WebKit

class AppCoordinator: NSObject {
    /* ... */
}

extension AppCoordinator: WKNavigationDelegate {}

```

##### `SFSafariViewController`

All that's left is actually displaying the content. I'm using the [standard in-app browser](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) but you are free to roll your own.

Implement `webView(_: decidePolicyFor:decisionHandler:)` in the navigation delegate. We only want to catch tapped links, so we want to check that the navigation type is `.linkActivated`. If so, we cancel the request and handle it on our own, via the Safari view controller.

```
import SafariServices

func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void) {
    guard
        navigationAction.navigationType == .linkActivated,
        let url = navigationAction.request.url
    else {
        decisionHandler(.allow)
        return
    }

    let safariViewController = SFSafariViewController(url: url)
    navigationController.present(safariViewController, animated: true)
    decisionHandler(.cancel)
}

```

Introduction to forms (and authentication)
------------------------------------------

A big surprise with Turbo development is that all non-GET requests are ignored. This means that normal (non-remote) form submissions no-op. No error message, no logs, just... nothing.

The short answer is that you need to convert these forms to AJAX. In a Rails world, this means `remote: true` or `local: false`, depending on which version of Rails you are running.

If you are on Rails 6.1 and Turbo v7, however, you can ignore all of this. All form submissions are handled via JavaScript which makes Turbo Native "just work" by default. If you are still running Turbolinks (Turbo v5) then you need to convert all of your forms by hand.

Part 3 will address the form conversion with a generic Stimulus controller. A client is using this JavaScript in production for 30+ forms while we transition from Turbolinks to Turbo.

We will also transition from the Turbo demo server to a real Rails app. Then, finally, can we start to talk about authentication!
## 3 Forms And Basic Authentication

Forms and basic authentication
==============================



March 19, 2021

This is part 3 of a [6-part series on Hybrid iOS apps with Turbo](https://masilotti.com/turbo-ios/). We kicked off with an [introduction to the Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/) and touched on why hybrid can be a great choice. Part 2 dove into [URL routing with Turbo](https://masilotti.com/turbo-ios/url-routing/) and how to get your path configuration set up.

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  *Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication*
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  [Hybrid iOS apps with Turbo -- Part 6: Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)

This article focuses on two major components of hybrid app development: forms and authentication. We will also migrate from Basecamp's example app to a real Rails app as examples to illustrate the points discussed. Let's dive in!

Turbo installation
------------------

If you're running Ruby on Rails 6.1+ with Turbo (v7) installed you can [skip this part](https://masilotti.com/turbo-ios/forms-and-basic-authentication/#basic-crud).

##### Step 0: Upgrade to Rails 6.1

This is technically optional, but the rest of this article assumes you are using Rails 6.1. This release [generates non-remote forms by default](https://github.com/rails/rails/pull/40708). This means no AJAX or JavaScript, regular old HTTP forms.

The PR has more details on how to make this the default configuration for earlier versions of Rails.

##### Step 1: Install `turbo-rails`

The `turbo-rails` gem adds the Turbo JavaScript and some additional helpers to your Rails application. Most importantly, it intercepts form submissions to respond with Turbo streams.

Following the [instructions from the README](https://github.com/hotwired/turbo-rails#installation):

1.  Add `gem 'turbo-rails'` to your Gemfile
2.  Run `bundle install`
3.  Run the generator with `rails turbo:install`

##### Step 2: Wire up the JavaScript

If you are using webpack(er), you can add the following to the end of your JavaScript pack. This imports the framework and exposes it to native adapters.

```
import { Turbo } from "@hotwired/turbo-rails"
window.Turbo = Turbo

```

Now is a good time to audit your app for any references to Turbo_links_. Most of the upgrade can be done with a find-and-replace and [Go Rails has a free video with more details](https://gorails.com/episodes/upgrade-from-turbolinks-to-hotwire-and-turbo).

Basic CRUD
----------

You can now start pointing your iOS app to your Rails server. If Turbo is configured you should be able to navigate around and tap through links.

Don't have a Turbo iOS app yet? The [first two parts](https://masilotti.com/turbo-ios/) of this series build one from scratch! Or, feel free to [download the source directly](https://github.com/joemasilotti/Turbo-iOS-Demo).

To demonstrate how well Turbo works out of the box, I'm using the default Rails scaffolding generator. This creates the route, database migration, ActiveRecord model, controller, and views.

```
rails generate scaffold BoardGame name:string players:integer

```

Run this command, migrate your database with `rails db:migrate`, and visit <http://localhost:3000/board_games> in your browser. You can view, create, edit, update, and destroy board games.

Even better, open the iOS app. Everything should work there, too! This is because Turbo (not Turbolinks) now handles form submissions entirely - no need for custom JavaScript to get everything working.

Validations and invalid forms
-----------------------------

However, there is one thing we need to handle manually. Open up the `BoardGame` model and add a validation. For example, that `name` has to be present.

```
class BoardGame < ApplicationRecord
  validates :name, presence: true
end

```

Submitting the form without a name will generate a flash message in your browser. Standard Rails stuff.

![Standard Rails flash message.](https://masilotti.com/assets/images/turbo-ios/forms-and-basic-authentication/flash-message-web.png)

Standard Rails flash message.

But try the same in the iOS app. The submit button gets disabled but then that's it. Nothing else happens. What gives?

![iOS form with the submit button disabled, but it doesn't seem to have actually submitted.](https://masilotti.com/assets/images/turbo-ios/forms-and-basic-authentication/broken-form-ios.png)

iOS form with the submit button disabled, but it doesn't seem to have actually submitted.

From the generator, our controller re-renders the "new" view if the board game is invalid. By default, this sets the response status code as 200 OK.

```
def create
  @board_game = BoardGame.new(board_game_params)

  if @board_game.save
    redirect_to @board_game, notice: 'Board game was successfully created.'
  else
    render :new
  end
end

```

The Turbo JavaScript doesn't know what to do with a `200 OK`. Instead, we can let the framework know something went wrong by giving it [anything in the 400 or 500 range](https://twitter.com/dhh/status/1346448749170749449?s=20); `422 Unprocessable Entity` works great.

```
render :new, status: :unprocessable_entity

```

Double pushed controllers
-------------------------

Now that forms are working you might notice a different issue. If you view then edit a board game, you end up with two "show" controllers on the navigation stack.

This is occurring because our `redirect_to` is coming down the wire as `VisitAction.advance`, which always pushes a new controller.

We can fix this by overwriting the `.advance` action. If we are being redirected to the same URL we are already viewing then perform a `.replace` instead.

```
let action: VisitAction = url ==
  session.topmostVisitable?.visitableURL ? .replace : action

```

Turbolinks form submissions
---------------------------

There's a bit more work if your server hasn't migrated to Turbo (v7) and is still using Turbolinks (v5). We no longer have access to all of that generic form handling JavaScript so we are forced to write our own.

My client and I have generalized most of this work into a single Stimulus controller and corresponding View Component. The component takes in the name of the partial to re-render and the controller hooks into the AJAX form submission.

The bones of the approach listens for the `ajax:error` event. When fired, the form is re-rendered. While naive, it goes a long way in keeping the amount of custom JavaScript low while you migrate to Turbo.

```
import { Controller } from "stimulus"

export default class extends Controller {
  onError({ detail: [data, , xhr] }) {
    this.element.innerHTML = xhr.response;
  }
}

```

```
<%= form_with(model: board_game, local: false, data: {
  controller: "form",
  action: "ajax:error->form#onError"
}) do |form| %>
  <%# ... %>
<% end %>

```

Basic authentication
--------------------

The Turbo-iOS repo outlines [a few approaches to authentication](https://github.com/hotwired/turbo-ios/blob/main/Docs/Authentication.md). Cookie-based authentication, which relies on the web view for session management, requires very little work. Native authentication is much more in depth, but has a few key benefits.

##### Cookie-based authentication

Many hybrid apps can get by with this approach. In short, you let the web view internally manage the cookies and session. There are, however, two gotchas.

First, the authentication cookie must never expire. It would feel very un-native to have to sign back in to an app every two weeks! If you are manually setting cookies in Rails you can use the `permanent` helper.

```
cookies.permanent.signed["user_id"] = current_user.id

```

> `#signed` sets a signed cookie, which prevents users from tampering with its value. The cookie is signed by your app's `secrets.secret_key_base` value. It can be read using the signed method `cookies.signed[:name]`. - [ActionDispatch::Cookies < Object](https://api.rubyonrails.org/v5.1.7/classes/ActionDispatch/Cookies.html)

With Devise you need to make two changes: one to your `User` model and the other to the Devise configuration.

```
### app/models/user.rb
class User < ApplicationRecord
  def remember_me
    (super == nil) ? '1' : super
  end
end

### config/initializers/devise.rb
Devise.setup do |config|
  config.remember_for = 20.years
end

```

These changes ensure the user is always remembered "forever." 20 years is what Rails uses for [permanent cookies](https://apidock.com/rails/ActionDispatch/Cookies/CookieJar/permanent). You might also want to hide the "Remember me?" option in the sign in form.

##### Client changes

We need to do very little to get this to work on the client. Since we are [routing `/new` paths to a modal controller](https://masilotti.com/turbo-ios/url-routing/), the sign in form already looks great. Signing in closes the modal and pushes or replaces a new page.

However, we don't seem to be signed in on that newly loaded page. What gives?

Turns out, each `Session` uses a distinct web view. And each `WKWebView` has its own cookie jar. We can tell them to share cookies with each other by initializing them with the same `WKProcessPool`.

```
let sharedProcessPool = WKProcessPool()
let configuration = WKWebViewConfiguration()
configuration.processPool = sharedProcessPool

let mainSession = Session(webViewConfiguration: configuration)
let modalSession = Session(webViewConfiguration: configuration)

```

##### Native authentication

One major limitation of web-only authentication is, well, its web only. That limits us to only interacting with our server via HTML and JavaScript. You're out of luck if you need to make an authenticated HTTP request. And since those usually power the interesting native screens, those are off the table, too.

Native authentication in a hybrid app follows this rough outline:

1.  Present a native sign in screen
2.  Sign in via a secure HTTP request
3.  Receive an authentication token for future requests
4.  Pass that token to the web view to persist the cookies

I've been doing some heavy thinking on this and have implementation recommendations. These will be discussed in the "native screens" article of this series.

Can't wait? Here's a sneak peek of what I will be covering.

1.  A native sign in screen powered by SwiftUI
2.  JWT-based auth via the [API Guard](https://github.com/Gokul595/api_guard) gem
3.  Parsing the `Set-Cookie` HTTP header response and passing the cookies to the web view

*Really* can't wait? Feel free to [send me an email](mailto:joe@masilotti.com) if you'd like 1:1 help.

Up next: The JavaScript bridge
------------------------------

Now that forms and basic authentication are out of the way we can dive into more exciting Turbo-iOS features.

The next article [in the series](https://masilotti.com/turbo-ios/) will cover the JavaScript bridge - this is how we send messages between Rails and iOS without HTTP requests. I use the bridge to trigger native actions, render native controls, register push notification tokens, and lots of other fun stuff.
## 4 The Javascript Bridge

The JavaScript bridge
=====================



April 02, 2021

This is part 4 of a 6 part series on building hybrid iOS apps with Turbo. Parts 1 through 3 built us an "out of the box" hybrid app with [navigation](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/), [URL routing](https://masilotti.com/turbo-ios/url-routing/), [forms, and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/). This week, we will customize our app to make it feel more native.

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  *Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge*
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  [Hybrid iOS apps with Turbo -- Part 6: Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)

One of the big trade-offs of hybrid apps is that all interaction (and content) usually lives in the web view. This means we can update it without much issue by making changes to our Rails app. But what if we want a native navigation bar button? Or want to register a notification token with the server?

Enter the JavaScript bridge, the intersection of client and server. With this bridge, we can pass messages between the two worlds without waiting for someone to tap a link.

Like most bridges, this one is a two-way street. Let's first dive into how the client can post messages to the rendered HTML. Then we will cross back over by talking to the client.

Client → Server
---------------

`WKWebView`, the web view that Turbo is built on top of, has a helper to evaluate arbitrary JavaScript. The method expects the JavaScript to execute and a completion handler. You can handle the returned object or raised error with the completion block.

```
let webView = session.webView
let script = "document.body.style.background = 'orange';"
webView.evaluateJavaScript(script) { object, error in
    if let error = error {
        // handle error
    } else if let object = object {
        // success
    }
}

```

> If you are targeting iOS 14+ I recommend taking a look at [`callAsyncJavaScript( _:arguments: in: in: completionHandler:)`](https://developer.apple.com/documentation/webkit/wkwebview/3656441-callasyncjavascript), which automatically serializes arguments.

Now that we know how to execute a script, let's integrate with our server's JavaScript. First, create a new JavaScript file in your `app/javascript/` directory. I put mine under a new folder named "turbo."

```
// app/javascript/turbo/bridge.js
export default class Bridge {
  static sayHello() {
    document.body.innerHTML = "<h1>Hello!</h1>"
  }
}

```

Then, attach this new class to the `window` by adding the following to your `application.js` pack file. This enables us to call into `Bridge` from any context, like our mobile app.

```
import Bridge from "turbo/bridge.js";
window.bridge = Bridge;

```

Finally, call your bespoke JavaScript from the mobile app. This method can't fail and doesn't return anything, so we are ignoring the two parameters of the callback.

```
let webView = session.webView
let script = "window.bridge.sayHello();"
webView.evaluateJavaScript(script) { _, _ in }

```

##### POSTing push notification tokens

We can extend this technique to do something *actually* useful, like associating a notification token with the sign in user.

First, let's get the Rails code out of the way. Feel free to skip this code snippet if you already have an endpoint to register notification tokens. We need...

1.  A place to store the tokens
2.  An association with the user
3.  A controller to create the new token
4.  Routing to accept the POST request

```
### 1. db/migrate/create_notification_tokens.rb
class CreateNotificationTokens < ActiveRecord::Migration
  def change
    create_table :notification_tokens do |t|
      t.belongs_to :user
      t.string :token, null: false

      t.timestamps
    end
  end
end

### 2. app/models/user.rb
class User < ApplicationRecord
  has_many :notification_tokens
end

### 3. app/controllers/notification_tokens_controller.rb
class NotificationTokensController < ApplicationController
  skip_before_action :verify_authenticity_token
  before_action :authenticate_user!

  def create
    current_user.notification_tokens.find_or_create_by!(token: params[:token])
    head :ok
  end
end

### 4. config/routes.rb
Rails.application.routes.draw do
  resources :notification_tokens, only: :create
end

```

Next up is the JavaScript. Add a new method to your `Bridge` class that accepts the token as a parameter and POSTs the token as JSON.

```
export default class Bridge {
  static register(token) {
    fetch("/notification_tokens", {
      body: JSON.stringify({ token: token }),
      method: "POST",
      headers: { "Content-Type": "application/json" },
    });
  }
}

```

Finally, we can call this function from our native code like before.

```
let webView = session.webView
let script = "window.bridge.register(\(token));"
webView.evaluateJavaScript(script) { _, _ in }

```

Since we are already authenticated in the web view we don't need to pass any sort of authentication with the request. This saves us a *ton* of Swift networking boilerplate. The downside is we need to ignore the CSRF check in the controller, but this can be avoided by [adding the token to the POST request](https://discuss.hotwired.dev/t/csrf-token-invalidauthenticitytoken/91/3).

Server → Client
---------------

OK, so now we have the iOS app talking to our Rails app. But what about the other way around? How do we send a message from Rails to the iOS client?

In a similar fashion to above, we need to expose a JavaScript hook. WebKit provides a convenient interface to receive JavaScript messages in a single delegate callback.

Let's get started by creating our message handler. This class needs to conform to the `WKScriptMessageHandler` protocol and implement a single method.

```
class ScriptMessageHandler: NSObject, WKScriptMessageHandler {
    func userContentController(
        _ userContentController: WKUserContentController,
        didReceive message: WKScriptMessage
    ) {
        print("JavaScript message received", message.body)
    }
}

```

We can then attach this to our web view via the configuration and pass it along to Turbo's `Session`. The `name` parameter provides a namespace, here we are using `nativeApp`.

```
let configuration = WKWebViewConfiguration()
let scriptMessageHandler = ScriptMessageHandler()
configuration.userContentController.add(scriptMessageHandler, name: "nativeApp")

let session = Session(webViewConfiguration: configuration)
// ...

```

Now, our Rails app can post JavaScript messages via WebKit's message handlers via the namespace set above. This message will arrive in our delegate callback with a serialized `body` of type `[String: Any]`.

```
window.webkit.messageHandlers.nativeApp
  .postMessage({name: "Message Name", more: "data"});

```

From there, we can parse out the name and any additional parameters. And based on which message we receive we can perform different native functionality.

##### Dynamically adding a native button

One of my clients uses this approach to add a native `UIBarButtonItem` to some screens. We call it an *Action Button* and configure everything from the server, including:

1.  Which screens show the button
2.  The icon the button displays
3.  Which URL to load when tapping the button

![A native UIBarButton item](https://masilotti.com/assets/images/turbo-ios/the-javascript-bridge/my-customers.png)

A native UIBarButton item

For screens that should show the button we post the following JavaScript message.

```
window.webkit.messageHandlers.nativeApp.postMessage({
  name: "ActionButton",
  path: "/customers/new",
  icon: "plus"
});

```

We attach a delegate to our script message handler and pass along the action. This bridges the gap between JavaScript and Swift.

```
protocol ScriptMessageDelegate: class {
    func addActionButton(url: URL, imageName: String)
}

class ScriptMessageHandler: NSObject, WKScriptMessageHandler {
    private weak var delegate: ScriptMessageDelegate?

    init(delegate: ScriptMessageDelegate) {
        self.delegate = delegate
    }

    func userContentController(
        _ userContentController: WKUserContentController,
        didReceive message: WKScriptMessage
    ) {
        guard
            let body = message.body as? [String: Any],
            let path = body["path"] as? String,
            let imageName = body["icon"] as? String
        else { return }

        let url = Endpoints.rootURL.appendingPathComponent(path)
        delegate?.addActionButton(url: url, imageName: imageName)
    }
}

```

This approach works fine for a single message. But when you have more than one I recommend creating a concrete type and doing the parsing there. A great example is [`ScriptMessage.swift`](https://github.com/hotwired/turbo-ios/blob/main/Source/WebView/ScriptMessage.swift) from the Turbo source code.

Now the fun part: Adding the button to the screen. Head back to our custom delegate callback --- the one responsible for creating the handler and session. Add the button and route the URL when tapped. And my favorite, use the image name to render a [SF Symbol icon](https://developer.apple.com/sf-symbols/)!

```
private var nextActionButtonURL: URL?

func addActionButton(url: URL, imageName: String) {
    let image = UIImage(systemName: imageName) // 🤩
    let actionButton = UIBarButtonItem(
        image: image,
        style: .plain,
        target: self,
        action: #selector(visitActionButtonURL)
    )
    navigationController.visibleViewController?
        .navigationItem.rightBarButtonItem = actionButton
}

@objc private func visitActionButtonURL() {
    if let url = nextActionButtonURL {
        route(url: url)
    }
    nextActionButtonURL = nil
}

```

A single line of JavaScript can now add custom buttons across our entire app with different icons and different functionality. Who would ever have thought JavaScript could be so powerful for iOS developers?

Looking ahead at Strada
-----------------------

Not a fan of all this JavaScript? You might be in luck. The bottom of [Hotwire's homepage](https://hotwired.dev) hints at a new part of the puzzle, Strada.

> [Strada] standardizes the way that web and native parts of a mobile hybrid application talk to each other via HTML bridge attributes. This makes it easy to progressively level up web interactions with native replacements.

My guess is that Strada will move this "on load" JavaScript to special `<meta>` tags in the HTML's `<head>`. And the framework will automatically parse them and provide native callbacks. This could speed up development drastically and remove the need to write custom Stimulus controllers to fire the methods.

Or maybe it's something else entirely! Basecamp likes to keep everything quite secret until they launch, so only time will tell.

Up next: native authentication
------------------------------

The [next part in this series](https://masilotti.com/turbo-ios/) is a big one: native authentication. I'm going to dive into how to present native screens from Turbo and how to implement authentication natively -- no web view required!
## 5 Native Authentication

Native authentication
=====================



April 22, 2021

Welcome back to my [6-part series on hybrid iOS apps with Turbo](https://masilotti.com/turbo-ios/). In [part 3](https://masilotti.com/turbo-ios/forms-and-basic-authentication/) we learned how to do basic authentication via the web view.

One major limitation of web-only authentication is, well, it's web only. That limits us to only interacting with our server via HTML and JavaScript. You're out of luck if you need to make an authenticated HTTP request.

Native authentication, on the other hand, opens up a world of possibilities. It breaks your app out of the web world and enables fully native screens. Meaning, you can integrate native SDKs like location services and push notifications. Or, you can render SwiftUI views for the really important stuff!

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  *Hybrid iOS apps with Turbo -- Part 5: Native authentication*
6.  [Hybrid iOS apps with Turbo -- Part 6: Tips and tricks](https://masilotti.com/turbo-ios/tips-and-tricks/)

Before diving in, let's outline the flow of information through the server and client.

![Native authentication workflow](https://masilotti.com/assets/images/turbo-ios/native-authentication/native-authentication-workflow.png)

Native authentication workflow

These steps can be grouped into three big flows: unauthenticated requests, initial authentication, and authenticated requests.

1.  [Unauthenticated requests](https://masilotti.com/turbo-ios/native-authentication/#1-unauthenticated-requests)
    1.  Client requests an authenticated endpoint
    2.  Server returns a 401 Unauthorized status code
    3.  Client renders a native form
2.  [Initial authentication](https://masilotti.com/turbo-ios/native-authentication/#2-initial-authentication)
    1.  Client POSTs the credentials
    2.  Server creates an access token and signs in the user
    3.  Client persists the access token and saves the cookies
3.  [Authenticated requests](https://masilotti.com/turbo-ios/native-authentication/#3-authenticated-requests)
    1.  Client uses the token to authenticate native screens
    2.  Server authenticates user via token

1\. Unauthenticated requests
----------------------------

In order to catch the unauthenticated response in Turbo we need the server to return a non-200 status code. [401 Unauthorized](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/401) is perfect, but you can also use [403 Forbidden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403).

If you're using Devise, you can set up a [Failure App](https://www.rubydoc.info/github/plataformatec/devise/Devise/FailureApp) to render custom status codes when your `authenticate_user!` before action fails. Add the following to `config/initializers/devise.rb` to configure the custom Failure App.

```
class TurboFailureApp < Devise::FailureApp
  include Turbo::Native::Navigation

  def respond
    if turbo_native_app?
      http_auth
    else
      super
    end
  end
end

Devise.setup do |config|
  # Your existing configuration...

  config.warden do |manager|
    manager.failure_app = TurboFailureApp
  end
end

```

`#turbo_native_app?` is part of [turbo-rails](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb) and checks if the user agent contains "Turbo Native." Make sure to set your user agent on each `Session` you use.

```
let session = Session()
session.webView.customUserAgent = "My App (Turbo Native) / 1.0"

```

##### Catching the error

Back to the client. Like all other errors, this response will route to `session(_:didFailRequestForVisitable:error:)`. We need to check the status code and kick off the authentication flow.

Sadly, the error parameter is untyped. So we need to first check if it is a `TurboError` and of type `.http`. If so, we can verify the status code.

```
func session(_ session: Session, didFailRequestForVisitable visitable: Visitable, error: Error) {
    if error.isUnauthorized {
        // Render native sign-in flow
    } else {
        // Handle actual errors
    }
}

extension Error {
    var isUnauthorized: Bool { httpStatusCode == 401 }

    private var httpStatusCode: Int? {
        guard
            let turboError = self as? TurboError,
            case let .http(statusCode) = turboError
        else { return nil }
        return statusCode
    }
}

```

Once we know the user needs to authenticate we can handle the sign-in flow natively. I usually reach for a new coordinator, but feel free to present a view controller if that is more comfortable for you.

##### Native sign-in form

At a minimum, your sign-in form needs an email field, a password field, and a submit button. I've been using `UIHostingController` to wrap SwiftUI views lately and I really like the ergonomics. You get the short feedback loops of SwiftUI but aren't required to convert your entire app away from UIKit.

```
let viewModel = SignInViewModel()
let view = SignInView(viewModel: viewModel)
let controller = UIHostingController(rootView: view)
navigationController.present(controller, animated: true)

class SignInViewModel: ObservableObject {
    @Published var email: String = ""
    @Published var password: String = ""

    func signIn() {
        // TODO: POST credentials to server.
    }
}

struct NewSessionView: View {
    @ObservedObject var viewModel: SignInViewModel

    var body: some View {
        Form {
            TextField("name@example.com", text: $viewModel.email)
                .textContentType(.username)
                .keyboardType(.emailAddress)

            SecureField("password", text: $viewModel.password)
                .textContentType(.password)

            Button("Sign in", action: viewModel.signIn)
        }
    }
}

```

This view isn't styled, but SwiftUI and `Form` do a pretty good job making it look decent. Also, this would have been like 50 lines of UIKit code. 😆

![SwiftUI Form](https://masilotti.com/assets/images/turbo-ios/native-authentication/native-sign-in-form.png)

SwiftUI Form

2\. Initial authentication
--------------------------

Once the user taps "Sign in" we need to send their email/password to the server. We also need to set the user agent and content type to JSON on the request. This ensures Rails can identify it as a Turbo Native API request.

```
func signIn() {
    URLSession.shared.dataTask(with: request) { data, response, error in
        // TODO: Handle response: persist token and cookies
    }
}

private var request: URLRequest {
    var request = URLRequest(url: url)
    request.httpMethod = "POST"

    request.setValue("application/json", forHTTPHeaderField: "Content-Type")
    request.setValue("My App (Turbo Native)", forHTTPHeaderField: "User-Agent")

    let credentials = Credentials(email: email, password: password)
    request.httpBody = try? JSONEncoder().encode(credentials)

    return request
}

private struct Credentials: Encodable {
    let email: String
    let password: String
}

```

##### Generate an access token

Back to the server. We need to authenticate this request, create an access token, and sign in the user. The access token will be used for future native requests and the cookies for future web requests.

First, authenticate the email/password combination. If you're using Devise, you can authenticate via `#valid_password?` after finding the user. Otherwise, make sure you are securely doing this validation and avoiding [timing attacks](https://en.wikipedia.org/wiki/Timing_attack).

Next, generate the cookies and pass them to the response. With Devise you first need to remember the user. This ensures that the `session` cookie is set, which we will pass to the web view.

Finally, pass the generated access/auth token. This example is just that, **an example**. In production you should ensure this token is not stored in plain text and can be revoked when needed. JWTs or Rails 7's [Active Record Encryption](https://edgeguides.rubyonrails.org/active_record_encryption.html) can help.

```
class User: ApplicationRecord
  before_create do
    self.access_token = SecureRandom.hex(10)
  end
end

class API::AuthController < API::ApplicationController
  def create
    user = User.find_by(email: params[:email])
    if user&.valid_password?(params[:password])
      user.remember_me = true
      sign_in(user)
      render json: { token: user.access_token }
    else
      render :unauthorized
    end
  end
end

class API::ApplicationController < ApplicationController
  skip_before_action :verify_authenticity_token
end

```

##### Persist the access token and cookies

Back to the client again. We now need to securely persist the access token and pass the cookies to the web view.

From [the docs](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/storing_keys_in_the_keychain), the "keychain is the best place to store small secrets, like passwords and cryptographic keys." The API is kind of rough, so I always reach for the [KeychainAccess](https://github.com/kishikawakatsumi/KeychainAccess) package when I need to persist secure information.

The cookies are available in the request in the `Set-Cookie` header. We can transform those into instances of `HTTPCookie` via [`cookies(withResponseHeaderFields:for:)`](https://developer.apple.com/documentation/foundation/httpcookie/1393011-cookies) and copy them to our web view's shared storage.

Here's a rough outline of how you could implement all of that in response to your POST request from earlier. Error handling was omitted to keep the example manageable. Also, note that setting the cookies is asynchronous.

```
private struct AccessToken: Decodable {
    let token: String
}

guard
    error == nil,
    let response = response as? HTTPURLResponse,
    // Ensure the response was successful
    (200 ..< 300).contains(response.statusCode),
    let headers = response.allHeaderFields as? [String: String],
    let data = data,
    let token = try? JSONDecoder().decode(AccessToken.self, from: data)
else { return /* TODO: Handle errors */ }

// Persist the access token in the secure keychain
let keychain = Keychain(service: "Turbo-Credentials")
keychain["access-token"] = token.token

// Copy the "Set-Cookie" headers to the shared web view storage
let cookies = HTTPCookie.cookies(withResponseHeaderFields: headers, for: url)
HTTPCookieStorage.shared.setCookies(cookies, for: url, mainDocumentURL: nil)
let cookieStore = WKWebsiteDataStore.default().httpCookieStore
cookies.forEach { cookie in
    cookieStore.setCookie(cookie, completionHandler: nil)
}

```

We now have our access token saved in the keychain (for native requests) and our web view has all session cookies it needs. All that's left is to reload our sessions and we are good to go!

```
let session = Session()
session.reload

```

3\. Authenticated requests
--------------------------

Let's revisit that GET request to `/me` in the diagram.

Now that we have an access token we can pass it to the server to authenticate the user. To keep with standard practices, we can use [Bearer Authentication](https://swagger.io/docs/specification/authentication/bearer-authentication/) to pass along our credentials. Bearer Authentication, also called Token Authentication, is implemented by setting a specific HTTP header, `Authorization`.

```
let keychain = Keychain(service: "Turbo-Credentials")
if let token = keychain["access-token"] {
    var request = URLRequest(url: url)
    request.setValue("Bearer: \(token)", forHTTPHeaderField: "Authorization")
    // ...
}

```

Back on the server, we can add a helper method to our API controller to find the user via the access token. Calling this in a `before_action` will authenticate the user via their access token. The "magic" here is using `#sign_in` from Devise. This sets `current_user` automatically!

Also, note that we are passing false to the `store` key. This tells Devise not to create a session for the request and ignore cookies.

```
class API::ApplicationController < ApplicationController
  skip_before_action :verify_authenticity_token

  protected

  def authenticate_api_user!
    if (user = api_user)
      sign_in(user, store: false)
    else
      head :unauthorized
    end
  end

  private

  def api_user
    token = request.headers.fetch("Authorization", "").split(" ").last
    User.find_by(access_token: token) if token.present?
  end
end

```

Wrapping up
-----------

This is only an example of one implementation of native authentication with Turbo. Ideas for improvement are a better designed sign-in screen, using JWT or OAuth for access tokens, and leveraging a Swift networking library to cut down on the boilerplate.

> I maintain [HTTP Client](https://github.com/joemasilotti/HTTP-Client), a small Swift library that drastically reduces the boilerplate needed to make network requests. It automatically sets HTTP headers and parses responses directly to your Codable objects.

You've now broken your hybrid app out of the web only world and opened up iOS SDKs and fully native screens. You could route `/my/items/map` to a native `MapView` instead of dealing with Google Maps in the browser. Or route `messages/new` to use a completely custom text editor instead of something web-based.
## 6 Tips And Tricks

Tips and tricks
===============



May 13, 2021

At this point in the [Hybrid iOS series](https://masilotti.com/turbo-ios/), you should have a working Turbo Native app. To wrap up the series I'm sharing tips and tricks I've picked up over the years that range from making development easier to making the app feel more native.

If you're still new to Turbo iOS, check out the beginning of the series, [The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/) . I walk you through building a Turbo Native app from scratch, including all the Ruby on Rails code needed for your server.

##### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  *Hybrid iOS apps with Turbo -- Part 6: Tips and tricks*

Developer quality of life improvements
--------------------------------------

To start, here are a few techniques I add to almost every Turbo Native app I work on. They make my life easier when I'm adding new code and help deal with how dynamic a Rails app can be.

##### Dismiss a modal after submitting a form

If you followed along with the [URL routing part of this series](https://masilotti.com/turbo-ios/url-routing/), your app is set up to present `/new` and `/edit` paths in a modal. Tapping a link, or submitting a form, can sometimes cause weird behavior with this set up.

A quick workaround is to always dismiss a presented controller before doing any navigation. You can safely call dismiss even if there isn't anything currently being presented.

```
private func visit(url: URL, action: VisitAction = .advance) {
    navigationController.dismiss(animated: true)

    // The rest of your implementation...
}

```

##### Fix for "double" pushed controllers

Some apps might experience the same screen being pushed twice on the navigation stack. Another quick fix is to replace, not push, if the proposed URL is the same as the one currently being displayed.

```
func visit(url: URL, action: VisitAction = .advance) {
    let viewController = VisitableViewController(url: url)

    if session.activeVisitable?.visitableURL == url {
        replaceLastController(with: viewController)
    } else if action == .advance {
        navigationController.pushViewController(viewController, animated: true)
    } else {
        replaceLastController(with: viewController)
    }

    session.visit(viewController)
}

func replaceLastController(with controller: UIViewController) {
    let viewControllers = navigationController.viewControllers.dropLast()
    navigationController.setViewControllers(viewControllers + [controller], animated: false)
}

```

##### Endpoints - development vs. TestFlight vs. production

There are usually 3 environments you need to worry about when building iOS apps: local development, TestFlight, and apps downloaded via the App Store (production).

Here's how I configure my apps to point to different servers, depending on how the app was installed on the device.

First, create an `Environment` enum with a case for each environment. Expose a static property that determines which environment we are currently running in.

```
enum Environment: String {
    case development, staging, production
}

extension Environment {
    static var current: Environment {
        if isTestFlight {
            return .staging
        } else if isDevelopment {
            return .development
        }
        return .production
    }

    private static var isTestFlight: Bool {
        guard let receiptURL = Bundle.main.appStoreReceiptURL else { return false }
        return receiptURL.path.contains("sandboxReceipt")
    }

    private static var isDevelopment: Bool {
        ProcessInfo.processInfo.environment["ENVIRONMENT"]?.lowercased() == "development"
    }
}

```

TestFlight builds are determined by a special receipt URL. This is used to test in-app purchases so they don't conflict with "real" ones from the App Store.

Development builds are determined by an environment variable. You can set this on the scheme by adding `"ENVIRONMENT"` and setting the value to `"development"`.

![Setting an environment variable for the scheme](https://masilotti.com/assets/images/turbo-ios/tips-and-tricks/environment-variable.png)

Setting an environment variable for the scheme

Then create another object, `Endpoint`, that returns the URL based on the current environment. Customize each option to match your needs, like development port or staging/production URLs.

```
enum Endpoint {
    static var root: URL {
        switch Environment.current {
        case .development:
            return URL(string: "http://localhost:3000")!
        case .staging:
            return URL(string: "https://staging.example.com")!
        case .production:
            return URL(string: "https://.example.com")!
        }
    }
}

```

Now you can reference the base URL with `Endpoint.root` and the environment is automatically taken into consideration. Use this when loading your initial page on the Turbo `Session`.

```
visit(url: Endpoint.root.appendingPathComponent("/home"))

```

Make your hybrid app feel more native
-------------------------------------

For the biggest impact, convert screens one-by-one to native when needed, like your [sign in screen](https://masilotti.com/turbo-ios/native-authentication/). Map views are also great candidates because the native experience is so much better than the web. However, these are big investments -- they usually require a lot of native code and new API endpoints.

Before reaching for native, try these low hanging fruits. They are only a few lines of code each but can go a long way in making your Turbo iOS app feel more native.

##### Show/hide web content on the app

If using the [Turbo Rails gem](https://github.com/hotwired/turbo-rails), you get [this helper](https://github.com/hotwired/turbo-rails/blob/fec33d9bc767aec612b283620d2a74e78c1f90ae/app/controllers/turbo/native/navigation.rb#L46) for free. Make sure your user agent includes "Turbo Native" and you can use this throughout your application.

```
let session = Session()
session.webView.customUserAgent = "My Great App (Turbo Native)"

```

You can use this helper to hide content that should only appear on the web, like the "Back" button generated from a scaffold. Or, create a new layout file and use that for native apps.

```
<% unless turbo_native_app? %>
  <%= link_to "Back", board_games_path %>
<% end %>

```

##### Disable link previews and Force Touch

Tap and hold a link in your app. See how the little preview dialog appears? That doesn't feel very native, does it!

![Link previews don't feel very native.](https://masilotti.com/assets/images/turbo-ios/tips-and-tricks/link-preview.png)

Link previews don't feel very native.

We can disable these with one line of code. Disable link previews on the web view when you create your Turbo `Session`.

```
let session = Session()
session.webView.allowsLinkPreview = false

```

##### Disable zoom

In a similar vein, you can disable web zoom when someone pinches the screen. Add the following to your layout template in the `<head>`.

`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, user-scalable=0">`

Note that this is an accessibility issue. If someone was zooming in to increase font size, they'd no longer have this option. You might need to add custom font scaling to account for the accessibility gap.