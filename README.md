import discord
from discord.ext import commands
import os, random
import requests

# Создаем объект бота и устанавливаем префикс команд
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix='/go', intents = intents)

# Создаем словарь с информацией о сортировке отходов
отходы = {
    "бумага": "перерабатывать",
    "пластик": "перерабатывать",
    "стекло": "перерабатывать",
    "металл": "перерабатывать",
    "пластиковые бутылки": "перерабатывать",
    "компьютеры": "перерабатывать",
    "органические отходы": "выбрасывать",
    "одежда": "перерабатывать",
}

# Определяем команду для сортировки отходов
@bot.command()
async def сортировка(ctx, предмет: str):
    предмет = предмет.lower()
    if предмет in отходы:
        действие = отходы[предмет]
        if действие == "перерабатывать":
            await ctx.send(f"Отнесите '{предмет}' на переработку.")
        elif действие == "выбрасывать":
            await ctx.send(f"Выбросите '{предмет}' в обычную урну.")
    else:
        await ctx.send(f"Мы не знаем, что делать с '{предмет}'.")

# Запускаем бота с помощью токена
TOKEN = 'MTE0NDk1NzUxOTc0ODQwNzI5Ng.G2xtOl.LLAGBXFCfcylJyG1Q35VGH6MgyRXHOgK1xgvGE'
bot.run(TOKEN)
