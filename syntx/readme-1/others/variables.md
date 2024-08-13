---
description: Use variables in your bot to allow saving information for later use.
icon: box
---

# Variables

## table of Contents

* [Why use variabes?](variables.md#why-use-variables)
* [How to use variables](variables.md#how-to-use-variables)
* [How to create a variable](variables.md#how-to-create-a-variable)
* [How to set a value to a variable](variables.md#how-to-set-a-value-to-a-variable)\
  \- [How to set a local value](variables.md#how-to-set-a-local-value)\
  \- [How to create a server variable](variables.md#how-to-create-a-server-variable)\
  \- [How to set a global variable](variables.md#how-to-set-a-global-variable)
* [How to get the value of a variable](variables.md#how-to-get-the-value-of-a-variable)\
  \- [How to get the value of a local variable](variables.md#how-to-get-the-value-of-a-local-variable)\
  \- [How to get the value of a server variable](variables.md#how-to-get-the-value-of-a-server-variable)\
  \- [How to get the value of a global variable](variables.md#how-to-get-the-value-of-a-global-variable)

### Why use variables?

Generally, Discord bots use variables in their applications because these variables allow them to store any information related to a user or server, whether globally, locally, or server-specific.

Variables are crucial when creating advanced commands, such as an AFK command. With variables, you can determine if the current user is AFK or not, for example.

### How to use variables

First, you must export the `Var` module from the `syntx.js` library.

```javascript
const { Var } = require("syntx.js")
```

As a second step, you must enable the `variable` option when configuring your client.

```javascript
const client = new ERXClient({
    prefix: "!",
    intents: Intents.All,
    token: "...",
    variable: {
        enabled: true,
        folder: "./variables" // If "folder" is not provided, then one will be created.
    }
})
```

***

### How to create a variable

To create a variable, we must use the `new_variable` method in our code, here is an example:

```javascript
<client>.new_variable({
    name: "test",
    value: "Testing"
})
```



| OPTION  | TYPE             | REQUIRED |
| ------- | ---------------- | -------- |
| `name`  | string           | true     |
| `value` | string \| object | true     |

***

### How to set a value to a variable

To set the value of a variable, we must first know if we want to do it `local`, `server` or `global`.



| OPTION   | DESCRIPTION                                                                                                                                                                                                                                                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `local`  | By setting a local variable, you are instructing it to be stored within the user on the provided server. That is to say, the information associated with this variable will only be available and relevant within that specific server for that user.                                                                                                          |
| `server` | By setting a variable per server, you would be indicating that the value you set in said variable will be stored on the server, not on the users. That is, the entire server will have a value.                                                                                                                                                                |
| `global` | By setting a global variable, you would be instructing this variable to be set for the user provided globally, but if no user is provided, the variable will be set for all users using your bot. That is, if a user is configured, the value of this user will be affected on all servers. Otherwise, the value of all users using your bot will be affected. |

### How to set a local value

```javascript
Var.local.set({
    name: string,
    value: string | object,
    user: string,
    server: string
})
```

Let's say we create a variable called `discord`, where its value is `hello world`. So, if I want to change this value to something different for a specific user:

```javascript
Var.local.set({
    name: "discord",
    value: "Hi! :)",
    user: cmd.user.authorId(<message>)
    server: cmd.guild.id(<message>)
})
```

What this will do is change the value of the variable for the user running the command, but it will only change it on the current server. So if this user looks at the value of their variable on a different server, it will return `hello world` instead of `Hi! :)`.\
\
But also, you can review the values ​​of each user and on their respective server by opening the `.var` file created with the name of their variable.

***

### How to create a server variable

```javascript
Var.server.set({
    name: string,
    value: string | object,
    server: string
})
```

As in the previous example, let's say we have a variable called `discord`, the value of that variable is `hello world`. So, let's say that we want to change the value of that variable to `Hello!` for the entire server:

```javascript
Var.server.set({
    name: "discord",
    value: "Hello!",
    server: cmd.guild.id(<message>)
})
```

What this will do is: change the previous value of the variable which was `hello world` to its new value which is `Hello!`, only on the current server. If it is a different server, this will return a different result.

***

### How to set a global variable

```javascript
Var.global.set({
    name: string,
    value: string | object,
    user?: string
})
```

| OPTION  | TYPE             | REQUIRED |
| ------- | ---------------- | -------- |
| `name`  | string           | true     |
| `value` | string \| object | true     |
| `user`  | string           | false    |

Likewise, as in the previous example, we have a variable called `discord` whose value is `hello world`, but then we want to change that value to a different one:

#### No user specification

```javascript
Var.global.set({
    name: "discord",
    value: "Syntx!"
})
```

By not specifying a user, then you will change the variable globally. All users will be affected; at least they have previously had a custom value.

***

#### Specified user

```javascript
Var.global.set({
    name: "discord",
    value: "Syntx!",
    user: cmd.user.authorId(<message>)
})
```

When you specify a user, the only one affected will be the provided user. That is, the value of your variable will be changed globally only for the given user.

***

### How to get the value of a variable

The same, first we must know if it is `local`, `server` or `global`.

### How to get the value of a local variable

```javascript
Var.local.get({
    name: string,
    user: string,
    server: string
})
```

| OPTION   | TYPE   | REQUIRED |
| -------- | ------ | -------- |
| `name`   | string | true     |
| `user`   | string | true     |
| `server` | string | true     |

We must use `await` to be able to correctly obtain the result of the variable.

Let's say we have a variable called `example`, where its value is `hello`:

```javascript
client.command({
    name: "abc",
    content: async (msg) => {
        const get = await Var.local.get({
            name: "example",
            user: cmd.user.authorId(msg),
            server: cmd.guild.id(msg)
        })
        
        console.log(get) // It should return "hello"
    }
})
```

***

### How to get the value of a server variable

```javascript
Var.server.get({
    name: string,
    server: string
})
```

| OPTION   | TYPE   | REQUIRED |
| -------- | ------ | -------- |
| `name`   | string | true     |
| `server` | string | true     |

As in the previous example, in this one we must also use `await`.

Let's say we have a variable called `example`, which its value is `hello`

```javascript
client.command({
    name: "abc",
    content: async (msg) => {
        const get = await Var.server.get({
            name: "example",
            server: cmd.guild.id(msg)
        })
        
        console.log(get) // It should return "hello"
    }
})
```

***

### How to get the value of a global variable

```javascript
Var.global.get({
    name: string,
    user?: string
})
```

| OPTION | TYPE   | REQUIRED |
| ------ | ------ | -------- |
| `name` | string | true     |
| `user` | string | false    |

#### No user specified

Same thing, we have to use `await` to get the value correctly.

Let's say we have a variable called `example`, and value `hello`:

```javascript
client.command({
    name: "abc",
    content: async (msg) => {
        const get = await Var.global.get({
            name: "example"
        })
        
        console.log(get) // It should return "hello"
    }
})
```

What it will do is return `hello`, because since it was not given a user, it will return the value of the default (global) variable.

***

#### Specified user

Same thing, we have to use `await` to get the value correctly.

Let's say we have a variable called `example`, and value `hello`:

```javascript
client.command({
    name: "abc",
    content: async (msg) => {
        const get = await Var.global.get({
            name: "example",
            user: cmd.user.authorId(msg)
        })
        
        console.log(get) // It should return "hello"
    }
})
```

What it will do is return the value of the global variable of the specified user, in this case it is `hello`.

***

{% hint style="info" %}
In the example codes, I used `cmd.user.authorId` as well as `cmd.guild.id`. However, you can change this however you want. By directly providing a user and/or server ID, or using other methods.
{% endhint %}

{% hint style="warning" %}
It is important to use these functions when you have set up your client. Otherwise they won't work.
{% endhint %}
