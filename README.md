<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Bir Mesajım Var</title>

    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: radial-gradient(circle, #fff5f5 0%, #fed7e2 100%);
            font-family: 'Times New Roman', Times, serif;
            overflow: hidden;
        }

        .container {
            text-align: center;
            padding: 50px;
            background: rgba(255, 255, 255, 0.92);
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
            max-width: 550px;
            position: relative;
            z-index: 2;
            border: 1px solid #fab1a0;
        }

        h1 {
            color: #d63031;
            font-style: italic;
            margin-bottom: 20px;
        }

        .text-content {
            font-size: 1.2rem;
            line-height: 1.8;
            margin-bottom: 40px;
            font-style: italic;
            min-height: 120px;
        }

        .heart-icon {
            font-size: 40px;
            color: #d63031;
            margin-bottom: 10px;
            display: block;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 30px;
            height: 60px;
            align-items: center;
        }

        button {
            padding: 15px 40px;
            font-size: 1.1rem;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            transition: transform 0.2s ease;
            font-weight: bold;
        }

        #yesBtn {
            background-color: #d63031;
            color: white;
            box-shadow: 0 4px 15px rgba(214, 48, 49, 0.3);
        }

        #yesBtn:hover {
            transform: scale(1.1);
        }

        #noBtn {
            background-color: #636e72;
            color: white;
            position: relative;
            transition: top 0.2s ease, left 0.2s ease;
        }

        .heart {
            position: fixed;
            bottom: -20px;
            font-size: 18px;
            animation: floatUp 6s linear forwards;
            opacity: 0.7;
            z-index: 0;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) scale(1); opacity: 0.7; }
            100% { transform: translateY(-110vh) scale(1.5); opacity: 0; }
        }

        #music-status {
            position: fixed;
            bottom: 10px;
            right: 10px;
            font-size: 0.8rem;
            color: #b2bec3;
        }
    </style>
</head>

<body onclick="playMusic()">

<iframe id="youtubePlayer" width="0" height="0"
        src="https://www.youtube.com/embed/S6z70vH5iI8?enablejsapi=1"
        frameborder="0" allow="autoplay"></iframe>

<div class="container">
    <span class="heart-icon">❦</span>
    <h1>Sana Bir Notum Var...</h1>

    <div class="text-content" id="text">
    </div>

    <div class="buttons">
        <button id="yesBtn" onclick="celebrate()">EVET!</button>
        <button id="noBtn" onmouseover="moveButton()" ontouchstart="moveButton()">YOOOOOK</button>
    </div>
</div>

<div id="music-status">Sayfaya dokunarak müziği başlatabilirsin...</div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>

<script>
let musicStarted = false;

// Typing effect
const message = `"Seninle geçirdiğim her an, hayatımın en güzel hikayesine dönüşüyor. Bu hikayeyi seninle yazmak istiyorum. Yanımda olduğun her an daha anlamlı..."

Benim için çok özelsin. Birlikte güzel bir "biz" olalım.`;

let i = 0;
function typeWriter() {
    if (i < message.length) {
        document.getElementById("text").innerHTML += message.charAt(i);
        i++;
        setTimeout(typeWriter, 25);
    }
}

function playMusic() {
    if (!musicStarted) {
        document.getElementById('youtubePlayer').src = 
        "https://www.youtube.com/embed/S6z70vH5iI8?autoplay=1&enablejsapi=1";
        musicStarted = true;
        document.getElementById('music-status').innerText = "🎵 Tanju Okan - Kadınım çalıyor...";
    }
}

function celebrate() {
    confetti({ particleCount: 250, spread: 120, origin: { y: 0.6 } });

    document.getElementById("text").innerHTML =
        "<h2>Seni Çok Seviyorum ❤️</h2><p>Bu hikaye artık bizim.</p>";

    document.querySelector('.buttons').style.display = 'none';
}

function moveButton() {
    const btn = document.getElementById('noBtn');
    const margin = 20;
    const maxX = window.innerWidth - btn.offsetWidth - margin;
    const maxY = window.innerHeight - btn.offsetHeight - margin;

    const x = Math.random() * maxX;
    const y = Math.random() * maxY;

    btn.style.position = 'fixed';
    btn.style.left = x + 'px';
    btn.style.top = y + 'px';
}

function createHearts() {
    const heart = document.createElement('div');
    heart.className = 'heart';
    heart.innerText = '❤️';
    heart.style.left = Math.random() * 100 + 'vw';
    heart.style.animationDuration = (4 + Math.random() * 3) + 's';
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 7000);
}

setInterval(createHearts, 900);

// start typing on load
window.onload = typeWriter;
</script>

</body>
</html>
