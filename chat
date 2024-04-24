from pyrogram import Client, filters
from pyrogram.types import Message

# Initialize your Pyrogram client with your bot token and other details
app = Client(
    "my_chatbot",
    bot_token="7123013710:AAHPo-adn_uC-sDV_KYm3ZK1P32CRrK_Hqc",
    api_id=12799559,  # Your API ID
    api_hash="077254e69d93d08357f25bb5f4504580"
)

# Function to handle chatbot functionality
@app.on_message(
    filters.text
    & filters.reply
    & ~filters.bot
    & ~filters.via_bot
    & ~filters.forwarded
)
async def chatbot_talk(_, message: Message):
    db = await check_chatbot()
    if message.chat.id not in db["bot"]:
        return
    if not message.reply_to_message:
        return
    if not message.reply_to_message.from_user:
        return
    if message.reply_to_message.from_user.id != BOT_ID:
        return
    await type_and_send(message)

# Command to display bot features
@app.on_message(filters.command("start"))
async def start_command(_, message: Message):
    features_message = (
        "Hi there! I am a chatbot designed to respond to messages when replied to the bot.\n\n"
        "Simply reply to any message with me, and I will respond accordingly.\n\n"
        "I am always active in this chat, ready to assist you!"
    )
    await message.reply_text(features_message)

# Run the bot
app.run()
