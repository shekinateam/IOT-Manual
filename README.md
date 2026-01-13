
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
    }
    @media (max-width: 420px){
      .brand{padding:10px;}
      .brand h1{font-size:14px;}
      .btnrow{grid-template-columns: 1fr;}
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
        <h1>IoT AS 매뉴얼</h1>
        <p>Support</p>
      </div>
    </div>
    <nav class="nav">
      <a href="#home" data-tab="home" class="active">🏠 홈 <span class="chip">Links</span></a>
      <a href="#self" data-tab="self">🧯 자가조치 <span class="chip">Guide</span></a>
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
  </main>
</div>

<script>
const CONFIG = {
  SHEET_ID: "14actQ-pC6cLXRlqNzS1F0AVuUTAdJC4K_hhq7rOyBX4",
  WIRELESS_GID: "890902374",
};

const $ = (q)=>document.querySelector(q);
const $$ = (q)=>Array.from(document.querySelectorAll(q));

function setTab(tab){
  $$(".nav a").forEach(a=>a.classList.toggle("active", a.dataset.tab===tab));
  $$(".section").forEach(s=>s.classList.remove("active"));
  const sec = $("#tab-"+tab);
  if(sec) sec.classList.add("active");
}
function tabFromHash(){
  const h = (location.hash || "#home").replace("#","");
  return (["home","self"].includes(h)) ? h : "home";
}
window.addEventListener("hashchange", ()=> setTab(tabFromHash()));
setTab(tabFromHash());

let lastSelf = [];
$("#q").addEventListener("input", ()=>renderSelf(lastSelf));

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
  return rows
    .filter(r => r.some(x => String(x).trim() !== ""))
    .map((r,idx)=>{
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
    a.href = x.link.startsWith("http") ? x.link : ("https://" + x.link);
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
      <div class="content">${escapeHtml(x.content)}</div>
      ${linkHtml}
    `;
    list.appendChild(d);
  });
}

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
