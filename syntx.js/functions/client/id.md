---
description: Gets the bot ID.
icon: angle-right
---

# id

### Usage

```javascript
cmd.client.id(<client>)
```



| OPTION   | TYPE     | DESCRIPTION                                                | REQUIRED |
| -------- | -------- | ---------------------------------------------------------- | -------- |
| `client` | function | Set the name of the variable where you created the client. | true     |

### Example

```javascript
const { ERXClient, cmd, Intents } = require("syntx.js")

const client = new ERXClient({
    prefix: "!",
    intents: Intents.Fast,
    token: ...
})

client.ready(() => {
    console.log(`Bot connected with ID ${cmd.client.id(client)}`)
})

client.start()
```
