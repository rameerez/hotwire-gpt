Module: Turbo::StreamsHelper
============================

Defined in:

app/helpers/turbo/streams_helper.rb

Instance Method Details
-----------------------

### **turbo_stream** ⇒ `Object`

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

### **turbo_stream_from**(*streamables, **attributes) ⇒ `Object`

Used in the view to create a subscription to a stream identified by the `streamables` running over the `Turbo::StreamsChannel`. The stream name being generated is safe to embed in the HTML sent to a user without fear of tampering, as it is signed using `Turbo.signed_stream_verifier`. Example:

```
# app/views/entries/index.html.erb
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