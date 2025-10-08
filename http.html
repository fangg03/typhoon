<!doctype html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>此時此刻天氣｜免金鑰</title>
  <style>
    :root{
      --bg:#0b1220; --card:#121a2b; --muted:#8aa0b5; --text:#e7eef7; --accent:#4cc9f0; --ok:#24d17c; --warn:#ffd166;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family: ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Noto Sans TC", "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji";
      background: radial-gradient(1200px 800px at 20% -10%, #6699CC, var(--bg)) fixed;
      color:var(--text); display:flex; align-items:center; justify-content:center; padding:24px;
    }
    .app{width:min(900px, 100%);}
    header{display:flex; gap:12px; align-items:center; justify-content:space-between; margin-bottom:14px}
    h1{font-size:20px; font-weight:700; letter-spacing:.2px; margin:0}
    .muted{color:var(--muted)}
    .row{display:flex; gap:10px; flex-wrap:wrap}
    .card{background:linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.02)); border:1px solid rgba(255,255,255,.06); border-radius:16px; padding:14px 16px; box-shadow:0 10px 30px rgba(0,0,0,.22)}
    .controls{display:flex; gap:8px; flex-wrap:wrap}
    input[type="search"], button, .unit-toggle{
      background:var(--card); border:1px solid rgba(255,255,255,.1); color:var(--text);
      padding:10px 12px; border-radius:12px; outline:none; font-size:15px
    }
    input[type="search"]{min-width:240px}
    input::placeholder{color:#9fb2c7}
    button{cursor:pointer}
    button.primary{background:linear-gradient(180deg, #1f6feb, #1560e0); border-color:rgba(255,255,255,.2)}
    .unit-toggle{display:flex; align-items:center; gap:8px}
    .unit-toggle input{accent-color:var(--accent)}

    .main{display:grid; grid-template-columns: 1.2fr .8fr; gap:12px}
    @media (max-width:820px){ .main{grid-template-columns: 1fr} }

    .big{display:flex; align-items:center; justify-content:space-between; gap:16px}
    .temp{font-size:64px; font-weight:800; letter-spacing:-1px}
    .wx{display:flex; align-items:center; gap:12px}
    .wx .icon{font-size:44px}
    .label{font-size:14px; color:var(--muted)}

    .list{display:grid; grid-template-columns: repeat(2, 1fr); gap:10px}
    @media (max-width:560px){ .list{grid-template-columns: 1fr} }
    .item{display:flex; align-items:center; justify-content:space-between; padding:10px 12px; border:1px solid rgba(255,255,255,.06); border-radius:12px; background:rgba(255,255,255,.03)}
    .item .k{color:var(--muted); font-size:14px}
    .item .v{font-weight:700}

    footer{margin-top:10px; font-size:13px}
    a{color:var(--accent); text-decoration:none}
    .small{font-size:12px}
    .error{color:#ff7b7b}
  </style>
</head>
<body>
  <div class="app">
    <header>
      <h1>此時此刻天氣 <span class="muted small">（免金鑰，使用 <a href="https://open-meteo.com/" target="_blank" rel="noopener">Open‑Meteo</a>）</span></h1>
      <div class="controls">
        <input id="q" type="search" placeholder="搜尋城市，例如：台北、Tokyo、New York…" list="suggest" />
        <datalist id="suggest"></datalist>
        <button id="useLoc">用我的定位</button>
        <button id="go" class="primary">查詢</button>
        <label class="unit-toggle"><input id="unit" type="checkbox" /> 顯示華氏 °F</label>
      </div>
    </header>

    <section class="main">
      <div class="card">
        <div class="big">
          <div>
            <div id="place" style="font-weight:700; font-size:20px">—</div>
            <div class="label" id="updated">—</div>
          </div>
          <div class="wx">
            <div class="icon" id="icon">☁️</div>
            <div>
              <div class="temp" id="temp">--°</div>
              <div class="label" id="desc">—</div>
            </div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="list" id="metrics">
          <!-- metrics injected here -->
        </div>
      </div>
          <div class="card">
        <div class="list" id="forecast">
          <!-- forecast injected here -->
        </div>
      </div>
    </section>

    <footer class="muted">
      <div>資料來源：<a href="https://open-meteo.com/" target="_blank" rel="noopener">Open‑Meteo 天氣與地理編碼 API</a>（免費、免金鑰）。</div>
      <div class="small">提示：若瀏覽器拒絕定位，可改用上方搜尋城市；結果以 Open‑Meteo 的 <code>timezone=auto</code> 轉為你的時區。</div>
      <div class="small error" id="err"></div>
    </footer>
  </div>

  <script>
  const q = document.getElementById('q');
  const suggest = document.getElementById('suggest');
  const goBtn = document.getElementById('go');
  const useLocBtn = document.getElementById('useLoc');
  const unitChk = document.getElementById('unit');
  const placeEl = document.getElementById('place');
  const updatedEl = document.getElementById('updated');
  const descEl = document.getElementById('desc');
  const tempEl = document.getElementById('temp');
  const iconEl = document.getElementById('icon');
  const metricsEl = document.getElementById('metrics');
  const forecastEl = document.getElementById('forecast');
  const errEl = document.getElementById('err');

  const state = {
    unit: localStorage.getItem('unit') === 'f' ? 'f' : 'c',
    lastLoc: JSON.parse(localStorage.getItem('lastLoc')||'null')
  }
  unitChk.checked = state.unit === 'f';

  const WMO = {
    0:['晴朗','☀️'],1:['多雲','🌤️'],2:['半多雲','⛅'],3:['陰','☁️'],45:['霧','🌫️'],48:['著霜霧','🌫️'],
    51:['毛毛雨','🌦️'],53:['小雨','🌦️'],55:['中雨','🌧️'],56:['凍毛毛雨','🌧️'],57:['凍小雨','🌧️'],
    61:['小雨','🌧️'],63:['中雨','🌧️'],65:['大雨','🌧️'],66:['凍雨','🌧️'],67:['強凍雨','🌧️'],
    71:['小雪','🌨️'],73:['中雪','🌨️'],75:['大雪','❄️'],77:['雪粒','🌨️'],
    80:['短暫陣雨','🌦️'],81:['陣雨','🌧️'],82:['強陣雨','🌧️'],
    85:['陣雪','🌨️'],86:['強陣雪','❄️'],
    95:['雷雨','⛈️'],96:['雷雨伴小冰雹','⛈️'],99:['雷雨伴大冰雹','⛈️']
  }

  function kph(ms){return (ms*3.6)}
  function toF(c){return c*9/5+32}
  function windDirText(deg){
    const dirs=['北','北北東','北東','東北東','東','東南東','南東','南南東','南','南南西','南西','西南西','西','西北西','北西','北北西'];
    const i=Math.round(deg/22.5)%16; return dirs[i];
  }
  function arrow(deg){return `↗️`.normalize();}

  function formatTime(iso){
    try{
      const d=new Date(iso);
      return new Intl.DateTimeFormat(undefined,{dateStyle:'medium', timeStyle:'short'}).format(d);
    }catch{ return iso }
  }

  async function geocode(name){
    const url = new URL('https://geocoding-api.open-meteo.com/v1/search');
    url.searchParams.set('name', name);
    url.searchParams.set('count', '5');
    url.searchParams.set('language', 'zh');
    const r = await fetch(url);
    if(!r.ok) throw new Error('地理編碼失敗');
    const j = await r.json();
    return (j.results||[]).map(x=>({
      name: `${x.name}${x.admin1? '，'+x.admin1:''}${x.country? '，'+x.country:''}`,
      lat:x.latitude, lon:x.longitude
    }))
  }

  async function fetchWeather(lat, lon){
    const url = new URL('https://api.open-meteo.com/v1/forecast');
    url.searchParams.set('latitude', lat);
    url.searchParams.set('longitude', lon);
    url.searchParams.set('current', 'temperature_2m,apparent_temperature,relative_humidity_2m,precipitation,cloud_cover,wind_speed_10m,wind_direction_10m,weather_code');
    url.searchParams.set('daily', 'weather_code,temperature_2m_max,temperature_2m_min,precipitation_sum,precipitation_probability_max');
    url.searchParams.set('forecast_days', '3');
    url.searchParams.set('timezone', 'auto');
    const r = await fetch(url);
    if(!r.ok) throw new Error('天氣資料擷取失敗');
    return r.json();
  }

  function renderWeather(locLabel, lat, lon, data){
    const c = data.current;
    const code = c.weather_code;
    const [desc, emoji] = WMO[code] || ['天氣狀況', '❔'];

    let t = c.temperature_2m;
    let at = c.apparent_temperature;
    if(state.unit==='f'){ t = toF(t); at = toF(at); }

    tempEl.textContent = `${Math.round(t)}°${state.unit==='f'?'F':'C'}`;
    descEl.textContent = desc;
    iconEl.textContent = emoji;
    placeEl.textContent = `${locLabel} · ${lat.toFixed(3)}, ${lon.toFixed(3)}`;
    updatedEl.textContent = `更新時間：${formatTime(c.time)}`;

    const items = [
      ['體感溫度', `${Math.round(at)}°${state.unit==='f'?'F':'C'}`],
      ['相對濕度', `${c.relative_humidity_2m}%`],
      ['降水量', `${c.precipitation} mm`],
      ['雲量', `${c.cloud_cover}%`],
      ['風速', `${kph(c.wind_speed_10m).toFixed(1)} km/h`],
      ['風向', `${windDirText(c.wind_direction_10m)}（${Math.round(c.wind_direction_10m)}°）`]
    ];

    metricsEl.innerHTML = items.map(([k,v])=>`
      <div class="item"><div class="k">${k}</div><div class="v">${v}</div></div>
    `).join('');

    // --- Forecast for tomorrow and the day after ---
    const d = data.daily;
    if(d && d.time && d.time.length){
      const today = new Date(c.time);
      const rows = [];
      for(let i=0; i<d.time.length; i++){
        const dt = new Date(d.time[i]);
        // pick only dates after today
        if(dt.getDate() === today.getDate() && dt.getMonth() === today.getMonth() && dt.getFullYear() === today.getFullYear()) continue;
        let tmax = d.temperature_2m_max[i];
        let tmin = d.temperature_2m_min[i];
        if(state.unit==='f'){ tmax = toF(tmax); tmin = toF(tmin); }
        const w = WMO[d.weather_code[i]] || ['天氣狀況','❔'];
        const pop = d.precipitation_probability_max ? d.precipitation_probability_max[i] : undefined;
        const psum = d.precipitation_sum ? d.precipitation_sum[i] : undefined;
        const labelRel = (()=>{
          const diff = Math.round((dt - new Date(today.toDateString()))/86400000);
          if(diff===1) return '明天';
          if(diff===2) return '後天';
          return new Intl.DateTimeFormat(undefined,{weekday:'short', month:'numeric', day:'numeric'}).format(dt);
        })();
        rows.push(`
          <div class="item">
            <div class="k">${labelRel} ${w[1]}</div>
            <div class="v">${Math.round(tmin)}° / ${Math.round(tmax)}°${state.unit==='f'?'F':'C'}${(pop!=null)?` · 降雨機率 ${pop}%`:''}${(psum!=null)?` · 降水 ${psum} mm`:''}</div>
          </div>
        `);
        if(rows.length===2) break; // only tomorrow & day after
      }
      forecastEl.innerHTML = rows.join('');
    } else {
      forecastEl.innerHTML = '<div class="item"><div class="k">預報</div><div class="v">暫無資料</div></div>';
    }
  }

  async function runWithCoords(locLabel, lat, lon){
    try{
      errEl.textContent = '';
      const data = await fetchWeather(lat, lon);
      renderWeather(locLabel, lat, lon, data);
      state.lastLoc = {label:locLabel, lat, lon};
      localStorage.setItem('lastLoc', JSON.stringify(state.lastLoc));
    }catch(e){ errEl.textContent = e.message || String(e); }
  }

  // Search suggestions (debounced)
  let tId = 0;
  q.addEventListener('input', ()=>{
    const val = q.value.trim();
    if(tId) clearTimeout(tId);
    if(!val){ suggest.innerHTML=''; return; }
    tId = setTimeout(async ()=>{
      try{
        const res = await geocode(val);
        suggest.innerHTML = res.map(r=>`<option value="${r.name}" data-lat="${r.lat}" data-lon="${r.lon}"></option>`).join('');
      }catch{ /* silence */ }
    }, 280);
  });

  // Go button
  goBtn.addEventListener('click', async ()=>{
    const val = q.value.trim();
    if(!val){ errEl.textContent = '請輸入城市名稱，或按「用我的定位」。'; return; }
    try{
      const results = await geocode(val);
      if(!results.length) { errEl.textContent = '找不到這個地點，請換個關鍵字試試。'; return; }
      const {name, lat, lon} = results[0];
      runWithCoords(name, lat, lon);
    }catch(e){ errEl.textContent = e.message || String(e); }
  });

  // Use my location
  useLocBtn.addEventListener('click', ()=>{
    if(!('geolocation' in navigator)){
      errEl.textContent = '此瀏覽器不支援定位，請改用上方搜尋城市。'; return;
    }
    errEl.textContent = '正在取得定位…';
    navigator.geolocation.getCurrentPosition(async pos=>{
      errEl.textContent = '';
      const {latitude:lat, longitude:lon} = pos.coords;
      try{
        // 反查地名（免金鑰）
        const rev = await fetch(`https://geocoding-api.open-meteo.com/v1/reverse?latitude=${lat}&longitude=${lon}&language=zh`);
        let label = '我的位置';
        if(rev.ok){
          const j = await rev.json();
          if(j && j.results && j.results[0]){
            const r = j.results[0];
            label = `${r.name}${r.admin1? '，'+r.admin1:''}${r.country? '，'+r.country:''}`;
          }
        }
        runWithCoords(label, lat, lon);
      }catch(e){
        runWithCoords('我的位置', lat, lon);
      }
    }, err=>{
      errEl.textContent = '無法取得定位：' + (err.message||'請確認權限');
    }, {enableHighAccuracy:true, timeout:10000, maximumAge:60000});
  });

  // Unit toggle
  unitChk.addEventListener('change', ()=>{
    state.unit = unitChk.checked ? 'f' : 'c';
    localStorage.setItem('unit', state.unit);
    // Re-render with cached data if available by re-fetching for accuracy
    if(state.lastLoc){ runWithCoords(state.lastLoc.label, state.lastLoc.lat, state.lastLoc.lon); }
  });

  // Boot: load last location or try geolocation
  (async function init(){
    if(state.lastLoc){ runWithCoords(state.lastLoc.label, state.lastLoc.lat, state.lastLoc.lon); return; }
    // Try geolocation quietly
    if('geolocation' in navigator){
      navigator.geolocation.getCurrentPosition(p=>{
        const {latitude:lat, longitude:lon} = p.coords;
        runWithCoords('我的位置', lat, lon);
      });
    }
  })();
  </script>
   </footer>
</div>

<!-- 固定底部返回主頁 -->
<a href="title.html" style="
  position:fixed;
  bottom:20px;
  left:50%;
  transform:translateX(-50%);
  display:inline-block;
  padding:12px 24px;
  background:	#D0D0D0;
  color:#000;
  border-radius:10px;
  text-decoration:none;
  font-weight:600;
  box-shadow:0 4px 10px rgba(0,0,0,.3);
  z-index:999;
">⬅返回主頁</a>

</body>
</html>
