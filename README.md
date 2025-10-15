# novostimurmanska.xyz
новости великой мурманской депржави 
<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Новости Мурманска — Главная</title>
  <meta name="description" content="Агрегатор локальных новостей Мурманска: события, происшествия, культура, погода и афиша.">
  <link rel="icon" href="data:;base64,iVBORw0KGgo="> <!-- простая пустая иконка -->
  <style>
    :root{
      --bg:#0f1720; --card:#0b1220; --muted:#9aa6b2; --accent:#0ea5a4; --glass: rgba(255,255,255,0.03);
      --max-width:1100px; --radius:12px;
    }
    *{box-sizing:border-box}
    body{font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; margin:0; background:linear-gradient(180deg,#071021 0%, #081425 100%); color:#e6eef3; -webkit-font-smoothing:antialiased}
    .container{max-width:var(--max-width);margin:28px auto;padding:20px}
    header{display:flex;gap:18px;align-items:center;justify-content:space-between}
    .brand{display:flex;gap:14px;align-items:center}
    .logo{width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#2dd4bf);display:flex;align-items:center;justify-content:center;font-weight:700;color:#022;box-shadow:0 6px 18px rgba(14,165,164,0.12)}
    .brand h1{font-size:18px;margin:0}
    .brand p{margin:0;color:var(--muted);font-size:13px}

    nav{display:flex;gap:10px;align-items:center}
    .btn{background:var(--glass);border:1px solid rgba(255,255,255,0.04);padding:8px 12px;border-radius:10px;color:var(--muted);cursor:pointer}
    .btn.primary{background:linear-gradient(90deg, rgba(14,165,164,0.12), rgba(34,197,94,0.06));color:#bff7f2;border:0}

    .search{display:flex;gap:8px;align-items:center;background:rgba(255,255,255,0.02);padding:8px;border-radius:10px;border:1px solid rgba(255,255,255,0.03)}
    .search input{background:transparent;border:0;outline:none;color:inherit;font-size:14px}

    main{display:grid;grid-template-columns:1fr 320px;gap:24px;margin-top:20px}

    .hero{background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);padding:18px;border-radius:14px;border:1px solid rgba(255,255,255,0.03)}
    .hero .big{display:flex;gap:16px}
    .thumb{width:320px;height:180px;border-radius:10px;flex-shrink:0;background-size:cover;background-position:center}
    .hero h2{margin:0 0 6px 0}
    .meta{color:var(--muted);font-size:13px}

    .grid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-top:12px}
    .card{background:var(--card);padding:12px;border-radius:12px;border:1px solid rgba(255,255,255,0.02);display:flex;gap:12px;align-items:flex-start}
    .card .c-thumb{width:120px;height:80px;border-radius:8px;background-size:cover;background-position:center;flex-shrink:0}
    .card h3{margin:0;font-size:15px}
    .card p{margin:6px 0 0 0;color:var(--muted);font-size:13px}

    aside{position:relative}
    .widget{background:rgba(255,255,255,0.02);padding:12px;border-radius:12px;border:1px solid rgba(255,255,255,0.03);margin-bottom:12px}
    .list{display:flex;flex-direction:column;gap:8px}
    .small{display:flex;gap:10px;align-items:center}
    .small .dot{width:46px;height:34px;border-radius:8px;background-size:cover;background-position:center;flex-shrink:0}
    footer{margin-top:26px;color:var(--muted);font-size:13px;text-align:center}

    /* responsive */
    @media (max-width:880px){main{grid-template-columns:1fr} .thumb{width:140px;height:100px} .grid{grid-template-columns:1fr} aside{order:2}}

    /* small utilities */
    .kicker{font-size:12px;color:var(--accent);font-weight:600}
    .muted{color:var(--muted)}
    a{color:inherit;text-decoration:none}
    .tag{background:rgba(14,165,164,0.12);color:var(--accent);padding:4px 8px;border-radius:999px;font-size:12px}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo">М</div>
        <div>
          <h1>Новости Мурманска</h1>
          <p>Локальные новости, события и афиша</p>
        </div>
      </div>

      <nav>
        <div class="search" role="search">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" aria-hidden><path d="M21 21l-4.35-4.35" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" opacity="0.6"></path><circle cx="11" cy="11" r="5" stroke="currentColor" stroke-width="1.5" opacity="0.6"></circle></svg>
          <input id="q" placeholder="Поиск по новостям...">
        </div>
        <button class="btn" id="btn-filter">Фильтры</button>
        <button class="btn primary" id="btn-add">Добавить новость</button>
      </nav>
    </header>

    <main>
      <section>
        <div class="hero" id="hero">
          <!-- hero будет заполнен скриптом -->
        </div>

        <div class="grid" id="list">
          <!-- новости -->
        </div>

        <footer>
          © <span id="year"></span> Новости Мурманска · Разработано для демонстрации
        </footer>
      </section>

      <aside>
        <div class="widget">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
            <strong>Популярное</strong>
            <span class="muted">за 24ч</span>
          </div>
          <div class="list" id="popular">
            <!-- популярное -->
          </div>
        </div>

        <div class="widget">
          <strong>Погода — Мурманск</strong>
          <p class="muted">Сегодня: ясно · Температура: −2°C · Ветер: 6 м/с</p>
        </div>

        <div class="widget">
          <strong>Афиша</strong>
          <ul class="muted" style="margin:8px 0 0 0;padding-left:18px">
            <li>Концерт филармонии — 22 октября</li>
            <li>Фестиваль снежных скульптур — 5 ноября</li>
            <li>Ярмарка локальных ремесленников — 10 ноября</li>
          </ul>
        </div>
      </aside>
    </main>
  </div>

  <template id="card-tpl">
    <article class="card">
      <div class="c-thumb"></div>
      <div>
        <div style="display:flex;gap:8px;align-items:center;margin-bottom:6px"><span class="tag">Категория</span><span class="muted" style="font-size:12px">Дата · Час</span></div>
        <h3></h3>
        <p class="muted"></p>
      </div>
    </article>
  </template>

  <script>
    // Пример локальных данных — в реальном проекте подгружайте через API
    const articles = [
      {id:1,title:'В Мурманске открылся новый музей северного сияния',excerpt:'В городе появился интерактивный музей, посвящённый полярной тематике и северному сиянию.',img:'https://picsum.photos/seed/mur1/800/500',category:'Культура',date:'2025-10-14',views:1280},
      {id:2,title:'Ремонт дорог: какие улицы закроют на следующей неделе',excerpt:'Коммунальные службы начали масштабный ремонт дорог в центральном районе.',img:'https://picsum.photos/seed/mur2/800/500',category:'Город',date:'2025-10-13',views:840},
      {id:3,title:'Молодёжный фестиваль стартапов прошёл в Арктике',excerpt:'Команды представили проекты в сфере экотехнологий и логистики.',img:'https://picsum.photos/seed/mur3/800/500',category:'Экономика',date:'2025-10-12',views:540},
      {id:4,title:'Морской порт готовит новые рейсы в Норвегию',excerpt:'Порт расширяет логистику для ускорения товарооборота между странами.',img:'https://picsum.photos/seed/mur4/800/500',category:'Транспорт',date:'2025-10-10',views:430},
      {id:5,title:'Школьный хор из Мурманска выиграл международный конкурс',excerpt:'Юные музыканты привезли золото и гран-при в вокальной категории.',img:'https://picsum.photos/seed/mur5/800/500',category:'Образование',date:'2025-10-09',views:390}
    ];

    const heroEl = document.getElementById('hero');
    const listEl = document.getElementById('list');
    const popularEl = document.getElementById('popular');
    const tpl = document.getElementById('card-tpl');

    function renderHero(item){
      heroEl.innerHTML = '';
      const div = document.createElement('div'); div.className='big';
      const thumb = document.createElement('div'); thumb.className='thumb'; thumb.style.backgroundImage=`url(${item.img})`;
      const info = document.createElement('div');
      info.innerHTML = `<div class="kicker">Главная</div><h2>${item.title}</h2><div class="meta">${item.date} · ${item.category} · ${item.views} просмотров</div><p class="muted" style="margin-top:10px">${item.excerpt}</p>`;
      div.appendChild(thumb); div.appendChild(info); heroEl.appendChild(div);
    }

    function renderList(items){
      listEl.innerHTML = '';
      items.forEach((it,idx)=>{
        const node = tpl.content.cloneNode(true);
        const root = node.querySelector('.card');
        root.querySelector('.c-thumb').style.backgroundImage = `url(${it.img})`;
        root.querySelector('h3').textContent = it.title;
        root.querySelector('p').textContent = it.excerpt;
        root.querySelector('.tag').textContent = it.category;
        root.querySelector('.muted').textContent = `${it.date} · ${it.views} просмотров`;
        // click -> открытие подробной карточки
        root.addEventListener('click',()=>openArticle(it));
        listEl.appendChild(node);
      });
    }

    function renderPopular(items){
      popularEl.innerHTML = '';
      const sorted = [...items].sort((a,b)=>b.views-a.views).slice(0,4);
      sorted.forEach(it=>{
        const el = document.createElement('div'); el.className='small';
        const d = document.createElement('div'); d.className='dot'; d.style.backgroundImage=`url(${it.img})`;
        const info = document.createElement('div'); info.innerHTML = `<strong style="display:block">${it.title}</strong><span class="muted" style="font-size:12px">${it.date} · ${it.views} просмотров</span>`;
        el.appendChild(d); el.appendChild(info); popularEl.appendChild(el);
      });
    }

    function openArticle(it){
      // простая модалка — заменим hero на полную статью
      heroEl.innerHTML = `<div style="padding:12px"><button class=\"btn\" onclick=\"location.reload()\">← Назад</button><h2 style=\"margin-top:12px\">${it.title}</h2><div class=\"meta\">${it.date} · ${it.category} · ${it.views} просмотров</div><img src=\"${it.img}\" alt=\"\" style=\"width:100%;max-height:420px;object-fit:cover;border-radius:10px;margin-top:12px\"><p class=\"muted\" style=\"margin-top:12px\">${it.excerpt} — Полный текст новости можно загрузить с сервера через API. Здесь показан пример оформления.</p></div>`;
      window.scrollTo({top:0,behavior:'smooth'});
    }

    // Инициализация
    (function(){
      document.getElementById('year').textContent = new Date().getFullYear();
      renderHero(articles[0]);
      renderList(articles.slice(1));
      renderPopular(articles);

      // поиск
      document.getElementById('q').addEventListener('input',e=>{
        const q = e.target.value.trim().toLowerCase();
        if(!q){ renderHero(articles[0]); renderList(articles.slice(1)); return; }
        const res = articles.filter(a=> (a.title+ ' '+ a.excerpt + ' '+ a.category).toLowerCase().includes(q));
        if(res.length) renderHero(res[0]);
        renderList(res.slice(1));
      });

      // добавление новости (локально)
      document.getElementById('btn-add').addEventListener('click',()=>{
        const title = prompt('Заголовок новости:'); if(!title) return;
        const excerpt = prompt('Короткое описание:') || '';
        const category = prompt('Категория (например: Город, Культура):') || 'Город';
        const img = `https://picsum.photos/seed/${Math.random().toString(36).slice(2)}/800/500`;
        const date = new Date().toISOString().slice(0,10);
        const newItem = {id:Date.now(),title,excerpt,img,category,date,views:0};
        articles.unshift(newItem); renderHero(articles[0]); renderList(articles.slice(1)); renderPopular(articles);
      });

      // фильтры (демо)
      document.getElementById('btn-filter').addEventListener('click',()=>{
        const cat = prompt('Показать только категорию (оставьте пустым — показать все):');
        if(!cat){ renderHero(articles[0]); renderList(articles.slice(1)); return; }
        const res = articles.filter(a=>a.category.toLowerCase().includes(cat.toLowerCase()));
        renderHero(res[0]||articles[0]); renderList(res.slice(1));
      });

    })();
  </script>
</body>
</html>
