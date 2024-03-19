Module: Turbo::FramesHelper
===========================

Defined in:

app/helpers/turbo/frames_helper.rb

Instance Method Details
-----------------------

### **turbo_frame_tag**(*ids, src: nil, target: nil, **attributes, &block) ⇒ `Object`

Returns a frame tag that can either be used simply to encapsulate frame content or as a lazy-loading container that starts empty but fetches the URL supplied in the `src` attribute.

#### Examples

```
<%= turbo_frame_tag "tray", src: tray_path(tray) %>
# => <turbo-frame id="tray" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag tray, src: tray_path(tray) %>
# => <turbo-frame id="tray_1" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag "tray", src: tray_path(tray), target: "_top" %>
# => <turbo-frame id="tray" target="_top" src="http://example.com/trays/1"></turbo-frame>

<%= turbo_frame_tag "tray", target: "other_tray" %>
# => <turbo-frame id="tray" target="other_tray"></turbo-frame>

<%= turbo_frame_tag "tray", src: tray_path(tray), loading: "lazy" %>
# => <turbo-frame id="tray" src="http://example.com/trays/1" loading="lazy"></turbo-frame>

<%= turbo_frame_tag "tray" do %>
  <div>My tray frame!</div>
<% end %>
# => <turbo-frame id="tray"><div>My tray frame!</div></turbo-frame>

<%= turbo_frame_tag [user_id, "tray"], src: tray_path(tray) %>
# => <turbo-frame id="1_tray" src="http://example.com/trays/1"></turbo-frame>

```

The `turbo_frame_tag` helper will convert the arguments it receives to their `dom_id` if applicable to easily generate unique ids for Turbo Frames:

```
<%= turbo_frame_tag(Article.find(1)) %>
# => <turbo-frame id="article_1"></turbo-frame>

<%= turbo_frame_tag(Article.find(1), "comments") %>
# => <turbo-frame id="comments_article_1"></turbo-frame>

```