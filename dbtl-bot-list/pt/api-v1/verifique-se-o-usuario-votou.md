# Verifique se o usuário votou

<mark style="color:green;">`GET`</mark> `/api/v1/vote/users/:userID?bot=botID`

Verifique se um usuário votou no seu bot.

#### Respostas

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

### Exemplos

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
    if (message.content.startsWith('!checkvote')) { // Supondo que o comando seja ativado com !checkvote
        const botID = 'ID_DO_SEU_BOT';
        const authorID = message.author.id;

        let sentMessage;
        try {
            sentMessage = await message.channel.send('Aguarde...');
        } catch (error) {
            return;
        }

        try {
            const response = await fetch(`https://dbtl.erxproject.xyz/api/v1/vote/users/${authorID}?bot=${botID}`);
            const status = response.status;

            if (status === 200) {
                // Se o usuário votou
                try {
                    await sentMessage.delete();
                } catch (error) {
                }
                await message.channel.send('Obrigado por votar!.');
                // Código de reivindicação
            } else if (status === 404) {
                // Se o usuário não votou
                try {
                    await sentMessage.edit(`¡<@${authorID}> Você ainda não votou em mim!`);
                } catch (error) {
                    await message.channel.send(`¡<@${authorID}> Você ainda não votou em mim!`);
                }
            } else {
                try {
                    await sentMessage.edit(`<@${authorID}> Não foi possível conectar com o DBTL.`);
                } catch (error) {
                    await message.channel.send(`<@${authorID}> Não foi possível conectar com o DBTL.`);
                }
            }
        } catch (error) {
            await sentMessage.edit(`<@${authorID}> Erro...`);
        }
    }
});

client.login('TOKEN_DO_SEU_BOT');
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
    bot_id = 'SUA_ID_DO_BOT'  # Substitua pela ID do seu bot
    author_id = ctx.author.id

    # Envia a mensagem inicial "Aguarde..."
    sent_message = await ctx.send('Aguarde...')

    try:
        response = requests.get(f'https://dbtl.erxproject.xyz/api/v1/vote/users/{author_id}?bot={bot_id}')
        status = response.status_code

        if status == 200:
            # O usuário votou
            try:
                await sent_message.delete()
                # Seu código de reivindicação
            except discord.DiscordException:
                pass
            await ctx.send('Seu código de reivindicação...')
        elif status == 404:
            # O usuário não votou
            try:
                await sent_message.edit(content=f'<@{author_id}> Você ainda não votou em mim!')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> Você ainda não votou em mim!')
        else:
            try:
                await sent_message.edit(content=f'<@{author_id}> Não foi possível conectar ao DBTL.')
            except discord.DiscordException:
                await ctx.send(f'<@{author_id}> Não foi possível conectar ao DBTL.')
    except requests.RequestException:
        await sent_message.edit(content=f'<@{author_id}> Houve um erro ao conectar-se à API.')

bot.run('SEU_TOKEN_DO_BOT')
```
{% endtab %}

{% tab title="BDFD" %}
```javascript
$nomention
$async[dbtl]
$var[id;$sendMessage[Aguarde...;yes]]
$endasync

$await[dbtl]
$httpGet[https://dbtl.erxproject.xyz/api/v1/vote/users/$authorID?bot=$botID]
$if[$httpStatus==200]
$try
$deleteMessage[$channelID;$var[id]]
$catch
$endtry
Seu código de reivindicação...
$elseif[$httpStatus==404]
$try
$editMessage[$channelID;$var[id];<@$authorID> Você ainda não votou em mim!]
$catch
$sendMessage[<@$authorID> Você ainda não votou em mim!]
$endtry
$else
$try
$editMessage[$channelID;$var[id];<@$authorID> Não foi possível conectar ao DBTL.]
$catch
$sendMessage[<@$authorID> Não foi possível conectar ao DBTL.]
$endtry
$endif

```
{% endtab %}
{% endtabs %}
