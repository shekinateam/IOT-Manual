<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>IoT AS 매뉴얼</title>
  <style>
    :root{
      --bg:#0b1020; --text:#e8ecff; --muted:#aab2d5; --bd:rgba(255,255,255,.10);
      --accent:#7aa2ff; --accent2:#8ef0d0;
      --shadow: 0 12px 40px rgba(0,0,0,.35);
      --radius:16px;
      --font: system-ui, -apple-system, Segoe UI, Roboto, "Noto Sans KR", Arial, sans-serif;
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family:var(--font); color:var(--text);
      background:
        radial-gradient(1200px 800px at 20% -10%, #1a2c6f 0%, transparent 55%),
        radial-gradient(900px 700px at 110% 10%, #1b5b4a 0%, transparent 55%),
        var(--bg);
    }
    a{color:inherit; text-decoration:none}
    .app{
      display:grid;
      grid-template-columns: 280px 1fr;
      min-height:100vh;
    }
    .side{
      position:sticky; top:0; height:100vh;
      padding:18px; border-right:1px solid var(--bd);
      background:linear-gradient(180deg, rgba(255,255,255,.04), transparent 40%);
    }
    .brand{
      display:flex; gap:12px; align-items:center;
      padding:12px; border:1px solid var(--bd);
      border-radius:var(--radius); background:rgba(255,255,255,.03);
      box-shadow:var(--shadow);
    }
    .logo{
      width:42px; height:42px; border-radius:14px;
      background:linear-gradient(135deg, var(--accent), var(--accent2));
      display:grid; place-items:center; color:#07101c; font-weight:900;
      flex:0 0 auto;
    }
    .brand h1{margin:0; font-size:15px; line-height:1.2}
    .brand p{margin:2px 0 0; font-size:12px; color:var(--muted)}
    .nav{margin-top:14px; display:flex; flex-direction:column; gap:8px;}
    .nav a{
      padding:10px 12px; border-radius:14px; border:1px solid transparent;
      color:var(--muted); display:flex; gap:10px; align-items:center;
    }
    .nav a:hover{background:rgba(255,255,255,.04); color:var(--text);}
    .nav a.active{background:rgba(122,162,255,.13); border-color:rgba(122,162,255,.28); color:var(--text);}
    .chip{
      font-size:11px; padding:2px 8px; border-radius:999px;
      border:1px solid var(--bd); color:var(--muted); margin-left:auto;
      flex:0 0 auto;
    }

    .main{padding:22px; max-width:1100px; width:100%;}
    .topbar{display:flex; gap:12px; align-items:center; flex-wrap:wrap; margin-bottom:14px;}
    .search{
      flex:1; min-width:0;
      display:flex; align-items:center; gap:10px;
      border:1px solid var(--bd); background:rgba(255,255,255,.03);
      border-radius:999px; padding:10px 14px;
    }
    .search input{border:0; outline:0; width:100%; background:transparent; color:var(--text); font-size:14px;}

    .card{
      border:1px solid var(--bd); border-radius:var(--radius);
      background:rgba(255,255,255,.03); box-shadow:var(--shadow);
      padding:16px;
    }
    .card h2{margin:0 0 10px; font-size:18px;}
    .card h3{margin:0 0 10px; font-size:15px;}

    .btnrow{
      display:grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap:10px;
      margin-top:12px;
    }
    .btn{
      display:flex; align-items:center; justify-content:center;
      padding:12px 14px; border-radius:14px;
      border:1px solid rgba(122,162,255,.35);
      background:rgba(122,162,255,.12);
      color:var(--text); font-size:14px;
      text-align:center;
      white-space:nowrap; overflow:hidden; text-overflow:ellipsis;
      min-width:0;
    }
    .btn:hover{filter:brightness(1.08);}

    .section{display:none;}
    .section.active{display:block;}

    .list{display:flex; flex-direction:column; gap:10px; margin-top:12px;}
    details{
      border:1px solid var(--bd); border-radius:14px;
      padding:10px 12px; background:rgba(0,0,0,.14);
      overflow:hidden;
    }
    summary{cursor:pointer; font-weight:800;}
    summary::-webkit-details-marker{display:none}
    .meta{margin-top:8px; font-size:12px; color:var(--muted); word-break:break-word;}
    .content{margin-top:10px; color:var(--text); font-size:13px; line-height:1.6; white-space:pre-wrap; word-break:break-word;}
    .pillchip{display:flex; gap:6px; flex-wrap:wrap; margin-top:8px;}
    .pillchip span{
      font-size:11px; padding:4px 8px; border-radius:999px;
      border:1px solid var(--bd); color:var(--muted); background:rgba(0,0,0,.10);
      max-width:100%;
      overflow:hidden; text-overflow:ellipsis;
    }
    .empty{
      padding:14px; border:1px dashed rgba(255,255,255,.18);
      border-radius:14px; color:var(--muted); background:rgba(0,0,0,.10);
    }

    /* ✅ AS 이력 */
    .formgrid{
      display:grid; gap:10px;
      grid-template-columns: 1.2fr 1fr;
      margin-top:10px;
    }
    .field{
      border:1px solid var(--bd);
      background:rgba(0,0,0,.14);
      border-radius:14px;
      padding:10px 12px;
      display:flex; flex-direction:column; gap:6px;
      min-width:0;
    }
    .field label{font-size:12px; color:var(--muted);}
    .field input, .field textarea, .field select{
      width:100%;
      border:0; outline:0;
      background:transparent;
      color:var(--text);
      font-size:14px;
      font-family:var(--font);
      resize:vertical;
      min-height:22px;
    }
    .field textarea{min-height:90px; line-height:1.5;}
    .actions{
      display:flex; gap:10px; flex-wrap:wrap;
      margin-top:10px;
    }
    .btn2{
      padding:10px 12px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,.14);
      background:rgba(255,255,255,.04);
      color:var(--text);
      font-size:13px;
      cursor:pointer;
    }
    .btn2.primary{
      border-color:rgba(122,162,255,.35);
      background:rgba(122,162,255,.12);
    }
    .btn2.danger{
      border-color:rgba(255,120,120,.28);
      background:rgba(255,120,120,.10);
    }
    .logtable{
      margin-top:12px;
      border:1px solid var(--bd);
      background:rgba(0,0,0,.14);
      border-radius:14px;
      overflow:hidden;
    }
    .logrow{
      display:grid;
      grid-template-columns: 170px 1.2fr 2fr 110px 86px;
      gap:10px;
      padding:10px 12px;
      border-top:1px solid rgba(255,255,255,.08);
      align-items:center;
      min-width:0;
    }
    .logrow.head{
      border-top:0;
      background:rgba(255,255,255,.03);
      color:var(--muted);
      font-size:12px;
      font-weight:700;
    }
    .logcell{
      min-width:0;
      overflow:hidden;
      text-overflow:ellipsis;
      white-space:nowrap;
      font-size:13px;
    }
    .logcell.wrap{
      white-space:normal;
      overflow:visible;
      word-break:break-word;
      line-height:1.5;
    }
    .badge{
      display:inline-flex;
      align-items:center;
      justify-content:center;
      padding:4px 8px;
      border-radius:999px;
      border:1px solid var(--bd);
      font-size:12px;
      color:var(--muted);
      background:rgba(0,0,0,.10);
      max-width:100%;
    }
    .badge.done{
      border-color:rgba(142,240,208,.35);
      color:#c6fff0;
      background:rgba(142,240,208,.10);
    }
    .badge.todo{
      border-color:rgba(255,210,120,.35);
      color:#ffe9c1;
      background:rgba(255,210,120,.10);
    }
    .iconbtn{
      cursor:pointer;
      border:1px solid rgba(255,255,255,.14);
      background:rgba(255,255,255,.04);
      color:var(--text);
      border-radius:12px;
      padding:8px 10px;
      font-size:12px;
      text-align:center;
      white-space:nowrap;
    }
    .iconbtn:hover{filter:brightness(1.08);}

    /* ✅ 모바일 최적화 */
    @media (max-width: 900px){
      .app{grid-template-columns: 1fr;}
      .side{
        position:sticky;
        top:0;
        height:auto;
        z-index:10;
        border-right:0;
        border-bottom:1px solid var(--bd);
        padding:12px;
        backdrop-filter: blur(10px);
        background:rgba(11,16,32,.92);
      }
      .nav{
        flex-direction:row;
        gap:8px;
        margin-top:10px;
      }
      .nav a{
        flex:1;
        justify-content:center;
        padding:10px 10px;
      }
      .chip{display:none;}
      .main{padding:14px;}
      .btnrow{grid-template-columns: repeat(2, minmax(0, 1fr));}

      .formgrid{grid-template-columns: 1fr;}
      .logrow{grid-template-columns: 1fr; gap:6px;}
      .logrow.head{display:none;}
      .logcell{white-space:normal;}
    }
    @media (max-width: 420px){
      .brand{padding:10px;}
      .brand h1{font-size:14px;}
      .btnrow{grid-template-columns: 1fr;}
      .btn{white-space:normal; line-height:1.2;}
    }

    /* ✅ 터치(모바일/태블릿)에서는 리스트 내부 스크롤 전부 제거 */
    @media (hover: none) and (pointer: coarse) {
      .list .body{
        max-height: none !important;
        overflow: visible !important;
      }
    }
  </style>
</head>
<body>
<div class="app">
  <aside class="side">
    <div class="brand">
      <div class="logo">IOT</div>
      <div>
        <h1>IoT AS 매뉴얼</h1>
        <p>Support</p>
      </div>
    </div>
    <nav class="nav">
      <a href="#home" data-tab="home" class="active">🏠 홈 <span class="chip">Links</span></a>
      <a href="#self" data-tab="self">🧯 자가조치 <span class="chip">Guide</span></a>
      <a href="#log"  data-tab="log">📝 AS 이력 <span class="chip">Log</span></a>
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
        <h2>매뉴얼</h2>
        <div class="btnrow" id="manualButtons"></div>
      </div>
    </section>

    <section class="section" id="tab-self">
      <div class="card">
        <h3>자가조치</h3>
        <div class="list" id="selfList"></div>
      </div>
    </section>

    <section class="section" id="tab-log">
      <div class="card">
        <h3>AS 이력</h3>

        <div class="formgrid">
          <div class="field">
            <label>일시</label>
            <input id="logWhen" type="datetime-local" />
          </div>
          <div class="field">
            <label>매장명</label>
            <input id="logStore" type="text" placeholder="예) OO점" />
          </div>
          <div class="field" style="grid-column: 1 / -1;">
            <label>상담내용</label>
            <textarea id="logMemo" placeholder="상담 내용 / 증상 / 조치 내용"></textarea>
          </div>
          <div class="field" style="grid-column: 1 / -1;">
            <label>처리여부</label>
            <select id="logStatus">
              <option value="미처리">미처리</option>
              <option value="진행중">진행중</option>
              <option value="처리완료">처리완료</option>
            </select>
          </div>
        </div>

        <div class="actions">
          <button class="btn2 primary" id="btnSaveLog">저장</button>
          <button class="btn2" id="btnExportCsv">CSV 내보내기</button>
          <button class="btn2 danger" id="btnClearLogs">전체 삭제</button>
        </div>

        <div class="logtable" id="logTable"></div>
      </div>
    </section>
  </main>
</div>

<script>
const CONFIG = {
  SHEET_ID: "14actQ-pC6cLXRlqNzS1F0AVuUTAdJC4K_hhq7rOyBX4",
  WIRELESS_GID: "890902374",
};

const STORAGE_KEY = "iot_as_logs_v1";

const $ = (q)=>document.querySelector(q);
const $$ = (q)=>Array.from(document.querySelectorAll(q));

function setTab(tab){
  $$(".nav a").forEach(a=>a.classList.toggle("active", a.dataset.tab===tab));
  $$(".section").forEach(s=>s.classList.remove("active"));
  const sec = $("#tab-"+tab);
  if(sec) sec.classList.add("active");
  // 탭 바뀌면 현재 검색어 기준으로 다시 렌더
  if(tab==="self") renderSelf(lastSelf);
  if(tab==="log") renderLogs(loadLogs());
}
function tabFromHash(){
  const h = (location.hash || "#home").replace("#","");
  return (["home","self","log"].includes(h)) ? h : "home";
}
window.addEventListener("hashchange", ()=> setTab(tabFromHash()));
setTab(tabFromHash());

let lastSelf = [];

// 검색창: 자가조치/AS이력 탭에서만 필터 적용
$("#q").addEventListener("input", ()=>{
  const tab = tabFromHash();
  if(tab==="self") renderSelf(lastSelf);
  if(tab==="log") renderLogs(loadLogs());
});

function escapeHtml(str){
  return String(str ?? "")
    .replaceAll("&","&amp;").replaceAll("<","&lt;").replaceAll(">","&gt;")
    .replaceAll('"',"&quot;").replaceAll("'","&#039;");
}

function ensureGvizHook(){
  if(!window.google) window.google = {};
  if(!window.google.visualization) window.google.visualization = {};
  if(!window.google.visualization.Query) window.google.visualization.Query = {};
  if(typeof window.google.visualization.Query.setResponse !== "function"){
    window.google.visualization.Query.setResponse = function(){};
  }
}

function loadSheetByGid(gid){
  return new Promise((resolve, reject) => {
    ensureGvizHook();

    const prev = window.google.visualization.Query.setResponse;
    let done = false;

    const url = `https://docs.google.com/spreadsheets/d/${CONFIG.SHEET_ID}/gviz/tq?gid=${encodeURIComponent(gid)}&tqx=out:json`;

    const script = document.createElement("script");
    const timer = setTimeout(() => {
      cleanup();
      reject(new Error("timeout"));
    }, 12000);

    function cleanup(){
      clearTimeout(timer);
      window.google.visualization.Query.setResponse = prev;
      if(script.parentNode) script.parentNode.removeChild(script);
    }

    window.google.visualization.Query.setResponse = (resp) => {
      if(done) return;
      done = true;
      try{
        cleanup();
        if(!resp || resp.status !== "ok"){
          throw new Error(resp?.errors?.[0]?.message || "load failed");
        }
        const rows = resp.table.rows.map(r => r.c.map(cell => {
          if(!cell) return "";
          const v = (cell.v != null) ? String(cell.v) : "";
          const f = (cell.f != null) ? String(cell.f) : "";
          const p = (cell.p != null) ? JSON.stringify(cell.p) : "";
          const blob = [v, f, p].filter(Boolean).join(" ");
          const m = blob.match(/https?:\/\/[^\s"']+/i);
          if(m) return m[0];
          return f.trim() ? f : v;
        }));
        resolve({ rows });
      }catch(e){
        reject(e);
      }
    };

    script.src = url;
    script.async = true;
    script.onerror = () => { cleanup(); reject(new Error("network")); };
    document.head.appendChild(script);
  });
}

function isLikelyUrl(s){
  const t = String(s||"").trim();
  if(!t) return false;
  if(/^https?:\/\//i.test(t)) return true;
  if(t.includes("docs.google.com") || t.includes("drive.google.com")) return true;
  return false;
}

function findFirstUrlInRow(row){
  const blob = row.map(x => String(x ?? "")).join(" ");
  const m = blob.match(/https?:\/\/[^\s"']+/i);
  return m ? m[0] : "";
}

// A:구분(0) B:제목(1) C:내용(2) D:링크(3) E:키워드(4)
function toObjects(rows){
  const safe = (r,i)=> (i>=0 && i<r.length) ? String(r[i]||"").trim() : "";

  const data = rows.filter(r => r.some(x => String(x).trim() !== ""));

  // ✅ 첫 행이 헤더(제목/내용/키워드)면 제거
  if (data.length){
    const r0 = data[0];
    const isHeader =
      (safe(r0,1)==="제목" && safe(r0,2)==="내용") ||
      (safe(r0,4)==="키워드" && safe(r0,1).includes("제목") && safe(r0,2).includes("내용"));
    if(isHeader) data.shift();
  }

  return data.map((r,idx)=>{
    let type = safe(r,0);
    let title = safe(r,1);
    let content = safe(r,2);
    let link = safe(r,3);
    let tags = safe(r,4);

    if(!isLikelyUrl(link)){
      const found = findFirstUrlInRow(r);
      if(found) link = found;
    }
    if(!isLikelyUrl(link) && isLikelyUrl(type)) { link = type; type = ""; }
    if(!isLikelyUrl(link) && isLikelyUrl(title)) { link = title; title = ""; }

    return { rowNo: idx+2, type, title, content, link, tags };
  });
}

function dedupeByLink(items){
  const map = new Map();
  for(const it of items){
    const key = String(it.link||"").trim();
    if(!key) continue;
    if(!map.has(key)) map.set(key, it);
  }
  return Array.from(map.values());
}

function labelForLink(item, n){
  if(item.title) return item.title;
  try{
    const u = item.link.startsWith("http") ? new URL(item.link) : null;
    if(u) return `${u.hostname} #${n}`;
  }catch(e){}
  return `Link #${n}`;
}

function labelForSelf(item, n){
  if(item.title) return item.title;
  const first = (item.content||"").split("\n").map(x=>x.trim()).filter(Boolean)[0];
  if(first) return first.length > 28 ? first.slice(0,28)+"…" : first;
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
    const href = x.link.startsWith("http") ? x.link : ("https://" + x.link);
    a.href = href;
    a.target = "_blank";
    a.rel = "noopener";
    a.textContent = x.title;
    wrap.appendChild(a);
  });
}

function renderSelf(items){
  const list = $("#selfList");
  const q = $("#q").value.trim().toLowerCase();

  const filtered = items.filter(x=>{
    if(!q) return true;
    const blob = `${x.title} ${x.content} ${x.tags}`.toLowerCase();
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
      ? `<div class="meta">관련 링크: <a href="${x.link.startsWith("http")?x.link:"https://"+x.link}" target="_blank" rel="noopener">${escapeHtml(x.link)}</a></div>`
      : "";

    d.innerHTML = `
      <summary>${escapeHtml(x.title)}</summary>
      ${tagsHtml}
      <div class="content body">${escapeHtml(x.content)}</div>
      ${linkHtml}
    `;
    list.appendChild(d);
  });
}

/* =========================
   AS 이력 (로컬 저장)
========================= */
function nowKstForDatetimeLocal(){
  const d = new Date();
  const kst = new Date(d.getTime() + (9*60*60*1000) - (d.getTimezoneOffset()*60*1000));
  // yyyy-MM-ddTHH:mm
  const pad = (n)=>String(n).padStart(2,"0");
  const yyyy = kst.getFullYear();
  const mm = pad(kst.getMonth()+1);
  const dd = pad(kst.getDate());
  const hh = pad(kst.getHours());
  const mi = pad(kst.getMinutes());
  return `${yyyy}-${mm}-${dd}T${hh}:${mi}`;
}

function loadLogs(){
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    const arr = raw ? JSON.parse(raw) : [];
    return Array.isArray(arr) ? arr : [];
  }catch(e){
    return [];
  }
}
function saveLogs(arr){
  localStorage.setItem(STORAGE_KEY, JSON.stringify(arr));
}
function uid(){
  return Math.random().toString(16).slice(2) + Date.now().toString(16);
}
function fmtWhen(v){
  const s = String(v||"").trim();
  if(!s) return "";
  // datetime-local 형식이면 보기 좋게
  // 2026-01-22T10:30 -> 2026-01-22 10:30
  return s.replace("T"," ");
}
function statusBadge(status){
  const st = String(status||"").trim();
  if(st==="처리완료") return `<span class="badge done">처리완료</span>`;
  if(st==="진행중") return `<span class="badge todo">진행중</span>`;
  return `<span class="badge todo">미처리</span>`;
}

function renderLogs(items){
  const wrap = $("#logTable");
  const q = $("#q").value.trim().toLowerCase();

  const filtered = items.filter(x=>{
    if(!q) return true;
    const blob = `${x.when} ${x.store} ${x.memo} ${x.status}`.toLowerCase();
    return blob.includes(q);
  });

  if(!filtered.length){
    wrap.innerHTML = `<div class="empty">등록된 이력이 없습니다.</div>`;
    return;
  }

  const head = `
    <div class="logrow head">
      <div>일시</div>
      <div>매장명</div>
      <div>상담내용</div>
      <div>처리여부</div>
      <div>관리</div>
    </div>
  `;

  const rows = filtered.map(x=>`
    <div class="logrow">
      <div class="logcell">${escapeHtml(fmtWhen(x.when))}</div>
      <div class="logcell">${escapeHtml(x.store)}</div>
      <div class="logcell wrap">${escapeHtml(x.memo)}</div>
      <div class="logcell">${statusBadge(x.status)}</div>
      <div class="logcell" style="display:flex; gap:8px; flex-wrap:wrap;">
        <button class="iconbtn" data-act="toggle" data-id="${escapeHtml(x.id)}">상태변경</button>
        <button class="iconbtn" data-act="del" data-id="${escapeHtml(x.id)}">삭제</button>
      </div>
    </div>
  `).join("");

  wrap.innerHTML = `<div>${head}${rows}</div>`;

  // 이벤트 위임
  wrap.querySelectorAll("button[data-act]").forEach(btn=>{
    btn.addEventListener("click", ()=>{
      const act = btn.dataset.act;
      const id = btn.dataset.id;
      let logs = loadLogs();

      if(act==="del"){
        logs = logs.filter(x=>x.id!==id);
        saveLogs(logs);
        renderLogs(logs);
        return;
      }

      if(act==="toggle"){
        logs = logs.map(x=>{
          if(x.id!==id) return x;
          const cur = String(x.status||"미처리");
          const next = (cur==="미처리") ? "진행중" : (cur==="진행중" ? "처리완료" : "미처리");
          return { ...x, status: next };
        });
        saveLogs(logs);
        renderLogs(logs);
      }
    });
  });
}

function downloadText(filename, text){
  const blob = new Blob([text], {type:"text/plain;charset=utf-8"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = filename;
  document.body.appendChild(a);
  a.click();
  setTimeout(()=>{ URL.revokeObjectURL(a.href); a.remove(); }, 0);
}

function toCsv(logs){
  const esc = (s)=> `"${String(s??"").replaceAll('"','""')}"`;
  const head = ["일시","매장명","상담내용","처리여부"].map(esc).join(",");
  const body = logs.map(x=>[
    fmtWhen(x.when),
    x.store,
    x.memo,
    x.status
  ].map(esc).join(",")).join("\n");
  return head + "\n" + body;
}

$("#btnSaveLog").addEventListener("click", ()=>{
  const when = $("#logWhen").value.trim();
  const store = $("#logStore").value.trim();
  const memo = $("#logMemo").value.trim();
  const status = $("#logStatus").value;

  if(!when || !store || !memo){
    alert("일시 / 매장명 / 상담내용은 필수입니다.");
    return;
  }

  const logs = loadLogs();
  logs.unshift({ id: uid(), when, store, memo, status, createdAt: Date.now() });
  saveLogs(logs);

  // 입력 초기화(일시는 현재로)
  $("#logWhen").value = nowKstForDatetimeLocal();
  $("#logStore").value = "";
  $("#logMemo").value = "";
  $("#logStatus").value = "미처리";

  renderLogs(logs);
});

$("#btnExportCsv").addEventListener("click", ()=>{
  const logs = loadLogs();
  if(!logs.length){
    alert("내보낼 이력이 없습니다.");
    return;
  }
  downloadText(`AS이력_${new Date().toISOString().slice(0,10)}.csv`, toCsv(logs));
});

$("#btnClearLogs").addEventListener("click", ()=>{
  const logs = loadLogs();
  if(!logs.length) return;
  if(!confirm("전체 이력을 삭제할까요?")) return;
  saveLogs([]);
  renderLogs([]);
});

(function initLogForm(){
  $("#logWhen").value = nowKstForDatetimeLocal();
  renderLogs(loadLogs());
})();

/* =========================
   초기 로딩
========================= */
(async function init(){
  try{
    const raw = await loadSheetByGid(CONFIG.WIRELESS_GID);
    const rows = toObjects(raw.rows);

    const manualRows = dedupeByLink(rows.filter(x => isLikelyUrl(x.link)))
      .map((x,i)=>({ ...x, title: labelForLink(x, i+1) }));

    const selfRowsRaw = rows.filter(x => String(x.content||"").trim() !== "");
    const selfRows = selfRowsRaw.map((x,i)=>({ ...x, title: labelForSelf(x, i+1) }));

    renderManualButtons(manualRows);
    lastSelf = selfRows;
    renderSelf(lastSelf);
  }catch(e){
    renderManualButtons([]);
    lastSelf = [];
    renderSelf(lastSelf);
  }
})();
</script>
</body>
</html>
