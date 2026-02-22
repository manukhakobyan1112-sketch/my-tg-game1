import asyncio
from aiogram import Bot, Dispatcher, types
from aiogram.filters import Command
from aiogram.types import WebAppInfo, InlineKeyboardMarkup, InlineKeyboardButton

# ТОКЕН ОТ BOTFATHER
TOKEN = "ВСТАВЬ_СЮДА_СВОЙ_ТОКЕН"

# ТВОЯ ССЫЛКА С GITHUB
GAME_URL = "https://manukhakobyan1112-sketch.github.io/my-tg-game/"

bot = Bot(token=TOKEN)
dp = Dispatcher()

@dp.message(Command("start"))
async def cmd_start(message: types.Message):
    # Создаем кнопку для запуска игры
    markup = InlineKeyboardMarkup(inline_keyboard=[
        [
            InlineKeyboardButton(
                text="Играть в Монетки 💰", 
                web_app=WebAppInfo(url=GAME_URL)
            )
        ]
    ])
    
    await message.answer(
        f"Привет, {message.from_user.first_name}! 👋\n"
        "Нажми на кнопку ниже, чтобы запустить игру прямо здесь!",
        reply_markup=markup
    )

async def main():
    print("🚀 Бот запущен! Иди в Telegram и пиши /start")
    await dp.start_polling(bot)

if __name__ == "__main__":
    try:
        asyncio.run(main())
    except Exception as e:
        print(f"Ошибка: {e}")
        <!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>TG Clicker</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body {
            font-family: sans-serif;
            background-color: #121212;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        .coin {
            width: 200px;
            height: 200px;
            background: linear-gradient(145deg, #ffcc00, #ff9900);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 80px;
            cursor: pointer;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5), 0 0 20px rgba(255,204,0,0.3);
            user-select: none;
            transition: transform 0.1s;
        }
        .coin:active {
            transform: scale(0.95);
        }
        .score-text {
            font-size: 32px;
            margin-bottom: 20px;
        }
    </style>
</head>
<body>

    <div class="score-text">Счёт: <span id="score">0</span></div>
    <div class="coin" id="clicker">💰</div>

    <script>
        const tg = window.Telegram.WebApp;
        const scoreElement = document.getElementById('score');
        const clicker = document.getElementById('clicker');
        
        let score = 0;

        tg.expand(); // Развернуть на весь экран

        clicker.addEventListener('click', () => {
            score++;
            scoreElement.innerText = score;
            
            // Вибрация при нажатии
            if (tg.HapticFeedback) {
                tg.HapticFeedback.impactOccurred('light');
            }
        });

        // Сообщаем Telegram, что приложение готово
        tg.ready();
    </script>
</body>
</html>
