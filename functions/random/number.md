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
        message.channel.send(`Number: ${cmd.random.number(1, 100)}`)
    }
})
```
