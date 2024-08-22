# Verificar si un usuario votó

<mark style="color:green;">`GET`</mark> `/api/v1/vote/users/:userID?bot=botID`

Verifica si un usuario votó por su bot.

**Respuestas**

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

### Ejemplos

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
    if (message.content.startsWith('!checkvote')) { // Suponiendo que el comando se activa con !checkvote
        const botID = 'ID_DE_SU_BOT';
        const authorID = message.author.id;

        let sentMessage;
        try {
            sentMessage = await message.channel.send('Espere...');
        } catch (error) {
            return;
        }

        try {
            const response = await fetch(`https://dbtl.erxproject.xyz/api/v1/vote/users/${authorID}?bot=${botID}`);
            const status = response.status;

            if (status === 200) {
                // Si el usuario votó
                try {
                    await sentMessage.delete();
                } catch (error) {
                }
                await message.channel.send('¡Gracias por votar!.');
                // Código de reclamación
            } else if (status === 404) {
                // Si el usuario no votó
                try {
                    await sentMessage.edit(`¡<@${authorID}> Aún no votas por mi!`);
                } catch (error) {
                    await message.channel.send(`¡<@${authorID}> Aún no votas por mi!`);
                }
            } else {
                try {
                    await sentMessage.edit(`<@${authorID}> No me pude conectar con DBTL.`);
                } catch (error) {
                    await message.channel.send(`<@${authorID}> No me pude conectar con DBTL.`);
                }
            }
        } catch (error) {
            await sentMessage.edit(`<@${authorID}> Error...`);
        }
    }
});

client.login('TOKEN_DE_SU_BOT');

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
    print(f'Conectado como {bot.user}')

@bot.command()
async def checkvote(ctx):
    bot_id = 'TU_ID_DEL_BOT'  # Reemplaza con la ID de tu bot
    author_id = ctx.author.id

    # Envía el mensaje inicial "Espera..."
    sent_message = await ctx.send('Espera...')

    try:
        response = requests.get(f'https://dbtl.erxproject.xyz/api/v1/vote/users/{author_id}?bot={bot_id}')
        status = response.status_code

        if status == 200:
            # El usuario ha votado
            try:
                await sent_message.delete()
                # Tu código de reclamación
            except discord.DiscordException:
                pass
            await ctx.send('Tu código de reclamación...')
        elif status == 404:
            # El usuario no ha votado
            try:
                await sent_message.edit(content=f'<@{author_id}> ¡Aún no has votado por mí!')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> ¡Aún no has votado por mí!')
        else:
            try:
                await sent_message.edit(content=f'<@{author_id}> No se pudo conectar a DBTL.')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> No se pudo conectar a DBTL.')
    except requests.RequestException:
        await sent_message.edit(content=f'<@{author_id}> Hubo un error al conectarse a la API.')

bot.run('TU_TOKEN_DEL_BOT')
```
{% endtab %}

{% tab title="BDFD" %}
```javascript
$nomention
$async[dbtl]
$var[id;$sendMessage[Espera...;yes]]
$endasync

$await[dbtl]
$httpGet[https://dbtl.erxproject.xyz/api/v1/vote/users/$authorID?bot=$botID]
$if[$httpStatus==200]
$try
$deleteMessage[$channelID;$var[id]]
$catch
$endtry
Tu código de reclamación...
$elseif[$httpStatus==404]
$try
$editMessage[$channelID;$var[id];<@$authorID> ¡Aún no has votado por mí!]
$catch
$sendMessage[<@$authorID> ¡Aún no has votado por mí!]
$endtry
$else
$try
$editMessage[$channelID;$var[id];<@$authorID> No se pudo conectar a DBTL.]
$catch
$sendMessage[<@$authorID> No se pudo conectar a DBTL.]
$endtry
$endif
```
{% endtab %}
{% endtabs %}
