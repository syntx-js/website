---
description: Gets the ID of the message author.
---

# authorId

### Usage

```javascript
cmd.user.authorId(<message>)
```



| OPTION    | TYPE     | DESCRIPTIONN                                       | REQUIRED |
| --------- | -------- | -------------------------------------------------- | -------- |
| `message` | function | The name of the variable you entered in `content`. | true     |

### Example

```javascript
const { ERXClient, cmd, Intents } = require("syntx.js")

const client = new ERXClient({
    prefix: "!",
    intents: Intents.Fast,
    token: ...
})

client.ready(() => {
    console.log("Bot Ready")
})

client.command({
    name: "user",
    content: (message) => {
        cmd.message.send({
            text: `Your ID: ${cmd.user.authorId(message)}`,
        }, message)
    }
})

client.start()
```
