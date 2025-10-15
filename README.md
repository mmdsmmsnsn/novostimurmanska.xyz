# novostimurmanska.xyz
новости великой мурманской депржави 

<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Новости Мууурманска — Фронт "Корова vs Свинья"</title>
    <!-- Загрузка Tailwind CSS и шрифта Inter -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        /* Стиль для общего вида */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f3e8; /* Светлый пастельный фон */
            color: #3b281f;
            transition: all 0.3s ease; /* Для плавного перехода в режим доступности */
        }
        .container {
            max-width: 1280px;
        }
        /* Стиль для Карты Боевых Действий (Canvas) */
        #warMapCanvas {
            display: block;
            width: 100%;
            border-radius: 12px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            margin-top: 1rem;
        }
        /* Стиль для Графика Биржи */
        #stockChartCanvas {
            display: block;
            width: 100%;
            height: 300px;
            border-radius: 12px;
            background-color: #f9f9f9;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }
        /* Анимация для кнопок-вкладок */
        .tab-button {
            transition: all 0.3s ease;
            box-shadow: 0 4px #e5a400; /* Тень под кнопкой */
            white-space: nowrap; /* Не переносить текст */
        }
        .tab-button:hover:not(.active) {
            transform: translateY(-2px);
            box-shadow: 0 6px #e5a400;
        }
        .tab-button.active {
            transform: translateY(2px);
            box-shadow: none; /* "Нажатый" вид */
            background-color: #e5a400 !important;
        }
        /* Стиль для кнопки ТГК */
        #tgk-button {
            transition: transform 0.2s, box-shadow 0.2s;
        }
        #tgk-button:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 30px -5px rgba(26, 153, 230, 0.5);
        }
        /* Стиль для мини-игры */
        #milk-button {
            transition: transform 0.1s;
        }
        #milk-button:active {
            transform: scale(0.95);
        }
        
        /* === РЕЖИМ ДОСТУПНОСТИ (Accessibility Mode - Визуальный Брайль) === */
        .accessibility-mode {
            /* Устанавливаем моноширинный шрифт для символов Брайля */
            font-family: 'Inter', sans-serif, monospace; 
            font-size: 1.5rem; /* Значительно увеличиваем шрифт */
            line-height: 1.8;
            background-color: #000000 !important;
            color: #ffffff !important;
        }
        .accessibility-mode .text-white, .accessibility-mode .text-yellow-900, .accessibility-mode .text-gray-700, .accessibility-mode .text-gray-500 {
            color: #ffffff !important;
        }
        .accessibility-mode .bg-white, .accessibility-mode .bg-gray-100 {
            background-color: #333333 !important;
            border: 2px solid #ffff00 !important;
            box-shadow: none !important;
        }
        .accessibility-mode .tab-button, .accessibility-mode #tgk-button, .accessibility-mode #milk-button, .accessibility-mode .bg-blue-500, .accessibility-mode .bg-green-600, .accessibility-mode .bg-red-600, .accessibility-mode .bg-gray-500 {
            border: 3px solid #ffff00 !important;
            background-color: #000000 !important;
            color: #ffff00 !important;
            box-shadow: none !important;
        }
        .accessibility-mode .active {
            background-color: #ffff00 !important;
            color: #000000 !important;
        }

    </style>
</head>
<body class="min-h-screen">

    <div class="container mx-auto p-4 md:p-8">
        <!-- Шапка -->
        <header class="text-center mb-8 bg-yellow-500/90 p-4 rounded-xl shadow-xl">
            <!-- Кнопка смены языка/режима -->
            <div class="flex justify-end mb-4">
                 <button onclick="toggleLanguageMode()" id="lang-toggle" class="bg-gray-700 text-white font-semibold py-2 px-4 rounded-full text-sm hover:bg-gray-800 transition-colors">
                    ⠓⠕⠃ ⠃⠗⠁⠃⠇⠕ ⠴ **Режим Брайля**
                </button>
            </div>

            <h1 class="text-4xl md:text-6xl font-extrabold text-white tracking-tight">
                🐮 Новости Мууурманска 🐄
            </h1>
            <p class="text-xl text-yellow-900 mt-2 font-semibold">Город Коров. Серьезные события, вызывающие улыбку.</p>
        </header>

        <!-- Навигация / Вкладки -->
        <nav class="flex justify-center flex-wrap gap-2 mb-8">
            <button onclick="showView('news')" id="tab-news" class="tab-button active bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                📰 Новости
            </button>
            <button onclick="showView('stock')" id="tab-stock" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                📈 Биржа Муу
            </button>
            <button onclick="showView('weather')" id="tab-weather" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                ☀️ Мууу-Прогноз
            </button>
             <button onclick="showView('hall')" id="tab-hall" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                🏆 Зал Славы
            </button>
            <button onclick="showView('games')" id="tab-games" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                🕹️ Мини-игры
            </button>
            <button onclick="showView('war')" id="tab-war" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-4 rounded-xl text-md hover:bg-yellow-500">
                ⚔️ Боевые действия
            </button>
        </nav>

        <!-- Кнопка Telegram -->
        <div class="flex justify-center mb-8">
            <a id="tgk-button" href="https://t.me/NovostiMyyyrmanska" target="_blank" class="flex items-center space-x-2 bg-blue-500 text-white font-extrabold py-3 px-8 rounded-full text-xl shadow-lg shadow-blue-300/50">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.35 6.64l-2.8 1.94 1.15 3.52c.07.24-.03.5-.24.6l-1.99 1.45c-.2.15-.46.15-.65 0l-.82-.63c-.1-.08-.24-.08-.33 0l-2.43 1.86c-.1.08-.2.12-.31.12-.13 0-.25-.04-.36-.12-.22-.16-.3-.44-.19-.7L8.9 9.3c.09-.27-.06-.55-.33-.64L4.85 7.49c-.29-.09-.59.07-.68.37-.09.3.07.6.37.69l12 3.6c.27.08.55-.07.64-.34l1.2-3.72c.1-.32-.08-.66-.4-.76z"/>
                </svg>
                <span>Наш ТГК — Канал Мууурманских Новостей</span>
            </a>
        </div>

        <!-- Сообщение о статусе (замена alert) -->
        <div id="status-message-box" class="fixed top-0 left-1/2 -translate-x-1/2 mt-4 p-4 bg-blue-100 border border-blue-400 text-blue-700 rounded-lg shadow-xl z-50 hidden transition-opacity duration-300 opacity-0">
            <p id="status-message"></p>
        </div>


        <!-- Контент Вкладок -->
        <div id="content-area">
            
            <!-- 1. Секция Новостей -->
            <div id="view-news" class="view-content grid grid-cols-1 md:grid-cols-3 gap-6">
                
                <!-- Новость 1 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-yellow-600">
                    <span class="text-sm font-semibold text-yellow-700">Официально</span>
                    <h2 class="text-2xl font-bold mt-2">Годовой Отчет: Запас сена в Заполярье на рекордном уровне</h2>
                    <p class="mt-4 text-gray-700">Министерство продовольствия сообщило о стабилизации цен на травяные тюки. Коровы могут спать спокойно: дефицита не предвидится. Власти планируют провести "Сенной Фестиваль".</p>
                    <p class="text-xs mt-3 text-gray-500">2 часа назад | Сектор "Травяной"</p>
                </div>

                <!-- Новость 2 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-blue-600">
                    <span class="text-sm font-semibold text-blue-700">События</span>
                    <h2 class="text-2xl font-bold mt-2">Сенсация: Уникальная Корова-Спортсменка научилась бегать боком</h2>
                    <p class="mt-4 text-gray-700">Звезда местного бегового клуба "Рябой Спринтер" разработала новую технику передвижения. Тренеры в восторге, конкуренты в замешательстве. Это может изменить мировой спорт!</p>
                    <p class="text-xs mt-3 text-gray-500">Вчера | Сектор "Спортивный"</p>
                </div>

                <!-- Новость 3 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-green-600">
                    <span class="text-sm font-semibold text-green-700">Наука</span>
                    <h2 class="text-2xl font-bold mt-2">Эксперимент: Выявлено, что коровы лучше видят мир в пастельных тонах</h2>
                    <p class="mt-4 text-gray-700">Группа ученых из Мууурманского Университета Скотоводства завершила исследование. Рекомендовано красить дома в нежно-розовый и мятный цвета для "визуальной гармонии".</p>
                    <p class="text-xs mt-3 text-gray-500">4 часа назад | Сектор "Ветеринарный"</p>
                </div>

                <!-- Новость 4 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-pink-600 md:col-span-3">
                    <span class="text-sm font-semibold text-pink-700">Культура</span>
                    <h2 class="text-2xl font-bold mt-2">Мууузыкальный Фестиваль: "Симфония Пищеварения" собрал тысячи слу слушателей</h2>
                    <p class="mt-4 text-gray-700">Главное событие года состоялось на Центральном Лугу. Выдающиеся композиторы представили произведения, основанные на ритмичном пережевывании. Главный гость — "Квартет из Четырех Вымени".</p>
                    <p class="text-xs mt-3 text-gray-500">Неделю назад | Сектор "Искусство"</p>
                </div>
                
            </div>

            <!-- 2. Секция Биржа Муу -->
            <div id="view-stock" class="view-content hidden p-6 bg-white rounded-xl shadow-xl">
                <h2 class="text-3xl font-bold mb-6 text-green-800">📈 Биржа Муу: Котировки Молока и Сена</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                    <div class="p-4 rounded-lg border border-green-400 bg-green-50">
                        <h3 class="text-xl font-bold text-green-700">МОЛОКО (MOOO)</h3>
                        <p class="text-3xl font-extrabold mt-1 text-green-600" id="milk-price">0.00</p>
                        <p class="text-sm text-gray-600">За один литр. Эксперты ожидают бычий тренд на жвачку.</p>
                    </div>
                    <div class="p-4 rounded-lg border border-yellow-400 bg-yellow-50">
                        <h3 class="text-xl font-bold text-yellow-700">ТРАВЯНОЙ ТЮК (HAY)</h3>
                        <p class="text-3xl font-extrabold mt-1 text-yellow-600" id="hay-price">0.00</p>
                        <p class="text-sm text-gray-600">За один стандартный тюк. Цена падает из-за слухов о "неурожае клевера".</p>
                    </div>
                </div>
                
                <div class="relative w-full aspect-[3/1] max-h-[400px]">
                     <canvas id="stockChartCanvas"></canvas>
                </div>

                <div class="mt-6 p-4 bg-gray-100 rounded-lg">
                    <h4 class="text-lg font-semibold text-gray-700">Аналитика от "Рога и Копыта Трейдинг":</h4>
                    <p id="stock-commentary" class="mt-2 text-gray-600">Цены стабильны. Аналитики советуют держать позиции и не нервировать пастуха.</p>
                </div>
            </div>

            <!-- 3. Секция Мууу-Прогноз -->
            <div id="view-weather" class="view-content hidden p-6 bg-white rounded-xl shadow-xl text-center">
                <h2 class="text-3xl font-bold mb-6 text-blue-800">☀️ Мууу-Прогноз: Погодный Центр Мууурманска</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="p-4 bg-blue-100 rounded-lg border border-blue-400">
                        <p class="text-5xl mb-2">🌤️</p>
                        <h3 class="text-xl font-bold text-blue-700">Температура</h3>
                        <p class="text-4xl font-extrabold mt-1 text-blue-600">+15°C</p>
                    </div>
                    <div class="p-4 bg-gray-100 rounded-lg border border-gray-400">
                        <p class="text-5xl mb-2">💧</p>
                        <h3 class="text-xl font-bold text-gray-700">Осадки</h3>
                        <p class="text-2xl font-extrabold mt-1 text-gray-600">Вероятность росы: 95%</p>
                    </div>
                    <div class="p-4 bg-green-100 rounded-lg border border-green-400">
                        <p class="text-5xl mb-2">💨</p>
                        <h3 class="text-xl font-bold text-green-700">Ветер</h3>
                        <p class="text-2xl font-extrabold mt-1 text-green-600">С севера, несет запах свежескошенной травы.</p>
                    </div>
                </div>

                <div class="mt-8 p-6 bg-yellow-50 rounded-lg border border-yellow-300">
                    <h4 class="text-2xl font-bold text-yellow-800">🐮 Влияние на Настроение:</h4>
                    <p class="text-xl mt-2 text-gray-700">Идеальное время для **медленной жвачки**. Пастухи рекомендуют продолжительный выпас на дальних лугах.</p>
                </div>
            </div>

            <!-- 4. Секция Зал Славы -->
             <div id="view-hall" class="view-content hidden p-6 bg-white rounded-xl shadow-xl">
                <h2 class="text-3xl font-bold mb-6 text-purple-800">🏆 Зал Славы Мууурманска</h2>
                <p class="text-xl mb-8 text-gray-700">Самые выдающиеся Коровы, прославившие наш город своими беспримерными достижениями.</p>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Герой 1 -->
                    <div class="bg-gray-100 p-4 rounded-xl shadow-lg border-t-4 border-yellow-500 text-center">
                        <div class="text-6xl mb-3">🏅</div>
                        <h3 class="text-2xl font-bold text-purple-700">Мумусильда Ленивая</h3>
                        <p class="text-lg font-semibold text-gray-600">Корова-рекордсмен по лени</p>
                        <p class="mt-3 text-gray-700">Провела 37 часов подряд в одной и той же позе, чем вдохновила скульпторов на монумент "Вечное Спокойствие".</p>
                        <p class="text-xs mt-2 text-gray-500">Достижение: 2024 г.</p>
                    </div>

                    <!-- Герой 2 -->
                    <div class="bg-gray-100 p-4 rounded-xl shadow-lg border-t-4 border-blue-500 text-center">
                        <div class="text-6xl mb-3">🍼</div>
                        <h3 class="text-2xl font-bold text-purple-700">Зорька Плодовитая</h3>
                        <p class="text-lg font-semibold text-gray-600">Самая плодовитая Корова</p>
                        <p class="mt-3 text-gray-700">Занесена в Книгу Рекордов Мууурманска за рождение тройни дважды за один пастбищный сезон. Герой материнства!</p>
                        <p class="text-xs mt-2 text-gray-500">Достижение: 2023 г.</p>
                    </div>

                    <!-- Герой 3 -->
                    <div class="bg-gray-100 p-4 rounded-xl shadow-lg border-t-4 border-green-500 text-center">
                        <div class="text-6xl mb-3">💡</div>
                        <h3 class="text-2xl font-bold text-purple-700">Буренка Инноватор</h3>
                        <p class="text-lg font-semibold text-gray-600">Корова-Инноватор</p>
                        <p class="mt-3 text-gray-700">Изобрела новый, более эффективный способ чесать бок о забор, чем снизила затраты на инфраструктуру на 12%.</p>
                        <p class="text-xs mt-2 text-gray-500">Достижение: 2025 г.</p>
                    </div>
                </div>
            </div>

            <!-- 5. Секция Мини-Игр -->
            <div id="view-games" class="view-content hidden p-6 bg-white rounded-xl shadow-xl text-center">
                <h2 class="text-3xl font-bold mb-6 text-yellow-800">🥛 Мууу-Кликер: Надой Свой Рубль!</h2>
                <p class="text-xl mb-8">Нажимайте кнопку, чтобы собрать как можно больше **Мууу-Монет** и стать самой богатой Коровой Мууурманска!</p>
                
                <p class="text-6xl font-extrabold mb-8">
                    <span id="milk-counter" class="text-yellow-600">0</span> 💰
                </p>

                <button id="milk-button" class="bg-green-500 hover:bg-green-600 text-white font-black py-4 px-10 rounded-full text-2xl shadow-lg hover:shadow-xl transition-all">
                    Надоить Молока! 🐄
                </button>

                <div class="mt-10 p-4 bg-gray-100 rounded-lg max-w-sm mx-auto">
                    <h3 class="text-xl font-semibold mb-2">Автоматизация (1000 💰)</h3>
                    <p id="automation-status" class="text-gray-700 mb-4">Требуется 1000 Мууу-Монет. Сейчас: 0/1 Автоматов.</p>
                    <button id="buy-automation" class="bg-blue-500 text-white py-2 px-4 rounded-lg text-lg disabled:opacity-50 hover:bg-blue-600 transition-colors">
                        Купить Автомат
                    </button>
                </div>
            </div>

            <!-- 6. Секция Боевых Действий (Canvas) -->
            <div id="view-war" class="view-content hidden p-6 bg-white rounded-xl shadow-xl">
                <h2 class="text-3xl font-bold mb-4 text-red-800">⚔️ Фронт "Корова vs Свинья" 🐖</h2>
                <p class="text-xl mb-4 text-gray-700">Следите за ситуацией на границе с Южными Территориями. Интерактивная карта показывает текущую линию разграничения.</p>
                
                <!-- Динамический статус (Классы bg/text/border будут установлены JS) -->
                <div id="war-status-box" class="p-4 rounded-lg text-center font-bold mb-6 transition-all duration-500 bg-gray-100 border border-gray-300 text-gray-700">
                    <span id="war-status">Фронт стабилен: 50.0%. Напряженное равновесие. ⚖️</span>
                </div>

                <div class="relative w-full aspect-[2/1] max-h-[500px] bg-gray-200 rounded-xl overflow-hidden">
                    <canvas id="warMapCanvas"></canvas>
                    <div class="absolute top-2 left-2 p-2 bg-green-700 text-white rounded-lg opacity-90 text-sm font-bold">
                        🟢 ТЕРРИТОРИЯ КОРОВ
                    </div>
                    <div class="absolute top-2 right-2 p-2 bg-red-700 text-white rounded-lg opacity-90 text-sm font-bold">
                        🔴 ТЕРРИТОРИЯ СВИНЕЙ
                    </div>
                </div>

                <div class="mt-6 flex flex-wrap justify-center gap-4">
                    <button onclick="simulateAdvance('cow')" class="bg-green-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-green-700 shadow-md transition-colors">
                        Коровы: ВПЕРЕД! 🚀
                    </button>
                    <button onclick="simulateAdvance('pig')" class="bg-red-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-red-700 shadow-md transition-colors">
                        Свиньи: КОНТРАТАКА! 💣
                    </button>
                    <button onclick="resetMap()" class="bg-gray-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-gray-600 shadow-md transition-colors">
                        Сбросить Карту 🔄
                    </button>
                </div>
            </div>

        </div>

        <!-- Подвал -->
        <footer class="text-center mt-12 pt-6 border-t-2 border-yellow-300 text-gray-500">
            <p>&copy; 2025 Новости Мууурманска. Все права защищены и запатентованы.</p>
        </footer>

    </div>

    <!-- JavaScript Логика -->
    <script>
        // --- Глобальное хранилище для оригинального текста ---
        const originalTexts = new Map();
        
        // --- Карта символов Брайля для кириллицы (упрощенная) ---
        const brailleMap = {
            'а': '⠁', 'б': '⠃', 'в': '⠧', 'г': '⠛', 'д': '⠙', 'е': '⠑', 'ж': '⠚', 'з': '⠵', 
            'и': '⠊', 'й': '⠯', 'к': '⠅', 'л': '⠇', 'м': '⠍', 'н': '⠝', 'о': '⠕', 'п': '⠏', 
            'р': '⠗', 'с': '⠎', 'т': '⠞', 'у': '⠥', 'ф': '⠋', 'х': '⠓', 'ц': '⠉', 'ч': '⠱', 
            'ш': '⠹', 'щ': '⠭', 'ъ': '⠷', 'ы': '⠮', 'ь': '⠾', 'э': '⠪', 'ю': '⠳', 'я': '⠜',
            '0': '⠼⠚', '1': '⠼⠁', '2': '⠼⠃', '3': '⠼⠉', '4': '⠼⠙', '5': '⠼⠑', 
            '6': '⠼⠋', '7': '⠼⠛', '8': '⠼⠓', '9': '⠼⠊',
            '.': '⠲', ',': '⠂', '!': '⠖', '?': '⠦', ':': '⠒', '-': '⠤', ' ': ' '
        };

        function translateToBraille(text) {
            if (!text) return '';
            let brailleText = '';
            // Символ-индикатор заглавной буквы
            const capIndicator = '⠨'; 
            // Символ-индикатор цифры
            const numIndicator = '⠼'; 

            let inNumber = false;
            let currentNumber = '';

            for (let i = 0; i < text.length; i++) {
                let char = text[i];
                let lowerChar = char.toLowerCase();

                // Обработка цифр (русский Брайль использует числовой знак перед группой цифр)
                if (char >= '0' && char <= '9') {
                    if (!inNumber) {
                        brailleText += numIndicator;
                        inNumber = true;
                    }
                    // Добавляем цифру (используем Брайль-представление латинских a-j)
                    const digitBraille = ['⠁', '⠃', '⠉', '⠙', '⠑', '⠋', '⠛', '⠓', '⠊', '⠚'][parseInt(char)];
                    brailleText += digitBraille;
                } else {
                    if (inNumber) {
                        inNumber = false;
                    }

                    // Обработка заглавных букв
                    if (char !== lowerChar && brailleMap[lowerChar]) {
                        brailleText += capIndicator;
                    }

                    // Перевод буквы/символа
                    if (brailleMap[lowerChar]) {
                        brailleText += brailleMap[lowerChar];
                    } else {
                        // Для всех остальных символов (эмодзи, скобки и т.д.) просто оставляем пробел или сам символ
                        brailleText += char === '\n' ? '\n' : (char === ' ' ? ' ' : (brailleMap[char] || char));
                    }
                }
            }

            return brailleText.replace(/⠼/g, numIndicator); // Убедимся, что числовой знак используется корректно
        }

        function collectTextNodes(node) {
            const nodes = [];
            const walker = document.createTreeWalker(
                node,
                NodeFilter.SHOW_TEXT,
                { acceptNode: (node) => {
                    // Игнорируем узлы внутри script, style, emoji (их текст пуст)
                    if (node.parentElement && (node.parentElement.tagName === 'SCRIPT' || node.parentElement.tagName === 'STYLE' || node.parentElement.tagName === 'CANVAS')) {
                        return NodeFilter.FILTER_SKIP;
                    }
                    // Игнорируем узлы, содержащие только пробелы или пустые
                    if (node.nodeValue.trim().length === 0) {
                        return NodeFilter.FILTER_SKIP;
                    }
                    return NodeFilter.FILTER_ACCEPT;
                }}
            );

            let currentNode;
            while (currentNode = walker.nextNode()) {
                nodes.push(currentNode);
            }
            return nodes;
        }


        // --- Вспомогательная функция для замены alert/confirm ---
        function showStatus(message, type = 'info') {
            const box = document.getElementById('status-message-box');
            const msg = document.getElementById('status-message');

            // Сброс классов
            box.className = 'fixed top-0 left-1/2 -translate-x-1/2 mt-4 p-4 rounded-lg shadow-xl z-50 transition-opacity duration-300 opacity-0 hidden';

            // Настройка по типу
            let bgColor, borderColor, textColor;
            if (type === 'success') {
                bgColor = 'bg-green-100';
                borderColor = 'border-green-400';
                textColor = 'text-green-700';
            } else if (type === 'error') {
                bgColor = 'bg-red-100';
                borderColor = 'border-red-400';
                textColor = 'text-red-700';
            } else { // info
                bgColor = 'bg-blue-100';
                borderColor = 'border-blue-400';
                textColor = 'text-blue-700';
            }

            box.classList.add(bgColor, borderColor, textColor);
            msg.textContent = message;
            box.classList.remove('hidden');
            
            // Плавное появление
            setTimeout(() => {
                box.classList.remove('opacity-0');
            }, 10); 

            // Автоматическое скрытие через 5 секунд
            setTimeout(() => {
                box.classList.add('opacity-0');
                box.addEventListener('transitionend', function handler() {
                    box.classList.add('hidden');
                    box.removeEventListener('transitionend', handler);
                });
            }, 5000);
        }

        // --- 0. Логика Переключения Режима Доступности (Брайль) ---
        let isA11yMode = false;

        function toggleLanguageMode() {
            isA11yMode = !isA11yMode;
            document.body.classList.toggle('accessibility-mode', isA11yMode);
            const toggleButton = document.getElementById('lang-toggle');
            const body = document.body;

            if (isA11yMode) {
                // 1. Собираем и переводим текст
                const nodes = collectTextNodes(body);
                nodes.forEach(node => {
                    const original = node.nodeValue;
                    originalTexts.set(node, original);
                    node.nodeValue = translateToBraille(original);
                });
                
                // 2. Обновляем кнопку и статус
                toggleButton.innerHTML = '🔊 **Режим для зрячих**';
                showStatus('Активирован режим Брайля (визуальное отображение символами Юникод).', 'success');
            } else {
                // 1. Восстанавливаем оригинальный текст
                originalTexts.forEach((original, node) => {
                    node.nodeValue = original;
                });
                originalTexts.clear();

                // 2. Обновляем кнопку и статус
                toggleButton.innerHTML = '⠓⠕⠃ ⠃⠗⠁⠃⠇⠕ ⠴ **Режим Брайля**';
                showStatus('Режим Брайля деактивирован. Стандартное отображение.', 'info');
            }
        }


        // --- 1. Логика Переключения Вкладок (SPA) ---
        function showView(viewName) {
            // Скрываем все контентные секции
            document.querySelectorAll('.view-content').forEach(el => {
                el.classList.add('hidden');
            });
            // Деактивируем все кнопки
            document.querySelectorAll('.tab-button').forEach(el => {
                el.classList.remove('active', 'bg-yellow-500');
                el.classList.add('bg-yellow-400');
            });

            // Показываем нужную секцию
            const viewElement = document.getElementById('view-' + viewName);
            const tabButton = document.getElementById('tab-' + viewName);
            if (viewElement) viewElement.classList.remove('hidden');
            if (tabButton) {
                tabButton.classList.add('active', 'bg-yellow-500');
                tabButton.classList.remove('bg-yellow-400');
            }

            // Запуск/остановка анимаций по необходимости
            if (viewName === 'war') {
                if (!warMapRunning) startWarMap();
            } else {
                stopWarMap();
            }
            
            if (viewName === 'stock') {
                if (!stockRunning) startStockChart();
            } else {
                stopStockChart();
            }
        }

        // Инициализация на старте
        document.addEventListener('DOMContentLoaded', () => {
            showView('news'); // Начинаем с новостей
            // Инициализация размеров Canvas
            resizeCanvas();
            initFrontLine();
            drawMap();
            initStockData();
            drawStockChart();
        });


        // --- 2. Логика Мини-Игры (Мууу-Кликер) ---
        let milkCount = 0;
        let automationBought = false;
        const automationCost = 1000;
        const milkButton = document.getElementById('milk-button');
        const milkCounter = document.getElementById('milk-counter');
        const buyAutomationButton = document.getElementById('buy-automation');
        const automationStatus = document.getElementById('automation-status');
        let automationInterval = null;

        milkButton.addEventListener('click', () => {
            milkCount += 1;
            updateMilkDisplay();
        });

        buyAutomationButton.addEventListener('click', () => {
            if (milkCount >= automationCost && !automationBought) {
                milkCount -= automationCost;
                automationBought = true;
                updateMilkDisplay();
                startAutomation();
                showStatus('Автоматизированная дойка успешно установлена!', 'success');
            }
        });

        function updateMilkDisplay() {
            milkCounter.textContent = milkCount;
            // Проверка, можно ли купить автомат
            if (!automationBought && milkCount >= automationCost) {
                buyAutomationButton.disabled = false;
                buyAutomationButton.textContent = 'КУПИТЬ ЗА 1000 💰';
            } else if (automationBought) {
                buyAutomationButton.disabled = true;
                buyAutomationButton.textContent = 'Автомат Установлен';
                automationStatus.textContent = 'Статус: Автоматизировано! +1 💰 каждую секунду.';
            } else {
                buyAutomationButton.disabled = true;
                buyAutomationButton.textContent = 'Требуется 1000 💰';
            }
        }

        function startAutomation() {
            automationInterval = setInterval(() => {
                if (automationBought) {
                    milkCount += 1;
                    updateMilkDisplay();
                }
            }, 1000);
        }
        
        // Инициализация счетчика
        updateMilkDisplay();
        
        // --- 3. Логика Биржи Муу (Canvas Chart) ---
        const stockCanvas = document.getElementById('stockChartCanvas');
        const stockCtx = stockCanvas.getContext('2d');
        const milkPriceEl = document.getElementById('milk-price');
        const hayPriceEl = document.getElementById('hay-price');
        const stockCommentaryEl = document.getElementById('stock-commentary');

        let stockHistory = [];
        const MAX_POINTS = 50;
        let stockRunning = false;
        let stockAnimationFrameId = null;
        let milkPrice = 100;
        let hayPrice = 50;

        function initStockData() {
            stockHistory = [];
            for (let i = 0; i < MAX_POINTS; i++) {
                stockHistory.push({
                    milk: 100 + Math.random() * 20 - 10,
                    hay: 50 + Math.random() * 10 - 5
                });
            }
            milkPrice = stockHistory[MAX_POINTS - 1].milk;
            hayPrice = stockHistory[MAX_POINTS - 1].hay;
        }

        function updateStockPrices() {
            // Случайные колебания
            const milkDelta = (Math.random() - 0.5) * 1.5;
            const hayDelta = (Math.random() - 0.5) * 0.8;

            milkPrice = Math.max(90, Math.min(120, milkPrice + milkDelta));
            hayPrice = Math.max(45, Math.min(60, hayPrice + hayDelta));

            // Сдвигаем историю и добавляем новые данные
            stockHistory.shift();
            stockHistory.push({ milk: milkPrice, hay: hayPrice });
            
            // Обновление DOM
            milkPriceEl.textContent = milkPrice.toFixed(2);
            hayPriceEl.textContent = hayPrice.toFixed(2);
            updateStockCommentary();
        }

        function updateStockCommentary() {
            let comment = '';
            if (milkPrice > 115) {
                comment = 'Молоко бьет рекорды! Коровы в восторге от спроса на сметану.';
            } else if (hayPrice < 47) {
                comment = 'Цена на сено рухнула! Отличный момент для пополнения запасов.';
            } else if (milkPrice < 95 && hayPrice > 55) {
                comment = 'Кризис: Молоко дешевеет, а сено дорожает. Аналитики советуют пить воду.';
            } else {
                comment = 'Цены стабильны. Аналитики советуют держать позиции и не нервировать пастуха.';
            }
            stockCommentaryEl.textContent = comment;
        }

        function drawStockChart() {
            const w = stockCanvas.width;
            const h = stockCanvas.height;
            const ctx = stockCtx;
            ctx.clearRect(0, 0, w, h);

            const padding = 20;
            const chartW = w - 2 * padding;
            const chartH = h - 2 * padding;
            const pointSpacing = chartW / (MAX_POINTS - 1);

            // Ось Y: от 40 до 130
            const minY = 40;
            const maxY = 130;
            const rangeY = maxY - minY;

            // Функция для масштабирования Y
            const scaleY = (value) => padding + chartH - ((value - minY) / rangeY) * chartH;

            // 1. Горизонтальные линии (Градуировка)
            ctx.strokeStyle = '#eee';
            ctx.lineWidth = 1;
            for (let i = 0; i <= 3; i++) {
                const y = padding + i * (chartH / 3);
                ctx.beginPath();
                ctx.moveTo(padding, y);
                ctx.lineTo(w - padding, y);
                ctx.stroke();
                
                // Метки Y
                ctx.fillStyle = '#999';
                ctx.font = '10px Inter';
                const labelValue = maxY - i * (rangeY / 3);
                ctx.fillText(labelValue.toFixed(0), 5, y + 3);
            }

            // 2. Рисование линии Молока (Зеленый)
            ctx.strokeStyle = '#10b981'; // Tailwind green-500
            ctx.lineWidth = 3;
            ctx.beginPath();
            stockHistory.forEach((point, i) => {
                const x = padding + i * pointSpacing;
                const y = scaleY(point.milk);
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            });
            ctx.stroke();

            // 3. Рисование линии Сена (Желтый)
            ctx.strokeStyle = '#fbbf24'; // Tailwind yellow-500
            ctx.lineWidth = 3;
            ctx.beginPath();
            stockHistory.forEach((point, i) => {
                const x = padding + i * pointSpacing;
                const y = scaleY(point.hay);
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            });
            ctx.stroke();
        }

        function animateStockChart() {
            if (!stockRunning) return;

            // Обновляем цены каждые 10 кадров (для замедления)
            if (Date.now() % 500 < 16) { // Обновление примерно 2 раза в секунду
                updateStockPrices();
            }
            drawStockChart();
            stockAnimationFrameId = requestAnimationFrame(animateStockChart);
        }

        function startStockChart() {
            if (stockRunning) return;
            stockRunning = true;
            resizeStockCanvas();
            animateStockChart();
        }

        function stopStockChart() {
            if (stockAnimationFrameId) {
                cancelAnimationFrame(stockAnimationFrameId);
                stockAnimationFrameId = null;
                stockRunning = false;
            }
        }

        function resizeStockCanvas() {
            if (!stockCanvas) return;
            const container = stockCanvas.parentElement;
            stockCanvas.width = container.offsetWidth;
            stockCanvas.height = container.offsetHeight;
        }

        window.addEventListener('resize', () => {
            resizeCanvas(); // Для карты
            resizeStockCanvas(); // Для биржи
            drawStockChart();
        });

        // --- 4. Логика Карты Боевых Действий (Canvas) ---
        const canvas = document.getElementById('warMapCanvas');
        const ctx = canvas.getContext('2d');
        const statusElement = document.getElementById('war-status');
        const statusBox = document.getElementById('war-status-box'); 

        let frontLine = []; 
        let animationFrameId = null;
        let warMapRunning = false;
        let advancementDirection = 0; 

        // Начальные параметры
        const RESOLUTION = 60; 
        const BASE_Y_RATIO = 0.5;
        const WOBBLE_RANGE = 20;

        function initFrontLine() {
            frontLine = [];
            for (let i = 0; i <= RESOLUTION; i++) {
                const noise = (Math.random() - 0.5) * WOBBLE_RANGE; 
                frontLine.push(canvas.height * BASE_Y_RATIO + noise);
            }
        }

        function drawMap() {
            if (!canvas || !ctx) return;
            const w = canvas.width;
            const h = canvas.height;
            const segmentWidth = w / RESOLUTION;

            ctx.clearRect(0, 0, w, h);

            // 1. Рисуем Территорию Свиней (КРАСНЫЙ, внизу)
            ctx.fillStyle = '#651d1d'; // Темно-красный (Pig territory)
            ctx.fillRect(0, 0, w, h);
            
            // Добавляем текстуру грязи/канав для Свиней (горизонтальные линии)
            ctx.strokeStyle = 'rgba(100, 50, 50, 0.4)'; // Грязный цвет
            ctx.lineWidth = 2;
            for (let i = 0; i < w; i += 10) {
                ctx.beginPath();
                ctx.moveTo(i, h / 2);
                ctx.lineTo(i, h);
                ctx.stroke();
            }

            // 2. Рисуем Территорию Коров (ЗЕЛЕНЫЙ, вгорі)
            ctx.fillStyle = '#227845'; // Темно-зеленый (Cow territory)
            ctx.beginPath();
            
            ctx.moveTo(0, 0); 
            ctx.lineTo(w, 0); 
            ctx.lineTo(w, frontLine[RESOLUTION]); 
            
            for (let i = RESOLUTION; i >= 0; i--) {
                const x = i * segmentWidth;
                const y = frontLine[i];
                ctx.lineTo(x, y);
            }

            ctx.closePath();
            ctx.fill();

            // Добавляем текстуру травы/поля для Коров (вертикальные штрихи)
            ctx.strokeStyle = 'rgba(150, 255, 150, 0.3)'; // Светло-зеленый для травы
            ctx.lineWidth = 1;
            for (let i = 0; i < w; i += 15) {
                ctx.beginPath();
                ctx.moveTo(i + Math.sin(i * 0.1) * 5, 0); // Добавим легкое смещение
                const endY = frontLine[Math.min(RESOLUTION, Math.floor(i / segmentWidth))];
                ctx.lineTo(i + Math.sin(i * 0.1) * 5, endY);
                ctx.stroke();
            }
            
            // --- Добавляем Сетку (Gridlines) ---
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 0.5;
            const gridSpacing = w / 10;
            
            // Вертикальные линии
            for (let i = 1; i < 10; i++) {
                ctx.beginPath();
                ctx.moveTo(i * gridSpacing, 0);
                ctx.lineTo(i * gridSpacing, h);
                ctx.stroke();
            }
            // Горизонтальные линии
            const vGridSpacing = h / 5;
            for (let i = 1; i < 5; i++) {
                ctx.beginPath();
                ctx.moveTo(0, i * vGridSpacing);
                ctx.lineTo(w, i * vGridSpacing);
                ctx.stroke();
            }


            // 3. Рисуем Саму Линию Фронта (визуально яркая, с тенью)
            ctx.strokeStyle = '#f8d254'; // Ярко-желтый
            ctx.lineWidth = 8;
            ctx.lineJoin = 'round';
            ctx.shadowColor = 'rgba(0,0,0,0.8)';
            ctx.shadowBlur = 10;
            ctx.beginPath();
            ctx.moveTo(0, frontLine[0]);
            for (let i = 1; i <= RESOLUTION; i++) {
                const x = i * segmentWidth;
                const y = frontLine[i];
                ctx.lineTo(x, y);
            }
            ctx.stroke();

            // 4. Добавляем маркеры/юниты (без тени)
            ctx.shadowBlur = 0;
            ctx.textAlign = 'center';
            ctx.font = '28px Inter'; 
            
            for (let i = 0; i <= RESOLUTION; i += 7) {
                const x = i * segmentWidth;
                const y = frontLine[i];
                
                // Коров'ячий юніт (чуть выше линии)
                ctx.fillText('🐄', x, y - 20);
                
                // Свинячий юніт (чуть ниже линии)
                ctx.fillText('🐖', x, y + 25);
            }
        }

        function calculateFrontPercentage() {
            if (frontLine.length === 0) return 50;
            
            // Средняя Y-координата фронта
            const sumY = frontLine.reduce((a, b) => a + b, 0);
            const avgY = sumY / frontLine.length;
            
            const h = canvas.height;
            // Y=h (низ) -> 0% Коровы (100% Свиньи)
            // Y=0 (верх) -> 100% Коровы (0% Свиньи)
            const cowControl = 100 - (avgY / h) * 100;
            
            return Math.max(0, Math.min(100, cowControl)); // Ограничиваем 0-100%
        }


        function updateFrontLine() {
            const ADVANCE_STEP = 0.03; 
            const WOBBLE_SPEED = 0.05; 
            const WOBBLE_STRENGTH = 6; 

            // --- Обновление Статуса ---
            const cowControl = calculateFrontPercentage();
            statusBox.className = "p-4 rounded-lg text-center font-bold mb-6 transition-all duration-500";
            
            if (advancementDirection === 1) { 
                statusElement.textContent = `Коровы в атаке! Попытка прорыва на линии ${cowControl.toFixed(1)}%! 🚀`;
                statusBox.classList.add('text-green-800', 'bg-green-100', 'border', 'border-green-400');
            } else if (advancementDirection === -1) { 
                statusElement.textContent = `Свиньи контратакуют! Позиции под угрозой: ${cowControl.toFixed(1)}%! 💣`;
                statusBox.classList.add('text-red-800', 'bg-red-100', 'border', 'border-red-400');
            } else {
                if (cowControl > 55) {
                    statusElement.textContent = `Коровы доминируют: ${cowControl.toFixed(1)}% территории под контролем! 👑`;
                    statusBox.classList.add('text-green-700', 'bg-green-50', 'border', 'border-green-300');
                } else if (cowControl < 45) {
                    statusElement.textContent = `Свиньи захватили инициативу: ${cowControl.toFixed(1)}% остается Коровий территорией. ⚠️`;
                    statusBox.classList.add('text-red-700', 'bg-red-50', 'border', 'border-red-300');
                } else {
                    statusElement.textContent = `Фронт стабилен: ${cowControl.toFixed(1)}%. Напряженное равновесие. ⚖️`;
                    statusBox.classList.add('text-blue-700', 'bg-blue-50', 'border', 'border-blue-300');
                }
            }


            for (let i = 0; i <= RESOLUTION; i++) {
                // 1. Добавляем случайные колебания
                const noise = Math.sin(Date.now() * WOBBLE_SPEED + i) * WOBBLE_STRENGTH;
                
                // 2. Базовое смещение (Наступление)
                let baseShift = 0;
                if (advancementDirection === 1) { 
                    baseShift = -ADVANCE_STEP;
                } else if (advancementDirection === -1) { 
                    baseShift = ADVANCE_STEP;
                } 


                // Ограничение, чтобы линия не выходила за пределы 10% и 90% высоты
                let newY = frontLine[i] + baseShift + noise;
                newY = Math.max(canvas.height * 0.1, Math.min(canvas.height * 0.9, newY));
                
                frontLine[i] = newY;
            }
        }

        function animateWarMap() {
            if (!warMapRunning) return;
            
            updateFrontLine();
            drawMap();
            
            animationFrameId = requestAnimationFrame(animateWarMap);
        }

        function startWarMap() {
            if (warMapRunning) return;
            warMapRunning = true;
            resizeCanvas();
            if (frontLine.length === 0) initFrontLine();
            animateWarMap();
        }
        
        function stopWarMap() {
            if (animationFrameId) {
                cancelAnimationFrame(animationFrameId);
                animationFrameId = null;
                warMapRunning = false;
            }
        }

        // Функция для симуляции наступления
        window.simulateAdvance = function(faction) {
            if (faction === 'cow') {
                advancementDirection = 1;
                // Автоматический возврат к стабильному состоянию через 5 секунд
                setTimeout(() => advancementDirection = 0, 5000); 
            } else if (faction === 'pig') {
                advancementDirection = -1;
                setTimeout(() => advancementDirection = 0, 5000); 
            }
        }

        // Функция для сброса карты
        window.resetMap = function() {
            initFrontLine();
            advancementDirection = 0;
            showStatus('Карта сброшена. Начинаем с нейтральных позиций!', 'info');
            drawMap();
        }


        // Обработка изменения размера окна для адаптивности Canvas
        function resizeCanvas() {
            if (!canvas) return;
            const container = canvas.parentElement;
            const size = container.offsetWidth;

            canvas.width = size;
            canvas.height = size / 2; 

            if (frontLine.length === 0) initFrontLine();
            drawMap(); 
        }

        window.addEventListener('resize', () => {
            if (warMapRunning) {
                stopWarMap();
                resizeCanvas();
                startWarMap();
            } else {
                 resizeCanvas();
            }
        });
        
    </script>
</body>
</html>
