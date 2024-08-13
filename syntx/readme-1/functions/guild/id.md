---
description: Gets the ID of the current guild.
icon: angle-right
---

# id

### Usage

```javascript
cmd.guild.id(<message>)
```

|           |          |      |
| --------- | -------- | ---- |
| `message` | callback | true |

### Example

```javascript
client.command({
    name: "guildID",
    content: (msg) => {
        cmd.message.send({
            text: `Guild ID: ${cmd.guild.id(msg)}`
        }, msg)
    }
})
```
