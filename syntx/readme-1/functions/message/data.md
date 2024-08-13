---
description: Gets certain information from the provided message.
icon: angle-right
---

# data

### Usage

```javascript
cmd.message.data({ channel, messageID, type }, <client>)
```

| OPTION      | TYPE   | REQUIRED |
| ----------- | ------ | -------- |
| `channel`   | string | true     |
| `messageID` | string | true     |
| `type`      | string | true     |
| `client`    | string | true     |

For the `type` body, you only have these options:

#### Embed message

* title
* titleURL
* description
* color
* image
* thumbnail
* author
* authorIcon
* authorURL
* footer
* footerIcon

#### Normal message

* content
* authorId
* attachment

If a `type` is provided that does not correspond to its category or does not exist, an error will be returned.

### Example

```javascript
client.command({
    name: "test",
    content: async (msg) => {
        const id = await cmd.message.send({
            text: "Hello!",
            returnId: true
        }, msg)

        // Get us the message data
        const data =  await cmd.message.data({
            channel: cmd.channel.id(msg),
            messageID: id,
            type: "content" // Content: "Hello!"
        }, client)

        cmd.message.send({
            text: `Data: ${data}`
        }, msg)
    }
})
```
