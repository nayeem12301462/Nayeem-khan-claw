import anthropic
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes

TELEGRAM_TOKEN = "8899282752:AAFbTUdGUditRneqCWT3M_fSb8138Syr4B8"
ANTHROPIC_API_KEY = "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"

client = anthropic.Anthropic(api_key=ANTHROPIC_API_KEY)

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("আমি Claude AI Assistant!")

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_message = update.message.text
    message = client.messages.create(
        model="claude-haiku-4-5-20251001",
        max_tokens=1024,
        messages=[{"role": "user", "content": user_message}]
    )
    await update.message.reply_text(message.content[0].text)

app = ApplicationBuilder().token(TELEGRAM_TOKEN).build()
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
app.run_polling()
