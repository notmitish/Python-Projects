import discord
from discord.ext import commands

# Make sure to store your token securely (e.g., in an environment variable)
TOKEN = 'your-bot-token-here'

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='!', intents=intents)

# Replace this with the actual channel ID you want the bot to send messages to
TARGET_CHANNEL_ID = your_channel_id_here

@bot.event
async def on_ready():
    print(f'Logged in as {bot.user} (ID: {bot.user.id})')
    print('------')
    print('Bot is ready to send messages!')

def is_admin():
    def predicate(ctx):
        return ctx.author.guild_permissions.administrator
    return commands.check(predicate)

@bot.command(name='msg', help='Sends an embedded message to a specific channel')
@is_admin()
async def send_message(ctx, *, message: str):
    target_channel = bot.get_channel(TARGET_CHANNEL_ID)

    if target_channel is None:
        await ctx.send('The target channel was not found. Please check the channel ID.')
        return
    
    # You can customize the emoji here
    custom_emoji = f"<:emoji_name:emoji_id>"

    embed = discord.Embed(
        title=f"{custom_emoji}   In Depth Story",
        description=message,
        color=discord.Color.gold()
    )

    try:
        await target_channel.send(embed=embed)
        await ctx.send(f'Message successfully sent to {target_channel.mention}.')
    except discord.Forbidden:
        await ctx.send('Bot does not have permission to send messages to the target channel.')
    except discord.HTTPException as e:
        await ctx.send(f'Failed to send message due to an HTTP error: {e}')

if __name__ == "__main__":
    if TOKEN:
        bot.run(TOKEN)
    else:
        print("Error: Discord bot token not set.")
