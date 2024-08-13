---
description: Gets the ID of the mentioned user
icon: angle-right
---

# mentioned

### Usage

```javascript
cmd.message.mentioned(<message>, index?)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `message` | callback | true     |
| `index`   | number   | false    |

### Example

```javascript
client.command({
    name: "mentioned",
    content: (msg) => {
        const mention = cmd.message.mentioned(msg)
        cmd.message.send({
            text: `ID: ${mention}`
        }, msg)
    }
})
```
