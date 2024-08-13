---
icon: tag
description: Gets the name of a user using their ID.
---

# username

### Usage

```javascript
cmd.user.username(id, <client>)
```



| OPTION   | TYPE     | DESCRIPTION                                        | REQUIRED |
| -------- | -------- | -------------------------------------------------- | -------- |
| `id`     | string   | User ID.                                           | true     |
| `client` | callback | Name of the variable where you created the client. | true     |

### Example

```javascript
const { ERXClient, cmd, Intents } = require("syntx.js")

const client = new ERXClient({
    prefix: "!",}
    intents: Intents.Fast,
    token: ...
})

client.ready(() => {
    console.log("Bot ready")
})

client.command({
    name: "username",
    content: async (message) => {
        const id = cmd.user.authorId(message)
        const user = await cmd.user.username(id, client)
        cmd.message.send({
            text: `Your username is: ${user}`
        }, message)
    }
})
```
