<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pse duhet të më pëlqesh? ❤️</title>

<style>
    body {
        margin: 0;
        overflow: hidden;
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #ffb6d9, #ffeef7);
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        text-align: center;
    }

    .container {
        background: rgba(255,255,255,0.95);
        padding: 40px;
        border-radius: 25px;
        max-width: 700px;
        width: 85%;
        box-shadow: 0 8px 20px rgba(0,0,0,0.15);
        transition: 0.5s ease;
    }

    h1 { color: #ff4081; }

    p {
        font-size: 24px;
        min-height: 60px;
    }

    button {
        padding: 12px 28px;
        font-size: 18px;
        border: none;
        border-radius: 12px;
        cursor: pointer;
        margin-top: 15px;
    }

    #yesBtn { background: #4CAF50; color: white; }
    #noBtn { background: #ff5252; color: white; position: relative; }

    #choiceButtons { display: none; }

    .heart {
        position: absolute;
        font-size: 24px;
        animation: float 6s linear infinite;
        pointer-events: none;
    }

    @keyframes float {
        from { transform: translateY(100vh); opacity: 1; }
        to { transform: translateY(-120vh); opacity: 0; }
    }
</style>
</head>

<body>

<!-- 🎵 YouTube API -->
<script src="https://www.youtube.com/iframe_api"></script>

<div id="player" style="display:none;"></div>

<div class="container" id="box">
    <h1 id="title">Pse duhet të më pëlqesh? ❤️</h1>

    <p id="text">Shtyp Start për të filluar...</p>

    <button id="nextBtn" onclick="nextPage()">Start</button>

    <div id="choiceButtons">
        <button id="yesBtn">Po ❤️</button>
        <button id="noBtn">Jo 🙈</button>
    </div>
</div>

<script>
const pages = [
    "Kujdesem sinqerisht për njerëzit që kam afër. ❤️",
    "Di të dëgjoj kur dikush ka nevojë të flasë. 🎧",
    "Mund të të bëj të qeshësh edhe në momente të sikletshme. 😂",
    "I mbështes njerëzit për të cilët më intereson. 🤝",
    "Mbaj mend gjërat e vogla që kanë rëndësi. 🧠",
    "Ndonjëherë jam pak i turpshëm, por gjithmonë kam qëllime të mira. 💬",
    "Kur më pëlqen dikush, tregoj përkushtim të vërtetë. ✨",
    "Jeta bëhet më e bukur kur e ndan me dikë të veçantë. 🎉",
    "Dhe sinqerisht... mënyra më e mirë për të vendosur është të më njohësh më mirë. 😊"
];

let currentPage = -1;
let player;
let musicStarted = false;

function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
        height: '0',
        width: '0',
        videoId: 'pdDud1JYYhw',
        playerVars: {
            autoplay: 0,
            controls: 0,
            loop: 1,
            playlist: 'pdDud1JYYhw',
            playsinline: 1
        }
    });
}

function startMusic() {
    if (musicStarted) return;

    player.playVideo();
    player.setVolume(20); // low background vibe
    musicStarted = true;
}

function lowerMusicGradually() {
    let vol = player.getVolume();

    const fade = setInterval(() => {
        vol -= 2;
        if (vol <= 6) {
            vol = 6;
            clearInterval(fade);
        }
        player.setVolume(vol);
    }, 300);
}

function fade(callback) {
    const box = document.getElementById("box");

    box.style.opacity = 0;
    box.style.transform = "scale(0.95)";

    setTimeout(() => {
        callback();
        box.style.opacity = 1;
        box.style.transform = "scale(1)";
    }, 300);
}

function nextPage() {
    if (!musicStarted) startMusic();

    currentPage++;

    if (currentPage < pages.length) {

        fade(() => {
            document.getElementById("title").textContent =
                `Arsyeja ${currentPage + 1} ❤️`;

            document.getElementById("text").textContent =
                pages[currentPage];

            document.getElementById("nextBtn").textContent = "Tjetra ➜";
        });

    } else {

        lowerMusicGradually();

        fade(() => {
            document.getElementById("title").textContent =
                "Pra... çfarë mendon?";

            document.getElementById("text").textContent =
                "Nëse ndihesh rehat me këtë... a mund të më japësh një mundësi?";

            document.getElementById("nextBtn").style.display = "none";
            document.getElementById("choiceButtons").style.display = "block";
        });
    }
}

// YES
document.getElementById("yesBtn").onclick = () => {
    fade(() => {
        document.getElementById("title").textContent = "Më vjen shumë mirë 😊";
        document.getElementById("text").textContent =
            "Faleminderit që më dhe një mundësi. Do të kujdesem për këtë.";
        document.getElementById("choiceButtons").style.display = "none";
    });
};

// NO (fun dodge button)
document.getElementById("noBtn").addEventListener("mouseover", function() {
    this.style.position = "fixed";
    this.style.left = Math.random() * (window.innerWidth - 100) + "px";
    this.style.top = Math.random() * (window.innerHeight - 60) + "px";
});

// HEARTS
setInterval(() => {
    const heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * window.innerWidth + "px";
    heart.style.fontSize = (20 + Math.random() * 20) + "px";
    document.body.appendChild(heart);

    setTimeout(() => heart.remove(), 6000);
}, 400);

</script>

</body>
</html>
