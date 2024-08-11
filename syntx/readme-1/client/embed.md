---
icon: angle-right
description: Set up an embed message to send later.
---

# Embed

### Export the `Embed` module from the library

```javascript
const { ERXClient, Intents, Embed, cmd } = require("syntx.js")
```

### Create a new command and use the `Embed` method

```javascript
client.command({
    name: "embed",
    content: (msg) => {
        const embed = new Embed()
        embed.set({ // We start creating the embed
            title: "Hello",
            description: "This is an embedded message",
            color: 0x2ecc71
        })
        cmd.message.send({
            text: { embeds: [embed.build()] }
        }, msg) // We send the embed message
    }
})
```

We use `embed.build()` to get the embed information and send it.



| OPTION        | TYPE                 | REQUIRED |
| ------------- | -------------------- | -------- |
| `title`       | string               | false    |
| `description` | string               | false    |
| `color`       | number (hexadecimal) | false    |
| `footer`      | string               | false    |
| `footerIcon`  | string               | false    |
| `image`       | string               | false    |
| `author`      | string               | false    |
| `authorIcon`  | string               | false    |
| `authorURL`   | string               | false    |

You can use more `embeds` options in the code, such as adding fields or the timestamp.

```javascript
client.command({
    name: "embed",
    content: (msg) => {
        const embed = new Embed()
        embed.set({ // We start creating the embed
            title: "Hello",
            description: "This is an embedded message",
            color: 0x2ecc71
        })
        embed.addField(name, value, inline?),
        embed.setURL(url)
        embed.timestamp()
        cmd.message.send({
            text: { embeds: [embed.build()] }
        }, msg) // We send the embed message
    }
})
```

### Fields

| OPTION   | TYPE    | REQUIRED |
| -------- | ------- | -------- |
| `name`   | string  | true     |
| `value`  | string  | true     |
| `inline` | boolean | false    |

### SetURL

| OPTION | TYPE   | REQUIRED |
| ------ | ------ | -------- |
| `url`  | string | true     |
