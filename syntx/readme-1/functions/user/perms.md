---
description: >-
  Returns true if the user is granted permissions; otherwise it will return
  false.
icon: square-check
---

# perms

### Usage

```javascript
cmd.user.perms({ userID, permissions }, message)
```

| OPTION       | TYPE     | REQUIRED |
| ------------ | -------- | -------- |
| `userID`     | string   | true     |
| `permission` | string   | true     |
| `message`    | callback | true     |

**Note:** You can use `&&` as well as `||` to add more permissions.

### Examples

```javascript
client.command({
    name: "perms1",
    content: async (msg) => {
        const p = await cmd.user.perms({ userID: cmd.user.authorId(msg), permissions: "SEND_MESSAGES" }, msg) // If the user has the permission, it will return true
        cmd.message.send({
            text: `${p}`
        }, msg)
    }
})

client.command({
    name: "perms2",
    content: async (msg) => {
        const p = await cmd.user.perms({ userID: cmd.user.authorId(msg), permissions: "SEND_MESSAGES && MANAGE_CHANNELS" }, msg) // If the user has both permissions, it will return true; otherwise false
        cmd.message.send({
            text: `${p}`
        }, msg)
    }
})

client.command({
    name: "perms3",
    content: async (msg) => {
        const p = await cmd.user.perms({ userID: cmd.user.authorId(msg), permissions: "SEND_MESSAGES || MANAGE_CHANNELS" }, msg) // If the user contains any of the 2 permissions it will return true, but if it does not have any it will return false
        cmd.message.send({
            text: `${p}`
        }, msg)
    }
})
```

### Permission list

* `CREATE_INSTANT_INVITE`
* `KICK_MEMBERS`
* `BAN_MEMBERS`
* `ADMINISTRATOR`
* `MANAGE_CHANNELS`
* `MANAGE_GUILD`
* `ADD_REACTIONS`
* `VIEW_AUDIT_LOG`
* `PRIORITY_SPEAKER`
* `STREAM`
* `VIEW_CHANNEL`
* `SEND_MESSAGES`
* `SEND_TTS_MESSAGES`
* `MANAGE_MESSAGES`
* `EMBED_LINKS`
* `ATTACH_FILES`
* `READ_MESSAGE_HISTORY`
* `MENTION_EVERYONE`
* `USE_EXTERNAL_EMOJIS`
* `VIEW_GUILD_INSIGHTS`
* `CONNECT`
* `SPEAK`
* `MUTE_MEMBERS`
* `DEAFEN_MEMBERS`
* `MOVE_MEMBERS`
* `USE_VAD`
* `CHANGE_NICKNAME`
* `MANAGE_NICKNAMES`
* `MANAGE_ROLES`
* `MANAGE_WEBHOOKS`
* `MANAGE_EMOJIS_AND_STICKERS`
* `USE_APPLICATION_COMMANDS`
* `REQUEST_TO_SPEAK`
* `MANAGE_THREADS`
* `CREATE_PUBLIC_THREADS`
* `CREATE_PRIVATE_THREADS`
* `USE_EXTERNAL_STICKERS`
* `SEND_MESSAGES_IN_THREADS`
* `USE_EMBEDDED_ACTIVITIES`
* `MODERATE_MEMBERS`
