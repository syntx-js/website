---
icon: angle-right
---

# Command & Events

***

### Create commands

Command creation is a pivotal feature for enhancing the versatility and uniqueness of your bot. Through custom commands, you can infuse it with distinctive appeal, tailoring them to fit specific needs and purposes. I'll guide you through the structure for creating commands using Syntx.js, in case you're not utilizing handlers.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
<client>.command({
    ...
})
```
{% endcode %}

`<client>` is the instance you previously defined in your project.

The `command` method has a straightforward structure to understand and learn, yet the real challenge arises when it comes to adding content. However, we've created functions that could make this creation process much easier.

{% code lineNumbers="true" %}
```javascript
<client>.command({
    name: ...,
    content: (...) => {
        ...
    }
})
```
{% endcode %}

Make sure to assign a string value to `name`, as this will be the name of your command. As for `content`, you should add a name (of your choosing) inside the `()` ensure it's not too lengthy to proceed with the command creation.

#### Example

{% code lineNumbers="true" %}
```javascript
<client>.command({
    name: "hi",
    content: (message) => {
        message.channel.send(`Hello ${message.author.username}!`)
    }
})
```
{% endcode %}

| OPTION    | TYPE     | DESCRIPTION   |
| --------- | -------- | ------------- |
| `name`    | string   | Command name. |
| `content` | function | Command code. |

***

### Command Handler

If you appreciate orderliness, handler commands are perfect for you. These commands enhance the structure and aesthetics of your project by organizing each command into separate files.

While this structure is somewhat similar to the traditional `<client>.command` form, it introduces a more streamlined and organized approach.

#### How to use it

1. Introduce the `handler` method in your client.

{% code lineNumbers="true" %}
```javascript
const { ERXClient, Intents } = require("syntx.js")

const client = new ERXClient({
    // You configuration
})

client.handler({ commands: "./commands", events: "./events" }, true) // Enter the folder where all the commands will be.
```
{% endcode %}

2. Make sure the folder exists.

```
🗀 commands/
│   └── hello.js
🗀 events/
│   └── messagecreate.js
├── index.js
└── package.json
```

3. Start making the code.

{% code lineNumbers="true" %}
```javascript
module.exports = {
    name: "hi",
    content: (message) => {
        message.channel.send(`Hello ${message.author.username}!`)
    }
}
```
{% endcode %}

Now, running !hi will display the entered content.\
\
Do you notice the difference? If not, look at the next block.

{% code lineNumbers="true" %}
```diff
- <client>.command({...})
+ module.exports =({
    name: "hi",
    content: (message) => {
        message.channel.send(`Hello ${message.author.username}!`)
    }
})
```
{% endcode %}

## Events

To create an event, it's almost the same as if you were creating a command. Compared to little things.\
\


There are 2 ways to create events.

1. Add the `Events` module to `syntx.js` (recommended)
2. Write the name of the event.

```javascript
const { Events, cmd } = require("syntx.js")
```

```javascript
<client>.event(Events.MessageDelete, (callback) => {
    cmd.message.send({
        text: "Hi"
    }, callback)
})
```

If you like everything more organized, you also have the option of making it a handler.

```javascript
// <client>.handler({ events: EVENTS_PATH })
client.handler({ events: "./events" }, true)
```

```
🗀 commands/
│   └── hello.js
🗀 events/
│   └── hi.js
├── index.js
└── package.json
```

```diff
- <client>.event(Events.MessageCreate, (callback) => {
-    cmd.message.send({ text: "Hi" }, callback)
- })
+  const { Events, cmd } = require("syntx.js")
+ module.exports = {
+     event: Events.MessageCreate,
+     content: async (callback) => {
+        cmd.message.send({ text: "Hi" }, callback)
+    }
+ }
```
