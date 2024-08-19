---
description: Add reactions to the provided message.
icon: angle-right
---

# addReactions

### Usage

```javascript
cmd.message.addReactions({ channelID, messageID, reactions }, client)
```

| OPTION      | TYPE     | REQUIRED |
| ----------- | -------- | -------- |
| `channelID` | string   | true     |
| `messageID` | string   | true     |
| `reactions` | array    | true     |
| `client`    | callback | true     |

### Example

```javascript
client.command({
    name: "reaction",
    content: async (msg) => {
        const id = await cmd.message.send({
            text: "Hello!",
            returnId: true
        }, msg)
        cmd.message.addReactions({
            channelID: cmd.channel.id(msg),
            messageID: id,
            reactions: [
                "🍃"
            ]
        }, client)
    }
})
```
