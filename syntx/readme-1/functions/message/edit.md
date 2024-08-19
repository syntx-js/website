---
description: Edit a message sent by the bot.
icon: angle-right
---

# edit

### Usage

```javascript
cmd.message.edit({ data: { channel, message }, content?, embed?: { title?, description?, color?, image?, thumbnail?, timestamp?, author?, authorIcon?, authorURL?, footer?, footerIcon? } }), client
```

| OPTION        | TYPE     | REQUIRED |
| ------------- | -------- | -------- |
| `channel`     | string   | true     |
| `message`     | string   | true     |
| `content`     | string   | false    |
| `title`       | string   | false    |
| `titleURL`    | string   | false    |
| `description` | string   | false    |
| `color`       | string   | false    |
| `image`       | string   | false    |
| `thumbnail`   | string   | false    |
| `timestamp`   | boolean  | false    |
| `author`      | string   | false    |
| `authorIcon`  | string   | false    |
| `authorURL`   | string   | false    |
| `footer`      | string   | false    |
| `footerIcon`  | string   | false    |
| `client`      | callback | true     |

### Example

```javascript
client.command({
    name: "testing",
    content: async (msg) => {
        const id = await cmd.message.send({
            text: "Hello!",
            returnId: true
        }, msg)

        setTimeout(() => {
            cmd.message.edit({
                data: {
                    channel: cmd.channel.id(msg),
                    message: id
                },
                content: "Hello World!"
            }, client)
        }, 1000) // Edit the message after 1 second has passed
    }
})
```
