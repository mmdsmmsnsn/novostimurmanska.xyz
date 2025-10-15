# novostimurmanska.xyz
новости великой мурманской депржави 

<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Новини Мууурманська — Фронт "Корова vs Свиня"</title>
    <!-- Завантаження Tailwind CSS та шрифту Inter -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        /* Стилі для загального вигляду */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f3e8; /* Світлий пастельний фон */
            color: #3b281f;
        }
        .container {
            max-width: 1280px;
        }
        /* Стилі для Карти Бойових Дій (Canvas) */
        #warMapCanvas {
            display: block;
            width: 100%;
            border-radius: 12px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            margin-top: 1rem;
        }
        /* Анімація для кнопок-вкладок */
        .tab-button {
            transition: all 0.3s ease;
            box-shadow: 0 4px #e5a400; /* Тінь під кнопкою */
        }
        .tab-button:hover:not(.active) {
            transform: translateY(-2px);
            box-shadow: 0 6px #e5a400;
        }
        .tab-button.active {
            transform: translateY(2px);
            box-shadow: none; /* "Натиснутий" вигляд */
            background-color: #e5a400 !important;
        }
        /* Стилі для кнопки ТГК */
        #tgk-button {
            transition: transform 0.2s, box-shadow 0.2s;
        }
        #tgk-button:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 30px -5px rgba(26, 153, 230, 0.5);
        }
        /* Стилі для міні-гри */
        #milk-button {
            transition: transform 0.1s;
        }
        #milk-button:active {
            transform: scale(0.95);
        }
    </style>
</head>
<body class="min-h-screen">

    <div class="container mx-auto p-4 md:p-8">
        <!-- Шапка -->
        <header class="text-center mb-8 bg-yellow-500/90 p-4 rounded-xl shadow-xl">
            <h1 class="text-4xl md:text-6xl font-extrabold text-white tracking-tight">
                🐮 Новини Мууурманська 🐄
            </h1>
            <p class="text-xl text-yellow-900 mt-2 font-semibold">Місто Корів. Серйозні події, які викликають усмішку.</p>
        </header>

        <!-- Навігація / Вкладки -->
        <nav class="flex justify-center space-x-3 mb-8">
            <button onclick="showView('news')" id="tab-news" class="tab-button active bg-yellow-400 text-yellow-900 font-bold py-3 px-6 rounded-xl text-lg hover:bg-yellow-500">
                📰 Новини
            </button>
            <button onclick="showView('games')" id="tab-games" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-6 rounded-xl text-lg hover:bg-yellow-500">
                🕹️ Міні-ігри
            </button>
            <button onclick="showView('war')" id="tab-war" class="tab-button bg-yellow-400 text-yellow-900 font-bold py-3 px-6 rounded-xl text-lg hover:bg-yellow-500">
                ⚔️ Бойові дії
            </button>
        </nav>

        <!-- Кнопка Telegram -->
        <div class="flex justify-center mb-8">
            <a id="tgk-button" href="https://t.me/NovostiMyyyrmanska" target="_blank" class="flex items-center space-x-2 bg-blue-500 text-white font-extrabold py-3 px-8 rounded-full text-xl shadow-lg shadow-blue-300/50">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.35 6.64l-2.8 1.94 1.15 3.52c.07.24-.03.5-.24.6l-1.99 1.45c-.2.15-.46.15-.65 0l-.82-.63c-.1-.08-.24-.08-.33 0l-2.43 1.86c-.1.08-.2.12-.31.12-.13 0-.25-.04-.36-.12-.22-.16-.3-.44-.19-.7L8.9 9.3c.09-.27-.06-.55-.33-.64L4.85 7.49c-.29-.09-.59.07-.68.37-.09.3.07.6.37.69l12 3.6c.27.08.55-.07.64-.34l1.2-3.72c.1-.32-.08-.66-.4-.76z"/>
                </svg>
                <span>Наш ТГК — Канал Мууурманських Новин</span>
            </a>
        </div>

        <!-- Контент Вкладок -->
        <div id="content-area">
            <!-- 1. Секція Новин -->
            <div id="view-news" class="view-content grid grid-cols-1 md:grid-cols-3 gap-6">
                
                <!-- Новина 1 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-yellow-600">
                    <span class="text-sm font-semibold text-yellow-700">Офіційно</span>
                    <h2 class="text-2xl font-bold mt-2">Річний Звіт: Запас сіна у Заполяр'ї на рекордному рівні</h2>
                    <p class="mt-4 text-gray-700">Міністерство продовольства повідомило про стабілізацію цін на трав'яні тюки. Корови можуть спати спокійно: дефіциту не передбачається. Влада планує провести "Сіновий Фестиваль".</p>
                    <p class="text-xs mt-3 text-gray-500">2 години тому | Сектор "Трав'яний"</p>
                </div>

                <!-- Новина 2 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-blue-600">
                    <span class="text-sm font-semibold text-blue-700">Події</span>
                    <h2 class="text-2xl font-bold mt-2">Сенсація: Унікальна Корова-Спортсменка навчилася бігати боком</h2>
                    <p class="mt-4 text-gray-700">Зірка місцевого бігового клубу "Рябий Спринтер" розробила нову техніку пересування. Тренери в захваті, конкуренти збентежені. Це може змінити світовий спорт!</p>
                    <p class="text-xs mt-3 text-gray-500">Вчора | Сектор "Спортивний"</p>
                </div>

                <!-- Новина 3 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-green-600">
                    <span class="text-sm font-semibold text-green-700">Наука</span>
                    <h2 class="text-2xl font-bold mt-2">Експеримент: Виявлено, що корови краще бачать світ у пастельних тонах</h2>
                    <p class="mt-4 text-gray-700">Група вчених із Мууурманського Університету Корівництва завершила дослідження. Рекомендовано фарбувати будинки у ніжно-рожевий та м'ятний кольори для "візуальної гармонії".</p>
                    <p class="text-xs mt-3 text-gray-500">4 години тому | Сектор "Ветеринарний"</p>
                </div>

                <!-- Новина 4 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-2xl transition-shadow border-t-4 border-pink-600 md:col-span-3">
                    <span class="text-sm font-semibold text-pink-700">Культура</span>
                    <h2 class="text-2xl font-bold mt-2">Мууузичний Фестиваль: "Симфонія Травлення" зібрала тисячі слухачів</h2>
                    <p class="mt-4 text-gray-700">Головна подія року відбулася на Центральній Луці. Видатні композитори представили твори, засновані на ритмічному пережовуванні. Головний гість — "Квартет із Чотирьох Вим’я".</p>
                    <p class="text-xs mt-3 text-gray-500">Тиждень тому | Сектор "Мистецький"</p>
                </div>
                
            </div>

            <!-- 2. Секція Міні-Ігор -->
            <div id="view-games" class="view-content hidden p-6 bg-white rounded-xl shadow-xl text-center">
                <h2 class="text-3xl font-bold mb-6 text-yellow-800">🥛 Мууу-Клікер: Надій Свій Вим'я!</h2>
                <p class="text-xl mb-8">Натискайте кнопку, щоб зібрати якомога більше **Мууу-Монет** та стати найбагатшою Коровою Мууурманська!</p>
                
                <p class="text-6xl font-extrabold mb-8">
                    <span id="milk-counter" class="text-yellow-600">0</span> 💰
                </p>

                <button id="milk-button" class="bg-green-500 hover:bg-green-600 text-white font-black py-4 px-10 rounded-full text-2xl shadow-lg hover:shadow-xl transition-all">
                    Надоїти Молока! 🐄
                </button>

                <div class="mt-10 p-4 bg-gray-100 rounded-lg max-w-sm mx-auto">
                    <h3 class="text-xl font-semibold mb-2">Автоматизація (1000 💰)</h3>
                    <p id="automation-status" class="text-gray-700 mb-4">Потрібно 1000 Мууу-Монет. Наразі: 0/1 Автоматів.</p>
                    <button id="buy-automation" class="bg-blue-500 text-white py-2 px-4 rounded-lg text-lg disabled:opacity-50 hover:bg-blue-600 transition-colors">
                        Купити Автомат
                    </button>
                </div>
            </div>

            <!-- 3. Секція Бойових Дій (Canvas) -->
            <div id="view-war" class="view-content hidden p-6 bg-white rounded-xl shadow-xl">
                <h2 class="text-3xl font-bold mb-4 text-red-800">⚔️ Фронт "Корова vs Свиня" 🐖</h2>
                <p class="text-xl mb-4 text-gray-700">Слідкуйте за ситуацією на кордоні з Південними Територіями. Інтерактивна карта показує поточну лінію розмежування.</p>
                
                <div class="p-4 bg-red-50 border border-red-200 rounded-lg text-center font-bold text-red-700 mb-6">
                    <span id="war-status">Фронт стабільний, але Корови готуються до контратаки!</span>
                </div>

                <div class="relative w-full aspect-[2/1] max-h-[500px] bg-gray-200 rounded-xl overflow-hidden">
                    <canvas id="warMapCanvas"></canvas>
                    <div class="absolute top-2 left-2 p-2 bg-green-700 text-white rounded-lg opacity-90 text-sm font-bold">
                        🟢 ТЕРИТОРІЯ КОРІВ
                    </div>
                    <div class="absolute top-2 right-2 p-2 bg-red-700 text-white rounded-lg opacity-90 text-sm font-bold">
                        🔴 ТЕРИТОРІЯ СВИНЕЙ
                    </div>
                </div>

                <div class="mt-6 flex flex-wrap justify-center gap-4">
                    <button onclick="simulateAdvance('cow')" class="bg-green-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-green-700 shadow-md transition-colors">
                        Корови: ВПЕРЕД! 🚀
                    </button>
                    <button onclick="simulateAdvance('pig')" class="bg-red-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-red-700 shadow-md transition-colors">
                        Свині: КОНТРАТАКА! 💣
                    </button>
                    <button onclick="resetMap()" class="bg-gray-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-gray-600 shadow-md transition-colors">
                        Скинути Карту 🔄
                    </button>
                </div>
            </div>

        </div>

        <!-- Підвал -->
        <footer class="text-center mt-12 pt-6 border-t-2 border-yellow-300 text-gray-500">
            <p>&copy; 2025 Новини Мууурманська. Всі права захищені та запатентовані.</p>
        </footer>

    </div>

    <!-- JavaScript Логіка -->
    <script>
        // --- 1. Логіка Перемикання Вкладок (SPA) ---
        function showView(viewName) {
            // Приховуємо всі контентні секції
            document.querySelectorAll('.view-content').forEach(el => {
                el.classList.add('hidden');
            });
            // Деактивуємо всі кнопки
            document.querySelectorAll('.tab-button').forEach(el => {
                el.classList.remove('active', 'bg-yellow-500');
                el.classList.add('bg-yellow-400');
            });

            // Показуємо потрібну секцію
            const viewElement = document.getElementById('view-' + viewName);
            const tabButton = document.getElementById('tab-' + viewName);
            if (viewElement) viewElement.classList.remove('hidden');
            if (tabButton) {
                tabButton.classList.add('active', 'bg-yellow-500');
                tabButton.classList.remove('bg-yellow-400');
            }

            // Якщо перейшли на карту, запускаємо її анімацію
            if (viewName === 'war') {
                if (!warMapRunning) startWarMap();
            } else {
                // В інших випадках можна зупинити, щоб не витрачати ресурси
                stopWarMap();
            }
        }

        // Ініціалізація на старті
        document.addEventListener('DOMContentLoaded', () => {
            showView('news'); // Починаємо з новин
        });


        // --- 2. Логіка Міні-Гри (Мууу-Клікер) ---
        let milkCount = 0;
        let automationBought = false;
        const automationCost = 1000;
        const milkButton = document.getElementById('milk-button');
        const milkCounter = document.getElementById('milk-counter');
        const buyAutomationButton = document.getElementById('buy-automation');
        const automationStatus = document.getElementById('automation-status');

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
            }
        });

        function updateMilkDisplay() {
            milkCounter.textContent = milkCount;
            // Перевірка, чи можна купити автомат
            if (!automationBought && milkCount >= automationCost) {
                buyAutomationButton.disabled = false;
                buyAutomationButton.textContent = 'КУПИТИ ЗА 1000 💰';
            } else if (automationBought) {
                buyAutomationButton.disabled = true;
                buyAutomationButton.textContent = 'Автомат Встановлено';
                automationStatus.textContent = 'Статус: Автоматизовано! +1 💰 щосекунди.';
            } else {
                buyAutomationButton.disabled = true;
                buyAutomationButton.textContent = 'Потрібно 1000 💰';
            }
        }

        function startAutomation() {
            setInterval(() => {
                if (automationBought) {
                    milkCount += 1;
                    updateMilkDisplay();
                }
            }, 1000);
        }
        
        // Ініціалізація лічильника
        updateMilkDisplay();

        // --- 3. Логіка Карти Бойових Дій (Canvas) ---
        const canvas = document.getElementById('warMapCanvas');
        const ctx = canvas.getContext('2d');
        const statusElement = document.getElementById('war-status');

        let frontLine = []; // Масив Y-координат фронту
        let animationFrameId = null;
        let warMapRunning = false;
        let advancementDirection = 0; // -1: Pigs advance, 1: Cows advance, 0: Stable

        // Початкові параметри
        const RESOLUTION = 50; // Кількість точок на лінії фронту
        const BASE_Y_RATIO = 0.5; // Початкове положення (посередині)
        const WOBBLE_RANGE = 20; // Діапазон випадкових коливань лінії

        function initFrontLine() {
            // Ініціалізуємо фронт трохи вище/нижче центру з невеликим випадковим шумом
            frontLine = [];
            for (let i = 0; i <= RESOLUTION; i++) {
                // Випадкове зміщення відносно базової лінії
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

            // 1. Малюємо Територію Свиней (Червоний, внизу)
            ctx.fillStyle = '#b91c1c'; // Tailwind red-700
            ctx.fillRect(0, 0, w, h);

            // 2. Малюємо Територію Корів (Зелений, вгорі)
            ctx.fillStyle = '#16a34a'; // Tailwind green-700
            ctx.beginPath();
            ctx.moveTo(0, 0);
            ctx.lineTo(w, 0);

            // Малюємо лінію фронту (верхній контур)
            for (let i = 0; i <= RESOLUTION; i++) {
                const x = i * segmentWidth;
                const y = frontLine[i];
                ctx.lineTo(x, y);
            }
            ctx.lineTo(0, h * BASE_Y_RATIO); // Ця лінія вже не потрібна
            ctx.lineTo(0, 0);
            ctx.closePath();
            ctx.fill();


            // 3. Малюємо Саму Лінію Фронту (випадкова товста лінія)
            ctx.strokeStyle = '#facc15'; // Tailwind yellow-400
            ctx.lineWidth = 6;
            ctx.lineJoin = 'round';
            ctx.beginPath();
            ctx.moveTo(0, frontLine[0]);

            for (let i = 1; i <= RESOLUTION; i++) {
                const x = i * segmentWidth;
                const y = frontLine[i];
                ctx.lineTo(x, y);
            }
            ctx.stroke();
        }

        function updateFrontLine() {
            const ADVANCE_STEP = 0.05; // Швидкість поступу
            const WOBBLE_SPEED = 0.05; // Швидкість коливань
            const WOBBLE_STRENGTH = 10; // Сила коливань

            for (let i = 0; i <= RESOLUTION; i++) {
                // 1. Додаємо випадкові коливання
                const noise = Math.sin(Date.now() * WOBBLE_SPEED + i) * WOBBLE_STRENGTH;
                
                // 2. Базове зміщення (Поступ)
                let baseShift = 0;
                if (advancementDirection === 1) { // Корови наступають
                    baseShift = -ADVANCE_STEP;
                    statusElement.textContent = 'Корови наступають! 🐮 Тиснуть по центру.';
                    statusElement.classList.replace('text-red-700', 'text-green-700');
                    statusElement.classList.replace('bg-red-50', 'bg-green-50');
                } else if (advancementDirection === -1) { // Свині наступають
                    baseShift = ADVANCE_STEP;
                    statusElement.textContent = 'Свині намагаються контратакувати! 🐷 Ситуація напружена.';
                    statusElement.classList.replace('text-green-700', 'text-red-700');
                    statusElement.classList.replace('bg-green-50', 'bg-red-50');
                } else {
                    statusElement.textContent = 'Фронт стабільний, але Корови готуються до контратаки! 🛡️';
                    statusElement.classList.add('text-red-700');
                    statusElement.classList.add('bg-red-50');
                }


                // Обмеження, щоб лінія не виходила за межі 10% і 90% висоти
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

        // Функція для симуляції наступу
        window.simulateAdvance = function(faction) {
            if (faction === 'cow') {
                advancementDirection = 1;
                // Автоматичне повернення до стабільного стану через 5 секунд
                setTimeout(() => advancementDirection = 0, 5000); 
            } else if (faction === 'pig') {
                advancementDirection = -1;
                setTimeout(() => advancementDirection = 0, 5000); 
            }
        }

        // Функція для скидання карти
        window.resetMap = function() {
            initFrontLine();
            advancementDirection = 0;
            statusElement.textContent = 'Карту скинуто. Починаємо з нейтральних позицій!';
            drawMap();
        }


        // Обробка зміни розміру вікна для адаптивності Canvas
        function resizeCanvas() {
            if (!canvas) return;
            // Визначаємо розміри контейнера
            const container = canvas.parentElement;
            const size = container.offsetWidth;

            // Встановлюємо розміри Canvas. ВАЖЛИВО: setting width/height directly
            canvas.width = size;
            canvas.height = size / 2; // Зберігаємо співвідношення 2:1

            if (frontLine.length === 0) initFrontLine();
            drawMap(); // Перемалювати після зміни розміру
        }

        window.addEventListener('resize', () => {
             // Перезапускаємо карту, щоб перемалювати її в новому розмірі
            if (warMapRunning) {
                stopWarMap();
                resizeCanvas();
                startWarMap();
            } else {
                 resizeCanvas();
            }
        });
        
        // Ініціалізація карти на завантаженні (не запускаємо анімацію, поки не перейшли на вкладку)
        window.onload = function() {
            resizeCanvas();
            initFrontLine();
            drawMap();
            // showView('news'); // Вже викликається у DOMContentLoaded
        }

    </script>
</body>
</html>
