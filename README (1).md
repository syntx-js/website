# Syntx.js



<figure><img src="https://github.com/rqnjs/website/blob/main/img/syntx.js.png?raw=true" alt=""><figcaption><p>Create Discord bots a little faster and easier.</p></figcaption></figure>

[![npm version](https://img.shields.io/npm/v/syntx.js.svg?style=flat-square)](https://www.npmjs.org/package/syntx.js)     [![npm downloads](https://img.shields.io/npm/dm/syntx.js.svg)](https://www.npmjs.com/package/syntx.js)     ![License](https://img.shields.io/npm/l/syntx.js)     ![version](https://img.shields.io/npm/v/syntx.js.svg?color=3182b0)     [![Support Server](https://img.shields.io/badge/Discord-Support\_server-5865f2?logo=discord)](https://discord.gg/QQrSgyvykj)     ![code helpers](https://img.shields.io/badge/code\_helpers-1-5865f2?logo=htmx\&logoColor=white) &#x20;

Syntx.js is an NPM package designed to simplify and accelerate the creation of Discord bots. Although it is still under development, Syntx.js offers a wide range of functions for enhancing your bot. It utilizes a JSON-based structure for ease of use and flexibility. For further information or assistance, feel free to reach out to us via our [support server](https://discord.gg/invite/QQrSgyvykj) or through our [email syntxjs@gmail.com](https://mail.google.com/mail/u/0/?fs=1\&to=syntxjs@gmail.com\&su=Help+me\&tf=cm).

## Tables of contents

* [Installing](<README (1).md#installing>)
* [How to create a new client](<README (1).md#how-to-create-a-new-client>)\
  [Request the library](<README (1).md#request-the-library>)\
  [Create the new client](<README (1).md#create-the-new-client>)\
  [Run the bot](<README (1).md#run-the-bot>)
* [Example using the command method](<README (1).md#example-using-the-command-method>)
* [Change the presence of your bot](<README (1).md#change-the-presence-of-your-bot>)



## Installing

In npm

```
npm install syntx.js
```

In yarn

```
yarn add syntx.js
```

In pnpm

```
pnpm add syntx.js
```

### How to create a new client

#### Request the library

First, we must request `ERXClient` and `Intents` from the `syntx.js` library.

{% code lineNumbers="true" %}
```javascript
const { ERXClient, Intents } = require("syntx.js") 
```
{% endcode %}

#### Create the new client

Next, create a new `ERXClient` instance by passing in a configuration object with the necessary properties.

{% code lineNumbers="true" %}
```javascript
const client = new ERXClient({
    prefix: "!",
    intents: [Intents.All], // This can be changed by numbers. For example, all Discord intents in numbers are: 3276799
    token: "YOUR_DISCORD_BOT_TOKEN"
})
```
{% endcode %}



| OPTION    | TYPE           | DESCRIPTION                                             |
| --------- | -------------- | ------------------------------------------------------- |
| `prefix`  | string         | The symbol with which you will start all your commands. |
| `intents` | array / number | The number of intents the bot will have.                |
| `token`   | sting          | your bot token.                                         |

#### Run the bot

To run the client, we must use the `start` method.

{% code lineNumbers="true" %}
```javascript
client.start()
```
{% endcode %}

### Example using the command method

{% code lineNumbers="true" %}
```javascript
const { ERXClient, Intents } = require("syntx.js")

const client = new ERXClient({
    prefix: "!",
    intents: [Intents.All],
    token: "YOUR_DISCORD_BOT_TOKEN"
})

client.ready(() => {
    console.log(`Bot ${client.bot.user.username} ready.`)
})

client.command({
    name: "hi", // Command name.
    content: (message) => {
        message.channel.send(`Hi ${message.author.username}!`)
    }
})

client.start()
client.registerCommands()
```
{% endcode %}
