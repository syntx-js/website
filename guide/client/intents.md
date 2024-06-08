# Intents

## Table of Content

* [Intent list](intents.md#intent-list)
* [How to enter an intent](intents.md#how-to-enter-an-intent)
* [Quick intents](intents.md#quick-intents)

Another crucial component for your bot's functionality is the intents. Intents help the bot, for example, to read messages and thereby execute specific commands. They also allow access to server information, such as the number of members and the creation date.



## Intent list

* `Guilds`
* `Guilds GuildMembers`
* `GuildBans`
* `GuildEmojisAndStickers`
* `GuildIntegrations`
* `GuildWebhooks`
* `GuildInvites`
* `GuildVoiceStates`
* `GuildPresences`
* `GuildMessages`
* `GuildMessageReactions`
* `GuildMessageTyping`
* `DirectMessages`
* `DirectMessageReactions`
* `DirectMessageTyping`
* `MessageContent`
* `GuildScheduledEvents`
* `AutoModerationConfiguration`
* `AutoModerationExecution`

***

### How to enter an intent

First, we require `Intents` and `ERXClient`from the `syntx.js` library

{% code lineNumbers="true" %}
```javascript
const { ERXClient, Intents } = require("syntx.js")
```
{% endcode %}

Then we will create a new client.

{% code lineNumbers="true" %}
```javascript
const client = new ERXClient({})
```
{% endcode %}

After adding our client, we must add the "intents" body, where we will put the intents that your bot needs as a value within an array. Below is an example that adds the intents necessary for your bot's to function properly.

{% code lineNumbers="true" %}
```javascript
const client = new ERXClient({
    intents: [Intents.Guilds, Intents.GuildMessages, Intents.MessageContent]
})
```
{% endcode %}

If you like, you can also add number-based intents. To do this, you must enter an [intent calculator](https://discord-intents-calculator.vercel.app/) and choose the intents you want.

{% code lineNumbers="true" %}
```javascript
// Example
const client = new ERXClient({
    intents: 33281
})
```
{% endcode %}



| OPTION    | TYPE           |
| --------- | -------------- |
| `intents` | array / number |

***

## Quick intents

Yes, that's right, Quick Intents. But what is it for? Quick intents are used to avoid having to write the intents your bot needs 1x1. This option adds these intents more quickly.

### List

* `All`\
  Add absolutely all intents.
* `Fast`\
  Add the basic intents for your bot functionality.

#### All

{% code lineNumbers="true" %}
```diff
const client = new ERXClient({
-    intents: [Intents.Guilds, Intents.GuildMembers, Intents.GuildBans, Intents.GuildEmojisAndStickers, Intents.GuildIntegrations, Intents.GuildWebhooks, Intents.GuildInvites, Intents.GuildVoiceStates, Intents.GuildPresences, Intents.GuildMessages, Intents.GuildMessageReactions, Intents.GuildMessageTyping, Intents.DirectMessages, Intents.DirectMessageReactions, Intents.DirectMessageTyping, Intents.MessageContent, Intents.GuildScheduledEvents, Intents.AutoModerationConfiguration, Intents.AutoModerationExecution]
+    intents: [Intents.All]
})
```
{% endcode %}

#### Fast

{% code lineNumbers="true" %}
```diff
const client = new ERXClient({
-    intents: [Intents.Guilds, Intents.MessageContent, Intents.GuildMessages, Intents.GuildMembers]
+    intents: [Intents.Fast]
})
```
{% endcode %}
