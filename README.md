<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🍳 Cozinheiro Maluco</title>

<style>
* {
    box-sizing: border-box;
}

html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background: #111827;
    color: white;
    font-family: monospace;
}

body {
    overflow: hidden;
}

#game {
    width: 100vw;
    height: 100vh;
    position: relative;
}

canvas {
    width: 100%;
    height: 100%;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    display: block;
}

/* Interface acessível */
#screenReader {
    position: absolute;
    left: -9999px;
    width: 1px;
    height: 1px;
    overflow: hidden;
}

#message {
    position: absolute;
    left: 50%;
    bottom: 20px;
    transform: translateX(-50%);
    background: rgba(0,0,0,.88);
    border: 3px solid #fff;
    padding: 12px 20px;
    max-width: 90%;
    text-align: center;
    font-size: 18px;
    line-height: 1.4;
    border-radius: 8px;
    display: none;
}

#startOverlay {
    position: absolute;
    inset: 0;
    background: rgba(10, 15, 25, .96);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
}

#startBox {
    width: min(700px, 90%);
    border: 5px solid #facc15;
    background: #1f2937;
    padding: 30px;
    text-align: center;
    box-shadow: 0 0 0 6px #111827;
}

#startBox h1 {
    color: #facc15;
    font-size: 42px;
    margin-top: 0;
}

#startBox p {
    font-size: 18px;
    line-height: 1.6;
}

#startButton {
    background: #facc15;
    border: 4px solid #78350f;
    padding: 15px 30px;
    font-size: 22px;
    font-family: monospace;
    font-weight: bold;
    cursor: pointer;
}

#startButton:hover {
    background: #fde68a;
}

.hidden {
    display: none !important;
}
</style>
</head>

<body>

<div id="game">

<canvas id="canvas" width="960" height="540"></canvas>

<div id="screenReader" aria-live="assertive"></div>

<div id="message"></div>

<div id="startOverlay">
    <div id="startBox">
        <h1>🍳 COZINHEIRO MALUCO</h1>

        <p>
            Este jogo pode ser jogado inteiramente pelo teclado.
            <br><br>
            A introdução será narrada pelo computador.
            <br>
            Você não precisa usar o mouse.
        </p>

        <button id="startButton">
            COMEÇAR — ENTER
        </button>

        <p>
            Depois de começar, pressione <b>Backspace</b>
            para repetir informações importantes.
        </p>
    </div>
</div>

</div>

<script>

/* =========================================================
   COZINHEIRO MALUCO
   ========================================================= */

/* ---------- CANVAS ---------- */

const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

const W = canvas.width;
const H = canvas.height;


/* ---------- ACESSIBILIDADE ---------- */

const sr = document.getElementById("screenReader");
const message = document.getElementById("message");

let speechEnabled = true;
let speaking = false;

function speak(text, interrupt = false) {

    if (!speechEnabled || !("speechSynthesis" in window)) {
        return;
    }

    if (interrupt) {
        speechSynthesis.cancel();
    }

    const utterance = new SpeechSynthesisUtterance(text);

    utterance.lang = "pt-BR";

    /*
       Velocidade relativamente rápida para que as
       confirmações não atrapalhem o jogador.
    */
    utterance.rate = 1.25;
    utterance.pitch = 1;

    speaking = true;

    utterance.onend = () => {
        speaking = false;
    };

    speechSynthesis.speak(utterance);

    sr.textContent = text;
}

function quickSpeak(text) {

    if (!speechEnabled) return;

    if ("speechSynthesis" in window) {
        speechSynthesis.cancel();

        const utterance = new SpeechSynthesisUtterance(text);

        utterance.lang = "pt-BR";
        utterance.rate = 1.5;
        utterance.pitch = 1;

        speechSynthesis.speak(utterance);

        sr.textContent = text;
    }
}

function showMessage(text, duration = 2200) {

    message.innerText = text;
    message.style.display = "block";

    clearTimeout(showMessage.timer);

    showMessage.timer = setTimeout(() => {
        message.style.display = "none";
    }, duration);
}


/* ---------- ESTADO DO JOGO ---------- */

const STATE = {

    TUTORIAL: "tutorial",
    PLAYING: "playing",
    EVENT: "event",
    GAMEOVER: "gameover"

};

let state = STATE.TUTORIAL;


/* ---------- JOGADOR ---------- */

let score = 0;
let timeLeft = 180;
let bestScore = Number(localStorage.getItem("cozinheiroBest") || 0);

let lastTime = performance.now();

let currentOrder = null;

let selectedIngredients = [];

let event = null;

let tutorialStep = 0;

let gameStarted = false;


/* ---------- ESTOQUE ---------- */

const stock = {

    pao: 8,
    carne: 6,
    queijo: 4,
    tomate: 7,
    alface: 5,
    molho: 4,
    cebola: 3,
    cogumelo: 3,
    ovo: 3,
    especial: 1

};


/* ---------- INGREDIENTES ---------- */

const ingredients = {

    "1": {
        id: "pao",
        name: "pão",
        icon: "🍞"
    },

    "2": {
        id: "carne",
        name: "carne",
        icon: "🥩"
    },

    "3": {
        id: "queijo",
        name: "queijo",
        icon: "🧀"
    },

    "4": {
        id: "tomate",
        name: "tomate",
        icon: "🍅"
    },

    "5": {
        id: "alface",
        name: "alface",
        icon: "🥬"
    },

    "6": {
        id: "molho",
        name: "molho",
        icon: "🥫"
    },

    "7": {
        id: "cebola",
        name: "cebola",
        icon: "🧅"
    },

    "8": {
        id: "cogumelo",
        name: "cogumelo",
        icon: "🍄"
    },

    "9": {
        id: "ovo",
        name: "ovo",
        icon: "🥚"
    },

    "0": {
        id: "especial",
        name: "ingrediente especial",
        icon: "⭐"
    }

};


/* ---------- PEDIDOS ---------- */

const orders = [

    {
        client: "Maria",
        dish: "Hambúrguer",
        ingredients: ["pao", "carne", "queijo", "tomate"],
        names: ["pão", "carne", "queijo", "tomate"],
        points: 150
    },

    {
        client: "João",
        dish: "Hambúrguer com alface",
        ingredients: ["pao", "carne", "queijo", "alface"],
        names: ["pão", "carne", "queijo", "alface"],
        points: 170
    },

    {
        client: "Ana",
        dish: "Hambúrguer especial",
        ingredients: ["pao", "carne", "queijo", "tomate", "molho"],
        names: ["pão", "carne", "queijo", "tomate", "molho"],
        points: 200
    },

    {
        client: "Pedro",
        dish: "Hambúrguer com cebola",
        ingredients: ["pao", "carne", "queijo", "cebola"],
        names: ["pão", "carne", "queijo", "cebola"],
        points: 180
    }

];

let orderIndex = 0;


/* =========================================================
   PIXEL ART
   ========================================================= */

function rect(x, y, w, h, color) {

    ctx.fillStyle = color;
    ctx.fillRect(x, y, w, h);

}

function pixelText(text, x, y, size, color = "#fff") {

    ctx.fillStyle = color;
    ctx.font = `bold ${size}px monospace`;
    ctx.fillText(text, x, y);

}


/* ---------- COZINHA ---------- */

function drawKitchen() {

    /* fundo */

    rect(0, 0, W, H, "#182235");

    /* parede */

    rect(0, 70, W, 280, "#8b5e3c");

    /* azulejos */

    for (let x = 0; x < W; x += 60) {

        for (let y = 70; y < 350; y += 40) {

            ctx.strokeStyle = "#a97850";
            ctx.lineWidth = 2;

            ctx.strokeRect(x, y, 60, 40);

        }

    }

    /* chão */

    rect(0, 350, W, 190, "#57402f");

    for (let x = 0; x < W; x += 80) {

        for (let y = 350; y < H; y += 40) {

            ctx.strokeStyle = "#463323";
            ctx.strokeRect(x, y, 80, 40);

        }

    }

    /* balcão */

    rect(0, 300, W, 70, "#9b6032");
    rect(0, 300, W, 12, "#d18a4b");

    /* forno */

    rect(80, 130, 190, 150, "#252525");
    rect(100, 150, 150, 90, "#111");

    rect(115, 165, 120, 60, "#542f20");

    pixelText("FORNO", 125, 260, 20, "#facc15");

    /* chapa */

    rect(370, 150, 220, 90, "#222");
    rect(385, 165, 190, 50, "#444");

    pixelText("CHAPA", 425, 260, 20, "#facc15");

    /* pia */

    rect(680, 140, 180, 120, "#555");

    rect(700, 160, 140, 70, "#222");

    pixelText("PIA", 750, 250, 20, "#facc15");

    /* armário */

    rect(30, 70, 180, 55, "#754c2d");

    pixelText("DESPENSA", 50, 105, 20, "#fff");

    /* personagem */

    drawChef(480, 250);

}


/* ---------- COZINHEIRO ---------- */

function drawChef(x, y) {

    /* corpo */

    rect(x - 35, y, 70, 70, "#f5f5f5");

    /* cabeça */

    rect(x - 30, y - 45, 60, 55, "#d99a6c");

    /* chapéu */

    rect(x - 40, y - 70, 80, 30, "#fff");

    rect(x - 25, y - 90, 50, 25, "#fff");

    /* olhos */

    rect(x - 15, y - 25, 7, 7, "#111");
    rect(x + 8, y - 25, 7, 7, "#111");

    /* bigode */

    rect(x - 10, y - 8, 20, 6, "#3b2417");

}


/* ---------- RATO ---------- */

function drawRat() {

    if (!event || event.type !== "rat") return;

    const x = 720;
    const y = 310;

    /* corpo */

    rect(x, y, 45, 25, "#777");

    /* cabeça */

    rect(x + 35, y - 5, 25, 25, "#888");

    /* orelha */

    rect(x + 40, y - 15, 12, 12, "#999");

    /* olho */

    rect(x + 52, y, 5, 5, "#ff0000");

    /* cauda */

    ctx.strokeStyle = "#999";
    ctx.lineWidth = 4;

    ctx.beginPath();

    ctx.moveTo(x, y + 10);
    ctx.quadraticCurveTo(x - 40, y - 10, x - 55, y + 20);

    ctx.stroke();

}


/* =========================================================
   INTERFACE
   ========================================================= */

function drawUI() {

    /* barra superior */

    rect(0, 0, W, 70, "#111827");

    pixelText("🍳 COZINHEIRO MALUCO", 25, 42, 28, "#facc15");

    pixelText(
        `⭐ ${score}`,
        600,
        40,
        24,
        "#fff"
    );

    pixelText(
        `⏱️ ${formatTime(timeLeft)}`,
        780,
        40,
        24,
        timeLeft <= 30 ? "#ef4444" : "#fff"
    );

    /* pedidos */

    rect(20, 390, 430, 130, "#111827");

    pixelText("📋 PEDIDO", 40, 420, 22, "#facc15");

    if (currentOrder) {

        pixelText(
            `${currentOrder.client} — ${currentOrder.dish}`,
            40,
            450,
            19,
            "#fff"
        );

        pixelText(
            `[E] Ver pedido`,
            40,
            485,
            18,
            "#93c5fd"
        );

    } else {

        pixelText(
            "Nenhum pedido ativo.",
            40,
            450,
            18
        );

    }

    /* ingredientes */

    rect(470, 390, 470, 130, "#111827");

    pixelText("🧺 INGREDIENTES", 490, 420, 22, "#facc15");

    const list = Object.entries(ingredients);

    let x = 490;
    let y = 455;

    list.forEach(([key, item], index) => {

        pixelText(
            `[${key}] ${item.name}`,
            x,
            y,
            15,
            "#fff"
        );

        x += 145;

        if ((index + 1) % 3 === 0) {

            x = 490;
            y += 30;

        }

    });

}


/* ---------- EVENT UI ---------- */

function drawEventUI() {

    if (!event) return;

    rect(250, 110, 460, 170, "rgba(0,0,0,.92)");

    ctx.strokeStyle = "#ef4444";
    ctx.lineWidth = 5;
    ctx.strokeRect(250, 110, 460, 170);

    if (event.type === "rat") {

        pixelText(
            "🐀 RATO NA COZINHA!",
            290,
            155,
            27,
            "#f87171"
        );

        pixelText(
            "[1] Espantar",
            300,
            195,
            20
        );

        pixelText(
            "[2] Ignorar",
            300,
            225,
            20
        );

        pixelText(
            "[3] Chamar gerente",
            300,
            255,
            20
        );

    }

}


/* =========================================================
   PEDIDOS
   ========================================================= */

function newOrder() {

    currentOrder = orders[
        orderIndex % orders.length
    ];

    orderIndex++;

    selectedIngredients = [];

    speak(
        `Novo pedido. Cliente: ${currentOrder.client}. Pedido: ${currentOrder.dish}. Ingredientes: ${currentOrder.names.join(", ")}. Pressione E para começar o pedido. Pressione Backspace para repetir.`,
        true
    );

    showMessage(
        `🔔 NOVO PEDIDO — ${currentOrder.client}: ${currentOrder.dish}`
    );

}


/* ---------- COMEÇAR PEDIDO ---------- */

function startOrder() {

    if (!currentOrder) {

        speak("Não existe nenhum pedido agora.");

        return;

    }

    speak(
        `Pedido da ${currentOrder.client} iniciado. Você precisa de ${currentOrder.names.join(", ")}. Escolha os ingredientes usando as teclas numéricas.`,
        true
    );

}


/* ---------- INGREDIENTE ---------- */

function chooseIngredient(key) {

    if (!currentOrder) {

        quickSpeak("Não existe pedido ativo.");

        return;

    }

    const item = ingredients[key];

    if (!item) return;

    /* estoque */

    if (stock[item.id] <= 0) {

        speak(
            `${item.name} está esgotado.`
        );

        return;

    }

    selectedIngredients.push(item.id);

    stock[item.id]--;

    /* fala rápida */

    quickSpeak(item.name);

    /* verifica se o ingrediente é necessário */

    if (!currentOrder.ingredients.includes(item.id)) {

        setTimeout(() => {

            speak(
                `Atenção. O pedido não contém ${item.name}. Pressione Backspace para remover o último ingrediente.`,
                true
            );

        }, 250);

        return;

    }

    checkOrder();

}


/* ---------- BACKSPACE ---------- */

function removeLastIngredient() {

    if (selectedIngredients.length === 0) {

        repeatCurrentInformation();

        return;

    }

    const removed =
        selectedIngredients.pop();

    stock[removed]++;

    const item = Object.values(ingredients)
        .find(i => i.id === removed);

    speak(
        `${item.name} removido.`
    );

    checkOrder();

}


/* ---------- REPETIR ---------- */

function repeatCurrentInformation() {

    if (state === STATE.TUTORIAL) {

        tutorial();

        return;

    }

    if (currentOrder) {

        speak(
            `Pedido de ${currentOrder.client}. ${currentOrder.dish}. Ingredientes: ${currentOrder.names.join(", ")}.`,
            true
        );

        return;

    }

    if (event) {

        speak(
            "Opções: tecla 1 para espantar. Tecla 2 para ignorar. Tecla 3 para chamar o gerente.",
            true
        );

        return;

    }

    speak(
        `Tempo restante: ${formatTime(timeLeft)}. Pontuação: ${score}.`
    );

}


/* ---------- VERIFICA PEDIDO ---------- */

function checkOrder() {

    if (!currentOrder) return;

    const required =
        currentOrder.ingredients;

    /*
       Verifica se todos os ingredientes necessários
       estão presentes.
    */

    const complete =
        required.every(
            ingredient =>
                selectedIngredients.includes(ingredient)
        );

    if (!complete) return;

    /* se houver ingrediente errado */

    const wrong =
        selectedIngredients.some(
            ingredient =>
                !required.includes(ingredient)
        );

    if (wrong) return;

    speak(
        "Pedido completo. Pressione Enter para preparar.",
        true
    );

}


/* ---------- PREPARAR ---------- */

function prepareOrder() {

    if (!currentOrder) {

        speak("Não existe pedido ativo.");

        return;

    }

    const required =
        currentOrder.ingredients;

    const complete =
        required.every(
            ingredient =>
                selectedIngredients.includes(ingredient)
        );

    const wrong =
        selectedIngredients.some(
            ingredient =>
                !required.includes(ingredient)
        );

    if (!complete || wrong) {

        speak(
            "O pedido ainda não está correto."
        );

        return;

    }

    speak(
        "Preparando.",
        true
    );

    showMessage("🍳 PREPARANDO...");

    setTimeout(() => {

        speak(
            `${currentOrder.dish} pronto. Pressione Enter para entregar.`,
            true
        );

        showMessage("🍔 PEDIDO PRONTO!");

        state = STATE.PLAYING;

    }, 1500);

    currentOrder.prepared = true;

}


/* ---------- ENTREGAR ---------- */

function deliverOrder() {

    if (!currentOrder) {

        speak("Não existe pedido para entregar.");

        return;

    }

    if (!currentOrder.prepared) {

        prepareOrder();

        return;

    }

    const basePoints =
        currentOrder.points;

    const speedBonus =
        Math.min(
            50,
            Math.max(
                0,
                Math.floor(timeLeft / 10)
            )
        );

    const perfectBonus =
        25;

    const total =
        basePoints +
        speedBonus +
        perfectBonus;

    score += total;

    timeLeft += 7;

    speak(
        `Pedido entregue para ${currentOrder.client}. Você ganhou ${basePoints} pontos. Bônus de velocidade: ${speedBonus} pontos. Bônus de pedido perfeito: ${perfectBonus} pontos. Total: ${total} pontos. Tempo aumentado em sete segundos.`,
        true
    );

    showMessage(
        `🎉 +${total} PONTOS    ⏱️ +7 SEGUNDOS`
    );

    currentOrder = null;

    selectedIngredients = [];

    /* próximo pedido */

    setTimeout(() => {

        newOrder();

    }, 1800);

}


/* =========================================================
   EVENTOS
   ========================================================= */

function triggerRat() {

    if (state !== STATE.PLAYING) return;

    if (event) return;

    event = {
        type: "rat"
    };

    state = STATE.EVENT;

    speak(
        "Atenção. Um rato entrou na cozinha. Pressione Q para ver as opções.",
        true
    );

    showMessage("🐀 RATO NA COZINHA! [Q] VER OPÇÕES");

}


/* ---------- MENU DO RATO ---------- */

function openRatOptions() {

    if (!event) return;

    speak(
        "Opções. Tecla 1: espantar o rato. Tecla 2: ignorar o rato. Tecla 3: chamar o gerente.",
        true
    );

}


/* ---------- ESPANTAR ---------- */

function scareRat() {

    event = null;
    state = STATE.PLAYING;

    timeLeft = Math.max(
        0,
        timeLeft - 5
    );

    speak(
        "Você espantou o rato. Você perdeu cinco segundos.",
        true
    );

}


/* ---------- IGNORAR ---------- */

function ignoreRat() {

    state = STATE.PLAYING;

    speak(
        "Você ignorou o rato. Continue trabalhando.",
        true
    );

    /*
       Depois de alguns segundos o rato come
       um ingrediente.
    */

    setTimeout(() => {

        ratEatIngredient();

    }, 3500);

    event = null;

}


/* ---------- RATO COME ---------- */

function ratEatIngredient() {

    const possible =
        ["queijo", "carne", "pao", "tomate", "alface"];

    const available =
        possible.filter(
            id => stock[id] > 0
        );

    if (available.length === 0) {

        speak(
            "O rato não encontrou ingredientes para comer."
        );

        return;

    }

    const id =
        available[
            Math.floor(
                Math.random() * available.length
            )
        ];

    stock[id]--;

    const item =
        Object.values(ingredients)
        .find(i => i.id === id);

    speak(
        `O rato comeu um ${item.name}.`,
        true
    );

}


/* ---------- GERENTE ---------- */

function callManager() {

    event = null;

    state = STATE.PLAYING;

    timeLeft = Math.max(
        0,
        timeLeft - 10
    );

    speak(
        "Você chamou o gerente. O gerente removeu o rato. Você perdeu dez segundos e gastou dez reais.",
        true
    );

}


/* =========================================================
   TUTORIAL
   ========================================================= */

const tutorialLines = [

    "Bem-vindo ao Cozinheiro Maluco.",

    "Este jogo pode ser jogado completamente pelo teclado.",

    "Vou ensinar os botões dos ingredientes.",

    "Tecla 1: pão.",

    "Tecla 2: carne.",

    "Tecla 3: queijo.",

    "Tecla 4: tomate.",

    "Tecla 5: alface.",

    "Tecla 6: molho.",

    "Tecla 7: cebola.",

    "Tecla 8: cogumelo.",

    "Tecla 9: ovo.",

    "Tecla zero: ingrediente especial.",

    "A tecla E serve para abrir ou iniciar um pedido.",

    "A tecla Q abre as opções quando acontece um evento.",

    "A tecla Enter confirma ações e entrega pedidos.",

    "A tecla Backspace repete informações ou remove o último ingrediente.",

    "Você começa com três minutos.",

    "Cada pedido correto aumenta seu tempo em sete segundos.",

    "Se o tempo chegar a zero, seu restaurante irá à falência.",

    "Se quiser ouvir estas instruções novamente, pressione Backspace.",

    "Quando estiver pronto, pressione Enter para começar."

];

function tutorial() {

    state = STATE.TUTORIAL;

    const text =
        tutorialLines.join(" ");

    speak(
        text,
        true
    );

}


/* =========================================================
   GAME OVER
   ========================================================= */

function gameOver() {

    state = STATE.GAMEOVER;

    if (score > bestScore) {

        bestScore = score;

        localStorage.setItem(
            "cozinheiroBest",
            bestScore
        );

    }

    speak(
        `Tempo esgotado. Seu restaurante faliu. Sua pontuação final foi ${score} pontos. Seu recorde é ${bestScore} pontos. Pressione Enter para recomeçar ou Escape para voltar ao menu.`,
        true
    );

}


/* ---------- RECOMEÇAR ---------- */

function restartGame() {

    score = 0;

    timeLeft = 180;

    orderIndex = 0;

    currentOrder = null;

    selectedIngredients = [];

    event = null;

    /*
       restaura estoque
    */

    Object.assign(
        stock,
        {
            pao: 8,
            carne: 6,
            queijo: 4,
            tomate: 7,
            alface: 5,
            molho: 4,
            cebola: 3,
            cogumelo: 3,
            ovo: 3,
            especial: 1
        }
    );

    state = STATE.PLAYING;

    speak(
        "Novo jogo iniciado. Você tem três minutos. Pontuação zero.",
        true
    );

    setTimeout(() => {

        newOrder();

    }, 1500);

}


/* =========================================================
   TECLADO
   ========================================================= */

document.addEventListener("keydown", (e) => {

    /*
       evita comportamento padrão
       de algumas teclas
    */

    if (
        [
            " ",
            "ArrowUp",
            "ArrowDown",
            "Enter",
            "Backspace"
        ].includes(e.key)
    ) {

        e.preventDefault();

    }


    /* ---------- TUTORIAL ---------- */

    if (state === STATE.TUTORIAL) {

        if (e.key === "Backspace") {

            tutorial();

            return;

        }

        if (e.key === "Enter") {

            startGame();

            return;

        }

        return;

    }


    /* ---------- GAME OVER ---------- */

    if (state === STATE.GAMEOVER) {

        if (e.key === "Enter") {

            restartGame();

            return;

        }

        if (e.key === "Escape") {

            location.reload();

            return;

        }

        return;

    }


    /* ---------- BACKSPACE ---------- */

    if (e.key === "Backspace") {

        removeLastIngredient();

        return;

    }


    /* ---------- EVENTO ---------- */

    if (state === STATE.EVENT) {

        if (e.key.toLowerCase() === "q") {

            openRatOptions();

            return;

        }

        if (e.key === "1") {

            scareRat();

            return;

        }

        if (e.key === "2") {

            ignoreRat();

            return;

        }

        if (e.key === "3") {

            callManager();

            return;

        }

        return;

    }


    /* ---------- Q ---------- */

    if (e.key.toLowerCase() === "q") {

        if (event) {

            openRatOptions();

        }

        return;

    }


    /* ---------- E ---------- */

    if (e.key.toLowerCase() === "e") {

        startOrder();

        return;

    }


    /* ---------- ENTER ---------- */

    if (e.key === "Enter") {

        if (
            currentOrder &&
            currentOrder.prepared
        ) {

            deliverOrder();

        } else {

            prepareOrder();

        }

        return;

    }


    /* ---------- INGREDIENTES ---------- */

    if (ingredients[e.key]) {

        chooseIngredient(e.key);

        return;

    }

});


/* ---------- BOTÃO INICIAL ---------- */

document.getElementById("startButton")
.addEventListener("click", () => {

    startGame();

});


/* =========================================================
   INICIAR
   ========================================================= */

function startGame() {

    if (gameStarted) return;

    gameStarted = true;

    document
        .getElementById("startOverlay")
        .classList.add("hidden");

    tutorial();

}


/* =========================================================
   TEMPO
   ========================================================= */

function updateTime(delta) {

    if (state !== STATE.PLAYING) return;

    timeLeft -= delta;

    if (timeLeft <= 0) {

        timeLeft = 0;

        gameOver();

    }

}


/* ---------- FORMATAR TEMPO ---------- */

function formatTime(seconds) {

    seconds = Math.ceil(seconds);

    const minutes =
        Math.floor(seconds / 60);

    const secs =
        seconds % 60;

    return `${minutes}:${String(secs).padStart(2, "0")}`;

}


/* =========================================================
   EVENTOS ALEATÓRIOS
   ========================================================= */

let eventTimer = 0;

function randomEvents(delta) {

    if (state !== STATE.PLAYING) return;

    eventTimer += delta;

    /*
       primeiro evento depois de aproximadamente
       20 segundos.
    */

    if (
        eventTimer > 20 &&
        Math.random() < 0.0015
    ) {

        eventTimer = 0;

        triggerRat();

    }

}


/* =========================================================
   DESENHO
   ========================================================= */

function draw() {

    drawKitchen();

    drawUI();

    drawRat();

    drawEventUI();

    if (state === STATE.GAMEOVER) {

        drawGameOver();

    }

}


/* ---------- GAME OVER VISUAL ---------- */

function drawGameOver() {

    rect(
        0,
        0,
        W,
        H,
        "rgba(0,0,0,.90)"
    );

    pixelText(
        "💸 FALÊNCIA!",
        320,
        160,
        50,
        "#ef4444"
    );

    pixelText(
        `Pontuação final: ${score}`,
        310,
        220,
        25
    );

    pixelText(
        `Recorde: ${bestScore}`,
        340,
        260,
        22,
        "#facc15"
    );

    pixelText(
        "[ENTER] RECOMEÇAR",
        330,
        330,
        24,
        "#86efac"
    );

    pixelText(
        "[ESC] MENU PRINCIPAL",
        300,
        370,
        22,
        "#93c5fd"
    );

}


/* =========================================================
   LOOP PRINCIPAL
   ========================================================= */

function gameLoop(now) {

    const delta =
        (now - lastTime) / 1000;

    lastTime = now;

    updateTime(delta);

    randomEvents(delta);

    draw();

    requestAnimationFrame(gameLoop);

}

requestAnimationFrame(gameLoop);


/* =========================================================
   INÍCIO
   ========================================================= */

draw();

</script>

</body>
</html>
