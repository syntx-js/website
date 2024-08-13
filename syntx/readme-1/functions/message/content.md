---
description: Returns the user's entire message.
icon: angle-right
---

# content

### Usage

```javascript
cmd.message.content(<message>)
```

| OPTION    | TYPE     | REQUIRED |
| --------- | -------- | -------- |
| `message` | callback | true     |

### Example

```javascript
client.command({
    name: "say",
    content: (msg) => {
        const message = cmd.message.content(msg)
        cmd.message.send({
            text: message
        }, msg)
    }
})
```
