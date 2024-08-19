---
description: Returns the ID of the mentioned channel.
icon: angle-right
---

# mentioned

### Usage

```javascript
cmd.channel.mentioned(<message>, index?)
```

| OPTION    | TYPE   | REQUIRED |
| --------- | ------ | -------- |
| `message` | string | true     |
| `index`   | number | false    |

### Example

```javascript
client.command({
    name: "channel",
    content: (msg) => {
        cmd.message.send({
            text: `Channel ID: ${cmd.channel.mentioned(msg)}`
        }, msg)
    }
})
```
