---
icon: robot
description: Options of our client.
---

# Client

<pre class="language-javascript"><code class="lang-javascript"><strong>const { ERXClient } = require("syntx.js")
</strong><strong>
</strong><strong>const client = new ERXClient({
</strong>    prefix: string,
    intents: string,
    token: string,
    variable?: {
        enabled: boolean,
        folder: string
    }
})
</code></pre>

| OPTION     | TYPE    | RQUIRED |
| ---------- | ------- | ------- |
| `prefix`   | string  | true    |
| `intents`  | string  | true    |
| `token`    | string  | true    |
| `variable` | object  | false   |
| `enabled`  | boolean | false   |
| `folder`   | string  | false   |
