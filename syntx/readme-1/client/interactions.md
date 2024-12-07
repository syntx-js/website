---
icon: angle-right
---

# Interactions

## Create Interactions

To create an interaction we will need to use the `interaction` method of the `client.js` class, so first you must create your client.

```javascript
const client = new ERXClient({
    // ...
})
```

Now we can use the `interaction` method.

```javascript
client.interaction({
    // ...
})
```

| OPTON     | DESCRIPTION                                    |
| --------- | ---------------------------------------------- |
| `id`      | ID given to the interaction (interaction name) |
| `content` | Code to execute                                |

### Example

```javascript
client.command({
    name: "buttons",
    content: async (msg) => {
        const buttons = new Buttons([
            {
                id: "test",
                label: "Click Me",
                style: "Primary"
            }
        ])
        await cmd.message.send({ text: "Hi!", compontents: buttons.build() }, msg)
    }
})

client.interaction({
    id: "test",
    content: async (interaction) => {
        interaction.reply({ content: "Hello! :)", ephemeral: true })
    }
})
```

We also take into account those users who like everything organized, whether by files or folders, so we have decided to implement interactions as handlers in addition to commands, simply adding something new.\
\
First we must use the `handler` method to load the commands.

```javascript
client.handler({ interactions: "./path" }, true)
```

Replace `./path` with the actual path of the folder where all commands and interactions will be.

After this, we recommend creating a subfolder in `./path` called "interactions", where all the interactions will be. (This is optional)\
\
Then we will create a new file with any name, but with the following structure:

```javascript
const { cmd } = require("syntx.js")
module.exports = {
    idme: "test", // Replace "test" with the ID you gave to the interaction.
    content: async (interaction) => {
        interaction.reply({ content: "Hello! :)", ephemeral: true })
    }
}
```

## Dynamic IDs

We know that many of you do not like to complicate the issue of interactions and create chaos to verify that the user who pressed the button is the same one who executed the command, that is why we bring you dynamic IDs.\
\
**How do they work?**\
Easy. Simply in the button or menu that they are making, in its ID you must put something like for example: `id-${value}`. They must exchange `value` for the value they want to save. You can change the separator (-) for a custom one that you like best.

```javascript
client.command({
    name: "test",
    content: async (msg) => {
        const n = 1
        const buttons = new Buttons([
            { id: `button1-${n}`, style: "Primary", label: "Click me" }
        ])
        await cmd.message.send({
            text: "Hi",
            components: [buttons.build()]
        }, msg)
    }
})
```

Now in the interaction, you will need to add some new parameters for the interaction to work properly.

### Normal

```javascript
client.interaction({
    id: "button1-{value}",
    separator: "-", // You only add this if your separator is not "-".
    content: async (interaction, { value }) => {
        await interaction.reply({ content: `Value: ${value}`, ephemeral: true })
    }
})
```

### Handler

```javascript
module.expots({
    id: "button1-{value}",
    separator: "-", // You only add this if your separator is not "-".
    content: async (interaction, { value }) => {
        await interaction.reply({ content: `Value: ${value}`, ephemeral: true })
    }
})
```

You can change `value` to whatever name you prefer. Of course, the separator must be the same one you used previously and the ID must be complete.

## Example

```javascript
client.command({
    name: "test",
    content: async (msg) => {
        const n = 1
        const buttons = new Buttons([
            { id: `button1-${n}-${msg.author.id}`, style: "Primary", label: "Click me" }
        ])
        await cmd.message.send({
            text: "Hi",
            components: [buttons.build()]
        }, msg)
    }
})
```

Interaction

```javascript
client.interaction({
    id: "button1-{number}-{author}",
    separator: "-", // You only add this if your separator is not "-".
    content: async (interaction, { number, author }) => {
        if (author != interaction.user.id) {
            await interaction.reply({ content: "This interaction does not belong to you.", ephemeral: true })
            return;
        }
        await interaction.reply({ content: `Number: ${number}`, ephemeral: true })
    }
})
```
