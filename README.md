# Anime Telegram Bot
Simple Telegram bot that sends anime images.
const TelegramBot = require("node-telegram-bot-api");
const fetch = require("node-fetch");

const token = process.env.BOT_TOKEN;
const bot = new TelegramBot(token, { polling: true });

bot.onText(/\/start/, (msg) => {
  bot.sendMessage(
    msg.chat.id,
    "👋 Salom!\n🎌 Anime botga xush kelibsiz!",
    {
      reply_markup: {
        keyboard: [[{ text: "🎬 Anime rasm" }]],
        resize_keyboard: true
      }
    }
  );
});

bot.on("message", async (msg) => {
  if (msg.text === "🎬 Anime rasm") {
    const res = await fetch("https://api.waifu.pics/sfw/anime");
    const data = await res.json();
    bot.sendPhoto(msg.chat.id, data.url);
  }
});
