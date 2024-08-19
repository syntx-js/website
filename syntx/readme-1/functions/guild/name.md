---
description: Returns the name of a server.
icon: angle-right
---

# name

### Usage

```javascript
cmd.guild.name(guildID, client)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `guildID` | string   | true     |
| `client`  | callback | true     |

### Example

```javascript
client.command({
    name: "serverName",
    content: async (msg) => {
        const name = await cmd.guild.name(cmd.guild.id(msg), client)
        cmd.message.send({
            text: `Server name: ${name}`
        }, msg)
    }
})
```
