Tips and tricks
===============



May 13, 2021

At this point in the [Hybrid iOS series](https://masilotti.com/turbo-ios/), you should have a working Turbo Native app. To wrap up the series I'm sharing tips and tricks I've picked up over the years that range from making development easier to making the app feel more native.

If you're still new to Turbo iOS, check out the beginning of the series, [The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/) . I walk you through building a Turbo Native app from scratch, including all the Ruby on Rails code needed for your server.

### This is part of a 6-part series on Hybrid iOS apps with Turbo Native.

1.  [Hybrid iOS apps with Turbo -- Part 1: The Turbo framework](https://masilotti.com/turbo-ios/hybrid-apps-with-turbo/)
2.  [Hybrid iOS apps with Turbo -- Part 2: URL routing](https://masilotti.com/turbo-ios/url-routing/)
3.  [Hybrid iOS apps with Turbo -- Part 3: Forms and basic authentication](https://masilotti.com/turbo-ios/forms-and-basic-authentication/)
4.  [Hybrid iOS apps with Turbo -- Part 4: The JavaScript bridge](https://masilotti.com/turbo-ios/the-javascript-bridge/)
5.  [Hybrid iOS apps with Turbo -- Part 5: Native authentication](https://masilotti.com/turbo-ios/native-authentication/)
6.  *Hybrid iOS apps with Turbo -- Part 6: Tips and tricks*

Developer quality of life improvements
--------------------------------------

To start, here are a few techniques I add to almost every Turbo Native app I work on. They make my life easier when I'm adding new code and help deal with how dynamic a Rails app can be.

### Dismiss a modal after submitting a form

If you followed along with the [URL routing part of this series](https://masilotti.com/turbo-ios/url-routing/), your app is set up to present `/new` and `/edit` paths in a modal. Tapping a link, or submitting a form, can sometimes cause weird behavior with this set up.

A quick workaround is to always dismiss a presented controller before doing any navigation. You can safely call dismiss even if there isn't anything currently being presented.

```
private func visit(url: URL, action: VisitAction = .advance) {
    navigationController.dismiss(animated: true)

    // The rest of your implementation...
}

```

### Fix for "double" pushed controllers

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

### Endpoints - development vs. TestFlight vs. production

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

### Show/hide web content on the app

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

### Disable link previews and Force Touch

Tap and hold a link in your app. See how the little preview dialog appears? That doesn't feel very native, does it!

![Link previews don't feel very native.](https://masilotti.com/assets/images/turbo-ios/tips-and-tricks/link-preview.png)

Link previews don't feel very native.

We can disable these with one line of code. Disable link previews on the web view when you create your Turbo `Session`.

```
let session = Session()
session.webView.allowsLinkPreview = false

```

### Disable zoom

In a similar vein, you can disable web zoom when someone pinches the screen. Add the following to your layout template in the `<head>`.

`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, user-scalable=0">`

Note that this is an accessibility issue. If someone was zooming in to increase font size, they'd no longer have this option. You might need to add custom font scaling to account for the accessibility gap.