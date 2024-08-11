---
icon: text
---

# text

What `random.text` does is return a completely random text from those provided above.

### Usage

```yang
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
        message.channel.send(`Random text: ${cmd.random.text(["Seraph", "Discord", "Syntx"])}`)
    }
})
```
{% endcode %}
