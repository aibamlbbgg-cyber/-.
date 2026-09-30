# Кіріндееер

<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Апайлар туралы тест</title>
<style>
* {
    box-sizing: border-box;
}
body {
    margin: 0;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #ffd6e7, #e8dcff);
    color: #222;
    overflow-x: hidden;
}
body.jasmin {
    background:
        radial-gradient(circle at top, #fff0f7, transparent 45%),
        linear-gradient(135deg, #ffc8dc, #ded0ff);
}
/* ОСНОВНОЙ ЭКРАН */
.screen {
    width: 92%;
    max-width: 700px;
    text-align: center;
    padding: 25px 15px;
    animation: appear .45s ease;
}
/* ВОПРОС */
.question-box {
    background: rgba(255,255,255,.96);
    border-radius: 28px;
    padding: 30px 22px;
    margin-bottom: 25px;
    border: 3px solid rgba(255,105,150,.35);
    box-shadow:
        0 12px 35px rgba(0,0,0,.12),
        0 0 25px rgba(255,100,160,.15);
}
.question-number {
    font-size: 17px;
    font-weight: bold;
    color: #ff4f81;
    margin-bottom: 12px;
}
.question {
    font-size: clamp(25px, 6vw, 36px);
    font-weight: 800;
    line-height: 1.35;
    color: #202020;
}
/* ВАРИАНТЫ */
.answers {
    display: flex;
    flex-direction: column;
    gap: 14px;
}
.answer {
    width: 100%;
    padding: 18px 20px;
    border: none;
    border-radius: 17px;
    background: white;
    font-size: 20px;
    font-weight: bold;
    text-align: left;
    cursor: pointer;
    box-shadow: 0 6px 18px rgba(0,0,0,.10);
    transition: .2s;
}
.answer:hover {
    transform: translateY(-2px);
}
.answer:active {
    transform: scale(.97);
}
/* КНОПКА NEXT */
.next {
    margin-top: 28px;
    padding: 16px 50px;
    border: none;
    border-radius: 18px;
    background: #35c759;
    color: white;
    font-size: 21px;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 7px 18px rgba(0,0,0,.15);
    transition: .2s;
}
.next:hover {
    transform: scale(1.04);
}
/* РЕЗУЛЬТАТ */
.result {
    background: rgba(255,255,255,.96);
    border-radius: 30px;
    padding: 40px 25px;
    box-shadow: 0 15px 45px rgba(0,0,0,.15);
    animation: appear .45s ease;
}
.result h2 {
    font-size: clamp(27px, 7vw, 40px);
    line-height: 1.35;
    margin: 0;
}
.correct {
    margin-top: 20px;
    padding: 15px;
    border-radius: 15px;
    background: #e9f9ee;
    color: #159447;
    font-size: 19px;
    font-weight: bold;
}
/* НАЧАЛЬНЫЕ КНОПКИ */
.choice {
    border: none;
    border-radius: 17px;
    padding: 17px 38px;
    font-size: 22px;
    font-weight: bold;
    cursor: pointer;
    margin: 8px;
}
.yes {
    background: #35c759;
    color: white;
}
.no {
    background: #ff3b30;
    color: white;
}
/* ФИНАЛЬНЫЙ ЭКРАН */
.final-screen {
    width: 94%;
    max-width: 850px;
    min-height: 85vh;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: finalAppear 1s ease;
}
.final-card {
    width: 100%;
    padding: 55px 30px;
    border-radius: 35px;
    background: rgba(255,255,255,.97);
    box-shadow:
        0 20px 60px rgba(0,0,0,.2),
        0 0 45px rgba(255,80,140,.25);
    border: 3px solid rgba(255,100,150,.3);
    text-align: center;
    position: relative;
}
.final-title {
    font-size: clamp(30px, 7vw, 48px);
    font-weight: 900;
    color: #ff477e;
    margin-bottom: 35px;
    line-height: 1.2;
}
.final-message {
    font-size: clamp(21px, 5vw, 30px);
    line-height: 1.6;
    font-weight: 600;
    color: #333;
}
.final-highlight {
    margin-top: 35px;
    padding: 22px;
    border-radius: 20px;
    background: linear-gradient(
        135deg,
        #fff0f5,
        #f2eaff
    );
    font-size: clamp(22px, 5vw, 31px);
    font-weight: 800;
    color: #e83d72;
}
.heart {
    font-size: 55px;
    margin-bottom: 15px;
}
/* АНИМАЦИИ */
@keyframes appear {
    from {
        opacity: 0;
        transform: translateY(20px) scale(.95);
    }
    to {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}
@keyframes finalAppear {
    from {
        opacity: 0;
        transform: scale(.8);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}
</style>
</head>
<body>
<div id="app"></div>

<script>

const app = document.getElementById("app");
let current = 0;

/* ==========================
   ПЕРВЫЙ ЭКРАН
========================== */

function startScreen() {
    app.innerHTML = `
        <div class="screen">
            <div class="result">
                <h2>
                    Аяла апай туралы тест
                    өтуге дайынсыңдарма?
                </h2>
                <br>
                <button
                    class="choice yes"
                    onclick="startTest()">
                    Ия
                </button>
                <button
                    class="choice no"
                    id="noButton"
                    onclick="runAway()">
                    Жоқ
                </button>
            </div>
        </div>
    `;
}

/* ЖОҚ ҚАШАДЫ */

function runAway() {
    const no = document.getElementById("noButton");

    let size =
        parseFloat(no.dataset.size || "1");

    size -= .13;

    if (size < .2)
        size = .2;

    no.dataset.size = size;

    no.style.transform =
        `scale(${size})`;

    no.style.position = "fixed";

    const maxX =
        window.innerWidth -
        no.offsetWidth;

    const maxY =
        window.innerHeight -
        no.offsetHeight;

    no.style.left =
        Math.max(5, Math.random() * maxX) + "px";

    no.style.top =
        Math.max(5, Math.random() * maxY) + "px";

    const yes =
        document.querySelector(".yes");

    let yesSize =
        parseFloat(yes.dataset.size || "1");

    yesSize += .13;

    yes.dataset.size = yesSize;

    yes.style.transform =
        `scale(${yesSize})`;
}

/* ==========================
   ЖАСМИН ТУРАЛЫ ЕСТЕЙМІЗ
========================== */

function startTest() {
    app.innerHTML = `
        <div class="screen">
            <div class="result">
                <div class="heart">
                    ❤️
                </div>
                <h2>
                    Жасмин апайдыда
                    ұмытпайықта
                </h2>
                <button
                    class="next"
                    onclick="showQuestion(0)">
                    NEXT ➜
                </button>
            </div>
        </div>
    `;
}

/* ==========================
   СҰРАҚТАР
========================== */

const questions = [

{
    text: "Аяла апайдың ҰБТ-да таңдаған пәндері қандай?",
    answers: [
        "Гео-Англ",
        "Гео-Мат",
        "Гео-Джт",
        "Гео-Био"
    ],
    correct: 0,
    right: "Красавчик, адам боласың",
    wrong: "Таста, газель айдайсың"
},

{
    text: "Аяла апай қай университетке түсті?",
    answers: [
        "MNU",
        "NARXOZ",
        "Ену",
        "Сатбаев"
    ],
    correct: 1,
    right: "Е красавчик, жаттапсың",
    wrong: "Қадалдыңғо брат"
},

{
    text: "Аяла апайдың қандай хоббиы бар?",
    answers: [
        "Кубик Рубик жинау",
        "Катокқа бару",
        "Тауға міну",
        "Аниме көру"
    ],
    correct: 2,
    right: "Базар Джексон, мына жақта қадалама деп ойлагам",
    wrong: "Шайдыңғо, қате"
},

{
    text: "Аяла апайдың мектеп кезінде қандай увлечениялары бар еді?",
    answers: [
        "Сурет салу",
        "Дебатқа қатысу",
        "ДШ-да волейбол ойнау",
        "Математика шығарып отыру"
    ],
    correct: 1,
    right: "Ияяя, апайымыз мықты болған",
    wrong: "Қатеее("
},

{
    text: "Аяла апай ҰБТ-дан потолок неше балл алған?",
    answers: [
        "133",
        "48",
        "120",
        "123"
    ],
    correct: 0,
    right: "Дұрыыысс",
    wrong: "Апай простой емес, 133 алған"
},

/* ==========================
   НОВЫЙ ВОПРОС ПРО ЖАСМИН
========================== */

{
    text: "Жасмин апайымыздың кумиры",
    answers: [
        "Илон Маск",
        "Майкол Дженсон",
        "Стивен Джобс",
        "Железный человек"
    ],
    correct: 1,
    michaelQuestion: true
},

{
    text: "Жасмин апайымыздың қандай бизнестары болған?",
    answers: [
        "Киім тоқып сату",
        "Кішкентай балаларға қарау",
        "Парфюм сату",
        "Сурет сату"
    ],
    correct: 0,
    right: "Ияяя, апайымыз талантқо",
    wrong: "Қатеее("
},

{
    text: "Жасмин апайымыз жақсы көретін түсі?",
    answers: [
        "Темно-синий",
        "Розовый",
        "Красный",
        "Фиолетовый"
    ],
    correct: 2,
    right: "Ияяя, аватаркасыда қызылғо",
    wrong: "Жақында емес"
},

{
    text: "Жасмин апай географиядан басқа қандай пәннен мұғалім болған?",
    answers: [
        "Қазақ тілі",
        "Ағылшын тілі",
        "Орыс тілі",
        "Математика"
    ],
    correct: 0,
    right: "Ияя, апайымыз патриотқо",
    wrong: "Қатееее"
},

{
    text: "Жасмин апайдың қандай аллергиясы бар?",
    answers: [
        "Лимонға",
        "Мысыққа",
        "Дәріге",
        "Аллергиясы болмаған"
    ],
    correct: 1,
    right: "Дұрысс, оның өзімен апай мысықтарды қатты жақсы көреді 🤣",
    wrong: "Өзбекстанға билет ала бер"
}

];

/* ==========================
   СҰРАҚТЫ КӨРСЕТУ
========================== */

function showQuestion(index) {

    current = index;

    document.body.classList.toggle(
        "jasmin",
        index >= 5
    );

    const q = questions[index];

    const letters =
        ["A", "В", "С", "Д"];

    let html = `
        <div class="screen">
            <div class="question-box">

                <div class="question-number">
                    СҰРАҚ ${index + 1} / ${questions.length}
                </div>

                <div class="question">
                    ${q.text}
                </div>

            </div>

            <div class="answers">
    `;

    q.answers.forEach((answer, i) => {

        html += `
            <button
                class="answer"
                onclick="answerQuestion(${i})">

                ${letters[i]}) ${answer}

            </button>
        `;

    });

    html += `
            </div>
        </div>
    `;

    app.innerHTML = html;
}

/* ==========================
   ОТВЕТ
========================== */

function answerQuestion(selected) {

    const q = questions[current];

    /* СПЕЦИАЛЬНЫЙ ВОПРОС */

    if (q.michaelQuestion) {

        /*
        Вариант В — отдельный экран
        */

        if (selected === q.correct) {

            app.innerHTML = `
                <div class="screen">
                    <div class="result">

                        <div class="heart">
                            🕺
                        </div>

                        <h2>
                            Майкл Джексон
                        </h2>

                        <button
                            class="next"
                            onclick="nextQuestion()">
                            NEXT ➜
                        </button>

                    </div>
                </div>
            `;

            return;
        }

        /*
        А, С, Д — обычный экран
        */

        app.innerHTML = `
            <div class="screen">
                <div class="result">

                    <h2>
                        Неправильно
                    </h2>

                    <div class="correct">
                        ✓ Дұрыс жауап:
                        В) Майкол Дженсон
                    </div>

                    <button
                        class="next"
                        onclick="nextQuestion()">
                        NEXT ➜
                    </button>

                </div>
            </div>
        `;

        return;
    }

    /* ОБЫЧНЫЕ ВОПРОСЫ */

    const correct =
        selected === q.correct;

    let correctText = "";

    if (!correct) {

        const letters =
            ["A", "В", "С", "Д"];

        correctText = `
            <div class="correct">
                ✓ Дұрыс жауап:
                ${letters[q.correct]})
                ${q.answers[q.correct]}
            </div>
        `;
    }

    app.innerHTML = `
        <div class="screen">

            <div class="result">

                <h2>
                    ${correct
                        ? q.right
                        : q.wrong}
                </h2>

                ${correctText}

                <button
                    class="next"
                    onclick="nextQuestion()">
                    NEXT ➜
                </button>

            </div>

        </div>
    `;
}

/* ==========================
   NEXT
========================== */

function nextQuestion() {

    if (current < questions.length - 1) {

        /*
        После 5-го вопроса
        сразу идём на новый вопрос
        про Жасмин.
        */

        if (current === 4) {

            showQuestion(5);

        } else {

            showQuestion(current + 1);

        }

    } else {

        showEnd();

    }
}

/* ==========================
   ПЕРЕХОД
========================== */

function showTransition() {

    document.body.classList.remove("jasmin");

    app.innerHTML = `
        <div class="screen">

            <div class="result">

                <div class="heart">
                    ❤️
                </div>

                <div class="final-message">

                    Аллл Аяла апайымыз туралы
                    қызықты мәлімет естідіңдер
                    деген ойдамын.

                    <br><br>

                    Ал енді
                    <b>Жасмин апайымызға</b>
                    кеттік😍

                </div>

                <button
                    class="next"
                    onclick="showQuestion(5)">
                    NEXT ➜
                </button>

            </div>

        </div>
    `;
}

/* ==========================
   СОҢҒЫ ЭКРАН
========================== */

function showEnd() {

    document.body.classList.add("jasmin");

    app.innerHTML = `
        <div class="screen">

            <div class="result">

                <div class="heart">
                    ❤️
                </div>

                <div class="final-message">

                    Сонымен сұрақтар бітті,
                    осы сәтті қолданып
                    айтар сөзім бар.

                </div>

                <button
                    class="next"
                    onclick="showGoodbye()">
                    Келесі ➜
                </button>

            </div>

        </div>
    `;
}

/* ==========================
   ҮЛКЕН ҚОШТАСУ ЭКРАНЫ
========================== */

function showGoodbye() {

    document.body.classList.add("jasmin");

    app.innerHTML = `
        <div class="final-screen">

            <div class="final-card">

                <div class="heart">
                    ❤️
                </div>

                <div class="final-title">

                    Жасмин апайымызға
                    <br>
                    арнаймыз

                </div>

                <div class="final-message">

                    Осы жақын уақытта
                    Жасмин апайымыз кетейін
                    деп жатыр😔

                    <br><br>

                    Жасмин апайдың бізге келгеніне
                    көп болмаса да, көбімізге
                    көмектесіп, ориентир жасауға
                    көмек беріп үлгерді.

                </div>

                <div class="final-highlight">

                    Апайымызға бар алғысымызды
                    айтып қоштасайық ❤️

                </div>

            </div>

        </div>
    `;
}

/* START */

startScreen();

</script>
</body>
</html>
