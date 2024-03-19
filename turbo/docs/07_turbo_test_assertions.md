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

### **assert_no_turbo_stream**(action:, target: nil, targets: nil) ⇒ `Object`

Assert that the rendered fragment of HTML does not contain a '<turbo-stream>` element.

#### Options

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

### **assert_turbo_stream**(action:, target: nil, targets: nil, count: 1, &block) ⇒ `Object`

Assert that the rendered fragment of HTML contains a '<turbo-stream>` element.

#### Options

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