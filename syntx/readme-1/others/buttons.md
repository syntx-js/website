---
description: Add buttons to the message sent by the bot.
icon: circle-dot
---

# Buttons

First of all, we must export the `Buttons` method from the `syntx.js` library:

```javascript
const { Buttons } = require("syntx.js")
```

### Example of use

```javascript
const buttons = new Buttons([
    {
        id: string,
        label: string,
        style: string,
        url?: string,
        disabled?: boolean,
        emoji?: string
    },
    // You can add more if you want
])
```

## Available styles

* Primary
* Secondary
* Success
* Danger
* Link

Now, to send the buttons, we need to use the `build()` method inside the `components` body of `cmd.message.send` or the one you are currently using.

```javascript
await cmd.message.send({ components: buttons.build() }, <message>)
```

### Example

```javascript
client.command({
    name: "buttons",
    content: async (msg) => {
        const buttons = new Buttons([
            {
                id: "b1",
                label: "Button 1!",
                style: "Primary"
            },
            {
                id: "b2",
                label: "Button 2!",
                style: "Secondary"
            },
            {
                id: "b3",
                label: "Button 3!",
                style: "Success"
            },
            {
                id: "b5",
                label: "Button 5!",
                style: "Danger"
            },
            {
                id: "b5",
                label: "Button 5!",
                style: "Link",
                url: "https://www.npmjs.com/package/syntx.js"
            }
        ])
        
        await cmd.message.send({ text: "Buttons", components: buttons.build() }, msg)
    }
})
```
