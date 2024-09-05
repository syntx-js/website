---
description: Edit the buttons sent by the bot.
icon: angle-right
---

# buttons

### Usage

```javascript
cmd.message.send({ id, messageID, label, style, disabled?, emoji? }, message)
```

| OPTION      | TYPE     | REQUIRED |
| ----------- | -------- | -------- |
| `id`        | string   | true     |
| `messageID` | string   | true     |
| `label`     | string   | true     |
| `style`     | string   | true     |
| `disabled`  | boolean  | false    |
| `emoji`     | string   | false    |
| `mesage`    | callback | true     |

### Example

```javascript
client.command({
    name: "test",
    content: async (msg) => {
        const buttons = new Buttons([
            {
                id: "test-1",
                label: "Click Me",
                style: "Primary"
            }
        ])
        await cmd.message.send({ text: "Cick Me", components: buttons.build() }, msg)
    }
})

client.interaction({
    id: "test-1",
    content: async (interaction) => {
        cmd.message.edit.buttons({
            id: "test-1",
            messageID: interaction.message.id,
            label: "Click Me",
            style: "Primary",
            disabled: true
        }, interaction)
        await interaction.reply({ content: "Clicked!", ephemeral: true })
    }
})
```
