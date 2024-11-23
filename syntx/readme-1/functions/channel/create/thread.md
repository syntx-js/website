---
icon: angle-right
description: Create a thread.
---

# thread

### Usage

```javascript
cmd.channel.create.thread({ channelID, messageID, name, duration, returnID?, type?, content? }, client)
```

| OPTION      | TYPE     | REQUIRED |
| ----------- | -------- | -------- |
| `channelID` | string   | true     |
| `messageID` | string   | true     |
| `name`      | string   | true     |
| `duration`  | number   | true     |
| `returnID`  | boolean  | false    |
| `client`    | callback | true     |
| `type`      | string   | false    |
| `content`   | string   | false    |

## Duration times

* 60
* 1440
* 4320
* 10080

## Types of type

* GUILD\_PUBLIC\_THREAD
* GUILD\_PRIVATE\_THREAD

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
            returnID: true,
            content: "Hi"
        }, client)
        cmd.message.send({ text: `<#${thread}>` }, msg)
    }
})
```
