---
description: Gets the user's avatar.
icon: image
---

# avatar

### Usage

```javascript
cmd.user.avatar(userID, <message>, { size, dynamic? })
```



| OPTION    | TYPE    | REQUIRED |
| --------- | ------- | -------- |
| `userID`  | string  | false    |
| `message` | object  | true     |
| `size`    | number  | false    |
| `dynamic` | boolean | false    |

### Example

```javascript
const { ERXClient, Intents, cmd } = require("syntx.js")

const client = new ERXClient({
    // Your configuration
})

client.command({
    name: "avatar",
    content: async (msg) => {
        const avatar = await cmd.user.avatr(undefined, msg, { size: 4096 })
        cmd.message.send({
            text: avatar
        })
    }
})
```
