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
