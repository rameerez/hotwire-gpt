# Turbo: The speed of a single-page web application without having to write any JavaScript.

Current version: [8.0.4](https://github.com/hotwired/turbo/releases/tag/v8.0.4) --- released Mar 08, 2024

**Turbo** uses complementary techniques to dramatically reduce the amount of custom JavaScript that most web applications will need to write:

-   *Turbo Drive* accelerates links and form submissions by negating the need for full page reloads.
-   *Turbo Frames* decompose pages into independent contexts, which scope navigation and can be lazily loaded.
-   *Turbo Streams* deliver page changes over WebSocket, SSE or in response to form submissions using just HTML and a set of CRUD-like actions.
-   *Turbo Native* lets your [majestic monolith](https://m.signalvnoise.com/the-majestic-monolith/) form the center of your native iOS and Android apps, with seamless transitions between web and native sections.

It's all done by sending HTML over the wire. And for those instances when that's not enough, you can reach for the other side of [Hotwire](https://hotwired.dev), and finish the job with [Stimulus](https://stimulus.hotwired.dev).