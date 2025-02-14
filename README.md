<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>С Днём Святого Валентина! ❤️</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            margin: 0;
            padding: 0;
            height: 100vh;
            overflow: hidden;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        h1 {
            color: #fff;
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        .buttons {
            display: flex;
            gap: 100px; /* Расстояние между кнопками */
            margin-top: 20px;
        }
        .buttons button {
            padding: 15px 30px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            color: white;
            transition: transform 0.2s ease;
        }
        #yesButton {
            background-color: #ff6f61;
        }
        #noButton {
            background-color: #6b5b95;
            position: static; /* Убираем absolute, чтобы кнопка была в потоке */
        }
        .buttons button:active {
            transform: scale(0.95);
        }
        .falling-cats {
            position: absolute;
            top: -100px;
            width: 50px;
            height: 50px;
            background-size: cover;
            animation: fall linear infinite;
        }
        @keyframes fall {
            0% { transform: translateY(-100px); }
            100% { transform: translateY(100vh); }
        }

        /* Анимация для кота, который появляется снизу */
        .final-cat {
            position: absolute;
            bottom: -200px; /* Начальная позиция за пределами экрана */
            width: 150px;
            height: 150px;
            background-image: url('https://stickermaker.s3.eu-west-1.amazonaws.com/storage/uploads/sticker-pack/3-1618604576/sticker_4.png?ae9fdb16c61783155c0e1ed3f5722212&d=200x200');
            background-size: cover;
            animation: slideUp 2s ease forwards; /* Анимация выезда */
        }
        @keyframes slideUp {
            0% { bottom: -200px; }
            100% { bottom: 100px; } /* Конечная позиция (выше, чем было) */
        }
    </style>
</head>
<body>
    <h1 id="question">Ты моя принцесса? ❤️</h1>
    <div class="buttons">
        <button id="yesButton">Да</button>
        <button id="noButton">Нет</button>
    </div>

    <script>
        const questions = [
            "Ты моя принцесса? ❤️",
            "А ты меня любишь?",
            "А ты со мной будешь?",
            "И будем мы вместе?"
        ];
        
        const yesButton = document.getElementById('yesButton');
        const noButton = document.getElementById('noButton');
        const questionElement = document.getElementById('question');
        let currentQuestion = 0;

        // Функция для обновления вопроса
        const updateQuestion = () => {
            questionElement.textContent = questions[currentQuestion];
        };

        // Обработчик для кнопки "Да"
        yesButton.addEventListener('click', () => {
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                updateQuestion();
            } else {
                questionElement.textContent = "С тобой навсегда ❤️";
                yesButton.style.display = 'none';
                noButton.style.display = 'none';

                // Создаем кота, который появляется снизу
                const finalCat = document.createElement('div');
                finalCat.classList.add('final-cat');
                document.body.appendChild(finalCat);
            }
        });

        // Обработчик для кнопки "Нет" (убегает)
        noButton.addEventListener('mouseover', () => {
            const x = Math.random() * (window.innerWidth - noButton.offsetWidth);
            const y = Math.random() * (window.innerHeight - noButton.offsetHeight);
            noButton.style.position = 'absolute'; // Переключаем на absolute для перемещения
            noButton.style.left = `${x}px`;
            noButton.style.top = `${y}px`;
        });

        // Инициализация первого вопроса
        updateQuestion();

        // Массив с URL стикеров котиков
        const catStickers = [
            'https://yt3.googleusercontent.com/ytc/AIf8zZTkPm56NKejsc_jHhr0g6desEcNq30Z2NtRZWitEw=s900-c-k-c0x00ffffff-no-rj',
            'https://data.chpic.su/stickers/p/PinkPussyCat/PinkPussyCat_002.webp',
            // Добавьте больше URL стикеров, если нужно
        ];

        // Динамическое создание котиков
        function createCat() {
            const cat = document.createElement('div');
            cat.classList.add('falling-cats');
            cat.style.left = `${Math.random() * window.innerWidth}px`;
            cat.style.animationDuration = `${Math.random() * 4 + 3}s`; // Замедляем падение
            cat.style.backgroundImage = `url('${catStickers[Math.floor(Math.random() * catStickers.length)]}')`;
            document.body.appendChild(cat);

            // Удаляем котика после завершения анимации
            setTimeout(() => {
                cat.remove();
            }, 8000); // Увеличено время удаления
        }

        // Создаем котиков реже (каждые 500 мс)
        setInterval(createCat, 500);
    </script>
</body>
</html>
