# novostimurmanska.xyz
новости великой мурманской депржави 
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Новости Мурманска 🐄 — Интерактив</title>
  <style>
    :root{
      --bg-0:#071424; --bg-1:#0f2b3a; --panel:#0f2430; --accent:#ffd166; --muted:#9fb3bf; --cow:#7ee1a8; --pig:#ff8fa3;
      --glass: rgba(255,255,255,0.03);
      --max:1200px; --radius:12px;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,Segoe UI,system-ui,Arial;color:#e6f0f2;background:linear-gradient(180deg,var(--bg-0),var(--bg-1));-webkit-font-smoothing:antialiased}
    header{display:flex;align-items:center;justify-content:space-between;padding:18px 24px;background:linear-gradient(90deg,#0b2b3a,#07202a);box-shadow:0 6px 20px rgba(2,6,23,0.6)}
    .brand{display:flex;align-items:center;gap:14px}
    .logo{width:56px;height:56px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#ffb86b);display:flex;align-items:center;justify-content:center;font-weight:800;color:#082;box-shadow:0 6px 20px rgba(0,0,0,0.3)}
    h1{margin:0;font-size:18px}
    .tagline{color:var(--muted);font-size:13px}
    nav{display:flex;gap:10px;align-items:center}
    .nav-btn{background:var(--glass);border:1px solid rgba(255,255,255,0.04);padding:8px 12px;border-radius:10px;color:var(--muted);cursor:pointer}
    .nav-btn.active{background:linear-gradient(90deg,rgba(255,209,102,0.12),rgba(126,225,168,0.06));color:var(--accent);border-color:rgba(255,209,102,0.12)}
    main{max-width:var(--max);margin:22px auto;padding:18px;display:grid;grid-template-columns:1fr 360px;gap:20px}

    /* left */
    .panel{background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);padding:16px;border-radius:12px;border:1px solid rgba(255,255,255,0.03);}
    .hero{display:flex;gap:16px;align-items:center}
    .hero .lead{flex:1}
    .lead h2{margin:0 0 6px 0}
    .muted{color:var(--muted);font-size:13px}

    /* map */
    #mapWrap{height:520px;border-radius:12px;overflow:hidden;background:linear-gradient(180deg,#06202a,#0a2e3b);display:flex;flex-direction:column}
    .mapControls{display:flex;gap:8px;padding:10px;align-items:center}
    .legend{display:flex;gap:10px;align-items:center;margin-left:auto;margin-right:8px}
    .legend span{display:flex;gap:8px;align-items:center;font-size:13px}
    .swatch{width:18px;height:12px;border-radius:3px}
    #mapCanvas{flex:1;width:100%;display:block}
    #progressChart{height:140px;width:100%;background:linear-gradient(180deg,rgba(255,255,255,0.01),transparent);}

    /* right */
    aside .widget{margin-bottom:14px}
    .widget h3{margin:0 0 8px 0}
    .list{display:flex;flex-direction:column;gap:8px}
    .newsItem{background:var(--panel);padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.02)}

    /* games */
    #gamesWrap{display:flex;flex-direction:column;gap:12px}
    .gameCanvas{border-radius:10px;background:#081824;width:100%;height:320px}
    .controls{display:flex;gap:8px}

    footer{text-align:center;padding:18px;color:var(--muted)}

    @media(max-width:980px){main{grid-template-columns:1fr} #mapWrap{height:420px}}

    /* small utils */
    .btn{background:var(--accent);color:#032;border:0;padding:8px 12px;border-radius:8px;cursor:pointer;font-weight:700}
    a.tg{background:#2a9d8f;color:#021;padding:8px 12px;border-radius:8px;text-decoration:none;font-weight:700}
  </style>
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo">М</div>
      <div>
        <h1>Новости Мурманска — Все жители — коровы 🐄</h1>
        <div class="tagline">Рофл-издания, юмор и эпопеи коровьего величия</div>
      </div>
    </div>
    <nav>
      <button class="nav-btn active" data-section="news">Новости</button>
      <button class="nav-btn" data-section="war">Боевые действия</button>
      <button class="nav-btn" data-section="games">Мини-игры</button>
      <a class="tg" href="https://t.me/NovostiMyyyrmanska" target="_blank">Наш Telegram</a>
    </nav>
  </header>

  <main>
    <div>
      <div class="panel" id="newsPanel">
        <div class="hero">
          <div class="lead">
            <h2>Главные новости (только шутки — все жители коровы)</h2>
            <div class="muted">Подмигнуть нельзя — коровы следят</div>
          </div>
          <div style="text-align:right">
            <button id="refresh" class="btn">Обновить (рандом)</button>
          </div>
        </div>

        <div id="newsList" style="margin-top:14px" class="list">
          <!-- заполнится скриптом -->
        </div>
      </div>

      <!-- WAR section -->
      <div class="panel" id="warPanel" style="margin-top:18px;display:none">
        <h3 style="margin-top:0">Боевые действия — Карта захватов</h3>
        <div id="mapWrap">
          <div class="mapControls">
            <div class="muted">Сценарий: Рофл-война коров против свиней</div>
            <div class="legend">
              <span><i class="swatch" style="background:var(--cow)"></i> Коровы</span>
              <span><i class="swatch" style="background:var(--pig)"></i> Свинки</span>
              <span><i class="swatch" style="background:rgba(255,255,255,0.08)"></i> Нейтрально</span>
            </div>
          </div>
          <canvas id="mapCanvas"></canvas>
          <canvas id="progressChart"></canvas>
        </div>
        <div style="display:flex;gap:8px;margin-top:10px;align-items:center">
          <button id="simToggle" class="btn">Пауза симуляции</button>
          <div class="muted">Симуляция продвижения за последние 24 часа (обновляется)</div>
        </div>
      </div>

      <!-- GAMES section -->
      <div class="panel" id="gamesPanel" style="margin-top:18px;display:none">
        <h3 style="margin-top:0">Мини-игры — Турнир коров</h3>
        <div id="gamesWrap">
          <div style="display:flex;gap:8px;align-items:center;margin-bottom:8px">
            <button class="nav-btn" data-game="catch">Поймай ведро</button>
            <button class="nav-btn" data-game="dodge">Уклоняйся от свинок</button>
            <button id="resetGame" class="btn">Сброс</button>
            <div class="muted" style="margin-left:auto">Лучший результат сохранится локально</div>
          </div>

          <canvas id="gameCanvas" class="gameCanvas"></canvas>
          <div style="display:flex;gap:10px;margin-top:8px;align-items:center">
            <div class="muted">Очки: <strong id="gameScore">0</strong></div>
            <div class="muted">Время: <strong id="gameTime">0</strong>с</div>
            <button id="startGameBtn" class="btn">Старт</button>
          </div>
        </div>
      </div>

    </div>

    <aside>
      <div class="widget panel">
        <h3>Популярные рофлы</h3>
        <div id="sideNews" class="list">
          <!-- side news -->
        </div>
      </div>

      <div class="widget panel">
        <h3>Статистика фракций</h3>
        <div class="muted">Коровы контролируют <strong id="cowPercent">0%</strong>, свинки — <strong id="pigPercent">0%</strong></div>
      </div>

      <div class="widget panel">
        <h3>О проекте</h3>
        <div class="muted">Сайт-рифма и сатира. Все события выдуманы. Все жители — коровы. Не воспринимать всерьёз.</div>
      </div>
    </aside>
  </main>

  <footer>© 2025 Новости Мурманска — Рофл-канал · <a href="https://t.me/NovostiMyyyrmanska" target="_blank" style="color:var(--accent)">Наш Telegram</a></footer>

  <script>
    // --- Utilities ---
    const rand = (a,b)=> Math.floor(Math.random()*(b-a+1))+a;

    // --- News (satire) ---
    const sampleNews = [
      {t:'Коровы объявили забастовку молока — требуют поднять цену на сено',d:'Сегодня утром стада встали на пастбище и потребовали...'},
      {t:'Мурманская корова стала депутатом — она обещает больше лугов',d:'Программа: больше тени, меньше доения.'},
      {t:'Пингвины уступили коровам тротуар — шум на набережной',d:'Коровы заняли лучшие места для селфи.'},
      {t:'Открытие памятника лучшему вёдру — массовый марш коров',d:'Ведро благословлено.'}
    ];

    function renderNews(){
      const list = document.getElementById('newsList'); list.innerHTML='';
      for(let i=0;i<4;i++){
        const it = sampleNews[rand(0,sampleNews.length-1)];
        const el = document.createElement('div'); el.className='newsItem';
        el.innerHTML = `<strong>🐄 ${it.t}</strong><div class="muted">${it.d}</div>`;
        list.appendChild(el);
      }
      // side
      const side = document.getElementById('sideNews'); side.innerHTML='';
      for(let i=0;i<3;i++){ const it=sampleNews[rand(0,sampleNews.length-1)]; const s=document.createElement('div'); s.className='newsItem'; s.innerHTML=`<strong>🐮 ${it.t}</strong><div class=\"muted\">${it.d}</div>`; side.appendChild(s);} 
    }

    document.getElementById('refresh').addEventListener('click',renderNews);
    renderNews();

    // --- Navigation ---
    document.querySelectorAll('.nav-btn[data-section]').forEach(btn=>btn.addEventListener('click',e=>{
      document.querySelectorAll('.nav-btn[data-section]').forEach(b=>b.classList.remove('active'));
      btn.classList.add('active');
      const sec = btn.dataset.section;
      document.getElementById('newsPanel').style.display = sec==='news'? 'block':'none';
      document.getElementById('warPanel').style.display = sec==='war'? 'block':'none';
      document.getElementById('gamesPanel').style.display = sec==='games'? 'block':'none';
    }));

    // --- WAR: Map simulation ---
    const mapCanvas = document.getElementById('mapCanvas'); const mapCtx = mapCanvas.getContext('2d');
    const chart = document.getElementById('progressChart'); const chartCtx = chart.getContext('2d');
    let simRunning = true;
    const cols = 12, rows = 8; // grid for territories
    let territories = [];

    function resizeMap(){
      mapCanvas.width = mapCanvas.clientWidth; mapCanvas.height = mapCanvas.clientHeight - 140; // leave room for chart canvas
      chart.width = chart.clientWidth; chart.height = 140;
      drawMap(); drawChart(); updateStats();
    }
    window.addEventListener('resize',resizeMap);

    // init territories grid
    function initTerritories(){
      territories = [];
      for(let r=0;r<rows;r++){
        for(let c=0;c<cols;c++){
          const owner = Math.random()>0.5? 'cow':'pig';
          territories.push({r,c,owner,strength:rand(10,90)});
        }
      }
    }
    initTerritories();

    function drawMap(){
      const w = mapCanvas.width; const h = mapCanvas.height; mapCtx.clearRect(0,0,w,h);
      const cellW = w/cols, cellH = h/rows;
      // background grid texture
      mapCtx.fillStyle = 'rgba(255,255,255,0.02)'; mapCtx.fillRect(0,0,w,h);
      territories.forEach(t=>{
        const x = t.c*cellW, y = t.r*cellH;
        mapCtx.fillStyle = t.owner==='cow' ? 'rgba(126,225,168,0.95)' : 'rgba(255,143,163,0.95)';
        mapCtx.fillRect(x+2,y+2,cellW-4,cellH-4);
        // strength overlay
        mapCtx.fillStyle = 'rgba(0,0,0,0.12)'; mapCtx.fillRect(x+2,y+cellH-18,cellW-4,12);
        mapCtx.fillStyle = 'rgba(255,255,255,0.9)'; mapCtx.font = '10px Inter'; mapCtx.fillText(t.strength+'%', x+6, y+cellH-8);
      });
      // labels
      mapCtx.fillStyle='rgba(255,255,255,0.06)'; mapCtx.font='14px Inter'; mapCtx.fillText('Интерактивная карта — рыцари-пастухи и их коровы',8,16);
    }

    // simulate front movement: record cow-control percent per hour for last 24h
    let timeline = Array.from({length:24},()=>rand(30,70));
    function stepSimulation(){
      if(!simRunning) return;
      // random flips
      for(let i=0;i<rand(1,3);i++){
        const idx = rand(0,territories.length-1); territories[idx].owner = Math.random()>0.5? 'cow':'pig'; territories[idx].strength = Math.max(5,Math.min(99,territories[idx].strength + rand(-8,8)));
      }
      // compute cow percent
      const cowCount = territories.filter(t=>t.owner==='cow').length; const cowPercent = Math.round(cowCount/territories.length*100);
      timeline.shift(); timeline.push(cowPercent);
      drawMap(); drawChart(); updateStats();
    }
    setInterval(stepSimulation, 2500);

    document.getElementById('simToggle').addEventListener('click',()=>{
      simRunning = !simRunning; document.getElementById('simToggle').textContent = simRunning? 'Пауза симуляции' : 'Запустить симуляцию';
    });

    function drawChart(){
      const w = chart.width, h = chart.height; chartCtx.clearRect(0,0,w,h);
      // background
      chartCtx.fillStyle='rgba(255,255,255,0.02)'; chartCtx.fillRect(0,0,w,h);
      // grid
      chartCtx.strokeStyle='rgba(255,255,255,0.04)'; chartCtx.lineWidth=1;
      for(let i=0;i<4;i++){ chartCtx.beginPath(); chartCtx.moveTo(0,h/4*i); chartCtx.lineTo(w,h/4*i); chartCtx.stroke(); }
      // line
      chartCtx.beginPath(); const step = w/(timeline.length-1);
      timeline.forEach((v,i)=>{
        const x = i*step; const y = h - (v/100)*h;
        if(i===0) chartCtx.moveTo(x,y); else chartCtx.lineTo(x,y);
      });
      chartCtx.strokeStyle='rgba(126,225,168,0.95)'; chartCtx.lineWidth=3; chartCtx.stroke();
      // fill
      chartCtx.lineTo(w,h); chartCtx.lineTo(0,h); chartCtx.closePath(); chartCtx.fillStyle='rgba(126,225,168,0.06)'; chartCtx.fill();
    }

    function updateStats(){
      const cowCount = territories.filter(t=>t.owner==='cow').length; const pigCount = territories.length - cowCount;
      document.getElementById('cowPercent').textContent = Math.round(cowCount/territories.length*100) + '%';
      document.getElementById('pigPercent').textContent = Math.round(pigCount/territories.length*100) + '%';
    }

    // click on map to flip territory
    mapCanvas.addEventListener('click',(e)=>{
      const rect = mapCanvas.getBoundingClientRect(); const x = e.clientX-rect.left; const y = e.clientY-rect.top;
      const cellW = mapCanvas.width/cols, cellH = mapCanvas.height/rows;
      const c = Math.floor(x/cellW), r = Math.floor(y/cellH);
      const idx = territories.findIndex(t=>t.r===r && t.c===c);
      if(idx>=0){ territories[idx].owner = territories[idx].owner==='cow'? 'pig':'cow'; territories[idx].strength = rand(20,90); drawMap(); drawChart(); updateStats(); }
    });

    // start sizes
    setTimeout(resizeMap,50);

    // --- GAMES: improved two mini-games on single canvas ---
    const gameCanvas = document.getElementById('gameCanvas'); const gctx = gameCanvas.getContext('2d');
    let gameState = {mode:'catch',running:false,score:0,time:0,player:{x:150,y:260,w:60,h:40},objects:[],best:0,interval:null,ts:null};

    function resizeGame(){ gameCanvas.width = gameCanvas.clientWidth; gameCanvas.height = gameCanvas.clientHeight; drawGame(); }
    window.addEventListener('resize',resizeGame); setTimeout(resizeGame,50);

    document.querySelectorAll('[data-game]').forEach(b=>b.addEventListener('click',e=>{ document.querySelectorAll('[data-game]').forEach(x=>x.classList.remove('active')); e.currentTarget.classList.add('active'); gameState.mode=e.currentTarget.dataset.game; resetGame(); }));
    document.getElementById('startGameBtn').addEventListener('click',()=>{ if(!gameState.running) startGameLoop(); else stopGameLoop(); });
    document.getElementById('resetGame').addEventListener('click',resetGame);

    function resetGame(){ stopGameLoop(); gameState.score=0; gameState.time=0; gameState.objects=[]; gameState.player.x = gameCanvas.width/2 - gameState.player.w/2; gameState.best = Math.max(gameState.best, parseInt(localStorage.getItem('best')||0)); document.getElementById('gameScore').textContent=0; document.getElementById('gameTime').textContent=0; drawGame(); }

    function startGameLoop(){ gameState.running=true; gameState.ts = performance.now(); gameState.interval = requestAnimationFrame(gameLoop); document.getElementById('startGameBtn').textContent='Пауза'; }
    function stopGameLoop(){ gameState.running=false; if(gameState.interval) cancelAnimationFrame(gameState.interval); gameState.interval=null; document.getElementById('startGameBtn').textContent='Старт'; localStorage.setItem('best', gameState.best); }

    function gameLoop(t){ if(!gameState.running) return; const dt = (t - (gameState.lastT||t))/1000; gameState.lastT = t; gameState.time += dt; document.getElementById('gameTime').textContent = Math.floor(gameState.time);
      // spawn
      if(Math.random()<0.02 + Math.min(0.12, gameState.time/60)) spawnObject();
      // update objects
      for(let i=gameState.objects.length-1;i>=0;i--){ const o=gameState.objects[i]; o.y += o.vy*dt; if(o.y>gameCanvas.height+40) gameState.objects.splice(i,1); }
      // collisions
      for(let i=gameState.objects.length-1;i>=0;i--){ const o=gameState.objects[i]; if(collide(gameState.player,o)){ if(gameState.mode==='catch' && o.type==='bucket'){ gameState.score+=1; gameState.objects.splice(i,1);} else { // dodge mode lose
            gameState.score = Math.max(0, gameState.score-1); gameState.objects.splice(i,1); }
      }}
      // update UI
      document.getElementById('gameScore').textContent = gameState.score;
      gameState.best = Math.max(gameState.best, gameState.score);
      drawGame(); gameState.interval = requestAnimationFrame(gameLoop);
    }

    function spawnObject(){ if(gameState.mode==='catch'){ // buckets falling
        const x = Math.random()*(gameCanvas.width-40)+20; gameState.objects.push({x,y:-40,w:40,h:40,vy:80+Math.random()*80,type:'bucket'});
      } else { // dodge: pigs moving horizontally
        const side = Math.random()<0.5?-1:1; const y = Math.random()*(gameCanvas.height-120)+40; const vy=0; const vx = (50+Math.random()*120)*side; const x = side<0?gameCanvas.width+40:-40; gameState.objects.push({x,y,w:48,h:36,vx,vy,type:'pig'});
      }}

    // simple keyboard control
    window.addEventListener('keydown',e=>{ if(e.key==='ArrowLeft') gameState.player.x -= 40; if(e.key==='ArrowRight') gameState.player.x +=40; gameState.player.x = Math.max(0, Math.min(gameCanvas.width-gameState.player.w, gameState.player.x)); drawGame(); });

    function collide(a,b){ return !(a.x+a.w < b.x || a.x > b.x + (b.w||40) || a.y + a.h < b.y || a.y > b.y + (b.h||40)); }

    function drawGame(){ const c = gctx; const w=gameCanvas.width, h=gameCanvas.height; c.clearRect(0,0,w,h);
      // background
      const grad = c.createLinearGradient(0,0,0,h); grad.addColorStop(0,'#052129'); grad.addColorStop(1,'#08323b'); c.fillStyle=grad; c.fillRect(0,0,w,h);
      // player (cow) — stylized
      c.fillStyle='#7ee1a8'; c.fillRect(gameState.player.x, gameState.player.y, gameState.player.w, gameState.player.h); c.fillStyle='#032'; c.fillRect(gameState.player.x+10, gameState.player.y+6, 12, 12);
      // objects
      gameState.objects.forEach(o=>{
        if(o.type==='bucket'){ c.fillStyle='#ffd166'; c.beginPath(); c.arc(o.x+20,o.y+20,18,0,Math.PI*2); c.fill(); c.fillStyle='#663c00'; c.fillRect(o.x+8,o.y+26,24,6);} else { c.fillStyle='#ff8fa3'; c.fillRect(o.x,o.y,o.w,o.h); c.fillStyle='#fff'; c.fillRect(o.x+6,o.y+6,8,6); }
        // update moving pigs
        if(o.vx) o.x += o.vx*(1/60);
      });
      // HUD
      c.fillStyle='rgba(0,0,0,0.2)'; c.fillRect(8,8,160,36); c.fillStyle='#fff'; c.font='14px Inter'; c.fillText('Режим: '+(gameState.mode==='catch'?'Поймай ведро':'Уклоняйся от свинок'),16,30);
    }

    // initial game selection
    document.querySelector('[data-game="catch"]').classList.add('active'); gameState.mode='catch'; resetGame();

    // --- helpers ---
    resizeMap(); resizeGame();
  </script>
</body>
</html>
