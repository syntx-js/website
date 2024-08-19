---
icon: angle-right
description: Returns the user's entire message.
---

# content

### Usage

```javascript
cmd.message.content(<message>, firstArgument?: boolean)
```

| OPTION          | TYPE     | REQUIRED |
| --------------- | -------- | -------- |
| `message`       | callback | true     |
| `firstArgument` | boolean  | false    |

If you set `firstArgument` to true, then this function will take into account the first argument of your message. That is, it will take into account the trigger of your command.

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
