---
description: returns the user's message id.
icon: angle-right
---

# id

### Usage

```javascript
cmd.message.id(message)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `message` | callback | true     |

### Example

```javascript
client.command({
    name: "messageID",
    content: (msg) => {
        cmd.message.send({
            text: `Message ID: ${cmd.message.id(msg)}`
        }, msg)
    }
})
```
