<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Creative Portfolio | Persistence & Search & Zoom</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
/* --- CORE STYLE --- */
*{margin:0;padding:0;box-sizing:border-box}
body{
    font-family:'Inter', sans-serif;
    color:white;
    background:radial-gradient(circle at top,#1c2f6b 0%,#0b1435 40%,#050a18 100%);
    min-height:100vh;
    overflow-x:hidden;
}

/* --- VIEW-ONLY MODE --- */
body.view-only .admin-btn, 
body.view-only .delete-file, 
body.view-only .delete-project,
body.view-only input[type="file"],
body.view-only .hero-media button { 
    display: none !important; 
}

header{
    display:flex; align-items:center; justify-content:space-between; padding:20px 8%;
    border-bottom:1px solid rgba(255,255,255,.08); background: rgba(5, 10, 24, 0.9);
    backdrop-filter: blur(12px); position: sticky; top: 0; z-index: 100;
}
.header-left{display:flex;align-items:center;gap:15px;}
.logo{font-weight:700;font-size:22px;color:#4cc9f0;cursor:pointer;letter-spacing: 1px;}
.avatar{width:45px;height:45px;border-radius:50%;overflow:hidden;border:2px solid rgba(76, 201, 240, 0.5);cursor:pointer;position:relative;background:#222;}
.avatar img{width:100%;height:100%;object-fit:cover;}
.avatar input{display:none}
.avatar button{position:absolute;bottom:-5px;right:-5px;background:#ff4d6d;border:none;width:20px;height:20px;border-radius:50%;color:white;cursor:pointer;font-size:10px;display:flex;align-items:center;justify-content:center;}

.container { width: 100%; max-width: 1200px; margin: 0 auto; padding: 0 5%; }

.page { display: none; opacity: 0; padding: 40px 0 80px 0; }
.page.active { display: block; animation: fadeInPage 0.6s cubic-bezier(0.2, 0.8, 0.2, 1) forwards; }
@keyframes fadeInPage { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

.hero{text-align:center; padding: 40px 0 60px 0;}
.hero-media{max-width:850px; margin:30px auto; position:relative; border-radius: 15px; overflow: hidden; box-shadow: 0 20px 60px rgba(0,0,0,0.6);}
.hero-media img, .hero-media video{width:100%; display: block; aspect-ratio:16/9; object-fit:cover;}
.hero-media button{position:absolute;top:15px;right:15px;background:#ff4d6d;border:none;width:32px;height:32px;border-radius:50%;color:white;cursor:pointer;z-index:10;}

.about{max-width:750px; margin:0 auto 80px auto; text-align: center;}
.about p{color:#9aa4c7; margin-top:20px; line-height:1.8; font-size: 1.1rem; font-weight: 300;}

.category-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:30px; margin-bottom: 60px;}
.category{background:rgba(17, 24, 51, 0.6); padding:60px 30px; border-radius:18px; text-align:center; cursor:pointer; transition:all 0.4s ease; border: 1px solid rgba(255,255,255,0.05);}
.category:hover{transform:translateY(-12px); border-color: #4cc9f0; background:rgba(22, 31, 66, 0.8);}
.category span{font-size:55px; display:block; margin-bottom:15px;}

/* --- SEARCH BOX --- */
.search-box {
    margin-bottom: 35px;
    padding: 20px;
    background: rgba(76, 201, 240, 0.04);
    border-radius: 15px;
    border: 1px solid rgba(76, 201, 240, 0.15);
}
.search-box input { width: 100%; border: 1px solid #4cc9f0 !important; font-size: 16px; background: #1e264d; color: white; padding: 14px; border-radius: 10px; outline: none; }

.project-folder{ background:rgba(17, 24, 51, 0.8); padding:35px; border-radius:20px; margin-top:40px; border: 1px solid rgba(255,255,255,0.03);}
.project-header{display:flex; justify-content:space-between; align-items:center; margin-bottom:30px; gap: 20px;}
.project-media{ display:grid; grid-template-columns:repeat(auto-fill, minmax(200px, 1fr)); gap:18px; margin-top:25px;}
.media-item{position:relative; border-radius: 12px; overflow: hidden; background: #000;}
.media-item img, .media-item video{width:100%; cursor:pointer; aspect-ratio:1/1; object-fit:cover; display: block; transition: 0.3s;}
.media-item:hover img, .media-item:hover video { transform: scale(1.08); }

.delete-file{position:absolute; top:8px; right:8px; background:#ff4d6d; border:none; width:26px; height:26px; border-radius:50%; color:white; cursor:pointer; z-index:5; font-size: 12px; display:flex; align-items:center; justify-content:center;}

.btn{background:#4cc9f0; border:none; padding:12px 24px; border-radius:10px; cursor:pointer; font-weight:700; color:#050a18; transition: .3s;}
input[type="text"] { background: #1e264d; border: 1px solid #333; color: white; padding: 12px; border-radius: 10px; outline: none;}

/* --- VIEWER NÂNG CAO --- */
.viewer{ position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.98); display:none; align-items:center; justify-content:center; z-index:9999; overflow: hidden;}
.viewer.active{ display:flex; }
#viewerContainer { width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; cursor: grab; }
#viewerContainer:active { cursor: grabbing; }
#viewerContent { transition: transform 0.1s ease-out; transform-origin: center; display: flex; align-items: center; justify-content: center; }
#viewerContent img, #viewerContent video { max-width: 90vw; max-height: 90vh; box-shadow: 0 0 50px rgba(0,0,0,1); pointer-events: none; }
.viewer-arrow{position:absolute; top:50%; transform:translateY(-50%); font-size:45px; background:rgba(255,255,255,0.05); width: 65px; height: 65px; border-radius: 50%; border:none; color:white; cursor:pointer; z-index: 10001; display:flex; align-items:center; justify-content:center;}
.viewer-back{position:absolute; top:30px; left:30px; color:white; background:rgba(255,255,255,0.1); border:none; cursor:pointer; padding: 10px 20px; border-radius: 30px; z-index: 10001;}

/* --- SECRET DOTS --- */
.secret-controls { margin-top: 30px; display: flex; justify-content: center; gap: 20px; }
.dot-trigger { color: rgba(76, 201, 240, 0.15); cursor: pointer; font-size: 24px; font-weight: bold; user-select: none; transition: 0.3s; }
.dot-trigger:hover { color: #4cc9f0; }

footer{margin-top:100px; padding:80px 0; border-top:1px solid rgba(255,255,255,.05); text-align:center;}

/* --- BỔ SUNG: RESPONSIVE CHO DI ĐỘNG --- */
@media screen and (max-width: 768px) {
    header { padding: 15px 5%; }
    .logo { font-size: 18px; }
    .avatar { width: 38px; height: 38px; }
    .container { padding: 0 4%; }
    .hero h1 { font-size: 24px; }
    .hero-media { margin: 20px auto; }
    .about p { font-size: 1rem; }
    .category-grid { grid-template-columns: 1fr; gap: 15px; }
    .category { padding: 40px 20px; }
    .admin-btn[style*="display: flex"] { flex-direction: column; }
    .project-header { flex-direction: column; align-items: flex-start; gap: 10px; }
    .project-media { grid-template-columns: repeat(auto-fill, minmax(130px, 1fr)); gap: 10px; }
    .viewer-arrow { width: 45px; height: 45px; font-size: 25px; background: rgba(0,0,0,0.4); }
    .viewer-arrow[style*="left:30px"] { left: 10px !important; }
    .viewer-arrow[style*="right:30px"] { right: 10px !important; }
    .dot-trigger { padding: 15px; font-size: 32px; } /* Dễ chạm hơn trên mobile */
    #viewerContent img, #viewerContent video { max-width: 95vw; max-height: 80vh; }
}
</style>
</head>

<body>

<header>
    <div class="header-left">
        <div class="logo" onclick="goHome()">PORTFOLIO</div>
        <label class="avatar" title="Đổi ảnh đại diện">
            <input type="file" onchange="addAvatar(this)">
            <img id="avatarImg" src="">
            <button class="admin-btn" onclick="removeAvatar(event)">✕</button>
        </label>
    </div>
    <button id="exitViewBtn" class="btn" style="display:none; background:#ff4d6d; color:white;" onclick="exitViewMode()">Thoát Chế độ Xem</button>
</header>

<div class="container">

    <div class="page active" id="home">
        <section class="hero">
            <h1>Creative Portfolio</h1>
            <div class="admin-btn" style="margin-top: 25px;">
                <input type="file" id="heroUpload" multiple style="margin-bottom: 15px; display: block; margin-left: auto; margin-right: auto;">
                <button class="btn" onclick="addHero()">+ Add Showcase Media</button>
            </div>
            <div id="heroContainer"></div>
        </section>
        
        <section class="about">
            <h2>About Me</h2>
            <p>Graphic Designer chuyên sâu về hệ thống nhận diện, Poster quảng cáo và Sản xuất Video. Với lối tư duy tối giản và tập trung vào trải nghiệm thị giác.</p>
        </section>

        <section class="category-grid">
            <div class="category" onclick="openPage('posterPage')"><span>🖼</span>Poster Design</div>
            <div class="category" onclick="openPage('printPage')"><span>📦</span>Print Design</div>
            <div class="category" onclick="openPage('videoPage')"><span>🎬</span>Video Projects</div>
        </section>
    </div>

    <div class="page" id="posterPage">
        <div onclick="goHome()" style="cursor:pointer; color:#4cc9f0; margin-bottom:20px; font-weight:600;">← Back to Dashboard</div>
        <h2>Poster Collection</h2>
        <div class="search-box">
            <input type="text" id="posterSearch" placeholder="🔍 Tìm nhanh dự án theo ngành hàng (F&B, Tech, Medical...)" onkeyup="searchProjects('poster')">
        </div>
        <div class="admin-btn" style="display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 30px;">
            <input placeholder="Tên khách hàng" id="posterClient" type="text" style="flex: 1;">
            <input placeholder="Ngành hàng" id="posterIndustry" type="text" style="flex: 1;">
            <button class="btn" onclick="createProject('poster')">Tạo thư mục dự án</button>
        </div>
        <div id="posterProjects"></div>
    </div>

    <div class="page" id="printPage">
        <div onclick="goHome()" style="cursor:pointer; color:#4cc9f0; margin-bottom:20px; font-weight:600;">← Back to Dashboard</div>
        <h2>Print & Packaging</h2>
        <div class="search-box">
            <input type="text" id="printSearch" placeholder="🔍 Tìm nhanh dự án theo ngành hàng..." onkeyup="searchProjects('print')">
        </div>
        <div class="admin-btn" style="display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 30px;">
            <input placeholder="Tên khách hàng" id="printClient" type="text" style="flex: 1;">
            <input placeholder="Ngành hàng" id="printIndustry" type="text" style="flex: 1;">
            <button class="btn" onclick="createProject('print')">Tạo thư mục dự án</button>
        </div>
        <div id="printProjects"></div>
    </div>

    <div class="page" id="videoPage">
        <div onclick="goHome()" style="cursor:pointer; color:#4cc9f0; margin-bottom:20px; font-weight:600;">← Back to Dashboard</div>
        <h2>Video Production</h2>
        <div class="search-box">
            <input type="text" id="videoSearch" placeholder="🔍 Tìm nhanh dự án theo ngành hàng..." onkeyup="searchProjects('video')">
        </div>
        <div class="admin-btn" style="display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 30px;">
            <input placeholder="Tên khách hàng" id="videoClient" type="text" style="flex: 1;">
            <input placeholder="Ngành hàng" id="videoIndustry" type="text" style="flex: 1;">
            <button class="btn" onclick="createProject('video')">Tạo thư mục dự án</button>
        </div>
        <div id="videoProjects"></div>
    </div>

    <footer>
        <h3>Contact for Work</h3>
        <p>Email: yourmail@gmail.com | Phone: 0123 456 789</p>
        <p>&copy; 2026 Designed for Creators.</p>
        <div class="secret-controls">
            <span class="dot-trigger admin-btn" title="Xuất file" onclick="exportPortfolio()">.</span>
            <span class="dot-trigger" title="Mở file" onclick="document.getElementById('importFile').click()">..</span>
            <input type="file" id="importFile" style="display:none" accept=".json" onchange="importPortfolio(this)">
        </div>
    </footer>
</div>

<div id="viewer" class="viewer">
    <button class="viewer-back" onclick="closeViewer()">✕ Close (Esc)</button>
    <button class="viewer-arrow" style="left:30px" onclick="prevMedia()">❮</button>
    <div id="viewerContainer"><div id="viewerContent"></div></div>
    <button class="viewer-arrow" style="right:30px" onclick="nextMedia()">❯</button>
</div>

<script>
/** DATABASE **/
let db;
const request = indexedDB.open("PortfolioCompleteDB", 1);
request.onupgradeneeded = (e) => {
    db = e.target.result;
    db.createObjectStore("media", { keyPath: "id" });
    db.createObjectStore("projects", { keyPath: "id" });
};
request.onsuccess = (e) => { db = e.target.result; loadData(); checkMode(); };

function saveToDB(store, data) {
    if(document.body.classList.contains('view-only')) return;
    db.transaction(store, "readwrite").objectStore(store).put(data);
}

/** ZOOM & PAN (Desktop & Mobile) **/
let scale = 1, isDragging = false, startX, startY, translateX = 0, translateY = 0, lastTouchDist = 0;
const vContent = document.getElementById("viewerContent");
const vContainer = document.getElementById("viewerContainer");

// Mouse Wheel Zoom
document.getElementById("viewer").onwheel = (e) => {
    e.preventDefault();
    scale = Math.min(Math.max(.5, scale + (e.deltaY > 0 ? -0.2 : 0.2)), 5);
    updateTransform();
};

// Mouse Events
vContainer.onmousedown = (e) => { isDragging = true; startX = e.clientX - translateX; startY = e.clientY - translateY; };
window.onmousemove = (e) => { if (!isDragging) return; translateX = e.clientX - startX; translateY = e.clientY - startY; updateTransform(); };
window.onmouseup = () => isDragging = false;

// Touch Events (Hỗ trợ cảm ứng trên điện thoại)
vContainer.addEventListener('touchstart', e => {
    if (e.touches.length === 1) {
        isDragging = true; startX = e.touches[0].clientX - translateX; startY = e.touches[0].clientY - translateY;
    } else if (e.touches.length === 2) {
        lastTouchDist = Math.hypot(e.touches[0].pageX - e.touches[1].pageX, e.touches[0].pageY - e.touches[1].pageY);
    }
}, { passive: false });

vContainer.addEventListener('touchmove', e => {
    if (isDragging && e.touches.length === 1) {
        translateX = e.touches[0].clientX - startX; translateY = e.touches[0].clientY - startY; updateTransform();
    } else if (e.touches.length === 2) {
        const dist = Math.hypot(e.touches[0].pageX - e.touches[1].pageX, e.touches[0].pageY - e.touches[1].pageY);
        scale = Math.min(Math.max(.5, scale * (dist / lastTouchDist)), 5);
        updateTransform(); lastTouchDist = dist;
    }
    if(e.touches.length > 0) e.preventDefault();
}, { passive: false });

vContainer.addEventListener('touchend', () => { isDragging = false; lastTouchDist = 0; });

function updateTransform() { vContent.style.transform = `translate(${translateX}px, ${translateY}px) scale(${scale})`; }
function resetTransform() { scale = 1; translateX = 0; translateY = 0; updateTransform(); }

/** TÌM KIẾM **/
function searchProjects(type) {
    let input = document.getElementById(type + 'Search').value.toLowerCase();
    let container = document.getElementById(type + 'Projects');
    let folders = container.getElementsByClassName('project-folder');
    for (let i = 0; i < folders.length; i++) {
        let label = folders[i].querySelector('.industry-label').innerText.toLowerCase();
        folders[i].style.display = label.includes(input) ? "" : "none";
    }
}

/** PROJECT & MEDIA **/
function createProject(type, exId=null, exC=null, exI=null) {
    const id = exId || type + "_" + Date.now();
    const client = exC || document.getElementById(type + "Client").value;
    const industry = exI || document.getElementById(type + "Industry").value;
    if (!client && !exId) return;
    if (!exId) saveToDB("projects", { id, type, client, industry });

    const container = document.getElementById(type + "Projects");
    const folder = document.createElement("div"); folder.className = "project-folder"; folder.id = id;
    folder.innerHTML = `
        <div class="project-header">
            <div><b style="font-size:22px; color:#4cc9f0">${client}</b><div class="industry-label" style="color:#9aa4c7; font-size:15px;">Ngành hàng: ${industry}</div></div>
            <button class="btn delete-project admin-btn" style="background:#ff4d6d; color:white; padding:8px 16px; font-size:12px" onclick="deleteProject('${id}')">Xóa dự án</button>
        </div>
        <div class="admin-btn" style="background:rgba(255,255,255,0.02); padding:18px; border-radius:12px; margin-bottom:20px; border: 1px solid rgba(255,255,255,0.05)">
            <p style="font-size:13px; color:#4cc9f0; margin-bottom:10px; font-weight:600">Thêm tệp cho dự án:</p>
            <input type="file" multiple onchange="addMedia(event, '${id}')">
        </div>
        <div class="project-media"></div>
    `;
    container.prepend(folder);
    if(!exId){ document.getElementById(type+"Client").value=""; document.getElementById(type+"Industry").value=""; }
}

function addMedia(e, pId) {
    for (let f of e.target.files) {
        const reader = new FileReader();
        reader.onload = (ev) => {
            const item = { id: "m_"+Date.now()+Math.random(), projectId: pId, data: ev.target.result, type: f.type.startsWith("video")?"video":"image" };
            saveToDB("media", item); renderMedia(item);
        };
        reader.readAsDataURL(f);
    }
}

function renderMedia(item) {
    const folder = document.getElementById(item.projectId); if(!folder) return;
    const div = document.createElement("div"); div.className = "media-item"; div.id = item.id;
    const m = item.type === "video" ? document.createElement("video") : document.createElement("img");
    m.src = item.data; m.onclick = () => openViewer(div);
    const del = document.createElement("button"); del.className = "delete-file admin-btn"; del.innerHTML = "✕";
    del.onclick = (e) => { e.stopPropagation(); div.remove(); removeFromDB("media", item.id); };
    div.append(m, del); folder.querySelector(".project-media").append(div);
}

function deleteProject(id) {
    if(confirm("Xóa dự án này?")) {
        document.getElementById(id).remove();
        db.transaction("projects", "readwrite").objectStore("projects").delete(id);
        const tx = db.transaction("media", "readwrite");
        tx.objectStore("media").openCursor().onsuccess = (e) => {
            const c = e.target.result; if(c){ if(c.value.projectId === id) c.delete(); c.continue(); }
        };
    }
}

/** AVATAR & HERO **/
function addAvatar(input) {
    const reader = new FileReader();
    reader.onload = (e) => {
        document.getElementById("avatarImg").src = e.target.result;
        saveToDB("media", { id: "avatar", data: e.target.result });
    };
    reader.readAsDataURL(input.files[0]);
}
function removeAvatar(e) { e.preventDefault(); document.getElementById("avatarImg").src = ""; removeFromDB("media", "avatar"); }

function addHero() {
    const files = document.getElementById("heroUpload").files;
    for (let f of files) {
        const reader = new FileReader();
        reader.onload = (e) => {
            const item = { id: "hero_"+Date.now()+Math.random(), data: e.target.result, type: f.type.startsWith("video")?"video":"image" };
            saveToDB("media", item); renderHero(item);
        };
        reader.readAsDataURL(f);
    }
}
function renderHero(item) {
    const wrap = document.createElement("div"); wrap.className = "hero-media"; wrap.id = item.id;
    const m = item.type === "video" ? document.createElement("video") : document.createElement("img");
    if(item.type === "video") m.controls = true; m.src = item.data;
    const del = document.createElement("button"); del.innerHTML = "✕";
    del.onclick = () => { wrap.remove(); removeFromDB("media", item.id); };
    wrap.append(m, del); document.getElementById("heroContainer").append(wrap);
}

/** EXPORT / IMPORT **/
async function exportPortfolio() {
    const data = { media: [], projects: [] };
    const getS = (s) => new Promise(res => db.transaction(s,"readonly").objectStore(s).getAll().onsuccess = e => res(e.target.result));
    data.media = await getS("media"); data.projects = await getS("projects");
    const a = document.createElement("a");
    a.href = URL.createObjectURL(new Blob([JSON.stringify(data)], {type:"application/json"}));
    a.download = "Portfolio_Export.json"; a.click();
}

function importPortfolio(input) {
    const reader = new FileReader();
    reader.onload = (e) => {
        const data = JSON.parse(e.target.result);
        if(confirm("Tải dữ liệu này vào trình duyệt?")) {
            const clearStore = (s) => db.transaction(s,"readwrite").objectStore(s).clear();
            clearStore("media"); clearStore("projects");
            data.media.forEach(m => db.transaction("media","readwrite").objectStore("media").put(m));
            data.projects.forEach(p => db.transaction("projects","readwrite").objectStore("projects").put(p));
            window.location.reload();
        }
    };
    reader.readAsText(input.files[0]);
}

/** SYSTEM **/
function loadData() {
    db.transaction("media").objectStore("media").get("avatar").onsuccess = e => { if(e.target.result) document.getElementById("avatarImg").src = e.target.result.data; };
    db.transaction("projects").objectStore("projects").openCursor().onsuccess = e => {
        const c = e.target.result; if(c){ createProject(c.value.type, c.value.id, c.value.client, c.value.industry); c.continue(); }
        else {
            db.transaction("media").objectStore("media").openCursor().onsuccess = ev => {
                const m = ev.target.result; if(m){
                    if(m.value.id.startsWith("hero_")) renderHero(m.value);
                    else if(m.value.projectId) renderMedia(m.value);
                    m.continue();
                }
            };
        }
    };
}

function checkMode() { if (new URLSearchParams(window.location.search).get('mode') === 'view') { document.body.classList.add('view-only'); document.getElementById('exitViewBtn').style.display = 'block'; } }
function exitViewMode() { window.location.href = window.location.pathname; }
function removeFromDB(s, id) { if(!document.body.classList.contains('view-only')) db.transaction(s, "readwrite").objectStore(s).delete(id); }
function goHome() { document.querySelectorAll(".page").forEach(p=>{p.classList.remove("active"); p.style.display="none";}); document.getElementById("home").style.display="block"; setTimeout(()=>document.getElementById("home").classList.add("active"),10); }
function openPage(id) { document.querySelectorAll(".page").forEach(p=>{p.classList.remove("active"); p.style.display="none";}); document.getElementById(id).style.display="block"; setTimeout(()=>document.getElementById(id).classList.add("active"),10); }

let mediaList = []; let currentIndex = 0;
function openViewer(el) {
    mediaList = [...el.parentElement.querySelectorAll(".media-item img, .media-item video")];
    currentIndex = mediaList.indexOf(el.querySelector("img, video"));
    resetTransform(); showMedia();
    document.getElementById("viewer").style.display = "flex";
    setTimeout(() => document.getElementById("viewer").classList.add("active"), 10);
}
function showMedia() {
    resetTransform(); const content = document.getElementById("viewerContent"); content.innerHTML = "";
    let clone = mediaList[currentIndex].cloneNode(true); if(clone.tagName === "VIDEO") clone.controls = true;
    content.appendChild(clone);
}
function closeViewer() { document.getElementById("viewer").classList.remove("active"); setTimeout(() => document.getElementById("viewer").style.display = "none", 400); }
function nextMedia() { currentIndex = (currentIndex + 1) % mediaList.length; showMedia(); }
function prevMedia() { currentIndex = (currentIndex - 1 + mediaList.length) % mediaList.length; showMedia(); }

window.onkeydown = (e) => {
    if(e.key === "Escape") closeViewer();
    if(document.getElementById("viewer").style.display === "flex") {
        if(e.key === "ArrowRight") nextMedia();
        if(e.key === "ArrowLeft") prevMedia();
    }
};
</script>
</body>
</html>
