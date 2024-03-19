# Hotwire docs for Hotwire GPT

These are the Markdown docs used to feed the custom GPT ["Hotwire Expert"](https://chat.openai.com/g/g-fpzPJfYvQ-hotwire-expert-turbo-streams-frames-stimulus)

It's a custom GPT to answer questions about Hotwire: Turbo Streams, Turbo Frames & Stimulus

## Building few but big Markdown files

The problem with custom GPTs is that you have a 20 file upload limit. So you need a way to concatenate all the docs into few, but big, Markdown files. We use `concat-md` for that:

To concatenate folders into a big Markdown file:
```
concat-md --toc --decrease-title-levels --file-name-as-title --dir-name-as-title stimulus > stimulus.md
concat-md --toc --decrease-title-levels --file-name-as-title --dir-name-as-title turbo > turbo.md
```

Make sure to install `concat-md` first:
```
npm install -g concat-md
```

## Adding HTML docs as Markdown

Another trick I used was to literally just copy all the contents of all the [RubyDoc pages](https://rubydoc.info/github/hotwired/turbo-rails/main) for the [`turbo-rails` gem](https://github.com/hotwired/turbo-rails) and include them as Markdown files.

The reason I did this is beacause the Hotwire docs are framework-agnostic, and I'm particularly interested in the specific Rails helpers, which are only documented in the Ruby gems for Hotwire.

To convert all the RubyDoc pages into Markdown files I used [clipboard2markdown](https://euangoddard.github.io/clipboard2markdown/) and manually copied and pasted the contents of the website to get the Markdown.