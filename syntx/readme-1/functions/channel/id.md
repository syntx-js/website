---
description: Gets the ID of the current channel.
icon: angle-right
---

# id

### Usage

```javascript
cmd.channel.id(<message>)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `message` | callback | true     |

### Example

```javascript
client.command({
    name: "channelID",
    content: (msg) => {
        cmd.message.send({
            text: `Channel ID: ${cmd.channel.id(msg)}`
        }, msg)
    }
})
```
