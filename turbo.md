<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [01 Turbo Intro](#01-turbo-intro)
  - [Turbo: The speed of a single-page web application without having to write any JavaScript.](#turbo-the-speed-of-a-single-page-web-application-without-having-to-write-any-javascript)
- [02 Turbo Rails](#02-turbo-rails)
  - [Turbo for Ruby on Rails](#turbo-for-ruby-on-rails)
    - [Navigate with Turbo Drive](#navigate-with-turbo-drive)
    - [Decompose with Turbo Frames](#decompose-with-turbo-frames)
    - [Come Alive with Turbo Streams](#come-alive-with-turbo-streams)
    - [Installation](#installation)
    - [Usage](#usage)
    - [Compatibility with Rails UJS](#compatibility-with-rails-ujs)
    - [Testing](#testing)
    - [Development](#development)
    - [License](#license)
- [03 Turbo Upgrading](#03-turbo-upgrading)
  - [Upgrading from previous Turbo Rails versions](#upgrading-from-previous-turbo-rails-versions)
    - [Key digest changes in 1.1.1](#key-digest-changes-in-111)
  - [Upgrading from Rails UJS / Turbolinks to Turbo](#upgrading-from-rails-ujs--turbolinks-to-turbo)
    - [1. Ensure Rails UJS is using compatible selectors](#1-ensure-rails-ujs-is-using-compatible-selectors)
    - [2. Replace the turbolinks gem in Gemfile with turbo-rails](#2-replace-the-turbolinks-gem-in-gemfile-with-turbo-rails)
    - [3. Replace the inclusion of turbolinks in your pack file with turbo](#3-replace-the-inclusion-of-turbolinks-in-your-pack-file-with-turbo)
    - [4. Replace all turbolinks namespaces with turbo](#4-replace-all-turbolinks-namespaces-with-turbo)
    - [5. Optional: Provide backwards compatible shims for mobile adapters](#5-optional-provide-backwards-compatible-shims-for-mobile-adapters)
- [04 Turbo Handbook](#04-turbo-handbook)
  - [01 Introduction](#01-introduction)
    - [Introduction](#introduction)
  - [02 Drive](#02-drive)
    - [Navigate with Turbo Drive](#navigate-with-turbo-drive-1)
  - [03 Page Refreshes](#03-page-refreshes)
    - [Smooth page refreshes with morphing](#smooth-page-refreshes-with-morphing)
  - [04 Frames](#04-frames)
    - [Decompose with Turbo Frames](#decompose-with-turbo-frames-1)
  - [05 Streams](#05-streams)
    - [Come Alive with Turbo Streams](#come-alive-with-turbo-streams-1)
  - [06 Native](#06-native)
    - [Go Native on iOS & Android](#go-native-on-ios--android)
  - [07 Building](#07-building)
    - [Building Your Turbo Application](#building-your-turbo-application)
  - [08 Installing](#08-installing)
    - [Installing Turbo in Your Application](#installing-turbo-in-your-application)
- [05 Turbo Reference](#05-turbo-reference)
  - [01 Drive](#01-drive)
    - [Drive](#drive)
  - [02 Frames](#02-frames)
    - [Frames](#frames)
    - [Attributes, properties, and functions](#attributes-properties-and-functions)
  - [03 Streams](#03-streams)
    - [Streams](#streams)
  - [04 Events](#04-events)
    - [Events](#events)
  - [05 Attributes](#05-attributes)
    - [Attributes and Meta Tags](#attributes-and-meta-tags)
- [06 Turbo Docs](#06-turbo-docs)
  - [01 Turbo Drive Helper](#01-turbo-drive-helper)
- [Module: Turbo::DriveHelper](#module-turbodrivehelper)
  - [Overview](#overview)
  - [Instance Method Details](#instance-method-details)
  - [02 Turbo Frames Helper](#02-turbo-frames-helper)
- [Module: Turbo::FramesHelper](#module-turboframeshelper)
  - [Instance Method Details](#instance-method-details-1)
  - [03 Turbo Streams Helper](#03-turbo-streams-helper)
- [Module: Turbo::StreamsHelper](#module-turbostreamshelper)
  - [Instance Method Details](#instance-method-details-2)
  - [04 Turbo Broadcastable](#04-turbo-broadcastable)
- [Module: Turbo::Broadcastable](#module-turbobroadcastable)
  - [Overview](#overview-1)
  - [Suppressing broadcasts](#suppressing-broadcasts)
  - [Defined Under Namespace](#defined-under-namespace)
  - [Instance Method Details](#instance-method-details-3)
  - [05 Turbo Streams Channel](#05-turbo-streams-channel)
- [Class: Turbo::StreamsChannel](#class-turbostreamschannel)
  - [Overview](#overview-2)
  - [Instance Method Details](#instance-method-details-4)
  - [06 Turbo Native Navigation](#06-turbo-native-navigation)
- [Module: Turbo::Native::Navigation](#module-turbonativenavigation)
  - [Overview](#overview-3)
  - [Instance Method Details](#instance-method-details-5)
  - [07 Turbo Test Assertions](#07-turbo-test-assertions)
- [Module: Turbo::TestAssertions](#module-turbotestassertions)
  - [Defined Under Namespace](#defined-under-namespace-1)
  - [Instance Method Details](#instance-method-details-6)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 01 Turbo Intro

## Turbo: The speed of a single-page web application without having to write any JavaScript.

Current version: [8.0.4](https://github.com/hotwired/turbo/releases/tag/v8.0.4) --- released Mar 08, 2024

**Turbo** uses complementary techniques to dramatically reduce the amount of custom JavaScript that most web applications will need to write:

-   *Turbo Drive* accelerates links and form submissions by negating the need for full page reloads.
-   *Turbo Frames* decompose pages into independent contexts, which scope navigation and can be lazily loaded.
-   *Turbo Streams* deliver page changes over WebSocket, SSE or in response to form submissions using just HTML and a set of CRUD-like actions.
-   *Turbo Native* lets your [majestic monolith](https://m.signalvnoise.com/the-majestic-monolith/) form the center of your native iOS and Android apps, with seamless transitions between web and native sections.

It's all done by sending HTML over the wire. And for those instances when that's not enough, you can reach for the other side of [Hotwire](https://hotwired.dev), and finish the job with [Stimulus](https://stimulus.hotwired.dev).
# 02 Turbo Rails

## Turbo for Ruby on Rails

[Turbo](https://turbo.hotwired.dev) gives you the speed of a single-page web application without having to write any JavaScript. Turbo accelerates links and form submissions without requiring you to change your server-side generated HTML. It lets you carve up a page into independent frames, which can be lazy-loaded and operate as independent components. And finally, helps you make partial page updates using just HTML and a set of CRUD-like container tags. These three techniques reduce the amount of custom JavaScript that many web applications need to write by an order of magnitude. And for the few dynamic bits that are left, you're invited to finish the job with [Stimulus](https://github.com/hotwired/stimulus).

On top of accelerating web applications, Turbo was built from the ground-up to form the foundation of hybrid native applications. Write the navigational shell of your [Android](https://github.com/hotwired/turbo-android) or [iOS](https://github.com/hotwired/turbo-ios) app using the standard platform tooling, then seamlessly fill in features from the web, following native navigation patterns. Not every mobile screen needs to be written in Swift or Kotlin to feel native. With Turbo, you spend less time wrangling JSON, waiting on app stores to approve updates, or reimplementing features you've already created in HTML.

Turbo is a language-agnostic framework written in JavaScript, but this gem builds on top of those basics to make the integration with Rails as smooth as possible. You can deliver turbo updates via model callbacks over Action Cable, respond to controller actions with native navigation or standard redirects, and render turbo frames with helpers and layout-free responses.

### Navigate with Turbo Drive

Turbo is a continuation of the ideas from the previous [Turbolinks](https://github.com/turbolinks/turbolinks) framework, and the heart of that past approach lives on as Turbo Drive. When installed, Turbo automatically intercepts all clicks on `<a href>` links to the same domain. When you click an eligible link, Turbo prevents the browser from following it. Instead, Turbo changes the browser’s URL using the History API, requests the new page using `fetch`, and then renders the HTML response.

During rendering, Turbo replaces the current `<body>` element outright and merges the contents of the `<head>` element. The JavaScript window and document objects, and the `<html>` element, persist from one rendering to the next.

Whereas Turbolinks previously just dealt with links, Turbo can now also process form submissions and responses. This means the entire flow in the web application is wrapped into Turbo, making all the parts fast. No more need for `data-remote=true`.

Turbo Drive can be disabled on a per-element basis by annotating the element or any of its ancestors with `data-turbo="false"`. If you want Turbo Drive to be disabled by default, then you can adjust your import like this:

```js
import "@hotwired/turbo-rails"
Turbo.session.drive = false
```

Then you can use `data-turbo="true"` to enable Drive on a per-element basis.

[See documentation](https://turbo.hotwired.dev/handbook/drive).

### Decompose with Turbo Frames

Turbo reinvents the old HTML technique of frames without any of the drawbacks that lead to developers abandoning it. With Turbo Frames, **you can treat a subset of the page as its own component**, where links and form submissions **replace only that part**. This removes an entire class of problems around partial interactivity that before would have required custom JavaScript.

It also makes it dead easy to carve a single page into smaller pieces that can all live on their own cache timeline. While the bulk of the page might easily be cached between users, a small personalized toolbar perhaps cannot. With Turbo::Frames, you can designate the toolbar as a frame, which will be **lazy-loaded automatically** by the publicly-cached root page. This means simpler pages, easier caching schemes with fewer dependent keys, and all without needing to write a lick of custom JavaScript.

This gem provides a `turbo_frame_tag` helper to create those frames.

For instance:
```erb
<%# app/views/todos/show.html.erb %>
<%= turbo_frame_tag @todo do %>
  <p><%= @todo.description %></p>

  <%= link_to 'Edit this todo', edit_todo_path(@todo) %>
<% end %>

<%# app/views/todos/edit.html.erb %>
<%= turbo_frame_tag @todo do %>
  <%= render "form" %>

  <%= link_to 'Cancel', todo_path(@todo) %>
<% end %>
```

When the user clicks on the `Edit this todo` link, as a direct response to this user interaction, the turbo frame will be automatically replaced with the one in the `edit.html.erb` page.

[See documentation](https://turbo.hotwired.dev/handbook/frames).

#### A note on custom layouts

In order to render turbo frame requests without the application layout, Turbo registers a custom [layout method](https://api.rubyonrails.org/classes/ActionView/Layouts/ClassMethods.html#method-i-layout). 
If your application uses custom layout resolution, you have to make sure to return `"turbo_rails/frame"` (or `false` for TurboRails < 1.4.0) for turbo frame requests:

```ruby
layout :custom_layout

def custom_layout
  return "turbo_rails/frame" if turbo_frame_request?
  
  # ... your custom layout logic
```

If you are using a custom, but "static" layout,

```ruby
layout "some_static_layout"
```

you **have** to change it to a layout method in order to conditionally return `false` for turbo frame requests:

```ruby
layout :custom_layout

def custom_layout
  return "turbo_rails/frame" if turbo_frame_request?
  
  "some_static_layout"
```

### Come Alive with Turbo Streams

Partial page updates that are **delivered asynchronously over a web socket connection** is the hallmark of modern, reactive web applications. With Turbo Streams, you can get all of that modern goodness using the existing server-side HTML you're already rendering to deliver the first page load. With a set of simple CRUD container tags, you can send HTML fragments over the web socket (or in response to direct interactions), and see the page change in response to new data. Again, **no need to construct an entirely separate API**, **no need to wrangle JSON**, **no need to reimplement the HTML construction in JavaScript**. Take the HTML you're already making, wrap it in an update tag, and, voila, your page comes alive.

With this Rails integration, you can create these asynchronous updates directly in response to your model changes. Turbo uses Active Jobs to provide asynchronous partial rendering and Action Cable to deliver those updates to subscribers.

This gem provides a `turbo_stream_from` helper to create a turbo stream.

```erb
<%# app/views/todos/show.html.erb %>
<%= turbo_stream_from dom_id(@todo) %>

<%# Rest of show here %>
```

[See documentation](https://turbo.hotwired.dev/handbook/streams).

### Installation

This gem is automatically configured for applications made with Rails 7+ (unless --skip-hotwire is passed to the generator). But if you're on Rails 6, you can install it manually:

1. Add the `turbo-rails` gem to your Gemfile: `gem 'turbo-rails'`
2. Run `./bin/bundle install`
3. Run `./bin/rails turbo:install`
4. Run `./bin/rails turbo:install:redis` to change the development Action Cable adapter from Async (the default one) to Redis. The Async adapter does not support Turbo Stream broadcasting.

Running `turbo:install` will install through NPM if Node.js is used in the application. Otherwise the asset pipeline version is used. To use the asset pipeline version, you must have `importmap-rails` installed first and listed higher in the Gemfile.

If you're using node and need to use the cable consumer, you can import [`cable`](https://github.com/hotwired/turbo-rails/blob/main/app/javascript/turbo/cable.js) (`import { cable } from "@hotwired/turbo-rails"`), but ensure that your application actually *uses* the members it `import`s when using this style (see [turbo-rails#48](https://github.com/hotwired/turbo-rails/issues/48)).

The `Turbo` instance is automatically assigned to `window.Turbo` upon import:

```js
import "@hotwired/turbo-rails"
```

### Usage

You can watch [the video introduction to Hotwire](https://hotwired.dev/#screencast), which focuses extensively on demonstrating Turbo in a Rails demo. Then you should familiarize yourself with [Turbo handbook](https://turbo.hotwired.dev/handbook/introduction) to understand Drive, Frames, and Streams in-depth. Finally, dive into the code documentation by starting with [`Turbo::FramesHelper`](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/frames_helper.rb), [`Turbo::StreamsHelper`](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/streams_helper.rb), [`Turbo::Streams::TagBuilder`](https://github.com/hotwired/turbo-rails/blob/main/app/models/turbo/streams/tag_builder.rb), and [`Turbo::Broadcastable`](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb).

#### RubyDoc Documentation

For the API documentation covering this gem's classes and packages, [visit the RubyDoc page](https://rubydoc.info/github/hotwired/turbo-rails/main).
Note that this documentation is updated automatically from the main branch, so it may contain features that are not released yet.

- [Turbo Drive Helpers](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper)
- [Turbo Frames Helpers](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/FramesHelper)
- [Turbo Streams View Helpers](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/StreamsHelper)
- [Turbo Streams Broadcast Methods](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable)
- [Turbo Streams Channel](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/StreamsChannel)
- [Turbo Native Navigation](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation)
- [Turbo Test Assertions](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/TestAssertions)
- [Turbo Integration Test Assertions](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/TestAssertions/IntegrationTestAssertions)
- [Turbo Broadcastable Test Helper](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable/TestHelper)

### Compatibility with Rails UJS

Turbo can coexist with Rails UJS, but you need to take a series of upgrade steps to make it happen. See [the upgrading guide](https://github.com/hotwired/turbo-rails/blob/main/UPGRADING.md).

### Testing

The [`Turbo::TestAssertions`](./lib/turbo/test_assertions.rb) concern provides Turbo Stream test helpers that assert the presence or absence ofs  s  `<turbo-stream>` elements in a rendered fragment of HTML. `Turbo::TestAssertions` are automatically included in [`ActiveSupport::TestCase`](https://edgeapi.rubyonrails.org/classes/ActiveSupport/TestCase.html) and depend on the presence of [`rails-dom-testing`](https://github.com/rails/rails-dom-testing/) assertions.

The [`Turbo::TestAssertions::IntegrationTestAssertions`](./lib/turbo/test_assertions/integration_test_assertions.rb) are built on top of `Turbo::TestAssertions`, and add support for passing a `status:` keyword. They are automatically included in [`ActionDispatch::IntegrationTest`](https://edgeguides.rubyonrails.org/testing.html#integration-testing).

The [`Turbo::Broadcastable::TestHelper`](./lib/turbo/broadcastable/test_helper.rb) concern provides Action Cable-aware test helpers that assert that `<turbo-stream>` elements were or were not broadcast over Action Cable. `Turbo::Broadcastable::TestHelper` is automatically included in [`ActiveSupport::TestCase`](https://edgeapi.rubyonrails.org/classes/ActiveSupport/TestCase.html).

### Development

Run the tests with `./bin/test`.

### License

Turbo is released under the [MIT License](https://opensource.org/licenses/MIT).

# 03 Turbo Upgrading

## Upgrading from previous Turbo Rails versions

### Key digest changes in 1.1.1

Prior to version 1.1.1, Turbo Rails inadvertently caused applications to use SHA1 when deriving application secrets,
even if another digest class was specified in `config.active_support.key_generator_hash_digest_class`. Starting with
Rails 7, new applications default to SHA256 for key generation, and so are more likely to be affected by this.

This behavior was [fixed][1] in Turbo Rails 1.1.1. As a result, upgrading from an older version can cause an unexpected
change to application secrets.

For applications that use ActiveStorage, this causes a change to the secret used by its message verifier, which will make
assets previously stored by the application [inaccessible][2].

If your application is affected by this, you can use a key rotation to ensure the old asset digests remain readable.
Placing the following code inside `config/initializers` will add the necessary rotation:

```ruby
Rails.application.config.after_initialize do |app|
  key_generator = ActiveSupport::KeyGenerator.new app.secret_key_base,
    iterations: 1000,
    hash_digest_class: OpenSSL::Digest::SHA1

  app.message_verifier("ActiveStorage").rotate(key_generator.generate_key("ActiveStorage"))
end
```

Alternatively, you can configure the application to continue using SHA1-based secrets, by overriding the default:

```ruby
config.active_support.key_generator_hash_digest_class = OpenSSL::Digest::SHA1
```

[1]: https://github.com/hotwired/turbo-rails/pull/335
[2]: https://github.com/hotwired/turbo-rails/issues/340
## Upgrading from Rails UJS / Turbolinks to Turbo

Turbo supersedes the functionality offered by Rails UJS to turn links and form submissions into XMLHttpRequests, so if you're making a complete switch from Rails UJS / Turbolinks to Turbo, you should ensure that you have `config.action_view.form_with_generates_remote_forms = false` set in your `config/application.rb`. But not all applications can upgrade in one jump, and may need to have Rails UJS coexist alongside Turbo. Here are the steps you need to follow:

### 1. Ensure Rails UJS is using compatible selectors
Rails UJS is offered either directly from the Rails framework or by the classic jquery-ujs plugin. Whichever of these you use, you can leave in place, but you need to either upgrade to a compatible version (see https://github.com/rails/rails/pull/42476) or vendor the JavaScript file needed in your app and tweak it yourself.

### 2. Replace the turbolinks gem in Gemfile with turbo-rails
You no longer want `gem 'turbolinks'` in your Gemfile, but instead `gem 'turbo-rails'`. But in order to have Turbo work with the old-style XMLHttpRequests issued by UJS, you'll need to shim the old Turbolinks behavior that made those requests compatible with 302s (by invoking Turbolinks, now Turbo, directly).

First you need to add `app/controllers/concerns/turbo/redirection.rb`, which should be included in `ApplicationController` as `Turbo::Redirection`:

```ruby
module Turbo
  module Redirection
    extend ActiveSupport::Concern

    def redirect_to(url = {}, options = {})
      turbo = options.delete(:turbo)

      super.tap do
        if turbo != false && request.xhr? && !request.get?
          visit_location_with_turbo(location, turbo)
        end
      end
    end

    private
      def visit_location_with_turbo(location, action)
        visit_options = {
          action: action.to_s == "advance" ? action : "replace"
        }

        script = []
        script << "Turbo.cache.clear()"
        script << "Turbo.visit(#{location.to_json}, #{visit_options.to_json})"

        self.status = 200
        self.response_body = script.join("\n")
        response.content_type = "text/javascript"
        response.headers["X-Xhr-Redirect"] = location
      end
  end
end
```

Then you need `test/helpers/turbo_assertions_helper.rb`, which should be included in `ActionDispatch::IntegrationTest`:

```ruby
module TurboAssertionsHelper
  TURBO_VISIT = /Turbo\.visit\("([^"]+)", {"action":"([^"]+)"}\)/

  def assert_redirected_to(options = {}, message = nil)
    if turbo_request?
      assert_turbo_visited(options, message)
    else
      super
    end
  end

  def assert_turbo_visited(options = {}, message = nil)
    assert_response(:ok, message)
    assert_equal("text/javascript", response.try(:media_type) || response.content_type)

    visit_location, _ = turbo_visit_location_and_action

    redirect_is       = normalize_argument_to_redirection(visit_location)
    redirect_expected = normalize_argument_to_redirection(options)

    message ||= "Expected response to be a Turbo visit to <#{redirect_expected}> but was a visit to <#{redirect_is}>"
    assert_operator redirect_expected, :===, redirect_is, message
  end

  # Rough heuristic to detect whether this was a Turbolinks request:
  # non-GET request with a text/javascript response.
  #
  # Technically we'd check that Turbolinks-Referrer request header is
  # also set, but that'd require us to pass the header from post/patch/etc
  # test methods by overriding them to provide a `turbo:` option.
  #
  # We can't check `request.xhr?` here, either, since the X-Requested-With
  # header is cleared after controller action processing to prevent it
  # from leaking into subsequent requests.
  def turbo_request?
    !request.get? && (response.try(:media_type) || response.content_type) == "text/javascript"
  end

  def turbo_visit_location_and_action
    if response.body =~ TURBO_VISIT
      [ $1, $2 ]
    end
  end
end
```

### 3. Replace the inclusion of turbolinks in your pack file with turbo
You probably have something like `require("turbolinks").start()`, which needs to become `import "@hotwired/turbo-rails"`. You don't need to start anything. Turbo is automatically started (and assigned to `window.Turbo`) upon importation.


### 4. Replace all turbolinks namespaces with turbo
If you have anything like `document.addEventListener("turbolinks:before-cache" ...)`, you'll need to replace those event names with the turbo-namespaced version, like `turbo:before-cache`. Same goes for calls to `Turbolinks.visit`, which you'll need to replace them with calls to `Turbo.visit`. And DOM element attributes, like `data-turbolinks-action`, which need to become `data-turbo-action` (remember all those `data: { turbolinks: false }` -> `data: { turbo: false }` too).


### 5. Optional: Provide backwards compatible shims for mobile adapters
If you've built native apps using the Turbolinks mobile adapters, and you need to transition those as well, you might need a shim to translate calls to Turbolinks to Turbo. For Basecamp, this is what we needed:

```js
// Compatibility shim for mobile apps
window.Turbolinks = {
  visit: Turbo.visit,

  controller: {
    isDeprecatedAdapter(adapter) {
      return typeof adapter.visitProposedToLocation !== "function"
    },

    startVisitToLocationWithAction(location, action, restorationIdentifier) {
      window.Turbo.navigator.startVisit(location, restorationIdentifier, { action })
    },

    get restorationIdentifier() {
      return window.Turbo.navigator.restorationIdentifier
    },

    get adapter() {
      return window.Turbo.navigator.adapter
    },

    set adapter(adapter) {
      if (this.isDeprecatedAdapter(adapter)) {
        // Old mobile adapters do not support visitProposedToLocation()
        adapter.visitProposedToLocation = function(location, options) {
          adapter.visitProposedToLocationWithAction(location, options.action)
        }

        // Old mobile adapters use visit.location.absoluteURL, which is not available
        // because Turbo dropped the Location class in favor of the DOM URL API
        const adapterVisitStarted = adapter.visitStarted
        adapter.visitStarted = function(visit) {
          Object.defineProperties(visit.location, {
            absoluteURL: {
              configurable: true,
              get() { return this.toString() }
            }
          })

          adapter.currentVisit = visit
          adapterVisitStarted(visit)
        }
      }

      window.Turbo.registerAdapter(adapter)
    }
  }
}

// Required by the desktop app
document.addEventListener("turbo:load", function() {
  const event = new CustomEvent("turbolinks:load", { bubbles: true })
  document.documentElement.dispatchEvent(event)
})
```

# 04 Turbo Handbook

## 01 Introduction

### Introduction

Turbo bundles several techniques for creating fast, modern, progressively enhanced web applications without using much JavaScript. It offers a simpler alternative to the prevailing client-side frameworks which put all the logic in the front-end and confine the server side of your app to being little more than a JSON API.

With Turbo, you let the server deliver HTML directly, which means all the logic for checking permissions, interacting directly with your domain model, and everything else that goes into programming an application can happen more or less exclusively within your favorite programming language. You're no longer mirroring logic on both sides of a JSON divide. All the logic lives on the server, and the browser deals just with the final HTML.

You can read more about the benefits of this HTML-over-the-wire approach on the <a href="https://hotwired.dev/">Hotwire site</a>. What follows are the techniques that Turbo brings to make this possible.

#### Turbo Drive: Navigate within a persistent process

A key attraction with traditional single-page applications, when compared with the old-school, separate-pages approach, is the speed of navigation. SPAs get a lot of that speed from not constantly tearing down the application process, only to reinitialize it on the very next page.

Turbo Drive gives you that same speed by using the same persistent-process model, but without requiring you to craft your entire application around the paradigm. There's no client-side router to maintain, there's no state to carefully manage. The persistent process is managed by Turbo, and you write your server-side code as though you were living back in the early aughts – blissfully isolated from the complexities of today's SPA monstrosities!

This happens by intercepting all clicks on `<a href>` links to the same domain. When you click an eligible link, Turbo Drive prevents the browser from following it, changes the browser’s URL using the <a href="https://developer.mozilla.org/en-US/docs/Web/API/History">History API</a>, requests the new page using <a href="https://developer.mozilla.org/en-US/docs/Web/API/fetch">`fetch`</a>, and then renders the HTML response.

Same deal with forms. Their submissions are turned into `fetch` requests from which Turbo Drive will follow the redirect and render the HTML response.

During rendering, Turbo Drive replaces the current `<body>` element outright and merges the contents of the `<head>` element. The JavaScript window and document objects, and the `<html>` element, persist from one rendering to the next.

While it's possible to interact directly with Turbo Drive to control how visits happen or hook into the lifecycle of the request, the majority of the time this is a drop-in replacement where the speed is free just by adopting a few conventions.


#### Turbo Frames: Decompose complex pages

Most web applications present pages that contain several independent segments. For a discussion page, you might have a navigation bar on the top, a list of messages in the center, a form at the bottom to add a new message, and a sidebar with related topics. Generating this discussion page normally means generating each segment in a serialized manner, piecing them all together, then delivering the result as a single HTML response to the browser.

With Turbo Frames, you can place those independent segments inside frame elements that can scope their navigation and be lazily loaded. Scoped navigation means all interaction within a frame, like clicking links or submitting forms, happens within that frame, keeping the rest of the page from changing or reloading.

To wrap an independent segment in its own navigation context, enclose it in a `<turbo-frame>` tag. For example:

```html
<turbo-frame id="new_message">
  <form action="/messages" method="post">
    ...
  </form>
</turbo-frame>
```

When you submit the form above, Turbo extracts the matching `<turbo-frame id="new_message">` element from the redirected HTML response and swaps its content into the existing `new_message` frame element. The rest of the page stays just as it was.

Frames can also defer loading their contents in addition to scoping navigation. To defer loading a frame, add a `src` attribute whose value is the URL to be automatically loaded. As with scoped navigation, Turbo finds and extracts the matching frame from the resulting response and swaps its content into place:

```html
<turbo-frame id="messages" src="/messages">
  <p>This message will be replaced by the response from /messages.</p>
</turbo-frame>
```

This may sound a lot like old-school frames, or even `<iframe>`s, but Turbo Frames are part of the same DOM, so there's none of the weirdness or compromises associated with "real" frames. Turbo Frames are styled by the same CSS, part of the same JavaScript context, and are not placed under any additional content security restrictions.

In addition to turning your segments into independent contexts, Turbo Frames affords you:

1. **Efficient caching.** In the discussion page example above, the related topics sidebar needs to expire whenever a new related topic appears, but the list of messages in the center does not. When everything is just one page, the whole cache expires as soon as any of the individual segments do. With frames, each segment is cached independently, so you get longer-lived caches with fewer dependent keys.
1. **Parallelized execution.** Each defer-loaded frame is generated by its own HTTP request/response, which means it can be handled by a separate process. This allows for parallelized execution without having to manually manage the process. A complicated composite page that takes 400ms to complete end-to-end can be broken up with frames where the initial request might only take 50ms, and each of three defer-loaded frames each take 50ms. Now the whole page is done in 100ms because the three frames each taking 50ms run concurrently rather than sequentially.
1. **Ready for mobile.** In mobile apps, you usually can't have big, complicated composite pages. Each segment needs a dedicated screen. With an application built using Turbo Frames, you've already done this work of turning the composite page into segments. These segments can then appear in native sheets and screens without alteration (since they all have independent URLs).


#### Turbo Streams: Deliver live page changes

Making partial page changes in response to asynchronous actions is how we make the application feel alive. While Turbo Frames give us such updates in response to direct interactions within a single frame, Turbo Streams let us change any part of the page in response to updates sent over a WebSocket connection, SSE or other transport. (Think an <a href="http://itsnotatypo.com">imbox</a> that automatically updates when a new email arrives.)

Turbo Streams introduces a `<turbo-stream>` element with eight basic actions: `append`, `prepend`, `replace`, `update`, `remove`, `before`, `after`, and `refresh`. With these actions, along with the `target` attribute specifying the ID of the element you want to operate on, you can encode all the mutations needed to refresh the page. You can even combine several stream elements in a single stream message. Simply include the HTML you're interested in inserting or replacing in a <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template">template tag</a> and Turbo does the rest:

```html
<turbo-stream action="append" target="messages">
  <template>
    <div id="message_1">My new message!</div>
  </template>
</turbo-stream>
```

This stream element will take the `div` with the new message and append it to the container with the ID `messages`. It's just as simple to replace an existing element:

```html
<turbo-stream action="replace" target="message_1">
  <template>
    <div id="message_1">This changes the existing message!</div>
  </template>
</turbo-stream>
```

This is a conceptual continuation of what in the Rails world was first called <a href="https://weblog.rubyonrails.org/2006/3/28/rails-1-1-rjs-active-record-respond_to-integration-tests-and-500-other-things/">RJS</a> and then called <a href="https://signalvnoise.com/posts/3697-server-generated-javascript-responses">SJR</a>, but realized without any need for JavaScript. The benefits remain the same:

1. **Reuse the server-side templates**: Live page changes are generated using the same server-side templates that were used to create the first-load page.
1. **HTML over the wire**: Since all we're sending is HTML, you don't need any client-side JavaScript (beyond Turbo, of course) to process the update. Yes, the HTML payload might be a tad larger than a comparable JSON, but with gzip, the difference is usually negligible, and you save all the client-side effort it takes to fetch JSON and turn it into HTML.
1. **Simpler control flow**: It's really clear to follow what happens when messages arrive on the WebSocket, SSE or in response to form submissions. There's no routing, event bubbling, or other indirection required. It's just the HTML to be changed, wrapped in a single tag that tells us how.

Now, unlike RJS and SJR, it's not possible to call custom JavaScript functions as part of a Turbo Streams action. But this is a feature, not a bug. Those techniques can easily end up producing a tangled mess when way too much JavaScript is sent along with the response. Turbo focuses squarely on just updating the DOM, and then assumes you'll connect any additional behavior using <a href="https://stimulus.hotwired.dev">Stimulus</a> actions and lifecycle callbacks.


#### Turbo Native: Hybrid apps for iOS & Android

Turbo Native is ideal for building hybrid apps for iOS and Android. You can use your existing server-rendered HTML to get baseline coverage of your app's functionality in a native wrapper. Then you can spend all the time you saved on making the few screens that really benefit from high-fidelity native controls even better.

An application like Basecamp has hundreds of screens. Rewriting every single one of those screens would be an enormous task with very little benefit. Better to reserve the native firepower for high-touch interactions that really demand the highest fidelity. Something like the "New For You" inbox in Basecamp, for example, where we use swipe controls that need to feel just right. But most pages, like the one showing a single message, wouldn't really be any better if they were completely native.

Going hybrid doesn't just speed up your development process, it also gives you more freedom to upgrade your app without going through the slow and onerous app store release processes. Anything that's done in HTML can be changed in your web application, and instantly be available to all users. No waiting for Big Tech to approve your changes, no waiting for users to upgrade.

Turbo Native assumes you're using the recommended development practices available for iOS and Android. This is not a framework that abstracts native APIs away or even tries to let your native code be shareable between platforms. The part that's shareable is the HTML that's rendered server-side. But the native controls are written in the recommended native APIs.

See the <a href="https://github.com/hotwired/turbo-ios">Turbo Native: iOS</a> and <a href="https://github.com/hotwired/turbo-android">Turbo Native: Android</a> repositories for more documentation. See the native apps for HEY on <a href="https://apps.apple.com/us/app/hey-email/id1506603805">iOS</a> and <a href="https://play.google.com/store/apps/details?id=com.basecamp.hey&hl=en_US&gl=US">Android</a> to get a feel for just how good you can make a hybrid app powered by Turbo.


#### Integrate with backend frameworks

You don't need any backend framework to use Turbo. All the features are built to be used directly, without further abstractions. But if you have the opportunity to use a backend framework that's integrated with Turbo, you'll find life a lot simpler. [We've created a reference implementation for such an integration for Ruby on Rails](https://github.com/hotwired/turbo-rails).

## 02 Drive

### Navigate with Turbo Drive

Turbo Drive is the part of Turbo that enhances page-level navigation. It watches for link clicks and form submissions, performs them in the background, and updates the page without doing a full reload. It's the evolution of a library previously known as [Turbolinks](https://github.com/turbolinks/turbolinks).

${toc}

#### Page Navigation Basics

Turbo Drive models page navigation as a *visit* to a *location* (URL) with an *action*.

Visits represent the entire navigation lifecycle from click to render. That includes changing browser history, issuing the network request, restoring a copy of the page from cache, rendering the final response, and updating the scroll position.

During rendering, Turbo Drive replaces the contents of the requesting document's `<body>` with the contents of the response document's `<body>`, merges the contents of their `<head>`s too, and updates the `lang` attribute of the `<html>` element as needed. The point of merging instead of replacing the `<head>` elements is that if `<title>` or `<meta>` tags change, say, they will be updated as expected, but if links to assets are the same, they won't be touched and therefore the browser won't process them again.

There are two types of visit: an _application visit_, which has an action of _advance_ or _replace_, and a _restoration visit_, which has an action of _restore_.

#### Application Visits

Application visits are initiated by clicking a Turbo Drive-enabled link, or programmatically by calling [`Turbo.visit(location)`](#turbodrivevisit).

An application visit always issues a network request. When the response arrives, Turbo Drive renders its HTML and completes the visit.

If possible, Turbo Drive will render a preview of the page from cache immediately after the visit starts. This improves the perceived speed of frequent navigation between the same pages.

If the visit’s location includes an anchor, Turbo Drive will attempt to scroll to the anchored element. Otherwise, it will scroll to the top of the page.

Application visits result in a change to the browser’s history; the visit’s _action_ determines how.

![Advance visit action](https://s3.amazonaws.com/turbolinks-docs/images/advance.svg)

The default visit action is _advance_. During an advance visit, Turbo Drives pushes a new entry onto the browser’s history stack using [`history.pushState`](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState).

Applications using the Turbo Drive [iOS adapter](https://github.com/hotwired/turbo-ios) typically handle advance visits by pushing a new view controller onto the navigation stack. Similarly, applications using the [Android adapter](https://github.com/hotwired/turbo-android) typically push a new activity onto the back stack.

![Replace visit action](https://s3.amazonaws.com/turbolinks-docs/images/replace.svg)

You may wish to visit a location without pushing a new history entry onto the stack. The _replace_ visit action uses [`history.replaceState`](https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState) to discard the topmost history entry and replace it with the new location.

To specify that following a link should trigger a replace visit, annotate the link with `data-turbo-action="replace"`:

```html
<a href="/edit" data-turbo-action="replace">Edit</a>
```

To programmatically visit a location with the replace action, pass the `action: "replace"` option to `Turbo.visit`:

```js
Turbo.visit("/edit", { action: "replace" })
```

Applications using the Turbo Drive [iOS adapter](https://github.com/hotwired/turbo-ios) typically handle replace visits by dismissing the topmost view controller and pushing a new view controller onto the navigation stack without animation.

#### Restoration Visits

Turbo Drive automatically initiates a restoration visit when you navigate with the browser’s Back or Forward buttons. Applications using the [iOS](https://github.com/hotwired/turbo-ios) or [Android](https://github.com/hotwired/turbo-android) adapters initiate a restoration visit when moving backward in the navigation stack.

![Restore visit action](https://s3.amazonaws.com/turbolinks-docs/images/restore.svg)

If possible, Turbo Drive will render a copy of the page from cache without making a request. Otherwise, it will retrieve a fresh copy of the page over the network. See [Understanding Caching](#understanding-caching) for more details.

Turbo Drive saves the scroll position of each page before navigating away and automatically returns to this saved position on restoration visits.

Restoration visits have an action of _restore_ and Turbo Drive reserves them for internal use. You should not attempt to annotate links or invoke `Turbo.visit` with an action of `restore`.

#### Canceling Visits Before They Start

Application visits can be canceled before they start, regardless of whether they were initiated by a link click or a call to [`Turbo.visit`](#turbovisit).

Listen for the `turbo:before-visit` event to be notified when a visit is about to start, and use `event.detail.url` (or `$event.originalEvent.detail.url`, when using jQuery) to check the visit’s location. Then cancel the visit by calling `event.preventDefault()`.

Restoration visits cannot be canceled and do not fire `turbo:before-visit`. Turbo Drive issues restoration visits in response to history navigation that has *already taken place*, typically via the browser’s Back or Forward buttons.

#### Custom Rendering

Applications can customize the rendering process by adding a document-wide `turbo:before-render` event listener and overriding the `event.detail.render` property.

For example, you could merge the response document's `<body>` element into the requesting document's `<body>` element with [morphdom](https://github.com/patrick-steele-idem/morphdom):

```javascript
import morphdom from "morphdom"

addEventListener("turbo:before-render", (event) => {
  event.detail.render = (currentElement, newElement) => {
    morphdom(currentElement, newElement)
  }
})
```

#### Pausing Rendering

Applications can pause rendering and make additional preparations before continuing.

Listen for the `turbo:before-render` event to be notified when rendering is about to start, and pause it using `event.preventDefault()`. Once the preparation is done continue rendering by calling `event.detail.resume()`.

An example use case is adding exit animation for visits:
```javascript
document.addEventListener("turbo:before-render", async (event) => {
  event.preventDefault()

  await animateOut()

  event.detail.resume()
})
```

#### Pausing Requests

Application can pause request and make additional preparation before it will be executed.

Listen for the `turbo:before-fetch-request` event to be notified when a request is about to start, and pause it using `event.preventDefault()`. Once the preparation is done continue request by calling `event.detail.resume()`.

An example use case is setting `Authorization` header for the request:
```javascript
document.addEventListener("turbo:before-fetch-request", async (event) => {
  event.preventDefault()

  const token = await getSessionToken(window.app)
  event.detail.fetchOptions.headers["Authorization"] = `Bearer ${token}`

  event.detail.resume()
})
```

#### Performing Visits With a Different Method

By default, link clicks send a `GET` request to your server. But you can change this with `data-turbo-method`:

```html
<a href="/articles/54" data-turbo-method="delete">Delete the article</a>
```

The link will get converted into a hidden form next to the `a` element in the DOM. This means that the link can't appear inside another form, as you can't have nested forms.

You should also consider that for accessibility reasons, it's better to use actual forms and buttons for anything that's not a GET.

#### Requiring Confirmation for a Visit

Decorate links with `data-turbo-confirm`, and confirmation will be required for a visit to proceed.

```html
<a href="/articles" data-turbo-confirm="Do you want to leave this page?">Back to articles</a>
<a href="/articles/54" data-turbo-method="delete" data-turbo-confirm="Are you sure you want to delete the article?">Delete the article</a>
```

Use `Turbo.setConfirmMethod` to change the method that gets called for confirmation. The default is the browser's built in `confirm`.


#### Disabling Turbo Drive on Specific Links or Forms

Turbo Drive can be disabled on a per-element basis by annotating the element or any of its ancestors with `data-turbo="false"`.

```html
<a href="/" data-turbo="false">Disabled</a>

<form action="/messages" method="post" data-turbo="false">
  ...
</form>

<div data-turbo="false">
  <a href="/">Disabled</a>
  <form action="/messages" method="post">
    ...
  </form>
</div>
```

To reenable when an ancestor has opted out, use `data-turbo="true"`:

```html
<div data-turbo="false">
  <a href="/" data-turbo="true">Enabled</a>
</div>
```

Links or forms with Turbo Drive disabled will be handled normally by the browser.

If you want Drive to be opt-in rather than opt-out, then you can set `Turbo.session.drive = false`; then, `data-turbo="true"` is used to enable Drive on a per-element basis. If you're importing Turbo in a JavaScript pack, you can do this globally:

```js
import { Turbo } from "@hotwired/turbo-rails"
Turbo.session.drive = false
```

#### View transitions

In [browsers that support](https://caniuse.com/?search=View%20Transition%20API) the [View Transition API](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) Turbo can trigger view transitions when navigating between pages.

Turbo triggers a view transition when both the current and the next page have this meta tag:

```
<meta name="view-transition" content="same-origin" />
```

Turbo also adds a `data-turbo-visit-direction` attribute to the `<html>` element to indicate the direction of the transition. The attribute can have one of the following values:

- `forward` in advance visits.
- `back` in restoration visits.
- `none` in replace visits.

You can use this attribute to customize the animations that are performed during a transition:

```css
html[data-turbo-visit-direction="forward"]::view-transition-old(sidebar):only-child {
  animation: slide-to-right 0.5s ease-out;
}
```

#### Displaying Progress

During Turbo Drive navigation, the browser will not display its native progress indicator. Turbo Drive installs a CSS-based progress bar to provide feedback while issuing a request.

The progress bar is enabled by default. It appears automatically for any page that takes longer than 500ms to load. (You can change this delay with the [`Turbo.setProgressBarDelay`](#turbodrivesetprogressbardelay) method.)

The progress bar is a `<div>` element with the class name `turbo-progress-bar`. Its default styles appear first in the document and can be overridden by rules that come later.

For example, the following CSS will result in a thick green progress bar:

```css
.turbo-progress-bar {
  height: 5px;
  background-color: green;
}
```

To disable the progress bar entirely, set its `visibility` style to `hidden`:

```css
.turbo-progress-bar {
  visibility: hidden;
}
```

In tandem with the progress bar, Turbo Drive will also toggle the [`[aria-busy]` attribute][aria-busy] on the page's `<html>` element during page navigations started from Visits or Form Submissions. Turbo Drive will set `[aria-busy="true"]` when the navigation begins, and will remove the `[aria-busy]` attribute when the navigation completes.

[aria-busy]: https://www.w3.org/TR/wai-aria/#aria-busy
#### Reloading When Assets Change

As we saw above, Turbo Drive merges the contents of the `<head>` elements. However, if CSS or JavaScript change, that merge would evaluate them on top of the existing one. Typically, this would lead to undesirable conflicts. In such cases, it's necessary to fetch a completely new document through a standard, non-Ajax request.

To accomplish this, just annotate those asset elements with `data-turbo-track="reload"` and include a version identifier in your asset URLs. The identifier could be a number, a last-modified timestamp, or better, a digest of the asset’s contents, as in the following example.

```html
<head>
  ...
  <link rel="stylesheet" href="/application-258e88d.css" data-turbo-track="reload">
  <script src="/application-cbd3cd4.js" data-turbo-track="reload"></script>
</head>
```

#### Ensuring Specific Pages Trigger a Full Reload

You can ensure visits to a certain page will always trigger a full reload by including a `<meta name="turbo-visit-control">` element in the page’s `<head>`.

```html
<head>
  ...
  <meta name="turbo-visit-control" content="reload">
</head>
```

This setting may be useful as a workaround for third-party JavaScript libraries that don’t interact well with Turbo Drive page changes.

#### Setting a Root Location

By default, Turbo Drive only loads URLs with the same origin—i.e. the same protocol, domain name, and port—as the current document. A visit to any other URL falls back to a full page load.

In some cases, you may want to further scope Turbo Drive to a path on the same origin. For example, if your Turbo Drive application lives at `/app`, and the non-Turbo Drive help site lives at `/help`, links from the app to the help site shouldn’t use Turbo Drive.

Include a `<meta name="turbo-root">` element in your pages’ `<head>` to scope Turbo Drive to a particular root location. Turbo Drive will only load same-origin URLs that are prefixed with this path.

```html
<head>
  ...
  <meta name="turbo-root" content="/app">
</head>
```

#### Form Submissions

Turbo Drive handles form submissions in a manner similar to link clicks. The key difference is that form submissions can issue stateful requests using the HTTP POST method, while link clicks only ever issue stateless HTTP GET requests.

Throughout a submission, Turbo Drive will dispatch a series of [events][] that
target the `<form>` element and [bubble up][] through the document:

1. `turbo:submit-start`
2. `turbo:before-fetch-request`
3. `turbo:before-fetch-response`
4. `turbo:submit-end`

During a submission, Turbo Drive will set the "submitter" element's [disabled][] attribute when the submission begins, then remove the attribute after the submission ends. When submitting a `<form>` element, browsers will treat the `<input type="submit">` or `<button>` element that initiated the submission as the [submitter][]. To submit a `<form>` element programmatically, invoke the [HTMLFormElement.requestSubmit()][] method and pass an `<input type="submit">` or `<button>` element as an optional parameter.

If there are other changes you'd like to make during a `<form>` submission (for
example, disabling _all_ [fields within a submitted `<form>`][elements]), you
can declare your own event listeners:

```js
addEventListener("turbo:submit-start", ({ target }) => {
  for (const field of target.elements) {
    field.disabled = true
  }
})
```

[events]: /reference/events
[bubble up]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling_and_capture
[elements]: https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/elements
[disabled]: https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled
[submitter]: https://developer.mozilla.org/en-US/docs/Web/API/SubmitEvent/submitter
[HTMLFormElement.requestSubmit()]: https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/requestSubmit
#### Redirecting After a Form Submission

After a stateful request from a form submission, Turbo Drive expects the server to return an [HTTP 303 redirect response](https://en.wikipedia.org/wiki/HTTP_303), which it will then follow and use to navigate and update the page without reloading.

The exception to this rule is when the response is rendered with either a 4xx or 5xx status code. This allows form validation errors to be rendered by having the server respond with `422 Unprocessable Entity` and a broken server to display a "Something Went Wrong" screen on a `500 Internal Server Error`.

The reason Turbo doesn't allow regular rendering on 200's from POST requests is that browsers have built-in behavior for dealing with reloads on POST visits where they present a "Are you sure you want to submit this form again?" dialogue that Turbo can't replicate. Instead, Turbo will stay on the current URL upon a form submission that tries to render, rather than change it to the form action, since a reload would then issue a GET against that action URL, which may not even exist.

If the form submission is a GET request, you may render the directly rendered response by giving the form a `data-turbo-frame` target. If you'd like the URL to update as part of the rendering also pass a `data-turbo-action` attribute.

#### Streaming After a Form Submission

Servers may also respond to form submissions with a [Turbo Streams](streams) message by sending the header `Content-Type: text/vnd.turbo-stream.html` followed by one or more `<turbo-stream>` elements in the response body. This lets you update multiple parts of the page without navigating.

#### Prefetching Links on Hover

Turbo can also speed up perceived link navigation latency by automatically loading links on `mouseenter` events, and before the user clicks the link. This usually leads to a speed bump of 500-800ms per click navigation.

Prefetching links is enabled by default since Turbo v8, but you can disable it by adding this meta tag to your page:

```html
<meta name="turbo-prefetch" content="false">
```

To avoid prefetching links that the user is briefly hovering, Turbo waits 100ms after the user hovers over the link before prefetching it. But you may want to disable the prefetching behavior on certain links leading to pages with expensive rendering.

You can disable the behavior on a per-element basis by annotating the element or any of its ancestors with `data-turbo-prefetch="false"`.

```html
<html>
  <head>
    <meta name="turbo-prefetch" content="true">
  </head>
  <body>
    <a href="/articles">Articles</a> <!-- This link is prefetched -->
    <a href="/about" data-turbo-prefetch="false">About</a> <!-- Not prefetched -->
    <div data-turbo-prefetch="false"`>
      <!-- Links inside this div will not be prefetched -->
    </div>
  </body>
</html>
```

You can also disable the behaviour programatically by intercepting the `turbo:before-prefetch` event and calling `event.preventDefault()`.

```javascript
document.addEventListener("turbo:before-prefetch", (event) => {
  if (isSavingData() || hasSlowInternet()) {
    event.preventDefault()
  }
})

function isSavingData() {
  return navigator.connection?.saveData
}

function hasSlowInternet() {
  return navigator.connection?.effectiveType === "slow-2g" ||
         navigator.connection?.effectiveType === "2g"
}
```

#### Preload Links Into the Cache

Preload links into Turbo Drive's cache using the [data-turbo-preload][] boolean attribute.

This will make page transitions feel lightning fast by providing a preview of a page even before the first visit. Use it to preload the most important pages in your application. Avoid over usage, as it will lead to loading content that is not needed.

Not every `<a>` element can be preloaded. The `[data-turbo-preload]` attribute
won't have any effect on links that:

* navigate to another domain
* have a `[data-turbo-frame]` attribute that drives a `<turbo-frame>` element
* drive an ancestor `<turbo-frame>` element
* have the `[data-turbo="false"]` attribute
* have the `[data-turbo-stream]` attribute
* have a `[data-turbo-method]` attribute
* have an ancestor with the `[data-turbo="false"]` attribute
* have an ancestor with the `[data-turbo-prefetch="false"]` attribute

It also dovetails nicely with pages that leverage [Eager-Loading Frames](#eager-loaded-frame) or [Lazy-Loading Frames](#lazy-loaded-frame). As you can preload the structure of the page and show the user a meaningful loading state while the interesting content loads.
<br><br>

Note that preloaded `<a>` elements will dispatch [turbo:before-fetch-request](/reference/events) and [turbo:before-fetch-response](/reference/events) events. To distinguish a preloading `turbo:before-fetch-request` initiated event from an event initiated by another mechanism, check whether the request's `X-Sec-Purpose` header (read from the `event.detail.fetchOptions.headers["X-Sec-Purpose"]` property) is set to `"prefetch"`:

```js
addEventListener("turbo:before-fetch-request", (event) => {
  if (event.detail.fetchOptions.headers["X-Sec-Purpose"] === "prefetch") {
    // do additional preloading setup…
  } else {
    // do something else…
  }
})
```

[data-turbo-preload]: #data-attributes
## 03 Page Refreshes

### Smooth page refreshes with morphing

[Turbo Drive](/handbook/drive.html) makes navigation faster by avoiding full-page reloads. But there is a scenario where Turbo can raise the fidelity bar further: loading the current page again (page refresh).

A typical scenario for page refreshes is submitting a form and getting redirected back. In such scenarios, sensations significantly improve if only the changed contents get updated instead of replacing the `<body>` of the page. Turbo can do this on your behalf with morphing and scroll preservation.

${toc}

#### Morphing

You can configure how Turbo handles page refresh with a `<meta name="turbo-refresh-method">` in the page's head.

```html
<head>
  ...
  <meta name="turbo-refresh-method" content="morph">
</head>
```

The possible values are `morph` or `replace` (the default). When it is `morph,` when a page refresh happens, instead of replacing the page's `<body>,` Turbo will only update the DOM elements that have changed, keeping the rest untouched. This approach delivers better sensations because it keeps the screen state.

Under the hood, Turbo uses the fantastic [idiomorph library](https://github.com/bigskysoftware/idiomorph).

#### Scroll preservation

You can configure how Turbo handles scrolling with a `<meta name="turbo-refresh-scroll">` in the page's head.

```html
<head>
  ...
  <meta name="turbo-refresh-scroll" content="preserve">
</head>
```

The possible values are `preserve` or `reset` (the default). When it is `preserve`, when a page refresh happens, Turbo will keep the page's vertical and horizontal scroll.

#### Exclude sections from morphing

Sometimes, you want to ignore certain elements while morphing. For example, you might have a popover that you want to keep open when the page refreshes. You can flag such elements with `data-turbo-permanent`, and Turbo won't attempt to morph them.

```html
<div data-turbo-permanent>...</div>
```

#### Turbo frames

You can use [turbo frames](/handbook/frames.html) to define regions in your screen that will get reloaded using morphing when a page refresh happens. To do so, you must flag those frames with `refresh="morph"`.

```html
<turbo-frame id="my-frame" refresh="morph">
  ...
</turbo-frame>
```

With this mechanism, you can load additional content that didn't arrive in the initial page load (e.g., pagination). When a page refresh happens, Turbo won't remove the frame contents; instead, it will reload the turbo frame and render its contents with morphing.

#### Broadcasting page refreshes

There is a new [turbo stream action](/handbook/streams.html) called `refresh` that will trigger a page refresh:

```html
<turbo-stream action="refresh"></turbo-stream>
```

Server-side frameworks can leverage these streams to offer a simple but powerful broadcasting model: the server broadcasts a single general signal, and pages smoothly refresh with morphing. 

You can see how the  [`turbo-rails`](https://github.com/hotwired/turbo-rails) gem does it for Rails:

```ruby
### In the model
class Calendar < ApplicationRecord
  broadcasts_refreshes
end

### View
turbo_stream_from @calendar
```

## 04 Frames

### Decompose with Turbo Frames

Turbo Frames allow predefined parts of a page to be updated on request. Any links and forms inside a frame are captured, and the frame contents automatically updated after receiving a response. Regardless of whether the server provides a full document, or just a fragment containing an updated version of the requested frame, only that particular frame will be extracted from the response to replace the existing content.

Frames are created by wrapping a segment of the page in a `<turbo-frame>` element. Each element must have a unique ID, which is used to match the content being replaced when requesting new pages from the server. A single page can have multiple frames, each establishing their own context:

```html
<body>
  <div id="navigation">Links targeting the entire page</div>

  <turbo-frame id="message_1">
    <h1>My message title</h1>
    <p>My message content</p>
    <a href="/messages/1/edit">Edit this message</a>
  </turbo-frame>

  <turbo-frame id="comments">
    <div id="comment_1">One comment</div>
    <div id="comment_2">Two comments</div>

    <form action="/messages/comments">...</form>
  </turbo-frame>
</body>
```

This page has two frames: One to display the message itself, with a link to edit it. One to list all the comments, with a form to add another. Each create their own context for navigation, capturing both links and submitting forms.

When the link to edit the message is clicked, the response provided by `/messages/1/edit` has its `<turbo-frame id="message_1">` segment extracted, and the content replaces the frame from where the click originated. The edit response might look like this:

```html
<body>
  <h1>Editing message</h1>

  <turbo-frame id="message_1">
    <form action="/messages/1">
      <input name="message[name]" type="text" value="My message title">
      <textarea name="message[content]">My message content</textarea>
      <input type="submit">
    </form>
  </turbo-frame>
</body>
```

Notice how the `<h1>` isn't inside the `<turbo-frame>`. This means it will remain unchanged when the form replaces the display of the message upon editing. Only content inside a matching `<turbo-frame>` is used when the frame is updated.

Thus your page can easily play dual purposes: Make edits in place within a frame or edits outside of a frame where the entire page is dedicated to the action.

Frames serve a specific purpose: to compartmentalize the content and navigation for a fragment of the document. Their presence has ramification on any `<a>` elements or `<form>` elements contained by their child content, and shouldn't be introduced unnecessarily. Turbo Frames do not contribute support to the usage of [Turbo Stream](/handbook/streams). If your application utilizes `<turbo-frame>` elements for the sake of a `<turbo-stream>` element, change the `<turbo-frame>` into another [built-in element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

#### Eager-Loading Frames

Frames don't have to be populated when the page that contains them is loaded. If a `src` attribute is present on the `turbo-frame` tag, the referenced URL will automatically be loaded as soon as the tag appears on the page:

```html
<body>
  <h1>Imbox</h1>

  <div id="emails">
    ...
  </div>

  <turbo-frame id="set_aside_tray" src="/emails/set_aside">
  </turbo-frame>

  <turbo-frame id="reply_later_tray" src="/emails/reply_later">
  </turbo-frame>
</body>
```

This page lists all the emails available in your <a href="http://itsnotatypo.com">imbox</a> immediately upon loading the page, but then makes two subsequent requests to present small trays at the bottom of the page for emails that have been set aside or are waiting for a later reply. These trays are created out of separate HTTP requests made to the URLs referenced in the `src`.

In the example above, the trays start empty, but it's also possible to populate the eager-loading frames with initial content, which is then overwritten when the content is fetched from the `src`:

```html
<turbo-frame id="set_aside_tray" src="/emails/set_aside">
  <img src="/icons/spinner.gif">
</turbo-frame>
```

Upon loading the imbox page, the set-aside tray is loaded from `/emails/set_aside`, and the response must contain a corresponding `<turbo-frame id="set_aside_tray">` element as in the original example:

```html
<body>
  <h1>Set Aside Emails</h1>

  <p>These are emails you've set aside</p>

  <turbo-frame id="set_aside_tray">
    <div id="emails">
      <div id="email_1">
        <a href="/emails/1">My important email</a>
      </div>
    </div>
  </turbo-frame>
</body>
```

This page now works in both its minimized form, where only the `div` with the individual emails are loaded into the tray frame on the imbox page, but also as a direct destination where a header and a description is provided. Just like in the example with the edit message form.

Note that the `<turbo-frame>` on `/emails/set_aside` does not contain a `src` attribute. That attribute is only added to the frame that needs to lazily load the content, not to the rendered frame that provides the content.

During navigation, a Frame will set `[aria-busy="true"]` on the `<turbo-frame>` element when fetching the new contents. When the navigation completes, the Frame will remove the `[aria-busy]` attribute. When navigating the `<turbo-frame>` through a `<form>` submission, Turbo will toggle the Form's `[aria-busy="true"]` attribute in tandem with the Frame's.

After navigation finishes, a Frame will set the `[complete]` attribute on the
`<turbo-frame>` element.

[aria-busy]: https://www.w3.org/TR/wai-aria/#aria-busy
#### Lazy-Loading Frames

Frames that aren't visible when the page is first loaded can be marked with `loading="lazy"` such that they don't start loading until they become visible. This works exactly like the `lazy=true` attribute on `img`. It's a great way to delay loading of frames that sit inside `summary`/`detail` pairs or modals or anything else that starts out hidden and is then revealed.


#### Cache Benefits to Loading Frames

Turning page segments into frames can help make the page simpler to implement, but an equally important reason for doing this is to improve cache dynamics. Complex pages with many segments are hard to cache efficiently, especially if they mix content shared by many with content specialized for an individual user. The more segments, the more dependent keys required for the cache look-up, the more frequently the cache will churn.

Frames are ideal for separating segments that change on different timescales and for different audiences. Sometimes it makes sense to turn the per-user element of a page into a frame, if the bulk of the rest of the page is then easily shared across all users. Other times, it makes sense to do the opposite, where a heavily personalized page turns the one shared segment into a frame to serve it from a shared cache.

While the overhead of fetching loading frames is generally very low, you should still be judicious in just how many you load, especially if these frames would create load-in jitter on the page. Frames are, however, essentially free if the content isn't immediately visible upon loading the page. Either because they're hidden behind modals or below the fold.


#### Targeting Navigation Into or Out of a Frame

By default, navigation within a frame will target just that frame. This is true for both following links and submitting forms. But navigation can drive the entire page instead of the enclosing frame by setting the target to `_top`. Or it can drive another named frame by setting the target to the ID of that frame.

In the example with the set-aside tray, the links within the tray point to individual emails. You don't want those links to look for frame tags that match the `set_aside_tray` ID. You want to navigate directly to that email. This is done by marking the tray frames with the `target` attribute:

```html
<body>
  <h1>Imbox</h1>
  ...
  <turbo-frame id="set_aside_tray" src="/emails/set_aside" target="_top">
  </turbo-frame>
</body>

<body>
  <h1>Set Aside Emails</h1>
  ...
  <turbo-frame id="set_aside_tray" target="_top">
    ...
  </turbo-frame>
</body>
```

Sometimes you want most links to operate within the frame context, but not others. This is also true of forms. You can add the `data-turbo-frame` attribute on non-frame elements to control this:

```html
<body>
  <turbo-frame id="message_1">
    ...
    <a href="/messages/1/edit">
      Edit this message (within the current frame)
    </a>

    <a href="/messages/1/permission" data-turbo-frame="_top">
      Change permissions (replace the whole page)
    </a>
  </turbo-frame>

  <form action="/messages/1/delete" data-turbo-frame="message_1">
    <a href="/messages/1/warning" data-turbo-frame="_self">
      Load warning within current frame
    </a>

    <input type="submit" value="Delete this message">
    (with a confirmation shown in a specific frame)
  </form>
</body>
```

#### Promoting a Frame Navigation to a Page Visit

Navigating Frames provides applications with an opportunity to change part of
the page's contents while preserving the rest of the document's state (for
example, its current scroll position or focused element). There are times when
we want changes to a Frame to also affect the browser's [history][].

To promote a Frame navigation to a Visit, render the element with the
`[data-turbo-action]` attribute. The attribute supports all [Visit][] values,
and can be declared on:

* the `<turbo-frame>` element
* any `<a>` elements that navigate the `<turbo-frame>`
* any `<form>` elements that navigate the `<turbo-frame>`
* any `<input type="submit">` or `<button>` elements contained within `<form>`
  elements that navigate the `<turbo-frame>`

For example, consider a Frame that renders a paginated list of articles and
transforms navigations into ["advance" Actions][advance]:

```html
<turbo-frame id="articles" data-turbo-action="advance">
  <a href="/articles?page=2" rel="next">Next page</a>
</turbo-frame>
```

Clicking the `<a rel="next">` element will set _both_ the `<turbo-frame>`
element's `[src]` attribute _and_ the browser's path to `/articles?page=2`.

**Note:** when rendering the page after refreshing the browser, it is _the
application's_ responsibility to render the _second_ page of articles along with
any other state derived from the URL path and search parameters.

[history]: https://developer.mozilla.org/en-US/docs/Web/API/History
[Visit]: #page-navigation-basics
[advance]: #application-visits
#### "Breaking out" from a Frame

In most cases, requests that originate from a `<turbo-frame>` are expected to fetch content for that frame (or for
another part of the page, depending on the use of the `target` or `data-turbo-frame` attributes). This means the
response should always contain the expected `<turbo-frame>` element. If a response is missing the `<turbo-frame>`
element that Turbo expects, it's considered an error; when it happens Turbo will write an informational message into the
frame, and throw an exception.

In certain, specific cases, you might want the response to a `<turbo-frame>` request to be treated as a new, full-page
navigation instead, effectively "breaking out" of the frame. The classic example of this is when a lost or expired
session causes an application to redirect to a login page. In this case, it's better for Turbo to display that login
page rather than treat it as an error.

The simplest way to achieve this is to specify that the login page requires a full-page reload, by including the
[`turbo-visit-control`][meta] meta tag:

```html
<head>
  <meta name="turbo-visit-control" content="reload">
  ...
</head>
```

If you're using Turbo Rails, you can use the `turbo_page_requires_reload` helper to accomplish the same thing.

Pages that specify `turbo-visit-control` `reload` will always result in a full-page navigation, even if the request
originated from inside a frame.

If your application needs to handle missing frames in some other way, you can intercept the
[`turbo:frame-missing`][events] event to, for example, transform the response or perform a visit to another location.

[meta]: #meta-tags
[events]: /reference/events

#### Anti-Forgery Support (CSRF)

Turbo provides [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) protection by checking the DOM for the existence of a `<meta>` tag with a `name` value of either `csrf-param` or `csrf-token`. For example:

```html
<meta name="csrf-token" content="[your-token]">
```

Upon form submissions, the token will be automatically added to the request's headers as `X-CSRF-TOKEN`. Requests made with `data-turbo="false"` will skip adding the token to headers.

#### Custom Rendering

Turbo's default `<turbo-frame>` rendering process replaces the contents of the requesting `<turbo-frame>` element with the contents of a matching `<turbo-frame>` element in the response. In practice, a `<turbo-frame>` element's contents are rendered as if they operated on by [`<turbo-stream action="update">`](#update) element. The underlying renderer extracts the contents of the `<turbo-frame>` in the response and uses them to replace the requesting `<turbo-frame>` element's contents. The `<turbo-frame>` element itself remains unchanged, save for the [`[src]`, `[busy]`, and `[complete]` attributes that Turbo Drive manages](/reference/frames#html-attributes) throughout the stages of the element's request-response lifecycle.

Applications can customize the `<turbo-frame>` rendering process by adding a `turbo:before-frame-render` event listener and overriding the `event.detail.render` property.

For example, you could merge the response `<turbo-frame>` element into the requesting `<turbo-frame>` element with [morphdom](https://github.com/patrick-steele-idem/morphdom):

```javascript
import morphdom from "morphdom"

addEventListener("turbo:before-frame-render", (event) => {
  event.detail.render = (currentElement, newElement) => {
    morphdom(currentElement, newElement, { childrenOnly: true })
  }
})
```

Since `turbo:before-frame-render` events bubble up the document, you can override one `<turbo-frame>` element's rendering by attaching the event listener directly to the element, or override all `<turbo-frame>` elements' rendering by attaching the listener to the `document`.

#### Pausing Rendering

Applications can pause rendering and make additional preparations before continuing.

Listen for the `turbo:before-frame-render` event to be notified when rendering is about to start, and pause it using `event.preventDefault()`. Once the preparation is done continue rendering by calling `event.detail.resume()`.

An example use case is adding exit animation:

```javascript
document.addEventListener("turbo:before-frame-render", async (event) => {
  event.preventDefault()

  await animateOut()

  event.detail.resume()
})
```

## 05 Streams

### Come Alive with Turbo Streams

Turbo Streams deliver page changes as fragments of HTML wrapped in `<turbo-stream>` elements. Each stream element specifies an action together with a target ID to declare what should happen to the HTML inside it. These elements can be delivered to the browser synchronously as a classic HTTP response, or asynchronously over transports such as webSockets, SSE, etc, to bring the application alive with updates made by other users or processes.

They can be used to surgically update the DOM after a user action such as removing an element from a list without reloading the whole page, or to implement real-time capabilities such as appending a new message to a live conversation as it is sent by a remote user.

#### Stream Messages and Actions

A Turbo Streams message is a fragment of HTML consisting of `<turbo-stream>` elements. The stream message below demonstrates the eight possible stream actions:

```html
<turbo-stream action="append" target="messages">
  <template>
    <div id="message_1">
      This div will be appended to the element with the DOM ID "messages".
    </div>
  </template>
</turbo-stream>

<turbo-stream action="prepend" target="messages">
  <template>
    <div id="message_1">
      This div will be prepended to the element with the DOM ID "messages".
    </div>
  </template>
</turbo-stream>

<turbo-stream action="replace" target="message_1">
  <template>
    <div id="message_1">
      This div will replace the existing element with the DOM ID "message_1".
    </div>
  </template>
</turbo-stream>

<turbo-stream action="update" target="unread_count">
  <template>
    <!-- The contents of this template will replace the
    contents of the element with ID "unread_count" by
    setting innerHtml to "" and then switching in the
    template contents. Any handlers bound to the element
    "unread_count" would be retained. This is to be
    contrasted with the "replace" action above, where
    that action would necessitate the rebuilding of
    handlers. -->
    1
  </template>
</turbo-stream>

<turbo-stream action="remove" target="message_1">
  <!-- The element with DOM ID "message_1" will be removed.
  The contents of this stream element are ignored. -->
</turbo-stream>

<turbo-stream action="before" target="current_step">
  <template>
    <!-- The contents of this template will be added before the
    the element with ID "current_step". -->
    <li>New item</li>
  </template>
</turbo-stream>

<turbo-stream action="after" target="current_step">
  <template>
    <!-- The contents of this template will be added after the
    the element with ID "current_step". -->
    <li>New item</li>
  </template>
</turbo-stream>

<turbo-stream action="morph" target="current_step">
  <template>
    <!-- The contents of this template will replace the 
    element with ID "current_step" via morph. -->
    <li>New item</li>
  </template>
</turbo-stream>

<turbo-stream action="morph" target="current_step" children-only>
  <template>
    <!-- The contents of this template will replace the 
    children of the element with ID "current_step" via morph. -->
    <li>New item</li>
  </template>
</turbo-stream>

<turbo-stream action="refresh" request-id="abcd-1234"></turbo-stream>
```

Note that every `<turbo-stream>` element must wrap its included HTML inside a `<template>` element.

A Turbo Stream can integrate with any element in the document that can be
resolved by an [id](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id) attribute or [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) (with the exception of `<template>` element or `<iframe>` element content). It is not necessary to change targeted elements into [`<turbo-frame>` elements](/handbook/frames). If your application utilizes `<turbo-frame>` elements for the sake of a `<turbo-stream>` element, change the `<turbo-frame>` into another [built-in element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).


You can render any number of stream elements in a single stream message from a WebSocket, SSE or in response to a form submission.

#### Actions With Multiple Targets

Actions can be applied against multiple targets using the `targets` attribute with a CSS query selector, instead of the regular `target` attribute that uses a dom ID reference. Examples:

```html
<turbo-stream action="remove" targets=".old_records">
  <!-- The element with the class "old_records" will be removed.
  The contents of this stream element are ignored. -->
</turbo-stream>

<turbo-stream action="after" targets="input.invalid_field">
  <template>
    <!-- The contents of this template will be added after the
    all elements that match "inputs.invalid_field". -->
    <span>Incorrect</span>
  </template>
</turbo-stream>
```

#### Streaming From HTTP Responses

Turbo knows to automatically attach `<turbo-stream>` elements when they arrive in response to `<form>` submissions that declare a [MIME type][] of `text/vnd.turbo-stream.html`. When submitting a `<form>` element whose [method][] attribute is set to `POST`, `PUT`, `PATCH`, or `DELETE`, Turbo injects `text/vnd.turbo-stream.html` into the set of response formats in the request's [Accept][] header. When responding to requests containing that value in its [Accept][] header, servers can tailor their responses to deal with Turbo Streams, HTTP redirects, or other types of clients that don't support streams (such as native applications).

In a Rails controller, this would look like:

```ruby
def destroy
  @message = Message.find(params[:id])
  @message.destroy

  respond_to do |format|
    format.turbo_stream { render turbo_stream: turbo_stream.remove(@message) }
    format.html         { redirect_to messages_url }
  end
end
```

By default, Turbo doesn't add the `text/vnd.turbo-stream.html` MIME type when submitting links, or forms with a method type of `GET`. To use Turbo Streams responses with `GET` requests in an application you can instruct Turbo to include the MIME type by adding a `data-turbo-stream` attribute to a link or form.

[MIME type]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types
[method]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#attr-method
[Accept]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept
#### Reusing Server-Side Templates

The key to Turbo Streams is the ability to reuse your existing server-side templates to perform live, partial page changes. The HTML template used to render each message in a list of such on the first page load is the same template that'll be used to add one new message to the list dynamically later. This is at the essence of the HTML-over-the-wire approach: You don't need to serialize the new message as JSON, receive it in JavaScript, render a client-side template. It's just the standard server-side templates reused.

Another example from how this would look in Rails:

```erb
<!-- app/views/messages/_message.html.erb -->
<div id="<%= dom_id message %>">
  <%= message.content %>
</div>

<!-- app/views/messages/index.html.erb -->
<h1>All the messages</h1>
<%= render partial: "messages/message", collection: @messages %>
```

```ruby
### app/controllers/messages_controller.rb
class MessagesController < ApplicationController
  def index
    @messages = Message.all
  end

  def create
    message = Message.create!(params.require(:message).permit(:content))

    respond_to do |format|
      format.turbo_stream do
        render turbo_stream: turbo_stream.append(:messages, partial: "messages/message",
          locals: { message: message })
      end

      format.html { redirect_to messages_url }
    end
  end
end
```

When the form to create a new message submits to the `MessagesController#create` action, the very same partial template that was used to render the list of messages in `MessagesController#index` is used to render the turbo-stream action. This will come across as a response that looks like this:

```html
Content-Type: text/vnd.turbo-stream.html; charset=utf-8

<turbo-stream action="append" target="messages">
  <template>
    <div id="message_1">
      The content of the message.
    </div>
  </template>
</turbo-stream>
```

This `messages/message` template partial can then also be used to re-render the message following an edit/update operation. Or to supply new messages created by other users over a WebSocket or a SSE connection. Being able to reuse the same templates across the whole spectrum of use is incredibly powerful, and key to reducing the amount of work it takes to create these modern, fast applications.

#### Progressively Enhance When Necessary

It's good practice to start your interaction design without Turbo Streams. Make the entire application work as it would if Turbo Streams were not available, then layer them on as a level-up. This means you won't come to rely on the updates for flows that need to work in native applications or elsewhere without them.

The same is especially true for WebSocket updates. On poor connections, or if there are server issues, your WebSocket may well get disconnected. If the application is designed to work without it, it'll be more resilient.

#### But What About Running JavaScript?

Turbo Streams consciously restricts you to eight actions: append, prepend, (insert) before, (insert) after, replace, update, remove, and refresh. If you want to trigger additional behavior when these actions are carried out, you should attach behavior using <a href="https://stimulus.hotwired.dev">Stimulus</a> controllers. This restriction allows Turbo Streams to focus on the essential task of delivering HTML over the wire, leaving additional logic to live in dedicated JavaScript files.

Embracing these constraints will keep you from turning individual responses into a jumble of behaviors that cannot be reused and which make the app hard to follow. The key benefit from Turbo Streams is the ability to reuse templates for initial rendering of a page through all subsequent updates.

#### Custom Actions

By default, Turbo Streams support [eight values for its `action` attribute](#the-seven-actions). If your application needs to support other behaviors, you can override the `event.detail.render` function.

For example, if you'd like to expand upon the eight actions to support `<turbo-stream>` elements with `[action="alert"]` or `[action="log"]`, you could declare a `turbo:before-stream-render` listener to provide custom behavior:

```javascript
addEventListener("turbo:before-stream-render", ((event) => {
  const fallbackToDefaultActions = event.detail.render

  event.detail.render = function (streamElement) {
    if (streamElement.action == "alert") {
      // ...
    } else if (streamElement.action == "log") {
      // ...
    } else {
      fallbackToDefaultActions(streamElement)
    }
  }
}))
```

In addition to listening for `turbo:before-stream-render` events, applications
can also declare actions as properties directly on `StreamActions`:

```javascript
import { StreamActions } from "@hotwired/turbo"

// <turbo-stream action="log" message="Hello, world"></turbo-stream>
//
StreamActions.log = function () {
  console.log(this.getAttribute("message"))
}
```

#### Integration with Server-Side Frameworks

Of all the techniques that are included with Turbo, it's with Turbo Streams you'll see the biggest advantage from close integration with your backend framework. As part of the official Hotwire suite, we've created a reference implementation for what such an integration can look like in the <a href="https://github.com/hotwired/turbo-rails">turbo-rails gem</a>. This gem relies on the built-in support for both WebSockets and asynchronous rendering present in Rails through the Action Cable and Active Job frameworks, respectively.

Using the <a href="https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb">Broadcastable</a> concern mixed into Active Record, you can trigger WebSocket updates directly from your domain model. And using the <a href="https://github.com/hotwired/turbo-rails/blob/main/app/models/turbo/streams/tag_builder.rb">Turbo::Streams::TagBuilder</a>, you can render `<turbo-stream>` elements in inline controller responses or dedicated templates, invoking the five actions with associated rendering through a simple DSL.

Turbo itself is completely backend-agnostic, though. So we encourage other frameworks in other ecosystems to look at the reference implementation provided for Rails to create their own tight integration.

Turbo's `<turbo-stream-source>` custom element connects to a stream source
through its `[src]` attribute. When declared with an `ws://` or `wss://` URL,
the underlying stream source will be a [WebSocket][] instance. Otherwise, the
connection is through an [EventSource][].

When the element is connected to the document, the stream source is
connected. When the element is disconnected, the stream is disconnected.

Since the document's `<head>` is persistent across Turbo navigations, it's
important to mount the `<turbo-stream-source>` as a descendant of the document's
`<body>` element.

Typical full page navigations driven by Turbo will result in the `<body>` being
discarded and replaced with the resulting document. It's the server's
responsibility to ensure that the element is present on any page that requires
streaming.

Alternatively, a straightforward way to integrate any backend application with Turbo Streams is to rely on [the Mercure protocol](https://mercure.rocks). Mercure defines a convenient way for server applications to broadcast page changes to every connected clients through [Server-Sent Events (SSE)](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events). [Learn how to use Mercure with Turbo Streams](https://mercure.rocks/docs/ecosystem/hotwire).

[WebSocket]: https://developer.mozilla.org/en-US/docs/Web/API/WebSocket
[EventSource]: https://developer.mozilla.org/en-US/docs/Web/API/EventSource
## 06 Native

### Go Native on iOS & Android

Turbo Native for iOS provides the tooling to wrap your Turbo-enabled web app in a native iOS shell. It manages a single WKWebView instance across multiple view controllers, giving you native navigation UI with all the client-side performance benefits of Turbo. See <a href="https://github.com/hotwired/turbo-ios">Turbo Native: iOS</a> for more details.

Turbo Native for Android provides the same kind of tooling, managing a single WebView instance across multiple Fragment destinations. See <a href="https://github.com/hotwired/turbo-android">Turbo Native: Android</a> for more details.

The best way to see what's possible with the native adapters is to setup the demo native application. We have one [for iOS](https://github.com/hotwired/turbo-ios/blob/main/Demo/README.md) and [for Android](https://github.com/hotwired/turbo-android/blob/main/demo/README.md). You can open the code in your native environments and follow along to explore all the features.
## 07 Building

### Building Your Turbo Application

Turbo is fast because it prevents the whole page from reloading when you follow a link or submit a form. Your application becomes a persistent, long-running process in the browser. This requires you to rethink the way you structure your JavaScript.

In particular, you can no longer depend on a full page load to reset your environment every time you navigate. The JavaScript `window` and `document` objects retain their state across page changes, and any other objects you leave in memory will stay in memory.

With awareness and a little extra care, you can design your application to gracefully handle this constraint without tightly coupling it to Turbo.

#### Working with Script Elements

Your browser automatically loads and evaluates any `<script>` elements present on the initial page load.

When you navigate to a new page, Turbo Drive looks for any `<script>` elements in the new page’s `<head>` which aren’t present on the current page. Then it appends them to the current `<head>` where they’re loaded and evaluated by the browser. You can use this to load additional JavaScript files on-demand.

Turbo Drive evaluates `<script>` elements in a page’s `<body>` each time it renders the page. You can use inline body scripts to set up per-page JavaScript state or bootstrap client-side models. To install behavior, or to perform more complex operations when the page changes, avoid script elements and use the `turbo:load` event instead.

Annotate `<script>` elements with `data-turbo-eval="false"` if you do not want Turbo to evaluate them after rendering. Note that this annotation will not prevent your browser from evaluating scripts on the initial page load.

##### Loading Your Application’s JavaScript Bundle

Always make sure to load your application’s JavaScript bundle using `<script>` elements in the `<head>` of your document. Otherwise, Turbo Drive will reload the bundle with every page change.

```html
<head>
  ...
  <script src="/application-cbd3cd4.js" defer></script>
</head>
```

You should also consider configuring your asset packaging system to fingerprint each script so it has a new URL when its contents change. Then you can use the `data-turbo-track` attribute to force a full page reload when you deploy a new JavaScript bundle. See [Reloading When Assets Change](#reloading-when-assets-change) for information.

#### Understanding Caching

Turbo Drive maintains a cache of recently visited pages. This cache serves two purposes: to display pages without accessing the network during restoration visits, and to improve perceived performance by showing temporary previews during application visits.

When navigating by history (via [Restoration Visits](#restoration-visits)), Turbo Drive will restore the page from cache without loading a fresh copy from the network, if possible.

Otherwise, during standard navigation (via [Application Visits](#application-visits)), Turbo Drive will immediately restore the page from cache and display it as a preview while simultaneously loading a fresh copy from the network. This gives the illusion of instantaneous page loads for frequently accessed locations.

Turbo Drive saves a copy of the current page to its cache just before rendering a new page. Note that Turbo Drive copies the page using [`cloneNode(true)`](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode), which means any attached event listeners and associated data are discarded.

##### Preparing the Page to be Cached

Listen for the `turbo:before-cache` event if you need to prepare the document before Turbo Drive caches it. You can use this event to reset forms, collapse expanded UI elements, or tear down any third-party widgets so the page is ready to be displayed again.

```js
document.addEventListener("turbo:before-cache", function() {
  // ...
})
```

Certain page elements are inherently _temporary_, like flash messages or alerts. If they’re cached with the document they’ll be redisplayed when it’s restored, which is rarely desirable. You can annotate such elements with `data-turbo-temporary` to have Turbo Drive automatically remove them from the page before it’s cached.

```html
<body>
  <div class="flash" data-turbo-temporary>
    Your cart was updated!
  </div>
  ...
</body>
```

##### Detecting When a Preview is Visible

Turbo Drive adds a `data-turbo-preview` attribute to the `<html>` element when it displays a preview from cache. You can check for the presence of this attribute to selectively enable or disable behavior when a preview is visible.

```js
if (document.documentElement.hasAttribute("data-turbo-preview")) {
  // Turbo Drive is displaying a preview
}
```

##### Opting Out of Caching

You can control caching behavior on a per-page basis by including a `<meta name="turbo-cache-control">` element in your page’s `<head>` and declaring a caching directive.

Use the `no-preview` directive to specify that a cached version of the page should not be shown as a preview during an application visit. Pages marked no-preview will only be used for restoration visits.

To specify that a page should not be cached at all, use the `no-cache` directive. Pages marked no-cache will always be fetched over the network, including during restoration visits.

```html
<head>
  ...
  <meta name="turbo-cache-control" content="no-cache">
</head>
```

To completely disable caching in your application, ensure every page contains a no-cache directive.

##### Opting Out of Caching from the client-side

The value of the `<meta name="turbo-cache-control">` element can also be controlled by a client-side API exposed via `Turbo.cache`.

```js
// Set cache control of current page to `no-cache`
Turbo.cache.exemptPageFromCache()

// Set cache control of current page to `no-preview`
Turbo.cache.exemptPageFromPreview()
```

Both functions will create a `<meta name="turbo-cache-control">` element in the `<head>` if the element is not already present.

A previously set cache control value can be reset via:

```js
Turbo.cache.resetCacheControl()
```

#### Installing JavaScript Behavior

You may be used to installing JavaScript behavior in response to the `window.onload`, `DOMContentLoaded`, or jQuery `ready` events. With Turbo, these events will fire only in response to the initial page load, not after any subsequent page changes. We compare two strategies for connecting JavaScript behavior to the DOM below.

##### Observing Navigation Events

Turbo Drive triggers a series of events during navigation. The most significant of these is the `turbo:load` event, which fires once on the initial page load, and again after every Turbo Drive visit.

You can observe the `turbo:load` event in place of `DOMContentLoaded` to set up JavaScript behavior after every page change:

```js
document.addEventListener("turbo:load", function() {
  // ...
})
```

Keep in mind that your application will not always be in a pristine state when this event is fired, and you may need to clean up behavior installed for the previous page.

Also note that Turbo Drive navigation may not be the only source of page updates in your application, so you may wish to move your initialization code into a separate function which you can call from `turbo:load` and anywhere else you may change the DOM.

When possible, avoid using the `turbo:load` event to add other event listeners directly to elements on the page body. Instead, consider using [event delegation](https://learn.jquery.com/events/event-delegation/) to register event listeners once on `document` or `window`.

See the [Full List of Events](/reference/events) for more information.

##### Attaching Behavior With Stimulus

New DOM elements can appear on the page at any time by way of frame navigation, stream messages, or client-side rendering operations, and these elements often need to be initialized as if they came from a fresh page load.

You can handle all of these updates, including updates from Turbo Drive page loads, in a single place with the conventions and lifecycle callbacks provided by Turbo's sister framework, [Stimulus](https://stimulus.hotwired.dev).

Stimulus lets you annotate your HTML with controller, action, and target attributes:

```html
<div data-controller="hello">
  <input data-hello-target="name" type="text">
  <button data-action="click->hello#greet">Greet</button>
</div>
```

Implement a compatible controller and Stimulus connects it automatically:

```js
// hello_controller.js
import { Controller } from "@hotwired/stimulus"

export default class extends Controller {
  greet() {
    console.log(`Hello, ${this.name}!`)
  }

  get name() {
    return this.targets.find("name").value
  }
}
```

Stimulus connects and disconnects these controllers and their associated event handlers whenever the document changes using the [MutationObserver](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver) API. As a result, it handles Turbo Drive page changes, Turbo Frames navigation, and Turbo Streams messages the same way it handles any other type of DOM update.

#### Making Transformations Idempotent

Often you’ll want to perform client-side transformations to HTML received from the server. For example, you might want to use the browser’s knowledge of the user’s current time zone to group a collection of elements by date.

Suppose you have annotated a set of elements with `data-timestamp` attributes indicating the elements’ creation times in UTC. You have a JavaScript function that queries the document for all such elements, converts the timestamps to local time, and inserts date headers before each element that occurs on a new day.

Consider what happens if you’ve configured this function to run on `turbo:load`. When you navigate to the page, your function inserts date headers. Navigate away, and Turbo Drive saves a copy of the transformed page to its cache. Now press the Back button—Turbo Drive restores the page, fires `turbo:load` again, and your function inserts a second set of date headers.

To avoid this problem, make your transformation function _idempotent_. An idempotent transformation is safe to apply multiple times without changing the result beyond its initial application.

One technique for making a transformation idempotent is to keep track of whether you’ve already performed it by setting a `data` attribute on each processed element. When Turbo Drive restores your page from cache, these attributes will still be present. Detect these attributes in your transformation function to determine which elements have already been processed.

A more robust technique is simply to detect the transformation itself. In the date grouping example above, that means checking for the presence of a date divider before inserting a new one. This approach gracefully handles newly inserted elements that weren’t processed by the original transformation.

#### Persisting Elements Across Page Loads

Turbo Drive allows you to mark certain elements as _permanent_. Permanent elements persist across page loads, so that any changes you make to those elements do not need to be reapplied after navigation.

Consider a Turbo Drive application with a shopping cart. At the top of each page is an icon with the number of items currently in the cart. This counter is updated dynamically with JavaScript as items are added and removed.

Now imagine a user who has navigated to several pages in this application. She adds an item to her cart, then presses the Back button in her browser. Upon navigation, Turbo Drive restores the previous page’s state from cache, and the cart item count erroneously changes from 1 to 0.

You can avoid this problem by marking the counter element as permanent. Designate permanent elements by giving them an HTML `id` and annotating them with `data-turbo-permanent`.

```html
<div id="cart-counter" data-turbo-permanent>1 item</div>
```

Before each render, Turbo Drive matches all permanent elements by ID and transfers them from the original page to the new page, preserving their data and event listeners.

## 08 Installing

### Installing Turbo in Your Application

Turbo can either be referenced in compiled form via the Turbo distributable script directly in the `<head>` of your application or through npm via a bundler like esbuild.

#### In Compiled Form

You can float on the latest release of Turbo using a CDN bundler like Skypack. See <a href="https://www.skypack.dev/view/@hotwired/turbo">https://www.skypack.dev/view/@hotwired/turbo</a> for more details. Or <a href="https://unpkg.com/browse/@hotwired/turbo@latest/dist/">download the compiled packages from unpkg</a>.

#### As An npm Package

You can install Turbo from npm via the `npm` or `yarn` packaging tools. Then require or import that in your code:

```javascript
import * as Turbo from "@hotwired/turbo"
```

#### In a Ruby on Rails application

The Turbo JavaScript framework is included with [the turbo-rails gem](https://github.com/hotwired/turbo-rails) for direct use with the asset pipeline.

# 05 Turbo Reference

## 01 Drive

### Drive

#### Turbo.visit

```js
Turbo.visit(location)
Turbo.visit(location, { action: action })
Turbo.visit(location, { frame: frame })
```

Performs an [Application Visit][] to the given _location_ (a string containing a URL or path) with the specified _action_ (a string, either `"advance"` or `"replace"`).

If _location_ is a cross-origin URL, or falls outside of the specified root (see [Setting a Root Location](#setting-a-root-location)), Turbo performs a full page load by setting `window.location`.

If _action_ is unspecified, Turbo Drive assumes a value of `"advance"`.

Before performing the visit, Turbo Drive fires a `turbo:before-visit` event on `document`. Your application can listen for this event and cancel the visit with `event.preventDefault()` (see [Canceling Visits Before They Start](#canceling-visits-before-they-start)).

If _frame_ is specified, find a `<turbo-frame>` element with an `[id]` attribute that matches the provided value, and navigate it to the provided _location_. If the `<turbo-frame>` cannot be found, perform a page-level [Application Visit][].

[Application Visit]: #application-visits
#### Turbo.cache.clear

```js
Turbo.cache.clear()
```

Removes all entries from the Turbo Drive page cache. Call this when state has changed on the server that may affect cached pages.

**Note:** This function was previously exposed as `Turbo.clearCache()`. The top-level function was deprecated in favor of the new `Turbo.cache.clear()` function.

#### Turbo.setProgressBarDelay

```js
Turbo.setProgressBarDelay(delayInMilliseconds)
```

Sets the delay after which the [progress bar](#displaying-progress) will appear during navigation, in milliseconds. The progress bar appears after 500ms by default.

Note that this method has no effect when used with the iOS or Android adapters.

#### Turbo.setConfirmMethod

```js
Turbo.setConfirmMethod(confirmMethod)
```

Sets the method that is called by links decorated with [`data-turbo-confirm`](#requiring-confirmation-for-a-visit). The default is the browser's built in `confirm`. The method should return `true` if the visit can proceed.

#### Turbo.session.drive

```js
Turbo.session.drive = false
```

Turns Turbo Drive off by default. You must now opt-in to Turbo Drive on a per-link and per-form basis using `data-turbo="true"`.

## 02 Frames

### Frames

#### Basic frame

Confines all navigation within the frame by expecting any followed link or form submission to return a response including a matching frame tag:

```html
<turbo-frame id="messages">
  <a href="/messages/expanded">
    Show all expanded messages in this frame.
  </a>

  <form action="/messages">
    Show response from this form within this frame.
  </form>
</turbo-frame>
```

#### Eager-loaded frame

Works like the basic frame, but the content is loaded from a remote `src` first.

```html
<turbo-frame id="messages" src="/messages">
  Content will be replaced when /messages has been loaded.
</turbo-frame>
```

#### Lazy-loaded frame

Like an eager-loaded frame, but the content is not loaded from `src` until the frame is visible.

```html
<turbo-frame id="messages" src="/messages" loading="lazy">
  Content will be replaced when the frame becomes visible and /messages has been loaded.
</turbo-frame>
```

#### Frame targeting the whole page by default

```html
<turbo-frame id="messages" target="_top">
  <a href="/messages/1">
    Following link will replace the whole page, not this frame.
  </a>

  <a href="/messages/1" data-turbo-frame="_self">
    Following link will replace just this frame.
  </a>

  <form action="/messages">
    Submitting form will replace the whole page, not this frame.
  </form>
</turbo-frame>
```

#### Frame with overwritten navigation targets

```html
<turbo-frame id="messages">
  <a href="/messages/1">
    Following link will replace this frame.
  </a>

  <a href="/messages/1" data-turbo-frame="_top">
    Following link will replace the whole page, not this frame.
  </a>

  <form action="/messages" data-turbo-frame="navigation">
    Submitting form will replace the navigation frame.
  </form>
</turbo-frame>
```

#### Frame that promotes navigations to Visits

```html
<turbo-frame id="messages" data-turbo-action="advance">
  <a href="/messages?page=2">Advance history to next page</a>
  <a href="/messages?page=2" data-turbo-action="replace">Replace history with next page</a>
</turbo-frame>
```

#### Frame that will get reloaded with morphing during page refreshes

```html
<turbo-frame id="my-frame" refresh="morph">
  ...
</turbo-frame>
```

### Attributes, properties, and functions

The `<turbo-frame>` element is a [custom element][] with its own set of HTML
attributes and JavaScript properties.

[custom element]: https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements
#### HTML Attributes

* `src` accepts a URL or path value that controls navigation
  of the element

* `loading` has two valid [enumerated][] values: "eager" and "lazy". When
  `loading="eager"`, changes to the `src` attribute will immediately navigate
  the element. When `loading="lazy"`, changes to the `src` attribute will defer
  navigation until the element is visible in the viewport. The default value is `eager`.

* `busy` is a [boolean attribute][] toggled to be present when a
  `<turbo-frame>`-initiated request starts, and toggled false when the request
  ends

* `disabled` is a [boolean attribute][] that prevents any navigation when
  present

* `target` refers to another `<turbo-frame>` element by ID to be navigated when
  a descendant `<a>` is clicked. When `target="_top"`, navigate the window.

* `complete` is a boolean attribute whose presence or absence indicates whether
  or not the `<turbo-frame>` element has finished navigating.

* `autoscroll` is a [boolean attribute][] that controls whether or not to scroll
  a `<turbo-frame>` element (and its descendant `<turbo-frame>` elements) into
  view when after loading. Control the scroll's vertical alignment by setting the
  `data-autoscroll-block` attribute to a valid [Element.scrollIntoView({ block:
  "..." })][Element.scrollIntoView] value: one of `"end"`, `"start"`, `"center"`,
  or `"nearest"`. When `data-autoscroll-block` is absent, the default value is
  `"end"`. Control the scroll's behavior by setting the
  `data-autoscroll-behavior` attribute to a valid [Element.scrollIntoView({
    behavior:
  "..." })][Element.scrollIntoView] value: one of `"auto"`, or `"smooth"`.
  When `data-autoscroll-behavior` is absent, the default value is `"auto"`.


[boolean attribute]: https://www.w3.org/TR/html52/infrastructure.html#sec-boolean-attributes
[enumerated]: https://www.w3.org/TR/html52/infrastructure.html#keywords-and-enumerated-attributes
[Element.scrollIntoView]: https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView#parameters
#### Properties

All `<turbo-frame>` elements can be controlled in JavaScript environments
through instances of the `FrameElement` class.

* `FrameElement.src` controls the pathname or URL to be loaded. Setting the `src` 
   property will immediately navigate the element. When `FrameElement.loaded` is 
   set to `"lazy"`, changes to the `src` property will defer navigation until the 
   element is visible in the viewport.

* `FrameElement.disabled` is a boolean property that controls whether or not the
  element will load

* `FrameElement.loading` controls the style (either `"eager"` or `"lazy"`) that
  the frame will loading its content.

* `FrameElement.loaded` references a [Promise][] instance that resolves once the
  `FrameElement`'s current navigation has completed.

* `FrameElement.complete` is a read-only boolean property set to `true` when the
  `FrameElement` has finished navigating and `false` otherwise.

* `FrameElement.autoscroll` controls whether or not to scroll the element into
  view once loaded

* `FrameElement.isActive` is a read-only boolean property that indicates whether
  or not the frame is loaded and ready to be interacted with

* `FrameElement.isPreview` is a read-only boolean property that returns `true`
  when the `document` that contains the element is a [preview][].

#### Functions

* `FrameElement.reload()` is a function that reloads the frame element from its `src`.

[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[preview]: https://turbo.hotwired.dev/handbook/building#detecting-when-a-preview-is-visible
## 03 Streams

### Streams

#### The eight actions

##### Append

Appends the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="append" target="dom_id">
  <template>
    Content to append to container designated with the dom_id.
  </template>
</turbo-stream>
```
If the template's first element has an id that is already used by a direct child inside the container targeted by dom_id, it is replaced instead of appended.

##### Prepend

Prepends the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="prepend" target="dom_id">
  <template>
    Content to prepend to container designated with the dom_id.
  </template>
</turbo-stream>
```
If the template's first element has an id that is already used by a direct child inside the container targeted by dom_id, it is replaced instead of prepended.

##### Replace

Replaces the element designated by the target dom id.

```html
<turbo-stream action="replace" target="dom_id">
  <template>
    Content to replace the element designated with the dom_id.
  </template>
</turbo-stream>
```

##### Update

Updates the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="update" target="dom_id">
  <template>
    Content to update to container designated with the dom_id.
  </template>
</turbo-stream>
```

##### Remove

Removes the element designated by the target dom id.

```html
<turbo-stream action="remove" target="dom_id">
</turbo-stream>
```

##### Before

Inserts the content within the template tag before the element designated by the target dom id.

```html
<turbo-stream action="before" target="dom_id">
  <template>
    Content to place before the element designated with the dom_id.
  </template>
</turbo-stream>
```

##### After

Inserts the content within the template tag after the element designated by the target dom id.

```html
<turbo-stream action="after" target="dom_id">
  <template>
    Content to place after the element designated with the dom_id.
  </template>
</turbo-stream>
```

##### Morph

Replaces the element designated by the target dom id via morph.

```html
<turbo-stream action="morph" target="dom_id">
  <template>
    Content to replace the element.
  </template>
</turbo-stream>
```

The `children-only` attribute can be added to the `turbo-stream` element to morph only the children of the element designated by the target dom id.

```html
<turbo-stream action="morph" target="dom_id" children-only>
  <template>
    Content to replace the element.
  </template>
</turbo-stream>
```

##### Refresh

Initiates a [Page Refresh](/handbook/page_refreshes) to render new content with
morphing.

```html
<!-- without `[request-id]` -->
<turbo-stream action="refresh"></turbo-stream>

<!-- debounced with `[request-id]` -->
<turbo-stream action="refresh" request-id="abcd-1234"></turbo-stream>
```

#### Targeting Multiple Elements

To target multiple elements with a single action, use the `targets` attribute with a CSS query selector instead of the `target` attribute.

```html
<turbo-stream action="remove" targets=".elementsWithClass">
</turbo-stream>

<turbo-stream action="after" targets=".elementsWithClass">
  <template>
    Content to place after the elements designated with the css query.
  </template>
</turbo-stream>
```

#### Processing Stream Elements

Turbo can connect to any form of stream to receive and process stream actions. A stream source must dispatch [MessageEvent](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent) messages that contain the stream action HTML in the `data` attribute of that event. It's then connected by `Turbo.session.connectStreamSource(source)` and disconnected via `Turbo.session.disconnectStreamSource(source)`. If you need to process stream actions from different source than something producing `MessageEvent`s, you can use `Turbo.renderStreamMessage(streamActionHTML)` to do so.

A good way to wrap all this together is by using a custom element, like turbo-rails does with [TurboCableStreamSourceElement](https://github.com/hotwired/turbo-rails/blob/main/app/javascript/turbo/cable_stream_source_element.js).

## 04 Events

### Events

Turbo emits a variety of [Custom Events][] types, dispatched from the following
sources:

* [Document](#document)
* [Page Refreshes](#page-refreshes)
* [Forms](#forms)
* [Frames](#frames)
* [Streams](#streams)
* [HTTP Requests](#http-requests)

When using jQuery, the data on the event must be accessed as `$event.originalEvent.detail`.

[Custom Events]: https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent
#### Document

Turbo Drive emits events that allow you to track the navigation life cycle and respond to page loading. Except where noted, the following events fire on the [document.documentElement][] object (i.e., the `<html>` element).

[document.documentElement]: https://developer.mozilla.org/en-US/docs/Web/API/Document/documentElement
##### `turbo:click`

Fires when you click a Turbo-enabled link. The clicked element is the [event.target][]. Access the requested location with `event.detail.url`. Cancel this event to let the click fall through to the browser as normal navigation.

| `event.detail` property   | Type              | Description
|---------------------------|-------------------|------------
| `url`                     | `string`          | the requested location
| `originalEvent`           | [MouseEvent][]    | the original [`click` event]

[`click` event]: https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event
[MouseEvent]: https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent
[event.target]: https://developer.mozilla.org/en-US/docs/Web/API/Event/target
##### `turbo:before-visit`

Fires before visiting a location, except when navigating by history. Access the requested location with `event.detail.url`. Cancel this event to prevent navigation.

| `event.detail` property   | Type              | Description
|---------------------------|-------------------|------------
| `url`                     | `string`          | the requested location

##### `turbo:visit`

Fires immediately after a visit starts. Access the requested location with `event.detail.url` and action with `event.detail.action`.

| `event.detail` property   | Type                                  | Description
|---------------------------|---------------------------------------|------------
| `url`                     | `string`                              | the requested location
| `action`                  | `"advance" \| "replace" \| "restore"` | the visit's [Action][]

[Action]: #page-navigation-basics
##### `turbo:before-cache`

Fires before Turbo saves the current page to cache.

Instances of `turbo:before-cache` events do not have an `event.detail` property.

##### `turbo:before-render`

Fires before rendering the page. Access the new `<body>` element with `event.detail.newBody`. Rendering can be canceled and continued with `event.detail.resume` (see [Pausing Rendering](#pausing-rendering)). Customize how Turbo Drive renders the response by overriding the `event.detail.render` function (see [Custom Rendering](#custom-rendering)).

| `event.detail` property   | Type                              | Description
|---------------------------|-----------------------------------|------------
| `renderMethod`            | `"replace" \| "morph"`            | the strategy that will be used to render the new content
| `newBody`                 | [HTMLBodyElement][]               | the new `<body>` element that will replace the document's current `<body>` element
| `isPreview`               | `boolean`                         | whether or not the render is a [preview][] of a cached page
| `resume`                  | `(value?: any) => void`           | called when [Pausing Requests][]
| `render`                  | `(currentBody, newBody) => void`  | override to [Customize Rendering](#custom-rendering)

[HTMLBodyElement]: https://developer.mozilla.org/en-US/docs/Web/API/HTMLBodyElement
[preview]: #understanding-caching
##### `turbo:render`

Fires after Turbo renders the page. This event fires twice during an application visit to a cached location: once after rendering the cached version, and again after rendering the fresh version.

| `event.detail` property   | Type                      | Description
|---------------------------|---------------------------|------------
| `renderMethod`            | `"replace" \| "morph"`    | the strategy used to render the new content
| `isPreview`               | `boolean`                 | whether or not the render is a [preview][] of a cached page

##### `turbo:load`

Fires once after the initial page load, and again after every Turbo visit.

| `event.detail` property   | Type      | Description
|---------------------------|-----------|------------
| `url`                     | `string`  | the requested location
| `timing.visitStart`       | `number`  | timestamp at the start of the Visit
| `timing.requestStart`     | `number`  | timestamp at the start of the HTTP request for the next page
| `timing.requestEnd`       | `number`  | timestamp at the end of the HTTP request for the next page
| `timing.visitEnd`         | `number`  | timestamp at the end of the Visit


#### Page Refreshes

Turbo Drive emits events while morphing the page's content.

##### `turbo:morph`

Fires after Turbo morphs the page.

| `event.detail` property   | Type        | Description
|---------------------------|-------------|------------
| `currentElement`          | [Element][] | the original [Element][] that remains connected after the morph (most commonly `document.body`)
| `newElement`              | [Element][] | the [Element][] with the new attributes and children that is not connected after the morph

##### `turbo:before-morph-element`

Fires before Turbo morphs an element. The [event.target][] references the original element that will remain connected to the document. Cancel this event by calling `event.preventDefault()` to skip morphing and preserve the original element, its attributes, and its children.

| `event.detail` property   | Type          | Description
|---------------------------|---------------|------------
| `newElement`              | [Element][]   | the [Element][] with the new attributes and children that is not connected after the morph

##### `turbo:before-morph-attribute`

Fires before Turbo morphs an element's attributes. The [event.target][] references the original element that will remain connected to the document. Cancel this event by calling `event.preventDefault()` to skip morphing and preserve the original attribute value.

| `event.detail` property   | Type                      | Description
|---------------------------|---------------------------|------------
| `attributeName`           | `string`                  | the name of the attribute to be mutated
| `mutationType`            | `"updated" \| "removed"`  | how the attribute will be mutated

##### `turbo:morph-element`

Fires after Turbo morphs an element. The [event.target][] references the morphed element that remains connected after the morph.

| `event.detail` property   | Type          | Description
|---------------------------|---------------|------------
| `newElement`              | [Element][]   | the [Element][] with the new attributes and children that is not connected after the morph

[Element]: https://developer.mozilla.org/en-US/docs/Web/API/Element
#### Forms

Turbo Drive emits events during submission, redirection, and submission failure. The following events fire on the `<form>` element during submission.

##### `turbo:submit-start`

Fires during a form submission. Access the `FormSubmission` object with `event.detail.formSubmission`. Abort form submission (e.g. after validation failure) with `event.detail.formSubmission.stop()`. Use `event.originalEvent.detail.formSubmission.stop()` if you're using jQuery.

| `event.detail` property   | Type                                      | Description
|---------------------------|-------------------------------------------|------------
| `formSubmission`          | `FormSubmission`                          | the `<form>` element submission

##### `turbo:submit-end`

Fires after the form submission-initiated network request completes. Access the `FormSubmission` object with `event.detail.formSubmission` along with `FormSubmissionResult` properties included within `event.detail`.

| `event.detail` property   | Type                      | Description
|---------------------------|---------------------------|------------
| `success`                 | `boolean`                 | a `boolean` representing the request's success
| `fetchResponse`           | `FetchResponse \| null`   | present when `success: true`, `null` when `success: false`
| `error`                   | [Error][] or `null`       | `null` when `success: true`, present when `success: false`

[Error]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors#### Frames

Turbo Frames emit events during their navigation life cycle. The following events fire on the `<turbo-frame>` element.

##### `turbo:before-frame-render`

Fires before rendering the `<turbo-frame>` element. Access the new `<turbo-frame>` element with `event.detail.newFrame`. Rendering can be canceled and continued with `event.detail.resume` (see [Pausing Rendering](#pausing-rendering)). Customize how Turbo Drive renders the response by overriding the `event.detail.render` function (see [Custom Rendering](#custom-rendering)).

| `event.detail` property   | Type                              | Description
|---------------------------|-----------------------------------|------------
| `newFrame`                | `FrameElement`                    | the new `<turbo-frame>` element that will replace the current `<turbo-frame>` element
| `resume`                  | `(value?: any) => void`           | called when [Pausing Requests][]
| `render`                  | `(currentFrame, newFrame) => void`| override to [Customize Rendering](#custom-rendering)

##### `turbo:frame-render`

Fires right after a `<turbo-frame>` element renders its view. The specific `<turbo-frame>` element is the [event.target][]. Access the `FetchResponse` object with `event.detail.fetchResponse` property.

| `event.detail` property   | Type                              | Description
|---------------------------|-----------------------------------|------------
| `fetchResponse`           | `FetchResponse`                   | the HTTP request's response

##### `turbo:frame-load`

Fires when a `<turbo-frame>` element is navigated and finishes loading (fires after `turbo:frame-render`). The specific `<turbo-frame>` element is the [event.target][].

Instances of `turbo:frame-load` events do not have an `event.detail` property.

##### `turbo:frame-missing`

Fires when the response to a `<turbo-frame>` element request does not contain a matching `<turbo-frame>` element. By default, Turbo writes an informational message into the frame and throws an exception. Cancel this event to override this handling. You can access the [Response][] instance with `event.detail.response`, and perform a visit by calling `event.detail.visit(location, visitOptions)` (see [Turbo.visit][] to learn more about `VisitOptions`).

| `event.detail` property   | Type                                                                  | Description
|---------------------------|-----------------------------------------------------------------------|------------
| `response`                | [Response][]                                                          | the HTTP response for the request initiated by a `<turbo-frame>` element
| `visit`                   | `async (location: string \| URL, visitOptions: VisitOptions) => void` | a convenience function to initiate a page-wide navigation

[Response]: https://developer.mozilla.org/en-US/docs/Web/API/Response
[Turbo.visit]: #turbo.visit
#### Streams

Turbo Streams emit events during their life cycle. The following events fire on the `<turbo-stream>` element.

##### `turbo:before-stream-render`

Fires before rendering a Turbo Stream page update. Access the new `<turbo-stream>` element with `event.detail.newStream`. Customize the element's behavior by overriding the `event.detail.render` function (see [Custom Actions][]).

| `event.detail` property   | Type                              | Description
|---------------------------|-----------------------------------|------------
| `newStream`               | `StreamElement`                   | the new `<body>` element that will replace the document's current `<body>` element
| `render`                  | `async (currentElement) => void`  | override to define [Custom Actions][]

[Custom Actions]: #custom-actions
#### HTTP Requests

Turbo emits events when fetching content over HTTP. Depending on the what
initiated the request, the events could fire on:

* a `<turbo-frame>` during its navigation
* a `<form>` during its submission
* the `<html>` element during a page-wide Turbo Visit

##### `turbo:before-fetch-request`

Fires before Turbo issues a network request (to fetch a page, submit a form, preload a link, etc.). Access the requested location with `event.detail.url` and the fetch options object with `event.detail.fetchOptions`. This event fires on the respective element (`<turbo-frame>` or `<form>` element) which triggers it and can be accessed with [event.target][] property. Request can be canceled and continued with `event.detail.resume` (see [Pausing Requests][]).

| `event.detail` property   | Type                              | Description
|---------------------------|-----------------------------------|------------
| `fetchOptions`            | [RequestInit][]                   | the `options` used to construct the [Request][]
| `url`                     | [URL][]                           | the request's location
| `resume`                  | `(value?: any) => void` callback  | called when [Pausing Requests][]

[RequestInit]: https://developer.mozilla.org/en-US/docs/Web/API/Request/Request#options
[Request]: https://developer.mozilla.org/en-US/docs/Web/API/Request/Request
[URL]: https://developer.mozilla.org/en-US/docs/Web/API/URLm
[Pausing Requests]: #pausing-requests
##### `turbo:before-fetch-response`

Fires after the network request completes. Access the fetch options object with `event.detail`. This event fires on the respective element (`<turbo-frame>` or `<form>` element) which triggers it and can be accessed with [event.target][] property.

| `event.detail` property   | Type                      | Description
|---------------------------|---------------------------|------------
| `fetchResponse`           | `FetchResponse`           | the HTTP request's response

##### `turbo:before-prefetch`

Fires before Turbo prefetches a link. The link is the `event.target`. Cancel this event to prevent prefetching.

##### `turbo:fetch-request-error`

Fires when a form or frame fetch request fails due to network errors. This event fires on the respective element (`<turbo-frame>` or `<form>` element) which triggers it and can be accessed with [event.target][] property. This event can be canceled.

| `event.detail` property   | Type              | Description
|---------------------------|-------------------|------------
| `request`                 | `FetchRequest`    | The HTTP request that failed
| `error`                   | [Error][]         | provides the cause of the failure

[Error]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors

## 05 Attributes

### Attributes and Meta Tags

#### Data Attributes

The following data attributes can be applied to elements to customize Turbo's behaviour.

* `data-turbo="false"` disables Turbo Drive on links and forms including descendants. To reenable when an ancestor has opted out, use `data-turbo="true"`. Be careful: when Turbo Drive is disabled, browsers treat link clicks as normal, but [native adapters](/handbook/native) may exit the app.
* `data-turbo-track="reload"` tracks the element's HTML and performs a full page reload when it changes. Typically used to [keep `script` and CSS `link` elements up-to-date](#reloading-when-assets-change).
* `data-turbo-frame` identifies the Turbo Frame to navigate. Refer to the [Frames documentation](/reference/frames) for further details.
* `data-turbo-preload` signals to [Drive](#preload-links-into-the-cache) to pre-fetch the next page's content
* `data-turbo-action` customizes the [Visit](#page-navigation-basics) action. Valid values are `replace` or `advance`. Can also be used with Turbo Frames to [promote frame navigations to page visits](#promoting-a-frame-navigation-to-a-page-visit).
* `data-turbo-permanent` [persists the element between page loads](#persisting-elements-across-page-loads). The element must have a unique `id` attribute. It also serves to exclude elements from being morphed when using [page refreshes with morphing](/handbook/page_refreshes.html)
* `data-turbo-temporary` removes the element before the document is cached, preventing it from reappearing when restored.
* `data-turbo-eval="false"` prevents inline `script` elements from being re-evaluated on Visits.
* `data-turbo-method` changes the link request type from the default `GET`. Ideally, non-`GET` requests should be triggered with forms, but `data-turbo-method` might be useful where a form is not possible.
* `data-turbo-stream` specifies that a link or form can accept a Turbo Streams response. Turbo [automatically requests stream responses](#streaming-from-http-responses) for form submissions with non-`GET` methods; `data-turbo-stream` allows Turbo Streams to be used with `GET` requests as well.
* `data-turbo-confirm` presents a confirm dialog with the given value. Can be used on `form` elements or links with `data-turbo-method`.
* `data-turbo-submits-with` specifies text to display when submitting a form. Can be used on `input` or `button` elements. While the form is submitting the text of the element will show the value of `data-turbo-submits-with`. After the submission, the original text will be restored. Useful for giving user feedback by showing a message like "Saving..." while an operation is in progress.

#### Automatically Added Attributes

The following attributes are automatically added by Turbo and are useful to determine the Visit state at a given moment.

* `disabled` is added to the form submitter while the form request is in progress, to prevent repeat submissions.
* `data-turbo-preview` is added to the `html` element when displaying a [preview](#detecting-when-a-preview-is-visible) during a Visit.
* `data-turbo-visit-direction` is added to the `html` element during a visit, with a value of `forward` or `back` or `none`, to indicate its direction.
* `aria-busy` is added to `html` and `turbo-frame` elements when a navigation is in progress.

#### Meta Tags

The following `meta` elements, added to the `head`, can be used to customize caching and Visit behavior.

* `<meta name="turbo-cache-control">` to [opt out of caching](#opting-out-of-caching).
* `<meta name="turbo-visit-control" content="reload">` will perform a full page reload whenever Turbo navigates to the page, including when the request originates from a `<turbo-frame>`.
* `<meta name="turbo-root">` to [scope Turbo Drive to a particular root location](#setting-a-root-location).
* `<meta name="view-transition" content="same-origin">` to trigger view transitions on browsers that support the [View Transition API](https://caniuse.com/view-transitions).
* `<meta name="turbo-refresh-method" content="morph">` will configure [page refreshes with morphing](/handbook/page_refreshes.html).
* `<meta name="turbo-refresh-scroll" content="preserve">` will enable [scroll preservation during page refreshes](/handbook/page_refreshes.html).

# 06 Turbo Docs

## 01 Turbo Drive Helper

Module: Turbo::DriveHelper
==========================

Defined in:

app/helpers/turbo/drive_helper.rb

Overview
--------

Helpers to configure Turbo Drive via meta directives. They come in two variants:

The recommended option is to include `yield :head` in the `<head>` section of the layout. Then you can use the helpers in any view.

###### Example

```
### app/views/application.html.erb
<html><head><%= yield :head %></head><body><%= yield %></html>

### app/views/trays/index.html.erb
<% turbo_exempts_page_from_cache %>
<p>Page that shouldn't be cached by Turbo</p>

```

Alternatively, you can use the `_tag` variant of the helpers to only get the HTML for the meta directive.

Instance Method Details
-----------------------

##### **turbo_exempts_page_from_cache** ⇒ `Object`

Pages that are more likely than not to be a cache miss can skip turbo cache to avoid visual jitter. Cannot be used along with `turbo_exempts_page_from_preview`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L21)]

##### **turbo_exempts_page_from_cache_tag** ⇒ `Object`

See `turbo_exempts_page_from_cache`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L26)]

##### **turbo_exempts_page_from_preview** ⇒ `Object`

Specify that a cached version of the page should not be shown as a preview during an application visit. Cannot be used along with `turbo_exempts_page_from_cache`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L32)]

##### **turbo_exempts_page_from_preview_tag** ⇒ `Object`

See `turbo_exempts_page_from_preview`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L37)]

##### **turbo_page_requires_reload** ⇒ `Object`

Force the page, when loaded by Turbo, to be cause a full page reload.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L42)]

##### **turbo_page_requires_reload_tag** ⇒ `Object`

See `turbo_page_requires_reload`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L47)]

##### **turbo_refresh_method_tag**(method = :replace) ⇒ `Object`

Configure method to perform page refreshes. See `turbo_refreshes_with`.

Raises:

-   (`ArgumentError`)

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L76)]

##### **turbo_refresh_scroll_tag**(scroll = :reset) ⇒ `Object`

Configure scroll strategy for page refreshes. See `turbo_refreshes_with`.

Raises:

-   (`ArgumentError`)

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L82)]

##### **turbo_refreshes_with**(method: :replace, scroll: :reset) ⇒ `Object`

Configure how to handle page refreshes. A page refresh happens when Turbo loads the current page again with a **replace** visit:

##### Parameters:

-   `method` - Method to update the `<body>` of the page during a page refresh. It can be one of:

    -   `replace:`: Replaces the existing `<body>` with the new one. This is the

    default behavior.

    -   `morph:`: Morphs the existing `<body>` into the new one.

-   `scroll` - Controls the scroll behavior when a page refresh happens. It can be one of:

    -   `reset:`: Resets scroll to the top, left corner. This is the default.

    -   `preserve:`: Keeps the scroll.

##### Example Usage:

```
turbo_refreshes_with(method: :morph, scroll: :preserve)

```
## 02 Turbo Frames Helper

Module: Turbo::FramesHelper
===========================

Defined in:

app/helpers/turbo/frames_helper.rb

Instance Method Details
-----------------------

##### **turbo_frame_tag**(*ids, src: nil, target: nil, **attributes, &block) ⇒ `Object`

Returns a frame tag that can either be used simply to encapsulate frame content or as a lazy-loading container that starts empty but fetches the URL supplied in the `src` attribute.

###### Examples

```
<%= turbo_frame_tag "tray", src: tray_path(tray) %>
### => <turbo-frame id="tray" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag tray, src: tray_path(tray) %>
### => <turbo-frame id="tray_1" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag "tray", src: tray_path(tray), target: "_top" %>
### => <turbo-frame id="tray" target="_top" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag "tray", target: "other_tray" %>
### => <turbo-frame id="tray" target="other_tray"></turbo-frame>

<%= turbo_frame_tag "tray", src: tray_path(tray), loading: "lazy" %>
### => <turbo-frame id="tray" src="http://example.com/trays/1" loading="lazy"></turbo-frame>

<%= turbo_frame_tag "tray" do %>
  <div>My tray frame!</div>
<% end %>
### => <turbo-frame id="tray"><div>My tray frame!</div></turbo-frame>

<%= turbo_frame_tag [user_id, "tray"], src: tray_path(tray) %>
### => <turbo-frame id="1_tray" src="http://example.com/trays/1"></turbo-frame>

```

The `turbo_frame_tag` helper will convert the arguments it receives to their `dom_id` if applicable to easily generate unique ids for Turbo Frames:

```
<%= turbo_frame_tag(Article.find(1)) %>
### => <turbo-frame id="article_1"></turbo-frame>

<%= turbo_frame_tag(Article.find(1), "comments") %>
### => <turbo-frame id="comments_article_1"></turbo-frame>

```
## 03 Turbo Streams Helper

Module: Turbo::StreamsHelper
============================

Defined in:

app/helpers/turbo/streams_helper.rb

Instance Method Details
-----------------------

##### **turbo_stream** ⇒ `Object`

Returns a new `Turbo::Streams::TagBuilder` object that accepts stream actions and renders them as the template tags needed to send across the wire. This object is automatically yielded to turbo_stream.erb templates.

When responding to HTTP requests, controllers can declare 'turbo_stream` format response templates in that same style as `html` and `json` response formats. For example, consider a `MessagesController` that responds to both `text/html` and `text/vnd.turbo-stream.html` requests along with a `.turbo_stream.erb` action template:

```
def create
  @message = Message.create!(params.require(:message).permit(:content))
  respond_to do |format|
    format.turbo_stream
    format.html { redirect_to messages_url }
  end
end

<%# app/views/messages/create.turbo_stream.erb %>
<%= turbo_stream.append "messages", @message %>

<%= turbo_stream.replace "new_message" do %>
  <%= render partial: "new_message", locals: { room: @room } %>
<% end %>

```

When a 'app/views/messages/create.turbo_stream.erb` template exists, the `MessagesController#create` will respond to `text/vnd.turbo-stream.html` requests by rendering the `messages/create.turbo_stream.erb` view template and transmitting the response

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/StreamsHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/streams_helper.rb#L27)]

##### **turbo_stream_from**(*streamables, **attributes) ⇒ `Object`

Used in the view to create a subscription to a stream identified by the `streamables` running over the `Turbo::StreamsChannel`. The stream name being generated is safe to embed in the HTML sent to a user without fear of tampering, as it is signed using `Turbo.signed_stream_verifier`. Example:

```
### app/views/entries/index.html.erb
<%= turbo_stream_from Current.account, :entries %>
<div id="entries">New entries will be appended to this target</div>

```

The example above will process all turbo streams sent to a stream name like `account:5:entries` (when Current.account.id = 5). Updates to this stream can be sent like `entry.broadcast_append_to entry.account, :entries, target: "entries"`.

Custom channel class name can be passed using `:channel` option (either as a String or a class name):

```
<%= turbo_stream_from "room", channel: RoomChannel %>

```

It is also possible to pass additional parameters to the channel by passing them through 'data` attributes:

```
<%= turbo_stream_from "room", channel: RoomChannel, data: {room_name: "room #1"} %>

```
## 04 Turbo Broadcastable

Module: Turbo::Broadcastable
============================

Extended by:

ActiveSupport::Concern

Defined in:

app/models/concerns/turbo/broadcastable.rb [more...](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)

Overview
--------

This approach is an alternative to fine-grained stream actions targeting specific DOM elements. It offers good fidelity with a much simpler programming model. As a tradeoff, the fidelity you can reach is often not as high as with targeted stream actions since it renders the entire page again.

The `broadcast_refreshes` class method configures the model to broadcast a "page refresh" on creates, updates, and destroys to a stream name derived at runtime by the `stream` symbol invocation. Examples

```
class Board < ApplicationRecord
  broadcast_refreshes
end

```

In this example, when a board is created, updated, or destroyed, a Turbo Stream for a page refresh will be broadcasted to all clients subscribed to the "boards" stream.

This works great in hierarchical structures, where the child record touches parent records automatically to invalidate the cache:

```
class Column < ApplicationRecord
  belongs_to :board, touch: true # +Board+ will trigger a page refresh on column changes
end

```

You can also specify the streamable declaratively by passing a symbol to the `broadcast_refreshes_to` method:

```
class Column < ApplicationRecord
  belongs_to :board
  broadcast_refreshes_to :board
end

```

For more granular control, you can also broadcast a "page refresh" to a stream name derived from the passed `streamables` by using the instance-level methods `broadcast_refresh_to` or `broadcast_refresh_later_to`. These methods are particularly useful when you want to trigger a page refresh for more specific scenarios. Example:

```
class Clearance < ApplicationRecord
  belongs_to :petitioner, class_name: "Contact"
  belongs_to :examiner,   class_name: "User"

  after_create_commit :broadcast_refresh_later

  private
    def broadcast_refresh_later
      broadcast_refresh_later_to examiner.identity, :clearances
    end
end

```

In this example, a "page refresh" is broadcast to the stream named "identity:<identity-id>:clearances" after a new clearance is created. All clients subscribed to this stream will refresh the page to reflect the changes.

When broadcasting page refreshes, Turbo will automatically debounce multiple calls in a row to only broadcast the last one. This is meant for scenarios where you process records in mass. Because of the nature of such signals, it makes no sense to broadcast them repeatedly and individually.

Suppressing broadcasts
----------------------

Sometimes, you need to disable broadcasts in certain scenarios. You can use `.suppressing_turbo_broadcasts` to create execution contexts where broadcasts are disabled:

```
class Message < ApplicationRecord
  after_create_commit :update_message

  private
    def update_message
      broadcast_replace_to(user, :message, target: "message", renderable: MessageComponent.new)
    end
end

Message.suppressing_turbo_broadcasts do
  Message.create!(board: board) # This won't broadcast the replace action
end

```

Defined Under Namespace
-----------------------

**Modules:** [ClassMethods](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable/ClassMethods "Turbo::Broadcastable::ClassMethods (module)"), [TestHelper](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable/TestHelper "Turbo::Broadcastable::TestHelper (module)")


Instance Method Details
-----------------------

##### **broadcast_action**(action, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `#broadcast_action_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L388)]

##### **broadcast_action_later**(action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `#broadcast_action_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L448)]

####T urbo%2FBroadcastable:broadcast_action_later_to) #**broadcast_action_later_to**(*streamables, action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `broadcast_action_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L443)]

##### **broadcast_action_to**(*streamables, action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Broadcast a named `action`, allowing for dynamic dispatch, instead of using the concrete action methods. Examples:

```
### Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_action_to examiner.identity, :clearances, action: :prepend, target: "clearances"

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L383)]

##### **broadcast_after_to**(*streamables, target:, **rendering) ⇒ `Object`

Insert a rendering of this broadcastable model after the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="after" target="clearance_5"><template><div id="clearance_6">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_after_to examiner.identity, :clearances, target: "clearance_5"

### Sends <turbo-stream action="after" target="clearance_5"><template><div id="clearance_6">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_after_to examiner.identity, :clearances, target: "clearance_5",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L319)]

##### **broadcast_append**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_append_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L340)]

##### **broadcast_append_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_append_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L418)]

####T urbo%2FBroadcastable:broadcast_append_later_to) #**broadcast_append_later_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_append_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L413)]

##### **broadcast_append_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Append a rendering of this broadcastable model to the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="append" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_append_to examiner.identity, :clearances, target: "clearances"

### Sends <turbo-stream action="append" target="clearances"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_append_to examiner.identity, :clearances, target: "clearances",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L335)]

##### **broadcast_before_to**(*streamables, target:, **rendering) ⇒ `Object`

Insert a rendering of this broadcastable model before the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="before" target="clearance_5"><template><div id="clearance_4">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_before_to examiner.identity, :clearances, target: "clearance_5"

### Sends <turbo-stream action="before" target="clearance_5"><template><div id="clearance_4">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_before_to examiner.identity, :clearances, target: "clearance_5",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L303)]

##### **broadcast_morph**(**rendering) ⇒ `Object`

Same as `broadcast_morph_to` but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L503)]

##### **broadcast_morph_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_morph_later_to` but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L513)]

####T urbo%2FBroadcastable:broadcast_morph_later_to) #**broadcast_morph_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_morph_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L508)]

##### **broadcast_morph_to**(*streamables, **rendering) ⇒ `Object`

Broadcast a morph action to the stream name identified by the passed `streamables`. Example: sends <turbo-stream action="morph" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream> to the stream named "identity:2:clearances" clearance.broadcast_morph_to examiner.identity, :clearances

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L498)]

##### **broadcast_prepend**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_prepend_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L361)]

##### **broadcast_prepend_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_prepend_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L428)]

####T urbo%2FBroadcastable:broadcast_prepend_later_to) #**broadcast_prepend_later_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_prepend_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L423)]

##### **broadcast_prepend_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Prepend a rendering of this broadcastable model to the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_prepend_to examiner.identity, :clearances, target: "clearances"

### Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_prepend_to examiner.identity, :clearances, target: "clearances",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L356)]

##### **broadcast_refresh** ⇒ `Object`

Same as `#broadcast_refresh_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L374)]

##### **broadcast_refresh_later** ⇒ `Object`

Same as `#broadcast_refresh_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L438)]

####T urbo%2FBroadcastable:broadcast_refresh_later_to) #**broadcast_refresh_later_to**(*streamables) ⇒ `Object`

Same as `broadcast_refresh_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L433)]

##### **broadcast_refresh_to**(*streamables) ⇒ `Object`

Broadcast a "page refresh" to the stream name identified by the passed `streamables`. Example:

```
### Sends <turbo-stream action="refresh"></turbo-stream> to the stream named "identity:2:clearances"
clearance.broadcast_refresh_to examiner.identity, :clearances

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L369)]

##### **broadcast_remove** ⇒ `Object`

Same as `#broadcast_remove_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L249)]

##### **broadcast_remove_to**(*streamables, target: self) ⇒ `Object`

Remove this broadcastable model from the dom for subscribers of the stream name identified by the passed streamables. Example:

```
### Sends <turbo-stream action="remove" target="clearance_5"></turbo-stream> to the stream named "identity:2:clearances"
clearance.broadcast_remove_to examiner.identity, :clearances

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L244)]

##### **broadcast_render**(**rendering) ⇒ `Object`

Render a turbo stream template with this broadcastable model passed as the local variable. Example:

```
### Template: entries/_entry.turbo_stream.erb
<%= turbo_stream.remove entry %>

<%= turbo_stream.append "entries", entry if entry.active? %>

```

Sends:

```
<turbo-stream action="remove" target="entry_5"></turbo-stream>
<turbo-stream action="append" target="entries"><template><div id="entry_5">My Entry</div></template></turbo-stream>

```

...to the stream named "entry:5".

Note that rendering inline via this method will cause template rendering to happen synchronously. That is usually not desireable for model callbacks, certainly not if those callbacks are inside of a transaction. Most of the time you should be using `broadcast_render_later`, unless you specifically know why synchronous rendering is needed.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L469)]

##### **broadcast_render_later**(**rendering) ⇒ `Object`

Same as `broadcast_render_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L484)]

####T urbo%2FBroadcastable:broadcast_render_later_to) #**broadcast_render_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_render_later` but run with the added option of naming the stream using the passed `streamables`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L490)]

##### **broadcast_render_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_render` but run with the added option of naming the stream using the passed `streamables`.

Note that rendering inline via this method will cause template rendering to happen synchronously. That is usually not desireable for model callbacks, certainly not if those callbacks are inside of a transaction. Most of the time you should be using `broadcast_render_later_to`, unless you specifically know why synchronous rendering is needed.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L479)]

##### **broadcast_replace**(**rendering) ⇒ `Object`

Same as `#broadcast_replace_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L268)]

##### **broadcast_replace_later**(**rendering) ⇒ `Object`

Same as `#broadcast_replace_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L398)]

####T urbo%2FBroadcastable:broadcast_replace_later_to) #**broadcast_replace_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_replace_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L393)]

##### **broadcast_replace_to**(*streamables, **rendering) ⇒ `Object`

Replace this broadcastable model in the dom for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="replace" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_replace_to examiner.identity, :clearances

### Sends <turbo-stream action="replace" target="clearance_5"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_replace_to examiner.identity, :clearances, partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L263)]

##### **broadcast_update**(**rendering) ⇒ `Object`

Same as `#broadcast_update_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L287)]

##### **broadcast_update_later**(**rendering) ⇒ `Object`

Same as `#broadcast_update_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L408)]

####T urbo%2FBroadcastable:broadcast_update_later_to) #**broadcast_update_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_update_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L403)]

##### **broadcast_update_to**(*streamables, **rendering) ⇒ `Object`

Update this broadcastable model in the dom for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
### Sends <turbo-stream action="update" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_update_to examiner.identity, :clearances

### Sends <turbo-stream action="update" target="clearance_5"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
### to the stream named "identity:2:clearances"
clearance.broadcast_update_to examiner.identity, :clearances, partial: "clearances/other_partial", locals: { a: 1 }
```
## 05 Turbo Streams Channel

Class: Turbo::StreamsChannel
============================

Inherits:

ActionCable::Channel::Base [show all](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/StreamsChannel#)

Extended by:

Turbo::Streams::Broadcasts, Turbo::Streams::StreamName

Includes:

Turbo::Streams::StreamName::ClassMethods

Defined in:

app/channels/turbo/streams_channel.rb

Overview
--------

The streams channel delivers all the turbo-stream actions created (primarily) through `Turbo::Broadcastable`. A subscription to this channel is made for each individual stream that one wishes to listen for updates to. The subscription relies on being passed a `signed_stream_name` parameter generated by turning a set of streamables into signed stream name using `Turbo::Streams::StreamName#signed_stream_name`. This is automatically done using the view helper `Turbo::StreamsHelper#turbo_stream_from(*streamables)`. If the signed stream name cannot be verified, the subscription is rejected.

In case if custom behavior is desired, one can create their own channel and re-use some of the primitives from helper modules like `Turbo::Streams::StreamName`:

```
 class CustomChannel < ActionCable::Channel::Base
    extend Turbo::Streams::Broadcasts, Turbo::Streams::StreamName
    include Turbo::Streams::StreamName::ClassMethods

    def subscribed
      if (stream_name = verified_stream_name_from_params).present? &&
         subscription_allowed?
        stream_from stream_name
      else
        reject
      end
    end

    def subscription_allowed?
       # ...
    end
 end

This channel can be connected to a web page using <tt>:channel</tt> option in
<tt>turbo_stream_from</tt> helper:

  <%= turbo_stream_from 'room', channel: CustomChannel %>
```


Instance Method Details
-----------------------

##### **subscribed** ⇒ `Object`
## 06 Turbo Native Navigation

Module: Turbo::Native::Navigation
=================================

Extended by:

ActiveSupport::Concern

Defined in:

app/controllers/turbo/native/navigation.rb

Overview
--------

Turbo is built to work with native navigation principles and present those alongside what's required for the web. When you have Turbo Native clients running (see the Turbo iOS and Turbo Android projects for details), you can respond to native requests with three dedicated responses: `recede`, `resume`, `refresh`.

turbo-android handles these actions automatically. You are required to implement the handling on your own for turbo-ios.

Instance Method Details
-----------------------

##### **recede_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `recede_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L34)]

##### **recede_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to dismiss a modal (if presented) or pop a screen off of the navigation stack. Otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L19)]

##### **refresh_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `refresh_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L44)]

##### **refresh_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to refresh the current screen, otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L29)]

##### **resume_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `resume_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L39)]

##### **resume_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to ignore this navigation, otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L24)]

##### **turbo_native_app?** ⇒ `Boolean`

Turbo Native applications are identified by having the string "Turbo Native" as part of their user agent.

Returns:

-   (`Boolean`)
## 07 Turbo Test Assertions

Module: Turbo::TestAssertions
=============================

Extended by:

ActiveSupport::Concern

Defined in:

lib/turbo/test_assertions.rb [more...](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/TestAssertions#)

Defined Under Namespace
-----------------------

**Modules:** [IntegrationTestAssertions](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/TestAssertions/IntegrationTestAssertions "Turbo::TestAssertions::IntegrationTestAssertions (module)")


Instance Method Details
-----------------------

##### **assert_no_turbo_stream**(action:, target: nil, targets: nil) ⇒ `Object`

Assert that the rendered fragment of HTML does not contain a '<turbo-stream>` element.

###### Options

-   `:action` [String] matches the element's `[action]` attribute

-   `:target` [String, #to_key] matches the element's `[target]` attribute. If the value responds to `#to_key`, the value will be transformed by calling `dom_id`

-   `:targets` [String] matches the element's `[targets]` attribute

    Given the following HTML fragment:

    ```
    <turbo-stream action="remove" target="message_1"></turbo-stream>
    ```

    The following assertion would fail:

    ```
    assert_no_turbo_stream action: "remove", target: "message_1"
    ```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/TestAssertions#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/lib/turbo/test_assertions.rb#L76)]

##### **assert_turbo_stream**(action:, target: nil, targets: nil, count: 1, &block) ⇒ `Object`

Assert that the rendered fragment of HTML contains a '<turbo-stream>` element.

###### Options

-   `:action` [String] matches the element's `[action]` attribute

-   `:target` [String, #to_key] matches the element's `[target]` attribute. If the value responds to `#to_key`, the value will be transformed by calling `dom_id`

-   `:targets` [String] matches the element's `[targets]` attribute

-   `:count` [Integer] indicates how many turbo streams are expected. Defaults to `1`.

    Given the following HTML fragment:

    ```
    <turbo-stream action="remove" target="message_1"></turbo-stream>
    ```

    The following assertion would pass:

    ```
    assert_turbo_stream action: "remove", target: "message_1"
    ```

You can also pass a block make assertions about the contents of the element. Given the following HTML fragment:

```
  <turbo-stream action="replace" target="message_1">
    <template>
      <p>Hello!</p>
    <template>
  </turbo-stream>

The following assertion would pass:

  assert_turbo_stream action: "replace", target: "message_1" do
    assert_select "template p", text: "Hello!"
  end
```