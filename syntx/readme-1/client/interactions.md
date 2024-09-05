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
client.handler("./path", true)
```

Replace `./path` with the actual path of the folder where all commands and interactions will be.

After this, we recommend creating a subfolder in `./path` called "interactions", where all the interactions will be. (This is optional)\
\
Then we will create a new file with any name, but with the following structure:

```javascript
const { cmd } = require("syntx.js")
module.exports = {
    type: "interaction", // Indicates that it should be loaded as an interaction
    name: "test", // Replace "test" with the ID (name) you gave to the interaction.
    content: async (interaction) => {
        interaction.reply({ content: "Hello! :)", ephemeral: true })
    }
}
```
