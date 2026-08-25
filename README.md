<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0,
               maximum-scale=1.0, user-scalable=no">

<title>Cozinheiro Maluco</title>

<style>
/* =========================================================
   COZINHEIRO MALUCO
   ESTILO PIXEL ART 2D
========================================================= */

* {
    box-sizing: border-box;
}

html,
body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    background: #101725;
    color: white;
    font-family: "Courier New", monospace;
}

body {
    image-rendering: pixelated;
}

/* =========================================================
   CONTAINER PRINCIPAL
========================================================= */

#game {
    width: 100%;
    height: 100svh;
    min-height: 600px;
    display: flex;
    flex-direction: column;
    position: relative;
    overflow: hidden;
}

/* =========================================================
   TOPO
========================================================= */

#topbar {
    height: 74px;
    min-height: 74px;
    background: #111a2a;
    border-bottom: 4px solid #263652;

    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 0 25px;
    z-index: 5;
}

.logo {
    color: #ffd83d;
    font-size: clamp(20px, 3vw, 34px);
    font-weight: bold;
    letter-spacing: 2px;
    text-shadow:
        3px 3px 0 #7c5010;
}

.stats {
    display: flex;
    gap: 25px;
    align-items: center;
    font-size: 18px;
    font-weight: bold;
}

.stat {
    padding: 7px 12px;
    border: 2px solid #334463;
    background: #172238;
}

#timer {
    color: #fff;
}

#timer.danger {
    color: #ff5252;
    animation: dangerBlink .5s infinite alternate;
}

@keyframes dangerBlink {
    from { opacity: 1; }
    to { opacity: .45; }
}

/* =========================================================
   CENÁRIO PIXEL ART
========================================================= */

#scene {
    position: relative;
    flex: 1;
    min-height: 280px;
    overflow: hidden;

    background:
        linear-gradient(#4bb6dc 0 62%, #79c96b 62% 65%, #81502f 65%);
}

/* tijolos da parede */

#scene::before {
    content: "";
    position: absolute;
    inset: 0;

    background:
        repeating-linear-gradient(
            0deg,
            transparent 0 42px,
            rgba(255,255,255,.13) 43px 46px
        ),
        repeating-linear-gradient(
            90deg,
            transparent 0 72px,
            rgba(0,0,0,.13) 73px 76px
        );

    pointer-events: none;
}

/* chão */

.floor {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 34%;

    background:
        repeating-linear-gradient(
            90deg,
            #714526 0 55px,
            #58361f 55px 59px
        );

    border-top: 7px solid #b66a37;
}

/* =========================================================
   NUVENS
========================================================= */

.cloud {
    position: absolute;
    width: 90px;
    height: 24px;
    background: #eaf8ff;
    opacity: .8;
}

.cloud::before,
.cloud::after {
    content: "";
    position: absolute;
    background: #eaf8ff;
}

.cloud::before {
    width: 40px;
    height: 40px;
    left: 18px;
    top: -17px;
}

.cloud::after {
    width: 35px;
    height: 35px;
    right: 10px;
    top: -12px;
}

.cloud1 {
    top: 35px;
    left: 8%;
}

.cloud2 {
    top: 80px;
    right: 16%;
    transform: scale(.7);
}

/* =========================================================
   COZINHA
========================================================= */

.station {
    position: absolute;
    bottom: 32%;
    height: 105px;
    width: 190px;

    background: #242424;
    border: 10px solid #373737;

    display: flex;
    align-items: flex-end;
    justify-content: center;

    box-shadow:
        inset 0 -12px #171717,
        8px 8px rgba(0,0,0,.25);
}

.station span {
    position: absolute;
    bottom: -38px;
    color: #ffd83d;
    font-weight: bold;
    font-size: 18px;
    white-space: nowrap;
}

.oven {
    left: 7%;
}

.grill {
    left: 50%;
    transform: translateX(-50%);
}

.counter {
    right: 7%;
}

.ovenDoor {
    width: 120px;
    height: 60px;
    background: #171717;
    border: 6px solid #111;
}

.grillTop {
    width: 125px;
    height: 15px;
    background:
        repeating-linear-gradient(
            90deg,
            #111 0 12px,
            #777 12px 16px
        );
    margin-bottom: 25px;
}

/* =========================================================
   INGREDIENTES VISUAIS
========================================================= */

.food {
    position: absolute;
    width: 35px;
    height: 35px;
    bottom: 36%;
    z-index: 2;
}

.bread {
    background: #e9a743;
    border-radius: 8px 8px 3px 3px;
}

.cheese {
    background: #ffd83d;
    transform: rotate(3deg);
}

.tomato {
    background: #e94c4c;
    border-radius: 50%;
}

.lettuce {
    background: #54bd5d;
    border-radius: 8px;
}

.onion {
    background: #d18ae0;
    border-radius: 50%;
}

/* =========================================================
   COZINHEIRO PIXEL
========================================================= */

#chef {
    position: absolute;

    left: 50%;
    bottom: 31%;

    width: 72px;
    height: 120px;

    transform: translateX(-50%);
    z-index: 4;

    transition: left .08s linear;
}

/* cabeça */

.head {
    position: absolute;
    width: 55px;
    height: 55px;

    left: 9px;
    top: 20px;

    background: #d99769;
}

.eye {
    position: absolute;
    width: 7px;
    height: 7px;
    background: #111;
    top: 22px;
}

.eye.left {
    left: 12px;
}

.eye.right {
    right: 12px;
}

.mouth {
    position: absolute;
    width: 20px;
    height: 5px;
    background: #111;
    bottom: 12px;
    left: 17px;
}

/* chapéu */

.hat {
    position: absolute;
    width: 70px;
    height: 22px;

    left: 1px;
    top: 5px;

    background: #fff;
}

.hat::before {
    content: "";
    position: absolute;

    width: 48px;
    height: 25px;

    left: 11px;
    top: -18px;

    background: #fff;
}

/* corpo */

.body {
    position: absolute;
    width: 72px;
    height: 62px;

    bottom: 0;
    background: #f3f3f3;
}

/* braços */

.arm {
    position: absolute;
    width: 17px;
    height: 48px;
    background: #d99769;
    top: 67px;
}

.arm.left {
    left: -12px;
    transform: rotate(18deg);
}

.arm.right {
    right: -12px;
    transform: rotate(-18deg);
}

/* =========================================================
   PAINEL INFERIOR
========================================================= */

#bottom {
    height: 34%;
    min-height: 210px;

    background: #111a2a;

    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;

    padding: 12px;

    border-top: 5px solid #283852;
}

.panel {
    background: #151f32;
    border: 3px solid #334463;
    padding: 14px;

    overflow: hidden;
}

.panel-title {
    color: #ffd83d;
    font-size: 21px;
    font-weight: bold;
    margin-bottom: 10px;
}

#orderText {
    line-height: 1.45;
    font-size: 17px;
}

#ingredientsList {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 7px;
}

.ingredient {
    border: 2px solid #405476;
    background: #1b2940;
    padding: 8px;

    min-width: 0;

    font-weight: bold;
    font-size: 14px;
}

.ingredient.selected {
    background: #315c47;
    border-color: #70e090;
}

.key {
    color: #ffd83d;
    font-size: 18px;
}

/* =========================================================
   STATUS
========================================================= */

#status {
    position: absolute;

    left: 50%;
    bottom: calc(34% + 14px);

    transform: translateX(-50%);

    width: min(800px, 90%);

    padding: 10px 16px;

    background: rgba(8, 13, 22, .92);
    border: 3px solid #ffd83d;

    color: white;

    text-align: center;

    font-weight: bold;
    font-size: 16px;

    z-index: 10;

    pointer-events: none;
}

/* =========================================================
   TELA INICIAL
========================================================= */

#startScreen,
#gameOver {
    position: absolute;
    inset: 0;

    background:
        linear-gradient(
            rgba(8,14,24,.82),
            rgba(8,14,24,.94)
        );

    z-index: 100;

    display: flex;
    align-items: center;
    justify-content: center;

    padding: 20px;
}

.menuBox {
    width: min(760px, 95vw);

    background: #172238;

    border: 5px solid #50668d;

    box-shadow:
        10px 10px #080c14;

    padding: 30px;

    text-align: center;
}

.menuTitle {
    color: #ffd83d;

    font-size: clamp(30px, 6vw, 56px);

    font-weight: bold;

    text-shadow:
        4px 4px #7d5212;

    margin-bottom: 20px;
}

.startButton {
    display: inline-block;

    padding: 18px 35px;

    background: #d95b38;

    border: 4px solid #ffb14e;

    color: white;

    font-size: 24px;
    font-weight: bold;

    cursor: pointer;

    outline: none;

    box-shadow:
        0 7px #7f3221;
}

.startButton:hover,
.startButton:focus {
    background: #f06d43;
    transform: translateY(-2px);
}

.controls {
    margin-top: 25px;

    display: grid;

    grid-template-columns:
        repeat(2, minmax(200px, 1fr));

    gap: 8px;

    text-align: left;

    font-size: 15px;
}

.control {
    background: #101827;
    padding: 9px;
    border: 2px solid #30415f;
}

kbd {
    background: #f0f0f0;
    color: #111;
    border: 2px solid #999;

    padding: 2px 6px;

    font-weight: bold;
}

/* =========================================================
   MENU DO RATO
========================================================= */

#ratMenu {
    display: none;

    position: absolute;

    z-index: 80;

    left: 50%;
    top: 50%;

    transform: translate(-50%, -50%);

    width: min(520px, 90vw);

    background: #18243a;

    border: 5px solid #e3a33a;

    padding: 25px;

    text-align: center;
}

#ratMenu h2 {
    color: #ffd83d;
}

.ratOption {
    padding: 12px;
    margin: 7px 0;

    background: #111a2a;

    border: 2px solid #415473;
}

/* =========================================================
   GAME OVER
========================================================= */

#gameOver {
    display: none;
}

.gameOverTitle {
    color: #ff5a5a;
    font-size: 45px;
    font-weight: bold;
}

.restart {
    margin-top: 20px;
}

/* =========================================================
   RESPONSIVIDADE
========================================================= */

@media (max-width: 800px) {

    #topbar {
        padding: 0 10px;
    }

    .stats {
        gap: 7px;
        font-size: 13px;
    }

    .logo {
        font-size: 18px;
    }

    .station {
        transform: scale(.7);
        transform-origin: bottom;
    }

    .grill {
        left: 50%;
    }

    #bottom {
        grid-template-columns: 1fr;
        overflow-y: auto;
    }

    .panel {
        min-height: 150px;
    }

    #ingredientsList {
        grid-template-columns:
            repeat(4, minmax(60px, 1fr));
    }

    .controls {
        grid-template-columns: 1fr;
    }

    #status {
        bottom: 35%;
    }
}

@media (max-height: 700px) {

    #topbar {
        height: 58px;
        min-height: 58px;
    }

    #bottom {
        height: 38%;
    }

    #status {
        bottom: 39%;
    }

    .station {
        bottom: 35%;
    }

    #chef {
        bottom: 34%;
    }
}

/* =========================================================
   ACESSIBILIDADE
========================================================= */

.sr-only {
    position: absolute;

    width: 1px;
    height: 1px;

    padding: 0;
    margin: -1px;

    overflow: hidden;

    clip: rect(0, 0, 0, 0);

    white-space: nowrap;

    border: 0;
}

button {
    font-family: inherit;
}

:focus-visible {
    outline: 4px solid #65d9ff;
    outline-offset: 4px;
}
</style>
</head>

<body>

<div id="game">

    <!-- =====================================================
         TOPO
    ====================================================== -->

    <header id="topbar">

        <div class="logo">
            🍳 COZINHEIRO MALUCO
        </div>

        <div class="stats">

            <div class="stat">
                ⭐ <span id="score">0</span>
            </div>

            <div class="stat">
                ⏱️ <span id="timer">03:00</span>
            </div>

            <div class="stat">
                📅 Dia <span id="day">1</span>
            </div>

        </div>

    </header>


    <!-- =====================================================
         CENÁRIO
    ====================================================== -->

    <main id="scene">

        <div class="cloud cloud1"></div>
        <div class="cloud cloud2"></div>

        <div class="station oven">
            <div class="ovenDoor"></div>
            <span>FORNO</span>
        </div>

        <div class="station grill">
            <div class="grillTop"></div>
            <span>CHAPA</span>
        </div>

        <div class="station counter">
            <span>BALCÃO</span>
        </div>

        <div class="floor"></div>

        <!-- Ingredientes decorativos -->

        <div class="food bread"
             style="left:24%;"></div>

        <div class="food tomato"
             style="left:73%;"></div>

        <div class="food lettuce"
             style="left:82%;"></div>

        <!-- COZINHEIRO -->

        <div id="chef">

            <div class="hat"></div>

            <div class="head">

                <div class="eye left"></div>
                <div class="eye right"></div>

                <div class="mouth"></div>

            </div>

            <div class="arm left"></div>
            <div class="arm right"></div>

            <div class="body"></div>

        </div>

        <div id="status">
            Aguardando...
        </div>

    </main>


    <!-- =====================================================
         PAINÉIS
    ====================================================== -->

    <section id="bottom">

        <div class="panel">

            <div class="panel-title">
                📋 PEDIDO
            </div>

            <div id="orderText">
                Nenhum pedido ainda.
                Pressione E para ouvir o pedido.
            </div>

        </div>


        <div class="panel">

            <div class="panel-title">
                🧺 INGREDIENTES
            </div>

            <div id="ingredientsList">

                <div class="ingredient"
                     data-key="1">
                    <span class="key">1</span>
                    Pão
                </div>

                <div class="ingredient"
                     data-key="2">
                    <span class="key">2</span>
                    Carne
                </div>

                <div class="ingredient"
                     data-key="3">
                    <span class="key">3</span>
                    Queijo
                </div>

                <div class="ingredient"
                     data-key="4">
                    <span class="key">4</span>
                    Tomate
                </div>

                <div class="ingredient"
                     data-key="5">
                    <span class="key">5</span>
                    Alface
                </div>

                <div class="ingredient"
                     data-key="6">
                    <span class="key">6</span>
                    Molho
                </div>

                <div class="ingredient"
                     data-key="7">
                    <span class="key">7</span>
                    Cebola
                </div>

            </div>

        </div>

    </section>


    <!-- =====================================================
         MENU INICIAL
    ====================================================== -->

    <div id="startScreen">

        <div class="menuBox">

            <div class="menuTitle">
                🍳 COZINHEIRO MALUCO
            </div>

            <p>
                Uma cozinha pixel art onde você precisa
                preparar pedidos antes que o tempo acabe!
            </p>

            <button
                id="startButton"
                class="startButton"
                type="button"
                aria-label="Começar jogo, pressione Enter">

                COMEÇAR — ENTER

            </button>

            <div class="controls">

                <div class="control">
                    <kbd>ENTER</kbd>
                    Começar / preparar / entregar
                </div>

                <div class="control">
                    <kbd>E</kbd>
                    Ouvir pedido
                </div>

                <div class="control">
                    <kbd>1–7</kbd>
                    Ingredientes
                </div>

                <div class="control">
                    <kbd>BACKSPACE</kbd>
                    Remover ingrediente
                </div>

                <div class="control">
                    <kbd>Q</kbd>
                    Rato na cozinha
                </div>

                <div class="control">
                    <kbd>R</kbd>
                    Reabastecer estoque
                </div>

                <div class="control">
                    <kbd>W A S D</kbd>
                    Andar
                </div>

                <div class="control">
                    <kbd>SETAS</kbd>
                    Andar
                </div>

            </div>

            <p style="margin-top:20px;color:#ffd83d;">
                Tudo pode ser jogado pelo teclado.
            </p>

        </div>

    </div>


    <!-- =====================================================
         MENU RATO
    ====================================================== -->

    <div id="ratMenu">

        <h2>🐀 RATO NA COZINHA!</h2>

        <p>
            O rato entrou na despensa e está mexendo
            nos ingredientes!
        </p>

        <div class="ratOption">
            <strong>1 — ESPANTAR</strong><br>
            O rato foge e derruba um ingrediente.
        </div>

        <div class="ratOption">
            <strong>2 — IGNORAR</strong><br>
            O rato continua na cozinha e come um ingrediente.
        </div>

        <div class="ratOption">
            <strong>3 — CHAMAR O GERENTE</strong><br>
            O gerente resolve o problema, mas custa pontos.
        </div>

    </div>


    <!-- =====================================================
         GAME OVER
    ====================================================== -->

    <div id="gameOver">

        <div class="menuBox">

            <div class="gameOverTitle">
                FALÊNCIA!
            </div>

            <p id="gameOverText">
                O tempo acabou.
            </p>

            <button
                id="restartButton"
                class="startButton restart">

                RECOMEÇAR — ENTER

            </button>

        </div>

    </div>

</div>


<script>

/* =========================================================
   CONFIGURAÇÕES
========================================================= */

const GAME_TIME_START = 180; // 3 minutos
const BONUS_TIME = 7;
const ORDER_POINTS = 150;


/* =========================================================
   ELEMENTOS
========================================================= */

const startScreen =
    document.getElementById("startScreen");

const startButton =
    document.getElementById("startButton");

const restartButton =
    document.getElementById("restartButton");

const gameOver =
    document.getElementById("gameOver");

const gameOverText =
    document.getElementById("gameOverText");

const ratMenu =
    document.getElementById("ratMenu");

const scoreElement =
    document.getElementById("score");

const timerElement =
    document.getElementById("timer");

const dayElement =
    document.getElementById("day");

const orderText =
    document.getElementById("orderText");

const statusElement =
    document.getElementById("status");

const chef =
    document.getElementById("chef");


/* =========================================================
   ESTADO DO JOGO
========================================================= */

let gameStarted = false;

let gameOverState = false;

let score = 0;

let day = 1;

let timeLeft = GAME_TIME_START;

let timerInterval = null;

let ratMode = false;

let orderVisible = false;

let preparing = false;

let selectedIngredients = [];

let currentOrder = null;

let chefX = 50;

let inventory = {
    pao: 8,
    carne: 8,
    queijo: 8,
    tomate: 8,
    alface: 8,
    molho: 8,
    cebola: 8
};


/* =========================================================
   INGREDIENTES
========================================================= */

const ingredients = {

    "1": {
        id: "pao",
        name: "Pão"
    },

    "2": {
        id: "carne",
        name: "Carne"
    },

    "3": {
        id: "queijo",
        name: "Queijo"
    },

    "4": {
        id: "tomate",
        name: "Tomate"
    },

    "5": {
        id: "alface",
        name: "Alface"
    },

    "6": {
        id: "molho",
        name: "Molho"
    },

    "7": {
        id: "cebola",
        name: "Cebola"
    }

};


/* =========================================================
   PEDIDOS
========================================================= */

const orders = [

    {
        cliente: "Maria",
        prato: "Hambúrguer",
        ingredients: [
            "pao",
            "carne",
            "queijo",
            "tomate"
        ]
    },

    {
        cliente: "João",
        prato: "Hambúrguer completo",
        ingredients: [
            "pao",
            "carne",
            "queijo",
            "alface",
            "molho"
        ]
    },

    {
        cliente: "Ana",
        prato: "Hambúrguer especial",
        ingredients: [
            "pao",
            "carne",
            "queijo",
            "tomate",
            "cebola"
        ]
    },

    {
        cliente: "Pedro",
        prato: "X-salada",
        ingredients: [
            "pao",
            "carne",
            "queijo",
            "alface",
            "tomate",
            "molho"
        ]
    }

];

let orderIndex = 0;


/* =========================================================
   VOZ
========================================================= */

const synth =
    window.speechSynthesis;

let voices = [];


function loadVoices() {

    if (!synth) return;

    voices = synth.getVoices();

}


loadVoices();

if (synth) {

    synth.onvoiceschanged =
        loadVoices;

}


/* escolhe uma voz em português */

function getPortugueseVoice() {

    const ptBR =
        voices.find(v =>
            v.lang &&
            v.lang.toLowerCase()
                .startsWith("pt-br")
        );

    if (ptBR) return ptBR;


    const pt =
        voices.find(v =>
            v.lang &&
            v.lang.toLowerCase()
                .startsWith("pt")
        );

    if (pt) return pt;

    return null;
}


/* =========================================================
   FALA RÁPIDA
========================================================= */

function speak(text, options = {}) {

    if (!synth) return;

    synth.cancel();

    const utter =
        new SpeechSynthesisUtterance(text);

    const voice =
        getPortugueseVoice();

    if (voice) {
        utter.voice = voice;
    }

    utter.lang =
        voice ? voice.lang : "pt-BR";

    /*
       Mais rápido para evitar aquela fala
       extremamente lenta e robótica.
    */

    utter.rate =
        options.rate || 1.55;

    utter.pitch =
        options.pitch || 1.0;

    utter.volume =
        options.volume || 1.0;

    synth.speak(utter);

}


/* fala várias mensagens curtas */

async function speakSequence(messages) {

    for (const message of messages) {

        await new Promise(resolve => {

            if (!synth) {
                resolve();
                return;
            }

            const utter =
                new SpeechSynthesisUtterance(message);

            const voice =
                getPortugueseVoice();

            if (voice) {
                utter.voice = voice;
            }

            utter.lang =
                voice ? voice.lang : "pt-BR";

            utter.rate = 1.55;
            utter.pitch = 1.0;

            utter.onend = resolve;

            synth.speak(utter);

        });

    }

}


/* =========================================================
   HOVER DO BOTÃO COMEÇAR
========================================================= */

startButton.addEventListener(
    "mouseenter",
    () => {

        if (!gameStarted) {

            speak(
                "Começar. Pressione Enter.",
                { rate: 1.65 }
            );

        }

    }
);


startButton.addEventListener(
    "focus",
    () => {

        if (!gameStarted) {

            speak(
                "Começar. Pressione Enter.",
                { rate: 1.65 }
            );

        }

    }
);


/* =========================================================
   STATUS
========================================================= */

function setStatus(text) {

    statusElement.textContent =
        text;

}


/* =========================================================
   TIMER
========================================================= */

function updateTimer() {

    const minutes =
        Math.floor(timeLeft / 60);

    const seconds =
        timeLeft % 60;

    timerElement.textContent =
        `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;


    if (timeLeft <= 20) {

        timerElement.classList.add("danger");

    } else {

        timerElement.classList.remove("danger");

    }

}


function startTimer() {

    clearInterval(timerInterval);

    timerInterval =
        setInterval(() => {

            if (!gameStarted ||
                gameOverState) {
                return;
            }

            if (ratMode) {
                return;
            }

            timeLeft--;

            updateTimer();

            if (timeLeft <= 0) {

                timeLeft = 0;

                updateTimer();

                loseGame();

            }

        }, 1000);

}


/* =========================================================
   NOVO PEDIDO
========================================================= */

function createOrder() {

    currentOrder =
        orders[orderIndex % orders.length];

    orderIndex++;

    selectedIngredients = [];

    orderVisible = false;

    preparing = false;

    updateIngredientsVisual();

    orderText.innerHTML =
        `
        <strong>Novo pedido!</strong><br>
        Cliente: ${currentOrder.cliente}<br>
        Prato: ${currentOrder.prato}<br>
        <br>
        Pressione <strong>E</strong> para ouvir.
        `;

    setStatus(
        "🔔 Novo pedido! Pressione E."
    );

    speak(
        `Novo pedido. Cliente ${currentOrder.cliente}. ${currentOrder.prato}. Pressione E para ouvir.`,
        { rate: 1.5 }
    );

}


/* =========================================================
   OUVIR PEDIDO
========================================================= */

function readOrder() {

    if (!gameStarted ||
        gameOverState ||
        !currentOrder) {
        return;
    }

    orderVisible = true;

    const names =
        currentOrder.ingredients
            .map(id =>
                Object.values(ingredients)
                    .find(i => i.id === id)
                    ?.name
            );

    orderText.innerHTML =
        `
        <strong>Cliente: ${currentOrder.cliente}</strong><br>
        <strong>${currentOrder.prato}</strong><br><br>

        ${names.join(" + ")}
        `;

    speak(
        `Pedido de ${currentOrder.cliente}. ${currentOrder.prato}. Ingredientes: ${names.join(", ")}.`
    );

}


/* =========================================================
   INGREDIENTE
========================================================= */

function selectIngredient(key) {

    if (!gameStarted ||
        gameOverState ||
        ratMode ||
        preparing ||
        !currentOrder) {
        return;
    }

    const ingredient =
        ingredients[key];

    if (!ingredient) return;


    /* estoque */

    if (inventory[ingredient.id] <= 0) {

        speak(
            `${ingredient.name} acabou.`
        );

        setStatus(
            `❌ ${ingredient.name} acabou.`
        );

        return;
    }


    inventory[ingredient.id]--;

    selectedIngredients.push(
        ingredient.id
    );


    updateIngredientsVisual();


    speak(
        `${ingredient.name} selecionado.`,
        { rate: 1.7 }
    );


    setStatus(
        `${ingredient.name} selecionado.`
    );


    /*
       Verifica se colocou algo
       que não pertence ao pedido.
    */

    if (
        !currentOrder.ingredients
            .includes(ingredient.id)
    ) {

        speak(
            `${ingredient.name}. Atenção: o pedido não contém ${ingredient.name.toLowerCase()}. Pressione Backspace para remover.`
        );

        return;
    }


    /*
       Verifica se já possui todos
       os ingredientes necessários.
    */

    const allCorrect =
        currentOrder.ingredients.every(
            id =>
                selectedIngredients
                    .includes(id)
        );


    if (allCorrect) {

        const names =
            currentOrder.ingredients
                .map(id =>
                    Object.values(ingredients)
                        .find(i => i.id === id)
                        ?.name
                );

        speakSequence([

            "Todos os ingredientes necessários foram selecionados.",

            names.join(", ") + ".",

            "Pressione Enter para preparar o hambúrguer."

        ]);

        setStatus(
            "Todos os ingredientes corretos! ENTER para preparar."
        );

    }

}


/* =========================================================
   BACKSPACE
========================================================= */

function removeLastIngredient() {

    if (!gameStarted ||
        gameOverState ||
        ratMode ||
        preparing) {
        return;
    }

    if (selectedIngredients.length === 0) {

        speak(
            "Nenhum ingrediente para remover."
        );

        return;

    }


    const removed =
        selectedIngredients.pop();


    inventory[removed]++;


    const name =
        Object.values(ingredients)
            .find(i => i.id === removed)
            ?.name;


    updateIngredientsVisual();

    speak(
        `${name} removido.`,
        { rate: 1.7 }
    );

    setStatus(
        `${name} removido.`
    );

}


/* =========================================================
   VISUAL INGREDIENTES
========================================================= */

function updateIngredientsVisual() {

    document
        .querySelectorAll(".ingredient")
        .forEach(el => {

            el.classList.remove("selected");

            const key =
                el.dataset.key;

            const ingredient =
                ingredients[key];

            if (
                selectedIngredients
                    .includes(ingredient.id)
            ) {

                el.classList.add("selected");

            }

        });

}


/* =========================================================
   PREPARAR
========================================================= */

function prepareOrder() {

    if (!currentOrder ||
        preparing) {
        return;
    }


    const exact =
        selectedIngredients.length ===
        currentOrder.ingredients.length &&

        currentOrder.ingredients.every(
            id =>
                selectedIngredients
                    .includes(id)
        );


    if (!exact) {

        speak(
            "O pedido está errado. Verifique os ingredientes."
        );

        setStatus(
            "❌ Pedido incorreto."
        );

        return;

    }


    preparing = true;

    setStatus(
        "🍳 Preparando..."
    );

    speak(
        "Preparando.",
        { rate: 1.65 }
    );


    /*
       pequena animação da chapa
    */

    const grill =
        document.querySelector(".grill");

    grill.style.background =
        "#5b2d22";

    setTimeout(() => {

        grill.style.background =
            "#242424";

        speak(
            "Hambúrguer pronto.",
            { rate: 1.65 }
        );

        setStatus(
            `🍔 Hambúrguer pronto! ENTER para entregar a ${currentOrder.cliente}.`
        );

    }, 1100);

}


/* =========================================================
   ENTREGAR
========================================================= */

function deliverOrder() {

    if (!currentOrder ||
        !preparing) {
        return;
    }


    score += ORDER_POINTS;

    timeLeft += BONUS_TIME;


    scoreElement.textContent =
        score;

    updateTimer();


    const cliente =
        currentOrder.cliente;


    speakSequence([

        `Pedido entregue para ${cliente}.`,

        "Você ganhou 150 pontos.",

        "Mais 7 segundos adicionados."

    ]);


    setStatus(
        `🎉 Pedido perfeito! +150 pontos | +7 segundos`
    );


    /*
       Pequena pausa antes do próximo pedido
    */

    setTimeout(() => {

        createOrder();

    }, 1800);

}


/* =========================================================
   ENTER
========================================================= */

function handleEnter() {

    if (!gameStarted) {

        startGame();

        return;

    }


    if (gameOverState) {

        restartGame();

        return;

    }


    if (ratMode) {

        return;

    }


    if (!preparing) {

        /*
           Se os ingredientes estão corretos,
           prepara.
        */

        if (currentOrder) {

            const exact =
                selectedIngredients.length ===
                currentOrder.ingredients.length &&

                currentOrder.ingredients.every(
                    id =>
                        selectedIngredients
                            .includes(id)
                );


            if (exact) {

                prepareOrder();

                return;

            }

        }

    } else {

        deliverOrder();

    }

}


/* =========================================================
   RATO
========================================================= */

function openRatMenu() {

    if (!gameStarted ||
        gameOverState ||
        preparing) {
        return;
    }

    ratMode = true;

    ratMenu.style.display =
        "block";

    speakSequence([

        "Atenção! Rato na cozinha.",

        "Pressione 1 para espantar.",

        "Pressione 2 para ignorar.",

        "Pressione 3 para chamar o gerente."

    ]);

}


function closeRatMenu() {

    ratMode = false;

    ratMenu.style.display =
        "none";

}


/* =========================================================
   ESCOLHAS DO RATO
========================================================= */

function handleRatChoice(key) {

    if (!ratMode) return;


    /* 1 ESPANTAR */

    if (key === "1") {

        /*
           O rato derruba um ingrediente.
        */

        const possible =
            Object.keys(inventory)
                .filter(id =>
                    inventory[id] > 0
                );

        const chosen =
            possible[
                Math.floor(
                    Math.random() *
                    possible.length
                )
            ];


        if (chosen) {

            inventory[chosen]--;

            const name =
                Object.values(ingredients)
                    .find(i => i.id === chosen)
                    ?.name;

            speak(
                `Você espantou o rato. Ele derrubou ${name}.`
            );

            setStatus(
                `🐀 Rato espantado. ${name} foi derrubado.`
            );

        }

        closeRatMenu();

        return;

    }


    /* 2 IGNORAR */

    if (key === "2") {

        const possible =
            Object.keys(inventory)
                .filter(id =>
                    inventory[id] > 0
                );

        const chosen =
            possible[
                Math.floor(
                    Math.random() *
                    possible.length
                )
            ];


        if (chosen) {

            inventory[chosen]--;

            const name =
                Object.values(ingredients)
                    .find(i => i.id === chosen)
                    ?.name;

            speak(
                `Você ignorou o rato. Ele comeu ${name}.`
            );

            setStatus(
                `🐀 O rato comeu ${name}.`
            );

        }

        closeRatMenu();

        return;

    }


    /* 3 GERENTE */

    if (key === "3") {

        const cost = 50;

        if (score >= cost) {

            score -= cost;

            scoreElement.textContent =
                score;

            speak(
                "O gerente expulsou o rato. Custou 50 pontos."
            );

            setStatus(
                "👨‍💼 Gerente chamado. -50 pontos."
            );

        } else {

            speak(
                "Você não tem 50 pontos. O gerente não pode ser chamado."
            );

            setStatus(
                "❌ Pontos insuficientes."
            );

        }

        closeRatMenu();

    }

}


/* =========================================================
   REABASTECIMENTO
========================================================= */

function restock() {

    if (!gameStarted ||
        gameOverState ||
        ratMode) {
        return;
    }

    const cost = 25;

    if (score < cost) {

        speak(
            "Você precisa de 25 pontos para reabastecer."
        );

        setStatus(
            "❌ Faltam 25 pontos."
        );

        return;

    }


    score -= cost;


    for (const id in inventory) {

        inventory[id] = 8;

    }


    scoreElement.textContent =
        score;


    speak(
        "Despensa reabastecida. Custou 25 pontos."
    );

    setStatus(
        "🧺 Estoque reabastecido."
    );

}


/* =========================================================
   MOVIMENTO
========================================================= */

function moveChef(direction) {

    if (!gameStarted ||
        gameOverState ||
        ratMode) {
        return;
    }


    if (direction === "left") {

        chefX -= 2;

    }

    if (direction === "right") {

        chefX += 2;

    }


    chefX =
        Math.max(
            5,
            Math.min(
                95,
                chefX
            )
        );


    chef.style.left =
        chefX + "%";

}


/* =========================================================
   TECLADO
========================================================= */

document.addEventListener(
    "keydown",
    function(event) {

        const key =
            event.key;


        /*
           Impede o navegador de
           fazer coisas estranhas com
           espaço, setas e backspace.
        */

        if (
            [
                "ArrowUp",
                "ArrowDown",
                "ArrowLeft",
                "ArrowRight",
                "Backspace",
                " "
            ].includes(key)
        ) {

            event.preventDefault();

        }


        /* GAME OVER */

        if (gameOverState) {

            if (
                key === "Enter" ||
                key === " "
            ) {

                restartGame();

            }

            return;

        }


        /* MENU INICIAL */

        if (!gameStarted) {

            if (key === "Enter") {

                startGame();

            }

            return;

        }


        /* MENU DO RATO */

        if (ratMode) {

            if (
                ["1", "2", "3"]
                    .includes(key)
            ) {

                handleRatChoice(key);

            }

            return;

        }


        /* ENTER */

        if (key === "Enter") {

            handleEnter();

            return;

        }


        /* E */

        if (
            key.toLowerCase() === "e"
        ) {

            readOrder();

            return;

        }


        /* Q */

        if (
            key.toLowerCase() === "q"
        ) {

            openRatMenu();

            return;

        }


        /* R */

        if (
            key.toLowerCase() === "r"
        ) {

            restock();

            return;

        }


        /* BACKSPACE */

        if (key === "Backspace") {

            removeLastIngredient();

            return;

        }


        /* INGREDIENTES */

        if (
            ["1","2","3","4","5","6","7"]
                .includes(key)
        ) {

            selectIngredient(key);

            return;

        }


        /* MOVIMENTO */

        if (
            key === "ArrowLeft" ||
            key.toLowerCase() === "a"
        ) {

            moveChef("left");

        }


        if (
            key === "ArrowRight" ||
            key.toLowerCase() === "d"
        ) {

            moveChef("right");

        }


        if (
            key === "ArrowUp" ||
            key.toLowerCase() === "w"
        ) {

            setStatus(
                "⬆️ Você não pode atravessar o teto!"
            );

        }


        if (
            key === "ArrowDown" ||
            key.toLowerCase() === "s"
        ) {

            setStatus(
                "⬇️ Você está na área da cozinha."
            );

        }

    }
);


/* =========================================================
   INICIAR
========================================================= */

function startGame() {

    if (gameStarted) return;


    gameStarted = true;

    gameOverState = false;


    startScreen.style.display =
        "none";


    /*
       A música começa aqui porque
       o Enter é uma interação do usuário.
    */

    startItalianMusic();


    /*
       Primeiro pedido
    */

    createOrder();


    /*
       Fala inicial
    */

    speakSequence([

        "Bem-vindo ao Cozinheiro Maluco!",

        "Você tem três minutos.",

        "Pão é 1. Carne é 2. Queijo é 3.",

        "Tomate é 4. Alface é 5. Molho é 6. Cebola é 7.",

        "Memorizou bem?",

        "Se quiser repetir, pressione Backspace."

    ]);


    startTimer();

}


/* =========================================================
   GAME OVER
========================================================= */

function loseGame() {

    clearInterval(timerInterval);

    gameOverState = true;

    gameStarted = false;

    stopItalianMusic();


    gameOverText.innerHTML =
        `
        O tempo acabou.<br><br>

        Pontuação final:
        <strong>${score}</strong> pontos.
        `;


    gameOver.style.display =
        "flex";


    speakSequence([

        "Falência!",

        "O tempo acabou.",

        `Sua pontuação final foi ${score} pontos.`,

        "Pressione Enter para recomeçar."

    ]);

}


/* =========================================================
   RECOMEÇAR
========================================================= */

function restartGame() {

    gameOver.style.display =
        "none";


    score = 0;

    day = 1;

    timeLeft =
        GAME_TIME_START;

    orderIndex = 0;

    currentOrder = null;

    selectedIngredients = [];

    preparing = false;

    ratMode = false;

    gameOverState = false;

    gameStarted = false;


    inventory = {

        pao: 8,
        carne: 8,
        queijo: 8,
        tomate: 8,
        alface: 8,
        molho: 8,
        cebola: 8

    };


    scoreElement.textContent =
        "0";

    dayElement.textContent =
        "1";

    updateTimer();


    startScreen.style.display =
        "flex";


    speak(
        "Jogo reiniciado. Pressione Enter para começar."
    );

}


/* =========================================================
   MÚSICA ITALIANA ORIGINAL
========================================================= */

let audioContext = null;

let musicTimer = null;

let musicPlaying = false;


/*
   Escala com clima de música italiana.
*/

const melody = [

    659.25,
    783.99,
    880.00,
    783.99,

    659.25,
    587.33,
    523.25,
    587.33,

    659.25,
    783.99,
    987.77,
    880.00,

    783.99,
    659.25,
    587.33,
    523.25

];


function playNote(
    frequency,
    duration,
    startTime,
    volume = .035
) {

    if (!audioContext) return;


    const osc =
        audioContext.createOscillator();

    const gain =
        audioContext.createGain();


    /*
       Triângulo dá uma sensação
       mais leve, parecida com
       instrumento acústico.
    */

    osc.type = "triangle";

    osc.frequency.value =
        frequency;


    gain.gain.setValueAtTime(
        0,
        startTime
    );

    gain.gain.linearRampToValueAtTime(
        volume,
        startTime + .025
    );

    gain.gain.exponentialRampToValueAtTime(
        .001,
        startTime + duration
    );


    osc.connect(gain);

    gain.connect(
        audioContext.destination
    );


    osc.start(startTime);

    osc.stop(
        startTime + duration
    );

}


/* baixo */

function playBass(
    frequency,
    startTime
) {

    if (!audioContext) return;


    const osc =
        audioContext.createOscillator();

    const gain =
        audioContext.createGain();


    osc.type = "sine";

    osc.frequency.value =
        frequency;


    gain.gain.setValueAtTime(
        .0001,
        startTime
    );

    gain.gain.exponentialRampToValueAtTime(
        .025,
        startTime + .03
    );

    gain.gain.exponentialRampToValueAtTime(
        .0001,
        startTime + .35
    );


    osc.connect(gain);

    gain.connect(
        audioContext.destination
    );


    osc.start(startTime);

    osc.stop(
        startTime + .4
    );

}


/* =========================================================
   LOOP MUSICAL
========================================================= */

function scheduleMusic() {

    if (!musicPlaying ||
        !audioContext) {
        return;
    }


    const start =
        audioContext.currentTime + .05;


    const beat = .28;


    melody.forEach(
        (frequency, index) => {

            playNote(
                frequency,
                .22,
                start + index * beat
            );

        }
    );


    /*
       baixo italiano simples
    */

    const bassNotes = [

        130.81,
        164.81,
        146.83,
        174.61

    ];


    bassNotes.forEach(
        (frequency, index) => {

            playBass(
                frequency,
                start + index * beat * 4
            );

        }
    );


    const loopDuration =
        melody.length * beat;


    musicTimer =
        setTimeout(
            scheduleMusic,
            loopDuration * 1000
        );

}


/* =========================================================
   COMEÇAR MÚSICA
========================================================= */

function startItalianMusic() {

    try {

        if (!audioContext) {

            audioContext =
                new (
                    window.AudioContext ||
                    window.webkitAudioContext
                )();

        }


        if (
            audioContext.state ===
            "suspended"
        ) {

            audioContext.resume();

        }


        musicPlaying = true;

        clearTimeout(musicTimer);

        scheduleMusic();

    } catch (error) {

        console.log(
            "Áudio não disponível:",
            error
        );

    }

}


/* =========================================================
   PARAR MÚSICA
========================================================= */

function stopItalianMusic() {

    musicPlaying = false;

    clearTimeout(musicTimer);

}


/* =========================================================
   INICIALIZAÇÃO
========================================================= */

updateTimer();


setStatus(
    "Passe o mouse sobre COMEÇAR — ENTER para ouvir."
);


/*
   Também permite clicar no botão,
   mas o jogo continua totalmente
   jogável pelo teclado.
*/

startButton.addEventListener(
    "click",
    () => {

        startGame();

    }
);


restartButton.addEventListener(
    "click",
    () => {

        restartGame();

    }
);


/*
   Quando o mouse passa por cima dos
   ingredientes, fala o nome.
*/

document
    .querySelectorAll(".ingredient")
    .forEach(element => {

        element.addEventListener(
            "mouseenter",
            () => {

                const key =
                    element.dataset.key;

                const ingredient =
                    ingredients[key];

                if (ingredient) {

                    speak(
                        `${ingredient.name}. Tecla ${key}.`,
                        { rate: 1.7 }
                    );

                }

            }
        );

    });


</script>

</body>
</html>
