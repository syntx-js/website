---
description: Returns the user's nickname on the given server.
icon: tag
---

# nick

### Usage

```javascript
cmd.user.nick(userID, guildID, client)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `userID`  | string   | true     |
| `guildID` | string   | true     |
| `client`  | callback | true     |

### Example

```javascript
client.command({
    name: "nick",
    content: async (msg) => {
        const nick = await cmd.user.nick(cmd.user.authorId(msg), cmd.guild.id(msg), client)
        cmd.message.send({
            text: `Nick: ${nick}`
        }, msg)
    }
})
```
