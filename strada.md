<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [0 Intro](#0-intro)
- [Strada: Create fully native controls, driven by your web app.](#strada-create-fully-native-controls-driven-by-your-web-app)
- [01 Introduction](#01-introduction)
  - [Introduction](#introduction)
- [02 How It Works](#02-how-it-works)
  - [How it Works](#how-it-works)
    - [Demo Examples](#demo-examples)
    - [Building a Web Component](#building-a-web-component)
    - [Building a Native iOS Component](#building-a-native-ios-component)
    - [Building a Native Android Component](#building-a-native-android-component)
    - [Add CSS to Hide Bridged Elements](#add-css-to-hide-bridged-elements)
- [03 Web](#03-web)
  - [Strada Web](#strada-web)
- [04 Ios](#04-ios)
  - [Strada iOS](#strada-ios)
- [05 Android](#05-android)
  - [Strada Android](#strada-android)
- [06 Installing](#06-installing)
  - [Installing Strada in Your Application](#installing-strada-in-your-application)
    - [Prerequisite: Install Stimulus](#prerequisite-install-stimulus)
    - [In Compiled Form](#in-compiled-form)
    - [As An npm Package](#as-an-npm-package)
  - [Installing Strada in Your Native Apps](#installing-strada-in-your-native-apps)
- [Reference](#reference)
  - [0 Components](#0-components)
    - [Bridge Components](#bridge-components)
  - [1 Elements](#1-elements)
    - [Bridge Elements](#bridge-elements)
  - [2 Attributes](#2-attributes)
    - [Attributes](#attributes)
- [Strada Ios](#strada-ios)
  - [0 README](#0-readme)
    - [Strada iOS](#strada-ios-1)
  - [1 INSTALLATION](#1-installation)
    - [Installation](#installation)
  - [2 OVERVIEW](#2-overview)
    - [Overview](#overview)
  - [3 QUICK START](#3-quick-start)
    - [Quick Start Guide](#quick-start-guide)
  - [4 BUILD COMPONENTS](#4-build-components)
    - [Build Bridge Components](#build-bridge-components)
  - [5 ADVANCED OPTIONS](#5-advanced-options)
    - [Advanced Options](#advanced-options)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 0 Intro

Strada: Create fully native controls, driven by your web app.
=============================================================

Current version: [1.0.0-beta1](https://github.com/hotwired/strada-web/releases/tag/v1.0.0-beta1) --- released Sep 19, 2023

**Strada** enables you to create fully native controls in your hybrid mobile apps, driven by the web. Build web components and native components that work together in *WebView* screens to elevate your [Turbo Native](https://turbo.hotwired.dev/handbook/native) apps to the next level.

-   [Strada Web](https://strada.hotwired.dev/handbook/web) enables you to use your existing HTML to create web components that send and respond to messages with components in your native apps.
-   [Strada iOS](https://strada.hotwired.dev/handbook/ios) and [Strada Android](https://strada.hotwired.dev/handbook/android) enable you to create native components that receive and reply to messages from web components that are present on the page. All without writing any JavaScript in your native apps.

Strada components leverage [Stimulus](https://stimulus.hotwired.dev) and work seamlessly with [Turbo](https://turbo.hotwired.dev) web and [Turbo Native](https://turbo.hotwired.dev/handbook/native) apps.

[Handbook](https://strada.hotwired.dev/handbook/introduction)[Installation](https://strada.hotwired.dev/handbook/installing)[Source](https://github.com/hotwired/strada-web)

[Subscribe to project updates over email](https://world.hey.com/hotwired).

Brought to you by the makers of:

-   [![Basecamp](https://strada.hotwired.dev/assets/logo-basecamp.svg)](https://basecamp.com)
-   and
-   [![HEY](https://strada.hotwired.dev/assets/logo-hey.svg)](https://hey.com)

© 2024 [37signals](https://37signals.com)
# 01 Introduction

## Introduction

You can build [Turbo Native](https://turbo.hotwired.dev/handbook/native) apps to enjoy the best of the web alongside the best of native apps and fully native screens. But, there's a major limitation: there's no way for the native app to know what's happening within the `WebView` and adapt to the content that it's displaying.

Additionally, it'd be great for some web features to break out of the `WebView` container and drive native features — whether it's displaying native buttons in the top app bar, displaying native menu sheets, or calling native platform APIs. <strong>Strada</strong> enables you to do all of this and gives you the flexibility to build components that are specific to your app's needs.

Strada acts a "bridge" between your web code and your native app code, letting your web app and native app communicate through a component-based framework. It abstracts away the complexity of communicating with JavaScript code in a `WebView` and native code in your app.

# 02 How It Works

## How it Works

Strada uses a component-based approach to create a bidirectional communication channel between [web components](#web-components) in the `WebView` and [native components](#native-components) in the native app. Strada acts as a "bridge" between your web code and native app code and abstracting away the inherent complexity.

Web components "send" messages to their corresponding native components. Native components "receive" the messages to build and display native controls, populating them with `data` supplied in the messages. When native components want to inform their corresponding web components of a user action or state change, the native components "reply" to the originally received messages. Web components "receive" the replies and invoke a callback to update the web component based on the reply message `data`.

Strada leverages [Stimulus](https://stimulus.hotwired.dev) to bring the same power to your web components. In fact, the core `BridgeComponent` class is an extension of a Stimulus `Controller`, so you should be familiar with Stimulus before building Strada components.

### Demo Examples

If you'd like to see Strada in action with examples, you can run the [Turbo iOS demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo) or the [Turbo Android demo app](https://github.com/hotwired/turbo-android/tree/main/demo). They work together with the [Turbo Native demo web app](https://github.com/hotwired/turbo-native-demo), where you can see the source code for the demo web components.

The full source code for the `"form"` component example below can be found in the demo apps.

### Building a Web Component

Let's say you have a simple `<form>` in your web app with a submit button:

```html
<form method="post">

  <!-- form elements -->

  <button
    class="button"
    type="submit">
    Submit Form
  </button>

</form>
```

Displaying <b>submit</b> buttons in the top-right of the native app bar is a typical convention in mobile apps. It has the benefit of never being hidden underneath the virtual keyboard, and is always visible no matter where you're scrolled on the page. Instead of displaying the submit button in the `WebView`, we can display a native button through a set of `"form"` web and native components.

Let's update the form with bridge attributes and create a new web component, leveraging Strada and Stimulus conventions:
```html
<form
  method="post"
  data-controller="bridge--form">

  <!-- form elements -->

  <button
    class="button"
    type="submit"
    data-bridge--form-target="submit"
    data-bridge-title="Submit">
    Submit Form
  </button>

</form>
```

Now, we'll create a new `"form"` component. This is similar to the way you create Stimulus controllers, but extending the `BridgeComponent` class:
```javascript
// bridge/form_controller.js

import { BridgeComponent } from "@hotwired/strada"

export default class extends BridgeComponent {
  static component = "form"
  static targets = [ "submit" ]

  // ...
}
```

With the basic `"form"` component created, we can now send a `message` to a corresponding native `"form"` component. We'll send the submit button's title as JSON `data` in the message, so the native component can set the native button's title with the `submitTitle`.
```javascript
// bridge/form_controller.js

import { BridgeComponent, BridgeElement } from "@hotwired/strada"

export default class extends BridgeComponent {
  static component = "form"
  static targets = [ "submit" ]

  submitTargetConnected(target) {
    const submitButton = new BridgeElement(target)
    const submitTitle = submitButton.title

    this.send("connect", { submitTitle }, () => {
      target.click()
    })
  }
}
```

Notice the third parameter when calling `send()`. It's a callback function that will be called when the native component replies to the `"connect"` message. The submit button in the `<form>` is clicked, submitting the form to the server, just as if the user had tapped the button directly.

The web component is now ready and we can build a corresponding `"form"` component in the iOS and Android apps.

### Building a Native iOS Component

Let's create a native `"form"` component in a [Turbo iOS](https://github.com/hotwired/turbo-ios) app. First we'll subclass the `BridgeComponent` class:

```swift
final class FormComponent: BridgeComponent {
    override class var name: String { "form" }

    // ...
}
```

Now we can implement the code to handle receiving and replying to messages:

```swift
final class FormComponent: BridgeComponent {
    override class var name: String { "form" }

    // Handle incoming messages based on the message `event`.
    override func onReceive(message: Message) {
        switch message.event {
        case "connect":
            handleConnectEvent(message: message)
        }
    }

    private func handleConnectEvent(message: Message) {
        guard let data: MessageData = message.data() else { return }
        configureBarButton(with: data.submitTitle)
    }

    private func configureBarButton(with title: String) {
        let item = UIBarButtonItem(title: title,
                                   style: .plain,
                                   target: self,
                                   action: #selector(performAction))

        // Display the button in the app bar
    }

    // Reply to the originally received "connect" event message (without any new data).
    @objc func performAction() {
        reply(to: "connect")
    }
}

private extension FormComponent {
    struct MessageData: Decodable {
        let submitTitle: String
    }
}
```

The component receives the `message` for the `"connect"` `event`, displays the native button with the `submitTitle`, and replies to the web component when the native button is tapped.

_Note: There's additional work to set up [Strada iOS](https://github.com/hotwired/strada-ios) in your app for the first time. See the [Quick Start](https://github.com/hotwired/strada-ios/blob/main/docs/QUICK-START.md) guide for complete instructions._

### Building a Native Android Component

Let's create a native `"form"` component in a [Turbo Android](https://github.com/hotwired/turbo-android) app. First we'll subclass the `BridgeComponent` class:

```kotlin
class FormComponent(
    name: String,
    private val delegate: BridgeDelegate<NavDestination>
) : BridgeComponent<NavDestination>(name, delegate) {
    // ...
}
```

Now we can implement the code to handle receiving and replying to messages:

```kotlin
class FormComponent(
    name: String,
    private val delegate: BridgeDelegate<NavDestination>
) : BridgeComponent<NavDestination>(name, delegate) {

    // Handle incoming messages based on the message `event`.
    override fun onReceive(message: Message) {
        when (message.event) {
            "connect" -> handleConnectEvent(message)
        }
    }

    private fun handleConnectEvent(message: Message) {
        val data = message.data<MessageData>() ?: return
        showToolbarButton(data)
    }

    private fun showToolbarButton(data: MessageData) {
        // Display the button in the toolbar

        binding.formSubmit.apply {
            text = data.title
            setOnClickListener {
                performSubmit()
            }
        }
    }

    // Reply to the originally received "connect" event message (without any new data).
    private fun performSubmit(): Boolean {
        return replyTo("connect")
    }

    @Serializable
    data class MessageData(
        @SerialName("submitTitle") val title: String
    )
}
```

The component receives the `message` for the `"connect"` `event`, displays the native button with the `submitTitle`, and replies to the web component when the native button is tapped.

_Note: There's additional work to set up [Strada Android](https://github.com/hotwired/strada-android) in your app for the first time. See the [Quick Start](https://github.com/hotwired/strada-android/blob/main/docs/QUICK-START.md) guide for complete instructions._

### Add CSS to Hide Bridged Elements

We've now set up `"form"` components in the web and native apps. Whenever a native app supports the `"form"` component, it'll receive a message from the web component and display its native button.

There's one final piece to finish. We want to hide the web submit button in the `<form>` when a native button is being displayed. It's easy to write scoped css that is only applied if:
- A particular version of the native app supports the `"form"` component
- A particular `<form>` in your app is connected to a `"form"` component

```css
[data-bridge-components~="form"]
[data-controller~="bridge--form"]
[type="submit"] {
  display: none;
}
```

And now you've got an improved form screen in your app!

# 03 Web

## Strada Web

Strada is a JavaScript library that makes it easy to create web components in your application using your existing HTML. See [how it works](/handbook/how-it-works) and the [installation instructions](/handbook/installing).

<div class="landing-actions">
  <a class="landing-actions__item" href="https://github.com/hotwired/strada-web">
    <div class="landing-actions__icon landing-actions__icon--github" aria-hidden="true"></div>
    hotwired/strada-web
  </a>
</div>

<br/>

If you'd like to see Strada in action with examples, you can run the [Turbo iOS demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo) or the [Turbo Android demo app](https://github.com/hotwired/turbo-android/tree/main/demo). They work together with the [Turbo Native demo web app](https://github.com/hotwired/turbo-native-demo), where you can see the source code for the demo web components.

# 04 Ios

## Strada iOS

Strada iOS is a fully native library that makes it easy to create native components in your hybrid iOS app. There's thorough documentation in the [hotwired/strada-ios](https://github.com/hotwired/strada-ios) repository to help you get started and build your first native component.

<div class="landing-actions">
  <a class="landing-actions__item" href="https://github.com/hotwired/strada-ios">
    <div class="landing-actions__icon landing-actions__icon--github" aria-hidden="true"></div>
    Source & Documentation
  </a>
</div>

<br/>

If you'd like to see Strada iOS in action with examples, you can run the [Turbo iOS demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo).


# 05 Android

## Strada Android

Strada Android is a fully native library that makes it easy to create native components in your hybrid Android app. There's thorough documentation in the [hotwired/strada-android](https://github.com/hotwired/strada-android) repository to help you get started and build your first native component.

<div class="landing-actions">
  <a class="landing-actions__item" href="https://github.com/hotwired/strada-android">
    <div class="landing-actions__icon landing-actions__icon--github" aria-hidden="true"></div>
    Source & Documentation
  </a>
</div>

<br/>

If you'd like to see Strada Android in action with examples, you can run the [Turbo Android demo app](https://github.com/hotwired/turbo-android/tree/main/demo).

# 06 Installing

## Installing Strada in Your Application

Strada can either be referenced in compiled form via the Strada distributable script directly in the `<head>` of your application, or through npm via a bundler like esbuild.

### Prerequisite: Install Stimulus

Strada leverages [Stimulus](https://stimulus.hotwired.dev) and the core `BridgeComponent` class is an extension of a Stimulus `Controller`. You must have Stimulus installed in your web app before installing Strada. See the [Stimulus installation instructions](https://stimulus.hotwired.dev/handbook/installing).

### In Compiled Form

If you're using [importmap-rails](https://github.com/rails/importmap-rails) you just need to pin Stimulus and Strada in your config/importmap.rb file:

```sh
./bin/importmap pin @hotwired/stimulus @hotwired/strada
```

Alternatively, you can manually define importmap entries for both Strada and Stimulus, pointing to the latest versions of each:

```html
<head>
  <script type="importmap">
    {
      "imports": {
        "@hotwired/stimulus": "https://cdn.jsdelivr.net/npm/@hotwired/stimulus@latest/dist/stimulus.min.js",
        "@hotwired/strada": "https://cdn.jsdelivr.net/npm/@hotwired/strada@latest/dist/strada.min.js"
      }
    }
  </script>
</head>
```

Then you can import Strada anywhere in your application code:

```js
    import { BridgeComponent } from "@hotwired/strada"

    class BridgeTest extends BridgeComponent {
      // ...
    }
```

### As An npm Package

You can install Strada from npm via the `npm` or `yarn` packaging tools and use a JavaScript bundler, like webpack or esbuild, to import it in your application.

```javascript
import "@hotwired/strada"
```

## Installing Strada in Your Native Apps

Dedicated installation instructions are provided for the [iOS](https://github.com/hotwired/strada-ios) and [Android](https://github.com/hotwired/strada-android) libraries in their GitHub repos.

<div class="landing-actions">
  <a class="landing-actions__item" href="https://github.com/hotwired/strada-ios">
    <div class="landing-actions__icon landing-actions__icon--github" aria-hidden="true"></div>
    hotwired/strada-ios
  </a>

  <a class="landing-actions__item" href="https://github.com/hotwired/strada-android">
    <div class="landing-actions__icon landing-actions__icon--github" aria-hidden="true"></div>
    hotwired/strada-android
  </a>
</div>

# Reference

## 0 Components

### Bridge Components

#### Web Components

The `BridgeComponent` class is an extension of a Stimulus [Controller](https://stimulus.hotwired.dev/reference/controllers). You have everything available in a standard `Controller` in addition to the following Strada-specific bridge functionality:

* `static component`: The unique name of the component. This must match the name you use for the corresponding native component.
* `this.platformOptingOut`: Specifies whether the controller is opted out for the current platform using the `data-controller-optout-<platform>` attribute.
* `this.enabled`: Specifies whether the component is enabled and supported by the current version of the native app.
* `this.bridgeElement`: Provides `this.element` for the component instance wrapped in a `BridgeElement`.
* `this.send(event, data = {}, callback)`: Sends a message to the native component with the `event` name, optional JSON `data`, and a `callback` to be run when the native component replies to the message.

For example, to create a `"form"` component that displays a native submit button in your native app, you'd add the following controller, target, and title attributes to your web `<form>`:

```html
<form
  method="post"
  data-controller="bridge--form">

  <!-- form elements -->

  <button
    class="button"
    type="submit"
    data-bridge--form-target="submit"
    data-bridge-title="Submit">
    Submit Form
  </button>

</form>
```

Next, create a `BridgeComponent` with named `"form"` that sends a message to the native component with `data` that contains the form's `submitTitle`. Provide a callback to run when the native component replies to the message.

```javascript
// bridge/form_controller.js

import { BridgeComponent, BridgeElement } from "@hotwired/strada"

export default class extends BridgeComponent {
  static component = "form"
  static targets = [ "submit" ]

  submitTargetConnected(target) {
    const submitButton = new BridgeElement(target)
    const submitTitle = submitButton.title

    this.send("connect", { submitTitle }, () => {
      target.click()
    })
  }
}
```

_Note: It's recommended to place your bridge components in a `/bridge` subdirectory where your Stimulus controllers live to make them easily identifiable and isolated from your other Stimulus controllers._

#### Native Components

See the documentation for building the corresponding native components in the [hotwired/strada-ios](https://github.com/hotwired/strada-ios/blob/main/docs/BUILD-COMPONENTS.md) and [hotwired/strada-android](https://github.com/hotwired/strada-android/blob/main/docs/BUILD-COMPONENTS.md) repos.

<br/>

## 1 Elements

### Bridge Elements

The `BridgeElement` class lets you easily use bridge-specific data and behaviors on elements in your components. You can wrap any element in a `new BridgeElement(myElement)` within your bridge components to access the following:

* `title`: Returns the title of the element, attempting to use a `data-bridge-title` value first, the `aria-label` value second, then otherwise falling back to the element's `textContent` or `value`.
* `disabled`: Returns whether the element is disabled with the `data-bridge-disabled` attribute.
* `enabled`: Returns the opposite of `disabled`.
* `enableForComponent(component)`: Removes the `data-bridge-disabled` attribute on the element.
* `hasClass(className)`: Returns whether the element has a particular class in its `classList`.
* `attribute(name)`: Returns the value of an attribute on the element.
* `bridgeAttribute(name)`: Returns the value of a `data-bridge-<name>` attribute on the element.
* `setBridgeAttribute(name, value)`: Sets the value of a `data-bridge-<name>` attribute on the element.
* `removeBridgeAttribute(name)`: Removes the `data-bridge-<name>` attribute on the element.
* `click()`: Performs a click on the element.

## 2 Attributes

### Attributes

#### Data Attributes

The following data attributes can be applied to any element accessed via the `BridgeElement` class:

* `data-bridge-title="My Title"`: Specifies a custom bridge title for your element.
* `data-bridge-disabled`: Specifies whether the bridge element should be enabled or disabled for a particular platform. Values must be `"true"`, `"false"`, `"ios"`, or `"android"`.
* `data-bridge-*`: Specifies arbitrary attributes prefixed with `data-bridge-` whose values are accessible from a `BridgeElement`.

The following data attributes can be applied to elements associated with a `data-controller` and a `BridgeComponent` class:

* `data-controller-optout-ios`: Opt-out the component for your iOS app using [strada-ios](https://github.com/hotwired/strada-ios). Allows you to conditionally disable a component instance for iOS, even if the native app supports the component.
* `data-controller-optout-android`: Opt-out the component for your Android app using [strada-android](https://github.com/hotwired/strada-android). Allows you to conditionally disable a component instance for Android, even if the native app supports the component.

# Strada Ios

## 0 README

### Strada iOS

**[Strada](https://strada.hotwired.dev)** lets you create fully native controls, driven by your web app. It's a set of libraries that work across your [web](https://github.com/hotwired/strada-web), [Android](https://github.com/hotwired/strada-android), and iOS apps to help you build features that make your [Turbo Native](https://turbo.hotwired.dev/handbook/native) hybrid apps stand out. Turn HTML elements that exist in the WebView into native components and communicate messages across your native and web code.

**Strada iOS** enables you to create native components that receive and reply to messages from web components that are present on the page. Native components receive messages to run native code, whether it's to build high fidelity native UI or call platform APIs.

#### Features
- **Level up** your [Turbo Native](https://turbo.hotwired.dev/handbook/native) hybrid apps with high-fidelity native components, driven by web components.
- **Reuse web components** for your [Android](https://github.com/hotwired/strada-android) and iOS apps.
- **Communicate with the WebView** and its web components without writing any JavaScript in your app.

#### Requirements

1. iOS 14 or higher is required for your app.
1. This library is written entirely in [Swift](https://www.swift.org/), and your app should use Swift as well.
1. This library supports [Turbo Native](https://turbo.hotwired.dev/handbook/native) hybrid apps.
1. Your web app must be running [strada-web](https://github.com/hotwired/strada-web). The `window.Strada` object is automatically exposed on the loaded WebView page, which enables `strada-ios` to work.

**Note:** You should understand how Strada works in the browser before attempting to use Strada iOS. See the [Strada documentation](https://strada.hotwired.dev) for details.

#### Getting Started
The best way to get started with Strada iOS is to try out the Turbo iOS demo app first to get familiar with the framework and what it offers. The demo app provides several Strada component examples. To run the demo, clone the [turbo-ios](https://github.com/hotwired/turbo-ios) repo, and read the [instructions](https://github.com/hotwired/turbo-ios/tree/main/Demo#readme).

#### Documentation

1. [Installation](docs/INSTALLATION.md)
1. [Overview](docs/OVERVIEW.md)
1. [Quick Start](docs/QUICK-START.md)
1. [Build Components](docs/BUILD-COMPONENTS.md)
1. [Advanced Options](docs/ADVANCED-OPTIONS.md)

#### Contributing

Strada iOS is open-source software, freely distributable under the terms of an [MIT-style license](LICENSE). The [source code is hosted on GitHub](https://github.com/hotwired/strada-ios). Development is sponsored by [37signals](https://37signals.com/).

We welcome contributions in the form of bug reports, pull requests, or thoughtful discussions in the [GitHub issue tracker](https://github.com/hotwired/strada-ios/issues).

Please note that this project is released with a [Contributor Code of Conduct](docs/CONDUCT.md). By participating in this project you agree to abide by its terms.

---------

© 2023 37signals LLC

## 1 INSTALLATION

### Installation

#### Swift Package Manager
Add `strada-ios` as a dependency in your app directly in Xcode or in your `Package.swift` file:

```
dependencies: [
    .package(url: "https://github.com/hotwired/strada-ios", from: "<latest-version>")
]
```

**Note:** `strada-ios` works seamlessly with [turbo-ios](https://github.com/hotwired/turbo-ios) and the documentation provides instructions for integrating Strada with your [Turbo Native](https://turbo.hotwired.dev/handbook/native) app. Keep in mind that `turbo-ios` is not automatically included as a dependency in `strada-ios`, so you'll want to setup your `turbo-ios` app first.

## 2 OVERVIEW

### Overview
Strada iOS is a native adapter for your [Strada](https://strada.hotwired.dev)-enabled web app. It allows you to build native components driven by web-based components that exist in `WKWebView`. It's built entirely using standard iOS tools and conventions.

This library has been in use and tested in the wild since June 2020 in the [HEY iOS](https://apps.apple.com/lt/app/hey-email/id1506603805) app.

To understand how Strada works at a high level and see examples of web components working together with native components, see the [online handbook](https://strada.hotwired.dev/handbook/introduction).

#### Structure of Your App
Strada iOS will work with any `WKWebView`-based iOS app, but we only provide instructions for integrating with [turbo-ios](https://github.com/hotwired/turbo-ios) apps. As part of the [Hotwire](https://hotwired.dev/) family, `strada-ios` works seamlessly with your Turbo-powered hybrid apps.

We'll walk you through integrating `strada-ios` into your app in the [Quick Start Guide](QUICK-START.md) instructions.

## 3 QUICK START

### Quick Start Guide

This outlines everything you need to initially configure in your [`turbo-ios`](https://github.com/hotwired/turbo-ios) app to integrate `strada-ios`. Everything in this guide only needs to be done once in your app.

_NOTE: You can find the code in this guide fully implemented in the `turbo-ios` [demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo)._

#### Create an array of registered bridge components

For now, create an empty (global) list of registered component factories, so we have a reference. You'll need to populate this list with each bridge component that your app supports.

**`BridgeComponent+App.swift`**
```swift
extension BridgeComponent {
    static var allTypes: [BridgeComponent.Type] {
        [
            // Add registered components here later
        ]
    }
}
```

#### Initialize the WKWebView instance

For Strada to work properly across your web and native app, you'll need to make sure each `Turbo.Session` `WKWebView` instance is initialized with the following:
- An updated user agent string that includes the supported bridge components. Strada provides a utility function that builds the substring for you.
- Initialize the `WKWebView` with the `Bridge` class, so Strada can internally manage the `WKWebView` through the app's lifecycle.

Update the `WKWebView` user agent string where your `WKWebViewConfiguration` is configured. The `turbo-ios` [demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo) creates an extension like this:

**`WKWebViewConfiguration+App.swift`**
```swift
extension WKWebViewConfiguration {
    static var appConfiguration: WKWebViewConfiguration {
        let stradaSubstring = Strada.userAgentSubstring(for: BridgeComponent.allTypes)
        let userAgent = "Turbo Native iOS \(stradaSubstring)"

        let configuration = WKWebViewConfiguration()
        configuration.applicationNameForUserAgent = userAgent

        return configuration
    }
}
```

The `WKWebViewConfiguration` instance with the custom user agent string must be set when creating your `WKWebView` instance:

**`SceneController.swift`**
```swift
let webView = WKWebView(frame: .zero, configuration: .appConfiguration)
```

Initialize the `Bridge` where each `Turbo.Session` and `WKWebView` instance is created in your app:

**`SceneController.swift`**
```swift
Bridge.initialize(webView)
```

#### Implement the `BridgeDestination` protocol
You'll need to add the `BridgeDestination` protocol for you each `VisitableViewController` in your app:

**`TurboWebViewController.swift`**
```swift
final class TurboWebViewController: VisitableViewController, BridgeDestination {
    // ...
}
```

#### Delegate to the `BridgeDelegate` class
You'll need to subclass `VisitableViewController` (if you're not already) and delegate its lifecycle events to the `BridgeDelegate` class:

**`TurboWebViewController.swift`**
```swift
final class TurboWebViewController: VisitableViewController, BridgeDestination {

    private lazy var bridgeDelegate: BridgeDelegate = {
        BridgeDelegate(location: visitableURL.absoluteString,
                       destination: self,
                       componentTypes: BridgeComponent.allTypes)
    }()

    // MARK: View lifecycle

    override func viewDidLoad() {
        super.viewDidLoad()
        bridgeDelegate.onViewDidLoad()
    }

    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        bridgeDelegate.onViewWillAppear()
    }

    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        bridgeDelegate.onViewDidAppear()
    }

    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        bridgeDelegate.onViewWillDisappear()
    }

    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        bridgeDelegate.onViewDidDisappear()
    }

    // MARK: Visitable

    override func visitableDidActivateWebView(_ webView: WKWebView) {
        bridgeDelegate.webViewDidBecomeActive(webView)
    }

    override func visitableDidDeactivateWebView() {
        bridgeDelegate.webViewDidBecomeDeactivated()
    }
}
```

#### Build your first `BridgeComponent`

You're now down with the initial setup. See the [Build Components](BUILD-COMPONENTS.md) page to build your first bridge component.

## 4 BUILD COMPONENTS

### Build Bridge Components

#### Your first component

After you set up your app in the [Quick Start](QUICK-START.md) guide, it's time to build your first native bridge component. Native components receive messages from corresponding web components of the same `name`. So, be sure to understand how [web components](https://strada.hotwired.dev/handbook/web) work in your web app and start there.

Once a component receives a message, it uses that message's `event` and `data` to perform custom native functionality. If the user performs a native action, the native component can reply back to the corresponding web component using the originally received `message` and (optionally) new `data`.

You create your first native component by subclassing the `BridgeComponent` class. The example below is from the `FormComponent` in the `turbo-ios` [demo app](https://github.com/hotwired/turbo-ios/tree/main/Demo).

Override the `name` to provide the component's name. The `name` (`"form"` in this instance) that you give to each component must be unique and match the name of the web component that it corresponds to.

It'll look like this:

**`FormComponent.swift`**
```swift
final class FormComponent: BridgeComponent {
    override class var name: String { "form" }

    // ...
}
```

#### Handle received messages

Every component must implement the `onReceive(message: Message)` function. Each `message` has an `event` associated with it, so you should first look at the `event` to determine how to handle the incoming `message`. Here's how the `FormComponent` handles receiving messages:

**`FormComponent.swift`**
```swift
final class FormComponent: BridgeComponent {
    override class var name: String { "form" }

    override func onReceive(message: Message) {
        guard let event = Event(rawValue: message.event) else {
            return
        }

        switch event {
        case .connect:
            handleConnectEvent(message: message)
        case .submitEnabled:
            handleSubmitEnabled()
        case .submitDisabled:
            handleSubmitDisabled()
        }
    }

    // MARK: Private

    private func handleConnectEvent(message: Message) {
        guard let data: MessageData = message.data() else { return }

        // Write code to display a native submit button in the
        // app bar displayed in the delegate.destination. Use the
        // incoming data.title to set the button title. The
        // implementation depends on how your app is structured.
    }

    private func handleSubmitEnabled() {
        // Write code to enable the submit button.
    }

    private func handleSubmitDisabled() {
        // Write code to disable the submit button.
    }
}

// MARK: Events

private extension FormComponent {
    enum Event: String {
        case connect
        case submitEnabled
        case submitDisabled
    }
}

// MARK: Message data

private extension FormComponent {
    struct MessageData: Decodable {
        let submitTitle: String
    }
}
```

For each `BridgeComponent` subclass that you register in your app, zero or one component instances will exist for each destination screen. A component instance will be created when its first message is received from a corresponding web component of the same `name`. If no messages are received for a particular component in the current destination, no component instance will be created.

By default, `strada-ios` uses [JSONEncoder](https://developer.apple.com/documentation/foundation/jsonencoder) and [JSONDecoder](https://developer.apple.com/documentation/foundation/jsondecoder) to encode/decode `Message.data` with your own data models that implement the `Codeable`/`Decodable`/`Encodable` protocols. See the [Advanced Options](ADVANCED-OPTIONS.md) to configure your encoding/decoding strategy.

#### Reply to received messages

If you'd like to inform the corresponding web component that an action has occurred, such as the user tapping on a submit button, you can reply to the originally received message. For the `FormComponent` it looks like this:

**`FormComponent.swift`**
```swift
final class FormComponent: BridgeComponent {

    // ...

    private func configureBarButton(with title: String) {
        guard let viewController else { return }

        let item = UIBarButtonItem(title: title,
                                   style: .plain,
                                   target: self,
                                   action: #selector(performAction))

        // ...
    }

    @objc func performAction() {
        reply(to: Event.connect.rawValue)
    }
}
```

When a web component receives a reply from a sent message, it can run a callback to perform the appropriate action in the web app. In this example, tapping on the native submit button and sending back a reply results in the web `"form"` component clicking the hidden web submit button in its form.

For convenience, there are multiple ways to reply to received messages. If you use `reply(to: eventName)`, the `BridgeComponent` internally replies with the last message received for the given `eventName`. The available reply options are:

```swift
reply(to: "eventName")
reply(to: "eventName", newData)
reply(with: originalMessage)
reply(with: originalMessage.replacing(data: newData))
reply(with: originalMessage.replacing(event: "newEventName"))
```

#### Register your component

For every component that you want to use in your app, you must register it in the list you created in the [Quick Start](QUICK-START.md) guide. This allows the web app and backend (through the `WKWebView` user-agent) know what components are natively registered for the current version of the app. To register the new `FormComponent`, it looks like this:

**`BridgeComponent+App.swift`**
```swift
extension BridgeComponent {
    static var allTypes: [BridgeComponent.Type] {
        [
            FormComponent.self
        ]
    }
}
```

#### Using your component

Your component is now ready. Whenever a web `form` component exists on a page in your web app, it'll automatically send messages to your app, a `FormComponent` instance will be created for you, and your component's native code will be invoked.

## 5 ADVANCED OPTIONS

### Advanced Options

#### Enable Debug Logging
During development, you may want to see what `strada-ios` is doing behind the scenes. To enable debug logging, call `Strada.config.debugLoggingEnabled = true`. Debug logging should always be disabled in your production app. For example:

```swift
###if DEBUG
    Strada.config.debugLoggingEnabled = true
###endif
```

#### Using a custom JSON encoder or decoder
By default, `strada-ios` uses [JSONEncoder](https://developer.apple.com/documentation/foundation/jsonencoder) and [JSONDecoder](https://developer.apple.com/documentation/foundation/jsondecoder) to encode/decode `Message.data` with your own data models that implement the `Codeable`/`Decodable`/`Encodable` protocols.

If you'd like to customize the encoding/decoding strategy, you can configure this in your app:

```swift
let encoder = JSONEncoder()
encoder.keyEncodingStrategy = .convertToSnakeCase

// Configure your encoder as Strada's automatic encoder
Strada.config.jsonEncoder = encoder
```

```swift
let decoder = JSONDecoder()
decoder.keyDecodingStrategy = .convertFromSnakeCase

// Configure your decoder as Strada's automatic decoder
Strada.config.jsonDecoder = decoder
```
