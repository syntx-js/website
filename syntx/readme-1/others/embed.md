---
icon: code-branch
description: Set up an embed message to send later.
---

# Embed

### Table of Contents

* [Export the `Embed` module from the library](embed.md#export-the-embed-module-from-the-library)
* [Structure 1](embed.md#structure-1)\
  \- [Create a new command and use the `Embed` method](embed.md#create-a-new-command-and-use-the-embed-method)\
  \- [Fields](embed.md#fields)\
  \- [setURL](embed.md#seturl)
* [Structure 2](embed.md#structure-2)\
  \- [Example](embed.md#example)

### Export the `Embed` module from the library

```javascript
const { Embed } = require("syntx.js")
```

First, you need to know that this function has 2 types of structures. Both are valid and we will teach you how to put them on.

## Structure 1

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

```javascript
const embed = new Embed()
embed.set({
    title?: string,
    description?: string,
    color?: number,
    footer?: string,
    footerIcon?: string,
    image?: string,
    author?: string,
    authorIcon?: string,
    authorURL?: string
})
```

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

## Structure 2

In this structure it is all JSON. The fields are added as JSON, as are the `author`, `footer` and `timestamp`.

```javascript
embed.set({
    title?: {
        content?: string,
        url?: string,
    },
    description?: string,
    color?: number,
    image?: string,
    thumbnail?: string,
    timestamp?: boolean,
    footer?: {
        content?: string,
        icon?: string
    },
    author?: {
        content?: string,
        url?: string,
        icon?: string
    },
    fields?: [
        {
            name?: string,
            value?: string,
            inline?: boolean
        },
        ...
    ]
}, 2) // Specifies the structure of the embed, in this case it is 2
```

### Example

```javascript
client.command({
    name: "embed",
    content: (msg) => {
        const embed = new Embed()
        embed.set({
            title: {
                content: "Example",
                url: "https://discord.com"
            },
            description: "Example 2",
            color: 0x5865f2,
            image: "https://cdn.discordapp.com/avatars/990604235362140180/7f74c73606475f8bf1848a126833e2d1.png",
            thumbnail: "https://cdn.discordapp.com/avatars/990604235362140180/7f74c73606475f8bf1848a126833e2d1.png",
            timestamp: true,
            footer: {
                content: "Example 3",
                icon: "https://cdn.discordapp.com/avatars/990604235362140180/7f74c73606475f8bf1848a126833e2d1.png"
            },
            author: {
                content: "Example 4",
                url: "https://discord.com",
                icon: "https://cdn.discordapp.com/avatars/990604235362140180/7f74c73606475f8bf1848a126833e2d1.png"
            },
            fields: [
                {
                    name: "Example 5",
                    value: "Example 6",
                    inline: true
                },
                {
                    name: "Example 7",
                    value: "Example 8",
                    inline: true
                }
            ]
        }, 2) // We indicate that the structure used is 2
        cmd.message.send({
            text: { embeds: [embed.build()] },
        }, msg)
    }
})
```

{% hint style="danger" %}
It is important that you set `structureType` to the number 2. Otherwise structure 2 will not work for you. Only the 1.
{% endhint %}
