---
description: Create a thread.
icon: angle-right
---

# thread

### Usage

```javascript
cmd.channel.create.thread({ channelID, messageID, name, duration, returnID? }, client)
```

| OPTION      | TYPE     | REQUIRED |
| ----------- | -------- | -------- |
| `channelID` | string   | true     |
| `messageID` | string   | true     |
| `name`      | string   | true     |
| `duration`  | number   | true     |
| `returnID`  | boolean  | false    |
| `client`    | callback | true     |

## Duration times

* 60
* 1440
* 4320
* 10080

### Example

```javascript
client.command({
    name: "thread",
    content: async (msg) => {
        const thread = await cmd.channel.create.thread({
            channelID: cmd.channel.id(msg),
            messageID: msg.id,
            name: "Open",
            duration: 60, // in minutes
            returnID: true
        }, client)
        cmd.message.send({ text: `<#${thread}>` }, msg)
    }
})
```
