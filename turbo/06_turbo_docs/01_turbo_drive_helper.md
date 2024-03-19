Module: Turbo::DriveHelper
==========================

Defined in:

app/helpers/turbo/drive_helper.rb

Overview
--------

Helpers to configure Turbo Drive via meta directives. They come in two variants:

The recommended option is to include `yield :head` in the `<head>` section of the layout. Then you can use the helpers in any view.

#### Example

```
# app/views/application.html.erb
<html><head><%= yield :head %></head><body><%= yield %></html>

# app/views/trays/index.html.erb
<% turbo_exempts_page_from_cache %>
<p>Page that shouldn't be cached by Turbo</p>

```

Alternatively, you can use the `_tag` variant of the helpers to only get the HTML for the meta directive.

Instance Method Details
-----------------------

### **turbo_exempts_page_from_cache** ⇒ `Object`

Pages that are more likely than not to be a cache miss can skip turbo cache to avoid visual jitter. Cannot be used along with `turbo_exempts_page_from_preview`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L21)]

### **turbo_exempts_page_from_cache_tag** ⇒ `Object`

See `turbo_exempts_page_from_cache`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L26)]

### **turbo_exempts_page_from_preview** ⇒ `Object`

Specify that a cached version of the page should not be shown as a preview during an application visit. Cannot be used along with `turbo_exempts_page_from_cache`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L32)]

### **turbo_exempts_page_from_preview_tag** ⇒ `Object`

See `turbo_exempts_page_from_preview`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L37)]

### **turbo_page_requires_reload** ⇒ `Object`

Force the page, when loaded by Turbo, to be cause a full page reload.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L42)]

### **turbo_page_requires_reload_tag** ⇒ `Object`

See `turbo_page_requires_reload`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L47)]

### **turbo_refresh_method_tag**(method = :replace) ⇒ `Object`

Configure method to perform page refreshes. See `turbo_refreshes_with`.

Raises:

-   (`ArgumentError`)

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L76)]

### **turbo_refresh_scroll_tag**(scroll = :reset) ⇒ `Object`

Configure scroll strategy for page refreshes. See `turbo_refreshes_with`.

Raises:

-   (`ArgumentError`)

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/DriveHelper#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/helpers/turbo/drive_helper.rb#L82)]

### **turbo_refreshes_with**(method: :replace, scroll: :reset) ⇒ `Object`

Configure how to handle page refreshes. A page refresh happens when Turbo loads the current page again with a **replace** visit:

### Parameters:

-   `method` - Method to update the `<body>` of the page during a page refresh. It can be one of:

    -   `replace:`: Replaces the existing `<body>` with the new one. This is the

    default behavior.

    -   `morph:`: Morphs the existing `<body>` into the new one.

-   `scroll` - Controls the scroll behavior when a page refresh happens. It can be one of:

    -   `reset:`: Resets scroll to the top, left corner. This is the default.

    -   `preserve:`: Keeps the scroll.

### Example Usage:

```
turbo_refreshes_with(method: :morph, scroll: :preserve)

```