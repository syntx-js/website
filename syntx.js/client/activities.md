---
icon: angle-right
---

# Activities

## Table of Content

* [Types of activities](activities.md#types-of-activities)
* [Types of states](activities.md#types-of-states)

You can add activities to your bot to make it look more attractive on Discord. This can be customized to your liking.

To add an activity to your bot, we must use the `presence` method in your code.

{% code lineNumbers="true" %}
```javascript
<client>.presence({
    time: number,
    activities: [
        {
            content: string,
            type: string
        }
    ],
    status: string
})
```
{% endcode %}

You can modify the values ​​of these to your liking. Here is an example:

{% code lineNumbers="true" %}
```javascript
client.presence({
    time: 60, // Cooldown time in seconds to switch to another activity
    activities: [
        { content: "Hello World!", type: "Playing" }
    ]
})
```
{% endcode %}

<figure><img src="../../.gitbook/assets/Captura de pantalla 2024-06-08 021639.png" alt="Result"><figcaption><p>Result</p></figcaption></figure>

***

### Types of activities

* Playing
* Watching
* Listening
* Competing

### Types of states

* online
* idle
* dnd

***

But if you want to add more activities, use the following structure:

{% code lineNumbers="true" %}
```javascript
client.command({
    time: 60,
    activities: [
        { content: "Hello World!", type: "Playing" }, // Activity 1
        { content: "I am created with Syntx.js!", type: "Playing" } // Activity 2
    ]
})
```
{% endcode %}
