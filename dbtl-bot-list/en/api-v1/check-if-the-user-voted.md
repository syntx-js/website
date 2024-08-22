# Check if the user voted

<mark style="color:green;">`GET`</mark> `/api/v1/vote/users/:userID?bot=botID`

Check if the user voted for your bot.

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "vote": boolean,
  "timestamp": number,
  "expired": boolean,
  "expiryTime": string
}
```
{% endtab %}

{% tab title="404" %}
```json
{
  "error": "This user has not voted for this bot"
}
```
{% endtab %}

{% tab title="500" %}
```json
{
  "error": "Internal Server Error"
}
```
{% endtab %}
{% endtabs %}

### Examples



{% tabs %}
{% tab title="JavaScript" %}
```javascript
const { Client, GatewayIntentBits, EmbedBuilder } = require('discord.js');
const fetch = require('node-fetch');

const client = new Client({
    intents: [
        GatewayIntentBits.Guilds,
        GatewayIntentBits.GuildMessages,
        GatewayIntentBits.MessageContent,
    ]
});

client.on('messageCreate', async (message) => {
    if (message.content.startsWith('!checkvote')) { // Assuming the command is triggered with !checkvote
        const botID = 'YOUR_BOT_ID';
        const authorID = message.author.id;

        let sentMessage;
        try {
            sentMessage = await message.channel.send('Wait...');
        } catch (error) {
            return;
        }

        try {
            const response = await fetch(`https://dbtl.erxproject.xyz/api/v1/vote/users/${authorID}?bot=${botID}`);
            const status = response.status;

            if (status === 200) {
                // User has voted
                try {
                    await sentMessage.delete();
                } catch (error) {
                }
                await message.channel.send('Thanks for voting!');
                // Your claim code
            } else if (status === 404) {
                // User has not voted
                try {
                    await sentMessage.edit(`<@${authorID}> You haven't voted for me yet!`);
                } catch (error) {
                    await message.channel.send(`<@${authorID}> You haven't voted for me yet!`);
                }
            } else {
                try {
                    await sentMessage.edit(`<@${authorID}> Could not connect to DBTL.`);
                } catch (error) {
                    await message.channel.send(`<@${authorID}> Could not connect to DBTL.`);
                }
            }
        } catch (error) {
            await sentMessage.edit(`<@${authorID}> There was an error connecting to the API.`);
        }
    }
});

client.login('YOUR_BOT_TOKEN');

```
{% endtab %}

{% tab title="Python" %}
```python
import discord
import requests
from discord.ext import commands

intents = discord.Intents.default()
intents.messages = True
intents.guilds = True

bot = commands.Bot(command_prefix='!', intents=intents)

@bot.event
async def on_ready():
    print(f'Logged in as {bot.user}')

@bot.command()
async def checkvote(ctx):
    bot_id = 'YOUR_BOT_ID'  # Replace with your bot's ID
    author_id = ctx.author.id

    # Send initial "Wait..." message
    sent_message = await ctx.send('Wait...')

    try:
        response = requests.get(f'https://dbtl.erxproject.xyz/api/v1/vote/users/{author_id}?bot={bot_id}')
        status = response.status_code

        if status == 200:
            # User has voted
            try:
                await sent_message.delete()
            except discord.DiscordException:
                pass
            await ctx.send('Thanks for voting!')
            # Your claim code
        elif status == 404:
            # User has not voted
            try:
                await sent_message.edit(content=f'<@{author_id}> You haven\'t voted for me yet!')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> You haven\'t voted for me yet!')
        else:
            try:
                await sent_message.edit(content=f'<@{author_id}> Could not connect to DBTL.')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> Could not connect to DBTL.')
    except requests.RequestException:
        await sent_message.edit(content=f'<@{author_id}> There was an error connecting to the API.')

bot.run('YOUR_BOT_TOKEN')

```
{% endtab %}

{% tab title="BDFD" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>$nomention
</strong><strong>$async[dbtl]
</strong>$var[id;$sendMessage[Wait...;yes]]
$endasync

$await[dbtl]
$httpGet[https://dbtl.erxproject.xyz/api/v1/vote/users/$authorID?bot=$botID]
$if[$httpStatus==200]
$try
$deleteMessage[$channelID;$var[id]]
$catch
$endtry
Your claim code...
$elseif[$httpStatus==404]
$try
$editMessage[$channelID;$var[id];&#x3C;@$authorID> You haven't voted for me yet!]
$catch
$sendMessage[&#x3C;@$authorID> You haven't voted for me yet!]
$endtry
$else
$try
$editMessage[$channelID;$var[id];&#x3C;@$authorID> Could not connect to DBTL.]
$catch
$sendMessage[&#x3C;@$authorID> Could not connect to DBTL.]
$endtry
$endif
</code></pre>
{% endtab %}
{% endtabs %}
