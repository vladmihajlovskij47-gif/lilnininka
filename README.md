<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Для моей Лил Нинички ❤️</title>
    <style>
        :root { --skin: #ffdbac; --hair-g: #2c1b10; --hair-b: #4a3728; }
        body, html { margin: 0; padding: 0; overflow: hidden; background: #000; font-family: 'Verdana', sans-serif; color: white; }

        /* ЭКРАН 1: ВЕЧЕРНИЙ ГОРОД И ПЛАНЕТА */
        #intro {
            position: absolute; width: 100%; height: 100%; z-index: 1000;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            background: #050510; transition: 2s;
        }
        .planet-draw {
            width: 200px; height: 200px; border-radius: 50%; cursor: pointer;
            background: radial-gradient(circle at 30% 30%, #4facfe, #001220);
            box-shadow: 0 0 50px #4facfe; position: relative;
        }
        .planet-draw::after { content: "☁️"; position: absolute; top: 40%; left: 20%; opacity: 0.2; font-size: 40px; }

        /* ЭКРАН 2: МУЛЬТЯШНЫЙ МИР */
        #world { position: absolute; width: 100%; height: 100%; display: none; opacity: 0; background: #87CEEB; transition: 1.5s; overflow: hidden; }
        
        .skyline { position: absolute; bottom: 100px; width: 100%; height: 300px; display: flex; align-items: flex-end; justify-content: space-around; opacity: 0.3; }
        .building { width: 45px; background: #000; position: relative; }
        .win { width: 6px; height: 6px; background: #ffd700; position: absolute; }

        .massa-store { position: absolute; bottom: 100px; left: 50%; transform: translateX(-50%); width: 500px; height: 300px; background: #333; border: 5px solid #111; z-index: 2; }
        .massa-sign { width: 100%; text-align: center; color: #fff; font-size: 60px; font-weight: 900; margin-top: 15px; letter-spacing: 10px; }
        
        .lantern { position: absolute; bottom: 100px; width: 8px; height: 220px; background: #222; z-index: 10; }
        .lantern::after { content: ""; position: absolute; top: -10px; left: -16px; width: 40px; height: 20px; background: #ffdb58; border-radius: 20px; box-shadow: 0 0 30px #ffdb58; }
        
        .road { position: absolute; bottom: 0; width: 100%; height: 100px; background: #333; border-top: 5px solid #222; z-index: 5; transition: 3s; }

        /* ПЕРСОНАЖИ */
        .actor { position: absolute; bottom: 105px; z-index: 100; transition: 1.5s linear; display: flex; flex-direction: column; align-items: center; }
        .head { width: 40px; height: 42px; background: var(--skin); border-radius: 50%; position: relative; }
        .hair-g { position: absolute; width: 50px; height: 75px; background: var(--hair-g); border-radius: 15px; top: -5px; z-index: -1; }
        .pants-g { position: absolute; top: 50px; width: 52px; height: 70px; background: #000; left: -6px; border-radius: 5px; }
        .fur-slipper { position: absolute; bottom: -82px; width: 30px; height: 14px; background: #000; border-top: 6px solid #fff; border-radius: 8px; }

        .bag-b { position: absolute; width: 28px; height: 28px; background: #5d4037; border: 2px solid #000; left: -12px; top: 12px; transform: rotate(-10deg); }
        .socks-b { position: absolute; bottom: -85px; width: 10px; height: 40px; background: #fff; border-bottom: 5px solid green; left: 1px; }

        /* МЫШКА */
        #bat { position: absolute; width: 60px; height: 40px; display: none; z-index: 2000; transition: 4s ease-out; }
        .wing { position: absolute; width: 40px; height: 30px; background: #000; clip-path: polygon(0 20%, 100% 0, 80% 100%, 0 80%); animation: flap 0.1s infinite alternate; }

        #credits { position: absolute; top: 100%; width: 100%; text-align: center; z-index: 4000; transition: 18s linear; font-size: 22px; line-height: 2.2; background: rgba(0,0,0,0.9); padding: 50px 0; }

        @keyframes flap { from { transform: rotate(20deg); } to { transform: rotate(-40deg); } }
        @keyframes walk { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
        .walking { animation: walk 0.5s infinite; }
    </style>
</head>
<body>

<div id="intro">
    <div id="bg-city" style="position:absolute; width:100%; height:100%; opacity:0.1;"></div>
    <div class="planet-draw" onclick="startStory()"></div>
    <p style="margin-top:20px; color:#4facfe;">КЛИКНИ НА ПЛАНЕТУ</p>
</div>

<div id="world">
    <div class="skyline" id="skyline"></div>
    <div class="massa-store"><div class="massa-sign">MASSA</div></div>
    <div class="lantern" style="left: 15%;"></div><div class="lantern" style="right: 15%;"></div>
    <div class="road" id="road"></div>

    <!-- Она -->
    <div class="actor" id="girl" style="left: -150px;">
        <div class="head"><div class="hair-g"></div><div id="eg" style="text-align:center; padding-top:14px;">👀</div></div>
        <div style="width:40px; height:55px; background:#000; position:relative;"><div class="pants-g"></div><div class="fur-slipper" style="left:0;"></div><div class="fur-slipper" style="right:0;"></div></div>
    </div>

    <!-- Ты -->
    <div class="actor" id="boy" style="right: -150px;">
        <div class="head"><div style="position:absolute; width:40px; height:10px; background:var(--hair-b); top:-5px; border-radius:5px;"></div><div id="eb" style="text-align:center; padding-top:14px;">👀</div></div>
        <div style="width:40px; height:55px; background:#fff; position:relative;"><div class="bag-b"></div><div style="position:absolute; top:55px; width:40px; height:32px; background:#222;"></div><div class="socks-b" style="left:4px;"></div><div class="socks-b" style="right:4px;"></div></div>
    </div>

    <div id="bat"><div class="wing" style="left:-35px; transform:scaleX(-1);"></div><div class="wing" style="right:-35px;"></div><div style="width:25px; height:25px; background:#000; border-radius:50%; margin:0 auto;"></div></div>
</div>

<div id="credits">
    <h1 style="color: #ff4d4d; font-size: 36px;">ПОЛГОДИКА ВМЕСТЕ</h1>
    <p>В главных ролях: моя мышка летучая — <b>Лил Ниничка</b> ❤️</p>
    <p>В ролях: <b>Владик</b></p>
    <br>
    <p>Я тебя люблю очень сильно!</p>
    <p>И это уже наши пол годика!</p>
    <p>Ты у меня самая лучшая во всем мире!</p>
    <br><p><b>КОНЕЦ</b></p>
</div>

<script>
    // Рисуем вечерний город сзади
    const sky = document.getElementById('skyline');
    for(let i=0; i<15; i++) {
        let b = document.createElement('div'); b.className = 'building';
        b.style.height = (100 + Math.random()*200) + 'px';
        for(let j=0; j<6; j++) {
            let w = document.createElement('div'); w.className = 'win';
            w.style.top = (20 + j*20) + 'px'; w.style.left = (5 + Math.random()*25) + 'px';
            b.appendChild(w);
        }
        sky.appendChild(b);
    }

    function startStory() {
        document.getElementById('intro').style.transform = "scale(5)";
        document.getElementById('intro').style.opacity = "0";
        setTimeout(() => {
            document.getElementById('intro').style.display = "none";
            const w = document.getElementById('world');
            w.style.display = "block"; setTimeout(() => w.style.opacity = 1, 50);
            animateAction();
        }, 1000);
    }

    function animateAction() {
        const girl = document.getElementById('girl'), boy = document.getElementById('boy');
        // Лето (Идут)
        girl.classList.add('walking'); boy.classList.add('walking');
        setTimeout(() => { girl.style.left = "calc(50% - 90px)"; boy.style.right = "calc(50% - 90px)"; }, 500);

        // Столкновение
        setTimeout(() => {
            girl.classList.remove('walking'); boy.classList.remove('walking');
            girl.style.transform = "translateY(40px)"; boy.style.transform = "translateY(40px)";
        }, 2200);

        // Встают и Любовь
        setTimeout(() => {
            girl.style.transform = "translateY(0)"; boy.style.transform = "translateY(0)";
            document.getElementById('eg').innerHTML = document.getElementById('eb').innerHTML = "❤️";
            nextSeasons();
        }, 5000);
    }

    function nextSeasons() {
        const w = document.getElementById('world'), r = document.getElementById('road');
        setTimeout(() => { w.style.background = "#d2691e"; spawnE('🍂'); }, 1500); // Осень
        setTimeout(() => { 
            w.style.background = "#e3f2fd"; r.style.background = "#fff"; spawnE('❄️'); // Зима: снег на дороге
        }, 6000);
        setTimeout(() => { 
            w.style.background = "#c8e6c9"; r.style.background = "#333"; spawnE('🌸'); // Весна
            setTimeout(batFinal, 4000);
        }, 11000);
    }

    function batFinal() {
        const girl = document.getElementById('girl'), boy = document.getElementById('boy'), bat = document.getElementById('bat');
        bat.style.left = girl.offsetLeft + "px"; bat.style.top = girl.offsetTop + "px";
        girl.style.opacity = 0; bat.style.display = "block";

        setTimeout(() => {
            bat.style.left = "90%"; bat.style.top = "15%"; // Мышка улетает
            setTimeout(() => {
                boy.classList.add('walking');
                boy.style.transition = "4s linear"; boy.style.right = "5%"; // Ты бежишь
                setTimeout(() => {
                    boy.classList.remove('walking');
                    bat.style.opacity = 0; girl.style.left = "90%"; girl.style.opacity = 1;
                    // Поцелуй
                    girl.style.transform = "translateX(-15px)"; boy.style.transform = "translateX(15px)";
                    setTimeout(() => { document.getElementById('credits').style.top = "-1800px"; }, 2000);
                }, 4200);
            }, 1000);
        }, 500);
    }

    function spawnE(sym) {
        let t = setInterval(() => {
            const e = document.createElement('div'); e.innerHTML = sym; e.style.position = "absolute";
            e.style.left = Math.random()*100+"vw"; e.style.top = "-30px"; e.style.fontSize = "30px"; e.style.transition = "6s linear";
            document.getElementById('world').appendChild(e);
            setTimeout(() => e.style.top = "110vh", 100); setTimeout(() => e.remove(), 5500);
        }, 300);
        setTimeout(() => clearInterval(t), 4000);
    }
</script>
</body>
</html>
