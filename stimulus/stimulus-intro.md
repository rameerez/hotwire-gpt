# Stimulus: A modest JavaScript framework for the HTML you already have.

Stimulus is a JavaScript framework with modest ambitions. It doesn't seek to take over your entire front-end---in fact, it's not concerned with rendering HTML at all. Instead, it's designed to augment your HTML with just enough behavior to make it shine. Stimulus pairs beautifully with [Turbo](https://turbo.hotwired.dev) to provide a complete solution for fast, compelling applications with a minimal amount of effort.

## Example:

Sprinkle your HTML with controller, target, and action attributes:
```
<!--HTML from anywhere--><div data-controller="hello">  <input data-hello-target="name" type="text">  <button data-action="click->hello#greet">    Greet  </button>  <span data-hello-target="output">  </span></div>
```

Write a compatible controller and watch Stimulus bring it to life:
```
// hello_controller.jsimport { Controller } from "stimulus"export default class extends Controller {  static targets = [ "name", "output" ]  greet() {    this.outputTarget.textContent =      `Hello, ${this.nameTarget.value}!`  }}
```

Current version: [3.2.2](https://github.com/hotwired/stimulus/releases/tag/v3.2.2) --- released August 7th 2023