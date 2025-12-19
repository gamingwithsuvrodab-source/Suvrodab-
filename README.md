from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes, MessageHandler, filters, CallbackQueryHandler
import random

# ========================
# Bot Commands
# ========================

# /start কমান্ড
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    keyboard = [
        [InlineKeyboardButton("🎲 Roll Dice", callback_data='roll')],
        [InlineKeyboardButton("🐹 Hamster Facts", callback_data='fact')],
        [InlineKeyboardButton("🖼 Send Meme", callback_data='meme')],
        [InlineKeyboardButton("❓ Quiz Time", callback_data='quiz')]
    ]
    reply_markup = InlineKeyboardMarkup(keyboard)
    await update.message.reply_text(
        "হাই! আমি Hamster বট 🐹। তোমার জন্য মজা ফিচার আছে। নিচের বাটনে ক্লিক করো!",
        reply_markup=reply_markup
    )

# মেসেজ রেসপন্স (Text Echo)
async def echo(update: Update, context: ContextTypes.DEFAULT_TYPE):
    responses = [
        "😂 দারুন!", 
        "😎 সত্যি বলছো!",
        "🐹 আমি Hamster!",
        "😜 মজার কথা বলছো!",
        "🎉 মজা লাগছে!"
    ]
    await update.message.reply_text(random.choice(responses))

# Callback Query হ্যান্ডল (Inline Buttons)
async def button(update: Update, context: ContextTypes.DEFAULT_TYPE):
    query = update.callback_query
    await query.answer()
    
    if query.data == "roll":
        dice = random.randint(1, 6)
        await query.edit_message_text(f"🎲 তুমি {dice} পেলো! আবার চাইলে /start লিখো।")
    elif query.data == "fact":
        facts = [
            "Hamsters are nocturnal! 🌙",
            "Hamsters have cheek pouches! 🐹",
            "Hamsters can run up to 8 km in one night! 🏃",
            "Hamsters are great escape artists! 🏰",
            "A hamster's teeth never stop growing! 🦷"
        ]
        await query.edit_message_text(f"🐹 Fun Fact: {random.choice(facts)}")
    elif query.data == "meme":
        memes = [
            "https://i.imgur.com/1.png",
            "https://i.imgur.com/2.png",
            "https://i.imgur.com/3.png"
        ]
        await query.edit_message_text("🖼 দেখো, মেমে! (নিচের লিংক) " + random.choice(memes))
    elif query.data == "quiz":
        questions = [
            {"q": "Hamsters are nocturnal animals?", "a": "Yes"},
            {"q": "Hamsters can fly?", "a": "No"},
            {"q": "Hamsters store food in their cheeks?", "a": "Yes"}
        ]
        q = random.choice(questions)
        keyboard = [
            [InlineKeyboardButton("Yes", callback_data='quiz_yes')],
            [InlineKeyboardButton("No", callback_data='quiz_no')]
        ]
        reply_markup = InlineKeyboardMarkup(keyboard)
        context.user_data['quiz_answer'] = q['a']
        await query.edit_message_text(q['q'], reply_markup=reply_markup)
    elif query.data in ["quiz_yes", "quiz_no"]:
        answer = context.user_data.get('quiz_answer', "Yes")
        user_choice = "Yes" if query.data == "quiz_yes" else "No"
        if user_choice == answer:
            await query.edit_message_text(f"🎉 Correct! উত্তর: {answer}")
        else:
            await query.edit_message_text(f"❌ Wrong! সঠিক উত্তর: {answer}")

# ========================
# Bot Setup
# ========================
app = ApplicationBuilder().token("YOUR_BOT_TOKEN_HERE").build()

# Command Handlers
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, echo))
app.add_handler(CallbackQueryHandler(button))

# ========================
# Run Bot
# ========================
app.run_polling()
