# mind-quiz
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Викторина для самых лучших другов!</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #adffad;
            text-align: center;
            padding: 40px 20px;
            color: #2c3e2c;
            margin: 0;
            position: relative;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: rgb(227, 251, 227);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(27, 207, 87, 0.94);
            position: relative;
        }
        h1 {
            color: #2e7d32;
            margin-bottom: 20px;
        }
        .question-image {
            max-width: 100%;
            height: auto;
            border-radius: 15px;
            margin: 15px auto;
            border: 5px solid #a5d6a7;
            display: none;
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin: 25px 0;
        }
        button.option-btn {
            background-color: #e8f5e9;
            color: #2c3e2c;
            border: none;
            padding: 15px;
            border-radius: 12px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
            border: 2px solid #c8e6c9;
        }
        button.option-btn:hover {
            background-color: #3eb041;
            color: white;
            transform: scale(1.02);
        }
        button.option-btn:disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }
        #next-btn, #restart-btn, #start-btn, #retry-btn {
            background-color: #34a839;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            margin-top: 20px;
            transition: all 0.3s ease;
        }
        #next-btn:hover, #restart-btn:hover, #start-btn:hover, #retry-btn:hover {
            background-color: #2e7d32;
            transform: scale(1.05);
        }
        #next-btn {
            display: none;
        }
        #result {
            margin-top: 30px;
            font-size: 18px;
            min-height: 24px;
            font-weight: bold;
        }
        .hidden {
            display: none;
        }
        .gift-container {
            background: linear-gradient(135deg, #90f399, #c8e6c9);
            padding: 30px;
            border-radius: 20px;
            margin-top: 30px;
            border: 3px dashed #4caf50;
        }
        .gift-image {
            max-width: 100%;
            border-radius: 15px;
            margin: 20px auto;
            display: block;
        }
        .progress {
            margin: 15px 0;
            font-weight: bold;
            color: #2e7d32;
        }
        .warning-container {
            background: linear-gradient(135deg, #ffecb3, #ffd54f);
            padding: 25px;
            border-radius: 15px;
            margin: 20px 0;
            border: 3px solid #ffa000;
        }
        .warning-container h2 {
            color: #ff6f00;
            margin-top: 0;
        }
        .lives-container {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(227, 251, 227, 0.9);
            padding: 10px 15px;
            border-radius: 20px;
            border: 2px solid #a5d6a7;
            font-size: 20px;
            font-weight: bold;
        }
        .death-container {
            background: linear-gradient(135deg, #ff9f9f, #ff6b6b);
            padding: 30px;
            border-radius: 20px;
            margin-top: 30px;
            border: 3px dashed #ff4757;
            color: white;
        }
        .death-container h2 {
            color: #ff4757;
            margin-top: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <div id="lives-display" class="lives-container hidden">❤️❤️❤️❤️❤️</div>

        <div id="warning-screen">
            <div class="warning-container">
                <h2>⚠️ Внимание! ⚠️</h2>
                <p>Перед началом викторины учтите 1 правило:</p>
                <p><strong>Вы не получите подарок, если ответите на 5 вопросов из общего количества неправильно.</strong></p>
                <p>Старайтесь не ошибаться! У вас есть 5 жизней ❤️! И не забывайте, здес всё серьезно.</p>
                <button id="start-btn">ОК!</button>
            </div>
        </div>

        <div id="quiz-screen" class="hidden">
            <h1> Викториночка! </h1>
            <p>💕Ответьте на все вопросы и получите сюрприз!💗</p>
            <div class="progress" id="progress">Вопрос 1 из 25</div>
            <div id="question-container">
                <img id="question-image" class="question-image" src="" alt="Изображение к вопросу">
                <h2 id="question-text">Вопрос загружается...</h2>
                <div id="options-container" class="options"></div>
            </div>
            <button id="next-btn">Следующий вопрос <b>&#9829; &#8594;</b></button>
            <div id="result"></div>
        </div>

        <div id="gift-screen" class="hidden">
            <div class="gift-container">
                <h1>Вы ответили на все вопросы! Ваш подарок уже тут! 💝</h1>
                
                <img id="gift-image" class="gift-image" src="" alt="Ваш подарок">
                <div id="gift-message"></div>
                <div id="gift-links"></div>
                <button id="restart-btn">Пройти ещё раз! 🔄</button>
            </div>
        </div>

        <div id="death-screen" class="hidden">
            <div class="death-container">
                <h2>💀 ОЙ! Кажется вы умерли... 💀</h2>
                <p>То есть потеряли все жизни!</p>
                <p>Чтобы получить подарки, пожалуйста, перепройдите викторину!</p>
                <button id="retry-btn">Перепройти викторину!</button>
            </div>
        </div>
    </div>

    <script>
        // ========== КОНФИГУРАЦИЯ ВИКТОРИНЫ ==========
        const questions = [
            {
                question: "Вы готовы, дети?",
                image: "5930471.jpg",
                options: ["Нет", "Да, капитан!", "Нууу, 50 на 50"],
                correctAnswer: 1
            },
            {
                question: "Я не слышу!",
                image: "5314500139190188024.jpg",
                options: ["Нужно к врачу", "ГоспоДи, мне уже страшно", "Так точно, Капитан!", "*Упал*"],
                correctAnswer: 2
            },
            {
                question: "Ктоооооооо... Кто проживает в последнем дне?",
                image: "4dbe22882d18d64cc97f852fb8c6673c.jpg", 
                options: ["Глубоководный угорь-большерот, у которого рот, как у пеликана!", "Планктончик и две чудные рыбки", "Акула-домовой","Акула-гоблин","Прошлые два - одно и то же", "Слепой омар Dinochelus ausubeli"],
                correctAnswer: 1
            },
            {
                question: "От какого блюда веет особым вайбом комфорта, счастья и уюта при тусклом свете?",
                image: "", 
                options: ["Салат Цезарь", "Тортик Наполеон", "Куриный супчик", "Наши порно-фанфичные бутерброды", "Бутерброды с красной рыбой", "Жареное мясо с гарниром", "А-Ля нихуя Де дома нет"],
                correctAnswer: 3
            },
            {
                question: "Как расшифровывается ЛК?",
                image: "", 
                options: ["ЛичинкаКонфликта", "ЛобковыйКлещ", "ЛишайныйКоврик", "лжекрис", "ЛексическийКошмар", "ЛоговищеКринжа", "ЛысыйКрот"],
                correctAnswer: 1
            },
            { 
                question: "Внимательно смотрим на картинку, дамы и господа. Давайте вспомним, кто делал эту валентинку и текст от всей души?",
                image: "валентинка.jpg", 
                options: ["Делали для Блэйдика; Кафка и Страпон #FF00FF", "Делали для мистера Янга; Стелла Стелароновна, Даник Видьялыщлщкыахаров, Авантюрин Пиздалётик", "Делали для Диониса Ф.; Мириопия, Мил'отина, Евгей, Крысик", "Делали для любимой порно-писательницы; Голубка Женечка, Котик Машенька, Енотовидная Сашенька", "ЭТО БРЕДОВЫЙ СОН. ГРИБОЧКИ... ПОДОСИНОВИК..."],
                correctAnswer: 3
            },
            {
                question: "Кто в полицейском участке опознал звёздное трио ASS?",
                image: "елотька.jpg", 
                options: ["Крис", "Дядя полицай (Твоя любовь пройдет не скоро...)", "Микайо", "Дэниссимо Прист", "Микаэль (выдра)", "Изао Ферролибел", "Дионис"],
                correctAnswer: 3
            },
            {
                question: "Кто на сцене?",
                image: "5325689989285149291.jpg", 
                options: ["Лука и Тилл", "Миль и Мира (втф?)", "Хз", "Дед сердечник-астматик и подросток в пубертате", "сутулая псина и какойто ребенок"],
                correctAnswer: 3
            },
            { 
                question: "Почему надпись 'ЛК ЛОХ :)' не стирается?",
                image: "", 
                options: ["Это нерушимая печать одобрения от самого Сатурна", "Потому что Саша писала её пальцем Криса", "Крис плюнул в зеркало и ВУАЛЯ", "Потому что лк лох", "Каждый раз, когда ЛК дышит, надпись проявляется заново", "Зеркало отказывается забывать правду", "Корольки каждый раз пишут её заново", "Его аура лоховности впиталась в стекло на молекулярном уровне", "Все ответы верные"],
                correctAnswer: 8
            },
            {
                question: "На ком картинка?",
                image: "Aaa.png", 
                options: ["Садо-мазо, садо-мазо *пеение корольков*", "Оторви мне чего-нибудь,", "Укуси меня за...ерентий", "терентий"],
                correctAnswer: 3
            },
            {
                question: "Наглая ложь! То была лишь жалкая пародия! КТО НА КАРТИНКЕ?",
                image: "5330325233955110022.jpg", 
                options: ["А дайте-ка я вас лицом об стол,", "Потом попудрим и незаметно.", "Ну что вы стоите,как некий столб?????????", "Ах,да,я прибил вас к паркету,бедный.........", "Я полюбил вас за ваш азарт,", "НЕ НАДО ТОЛЬКО СМОТРЕТЬ В ГЛАЗА МНЕ!!!!!!!!!!!!!!!!!!!!!!!!", "*хОр КоРоЛьКоВ* ТЕРЕНТИЙ *хОр КоРоЛьКоВ*", "А какое у нас стоп слово???"],
                correctAnswer: 6
            },
            {
                question: "Кстати, а вы уже успели поиграть в BB? Мне очень понравилась! но сцена с ножом в глазу, ноге, легком, руке... ох боже, короче жестокая сцена. Но игра стоит своих денег.",
                image: "5325689989285149279.jpg", 
                options: ["У нас тут викторина вообще-то", "ДА, ВАЩЕ КРУТЬ. ПОЧКУ ЗА НЕЁ ПРОДАМ", "Ага. Не, она так себе... на троечку", "БЛЯ, ТАМ ТАКОЙ ПАУК СТРАШНЫЙ БЫЛ, ЧТО Я НАХУЙ УДАЛИЛА ЕЁ!!!", "Нет", "ЧЁ", "Мэй секси", "Ян вынес мозг на  0,0000001 секунде игры, ну нах, поиграю когда гг будет Август.", "Как у них вышло одеть Яна..?"],
                correctAnswer: 0
            },
            {
                question: "Ла-адно. Викторина, так викторина, САМИ НАПРОСИЛИСЬ. Кто написал надпись 'ЛК ЛОХ' в четвертом эпизоде фильма 'Убить ЛК - история счастья'?",
                image: "5319108140882590893.jpg", 
                options: ["Просто факт - ЛК ЛОХ", "Кристиан", "Евгений", "Дионис", "Его собственная рука в момент просветления. (Он наконец-то осознал истину и поспешил её зафиксировать)", "Лиссанька", "Мильотина", "Призрак его былой адекватности. (Явился ненадолго из небытия, чтобы оставить напоминание)", "Само время. Оно всё расставляет по местам", "Безымянный статист, которому просто надоело. (Какой-то случайный прохожий мимоходом констатировал факт)", "Автограф самого ЛК", "Откуда ты это взяла...???!!!"],
                correctAnswer: 6
            },
            {
                question: "Мне кстати обложка к фильму зашла! Ой, да, викторина же... Так и быть... э... Найдите ЛК на обложке.",
                image: "5319108140882590894.jpg",
                options: ["В правой части, прямо в волосах Мильотины", "Да ты надоела... когда нормальные вопросы будут?", "лк лох", "Да вон, прямо в глазах криса", "В названии", "В перечисленных главных актерах", "Его здесь нет", "я отказываюсь в этом участвовать", "Желтые тюльпаны, желтые тюльпаны, желтые тюльпаны, желтые тюльпан..."],
                correctAnswer: 2
            },
            {
                question: "Мне ещё зашёл симулятор бармена... там... тако-ой ба-армен... КХЭ. О чем мы? Викторина? Да-да, я вас слушаю, приеная Центра... кхэ... С какой стороны наша любимая попа?",
                image: "5294285171236923182.jpg", 
                options: ["левооооо", "по середине", "её тут нет", "правоооо", "А ссылку на симулятор мне самой давать?", "Что за бред...", "хочу Ди..."],
                correctAnswer: 3
            },
            {
                question: "Теперь немного отдохнём... Полюбуемся... Вспомним ту ночь",
                image: "мимими.jpg", 
                options: ["Да... Хорошо посидели тогда", "Я ещё от прошлого вопроса не отошла"],
                correctAnswer: 0
            },
            {
                question: "Ладненько, а теперь вопросы попроще. Кого любит Крис?",
                image: "", 
                options: ["Лису", "Попугайчика", "Миль", "Ди", "Евгения", "Лиссаньку", "Себя"],
                correctAnswer: 5
            },
            {
                question: "Ладненько, а теперь вопросы ещё проще. Кого любит ЛКрис?",
                image: "", 
                options: ["Лису", "Попугайчика", "Миль", "Ди", "Евгения", "Лиссаньку", "Маму"],
                correctAnswer: 3
            },
            {
                question: "Кто вы? 👊",
                image: "111.jpg", 
                options: ["Няшки", "Красотки", "Вупсен и Пупсен","👈Я ЛК👉👈Я ЛК👉👈Я ЛК👉","Подарите Ди", "Самуелучшиелапупусенюсенечкикрасотулелички..."],
                correctAnswer: 5
            },
            {
                question: "А теперь давайте серьёзно: сколько мне лет?",
                image: "", 
                options: ["20", "200", "2000","2","У меня 2 по математике", "кто я..."],
                correctAnswer: 3
            },
            {
                question: "А теперь давайте ещё серьёзнее: сколько вам лет?",
                image: "", 
                options: ["40", "200", "2000","20","У меня 2 по математике 2х", "кто я... 2х"],
                correctAnswer: 0
            },
            {
                question: "А теперь давайте прям ещё серьёзнее, включаем ум: сколько дней между моим др и Маши-Мирославы?",
                image: "", 
                options: ["180", "193", "190","200","Я не калькулятор", "223"],
                correctAnswer: 2
            },
            {
                question: "А теперь давайте ещё прям серьёзно-серьёзно, включаем ум: сколько дней между моим др и Женечки?",
                image: "", 
                options: ["180", "193", "190","200","Я не калькулятор 2х", "223"],
                correctAnswer: 1
            },
            {
                question: "Я знаю, вы устали, но осталось совсем чуточку: сколько дней между др Маши-Мирославы и Евгении Голубкиной?",
                image: "222333.png", 
                options: ["3", "4", "2","1","Господи помоги...", "Господи не поможет, надо к ГоспоДи обращаться"],
                correctAnswer: 0
            },
            {
                question: "И вот... наконец 25-й вопрос... А если быть точнее... Мое маленькое откровение:",
                image: "", 
                options: ["    Мои самые дорогие, мои мужья, жёны, други и просто мои самые любимые человеки! ❤️ Простите тысячу раз, что я так подвела вас в ваш день из-за этого проклятого синусита. Мне было так горько и обидно не быть рядом! Мой Грустный Солнечный Котенок, Машенька, и моя нежная Голубка, Женечка – я вас безумно сильно люблю. Вы – мой главный комфорт в этой жизни, моё самое тёплое и надёжное место. Всё, что мы прошли вместе – эвери варм энд эвери сэд моментс – это лучшее, что было в моей жизни. Я буду носить это в сердце до самого конца. Наши фотосессии до 7 утра, наши прогулки, истории, презентации на английский, бутербродики, песни и все персонажи... (Да всё не перечислить!) – всё это бесценно. Я до сих пор вспоминаю тех самых совушек и безмерно рада, что мы перекочевали в наше легендарное ASS! ✨ Спасибо вам за каждую секунду поддержки, понимания и этой сумасшедшей любви. Я бесконечно благодарна и готова идти с вами дальше, до самого конца. Пусть наша звезда ASS горит вечно и ярко! А вы никогда не забывайте, как много вы значите для меня и сколько всего волшебного мы уже сделали. Впереди только больше, только лучше! Я вас обожаю. Ваша Любовь, верный друг и просто Сашечка 🤧💖🤝"],
                correctAnswer: 0
            },
            {
                question: "Ага! Опять попались! Это не конец!!! БЫСТРО ОТВЕЧАЙТЕ: 2+2=...",
                image: "", 
                options: ["6", "66", "КРИС!!!!!!!!","666","6666", "6666666..."],
                correctAnswer: 2
            },
            {
                question: "ТИШЕ! Они в эдите...",
                image: "5319284170117215541.jpg", 
                options: ["..."],
                correctAnswer: 0
            },
            {
                question: "Ладно, простите... Я ВАС ОЧЕНЬ ЛЮБЛЮ!!!!",
                image: "", 
                options: ["..............44....................44............", "......44.........44........44.........44......", "4........................4........................4","И МЫ ТЕБЯ!!!!","........4.......................................4....", ".............4..............................4........", "....................4................4...............", "..............................4......................."],
                correctAnswer: 3
            }
        ];

        const giftData = {
            message: "Солнышки мои! Этот небольшой квест — лишь намёк на то, как я вас люблю и ценю! А настоящий подарок...",
            image: "с др.jpg",
            links: [
                { text: "💬💌 Стикерпак 'ASS' в Telegram", url: "https://t.me/addstickers/Ass_iSasni" }, 
                { text: "💋❤️ Аватакри для Telegram", url: "https://drive.google.com/drive/folders/1xeENzplac_z4eZ_BpZTx6LovIxMvkk0P" },
                { text: "🧐👅Эксклюзивный язык в Telegram  'Под яблоней'", url: "https://t.me/setlanguage/apple472" },
                { text: "🎨💟 Эксклюзивная тема Telegram  'Под яблоней'", url: "https://t.me/addtheme/KjBNGvMba0kccJMY" },
                { text: "❣️Картина 'Под яблоней' для вас❣️", url: "https://drive.google.com/drive/folders/1cEFH5ENg-WOe--78VHWHD28iXl80RJaT" },
                { text: "Чтобы открыть ссылки на телефоне, нажмите сюда. Она перенесёт вас в чат, в который нужно вступить. Обязательно зайдите в него после с вашего телефона!", url: "https://t.me/+lNAUtowzU1Q0NWZi" } 
            ]
        };

        // ========== ЛОГИКА ВИКТОРИНЫ ==========
        let currentQuestionIndex = 0;
        let score = 0;
        let errorCount = 0;
        let lives = 5;

        const warningScreen = document.getElementById('warning-screen');
        const quizScreen = document.getElementById('quiz-screen');
        const giftScreen = document.getElementById('gift-screen');
        const deathScreen = document.getElementById('death-screen');
        const questionImageEl = document.getElementById('question-image');
        const questionTextEl = document.getElementById('question-text');
        const optionsContainerEl = document.getElementById('options-container');
        const nextButton = document.getElementById('next-btn');
        const resultEl = document.getElementById('result');
        const giftImageEl = document.getElementById('gift-image');
        const giftMessageEl = document.getElementById('gift-message');
        const giftLinksEl = document.getElementById('gift-links');
        const restartButton = document.getElementById('restart-btn');
        const retryButton = document.getElementById('retry-btn');
        const progressEl = document.getElementById('progress');
        const startButton = document.getElementById('start-btn');
        const livesDisplay = document.getElementById('lives-display');

        // Показываем предупреждение при загрузке
        window.addEventListener('load', function() {
            warningScreen.classList.remove('hidden');
            quizScreen.classList.add('hidden');
            giftScreen.classList.add('hidden');
            deathScreen.classList.add('hidden');
            livesDisplay.classList.add('hidden');
        });

        startButton.addEventListener('click', function() {
            warningScreen.classList.add('hidden');
            quizScreen.classList.remove('hidden');
            livesDisplay.classList.remove('hidden');
            startQuiz();
        });

        retryButton.addEventListener('click', function() {
            deathScreen.classList.add('hidden');
            quizScreen.classList.remove('hidden');
            livesDisplay.classList.remove('hidden');
            startQuiz();
        });

        function startQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            errorCount = 0;
            lives = 5;
            updateLivesDisplay();
            showQuestion();
        }

        function updateLivesDisplay() {
            let livesHTML = '';
            for (let i = 0; i < 5; i++) {
                livesHTML += i < lives ? '❤️' : '🖤';
            }
            livesDisplay.innerHTML = livesHTML;
        }

        function showQuestion() {
            resultEl.textContent = '';
            nextButton.style.display = 'none';

            const currentQuestion = questions[currentQuestionIndex];
            questionTextEl.textContent = currentQuestion.question;
            
            // Всегда "25 вопросов" для эффекта неожиданности
            progressEl.textContent = `Вопрос ${Math.min(currentQuestionIndex + 1, 25)} из 25`;

            // Работа с картинкой 
            if (currentQuestion.image && currentQuestion.image.trim() !== "") {
                questionImageEl.src = currentQuestion.image;
                questionImageEl.style.display = 'block';
                questionImageEl.alt = "Изображение к вопросу";
            } else {
                questionImageEl.style.display = 'none';
            }

            optionsContainerEl.innerHTML = '';
            currentQuestion.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.textContent = option;
                button.classList.add('option-btn');
                button.addEventListener('click', function() {
                    selectAnswer(index);
                });
                optionsContainerEl.appendChild(button);
            });
        }

        function selectAnswer(selectedIndex) {
            const correctIndex = questions[currentQuestionIndex].correctAnswer;
            const allButtons = optionsContainerEl.querySelectorAll('button.option-btn');

            allButtons.forEach(btn => btn.disabled = true);

            if (selectedIndex === correctIndex) {
                resultEl.textContent = 'Правильно! 💋';
                resultEl.style.color = '#2e7d32';
                score++;
            } else {
                resultEl.textContent = 'Неправильно 😡! Правильный ответ: "' + questions[currentQuestionIndex].options[correctIndex] + '"';
                resultEl.style.color = '#d32f2f';
                errorCount++;
                lives--;
                updateLivesDisplay();
                
                // Проверяем, не закончились ли жизни
                if (lives <= 0) {
                    setTimeout(showDeathScreen, 1500);
                    return;
                }
            }

            // Показываем кнопку "Далее" только если это НЕ последний вопрос
            if (currentQuestionIndex < questions.length - 1) {
                nextButton.style.display = 'block';
            } else {
                // Если это последний вопрос, сразу показываем подарок
                setTimeout(showGift, 1500);
            }
        }

        nextButton.addEventListener('click', function() {
            currentQuestionIndex++;
            showQuestion();
        });

        restartButton.addEventListener('click', function() {
            giftScreen.classList.add('hidden');
            quizScreen.classList.remove('hidden');
            livesDisplay.classList.remove('hidden');
            startQuiz();
        });

        function showDeathScreen() {
            quizScreen.classList.add('hidden');
            livesDisplay.classList.add('hidden');
            deathScreen.classList.remove('hidden');
        }

        function showGift() {
            quizScreen.classList.add('hidden');
            livesDisplay.classList.add('hidden');
            giftScreen.classList.remove('hidden');

            // Проверяем, можно ли получить подарок
            if (errorCount >= 5) {
                showDeathScreen();
            } else {
                giftMessageEl.textContent = giftData.message;

                if (giftData.image && giftData.image.trim() !== "") {
                    giftImageEl.src = giftData.image;
                    giftImageEl.style.display = 'block';
                    giftImageEl.alt = "Ваш подарок";
                } else {
                    giftImageEl.style.display = 'none';
                }

                giftLinksEl.innerHTML = '<h3>Переходите по ссылочкам и забирайте свои подарки:</h3>';
                giftData.links.forEach(link => {
                    const linkEl = document.createElement('a');
                    linkEl.href = link.url;
                    linkEl.textContent = link.text;
                    linkEl.target = '_blank';
                    linkEl.style.display = 'block';
                    linkEl.style.margin = '10px 0';
                    linkEl.style.fontSize = '18px';
                    linkEl.style.color = '#2e7d32';
                    linkEl.style.textDecoration = 'none';
                    linkEl.style.fontWeight = 'bold';
                    linkEl.addEventListener('mouseover', function() {
                        this.style.color = '#4caf50';
                    });
                    linkEl.addEventListener('mouseout', function() {
                        this.style.color = '#2e7d32';
                    });
                    giftLinksEl.appendChild(linkEl);
                });
            }
        }
    </script>
</body>
</html>
