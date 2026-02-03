<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <meta name="theme-color" content="#0b1020" />
  <title>IoT AS 메뉴얼</title>
  <style>
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:system-ui,-apple-system,Segoe UI,Roboto,"Noto Sans KR",Arial,sans-serif;
      color:#e8ecff;
      background:
        radial-gradient(1200px 800px at 20% -10%, #1a2c6f 0%, transparent 55%),
        radial-gradient(900px 700px at 110% 10%, #1b5b4a 0%, transparent 55%),
        #0b1020;
    }
    a{color:inherit; text-decoration:none}
    .app{display:grid; grid-template-columns:280px 1fr; min-height:100vh;}

    .side{
      position:sticky; top:0; height:100vh;
      padding:18px;
      border-right:1px solid rgba(255,255,255,.10);
      background:linear-gradient(180deg, rgba(255,255,255,.04), transparent 40%);
    }
    .brand{
      display:flex; gap:12px; align-items:center;
      padding:12px;
      border:1px solid rgba(255,255,255,.10);
      border-radius:16px;
      background:rgba(255,255,255,.03);
      box-shadow:0 12px 40px rgba(0,0,0,.35);
    }
    .logo{
      width:42px; height:42px; border-radius:14px;
      background:linear-gradient(135deg, #7aa2ff, #8ef0d0);
      display:grid; place-items:center;
      color:#07101c; font-weight:900;
      flex:0 0 auto;
    }
    .brand h1{margin:0; font-size:15px; line-height:1.2}
    .brand p{margin:2px 0 0; font-size:12px; color:#aab2d5}

    .nav{margin-top:14px; display:flex; flex-direction:column; gap:8px;}
    .nav a{
      padding:10px 12px; border-radius:14px;
      border:1px solid transparent;
      color:#aab2d5;
      display:flex; gap:10px; align-items:center;
    }
    .nav a:hover{background:rgba(255,255,255,.04); color:#e8ecff;}
    .nav a.active{
      background:rgba(122,162,255,.13);
      border-color:rgba(122,162,255,.28);
      color:#e8ecff;
    }
    .chip{
      font-size:11px; padding:2px 8px; border-radius:999px;
      border:1px solid rgba(255,255,255,.10);
      color:#aab2d5;
      margin-left:auto;
      flex:0 0 auto;
      opacity:.75;
    }

    .main{padding:22px; max-width:1100px; width:100%;}
    .topbar{display:flex; gap:12px; align-items:center; flex-wrap:wrap; margin-bottom:14px;}
    .search{
      flex:1; min-width:0;
      display:flex; align-items:center; gap:10px;
      border:1px solid rgba(255,255,255,.10);
      background:rgba(255,255,255,.03);
      border-radius:999px;
      padding:10px 14px;
    }
    .search input, .search textarea{
      border:0; outline:0; width:100%;
      background:transparent; color:#e8ecff;
      font-size:14px;
    }
    .search textarea{
      resize:vertical;
      min-height:92px;
      line-height:1.45;
      padding:8px 0;
    }

    .card{
      border:1px solid rgba(255,255,255,.10);
      border-radius:16px;
      background:rgba(255,255,255,.03);
      box-shadow:0 12px 40px rgba(0,0,0,.35);
      padding:16px;
    }
    .card h2{margin:0 0 10px; font-size:18px;}
    .card h3{margin:0 0 10px; font-size:15px;}

    .btnrow{
      display:grid;
      grid-template-columns:repeat(2, minmax(0, 1fr));
      gap:10px;
      margin-top:12px;
    }
    .btn{
      display:flex; align-items:center; justify-content:center;
      padding:12px 14px; border-radius:14px;
      border:1px solid rgba(122,162,255,.35);
      background:rgba(122,162,255,.12);
      color:#e8ecff;
      font-size:14px;
      text-align:center;
      white-space:nowrap; overflow:hidden; text-overflow:ellipsis;
      min-width:0;
      cursor:pointer;
      user-select:none;
    }
    .btn:hover{filter:brightness(1.08);}
    .btn.disabled{
      opacity:.45;
      border-color:rgba(255,255,255,.18);
      background:rgba(255,255,255,.06);
      cursor:default;
      pointer-events:none;
    }

    #manualButtons{ display:grid; grid-template-columns:repeat(3, minmax(0, 1fr)); gap:10px; margin-top:12px; }

    .section{display:none;}
    .section.active{display:block;}

    .list{display:flex; flex-direction:column; gap:10px; margin-top:12px;}
    details{
      border:1px solid rgba(255,255,255,.10);
      border-radius:14px;
      padding:10px 12px;
      background:rgba(0,0,0,.14);
      overflow:hidden;
    }
    details[open]{background:rgba(0,0,0,.18);}
    summary{cursor:pointer; font-weight:800;}
    summary::-webkit-details-marker{display:none}
    .meta{margin-top:8px; font-size:12px; color:#aab2d5; word-break:break-word;}
    .content{
      margin-top:10px;
      color:#e8ecff;
      font-size:13px;
      line-height:1.6;
      white-space:pre-wrap;
      word-break:break-word;
    }

    .pillchip{display:flex; gap:6px; flex-wrap:wrap; margin-top:8px;}
    .pillchip span{
      font-size:11px; padding:4px 8px; border-radius:999px;
      border:1px solid rgba(255,255,255,.10);
      color:#aab2d5;
      background:rgba(0,0,0,.10);
      max-width:100%;
      overflow:hidden; text-overflow:ellipsis;
    }

    .empty{
      padding:14px;
      border:1px dashed rgba(255,255,255,.18);
      border-radius:14px;
      color:#aab2d5;
      background:rgba(0,0,0,.10);
    }

    .headrow{display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:10px;}
    .mini{
      display:inline-flex; align-items:center; justify-content:center;
      padding:10px 12px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,.14);
      background:rgba(255,255,255,.04);
      color:#e8ecff;
      font-size:13px;
      cursor:pointer;
      user-select:none;
      white-space:nowrap;
    }
    .mini:hover{filter:brightness(1.08);}

    .filters{display:flex; gap:8px; flex-wrap:wrap; margin:0;}
    .fchip{
      display:inline-flex; align-items:center;
      font-size:12px;
      padding:7px 10px;
      border-radius:999px;
      border:1px solid rgba(255,255,255,.14);
      background:rgba(0,0,0,.12);
      color:#aab2d5;
      cursor:pointer;
      user-select:none;
    }
    .fchip.active{
      color:#e8ecff;
      border-color:rgba(122,162,255,.35);
      background:rgba(122,162,255,.14);
    }

    .logsum{display:flex; gap:10px; align-items:center; flex-wrap:wrap; line-height:1.3;}
    .logsum .dt{color:#aab2d5; font-weight:800; font-size:12px;}
    .logsum .store{font-weight:900;}
    .badge{
      font-size:11px; padding:3px 8px; border-radius:999px;
      border:1px solid rgba(255,255,255,.10);
      background:rgba(0,0,0,.10);
      color:#aab2d5;
    }
    .badge.done{border-color:rgba(142,240,208,.35); color:#c6fff0; background:rgba(142,240,208,.10);}
    .badge.prog{border-color:rgba(255,210,120,.35); color:#ffe9c1; background:rgba(255,210,120,.10);}
    .badge.todo{border-color:rgba(255,255,255,.18);}

    .preview{
      margin-top:8px;
      color:rgba(232,236,255,.88);
      font-size:12.5px;
      line-height:1.45;
      display:-webkit-box;
      -webkit-line-clamp:3;
      -webkit-box-orient:vertical;
      overflow:hidden;
      word-break:break-word;
      white-space:pre-wrap;
    }
    details[open] .preview{display:none;}

    .toast{
      margin-top:10px;
      font-size:12px;
      color:#aab2d5;
      min-height:16px;
    }

    @media (max-width: 900px){
      .app{grid-template-columns:1fr;}
      .side{
        position:sticky; top:0; height:auto; z-index:10;
        border-right:0;
        border-bottom:1px solid rgba(255,255,255,.10);
        padding:12px;
        backdrop-filter:blur(10px);
        background:rgba(11,16,32,.92);
      }
      .nav{flex-direction:row; gap:8px; margin-top:10px;}
      .nav a{flex:1; justify-content:center; padding:10px 10px;}
      .chip{display:none;}
      .main{padding:14px;}
      #manualButtons{grid-template-columns:repeat(2, minmax(0, 1fr));}
    }
    @media (max-width: 420px){
      .brand{padding:10px;}
      .brand h1{font-size:14px;}
      .btnrow{grid-template-columns:1fr;}
      #manualButtons{grid-template-columns:1fr;}
      .btn{white-space:normal; line-height:1.2;}
    }
  </style>
</head>
<body>
<div class="app">
  <aside class="side">
    <div class="brand">
      <div class="logo">IOT</div>
      <div>
        <h1>IoT AS 메뉴얼</h1>
        <p>Support</p>
      </div>
    </div>
    <nav class="nav">
      <a href="#home" data-tab="home" class="active">🏠 홈 <span class="chip">Links</span></a>
      <a href="#self" data-tab="self">🧯 자가조치 <span class="chip">Guide</span></a>
      <a href="#ticket" data-tab="ticket">📮 AS 접수 <span class="chip">Tickets</span></a>
      <a href="#log"  data-tab="log">📝 AS 이력 <span class="chip">History</span></a>
    </nav>
  </aside>

  <main class="main">
    <div class="topbar">
      <div class="search" title="검색">
        🔎 <input id="q" placeholder="검색어를 입력하세요" />
      </div>
    </div>

    <section class="section active" id="tab-home">
      <div class="card">
        <h2>메뉴얼</h2>
        <div id="manualButtons"></div>
      </div>
    </section>

    <section class="section" id="tab-self">
      <div class="card">
        <div class="headrow">
          <h3 style="margin:0">자가조치</h3>
          <button class="mini" id="btnReloadSelf">새로고침</button>
        </div>
        <div class="list" id="selfList"></div>
      </div>
    </section>

    <section class="section" id="tab-ticket">
      <div class="card">
        <div class="headrow" style="align-items:flex-start;">
          <div style="display:flex; flex-direction:column; gap:10px; min-width:0;">
            <h3 style="margin:0">AS 접수</h3>
            <div class="filters" id="ticketFilters">
              <div class="fchip active" data-f="all">전체</div>
              <div class="fchip" data-f="미처리">미처리</div>
              <div class="fchip" data-f="처리중">처리중</div>
              <div class="fchip" data-f="처리완료">처리완료</div>
              <div class="fchip" data-f="이관요청">이관요청</div>
            </div>
          </div>
          <button class="mini" id="btnReloadTicket">새로고침</button>
        </div>

        <div style="display:grid; gap:10px; margin-top:10px;">
          <div class="search" style="border-radius:16px;">🏪 <input id="t_store" placeholder="매장명 (필수)" /></div>
          <div class="search" style="border-radius:16px;">📞 <input id="t_contact" placeholder="매장 연락처" /></div>
          <div class="search" style="border-radius:16px;">🧩 <input id="t_symptomRoom" placeholder="증상룸" /></div>

          <div class="search" style="border-radius:16px; align-items:flex-start;">
            📝 <textarea id="t_errorDetail" placeholder="오류 상세내용 (필수)"></textarea>
          </div>

          <div class="search" style="border-radius:16px; align-items:flex-start;">
            🧾 <textarea id="t_history" placeholder="대양 처리이력"></textarea>
          </div>

          <div class="search" style="border-radius:16px;">☎️ <input id="t_assigneeTel" placeholder="지앤서비스 담당자 연락처" /></div>

          <div class="btnrow" style="margin-top:0;">
            <div class="btn" id="btnSubmitTicket">등록</div>
            <div class="btn" id="btnClearTicket">초기화</div>
          </div>

          <div class="toast" id="ticketToast"></div>
        </div>

        <div class="list" id="ticketList" style="margin-top:14px;"></div>
      </div>
    </section>

    <section class="section" id="tab-log">
      <div class="card">
        <div class="headrow" style="align-items:flex-start;">
          <div style="display:flex; flex-direction:column; gap:10px; min-width:0;">
            <h3 style="margin:0">AS 이력</h3>
            <div class="filters" id="logFilters">
              <div class="fchip active" data-f="all">전체</div>
              <div class="fchip" data-f="미처리">미처리</div>
              <div class="fchip" data-f="진행중">진행중</div>
              <div class="fchip" data-f="처리완료">처리완료</div>
            </div>
          </div>
          <button class="mini" id="btnReloadLog">새로고침</button>
        </div>
        <div class="list" id="logList"></div>
      </div>
    </section>
  </main>
</div>

<script>
const SHEET_ID = "14actQ-pC6cLXRlqNzS1F0AVuUTAdJC4K_hhq7rOyBX4";
const WIRELESS_GID = "890902374";
const LOG_GID = "806380229";
const TICKET_GID = "638541022";

const TICKET_ENDPOINT = "https://script.google.com/macros/s/AKfycbyNuQ-uggjAIIA6wxmxO5TzPDMVTRPFbzB6b1cvBbTptHlVfMUfdfNRl_u9w3VPiYlh/exec";

const $ = (q)=>document.querySelector(q);
const $$ = (q)=>Array.from(document.querySelectorAll(q));

let wirelessLoaded = false;
let wirelessLoading = null;

let manualRowsCached = [];
let lastSelf = [];
let lastLog  = [];
let logFilter = "all";

let lastTickets = [];
let ticketFilter = "all";

function tabFromHash(){
  const h = (location.hash || "#home").replace("#","");
  return (["home","self","ticket","log"].includes(h)) ? h : "home";
}
function setTabUI(tab){
  $$(".nav a").forEach(a=>a.classList.toggle("active", a.dataset.tab===tab));
  $$(".section").forEach(s=>s.classList.remove("active"));
  const sec = $("#tab-"+tab);
  if(sec) sec.classList.add("active");
}

function isLikelyUrl(s){
  const t = String(s||"").trim();
  if(!t) return false;
  if(/^https?:\/\//i.test(t)) return true;
  if(t.includes("docs.google.com") || t.includes("drive.google.com")) return true;
  return false;
}
function escapeHtml(str){
  return String(str ?? "")
    .replaceAll("&","&amp;").replaceAll("<","&lt;").replaceAll(">","&gt;")
    .replaceAll('"',"&quot;").replaceAll("'","&#039;");
}
function toast(msg){
  const el = $("#ticketToast");
  if(el) el.textContent = msg || "";
}
function normType(s){ return String(s||"").trim().replace(/\s+/g,""); }

function loadSheetTextRows(gid, tq){
  return new Promise((resolve, reject) => {
    const cbName = "__gviz_cb_" + Math.random().toString(36).slice(2) + Date.now();
    const query = encodeURIComponent(tq || "select A,B,C,D,E limit 2000");
    const tqx = encodeURIComponent(`out:json;responseHandler:${cbName}`);
    const url = `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?gid=${encodeURIComponent(gid)}&tq=${query}&tqx=${tqx}&_=${Date.now()}`;

    const script = document.createElement("script");
    const timer = setTimeout(() => { cleanup(); reject(new Error("timeout")); }, 12000);

    function cleanup(){
      clearTimeout(timer);
      try{ delete window[cbName]; }catch(e){}
      if(script.parentNode) script.parentNode.removeChild(script);
    }

    window[cbName] = (resp) => {
      try{
        cleanup();
        if(!resp || resp.status !== "ok"){
          throw new Error(resp?.errors?.[0]?.message || "load failed");
        }
        const rows = (resp.table.rows||[]).map(r => (r.c||[]).map(cell => {
          if(!cell) return "";
          const f = (cell.f != null) ? String(cell.f).trim() : "";
          const v = (cell.v != null) ? String(cell.v).trim() : "";
          return f || v;
        }));
        resolve(rows);
      }catch(e){ reject(e); }
    };

    script.src = url;
    script.async = true;
    script.onerror = () => { cleanup(); reject(new Error("network")); };
    document.head.appendChild(script);
  });
}

/** HOME/SELF */
function isHeaderRowMS(r){
  const a = normType(r[0]), b = normType(r[1]), c = normType(r[2]);
  if((a==="구분"||a==="분류") && b==="제목" && c==="내용") return true;
  if(b==="제목" && c==="내용") return true;
  if(a==="제목" && b==="내용") return true;
  return false;
}
function compactRowsMS(rows){
  const data = (rows||[]).filter(r => (r||[]).some(x => String(x).trim() !== ""));
  while(data.length && isHeaderRowMS(data[0])) data.shift();
  return data;
}
function toMSObjects(rows){
  const data = compactRowsMS(rows);
  return data.map((r,idx)=>({
    rowNo: idx+2,
    type: normType(r[0]),
    title: String(r[1]||"").trim(),
    content: String(r[2]||"").trim(),
    link: String(r[3]||"").trim(),
    tags: String(r[4]||"").trim()
  })).filter(x => x.type || x.title || x.content || x.link || x.tags);
}
function labelForLink(item, n){ return item.title ? item.title : `메뉴얼 ${n}`; }
function labelForSelf(item, n){
  if(item.title) return item.title;
  const first = (item.content||"").split("\n").map(x=>x.trim()).filter(Boolean)[0];
  if(first) return first.length > 28 ? first.slice(0,28)+"…" : first;
  if(isLikelyUrl(item.link)) return "자료";
  return `자가조치 ${n}`;
}
function renderManualButtons(items){
  const wrap = $("#manualButtons");
  wrap.innerHTML = "";
  if(!items.length){
    wrap.innerHTML = `<div class="empty">등록된 항목이 없습니다.</div>`;
    return;
  }
  items.forEach(x=>{
    const a = document.createElement("a");
    a.className = "btn";
    a.textContent = x.title || "메뉴얼";
    if(isLikelyUrl(x.link)){
      a.href = x.link.startsWith("http") ? x.link : ("https://" + x.link);
      a.target = "_blank";
      a.rel = "noopener";
    }else{
      a.classList.add("disabled");
    }
    wrap.appendChild(a);
  });
}
function renderSelf(items){
  const list = $("#selfList");
  const q = $("#q").value.trim().toLowerCase();
  const filtered = items.filter(x=>{
    if(!q) return true;
    const blob = `${x.title} ${x.content} ${x.tags} ${x.link}`.toLowerCase();
    return blob.includes(q);
  });

  list.innerHTML = "";
  if(!filtered.length){
    list.innerHTML = `<div class="empty">검색 결과가 없습니다.</div>`;
    return;
  }

  filtered.forEach(x=>{
    const d = document.createElement("details");
    const tagArr = (x.tags||"").split(",").map(t=>t.trim()).filter(Boolean);

    const tagsHtml = tagArr.length
      ? `<div class="pillchip">${tagArr.map(t=>`<span>#${escapeHtml(t)}</span>`).join("")}</div>`
      : "";

    const linkHtml = isLikelyUrl(x.link)
      ? `<div class="meta">자료: <a href="${x.link.startsWith("http")?x.link:"https://"+x.link}" target="_blank" rel="noopener">링크</a></div>`
      : "";

    const contentHtml = String(x.content||"").trim()
      ? `<div class="content body">${escapeHtml(x.content)}</div>`
      : "";

    d.innerHTML = `
      <summary>${escapeHtml(x.title)}</summary>
      ${tagsHtml}
      ${contentHtml}
      ${linkHtml}
    `;
    list.appendChild(d);
  });
}
async function ensureWirelessLoaded(force=false){
  if(wirelessLoaded && !force) return;
  if(wirelessLoading && !force) return wirelessLoading;

  wirelessLoading = (async ()=>{
    const tab = tabFromHash();
    if(!force && tab !== "home" && tab !== "self") return;

    try{
      const rawRows = await loadSheetTextRows(WIRELESS_GID, "select A,B,C,D,E limit 2000");
      const rows = toMSObjects(rawRows);

      const manualByType = rows.filter(x => x.type === "메뉴얼");
      const selfByType   = rows.filter(x => x.type === "자가조치" && (x.title || x.content || isLikelyUrl(x.link)));

      const manualAuto = rows.filter(x => !x.type && isLikelyUrl(x.link));
      const selfAuto   = rows.filter(x => !x.type && (String(x.content||"").trim() !== "" || isLikelyUrl(x.link)));

      const manual = (manualByType.length ? manualByType : manualAuto)
        .map((x,i)=>({ ...x, title: labelForLink(x, i+1) }));

      const self = (selfByType.length ? selfByType : selfAuto)
        .filter(x => x.title || String(x.content||"").trim() !== "" || isLikelyUrl(x.link))
        .map((x,i)=>({ ...x, title: labelForSelf(x, i+1) }));

      manualRowsCached = manual;
      lastSelf = self;

      renderManualButtons(manualRowsCached);
      if(tabFromHash() === "self") renderSelf(lastSelf);

      wirelessLoaded = true;
    }catch(e){
      wirelessLoaded = false;
      renderManualButtons([]);
      lastSelf = [];
      if(tabFromHash() === "self") renderSelf(lastSelf);
    }
  })();

  try{ return await wirelessLoading; }
  finally{ wirelessLoading = null; }
}

/** LOG */
function normStatus(s){
  const v = String(s||"").trim();
  if(v==="처리완료" || v==="진행중" || v==="미처리") return v;
  return v || "미처리";
}
function statusBadge(status){
  const st = normStatus(status);
  if(st==="처리완료") return `<span class="badge done">처리완료</span>`;
  if(st==="진행중") return `<span class="badge prog">진행중</span>`;
  return `<span class="badge todo">미처리</span>`;
}
function parseDT(dateStr, timeStr){
  const d = String(dateStr||"").trim();
  const t = String(timeStr||"").trim();
  if(!d && !t) return 0;
  const base = d.replace(/\./g,"-").replace(/\//g,"-");
  const s = (base && t) ? `${base} ${t}` : (base || t);
  const dt = new Date(s);
  const ms = dt.getTime();
  return Number.isFinite(ms) ? ms : 0;
}
function compactLogRows(rows){
  const data = (rows||[]).filter(r => (r||[]).some(x => String(x).trim() !== ""));
  while(data.length){
    const a = normType(data[0][0]), b = normType(data[0][1]), c = normType(data[0][2]);
    if((a==="일시"||a==="날짜") && b==="시간" && c==="매장명") data.shift();
    else break;
  }
  return data;
}
async function loadLogFromSheet(){
  const raw = await loadSheetTextRows(LOG_GID, "select A,B,C,D,E limit 3000");
  const rows = compactLogRows(raw);

  const data = rows.map(r=>({
    date:  String(r[0]||"").trim(),
    time:  String(r[1]||"").trim(),
    store: String(r[2]||"").trim(),
    memo:  String(r[3]||"").trim(),
    status: normStatus(r[4])
  })).filter(x => x.date || x.time || x.store || x.memo);

  data.sort((a,b)=> parseDT(b.date,b.time) - parseDT(a.date,a.time));
  return data;
}
function renderLog(items){
  const list = $("#logList");
  const q = $("#q").value.trim().toLowerCase();

  const filtered = items.filter(x=>{
    if(logFilter !== "all" && String(x.status||"").trim() !== logFilter) return false;
    if(!q) return true;
    const blob = `${x.date} ${x.time} ${x.store} ${x.memo} ${x.status}`.toLowerCase();
    return blob.includes(q);
  });

  list.innerHTML = "";
  if(!filtered.length){
    list.innerHTML = `<div class="empty">표시할 항목이 없습니다.</div>`;
    return;
  }

  filtered.forEach(x=>{
    const d = document.createElement("details");
    const dtText = [x.date, x.time].filter(Boolean).join(" ");
    const preview = String(x.memo||"").trim();

    d.innerHTML = `
      <summary>
        <div class="logsum">
          <span class="dt">${escapeHtml(dtText)}</span>
          <span class="store">${escapeHtml(x.store || "매장명 없음")}</span>
          ${statusBadge(x.status)}
        </div>
        ${preview ? `<div class="preview">${escapeHtml(preview)}</div>` : ``}
      </summary>
      <div class="content body">${escapeHtml(x.memo || "")}</div>
      <div class="meta">${escapeHtml(normStatus(x.status))}</div>
    `;
    list.appendChild(d);
  });
}
async function reloadLog(){
  if(tabFromHash()==="log") $("#logList").innerHTML = `<div class="empty">불러오는 중…</div>`;
  try{
    lastLog = await loadLogFromSheet();
    renderLog(lastLog);
  }catch(e){
    lastLog = [];
    renderLog(lastLog);
  }
}

/** TICKETS */
function normTicketStatus(s){
  const v = String(s||"").trim();
  if(["미처리","처리중","처리완료","이관요청"].includes(v)) return v;
  return v || "미처리";
}
function ticketBadge(status){
  const st = normTicketStatus(status);
  if(st==="처리완료") return `<span class="badge done">처리완료</span>`;
  if(st==="처리중") return `<span class="badge prog">처리중</span>`;
  if(st==="이관요청") return `<span class="badge prog">이관요청</span>`;
  return `<span class="badge todo">미처리</span>`;
}
function isHeaderRowTicket(r){
  const a = String(r[0]||"").trim().toLowerCase();
  return a === "id";
}
async function loadTicketsFromSheet(){
  const raw = await loadSheetTextRows(TICKET_GID, "select A,B,C,D,E,F,G,H,I,J limit 3000");
  let rows = (raw||[]).filter(r => (r||[]).some(x => String(x).trim() !== ""));

  while(rows.length && isHeaderRowTicket(rows[0])) rows.shift();

  const data = rows.map(r=>({
    id: String(r[0]||"").trim(),
    createdAt: String(r[1]||"").trim(),
    updatedAt: String(r[2]||"").trim(),
    store: String(r[3]||"").trim(),
    contact: String(r[4]||"").trim(),
    symptomRoom: String(r[5]||"").trim(),
    errorDetail: String(r[6]||"").trim(),
    history: String(r[7]||"").trim(),
    assigneeTel: String(r[8]||"").trim(),
    status: normTicketStatus(r[9])
  })).filter(x => x.store || x.errorDetail || x.history || x.assigneeTel);

  data.reverse();
  return data;
}
function renderTickets(items){
  const list = $("#ticketList");
  const q = $("#q").value.trim().toLowerCase();

  const filtered = items.filter(x=>{
    if(ticketFilter !== "all" && x.status !== ticketFilter) return false;
    if(!q) return true;
    const blob = `${x.createdAt} ${x.store} ${x.contact} ${x.symptomRoom} ${x.errorDetail} ${x.history} ${x.assigneeTel} ${x.status}`.toLowerCase();
    return blob.includes(q);
  });

  list.innerHTML = "";
  if(!filtered.length){
    list.innerHTML = `<div class="empty">표시할 항목이 없습니다.</div>`;
    return;
  }

  filtered.forEach(x=>{
    const d = document.createElement("details");
    const head = `${x.store || "매장명 없음"}${x.symptomRoom ? " · " + x.symptomRoom : ""}`;
    const preview = String(x.errorDetail||"").trim();

    d.innerHTML = `
      <summary>
        <div class="logsum">
          <span class="dt">${escapeHtml(x.createdAt || "")}</span>
          <span class="store">${escapeHtml(head)}</span>
          ${ticketBadge(x.status)}
        </div>
        ${preview ? `<div class="preview">${escapeHtml(preview)}</div>` : ``}
      </summary>

      ${x.contact ? `<div class="meta">매장 연락처: ${escapeHtml(x.contact)}</div>` : ``}
      ${x.symptomRoom ? `<div class="meta">증상룸: ${escapeHtml(x.symptomRoom)}</div>` : ``}

      ${x.errorDetail ? `<div class="content"><b>오류 상세내용</b>\n${escapeHtml(x.errorDetail)}</div>` : ``}
      ${x.history ? `<div class="content"><b>대양 처리이력</b>\n${escapeHtml(x.history)}</div>` : ``}
      ${x.assigneeTel ? `<div class="meta">지앤서비스 담당자 연락처: ${escapeHtml(x.assigneeTel)}</div>` : ``}

      <div class="meta">상태: ${escapeHtml(normTicketStatus(x.status))}</div>
    `;
    list.appendChild(d);
  });
}
async function reloadTickets(){
  if(tabFromHash()==="ticket") $("#ticketList").innerHTML = `<div class="empty">불러오는 중…</div>`;
  try{
    lastTickets = await loadTicketsFromSheet();
    renderTickets(lastTickets);
    toast("");
  }catch(e){
    lastTickets = [];
    renderTickets(lastTickets);
    toast("불러오기 실패");
  }
}
async function submitTicket(){
  const store = ($("#t_store")?.value || "").trim();
  const contact = ($("#t_contact")?.value || "").trim();
  const symptomRoom = ($("#t_symptomRoom")?.value || "").trim();
  const errorDetail = ($("#t_errorDetail")?.value || "").trim();
  const history = ($("#t_history")?.value || "").trim();
  const assigneeTel = ($("#t_assigneeTel")?.value || "").trim();

  if(!store || !errorDetail){
    toast("필수값 확인");
    return;
  }

  const body = new URLSearchParams({
    action: "create",
    store,
    contact,
    symptomRoom,
    errorDetail,
    history,
    assigneeTel
  });

  toast("저장 중");

  await fetch(TICKET_ENDPOINT, {
    method: "POST",
    mode: "no-cors",
    headers: { "Content-Type": "application/x-www-form-urlencoded;charset=UTF-8" },
    body
  });

  toast("저장됨");
  $("#t_symptomRoom").value = "";
  $("#t_errorDetail").value = "";
  $("#t_history").value = "";
  $("#t_assigneeTel").value = "";

  setTimeout(reloadTickets, 900);
}

/** ROUTE */
function route(){
  const tab = tabFromHash();
  setTabUI(tab);

  if(tab==="home") ensureWirelessLoaded(false);
  if(tab==="self"){ ensureWirelessLoaded(false); renderSelf(lastSelf); }
  if(tab==="ticket") reloadTickets();
  if(tab==="log") reloadLog();
}
window.addEventListener("hashchange", route);

$("#q").addEventListener("input", ()=>{
  const tab = tabFromHash();
  if(tab==="self") renderSelf(lastSelf);
  if(tab==="log")  renderLog(lastLog);
  if(tab==="ticket") renderTickets(lastTickets);
});

$("#btnReloadSelf").addEventListener("click", ()=> ensureWirelessLoaded(true));
$("#btnReloadLog").addEventListener("click", reloadLog);
$("#btnReloadTicket").addEventListener("click", reloadTickets);
$("#btnSubmitTicket").addEventListener("click", submitTicket);
$("#btnClearTicket").addEventListener("click", ()=>{
  $("#t_store").value = "";
  $("#t_contact").value = "";
  $("#t_symptomRoom").value = "";
  $("#t_errorDetail").value = "";
  $("#t_history").value = "";
  $("#t_assigneeTel").value = "";
  toast("");
});

(function initTicketFilters(){
  const wrap = $("#ticketFilters");
  wrap.addEventListener("click", (ev)=>{
    const btn = ev.target.closest(".fchip");
    if(!btn) return;
    ticketFilter = btn.dataset.f || "all";
    $$("#ticketFilters .fchip").forEach(x=>x.classList.toggle("active", x.dataset.f === ticketFilter));
    renderTickets(lastTickets);
  });
})();
(function initLogFilters(){
  const wrap = $("#logFilters");
  wrap.addEventListener("click", (ev)=>{
    const btn = ev.target.closest(".fchip");
    if(!btn) return;
    logFilter = btn.dataset.f || "all";
    $$("#logFilters .fchip").forEach(x=>x.classList.toggle("active", x.dataset.f === logFilter));
    renderLog(lastLog);
  });
})();

route();
</script>
</body>
</html>
