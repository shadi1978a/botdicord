from settings import settings
import discord
from gen_password import gen_password
from gem_emoji import gen_emodji

# la variabile intents contiene i permessi al bot
intents = discord.Intents.default()
# abilita il permesso a leggere i contenuti dei messaggi
intents.message_content = True
# crea un bot e passa gli indents
client = discord.Client(intents=intents)


@client.event
async def on_ready():
    print(f'Abbiamo fatto l\'accesso come {client.user}')


@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith("$password"):
        await message.channel.send("Password generata: " + gen_password(10))
    elif message.content.startswith("$ciao"):
        await message.channel.send("Ciao! " + gen_emodji())
    elif message.content.startswith("$arrivederci"):
        await message.channel.send("\U0001f642")
    elif message.content.startswith("$cmv?"):
        await message.channel.send("In ottima forma oggi, grazie" + gen_emodji())
    else:
        await message.channel.send(
            "Non è possibile elaborare questo comando, mi dispiace!"
        )


client.run(settings["TOKEN"])
