<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>🍳 Cozinheiro Maluco</title>

<style>

/* =========================================================
   CONFIGURAÇÃO GERAL
========================================================= */

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


/* =========================================================
   JOGO
========================================================= */

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

    height: 76px;

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

    animation:
        blink .5s infinite alternate;
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
   ÁREA DA COZINHA
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


/* =========================================================
   PAREDE PIXELADA
========================================================= */

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
   COZINHEIRO
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
   BALCÃO / MENSAGEM
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

    border:
        4px solid #a76334;

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
        1fr 1fr;

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

    padding: 10px 7px;

    background: #1c2a42;

    border: 2px solid #415777;

    text-align: center;

    font-weight: bold;

    transition:
        background .15s,
        border-color .15s;
}

.ingredient.selected {

    background: #315c47;

    border-color: #72e092;
}

.ingredient.low-stock {

    border-color: #d59a3a;
}

.ingredient.empty {

    background: #5a2525;

    border-color: #ff5757;
}

.key {

    color: #ffd83d;

    font-size: 20px;
}

.stock {

    display: block;

    margin-top: 6px;

    color: #ffffff;

    font-size: 12px;

    font-weight: bold;
}

.ingredient.low-stock .stock {

    color: #ffb347;
}

.ingredient.empty .stock {

    color: #ff5757;
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
   RATO
========================================================= */

#ratMenu {

    display: none;

    position: fixed;

    z-index: 400;

    left: 50%;
    top: 50%;

    transform:
        translate(-50%, -50%);

    width: min(560px, 92vw);

    padding: 25px;

    background: #172238;

    border: 5px solid #e3a33b;

    text-align: center;
}

#ratMenu h2 {
    color: #ffd83d;
}

.ratOption {

    margin: 8px 0;

    padding: 12px;

    background: #101827;

    border: 2px solid #405473;
}


/* =========================================================
   CHUVA DE INGREDIENTES
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

.rainTarget {

    position: absolute;

    bottom: 30%;

    width: 2px;
    height: 2px;
}

#targetLeft {
    left: 20%;
}

#targetCenter {
    left: 50%;
}

#targetRight {
    left: 80%;
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
   TIPOS DE INGREDIENTES DA CHUVA
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


/* =========================================================
   CHEF DA CHUVA
========================================================= */

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


/* =========================================================
   GAME OVER
========================================================= */

#gameOver {

    display: none;
}


/* =========================================================
   RESPONSIVIDADE
========================================================= */

@media(max-width: 800px) {

    #topbar {

        height: auto;

        min-height: 70px;

        flex-direction: column;

        gap: 8px;
    }

    .stats {
        font-size: 12px;
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
            repeat(2, 1fr);
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


<!-- =====================================================
     TOPO
===================================================== -->

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
     COZINHA
===================================================== -->

<section id="scene">

    <div class="cloud cloud1"></div>
    <div class="cloud cloud2"></div>


    <div class="station oven">

        <div class="ovenDoor"></div>

        <span>
            FORNO
        </span>

    </div>


    <div class="station grill">

        <div class="grillTop"></div>

        <span>
            CHAPA
        </span>

    </div>


    <div class="station counter">

        <span>
            BALCÃO
        </span>

    </div>


    <div class="floor"></div>


    <div
        class="food bread"
        style="left:25%;">
    </div>


    <div
        class="food tomato"
        style="left:73%;">
    </div>


    <div
        class="food lettuce"
        style="left:82%;">
    </div>


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


    <!-- MENSAGEM -->

    <div id="messageBoard">
        Aguardando...
    </div>

</section>


<!-- =====================================================
     PAINÉIS
===================================================== -->

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

            <div
                class="ingredient"
                data-key="1">

                <span class="key">1</span>
                Pão

                <small
                    class="stock"
                    id="stock-pao">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="2">

                <span class="key">2</span>
                Carne

                <small
                    class="stock"
                    id="stock-carne">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="3">

                <span class="key">3</span>
                Queijo

                <small
                    class="stock"
                    id="stock-queijo">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="4">

                <span class="key">4</span>
                Tomate

                <small
                    class="stock"
                    id="stock-tomate">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="5">

                <span class="key">5</span>
                Alface

                <small
                    class="stock"
                    id="stock-alface">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="6">

                <span class="key">6</span>
                Molho

                <small
                    class="stock"
                    id="stock-molho">
                    10 unidades
                </small>

            </div>


            <div
                class="ingredient"
                data-key="7">

                <span class="key">7</span>
                Cebola

                <small
                    class="stock"
                    id="stock-cebola">
                    10 unidades
                </small>

            </div>

        </div>

        <br>

        <strong>
            E = ouvir pedido
            |
            Backspace = remover
            |
            Enter = preparar/entregar
        </strong>

    </div>

</section>


<!-- =====================================================
     TELA INICIAL
===================================================== -->

<div
    id="startScreen"
    class="overlay">

    <div class="menuBox">

        <div class="menuTitle">
            🍳 COZINHEIRO MALUCO
        </div>

        <p>
            Prepare os pedidos,
            sobreviva ao caos
            e mantenha seu restaurante vivo!
        </p>

        <p style="color:#ffd83d; font-weight:bold;">
            🧺 ESTOQUE INICIAL
        </p>

        <p>
            Você começa com
            <strong>10 unidades de cada ingrediente!</strong>
        </p>


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
                <kbd>1–7</kbd>
                Ingredientes
            </div>

            <div class="control">
                <kbd>BACKSPACE</kbd>
                Remover ingrediente
            </div>

            <div class="control">
                <kbd>Q</kbd>
                Rato
            </div>

            <div class="control">
                <kbd>A / ←</kbd>
                Andar para esquerda
            </div>

            <div class="control">
                <kbd>D / →</kbd>
                Andar para direita
            </div>

        </div>

        <p style="color:#ffd83d">
            Passe o mouse sobre
            COMEÇAR — ENTER para ouvir.
        </p>

    </div>

</div>


<!-- =====================================================
     MENU DO RATO
===================================================== -->

<div id="ratMenu">

    <h2>
        🐀 RATO NA COZINHA!
    </h2>

    <p>
        O que você vai fazer?
    </p>

    <div class="ratOption">
        <strong>
            1 — ESPANTAR
        </strong>
        <br>
        O rato derruba um ingrediente.
    </div>

    <div class="ratOption">
        <strong>
            2 — IGNORAR
        </strong>
        <br>
        O rato come um ingrediente.
    </div>

    <div class="ratOption">
        <strong>
            3 — CHAMAR O GERENTE
        </strong>
        <br>
        O gerente resolve o problema,
        mas custa 50 pontos.
    </div>

</div>


<!-- =====================================================
     CHUVA DE INGREDIENTES
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
     GAME OVER
===================================================== -->

<div
    id="gameOver"
    class="overlay">

    <div class="menuBox">

        <div
            style="
            color:#ff5757;
            font-size:45px;
            font-weight:bold;">
            FALÊNCIA!
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

const BONUS_TIME = 7;


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

const ratMenu =
    document.getElementById("ratMenu");

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

let ratMode = false;

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


/* =========================================================
   ESTOQUE
   AGORA SÃO 10 UNIDADES DE CADA
========================================================= */

let inventory = {

    pao: 10,

    carne: 10,

    queijo: 10,

    tomate: 10,

    alface: 10,

    molho: 10,

    cebola: 10

};


/* =========================================================
   INGREDIENTES
========================================================= */

const ingredients = {

    "1": {
        id: "pao",
        name: "Pão",
        css: "pixel-pao"
    },

    "2": {
        id: "carne",
        name: "Carne",
        css: "pixel-carne"
    },

    "3": {
        id: "queijo",
        name: "Queijo",
        css: "pixel-queijo"
    },

    "4": {
        id: "tomate",
        name: "Tomate",
        css: "pixel-tomate"
    },

    "5": {
        id: "alface",
        name: "Alface",
        css: "pixel-alface"
    },

    "6": {
        id: "molho",
        name: "Molho",
        css: "pixel-molho"
    },

    "7": {
        id: "cebola",
        name: "Cebola",
        css: "pixel-cebola"
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

    if (voice) {

        utter.voice =
            voice;

    }

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
        ) {

            return;

        }

        const utter =
            new SpeechSynthesisUtterance(
                list[index]
            );

        const voice =
            getPortugueseVoice();

        if (voice) {

            utter.voice =
                voice;

        }

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
   ATUALIZAR ESTOQUE NA TELA
========================================================= */

function updateInventoryVisual() {

    Object.keys(inventory).forEach(id => {

        const stockElement =
            document.getElementById(
                `stock-${id}`
            );

        if (!stockElement)
            return;


        const amount =
            inventory[id];


        stockElement.textContent =
            `${amount} ${
                amount === 1
                    ? "unidade"
                    : "unidades"
            }`;


        const key =
            Object.keys(ingredients)
                .find(
                    k =>
                        ingredients[k].id === id
                );


        if (!key)
            return;


        const ingredientElement =
            document.querySelector(
                `.ingredient[data-key="${key}"]`
            );


        if (!ingredientElement)
            return;


        ingredientElement.classList.toggle(
            "low-stock",
            amount > 0 && amount <= 3
        );


        ingredientElement.classList.toggle(
            "empty",
            amount <= 0
        );

    });

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
                rainActive ||
                ratMode
            ) {

                return;

            }

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
   NOVO PEDIDO
========================================================= */

function createOrder() {

    if (rainActive)
        return;


    currentOrder =
        orders[
            orderIndex %
            orders.length
        ];

    orderIndex++;


    selectedIngredients = [];

    preparing = false;


    updateIngredientVisual();


    orderText.innerHTML = `

        <strong>
            🔔 NOVO PEDIDO!
        </strong>

        <br><br>

        Cliente:
        ${currentOrder.cliente}

        <br>

        ${currentOrder.prato}

        <br><br>

        Pressione
        <strong>E</strong>
        para ouvir.

    `;


    message(
        "🔔 Novo pedido! Pressione E."
    );


    speak(
        `Novo pedido. Cliente ${currentOrder.cliente}. Pressione E.`
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


    const names =
        currentOrder.ingredients
            .map(
                id =>
                    Object
                        .values(
                            ingredients
                        )
                        .find(
                            i =>
                                i.id === id
                        )
                        .name
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

        ${names.join(" + ")}

    `;


    speak(
        `Pedido de ${currentOrder.cliente}. ${currentOrder.prato}. Ingredientes: ${names.join(", ")}.`
    );

}


/* =========================================================
   PEGAR INGREDIENTE
========================================================= */

function selectIngredient(key) {

    if (
        !gameStarted ||
        gameOverState ||
        rainActive ||
        ratMode ||
        preparing ||
        !currentOrder
    )
        return;


    const ingredient =
        ingredients[key];


    if (!ingredient)
        return;


    /* estoque acabou */

    if (
        inventory[
            ingredient.id
        ] <= 0
    ) {

        speak(
            `${ingredient.name} acabou. A chuva de ingredientes já vai começar.`
        );

        message(
            `❌ ${ingredient.name} acabou! 🌧️`
        );


        checkInventory();


        return;

    }


    inventory[
        ingredient.id
    ]--;


    updateInventoryVisual();


    selectedIngredients
        .push(
            ingredient.id
        );


    updateIngredientVisual();


    speak(
        `${ingredient.name} selecionado.`
    );


    message(
        `${ingredient.name} selecionado.`
    );


    /* ingrediente errado */

    if (
        !currentOrder
            .ingredients
            .includes(
                ingredient.id
            )
    ) {

        speak(
            `${ingredient.name}. Atenção: o pedido não contém ${ingredient.name.toLowerCase()}. Pressione Backspace para remover.`
        );

        checkInventory();

        return;

    }


    checkOrderReady();


    checkInventory();

}


/* =========================================================
   VERIFICAR PEDIDO
========================================================= */

function checkOrderReady() {

    const correct =
        currentOrder
            .ingredients
            .every(
                id =>
                    selectedIngredients
                        .includes(id)
            );


    if (
        correct &&
        selectedIngredients.length ===
        currentOrder.ingredients.length
    ) {

        const names =
            currentOrder.ingredients
                .map(
                    id =>
                        Object
                            .values(
                                ingredients
                            )
                            .find(
                                i =>
                                    i.id === id
                            )
                            .name
                );


        speakSequence([

            "Todos os ingredientes necessários foram selecionados.",

            names.join(", ") + ".",

            "Pressione Enter para preparar."

        ]);


        message(
            "Todos os ingredientes corretos! ENTER para preparar."
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


    updateInventoryVisual();


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


    speak(
        `${item.name} removido.`
    );


    message(
        `${item.name} removido.`
    );

}


/* =========================================================
   VISUAL DOS INGREDIENTES SELECIONADOS
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
                    element
                        .dataset
                        .key;

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


    const exact =
        selectedIngredients.length ===
        currentOrder.ingredients.length
        &&
        currentOrder.ingredients.every(
            id =>
                selectedIngredients
                    .includes(id)
        );


    if (!exact) {

        speak(
            "O pedido está errado. Verifique os ingredientes."
        );

        message(
            "❌ Pedido incorreto."
        );

        return;

    }


    preparing = true;


    message(
        "🍳 Preparando..."
    );


    speak(
        "Preparando."
    );


    setTimeout(() => {

        message(
            `🍔 Hambúrguer pronto! ENTER para entregar para ${currentOrder.cliente}.`
        );

        speak(
            "Hambúrguer pronto. Pressione Enter para entregar."
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


    speakSequence([

        `Pedido entregue para ${currentOrder.cliente}.`,

        "Você ganhou 150 pontos.",

        "Mais 7 segundos."

    ]);


    message(
        "🎉 PEDIDO PERFEITO! +150 PONTOS | +7 SEGUNDOS"
    );


    setTimeout(
        createOrder,
        1800
    );

}


/* =========================================================
   VERIFICAR ESTOQUE
   IMPORTANTE:
   SE QUALQUER INGREDIENTE CHEGAR A 0,
   A CHUVA COMEÇA.
========================================================= */

function checkInventory() {

    if (rainActive)
        return;


    const values =
        Object.values(
            inventory
        );


    const empty =
        values.some(
            amount =>
                amount <= 0
        );


    if (empty) {

        startIngredientRain();

    }

}


/* =========================================================
   COMEÇAR CHUVA
========================================================= */

function startIngredientRain() {

    if (rainActive)
        return;


    rainActive = true;


    rainMode.style.display =
        "block";


    rainInfo.textContent =
        "🌧️ ESTOQUE ESGOTADO! PREPARE-SE!";


    speakSequence([

        "Atenção! Um ingrediente acabou.",

        "Os pedidos estão pausados.",

        "O tempo também está pausado.",

        "Prepare-se para a chuva de ingredientes."

    ]);


    setTimeout(
        beginRainSequence,
        3200
    );

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
    "7"

];

let rainIndex = 0;

let collectedThisRain = 0;


/* =========================================================
   PRÓXIMO INGREDIENTE
========================================================= */

function beginRainSequence() {

    rainIndex = 0;

    collectedThisRain = 0;

    nextFallingIngredient();

}


function nextFallingIngredient() {

    if (
        rainIndex >=
        rainOrder.length
    ) {

        finishRain();

        return;

    }


    const key =
        rainOrder[
            rainIndex
        ];


    const item =
        ingredients[key];


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


    fallingIngredient
        .className = "";


    fallingIngredient
        .classList
        .add(
            item.css
        );


    fallingIngredient.style
        .display = "block";


    fallingIngredient.style
        .left =
        position + "%";


    fallingIngredient.style
        .top = "100px";


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


        const chefPosition =
            rainChefX;


        const ingredientPosition =
            position;


        const horizontalDistance =
            Math.abs(
                chefPosition -
                ingredientPosition
            );


        /*
           COLISÃO
        */

        if (
            progress >= .83 &&
            horizontalDistance <= 10
        ) {

            collectRainIngredient(
                item
            );

            return;

        }


        /*
           CAIU NO CHÃO
        */

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
   COLETAR INGREDIENTE
========================================================= */

function collectRainIngredient(
    item
) {

    fallingIngredient.style
        .display = "none";


    inventory[
        item.id
    ]++;


    updateInventoryVisual();


    collectedThisRain++;


    speak(
        `${item.name} coletado.`
    );


    rainInfo.textContent =
        `✅ ${item.name} COLETADO!`;


    rainIndex++;


    setTimeout(
        nextFallingIngredient,
        550
    );

}


/* =========================================================
   INGREDIENTE PERDIDO
========================================================= */

function loseRainIngredient(
    item
) {

    fallingIngredient.style
        .display = "none";


    speak(
        `${item.name} perdido.`
    );


    rainInfo.textContent =
        `❌ ${item.name} caiu no chão e foi perdido.`;


    rainIndex++;


    setTimeout(
        nextFallingIngredient,
        700
    );

}


/* =========================================================
   FINAL DA CHUVA
========================================================= */

function finishRain() {

    fallingIngredient.style
        .display = "none";


    rainInfo.textContent =
        "🍳 COLETA ENCERRADA! VOLTANDO À COZINHA...";


    speakSequence([

        "Coleta encerrada.",

        "Voltando à cozinha.",

        "O jogo continua."

    ]);


    setTimeout(() => {

        rainMode.style.display =
            "none";


        rainActive = false;


        updateInventoryVisual();


        message(
            "🍳 De volta à cozinha! Continue o pedido."
        );


        speak(
            "De volta à cozinha. Continue o pedido."
        );


        /*
           Se ainda houver algum ingrediente
           zerado depois da chuva, começa
           outra chuva.
        */

        checkInventory();

    }, 1800);

}


/* =========================================================
   MOVIMENTO NORMAL
========================================================= */

function moveChef(direction) {

    if (
        !gameStarted ||
        gameOverState ||
        rainActive ||
        ratMode
    )
        return;


    if (
        direction === "left"
    ) {

        chefX -= 3;

    }


    if (
        direction === "right"
    ) {

        chefX += 3;

    }


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


/* =========================================================
   MOVIMENTO NA CHUVA
========================================================= */

function moveRainChef(
    direction
) {

    if (!rainActive)
        return;


    if (
        direction === "left"
    ) {

        rainChefX -= 5;

    }


    if (
        direction === "right"
    ) {

        rainChefX += 5;

    }


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

function openRatMenu() {

    if (
        !gameStarted ||
        rainActive ||
        preparing
    )
        return;


    ratMode = true;


    ratMenu.style.display =
        "block";


    speakSequence([

        "Rato na cozinha.",

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


function ratChoice(key) {

    if (!ratMode)
        return;


    const possible =
        Object.keys(
            inventory
        )
        .filter(
            id =>
                inventory[id] > 0
        );


    if (
        possible.length === 0
    ) {

        closeRatMenu();

        startIngredientRain();

        return;

    }


    const chosen =
        possible[
            Math.floor(
                Math.random() *
                possible.length
            )
        ];


    const item =
        Object
            .values(
                ingredients
            )
            .find(
                i =>
                    i.id === chosen
            );


    /*
       ESPANTAR
    */

    if (key === "1") {

        inventory[
            chosen
        ]--;


        updateInventoryVisual();


        speak(
            `Você espantou o rato. Ele derrubou ${item.name}.`
        );


        message(
            `🐀 Rato espantado. ${item.name} foi derrubado.`
        );


        closeRatMenu();

        checkInventory();

        return;

    }


    /*
       IGNORAR
    */

    if (key === "2") {

        inventory[
            chosen
        ]--;


        updateInventoryVisual();


        speak(
            `Você ignorou o rato. Ele comeu ${item.name}.`
        );


        message(
            `🐀 O rato comeu ${item.name}.`
        );


        closeRatMenu();

        checkInventory();

        return;

    }


    /*
       GERENTE
    */

    if (key === "3") {

        if (score >= 50) {

            score -= 50;

            scoreElement.textContent =
                score;


            speak(
                "O gerente expulsou o rato. Menos 50 pontos."
            );


            message(
                "👨‍💼 Gerente chamado. -50 pontos."
            );

        } else {

            speak(
                "Você não tem 50 pontos para chamar o gerente."
            );


            message(
                "❌ Pontos insuficientes."
            );

        }


        closeRatMenu();

    }

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


    if (ratMode)
        return;


    if (rainActive)
        return;


    if (!preparing) {

        if (!currentOrder)
            return;


        const exact =
            selectedIngredients.length ===
            currentOrder.ingredients.length
            &&
            currentOrder.ingredients.every(
                id =>
                    selectedIngredients
                        .includes(id)
            );


        if (exact) {

            prepareOrder();

        } else {

            speak(
                "O pedido ainda não está completo."
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


        /*
           GAME OVER
        */

        if (
            gameOverState
        ) {

            if (
                key === "Enter"
            ) {

                restartGame();

            }

            return;

        }


        /*
           MENU INICIAL
        */

        if (
            !gameStarted
        ) {

            if (
                key === "Enter"
            ) {

                startGame();

            }

            return;

        }


        /*
           CHUVA
        */

        if (
            rainActive
        ) {

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


        /*
           RATO
        */

        if (
            ratMode
        ) {

            if (
                ["1","2","3"]
                    .includes(key)
            ) {

                ratChoice(key);

            }

            return;

        }


        /*
           ENTER
        */

        if (
            key === "Enter"
        ) {

            handleEnter();

            return;

        }


        /*
           E
        */

        if (
            key.toLowerCase() === "e"
        ) {

            readOrder();

            return;

        }


        /*
           Q
        */

        if (
            key.toLowerCase() === "q"
        ) {

            openRatMenu();

            return;

        }


        /*
           BACKSPACE
        */

        if (
            key === "Backspace"
        ) {

            removeLastIngredient();

            return;

        }


        /*
           INGREDIENTES
        */

        if (
            ["1","2","3","4","5","6","7"]
                .includes(key)
        ) {

            selectIngredient(key);

            return;

        }


        /*
           MOVIMENTO
        */

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


    startScreen.style.display =
        "none";


    /*
       Música
    */

    startItalianMusic();


    /*
       Tutorial falado
    */

    speakSequence([

        "Bem-vindo ao Cozinheiro Maluco.",

        "Você tem três minutos.",

        "Atenção: você começa com 10 unidades de cada ingrediente.",

        "Pão é 1. Carne é 2. Queijo é 3.",

        "Tomate é 4. Alface é 5. Molho é 6. Cebola é 7.",

        "Quando qualquer ingrediente acabar, começará a chuva de ingredientes.",

        "Memorizou bem?",

        "Bom jogo!"

    ]);


    createOrder();

    startTimer();

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

    currentOrder = null;

    selectedIngredients = [];

    preparing = false;

    rainActive = false;

    ratMode = false;

    gameOverState = false;

    gameStarted = false;


    /*
       ESTOQUE VOLTA PARA 10
    */

    inventory = {

        pao: 10,

        carne: 10,

        queijo: 10,

        tomate: 10,

        alface: 10,

        molho: 10,

        cebola: 10

    };


    rainMode.style.display =
        "none";


    ratMenu.style.display =
        "none";


    scoreElement.textContent =
        "0";


    updateTimer();

    updateInventoryVisual();


    startScreen.style.display =
        "flex";


    speak(
        "Jogo reiniciado. Você começa com 10 unidades de cada ingrediente. Pressione Enter para começar."
    );

}


/* =========================================================
   MOUSE NO COMEÇAR
========================================================= */

startButton.addEventListener(
    "mouseenter",
    () => {

        speak(
            "Começar. Você possui 10 unidades de cada ingrediente. Quando qualquer ingrediente acabar, começa a chuva de ingredientes. Pressione Enter."
        );

    }
);


startButton.addEventListener(
    "focus",
    () => {

        speak(
            "Começar. Você possui 10 unidades de cada ingrediente. Quando qualquer ingrediente acabar, começa a chuva de ingredientes. Pressione Enter."
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


/* =========================================================
   MOUSE NOS INGREDIENTES
========================================================= */

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

                    const amount =
                        inventory[
                            item.id
                        ];


                    speak(
                        `${item.name}. Tecla ${key}. ${amount} ${
                            amount === 1
                                ? "unidade"
                                : "unidades"
                        } disponíveis.`
                    );

                }
            );

        }
    );


/* =========================================================
   MÚSICA ITALIANA
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

updateInventoryVisual();

message(
    "Passe o mouse sobre COMEÇAR — ENTER para ouvir."
);

</script>

</body>
</html>
