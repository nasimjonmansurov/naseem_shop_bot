import telebot
from telebot import types

TOKEN = "BOT_TOKENINGNI_BU_YERGA_YOZ"
bot = telebot.TeleBot(TOKEN)

# NASEEM SHOP mahsulotlari
products = {
    "1": {"name": "👕 Futbolka - 150 somon", "price": 150},
    "2": {"name": "👖 Shim - 250 somon", "price": 250},
    "3": {"name": "👟 Krossovka - 400 somon", "price": 400}
}

@bot.message_handler(commands=['start'])
def start(message):
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    markup.add("🛍 Mahsulotlar", "📞 Aloqa")
    bot.send_message(message.chat.id, "Assalomu alaykum! NASEEM SHOP ga xush kelibsiz! 🎉\n\nMahsulot tanlang:", reply_markup=markup)

@bot.message_handler(func=lambda m: m.text == "🛍 Mahsulotlar")
def show_products(message):
    markup = types.InlineKeyboardMarkup()
    for id, p in products.items():
        markup.add(types.InlineKeyboardButton(p["name"], callback_data=id))
    bot.send_message(message.chat.id, "Bizning mahsulotlar:", reply_markup=markup)

@bot.callback_query_handler(func=lambda call: True)
def callback(call):
    prod = products[call.data]
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("✅ Buyurtma berish", callback_data=f"order_{call.data}"))
    bot.send_message(call.message.chat.id, f"Siz tanladingiz:\n{prod['name']}\n\nBuyurtma berish uchun bosing:", reply_markup=markup)

@bot.message_handler(func=lambda m: m.text == "📞 Aloqa")
def contact(message):
    bot.send_message(message.chat.id, "📞 Admin: @naseem_admin\n📍 Manzil: Dushanbe")

@bot.callback_query_handler(func=lambda c: c.data.startswith("order_"))
def order(c):
    prod = products[c.data.split("_")[1]]
    bot.send_message(c.message.chat.id, f"✅ Buyurtmangiz qabul qilindi!\n{prod['name']}\nTez orada admin siz bilan bog'lanadi!")
    bot.send_message(c.message.chat.id, "Rahmat! 🙏")

bot.infinity_polling()
