# sendMessage

Function that is used to send a message to a specific or current channel. Something similar to `<argument>.channel.send`&#x20;

### Usage

```javascript
cmd.message.sendMessage({text, channel, returnId?}, <message>)
```



| OPTION      | TYPE     | DESCRIPTION                                                          | REQUIRED |
| ----------- | -------- | -------------------------------------------------------------------- | -------- |
| `text`      | string   | The text to be sent.                                                 | true     |
| `channel`   | string   | The ID of the channel where the message will be sent.                | false    |
| `returnId?` | boolean  | if `true`, the id of the message that the bot will send is returned. | false    |
| `<message>` | function | The name of the previously defined variable is set.                  | true     |

## Example

```javascript
client.command({
    name: "test",
    content: (message) => {
        cmd.message.sendMessage({
            text: "Hi!"
        }, message)
    }
})
```

But it is not always used that way. If you decide that `returnId` is `true`, its structure would be as follows:

```javascript
client.command({
    name: "test",
    content: (message) => {
        const messageId = cmd.message.sendMessage({ text: "Hi!", returnId: true }) // This constant stores the id of the message.
        console.log(messageId) // Return the ID.
    }
})
```
