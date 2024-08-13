---
icon: text
---

# text

What `random.text` does is return a completely random text from those provided above.

### Usage

```javascript
cmd.random.text([texts])
```

| PARAMETER | TYPE   | DESCRIPTION        |
| --------- | ------ | ------------------ |
| `texts`   | string | Texts to randomize |

### Example

{% code lineNumbers="true" %}
```javascript
const { ERXClient, Intents, cmd } = require("syntx.js")

// Client

client.command({
    name: "random",
    content: (message) => {
        cmd.message.send({
            text: `Random Text: ${cmd.random.text(["Hi", "Hello", "Syntx"])}
        }, message)
    }
})
```
{% endcode %}
