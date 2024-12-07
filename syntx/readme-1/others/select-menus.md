---
description: Add Select Menus to the bot's response.
icon: bars-sort
---

# Select Menus

First, we require `SelectMenus` from the `syntx.js` library

```javascript
const { SelectMenus } = require("syntx.js")
```

## Example of usage

```javascript
const menus = new SelectMenus([
    {
        type: string,
        menu_id: string
        content?: string,
        max?: number
        min?: number
        fields: [
            {
                name: string,
                value: string,
                description?: string,
                default?: boolean,
                emoji?: string
            }
        ]
    }
])
```

## Types of `type`

* normal
* channel
* user
* role

{% hint style="info" %}
If `type` is not `normal` but is `channel`, `user` or `role`, then the `fields` parameter is not used.
{% endhint %}

## Example

```javascript
client.command({
    name: "test",
    content: async (msg) => {
        const menus = new SelectMenus([
            {
                type: "normal",
                menu_id: "menu",
                fields: [
                    {
                        name: "Value 1",
                        value: "value_1",
                        description: "This is value 1"
                    }
                ]
            },
            {
                type: "user",
                menu_id: "menu2"
            }
        ])
        
        await cmd.message.send({
            text: "Menus",
            components: menus.build()
        }, msg)
    }
})
```

Interaction

```javascript
// Normal interaction
client.interaction({
    id: "menu",
    content: async (msg) => {
        await msg.reply({ content: `Selected menu: ${msg.values[0]}`, ephemeral: true })
    }
})
```
