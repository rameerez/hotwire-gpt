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

### **recede_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `recede_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L34)]

### **recede_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to dismiss a modal (if presented) or pop a screen off of the navigation stack. Otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L19)]

### **refresh_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `refresh_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L44)]

### **refresh_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to refresh the current screen, otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L29)]

### **resume_or_redirect_back_or_to**(url, **options) ⇒ `Object`

Same as `resume_or_redirect_to` but redirects to the previous page or provided fallback location if the Turbo Native app is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L39)]

### **resume_or_redirect_to**(url, **options) ⇒ `Object`

Tell the Turbo Native app to ignore this navigation, otherwise redirect to the given URL if Turbo Native is not present.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Native/Navigation#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/controllers/turbo/native/navigation.rb#L24)]

### **turbo_native_app?** ⇒ `Boolean`

Turbo Native applications are identified by having the string "Turbo Native" as part of their user agent.

Returns:

-   (`Boolean`)