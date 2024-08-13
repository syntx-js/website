---
icon: '0'
---

# number

`random.number` works to choose a random number between `a` which is minimum and `b` which is maximum.

### Usage

```yang
cmd.random.number(a, b)
```

### Example

```javascript
const { ERXClient, Intents, cmd } = require("syntx.js")

// Client

client.command({
    name: "number",
    content: (message) => {
        cmd.message.send({
            text: `Number: ${cmd.random.number(1, 100)}`
        }, message)
    }
})
```
