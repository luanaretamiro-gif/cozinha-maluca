<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>🍳 Cozinheiro Maluco</title>

<style>

* {
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

body {
    margin: 0;
    background: #0d1422;
    color: white;
    font-family: "Courier New", monospace;
    overflow-x: hidden;
    overflow-y: auto;
    image-rendering: pixelated;
}

button {
    font-family: inherit;
}

kbd {
    background: #eee;
    color: #111;
    border: 2px solid #888;
    padding: 3px 7px;
    font-weight: bold;
}

#game {
    width: min(1200px, 100%);
    min-height: 100vh;
    margin: auto;
    background: #101827;
}


/* =========================================================
   TOPO
========================================================= */

#topbar {
    position: sticky;
    top: 0;
    z-index: 100;

    min-height: 76px;

    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 10px 25px;

    background: #101827;

    border-bottom: 4px solid #334563;
}

.logo {
    color: #ffd83d;
    font-size: clamp(21px, 3vw, 35px);
    font-weight: bold;

    text-shadow:
        4px 4px #684610;
}

.stats {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

.stat {
    padding: 9px 13px;

    background: #18243a;

    border: 2px solid #3a4e70;

    font-weight: bold;
}

#timer {
    color: #ffffff;
}

#timer.danger {
    color: #ff4e4e;
    animation: blink .5s infinite alternate;
}

@keyframes blink {
    from {
        opacity: 1;
    }

    to {
        opacity: .45;
    }
}


/* =========================================================
   CENA
========================================================= */

#scene {
    position: relative;

    height: 620px;

    overflow: hidden;

    background:
        linear-gradient(
            to bottom,
            #48b6d9 0%,
            #48b6d9 62%,
            #70c65e 62%,
            #70c65e 65%,
            #86532f 65%,
            #86532f 100%
        );
}

#scene::before {
    content: "";

    position: absolute;

    inset: 0;

    background:
        repeating-linear-gradient(
            0deg,
            transparent 0 40px,
            rgba(255,255,255,.12) 41px 44px
        ),

        repeating-linear-gradient(
            90deg,
            transparent 0 70px,
            rgba(0,0,0,.12) 71px 75px
        );

    pointer-events: none;
}


/* =========================================================
   NUVENS
========================================================= */

.cloud {
    position: absolute;

    width: 85px;
    height: 23px;

    background: #eafaff;

    opacity: .85;
}

.cloud::before,
.cloud::after {
    content: "";

    position: absolute;

    background: #eafaff;
}

.cloud::before {
    width: 40px;
    height: 38px;

    left: 15px;
    top: -17px;
}

.cloud::after {
    width: 32px;
    height: 32px;

    right: 10px;
    top: -12px;
}

.cloud1 {
    top: 55px;
    left: 9%;
}

.cloud2 {
    top: 120px;
    right: 14%;
    transform: scale(.7);
}


/* =========================================================
   CHÃO
========================================================= */

.floor {
    position: absolute;

    left: 0;
    right: 0;
    bottom: 0;

    height: 35%;

    background:
        repeating-linear-gradient(
            90deg,
            #744526 0 54px,
            #57351f 54px 59px
        );

    border-top: 8px solid #b86d39;
}


/* =========================================================
   ESTAÇÕES
========================================================= */

.station {
    position: absolute;

    bottom: 36%;

    width: 190px;
    height: 110px;

    background: #272727;

    border: 10px solid #3c3c3c;

    box-shadow:
        8px 8px rgba(0,0,0,.25);

    z-index: 3;
}

.station span {
    position: absolute;

    left: 50%;

    transform: translateX(-50%);

    bottom: -39px;

    white-space: nowrap;

    color: #ffd83d;

    font-size: 18px;

    font-weight: bold;
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

    margin: auto;
    margin-top: 12px;

    background: #171717;

    border: 6px solid #101010;
}

.grillTop {
    width: 130px;
    height: 18px;

    margin: 30px auto;

    background:
        repeating-linear-gradient(
            90deg,
            #111 0 12px,
            #777 12px 16px
        );
}


/* =========================================================
   CHEF
========================================================= */

#chef {
    position: absolute;

    left: 50%;

    bottom: 34%;

    width: 76px;
    height: 125px;

    transform: translateX(-50%);

    z-index: 20;

    transition: left .08s linear;
}

.head {
    position: absolute;

    left: 10px;
    top: 20px;

    width: 56px;
    height: 55px;

    background: #d99769;
}

.hat {
    position: absolute;

    left: 2px;
    top: 4px;

    width: 72px;
    height: 22px;

    background: white;

    z-index: 3;
}

.hat::before {
    content: "";

    position: absolute;

    left: 12px;
    top: -18px;

    width: 48px;
    height: 25px;

    background: white;
}

.eye {
    position: absolute;

    width: 7px;
    height: 7px;

    top: 22px;

    background: #111;
}

.eye.left {
    left: 12px;
}

.eye.right {
    right: 12px;
}

.mouth {
    position: absolute;

    left: 18px;
    bottom: 12px;

    width: 20px;
    height: 5px;

    background: #111;
}

.body {
    position: absolute;

    bottom: 0;

    width: 76px;
    height: 65px;

    background: #f4f4f4;
}

.arm {
    position: absolute;

    top: 68px;

    width: 17px;
    height: 48px;

    background: #d99769;

    z-index: -1;
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
   MENSAGEM
========================================================= */

#messageBoard {
    position: absolute;

    left: 5%;
    right: 5%;

    bottom: 13%;

    min-height: 70px;

    display: flex;

    align-items: center;
    justify-content: center;

    padding: 12px 20px;

    background:
        linear-gradient(
            #58341f,
            #472a1b
        );

    border: 4px solid #a76334;

    box-shadow:
        inset 0 0 0 3px #321c12;

    color: #fff;

    text-align: center;

    font-size: 18px;

    font-weight: bold;

    z-index: 30;
}


/* =========================================================
   INGREDIENTES DECORATIVOS
========================================================= */

.food {
    position: absolute;

    width: 35px;
    height: 35px;

    bottom: 37%;

    z-index: 5;
}

.bread {
    background: #e5a044;
    border-radius: 8px;
}

.tomato {
    background: #e94b4b;
    border-radius: 50%;
}

.lettuce {
    background: #51bd5b;
    border-radius: 8px;
}


/* =========================================================
   PAINÉIS
========================================================= */

#bottom {
    padding: 15px;

    display: grid;

    grid-template-columns:
        1fr 1.4fr;

    gap: 15px;

    background: #111a2b;
}

.panel {
    min-height: 230px;

    padding: 16px;

    background: #172238;

    border: 3px solid #344a6b;
}

.panel-title {
    margin-bottom: 15px;

    color: #ffd83d;

    font-size: 22px;

    font-weight: bold;
}

#orderText {
    font-size: 17px;
    line-height: 1.6;
}


/* =========================================================
   INGREDIENTES
========================================================= */

#ingredientsList {
    display: grid;

    grid-template-columns:
        repeat(4, 1fr);

    gap: 8px;
}

.ingredient {
    position: relative;

    min-height: 76px;

    padding: 7px;

    background: #1c2a42;

    border: 2px solid #415777;

    text-align: center;

    font-weight: bold;

    cursor: pointer;

    transition: .15s;
}

.ingredient:hover {
    transform: translateY(-2px);
    border-color: #ffd83d;
}

.ingredient.selected {
    background: #315c47;

    border-color: #72e092;

    box-shadow:
        0 0 8px rgba(114,224,146,.4);
}

.ingredient.locked {
    background: #10151f;

    border-color: #303746;

    color: #777;

    cursor: not-allowed;

    opacity: .65;
}

.key {
    color: #ffd83d;

    font-size: 20px;
}

.stock {
    display: block;

    margin-top: 5px;

    color: #72e092;

    font-size: 12px;
}

.lockText {
    display: block;

    margin-top: 5px;

    color: #ff7777;

    font-size: 11px;
}


/* =========================================================
   TELA INICIAL
========================================================= */

.overlay {
    position: fixed;

    inset: 0;

    z-index: 500;

    display: flex;

    align-items: center;
    justify-content: center;

    padding: 20px;

    background:
        rgba(5,10,18,.92);
}

.menuBox {
    width: min(760px, 95vw);

    max-height: 92vh;

    overflow-y: auto;

    padding: 30px;

    background: #172238;

    border: 5px solid #536a90;

    box-shadow:
        10px 10px #080c13;

    text-align: center;
}

.menuTitle {
    color: #ffd83d;

    font-size:
        clamp(30px, 6vw, 55px);

    font-weight: bold;

    text-shadow:
        4px 4px #70470f;

    margin-bottom: 20px;
}

.startButton {
    padding: 17px 30px;

    background: #d75b38;

    border: 4px solid #ffb34d;

    color: white;

    font-size: 23px;

    font-weight: bold;

    cursor: pointer;

    box-shadow:
        0 7px #7c3020;
}

.startButton:hover,
.startButton:focus {
    background: #f16d44;

    transform:
        translateY(-2px);
}

.controls {
    margin-top: 25px;

    display: grid;

    grid-template-columns:
        repeat(2, 1fr);

    gap: 8px;

    text-align: left;
}

.control {
    padding: 9px;

    background: #101827;

    border: 2px solid #334663;
}



/* =========================================================
   CHUVA
========================================================= */

#rainMode {
    display: none;

    position: fixed;

    inset: 0;

    z-index: 300;

    background:
        linear-gradient(
            #48b6d8,
            #56bedc 70%,
            #80502e 70%
        );

    overflow: hidden;
}

#rainInfo {
    position: absolute;

    top: 20px;

    left: 50%;

    transform:
        translateX(-50%);

    width: min(700px, 90%);

    padding: 15px;

    background:
        rgba(8,14,24,.92);

    border: 4px solid #ffd83d;

    color: white;

    text-align: center;

    font-size: 20px;

    font-weight: bold;

    z-index: 10;
}

#rainGround {
    position: absolute;

    left: 0;
    right: 0;
    bottom: 0;

    height: 30%;

    background:
        repeating-linear-gradient(
            90deg,
            #704324 0 55px,
            #54321e 55px 60px
        );

    border-top:
        8px solid #b86b38;
}

#rainChef {
    position: absolute;

    bottom: 30%;

    left: 50%;

    width: 70px;
    height: 110px;

    transform:
        translateX(-50%);

    z-index: 15;

    transition:
        left .08s linear;
}

.rainChefHead {
    position: absolute;

    top: 15px;
    left: 10px;

    width: 50px;
    height: 50px;

    background: #d99769;
}

.rainChefHat {
    position: absolute;

    top: 0;
    left: 0;

    width: 70px;
    height: 20px;

    background: white;
}

.rainChefBody {
    position: absolute;

    bottom: 0;

    width: 70px;
    height: 60px;

    background: white;
}

#fallingIngredient {
    position: absolute;

    width: 46px;
    height: 46px;

    left: 50%;
    top: 105px;

    transform:
        translateX(-50%);

    z-index: 20;

    display: none;
}


/* =========================================================
   TIPOS DE INGREDIENTES
========================================================= */

.pixel-pao {
    background: #e6a044;
    border-radius: 8px;
}

.pixel-carne {
    background: #8d422d;
}

.pixel-queijo {
    background: #ffd83d;
}

.pixel-tomate {
    background: #ed4c4c;
    border-radius: 50%;
}

.pixel-alface {
    background: #51c45d;
    border-radius: 12px;
}

.pixel-molho {
    background: #a83232;
    border-radius: 8px;
}

.pixel-cebola {
    background: #d28ae0;
    border-radius: 50%;
}

.pixel-cheddar {
    background: #f2a33b;
    border-radius: 8px;
}

.pixel-frango {
    background: #f0c38a;
    border-radius: 8px;
}

.pixel-catupiry {
    background: #fff1d0;
    border-radius: 8px;
}

.pixel-ketchup {
    background: #e22d2d;
    border-radius: 8px;
}

.pixel-mostarda {
    background: #e3c52f;
    border-radius: 8px;
}

.pixel-verde {
    background: #35a85b;
    border-radius: 8px;
}

.pixel-bacon {
    background:
        repeating-linear-gradient(
            0deg,
            #d65a45 0 7px,
            #ffd0a0 7px 11px
        );
}

.pixel-ovo {
    background: #fff8dc;

    border-radius:
        50% 45% 50% 45%;
}

.pixel-ovo::after {
    content: "";

    position: absolute;

    width: 18px;
    height: 18px;

    background: #ffca28;

    border-radius: 50%;

    left: 14px;
    top: 14px;
}


/* =========================================================
   VITÓRIA / GAME OVER
========================================================= */

#gameOver {
    display: none;
}

.victoryTitle {
    color: #ffd83d;

    font-size:
        clamp(32px, 6vw, 58px);

    font-weight: bold;

    text-shadow:
        4px 4px #70470f;
}

.victory {
    border-color: #ffd83d;
}


/* =========================================================
   RESPONSIVO
========================================================= */

@media(max-width: 800px) {

    #topbar {
        flex-direction: column;
        gap: 8px;
    }

    #scene {
        height: 500px;
    }

    .station {
        transform:
            scale(.72);

        transform-origin:
            bottom center;
    }

    .grill {
        transform:
            translateX(-50%)
            scale(.72);
    }

    #bottom {
        grid-template-columns:
            1fr;
    }

    #ingredientsList {
        grid-template-columns:
            repeat(3, 1fr);
    }

    .controls {
        grid-template-columns:
            1fr;
    }
}

</style>
</head>

<body>

<div id="game">

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


<section id="scene">

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

    <div class="food bread" style="left:25%;"></div>
    <div class="food tomato" style="left:73%;"></div>
    <div class="food lettuce" style="left:82%;"></div>

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

    <div id="messageBoard">
        Aguardando...
    </div>

</section>


<section id="bottom">

    <div class="panel">

        <div class="panel-title">
            📋 PEDIDO
        </div>

        <div id="orderText">
            Nenhum pedido ainda.
        </div>

    </div>


    <div class="panel">

        <div class="panel-title">
            🧺 INGREDIENTES
        </div>

        <div id="ingredientsList">

            <div class="ingredient" data-key="1"><span class="key">1</span>Pão<span class="stock" id="stock-pao">10 unidades</span></div>
            <div class="ingredient" data-key="2"><span class="key">2</span>Carne<span class="stock" id="stock-carne">10 unidades</span></div>
            <div class="ingredient" data-key="3"><span class="key">3</span>Queijo<span class="stock" id="stock-queijo">10 unidades</span></div>
            <div class="ingredient" data-key="4"><span class="key">4</span>Tomate<span class="stock" id="stock-tomate">10 unidades</span></div>
            <div class="ingredient" data-key="5"><span class="key">5</span>Alface<span class="stock" id="stock-alface">10 unidades</span></div>
            <div class="ingredient" data-key="6"><span class="key">6</span>Molho<span class="stock" id="stock-molho">10 unidades</span></div>
            <div class="ingredient" data-key="7"><span class="key">7</span>Cebola<span class="stock" id="stock-cebola">10 unidades</span></div>
            <div class="ingredient locked" data-key="8"><span class="key">8</span>Cheddar<span class="stock" id="stock-cheddar">BLOQUEADO</span></div>
            <div class="ingredient locked" data-key="9"><span class="key">9</span>Frango<span class="stock" id="stock-frango">BLOQUEADO</span></div>
            <div class="ingredient locked" data-key="0"><span class="key">0</span>Catupiry<span class="stock" id="stock-catupiry">BLOQUEADO</span></div>
            <div class="ingredient locked" data-key="-"><span class="key">−</span>Bacon<span class="stock" id="stock-bacon">BLOQUEADO</span></div>
            <div class="ingredient locked" data-key="+"><span class="key">+</span>Molho verde<span class="stock" id="stock-verde">BLOQUEADO</span></div>

        </div>

        <br>

        <strong>
            E = ouvir pedido |
            1–9, 0, −, + = ingredientes |
            Backspace = remover |
            Enter = preparar/entregar
        </strong>

    </div>

</section>


<!-- =====================================================
     TELA INICIAL
===================================================== -->

<div id="startScreen" class="overlay">

    <div class="menuBox">

        <div class="menuTitle">
            🍳 COZINHEIRO MALUCO
        </div>

        <p>
            Prepare os pedidos,
            sobreviva ao caos
            e torne-se o melhor chefe de Ubiratã!
        </p>

        <div style="
            background:#101827;
            border:3px solid #ffd83d;
            padding:15px;
            margin:20px 0;
            line-height:1.8;
        ">

            <strong style="color:#ffd83d;">
                🧺 ESTOQUE INICIAL
            </strong>

            <br>

            Você começa com
            <strong>10 unidades de CADA ingrediente.</strong>

            <br>

            Quando qualquer ingrediente chegar a
            <strong>0</strong>,
            começa a chuva de ingredientes!

            <br>

            A chuva adicionará
            <strong>+10 de TODOS os ingredientes.</strong>

        </div>

        <div style="
            background:#101827;
            border:2px solid #334663;
            padding:12px;
            margin-bottom:20px;
        ">

            <strong style="color:#ffd83d;">
                🔓 DESBLOQUEIOS
            </strong>

            <br><br>

            ⭐ 1800 — Cheddar

            <br>

            ⭐ 2300 — Frango

            <br>

            ⭐ 2800 — Catupiry

            <br>

            ⭐ 3450 — Bacon

            <br>

            ⭐ 4000 — Molho verde

            <br><br>

            🏆 <strong>4000 pontos = MELHOR CHEFE DE UBIRATÃ!</strong>

        </div>

        <button
            id="startButton"
            class="startButton">

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
                <kbd>1–9 / 0</kbd>
                Ingredientes
            </div>

            <div class="control">
                <kbd>− / +</kbd>
                Bacon / Molho verde
            </div>

            <div class="control">
                <kbd>BACKSPACE</kbd>
                Remover ingrediente
            </div>


            <div class="control">
                <kbd>A / ←</kbd>
                Esquerda
            </div>

            <div class="control">
                <kbd>D / →</kbd>
                Direita
            </div>

        </div>

        <p style="color:#ffd83d">
            Passe o mouse sobre
            COMEÇAR — ENTER para ouvir.
        </p>

    </div>

</div>


<!-- =====================================================
     CHUVA
===================================================== -->

<div id="rainMode">

    <div id="rainInfo">
        🌧️ PREPARE-SE PARA A CHUVA DE INGREDIENTES
    </div>

    <div id="rainGround"></div>

    <div id="rainChef">

        <div class="rainChefHat"></div>

        <div class="rainChefHead"></div>

        <div class="rainChefBody"></div>

    </div>

    <div id="fallingIngredient"></div>

</div>


<!-- =====================================================
     GAME OVER / VITÓRIA
===================================================== -->

<div id="gameOver" class="overlay">

    <div class="menuBox">

        <div id="gameOverTitle"
             class="victoryTitle">

            🏆 FIM DE JOGO!

        </div>

        <p id="gameOverText">
            O tempo acabou.
        </p>

        <button
            id="restartButton"
            class="startButton">

            RECOMEÇAR — ENTER

        </button>

    </div>

</div>


</div>


<script>

/* =========================================================
   CONFIGURAÇÕES
========================================================= */

const START_TIME = 180;

const ORDER_POINTS = 150;

const BONUS_TIME = 15;

const INITIAL_STOCK = 10;

const RAIN_REWARD = 10;

const WIN_SCORE = 5000;


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

const gameOverTitle =
    document.getElementById("gameOverTitle");

const gameOverText =
    document.getElementById("gameOverText");

const scoreElement =
    document.getElementById("score");

const timerElement =
    document.getElementById("timer");

const dayElement =
    document.getElementById("day");

const orderText =
    document.getElementById("orderText");

const messageBoard =
    document.getElementById("messageBoard");

const chef =
    document.getElementById("chef");

const rainMode =
    document.getElementById("rainMode");

const rainInfo =
    document.getElementById("rainInfo");

const rainChef =
    document.getElementById("rainChef");

const fallingIngredient =
    document.getElementById(
        "fallingIngredient"
    );


/* =========================================================
   ESTADO
========================================================= */

let gameStarted = false;

let gameOverState = false;

let victoryState = false;

let rainActive = false;

let score = 0;

let day = 1;

let timeLeft = START_TIME;

let timerInterval = null;

let chefX = 50;

let rainChefX = 50;

let currentOrder = null;

let selectedIngredients = [];

let preparing = false;

let orderIndex = 0;

let normalClientsSinceSpecial = 0;

let specialClientIndex = 0;

// Ingredientes recém-desbloqueados que precisam aparecer em um pedido logo em seguida.
let pendingUnlockedIngredients = [];

// Registra quais ingredientes já foram desbloqueados de verdade.
// Isso evita que um ingrediente seja "desbloqueado" novamente toda vez
// que o estoque dele chegar a zero.
let unlockedIngredientKeys = new Set([
    "1", "2", "3", "4", "5", "6", "7"
]);


/* =========================================================
   ESTOQUE
========================================================= */

const makeInitialInventory = () => ({

    pao: 10,
    carne: 10,
    queijo: 10,
    tomate: 10,
    alface: 10,
    molho: 10,
    cebola: 10,
    cheddar: 0,
    frango: 0,
    catupiry: 0,
    bacon: 0,
    verde: 0

});


let inventory =
    makeInitialInventory();


/* =========================================================
   INGREDIENTES
========================================================= */

const ingredients = {

    "1": { id: "pao", name: "Pão", css: "pixel-pao", unlock: 0 },
    "2": { id: "carne", name: "Carne", css: "pixel-carne", unlock: 0 },
    "3": { id: "queijo", name: "Queijo", css: "pixel-queijo", unlock: 0 },
    "4": { id: "tomate", name: "Tomate", css: "pixel-tomate", unlock: 0 },
    "5": { id: "alface", name: "Alface", css: "pixel-alface", unlock: 0 },
    "6": { id: "molho", name: "Molho", css: "pixel-molho", unlock: 0 },
    "7": { id: "cebola", name: "Cebola", css: "pixel-cebola", unlock: 0 },
    "8": { id: "cheddar", name: "Cheddar", css: "pixel-cheddar", unlock: 1800 },
    "9": { id: "frango", name: "Frango", css: "pixel-frango", unlock: 2300 },
    "0": { id: "catupiry", name: "Catupiry", css: "pixel-catupiry", unlock: 2800 },
    "-": { id: "bacon", name: "Bacon", css: "pixel-bacon", unlock: 3450 },
    "+": { id: "verde", name: "Molho verde", css: "pixel-verde", unlock: 4000 }

};


/* =========================================================
   CLIENTES NORMAIS
========================================================= */

const normalOrders = [

    {
        cliente: "Maria",
        prato: "Hambúrguer clássico",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1
        }
    },

    {
        cliente: "João",
        prato: "Hambúrguer completo",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            alface: 1,
            molho: 1
        }
    },

    {
        cliente: "Ana",
        prato: "X-salada",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            alface: 1,
            tomate: 1,
            molho: 1
        }
    },

    {
        cliente: "Pedro",
        prato: "X-bacon simples",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            bacon: 1
        }
    },

    {
        cliente: "Carlos",
        prato: "Duplo queijo",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1
        }
    },

    {
        cliente: "Juliana",
        prato: "Salada reforçada",
        ingredients: {
            pao: 1,
            carne: 1,
            alface: 1,
            tomate: 1,
            cebola: 1
        }
    },

    {
        cliente: "Lucas",
        prato: "Hambúrguer triplo",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            molho: 1
        }
    },

    {
        cliente: "Beatriz",
        prato: "X-tudo",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1,
            alface: 1,
            cebola: 1,
            molho: 1
        }
    },

    {
        cliente: "Rafael",
        prato: "Duplo tomate",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1,
            cebola: 1
        }
    },

    {
        cliente: "Camila",
        prato: "Mega alface",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            alface: 1,
            tomate: 1
        }
    },

    {
        cliente: "Bruno",
        prato: "Hambúrguer ceboleiro",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            cebola: 1,
            molho: 1
        }
    },

    {
        cliente: "Fernanda",
        prato: "Monstro de 5 carnes",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1,
            alface: 1
        }
    },

    {
        cliente: "Gustavo",
        prato: "Hambúrguer quíntuplo",
        ingredients: {
            pao: 1,
            carne: 1
        }
    },

    {
        cliente: "Paula",
        prato: "Torre de queijo",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            tomate: 1,
            alface: 1
        }
    },

    {
        cliente: "Roberto",
        prato: "Saladão gigante",
        ingredients: {
            pao: 1,
            carne: 1,
            alface: 1,
            tomate: 1,
            cebola: 1
        }
    },

    {
        cliente: "Bianca",
        prato: "X-cheddar",
        ingredients: {
            pao: 1,
            carne: 1,
            cheddar: 1,
            tomate: 1
        }
    },

    {
        cliente: "Diego",
        prato: "X-frango",
        ingredients: {
            pao: 1,
            frango: 1,
            queijo: 1,
            alface: 1
        }
    },

    {
        cliente: "Marina",
        prato: "X-catupiry",
        ingredients: {
            pao: 1,
            carne: 1,
            catupiry: 1,
            tomate: 1
        }
    },

    {
        cliente: "Thiago",
        prato: "X-bacon",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            bacon: 1
        }
    },

    {
        cliente: "Larissa",
        prato: "X-molho verde",
        ingredients: {
            pao: 1,
            carne: 1,
            queijo: 1,
            verde: 1
        }
    }

];


/* =========================================================
   CLIENTES ESPECIAIS
========================================================= */

const specialOrders = [

    {
        cliente: "Neymar",
        prato: "Hambúrguer driblador",
        ingredients: {
            pao: 1,
            carne: 3,
            queijo: 3,
            alface: 2,
            tomate: 3,
            molho: 2
        }
    },

    {
        cliente: "Lula",
        prato: "X-Lula especial",
        ingredients: {
            pao: 1,
            carne: 4,
            queijo: 4,
            tomate: 2,
            cebola: 2
        }
    },

    {
        cliente: "Felipe Neto",
        prato: "Hambúrguer exagerado do Felipe",
        ingredients: {
            pao: 1,
            carne: 3,
            queijo: 3,
            tomate: 2,
            alface: 2,
            molho: 2
        }
    },

    {
        cliente: "Zeca Pagodinho",
        prato: "X-samba",
        ingredients: {
            pao: 1,
            carne: 2,
            queijo: 2,
            tomate: 2,
            cebola: 2,
            molho: 2
        }
    },

    {
        cliente: "Ronaldinho Gaúcho",
        prato: "X-Gaúcho",
        ingredients: {
            pao: 1,
            carne: 4,
            queijo: 3,
            alface: 2,
            tomate: 2,
            cebola: 1
        }
    },

    {
        cliente: "Pai do Bebê",
        prato: "Hambúrguer do papai",
        ingredients: {
            pao: 1,
            carne: 2,
            queijo: 2,
            alface: 2,
            tomate: 2,
            cebola: 2
        }
    },

    {
        cliente: "Sosô Careca",
        prato: "X-careca especial",
        ingredients: {
            pao: 1,
            carne: 5,
            queijo: 4,
            tomate: 2,
            molho: 2
        }
    },

    {
        cliente: "Liz Macedo",
        prato: "Hambúrguer da Liz",
        ingredients: {
            pao: 1,
            carne: 2,
            queijo: 3,
            alface: 3,
            tomate: 2,
            cebola: 2
        }
    },

    {
        cliente: "Luluca",
        prato: "X-Luluca",
        ingredients: {
            pao: 1,
            carne: 3,
            queijo: 3,
            alface: 3,
            tomate: 3,
            molho: 2
        }
    },

    {
        cliente: "Rainha Elizabeth",
        prato: "Hambúrguer real",
        ingredients: {
            pao: 1,
            carne: 4,
            queijo: 4,
            tomate: 2,
            alface: 2,
            cebola: 2
        }
    },

    {
        cliente: "Anitta",
        prato: "X-Anitta",
        ingredients: {
            pao: 1,
            carne: 3,
            queijo: 3,
            tomate: 3,
            alface: 2,
            cebola: 2
        }
    },

    {
        cliente: "Malala",
        prato: "Hambúrguer especial",
        ingredients: {
            pao: 1,
            carne: 2,
            queijo: 2,
            alface: 4,
            tomate: 2,
            cebola: 2
        }
    },

    {
        cliente: "Virgínia Fonseca",
        prato: "X-Virgínia",
        ingredients: {
            pao: 1,
            carne: 4,
            queijo: 4,
            tomate: 3,
            alface: 3,
            molho: 2
        }
    },

    {
        cliente: "Zé Felipe",
        prato: "X-Felipe",
        ingredients: {
            pao: 1,
            carne: 5,
            queijo: 3,
            tomate: 2,
            cebola: 3,
            molho: 2
        }
    },

    {
        cliente: "Vini Jr",
        prato: "Hambúrguer velocidade máxima",
        ingredients: {
            pao: 1,
            carne: 4,
            queijo: 3,
            alface: 3,
            tomate: 3,
            cebola: 2
        }
    },

    {
        cliente: "Zago",
        prato: "Hambúrguer do Zago",
        ingredients: {
            pao: 1,
            carne: 5,
            queijo: 4,
            tomate: 2,
            alface: 2,
            cebola: 2
        }
    },

    { cliente: "Cristiano Ronaldo", prato: "CR7 Burger", ingredients: { pao: 1, carne: 5, cheddar: 4, tomate: 2, alface: 2 } },

    { cliente: "Bolsonaro", prato: "X-Brasil", ingredients: { pao: 1, carne: 5, queijo: 3, bacon: 2, cebola: 2 } },

    { cliente: "Scooby Doo", prato: "Scooby Burger", ingredients: { pao: 1, carne: 5, cheddar: 3, catupiry: 2, bacon: 2 } },

    { cliente: "Cristiano Ronaldo", prato: "CR7 Frango", ingredients: { pao: 1, frango: 4, cheddar: 2, alface: 2 } },

    { cliente: "Virgínia Fonseca", prato: "X-Catupiry da Virgínia", ingredients: { pao: 1, carne: 3, catupiry: 4, tomate: 2 } },

    { cliente: "Vini Jr", prato: "X-Verde do Vini", ingredients: { pao: 1, carne: 4, verde: 3, queijo: 2 } }

];


/* =========================================================
   VOZ
========================================================= */

const synth =
    window.speechSynthesis;

let voices = [];

function loadVoices() {

    voices =
        synth.getVoices();

}

loadVoices();

if (synth) {

    synth.onvoiceschanged =
        loadVoices;

}

function getPortugueseVoice() {

    return (
        voices.find(
            v =>
                v.lang &&
                v.lang
                    .toLowerCase()
                    .startsWith("pt-br")
        )
        ||
        voices.find(
            v =>
                v.lang &&
                v.lang
                    .toLowerCase()
                    .startsWith("pt")
        )
        ||
        null
    );

}


const clientVoiceProfiles = {
    "Virgínia Fonseca": { pitch: 1.18, rate: 1.48 },
    "Neymar": { pitch: 0.88, rate: 1.62 },
    "Vini Jr": { pitch: 0.96, rate: 1.70 },
    "Sosô Careca": { pitch: 0.78, rate: 1.40 },
    "Cristiano Ronaldo": { pitch: 0.92, rate: 1.50 },
    "Zeca Pagodinho": { pitch: 0.74, rate: 1.32 },
    "Bolsonaro": { pitch: 0.82, rate: 1.42 },
    "Lula": { pitch: 0.76, rate: 1.30 },
    "Liz Macedo": { pitch: 1.15, rate: 1.52 },
    "Scooby Doo": { pitch: 0.68, rate: 1.20 }
};

// Perfis genéricos de voz: o navegador usa síntese para os demais clientes.
function speakSpecialOrder(order, orderDescription) {
    if (!synth) return;
    const profile = clientVoiceProfiles[order.cliente] || { pitch: 1, rate: 1.55 };
    const voice = getPortugueseVoice();
    const utter = new SpeechSynthesisUtterance(`Oi! Eu sou ${order.cliente}. Quero ${order.prato}. Ingredientes: ${orderDescription}.`);
    if (voice) utter.voice = voice;
    utter.lang = voice ? voice.lang : "pt-BR";
    utter.rate = profile.rate;
    utter.pitch = profile.pitch;
    utter.volume = 1;
    synth.cancel();
    synth.speak(utter);
}

function speak(text) {

    if (!synth)
        return;

    synth.cancel();

    const utter =
        new SpeechSynthesisUtterance(
            text
        );

    const voice =
        getPortugueseVoice();

    if (voice)
        utter.voice = voice;

    utter.lang =
        voice
            ? voice.lang
            : "pt-BR";

    utter.rate = 1.55;

    utter.pitch = 1;

    utter.volume = 1;

    synth.speak(utter);

}


function speakSequence(list) {

    if (!synth)
        return;

    synth.cancel();

    let index = 0;

    function next() {

        if (
            index >= list.length
        )
            return;

        const utter =
            new SpeechSynthesisUtterance(
                list[index]
            );

        const voice =
            getPortugueseVoice();

        if (voice)
            utter.voice = voice;

        utter.lang =
            voice
                ? voice.lang
                : "pt-BR";

        utter.rate = 1.55;

        utter.pitch = 1;

        utter.onend = () => {

            index++;

            setTimeout(
                next,
                80
            );

        };

        synth.speak(utter);

    }

    next();

}


/* =========================================================
   MENSAGEM
========================================================= */

function message(text) {

    messageBoard.textContent =
        text;

}


/* =========================================================
   ESTOQUE / DESBLOQUEIOS
========================================================= */

function isUnlocked(key) {

    const item =
        ingredients[key];

    return score >= item.unlock;

}


function updateInventoryDisplay() {

    document
        .querySelectorAll(".ingredient")
        .forEach(button => {

            const key =
                button.dataset.key;

            const item =
                ingredients[key];

            const stockElement =
                button.querySelector(".stock");

            if (!isUnlocked(key)) {

                button.classList.add(
                    "locked"
                );

                stockElement.textContent =
                    `🔒 ${item.unlock} pontos`;

            } else {

                button.classList.remove(
                    "locked"
                );

                stockElement.textContent =
                    `${inventory[item.id]} unidades`;

                if (
                    inventory[item.id] <= 0
                ) {

                    stockElement.style.color =
                        "#ff5757";

                } else {

                    stockElement.style.color =
                        "#72e092";

                }

            }

        });

}


/* =========================================================
   DESBLOQUEIOS
========================================================= */

function checkUnlocks() {

    const newlyUnlocked = [];

    Object.entries(ingredients).forEach(([key, item]) => {

        if (
            item.unlock > 0 &&
            score >= item.unlock &&
            !unlockedIngredientKeys.has(key)
        ) {

            unlockedIngredientKeys.add(key);
            inventory[item.id] = INITIAL_STOCK;
            newlyUnlocked.push(item.name);

            if (!pendingUnlockedIngredients.includes(key)) {
                pendingUnlockedIngredients.push(key);
            }
        }

    });

    if (newlyUnlocked.length) {

        const names = newlyUnlocked.join(", ");

        message(
            `🔓 DESBLOQUEADO: ${names}! +10 unidades`
        );

        speak(
            `${names} desbloqueado. Você recebeu 10 unidades. O próximo cliente vai pedir esse ingrediente.`
        );
    }

    updateInventoryDisplay();
}



/* =========================================================
   TIMER
========================================================= */

function updateTimer() {

    const minutes =
        Math.floor(
            timeLeft / 60
        );

    const seconds =
        timeLeft % 60;

    timerElement.textContent =
        `${String(minutes).padStart(2,"0")}:${String(seconds).padStart(2,"0")}`;


    if (
        timeLeft <= 20
    ) {

        timerElement.classList
            .add("danger");

    } else {

        timerElement.classList
            .remove("danger");

    }

}


function startTimer() {

    clearInterval(
        timerInterval
    );

    timerInterval =
        setInterval(() => {

            if (
                !gameStarted ||
                gameOverState ||
                rainActive
            )
                return;

            timeLeft--;

            updateTimer();

            if (
                timeLeft <= 0
            ) {

                timeLeft = 0;

                updateTimer();

                loseGame();

            }

        }, 1000);

}


/* =========================================================
   FORMATAR PEDIDO
========================================================= */

function orderToText(order) {

    const multiplierNames = {
        2: "dupla",
        3: "tripla",
        4: "quádrupla",
        5: "quíntupla"
    };

    return Object.entries(order.ingredients)
        .map(([id, amount]) => {
            const item = Object.values(ingredients).find(i => i.id === id);
            if (item.id === "pao" || amount <= 1) return item.name;
            return `${item.name} ${multiplierNames[amount] || `${amount}x`}`;
        })
        .join(" + ");

}


/* =========================================================
   PEDIDO ESPECIAL
========================================================= */

function shouldUseSpecialClient() {

    return (
        normalClientsSinceSpecial >= 4 ||
        (specialClientIndex > 0 && normalClientsSinceSpecial >= 1)
    );

}


function orderUsesUnlockedIngredients(order) {
    return Object.keys(order.ingredients).every(id => {
        const item = Object.values(ingredients).find(i => i.id === id);
        return item && score >= item.unlock;
    });
}

function getNextOrder() {

    const wantsSpecial = shouldUseSpecialClient();

    /*
       REGRA DE DESBLOQUEIO:
       Assim que um ingrediente novo é desbloqueado, o PRÓXIMO cliente
       obrigatoriamente recebe um pedido que usa esse ingrediente.
       Se for a vez de um especial, usamos um especial compatível;
       caso contrário, criamos um pedido normal simples.
    */
    if (pendingUnlockedIngredients.length) {

        const pendingId = pendingUnlockedIngredients[0];

        if (wantsSpecial) {
            const matchingSpecial = specialOrders.find(order =>
                order.ingredients[pendingId] > 0 &&
                orderUsesUnlockedIngredients(order)
            );

            if (matchingSpecial) {
                pendingUnlockedIngredients.shift();
                specialClientIndex++;
                normalClientsSinceSpecial = 0;

                return {
                    ...matchingSpecial,
                    special: true
                };
            }
        }

        // Cliente normal: somente 1 unidade do ingrediente novo.
        const item = ingredients[pendingId];
        const normalUnlockOrder = {
            cliente: `Cliente ${item.name}`,
            prato: `Hambúrguer com ${item.name}`,
            ingredients: {
                pao: 1,
                carne: 1,
                [pendingId === "8" ? "cheddar" :
                 pendingId === "9" ? "frango" :
                 pendingId === "0" ? "catupiry" :
                 pendingId === "-" ? "bacon" : "verde"]: 1
            }
        };

        pendingUnlockedIngredients.shift();
        orderIndex++;
        normalClientsSinceSpecial++;

        return {
            ...normalUnlockOrder,
            special: false
        };
    }

    if (wantsSpecial) {

        const availableSpecials =
            specialOrders.filter(orderUsesUnlockedIngredients);

        if (availableSpecials.length) {
            const order = availableSpecials[
                specialClientIndex % availableSpecials.length
            ];

            specialClientIndex++;
            normalClientsSinceSpecial = 0;

            return {
                ...order,
                special: true
            };
        }
    }

    const availableNormals =
        normalOrders.filter(orderUsesUnlockedIngredients);

    const order =
        availableNormals[orderIndex % availableNormals.length];

    orderIndex++;
    normalClientsSinceSpecial++;

    return {
        ...order,
        special: false
    };
}



/* =========================================================
   NOVO PEDIDO
========================================================= */

function createOrder() {

    if (rainActive)
        return;


    currentOrder =
        getNextOrder();


    selectedIngredients = [];

    preparing = false;


    updateIngredientVisual();


    const specialText =
        currentOrder.special
            ? " ⭐ CLIENTE ESPECIAL!"
            : "";


    orderText.innerHTML = `

        <strong>
            🔔 NOVO PEDIDO!${specialText}
        </strong>

        <br><br>

        Cliente:
        <strong>
            ${currentOrder.cliente}
        </strong>

        <br>

        ${currentOrder.prato}

        <br><br>

        Pressione
        <strong>E</strong>
        para ouvir.

    `;


    message(
        currentOrder.special
            ? `⭐ CLIENTE ESPECIAL: ${currentOrder.cliente}!`
            : "🔔 Novo pedido! Pressione E."
    );


    speak(
        currentOrder.special
            ? `Atenção! Cliente especial. ${currentOrder.cliente} fez um pedido especial. Pressione E para ouvir.`
            : `Novo pedido. Cliente ${currentOrder.cliente}. Pressione E.`
    );

}


/* =========================================================
   OUVIR PEDIDO
========================================================= */

function readOrder() {

    if (
        !gameStarted ||
        rainActive ||
        !currentOrder
    )
        return;


    const orderDescription =
        orderToText(
            currentOrder
        );


    orderText.innerHTML = `

        <strong>
            Cliente:
            ${currentOrder.cliente}
        </strong>

        <br>

        <strong>
            ${currentOrder.prato}
        </strong>

        <br><br>

        ${orderDescription}

    `;


    if (
        currentOrder.special
    ) {

        speakSpecialOrder(
            currentOrder,
            orderDescription
        );

    } else {

        speak(
            `Pedido de ${currentOrder.cliente}. ${currentOrder.prato}. Ingredientes: ${orderDescription}.`
        );

    }

}


/* =========================================================
   SELECIONAR INGREDIENTE
========================================================= */

function selectIngredient(key) {

    if (
        !gameStarted ||
        gameOverState ||
        rainActive ||
        preparing ||
        !currentOrder
    )
        return;


    const ingredient =
        ingredients[key];


    if (!ingredient)
        return;


    if (!isUnlocked(key)) {

        speak(
            `${ingredient.name} está bloqueado. Você precisa de ${ingredient.unlock} pontos.`
        );

        message(
            `🔒 ${ingredient.name}: desbloqueia com ${ingredient.unlock} pontos.`
        );

        return;

    }


    if (
        inventory[ingredient.id] <= 0
    ) {

        speak(
            `${ingredient.name} acabou.`
        );

        message(
            `❌ ${ingredient.name} acabou.`
        );

        checkInventory();

        return;

    }


    inventory[
        ingredient.id
    ]--;


    selectedIngredients.push(
        ingredient.id
    );


    updateIngredientVisual();

    updateInventoryDisplay();


    speak(
        `${ingredient.name} selecionado.`
    );


    message(
        `${ingredient.name} selecionado.`
    );


    checkOrderReady();

    checkInventory();

}


/* =========================================================
   CONTAGEM DOS INGREDIENTES SELECIONADOS
========================================================= */

function countIngredients(list) {

    const counts = {};

    list.forEach(
        id => {

            counts[id] =
                (counts[id] || 0) + 1;

        }
    );

    return counts;

}


/* =========================================================
   PEDIDO CORRETO
========================================================= */

function orderHasValidAmounts(order) {
    return Object.entries(order.ingredients).every(([id, amount]) =>
        id === "pao" ? amount === 1 : amount >= 1 && amount <= 5
    );
}

function orderIsExact() {

    if (!currentOrder)
        return false;


    const selected =
        countIngredients(
            selectedIngredients
        );


    const required =
        currentOrder.ingredients;


    const requiredKeys =
        Object.keys(required);

    const selectedKeys =
        Object.keys(selected);


    if (
        requiredKeys.length !==
        selectedKeys.length
    )
        return false;


    return requiredKeys.every(
        id =>
            selected[id] ===
            required[id]
    );

}


/* =========================================================
   VERIFICAR PEDIDO
========================================================= */

function checkOrderReady() {

    if (
        !currentOrder
    )
        return;


    if (
        orderIsExact()
    ) {

        speak(
            "Todos os ingredientes e quantidades estão corretos. Pressione Enter para preparar."
        );

        message(
            "✅ PEDIDO COMPLETO! ENTER para preparar."
        );

    }

}


/* =========================================================
   BACKSPACE
========================================================= */

function removeLastIngredient() {

    if (
        !gameStarted ||
        rainActive ||
        preparing
    )
        return;


    if (
        selectedIngredients.length === 0
    ) {

        speak(
            "Nenhum ingrediente para remover."
        );

        return;

    }


    const removed =
        selectedIngredients.pop();


    inventory[
        removed
    ]++;


    const item =
        Object
            .values(
                ingredients
            )
            .find(
                i =>
                    i.id === removed
            );


    updateIngredientVisual();

    updateInventoryDisplay();


    speak(
        `${item.name} removido.`
    );


    message(
        `${item.name} removido.`
    );

}


/* =========================================================
   VISUAL
========================================================= */

function updateIngredientVisual() {

    document
        .querySelectorAll(
            ".ingredient"
        )
        .forEach(
            element => {

                element
                    .classList
                    .remove(
                        "selected"
                    );

                const key =
                    element.dataset.key;

                const item =
                    ingredients[key];


                if (
                    selectedIngredients
                        .includes(
                            item.id
                        )
                ) {

                    element
                        .classList
                        .add(
                            "selected"
                        );

                }

            }
        );

}


/* =========================================================
   PREPARAR
========================================================= */

function prepareOrder() {

    if (
        !currentOrder ||
        preparing
    )
        return;


    if (
        !orderIsExact()
    ) {

        speak(
            "O pedido está errado. Verifique os ingredientes e as quantidades."
        );

        message(
            "❌ Pedido incorreto. Verifique as quantidades."
        );

        return;

    }


    preparing = true;


    message(
        "🍳 Preparando..."
    );


    speak(
        "Preparando o pedido."
    );


    setTimeout(() => {

        message(
            `🍔 Pedido pronto! ENTER para entregar para ${currentOrder.cliente}.`
        );

        speak(
            "Pedido pronto. Pressione Enter para entregar."
        );

    }, 1100);

}


/* =========================================================
   ENTREGAR
========================================================= */

function deliverOrder() {

    if (
        !currentOrder ||
        !preparing
    )
        return;


    score +=
        ORDER_POINTS;


    timeLeft +=
        BONUS_TIME;


    scoreElement.textContent =
        score;


    updateTimer();


    checkUnlocks();


    speakSequence([

        `Pedido entregue para ${currentOrder.cliente}.`,

        "Você ganhou 150 pontos.",

        "Mais 7 segundos."

    ]);


    message(
        "🎉 PEDIDO PERFEITO! +150 PONTOS | +15 SEGUNDOS"
    );


    if (
        score >= WIN_SCORE
    ) {

        winGame();

        return;

    }


    setTimeout(
        createOrder,
        1800
    );

}


/* =========================================================
   VERIFICAR ESTOQUE
========================================================= */

function checkInventory() {

    if (
        rainActive ||
        !gameStarted
    )
        return;


    /*
       IMPORTANTE:
       Se QUALQUER ingrediente desbloqueado
       chegar a zero, começa a chuva.
    */

    const emptyIngredient =
        Object.entries(
            ingredients
        )
        .find(
            ([key, item]) =>
                isUnlocked(key) &&
                inventory[item.id] <= 0
        );


    if (emptyIngredient) {

        startIngredientRain();

    }

}


/* =========================================================
   CHUVA
========================================================= */

const rainOrder = [

    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
    "9",
    "0",
    "-",
    "+"

];

let rainIndex = 0;
let rainSequence = [];
let collectedThisRain = 0;


function startIngredientRain() {

    if (rainActive)
        return;


    rainActive = true;

    stopItalianMusic();
    startRainMusic();

    rainMode.style.display =
        "block";


    rainInfo.textContent =
        "🌧️ ESTOQUE ESGOTADO! PREPARE-SE!";


    speakSequence([

        "Atenção! Um ingrediente acabou.",

        "Os pedidos estão pausados.",

        "O tempo está pausado.",

        "Vai começar a chuva de ingredientes.",

        "Você receberá dez unidades de cada ingrediente."

    ]);


    setTimeout(
        beginRainSequence,
        4000
    );

}


function beginRainSequence() {

    rainIndex = 0;

    collectedThisRain = 0;

    // Todos os ingredientes já desbloqueados participam da chuva.
    // O ingrediente que acabou sempre cai primeiro.
    const unlockedKeys = Object.keys(ingredients)
        .filter(key => isUnlocked(key));

    const emptyKeys = unlockedKeys.filter(key => {
        const item = ingredients[key];
        return inventory[item.id] <= 0;
    });

    const otherKeys = unlockedKeys.filter(key => !emptyKeys.includes(key));

    for (let i = otherKeys.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [otherKeys[i], otherKeys[j]] = [otherKeys[j], otherKeys[i]];
    }

    rainSequence = [...emptyKeys, ...otherKeys];

    nextFallingIngredient();

}


/* =========================================================
   PRÓXIMO INGREDIENTE DA CHUVA
========================================================= */

function nextFallingIngredient() {

    /*
       Depois de todos os ingredientes,
       adicionamos +10 em TODOS.
    */

    if (
        rainIndex >=
        rainSequence.length
    ) {

        finishRain();

        return;

    }


    const key =
        rainSequence[
            rainIndex
        ];


    const item =
        ingredients[key];


    /*
       Ingredientes bloqueados não caem.
    */

    if (
        !isUnlocked(key)
    ) {

        rainIndex++;

        nextFallingIngredient();

        return;

    }


    const positionNames = [
        "esquerda",
        "centro",
        "direita"
    ];


    const positionIndex =
        Math.floor(
            Math.random() * 3
        );


    const position =
        [
            20,
            50,
            80
        ][positionIndex];


    rainChef.style.left =
        rainChefX + "%";


    fallingIngredient.className =
        "";


    fallingIngredient
        .classList
        .add(
            item.css
        );


    fallingIngredient.style
        .display =
        "block";


    fallingIngredient.style
        .left =
        position + "%";


    fallingIngredient.style.top =
        "100px";


    rainInfo.textContent =
        `🌧️ ${item.name} — ${positionNames[positionIndex].toUpperCase()}`;


    speak(
        `${item.name}. ${positionNames[positionIndex]}.`
    );


    const duration =
        2400;


    const startTime =
        performance.now();


    function animateFall(now) {

        const elapsed =
            now - startTime;


        const progress =
            Math.min(
                elapsed /
                duration,
                1
            );


        const top =
            100 +
            progress * 420;


        fallingIngredient
            .style
            .top =
            top + "px";


        const horizontalDistance =
            Math.abs(
                rainChefX -
                position
            );


        if (
            progress >= .83 &&
            horizontalDistance <= 10
        ) {

            collectRainIngredient(
                item
            );

            return;

        }


        if (
            progress >= 1
        ) {

            loseRainIngredient(
                item
            );

            return;

        }


        requestAnimationFrame(
            animateFall
        );

    }


    requestAnimationFrame(
        animateFall
    );

}


/* =========================================================
   PEGAR NA CHUVA
========================================================= */

function collectRainIngredient(
    item
) {

    fallingIngredient.style
        .display =
        "none";


    collectedThisRain++;

    inventory[item.id] += RAIN_REWARD;
    updateInventoryDisplay();

    speak(
        `${item.name} coletado. Você recebeu ${RAIN_REWARD} unidades.`
    );


    rainInfo.textContent =
        `✅ ${item.name} coletado!`;


    rainIndex++;


    setTimeout(
        nextFallingIngredient,
        400
    );

}


/* =========================================================
   PERDER NA CHUVA
========================================================= */

function loseRainIngredient(
    item
) {

    fallingIngredient.style
        .display =
        "none";


    speak(
        `${item.name} caiu no chão.`
    );


    rainInfo.textContent =
        `❌ ${item.name} caiu no chão.`
    ;


    rainIndex++;


    setTimeout(
        nextFallingIngredient,
        500
    );

}


/* =========================================================
   FINAL DA CHUVA
========================================================= */

function finishRain() {

    fallingIngredient.style
        .display =
        "none";


    updateInventoryDisplay();

    rainInfo.textContent =
        `🌧️ CHUVA ENCERRADA! ${collectedThisRain} ingrediente(s) coletado(s)!`;

    speakSequence([

        "Coleta encerrada.",

        `${collectedThisRain} ingrediente(s) foram coletados.`,

        `Cada ingrediente coletado rendeu ${RAIN_REWARD} unidades.`,

        "Voltando à cozinha."

    ]);


    setTimeout(() => {

        rainMode.style.display =
            "none";

        stopRainMusic();
        rainActive = false;
        startItalianMusic();


        message(
            "🍳 De volta à cozinha! +10 de cada ingrediente."
        );


        speak(
            "De volta à cozinha. O pedido continua."
        );

    }, 1800);

}


/* =========================================================
   MOVIMENTO
========================================================= */

function moveChef(direction) {

    if (
        !gameStarted ||
        gameOverState ||
        rainActive
    )
        return;


    if (
        direction === "left"
    )
        chefX -= 3;


    if (
        direction === "right"
    )
        chefX += 3;


    chefX =
        Math.max(
            7,
            Math.min(
                93,
                chefX
            )
        );


    chef.style.left =
        chefX + "%";

}


function moveRainChef(direction) {

    if (!rainActive)
        return;


    if (
        direction === "left"
    )
        rainChefX -= 5;


    if (
        direction === "right"
    )
        rainChefX += 5;


    rainChefX =
        Math.max(
            10,
            Math.min(
                90,
                rainChefX
            )
        );


    rainChef.style.left =
        rainChefX + "%";

}


/* =========================================================
   RATO
========================================================= */


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



    if (rainActive)
        return;


    if (!preparing) {

        if (!currentOrder)
            return;


        if (
            orderIsExact()
        ) {

            prepareOrder();

        } else {

            speak(
                "O pedido ainda não está correto."
            );

        }

    } else {

        deliverOrder();

    }

}


/* =========================================================
   TECLADO
========================================================= */

document.addEventListener(
    "keydown",
    event => {

        const key =
            event.key;


        if (
            [
                "ArrowLeft",
                "ArrowRight",
                "Backspace",
                " "
            ].includes(key)
        ) {

            event.preventDefault();

        }


        if (gameOverState) {

            if (
                key === "Enter"
            )
                restartGame();

            return;

        }


        if (!gameStarted) {

            if (
                key === "Enter"
            )
                startGame();

            return;

        }


        if (rainActive) {

            if (
                key === "ArrowLeft" ||
                key.toLowerCase() === "a"
            ) {

                moveRainChef(
                    "left"
                );

            }


            if (
                key === "ArrowRight" ||
                key.toLowerCase() === "d"
            ) {

                moveRainChef(
                    "right"
                );

            }


            return;

        }


        if (
            key === "Enter"
        ) {

            handleEnter();

            return;

        }


        if (
            key.toLowerCase() === "e"
        ) {

            readOrder();

            return;

        }



        if (
            key === "Backspace"
        ) {

            removeLastIngredient();

            return;

        }


        /*
           NOVOS BOTÕES

           8 = cheddar
           9 = frango
           0 = catupiry
           - = bacon
           + = molho verde

           No teclado, + pode aparecer como
           "+" ou "=" dependendo da tecla.
        */

        if (
            [
                "1",
                "2",
                "3",
                "4",
                "5",
                "6",
                "7",
                "8",
                "9",
                "0",
                "-"
            ].includes(key)
        ) {

            selectIngredient(key);

            return;

        }


        if (
            key === "+" ||
            key === "="
        ) {

            selectIngredient("+");

            return;

        }


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

    }
);


/* =========================================================
   COMEÇAR
========================================================= */

function startGame() {

    if (gameStarted)
        return;


    gameStarted = true;

    gameOverState = false;

    victoryState = false;


    startScreen.style.display =
        "none";


    startItalianMusic();


    speakSequence([

        "Bem-vindo ao Cozinheiro Maluco.",

        "Você começa com dez unidades de cada ingrediente.",

        "Se qualquer ingrediente acabar, começa a chuva e você recebe mais dez de cada.",

        "Os ingredientes novos são desbloqueados conforme você ganha pontos.",
        "Depois de quatro clientes normais, chega um cliente especial.",

        "Aos cinco mil pontos, você se torna o melhor chefe de Ubiratã.",

        "Vamos começar!"

    ]);


    createOrder();

    updateInventoryDisplay();

    startTimer();

}


/* =========================================================
   VITÓRIA
========================================================= */

function winGame() {

    clearInterval(
        timerInterval
    );


    gameOverState = true;

    victoryState = true;

    gameStarted = false;


    stopItalianMusic();


    gameOverTitle.textContent =
        "🏆 MELHOR CHEFE DE UBIRATÃ!";


    gameOverTitle.classList.add(
        "victoryTitle"
    );


    gameOverText.innerHTML = `

        🎉 PARABÉNS! 🎉

        <br><br>

        Você alcançou
        <strong>5000 pontos</strong>!

        <br><br>

        Você terminou o jogo como:

        <br>

        👨‍🍳
        <strong>
            O MELHOR CHEFE DE UBIRATÃ!
        </strong>

        <br><br>

        Pontuação final:
        <strong>
            ${score}
        </strong>

    `;


    gameOver.style.display =
        "flex";


    speakSequence([

        "Parabéns!",

        "Você chegou aos quatro mil pontos.",

        "Você terminou o jogo.",

        "Agora você é oficialmente o melhor chefe de Ubiratã!"

    ]);

}


/* =========================================================
   GAME OVER
========================================================= */

function loseGame() {

    clearInterval(
        timerInterval
    );


    gameOverState = true;

    gameStarted = false;


    stopItalianMusic();


    gameOverTitle.textContent =
        "💀 FALÊNCIA!";


    gameOverText.innerHTML = `

        O tempo acabou.

        <br><br>

        Pontuação final:

        <strong>
            ${score}
        </strong>

        pontos.

        <br><br>

        Pressione Enter para tentar novamente.

    `;


    gameOver.style.display =
        "flex";


    speakSequence([

        "Falência.",

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
        START_TIME;

    orderIndex = 0;

    specialClientIndex = 0;

    normalClientsSinceSpecial = 0;

    pendingUnlockedIngredients = [];

    unlockedIngredientKeys = new Set([
        "1", "2", "3", "4", "5", "6", "7"
    ]);

    currentOrder = null;

    selectedIngredients = [];

    preparing = false;

    rainActive = false;


    gameOverState = false;

    victoryState = false;

    inventory =
        makeInitialInventory();


    rainMode.style.display =
        "none";


    scoreElement.textContent =
        "0";


    updateTimer();

    updateInventoryDisplay();


    startScreen.style.display =
        "flex";


    speak(
        "Jogo reiniciado. Pressione Enter para começar."
    );

}


/* =========================================================
   MOUSE
========================================================= */

startButton.addEventListener(
    "mouseenter",
    () => {

        speak(
            "Começar. Pressione Enter."
        );

    }
);


startButton.addEventListener(
    "focus",
    () => {

        speak(
            "Começar. Pressione Enter."
        );

    }
);


startButton.addEventListener(
    "click",
    startGame
);


restartButton.addEventListener(
    "click",
    restartGame
);


document
    .querySelectorAll(
        ".ingredient"
    )
    .forEach(
        element => {

            element.addEventListener(
                "mouseenter",
                () => {

                    const key =
                        element.dataset.key;

                    const item =
                        ingredients[key];


                    if (
                        !isUnlocked(key)
                    ) {

                        speak(
                            `${item.name}. Desbloqueia com ${item.unlock} pontos.`
                        );

                    } else {

                        speak(
                            `${item.name}. ${inventory[item.id]} unidades. Tecla ${key}.`
                        );

                    }

                }
            );

        }
    );


/* =========================================================
   MÚSICA
========================================================= */

let audioContext = null;

let musicTimer = null;

let musicPlaying = false;


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
    start
) {

    if (!audioContext)
        return;


    const oscillator =
        audioContext
            .createOscillator();

    const gain =
        audioContext
            .createGain();


    oscillator.type =
        "triangle";


    oscillator.frequency.value =
        frequency;


    gain.gain.setValueAtTime(
        .0001,
        start
    );


    gain.gain
        .linearRampToValueAtTime(
            .035,
            start + .025
        );


    gain.gain
        .exponentialRampToValueAtTime(
            .001,
            start + duration
        );


    oscillator.connect(gain);

    gain.connect(
        audioContext.destination
    );


    oscillator.start(start);

    oscillator.stop(
        start + duration
    );

}


function playBass(
    frequency,
    start
) {

    if (!audioContext)
        return;


    const oscillator =
        audioContext
            .createOscillator();

    const gain =
        audioContext
            .createGain();


    oscillator.type =
        "sine";


    oscillator.frequency.value =
        frequency;


    gain.gain.setValueAtTime(
        .0001,
        start
    );


    gain.gain
        .exponentialRampToValueAtTime(
            .025,
            start + .03
        );


    gain.gain
        .exponentialRampToValueAtTime(
            .0001,
            start + .35
        );


    oscillator.connect(gain);

    gain.connect(
        audioContext.destination
    );


    oscillator.start(start);

    oscillator.stop(
        start + .4
    );

}


function scheduleMusic() {

    if (
        !musicPlaying ||
        !audioContext
    )
        return;


    const start =
        audioContext.currentTime
        + .05;


    const beat =
        .28;


    melody.forEach(
        (note, index) => {

            playNote(
                note,
                .22,
                start +
                index * beat
            );

        }
    );


    const bass = [

        130.81,
        164.81,
        146.83,
        174.61

    ];


    bass.forEach(
        (note, index) => {

            playBass(
                note,
                start +
                index *
                beat *
                4
            );

        }
    );


    musicTimer =
        setTimeout(
            scheduleMusic,
            melody.length *
            beat *
            1000
        );

}


const rainMelody = [
    523.25, 659.25, 783.99, 659.25,
    587.33, 698.46, 880.00, 698.46,
    523.25, 659.25, 783.99, 987.77,
    880.00, 783.99, 659.25, 523.25
];

let rainMusicPlaying = false;
let rainMusicTimer = null;

function scheduleRainMusic() {
    if (!rainMusicPlaying || !audioContext) return;

    const start = audioContext.currentTime + 0.05;
    const beat = 0.22;

    rainMelody.forEach((note, index) => {
        playNote(note, 0.17, start + index * beat);
    });

    [174.61, 196.00, 220.00, 246.94].forEach((note, index) => {
        playBass(note, start + index * beat * 4);
    });

    rainMusicTimer = setTimeout(
        scheduleRainMusic,
        rainMelody.length * beat * 1000
    );
}

function startRainMusic() {
    try {
        if (!audioContext) {
            audioContext = new (window.AudioContext || window.webkitAudioContext)();
        }

        if (audioContext.state === "suspended") {
            audioContext.resume();
        }

        rainMusicPlaying = true;
        clearTimeout(rainMusicTimer);
        scheduleRainMusic();
    } catch (error) {
        console.log("Música da chuva indisponível.");
    }
}

function stopRainMusic() {
    rainMusicPlaying = false;
    clearTimeout(rainMusicTimer);
}


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

        clearTimeout(
            musicTimer
        );

        scheduleMusic();

    }
    catch (error) {

        console.log(
            "Áudio indisponível."
        );

    }

}


function stopItalianMusic() {

    musicPlaying = false;

    clearTimeout(
        musicTimer
    );

}


/* =========================================================
   INICIALIZAÇÃO
========================================================= */

updateTimer();

updateInventoryDisplay();

message(
    "Passe o mouse sobre COMEÇAR — ENTER para ouvir."
);

</script>

</body>
</html>
