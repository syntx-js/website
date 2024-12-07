---
icon: angle-right
---

# send

Function that is used to send a message to a specific or current channel. Something similar to `<argument>.channel.send`&#x20;

### Usage

```javascript
cmd.message.send({ text, channel, returnId?, options?: { reply?, ping? }, components?, files? }, <message>)
```

| OPTION       | TYPE     | DESCRIPTION                                                                                                                                      | REQUIRED |
| ------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| `text`       | string   | The text to be sent.                                                                                                                             | true     |
| `channel`    | string   | The ID of the channel where the message will be sent.                                                                                            | false    |
| `returnId`   | boolean  | if `true`, the id of the message that the bot will send is returned.                                                                             | false    |
| `<message>`  | callback | The name of the previously defined variable is set.                                                                                              | true     |
| `reply`      | boolean  | If the value is `true`, when the message is sent it will also reply to the message sent by the user.                                             | false    |
| `ping`       | boolean  | If the value is `true`, then it will enable all mentions of the message. Otherwise it will disable all mentions in the message.                  | false    |
| `components` | array    | Adds the created components to the bot's sent message. If it is a single component, there is no need to use an array. Otherwise it is necessary. | false    |
| `files`      | array    | It sends, along with the bot's message, a certain number of files indicated.                                                                     | false    |

## Example

```javascript
client.command({
    name: "test",
    content: (message) => {
        cmd.message.send({
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
        const messageId = cmd.message.send({ text: "Hi!", returnId: true }, message) // This constant stores the id of the message.
        console.log(messageId) // Return the ID.
    }
})
```
