---
icon: angle-right
description: It works to get a specific argument from the user's message.
---

# argument

### Usage

<pre class="language-javascript"><code class="lang-javascript"><strong>cmd.message.argument(&#x3C;message>, index)
</strong></code></pre>

Exchange `<message>` with the name you gave to your content. For example, if you added the name `msg` to your content, you must exchange `<message>` with `msg`.

```javascript
client.command({
    name: "test",
    content: (message) => {
        cmd.message.send({
        text: `First argument: ${cmd.message.argument(msg, 1)}`
        }, message)
    }
})
```

## Another example

```javascript
client.command({
    name: "test",
    content: (message) => {
        const arg = cmd.message.argument(message, 1) // Will return the first argument
        if (arg == "hi") {
            cmd.message.send({
                text: `Hi!`
            }, message)
        } else {
            cmd.message.send({
                text: "I couldn't understand your message."
            }. message)
        }
    }
})
```

This will mean that if the first argument of the message is "hi", the bot will greet you.
