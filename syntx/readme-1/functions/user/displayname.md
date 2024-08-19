---
description: Returns the user's global nickname.
icon: tag
---

# displayName

### Usage

```javascript
cmd.user.displayName(userID, client)
```

| OPTION   | TYPE     | REQUIRED |
| -------- | -------- | -------- |
| `userID` | string   | true     |
| `client` | callback | true     |

### Example

```javascript
client.command({
    name: "displayName",
    content: async (msg) => {
        const name = await cmd.user.displayName(cmd.user.authorId(msg), client)
        cmd.message.send({
            text: `Display Name: ${name}`
        }, msg)
    }
})
```
