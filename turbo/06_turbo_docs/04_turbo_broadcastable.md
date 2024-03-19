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

### **broadcast_action**(action, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `#broadcast_action_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L388)]

### **broadcast_action_later**(action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `#broadcast_action_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L448)]

##T urbo%2FBroadcastable:broadcast_action_later_to) #**broadcast_action_later_to**(*streamables, action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Same as `broadcast_action_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L443)]

### **broadcast_action_to**(*streamables, action:, target: broadcast_target_default, attributes: {}, **rendering) ⇒ `Object`

Broadcast a named `action`, allowing for dynamic dispatch, instead of using the concrete action methods. Examples:

```
# Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_action_to examiner.identity, :clearances, action: :prepend, target: "clearances"

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L383)]

### **broadcast_after_to**(*streamables, target:, **rendering) ⇒ `Object`

Insert a rendering of this broadcastable model after the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="after" target="clearance_5"><template><div id="clearance_6">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_after_to examiner.identity, :clearances, target: "clearance_5"

# Sends <turbo-stream action="after" target="clearance_5"><template><div id="clearance_6">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_after_to examiner.identity, :clearances, target: "clearance_5",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L319)]

### **broadcast_append**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_append_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L340)]

### **broadcast_append_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_append_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L418)]

##T urbo%2FBroadcastable:broadcast_append_later_to) #**broadcast_append_later_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_append_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L413)]

### **broadcast_append_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Append a rendering of this broadcastable model to the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="append" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_append_to examiner.identity, :clearances, target: "clearances"

# Sends <turbo-stream action="append" target="clearances"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_append_to examiner.identity, :clearances, target: "clearances",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L335)]

### **broadcast_before_to**(*streamables, target:, **rendering) ⇒ `Object`

Insert a rendering of this broadcastable model before the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="before" target="clearance_5"><template><div id="clearance_4">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_before_to examiner.identity, :clearances, target: "clearance_5"

# Sends <turbo-stream action="before" target="clearance_5"><template><div id="clearance_4">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_before_to examiner.identity, :clearances, target: "clearance_5",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L303)]

### **broadcast_morph**(**rendering) ⇒ `Object`

Same as `broadcast_morph_to` but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L503)]

### **broadcast_morph_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_morph_later_to` but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L513)]

##T urbo%2FBroadcastable:broadcast_morph_later_to) #**broadcast_morph_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_morph_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L508)]

### **broadcast_morph_to**(*streamables, **rendering) ⇒ `Object`

Broadcast a morph action to the stream name identified by the passed `streamables`. Example: sends <turbo-stream action="morph" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream> to the stream named "identity:2:clearances" clearance.broadcast_morph_to examiner.identity, :clearances

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L498)]

### **broadcast_prepend**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_prepend_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L361)]

### **broadcast_prepend_later**(target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `#broadcast_prepend_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L428)]

##T urbo%2FBroadcastable:broadcast_prepend_later_to) #**broadcast_prepend_later_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Same as `broadcast_prepend_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L423)]

### **broadcast_prepend_to**(*streamables, target: broadcast_target_default, **rendering) ⇒ `Object`

Prepend a rendering of this broadcastable model to the target identified by it's dom id passed as `target` for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_prepend_to examiner.identity, :clearances, target: "clearances"

# Sends <turbo-stream action="prepend" target="clearances"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_prepend_to examiner.identity, :clearances, target: "clearances",
  partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L356)]

### **broadcast_refresh** ⇒ `Object`

Same as `#broadcast_refresh_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L374)]

### **broadcast_refresh_later** ⇒ `Object`

Same as `#broadcast_refresh_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L438)]

##T urbo%2FBroadcastable:broadcast_refresh_later_to) #**broadcast_refresh_later_to**(*streamables) ⇒ `Object`

Same as `broadcast_refresh_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L433)]

### **broadcast_refresh_to**(*streamables) ⇒ `Object`

Broadcast a "page refresh" to the stream name identified by the passed `streamables`. Example:

```
# Sends <turbo-stream action="refresh"></turbo-stream> to the stream named "identity:2:clearances"
clearance.broadcast_refresh_to examiner.identity, :clearances

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L369)]

### **broadcast_remove** ⇒ `Object`

Same as `#broadcast_remove_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L249)]

### **broadcast_remove_to**(*streamables, target: self) ⇒ `Object`

Remove this broadcastable model from the dom for subscribers of the stream name identified by the passed streamables. Example:

```
# Sends <turbo-stream action="remove" target="clearance_5"></turbo-stream> to the stream named "identity:2:clearances"
clearance.broadcast_remove_to examiner.identity, :clearances

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L244)]

### **broadcast_render**(**rendering) ⇒ `Object`

Render a turbo stream template with this broadcastable model passed as the local variable. Example:

```
# Template: entries/_entry.turbo_stream.erb
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

### **broadcast_render_later**(**rendering) ⇒ `Object`

Same as `broadcast_render_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L484)]

##T urbo%2FBroadcastable:broadcast_render_later_to) #**broadcast_render_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_render_later` but run with the added option of naming the stream using the passed `streamables`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L490)]

### **broadcast_render_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_render` but run with the added option of naming the stream using the passed `streamables`.

Note that rendering inline via this method will cause template rendering to happen synchronously. That is usually not desireable for model callbacks, certainly not if those callbacks are inside of a transaction. Most of the time you should be using `broadcast_render_later_to`, unless you specifically know why synchronous rendering is needed.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L479)]

### **broadcast_replace**(**rendering) ⇒ `Object`

Same as `#broadcast_replace_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L268)]

### **broadcast_replace_later**(**rendering) ⇒ `Object`

Same as `#broadcast_replace_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L398)]

##T urbo%2FBroadcastable:broadcast_replace_later_to) #**broadcast_replace_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_replace_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L393)]

### **broadcast_replace_to**(*streamables, **rendering) ⇒ `Object`

Replace this broadcastable model in the dom for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="replace" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_replace_to examiner.identity, :clearances

# Sends <turbo-stream action="replace" target="clearance_5"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_replace_to examiner.identity, :clearances, partial: "clearances/other_partial", locals: { a: 1 }

```

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L263)]

### **broadcast_update**(**rendering) ⇒ `Object`

Same as `#broadcast_update_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L287)]

### **broadcast_update_later**(**rendering) ⇒ `Object`

Same as `#broadcast_update_later_to`, but the designated stream is automatically set to the current model.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L408)]

##T urbo%2FBroadcastable:broadcast_update_later_to) #**broadcast_update_later_to**(*streamables, **rendering) ⇒ `Object`

Same as `broadcast_update_to` but run asynchronously via a `Turbo::Streams::BroadcastJob`.

[[View source](https://rubydoc.info/github/hotwired/turbo-rails/main/Turbo/Broadcastable#)] [[View on GitHub](https://github.com/hotwired/turbo-rails/blob/main/app/models/concerns/turbo/broadcastable.rb#L403)]

### **broadcast_update_to**(*streamables, **rendering) ⇒ `Object`

Update this broadcastable model in the dom for subscribers of the stream name identified by the passed `streamables`. The rendering parameters can be set by appending named arguments to the call. Examples:

```
# Sends <turbo-stream action="update" target="clearance_5"><template><div id="clearance_5">My Clearance</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_update_to examiner.identity, :clearances

# Sends <turbo-stream action="update" target="clearance_5"><template><div id="clearance_5">Other partial</div></template></turbo-stream>
# to the stream named "identity:2:clearances"
clearance.broadcast_update_to examiner.identity, :clearances, partial: "clearances/other_partial", locals: { a: 1 }
```