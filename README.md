# emerson-mods-blooket-1
working blooket mods 

right-click your mouse on the blooket web page click inspect/inspect element look up and click console and paste the cod you get from my file and hit enter click ok and BOOOOM you have it finished



   <!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Pack Opener — CodePen Ready</title>
  <style>
    :root{
      --bg:#0f1724;
      --card:#0b1220;
      --accent:#7c3aed;
      --glass:rgba(255,255,255,0.04);
      --badge-bg:rgba(255,255,255,0.06);
    }
    html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,Helvetica,Arial}
    body{
      background:linear-gradient(180deg,#081225 0%, #071127 60%);
      color:#e6eef8;
      display:flex;
      align-items:flex-start;
      justify-content:center;
      padding:32px;
      min-height:100vh;
    }
    .wrap{max-width:980px;width:100%}
    header{display:flex;align-items:center;gap:16px;margin-bottom:18px}
    h1{font-size:20px;margin:0}
    p.lead{margin:0;color:#a9c0df;font-size:13px}

    .packs{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-top:18px}
    .pack{
      background:var(--card);
      border-radius:14px;
      padding:18px;
      box-shadow:0 6px 18px rgba(2,6,23,0.6);
      text-align:center;
      cursor:pointer;
      user-select:none;
      transition:transform .14s ease,box-shadow .14s ease;
    }
    .pack:hover{transform:translateY(-6px);box-shadow:0 12px 30px rgba(2,6,23,0.7)}
    .pack .label{font-weight:600;color:#dbeafe}
    .pack .subtitle{font-size:12px;color:#9fb2d6}

    .result{
      margin-top:22px;
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      padding:18px;border-radius:12px;display:flex;align-items:center;gap:16px;flex-wrap:wrap;
    }
    .result .num{font-size:40px;font-weight:700;min-width:90px;text-align:center}
    .result .meta{color:#b9d0f0}

    .log{margin-top:14px;max-height:180px;overflow:auto;background:var(--glass);padding:10px;border-radius:10px;font-size:13px;color:#cfe6ff}

    .tiny{font-size:12px;color:#9fb2d6}
    .btn-row{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
    .btn{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:8px;color:#e6eef8;font-weight:600;cursor:pointer}

    .r-low{color:#ffd1c4}
    .r-mid{color:#fff1a8}
    .r-high{color:#b6ffd6}
    /* blue + radiant glow for value 1 */
    .r-one{
      color:#3b82f6;
      text-shadow:0 0 10px #3b82f6,0 0 20px #60a5fa,0 0 30px #93c5fd;
    }

    footer{margin-top:14px;color:#8ea8d6;font-size:12px}
    .particle{position:fixed;pointer-events:none;font-size:14px;will-change:transform,opacity}
    .pixel{position:fixed;pointer-events:none;will-change:transform,opacity}

    /* INDEX overlay/backdrop */
    #indexBackdrop{
      position:fixed;inset:0;background:rgba(2,6,23,0.6);display:none;z-index:9997;
    }
    #indexContainer{
      position:fixed;
      left:50%;top:50%;
      transform:translate(-50%,-50%) scale(0.98);
      width:92%;
      max-width:980px;
      max-height:72vh;
      display:grid;
      grid-template-columns:repeat(auto-fill,minmax(44px,1fr));
      gap:8px;
      margin:0;
      background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
      padding:12px;
      border-radius:12px;
      overflow:auto;
      box-shadow:0 14px 40px rgba(2,6,23,0.7);
      z-index:9998;
      opacity:0;pointer-events:none;
      transition:opacity 220ms ease, transform 220ms cubic-bezier(.2,.8,.2,1);
    }
    #indexBackdrop.open{display:block;}
    #indexContainer.open{opacity:1;pointer-events:auto;transform:translate(-50%,-50%) scale(1);}

    /* index cells */
    .index-num{
      display:flex;align-items:center;justify-content:center;
      background:#0b1220;border-radius:6px;padding:8px;font-weight:600;color:#9fb2d6;transition:transform .15s;
      user-select:none;position:relative;overflow:visible;
    }
    .index-num.unlocked{color:#fff;background:linear-gradient(180deg,#1e293b,#334155)}
    .index-num.one-unlocked{
      background:radial-gradient(circle,#3b82f6,#1e3a8a);
      color:#fff;
      text-shadow:0 0 10px #60a5fa,0 0 20px #93c5fd,0 0 30px #bfdbfe;
    }

    /* small counter badge shown at top-right of each index cell when rolled multiple times */
    .count-badge{
      position:absolute;top:6px;right:6px;min-width:18px;height:18px;padding:0 6px;border-radius:10px;font-size:11px;line-height:18px;text-align:center;background:var(--badge-bg);color:#e6eef8;font-weight:700;box-shadow:0 2px 6px rgba(0,0,0,0.4);
      transform-origin:center;transition:transform 160ms ease,opacity 160ms ease;
    }
    .count-badge.show{transform:scale(1);opacity:1}
    .count-badge.hide{transform:scale(0.6);opacity:0}

    /* small responsive nicety */
    @media (max-width:520px){
      .packs{grid-template-columns:repeat(2,1fr)}
      .result .num{font-size:34px}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <h1>Pack Opener — CodePen-ready</h1>
        <p class="lead">Click a pack to open it — numbers 1–100. Open the Index to view unlocked numbers and see how many times you rolled each.</p>
      </div>
    </header>

    <div class="packs" id="packs">
      <div class="pack" data-pack="1"><div class="label">Pack 1</div><div class="subtitle">Most generous</div></div>
      <div class="pack" data-pack="2"><div class="label">Pack 2</div><div class="subtitle">Balanced</div></div>
      <div class="pack" data-pack="3"><div class="label">Pack 3</div><div class="subtitle">Slightly stingy</div></div>
      <div class="pack" data-pack="4"><div class="label">Pack 4</div><div class="subtitle">Lower chance for low numbers</div></div>
    </div>

    <div class="result" id="result">
      <div class="num" id="num">—</div>
      <div>
        <div class="meta" id="meta">Click a pack to open it</div>
        <div style="height:8px"></div>
        <div class="btn-row">
          <button class="btn" id="reset">Reset log</button>
          <button class="btn" id="explain">Show odds (console)</button>
          <button class="btn" id="toggleIndex">Index</button>
        </div>
      </div>
    </div>

    <div id="indexContainer" aria-hidden="true"></div>
    <div id="indexBackdrop" tabindex="-1"></div>

    <div class="log" id="log"></div>
    <footer>Numbers range 1 (lowest) to 100 (highest). The small badge in the Index shows how many times you rolled a number. Reset clears counts.</footer>
  </div>

  <script>
    // === Weighted distribution setup (1..100) ===
    const baseWeights = Array.from({length:100}, (_, i) => Math.pow((i+1)/10, 1.3));

    const packModifiers = {
      1: (weights) => weights.map((w,i) => i >= 60 ? w * 1.8 : w),
      2: (weights) => weights,
      3: (weights) => weights.map((w,i) => i <= 30 ? w * 0.8 : w),
      4: (weights) => weights.map((w,i) => i <= 40 ? w * 0.6 : w * 1.15),
    };

    // Track unlocked numbers and counts
    const unlocked = new Set();
    const counts = new Array(101).fill(0); // index by number 1..100

    // DOM refs
    const packsEl = document.getElementById('packs');
    const numEl = document.getElementById('num');
    const metaEl = document.getElementById('meta');
    const logEl = document.getElementById('log');
    const resetBtn = document.getElementById('reset');
    const explainBtn = document.getElementById('explain');
    const toggleIndexBtn = document.getElementById('toggleIndex');
    const indexContainer = document.getElementById('indexContainer');
    const indexBackdrop = document.getElementById('indexBackdrop');

    // Weighted pick routine
    function weightedPick(weights){
      const total = weights.reduce((a,b)=>a+b,0);
      const r = Math.random() * total;
      let acc = 0;
      for(let i=0;i<weights.length;i++){
        acc += weights[i];
        if(r <= acc) return i+1; // values 1..100
      }
      return weights.length;
    }

    function displayWeights(name, weights){ console.log(name, 'first10:', weights.slice(0,10)); }

    function openPack(packId){
      const modFn = packModifiers[packId] || packModifiers[2];
      const adjusted = modFn(baseWeights.slice());
      const value = weightedPick(adjusted);

      // update UI
      numEl.textContent = value;
      if(value === 1){
        numEl.className = 'num r-one';
      } else {
        if(value <= 33) numEl.className = 'num r-low';
        else if(value <= 66) numEl.className = 'num r-mid';
        else numEl.className = 'num r-high';
      }
      metaEl.textContent = `Opened pack ${packId} — result: ${value}`;

      // log
      const time = new Date().toLocaleTimeString();
      logEl.insertAdjacentHTML('afterbegin', `<div><strong>[${time}]</strong> Pack ${packId} → <strong>${value}</strong></div>`);

      // increment counts and unlocked set
      counts[value]++;
      unlocked.add(value);

      // visual effects
      if(value === 1) showOneEffect(); else burst(value);

      // update index badges (if index exists)
      updateIndex();
      displayWeights('Pack ' + packId, adjusted);
    }

    function burst(value){
      for(let i=0;i<12;i++){
        const el = document.createElement('div'); el.className = 'particle'; el.textContent = '✦';
        const rect = numEl.getBoundingClientRect();
        el.style.left = (rect.left + rect.width/2 + (Math.random()-0.5)*80) + 'px';
        el.style.top = (rect.top + (Math.random()-0.5)*40) + 'px';
        el.style.opacity = '0.95'; el.style.transform = `translateY(0) scale(${0.8 + Math.random()*0.6})`;
        el.style.transition = `all 900ms cubic-bezier(.2,.8,.2,1)`; el.style.zIndex = 9999;
        el.style.color = value >= 80 ? '#b6ffd6' : value >= 50 ? '#fff1a8' : '#ffd1c4';
        document.body.appendChild(el);
        requestAnimationFrame(()=>{ el.style.transform = `translateY(${ -120 - Math.random()*80 }px) scale(0.2)`; el.style.opacity = '0'; el.style.left = (parseFloat(el.style.left) + (Math.random()-0.5)*160) + 'px'; });
        setTimeout(()=> el.remove(), 950);
      }
    }

    function showOneEffect(){
      numEl.animate([{ transform: 'scale(1)' },{ transform: 'scale(1.18)' },{ transform: 'scale(1)' }], { duration: 600, easing: 'cubic-bezier(.2,.8,.2,1)' });
      const rect = numEl.getBoundingClientRect(); const cx = rect.left + rect.width/2; const cy = rect.top + rect.height/2;
      const colors = ['#ff4d6d','#ff839d','#ff2b5c','#ffb6c1','#ff6f91'];
      const count = 40;
      for(let i=0;i<count;i++){
        const px = document.createElement('div'); px.className = 'pixel';
        const size = 6 + Math.round(Math.random()*6); px.style.width = `${size}px`; px.style.height = `${size}px`;
        px.style.left = `${cx - 10 + (Math.random()-0.5)*80}px`; px.style.top = `${cy - 10 + (Math.random()-0.5)*80}px`;
        px.style.background = colors[Math.floor(Math.random()*colors.length)]; px.style.opacity = '1'; px.style.borderRadius = (Math.random() > 0.7 ? '4px' : '2px');
        px.style.transition = 'transform 1000ms cubic-bezier(.2,.8,.2,1), opacity 900ms'; px.style.zIndex = 9999; document.body.appendChild(px);
        requestAnimationFrame(()=>{ const dx = (Math.random()-0.5)*280; const dy = -120 + (Math.random()*240); const rot = (Math.random()-0.5)*720; px.style.transform = `translate(${dx}px, ${dy}px) rotate(${rot}deg) scale(${0.4 + Math.random()*0.9})`; px.style.opacity = '0'; });
        setTimeout(()=> px.remove(), 1100 + Math.random()*300);
      }
      for(let i=0;i<8;i++){ const el = document.createElement('div'); el.className = 'particle'; el.textContent = '✦'; el.style.left = `${cx + (Math.random()-0.5)*50}px`; el.style.top = `${cy + (Math.random()-0.5)*30}px`; el.style.opacity = '0.95'; el.style.transform = `translateY(0) scale(${0.8 + Math.random()*0.6})`; el.style.transition = 'all 900ms cubic-bezier(.2,.8,.2,1)'; el.style.zIndex = 9998; el.style.color = '#3b82f6'; document.body.appendChild(el); requestAnimationFrame(()=>{ el.style.transform = `translateY(${ -100 - Math.random()*60 }px) scale(0.2)`; el.style.opacity = '0'; }); setTimeout(()=> el.remove(), 900 + Math.random()*200); }
    }

    // === INDEX grid with count badges ===
    function ensureIndexCells(){
      if(indexContainer.children.length === 0){
        for(let i=1;i<=100;i++){
          const cell = document.createElement('div');
          cell.className = 'index-num';
          cell.textContent = i;
          // create badge element and attach
          const badge = document.createElement('div');
          badge.className = 'count-badge hide';
          badge.textContent = '';
          cell.appendChild(badge);

          // clicking a cell highlights it briefly
          cell.addEventListener('click', () => { cell.animate([{ transform: 'scale(1)' }, { transform: 'scale(1.06)' }, { transform: 'scale(1)' }], { duration: 220 }); });

          indexContainer.appendChild(cell);
        }
      }
    }

    function updateIndex(){
      ensureIndexCells();
      const cells = indexContainer.children;
      for(let i=0;i<cells.length;i++){
        const val = i+1;
        const cell = cells[i];
        cell.className = 'index-num';
        const badge = cell.querySelector('.count-badge');
        if(unlocked.has(val)){
          cell.classList.add('unlocked');
          if(val === 1) cell.classList.add('one-unlocked');
        }
        const c = counts[val] || 0;
        if(c > 0){
          badge.textContent = c;
          badge.classList.remove('hide');
          badge.classList.add('show');
          // small pulse to indicate update
          badge.animate([{ transform: 'scale(1)' }, { transform: 'scale(1.18)' }, { transform: 'scale(1)' }], { duration: 260 });
        } else {
          badge.textContent = '';
          badge.classList.remove('show');
          badge.classList.add('hide');
        }
      }
    }

    function openIndex(){ updateIndex(); indexBackdrop.classList.add('open'); indexContainer.classList.add('open'); indexContainer.setAttribute('aria-hidden', 'false'); document.body.style.overflow = 'hidden'; }
    function closeIndex(){ indexBackdrop.classList.remove('open'); indexContainer.classList.remove('open'); indexContainer.setAttribute('aria-hidden', 'true'); document.body.style.overflow = ''; }

    // === event wiring ===
    packsEl.addEventListener('click', (e) => { const p = e.target.closest('.pack'); if(!p) return; const id = p.getAttribute('data-pack'); openPack(id); });
    resetBtn.addEventListener('click', () => { logEl.innerHTML = ''; unlocked.clear(); for(let i=0;i<counts.length;i++) counts[i]=0; [...indexContainer.children].forEach(c=>{ if(c) c.className='index-num'; const b=c.querySelector? c.querySelector('.count-badge'): null; if(b) { b.textContent=''; b.className='count-badge hide'; }}); });
    explainBtn.addEventListener('click', () => { console.log('Base weights (1..100) sample:', baseWeights.slice(0,10)); alert('Weights printed to console (sample).'); });
    toggleIndexBtn.addEventListener('click', () => { if(indexContainer.classList.contains('open')) closeIndex(); else openIndex(); });
    indexBackdrop.addEventListener('click', closeIndex);
    document.addEventListener('keydown', (e) => { if(e.key === 'Escape' && indexContainer.classList.contains('open')) closeIndex(); if(e.key >= '1' && e.key <= '4') openPack(e.key); });

    // initialize a tiny index so toggle opens instantly
    ensureIndexCells();
  </script>
</body>
</html>
