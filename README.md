<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Creative Portfolio</title>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<style>
/* --- RESPONSIVE HANDLES (MOBILE) --- */
@media screen and (max-width: 768px) {
    /* Header & Logo */
    header { padding: 15px 5%; }
    .logo { font-size: 18px; }
    .avatar { width: 35px; height: 35px; }

    /* Container padding */
    .container { padding: 0 4%; }

    /* Hero section */
    .hero { padding: 20px 0 40px 0; }
    .hero h1 { font-size: 24px; }
    .hero-media button { width: 28px; height: 28px; top: 10px; right: 10px; font-size: 10px; }

    /* About section */
    .about { margin-bottom: 50px; }
    .about h2 { font-size: 20px; }
    .about p { font-size: 1rem; line-height: 1.6; }

    /* Category Grid (Trang chủ) */
    .category-grid { gap: 15px; grid-template-columns: 1fr; } /* Chuyển thành 1 cột trên mobile */
    .category { padding: 30px 20px; }
    .category span { font-size: 40px; }

    /* Page Titles */
    .page h2 { font-size: 20px; margin-bottom: 15px; }

    /* Search Box & Admin Controls */
    .search-box { padding: 15px; margin-bottom: 20px; }
    .search-box input { padding: 10px; font-size: 14px; }
    
    /* Phần input tạo dự án */
    .admin-btn[style*="flex-wrap: wrap"] { gap: 8px !important; flex-direction: column; }
    .admin-btn[style*="flex-wrap: wrap"] input { width: 100%; }

    /* Project Folder */
    .project-folder { padding: 20px; margin-top: 25px; }
    .project-header { flex-direction: column; align-items: flex-start; gap: 10px; }
    .project-header b { font-size: 18px !important; }
    
    /* Upload media input trong dự án */
    .project-folder .admin-btn { padding: 12px; }

    /* Grid ảnh dự án */
    .project-media { grid-template-columns: repeat(auto-fill, minmax(130px, 1fr)); gap: 10px; }
    .delete-file { width: 22px; height: 22px; font-size: 10px; top: 5px; right: 5px; }

    /* Viewer (Trình xem ảnh) */
    .viewer-back { top: 15px; left: 15px; padding: 8px 15px; font-size: 12px; }
    .viewer-arrow { width: 40px; height: 40px; font-size: 25px; background: rgba(0,0,0,0.5); }
    .viewer-arrow[style*="left:30px"] { left: 10px !important; }
    .viewer-arrow[style*="right:30px"] { right: 10px !important; }
    #viewerContent img, #viewerContent video { max-width: 95vw; max-height: 80vh; }

    /* Footer */
    footer { margin-top: 60px; padding: 40px 0; }
    footer h3 { font-size: 18px; }
    footer p { font-size: 14px; }
}
:root{
--bg:#070b14;
--card:#0f1629;
--accent:#4cc9f0;
--danger:#ff4d6d;
--text:#ffffff;
--sub:#9aa4c7;
}

*{margin:0;padding:0;box-sizing:border-box}

body{
font-family:'Inter',sans-serif;
background:radial-gradient(circle at top,#111a35,#05070f);
color:var(--text);
line-height:1.6;
}

header{
position:sticky;
top:0;
backdrop-filter:blur(10px);
background:rgba(10,15,30,.6);
padding:25px 8%;
display:flex;
justify-content:space-between;
align-items:center;
border-bottom:1px solid rgba(255,255,255,.05);
}

.logo{
font-weight:700;
letter-spacing:2px;
font-size:20px;
color:var(--accent)
}

nav a{
margin-left:30px;
text-decoration:none;
color:#cfd6ff;
font-size:14px;
}

nav a:hover{color:var(--accent)}

section{padding:90px 10%}

.section-title{
font-size:34px;
margin-bottom:40px;
}

.hero{
text-align:center;
}

.hero h1{
font-size:58px;
margin-bottom:15px;
background:linear-gradient(90deg,#4cc9f0,#7b9cff);
-webkit-background-clip:text;
-webkit-text-fill-color:transparent;
}

.hero p{
color:var(--sub);
margin-bottom:30px
}

.hero-image{
max-width:1000px;
margin:auto;
border-radius:14px;
overflow:hidden;
position:relative;
}

.hero-image img{
width:100%;
aspect-ratio:16/9;
object-fit:cover;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
gap:30px
}

.card{
background:var(--card);
border-radius:14px;
overflow:hidden;
border:1px solid rgba(255,255,255,.05);
display:flex;
flex-direction:column;
}

.card img{
width:100%;
cursor:pointer
}

.card video{
width:100%
}

.card .info{
padding:18px
}

.card-footer{
display:flex;
justify-content:flex-end;
padding:10px 15px;
border-top:1px solid rgba(255,255,255,.05);
}

.action-btn{
background:none;
border:none;
cursor:pointer;
font-size:18px;
margin-left:10px
}

.delete-btn{color:var(--danger)}
.edit-btn{color:var(--accent)}

.upload-panel{
margin-bottom:40px;
padding:25px;
background:#0f1629;
border-radius:10px;
border:1px solid rgba(255,255,255,.05);
}

.upload-panel input{
margin-top:10px
}

.upload-panel button{
margin-top:10px;
padding:8px 16px;
border:none;
background:var(--accent);
color:#000;
border-radius:6px;
cursor:pointer
}

.experience-list{
max-width:800px
}

.exp-item{
background:var(--card);
padding:25px;
border-radius:10px;
margin-bottom:20px;
border:1px solid rgba(255,255,255,.05);
}

.exp-role{font-weight:600;font-size:18px}
.exp-company{color:var(--accent)}
.exp-time{color:var(--sub);margin-bottom:10px}

.exp-actions{
margin-top:10px
}

.modal{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,.9);
display:none;
align-items:center;
justify-content:center;
z-index:2000
}

.modal img{
max-width:90%;
max-height:90%
}

.modal.show{display:flex}

footer{
margin-top:100px;
padding:40px;
text-align:center;
color:#7d88b8;
border-top:1px solid rgba(255,255,255,.05)
}

</style>
</head>

<body>

<header>

<div class="logo">PORTFOLIO</div>

<nav>
<a href="#experience">Experience</a>
<a href="#catalogue">Catalogue</a>
<a href="#poster">Poster</a>
<a href="#logo">Logo</a>
<a href="#video">Video</a>
</nav>

</header>


<section class="hero">

<h1>Creative Design Portfolio</h1>
<p>Catalogue • Poster • Advertising • Video Production</p>

<div class="upload-panel">

<h3>Thêm ảnh tiêu đề (16:9)</h3>

<input type="file" id="heroUpload" accept="image/*">

<br>

<button onclick="addHeroImage()">Add Cover Image</button>

</div>

<div class="hero-image" id="heroImageContainer"></div>

</section>


<section id="experience">

<h2 class="section-title">Kinh nghiệm làm việc</h2>

<div class="upload-panel">

<h3>Thêm kinh nghiệm</h3>

<input type="text" id="expRole" placeholder="Vị trí">

<br>

<input type="text" id="expCompany" placeholder="Công ty">

<br>

<input type="text" id="expTime" placeholder="Thời gian">

<br>

<button onclick="addExperience()">Add Experience</button>

</div>

<div class="experience-list" id="experienceList"></div>

</section>


<section id="catalogue">

<h2 class="section-title">Catalogue Design</h2>

<div class="upload-panel">

<input type="file" id="catalogueUpload" accept="image/*">

<button onclick="addCatalogue()">Add Image</button>

</div>

<div class="grid" id="catalogueGrid"></div>

</section>


<section id="poster">

<h2 class="section-title">Poster Design</h2>

<div class="upload-panel">

<input type="file" id="posterUpload" accept="image/*">

<button onclick="addPoster()">Add Poster</button>

</div>

<div class="grid" id="posterGrid"></div>

</section>


<section id="logo">

<h2 class="section-title">Logo Design</h2>

<div class="upload-panel">

<input type="file" id="logoUpload" accept="image/*">

<button onclick="addLogo()">Add Logo</button>

</div>

<div class="grid" id="logoGrid"></div>

</section>


<section id="video">

<h2 class="section-title">Video Projects</h2>

<div class="upload-panel">

<input type="file" id="videoUpload" accept="video/*">

<button onclick="addVideo()">Add Video</button>

</div>

<div class="grid" id="videoGrid"></div>

</section>


<div class="modal" id="modal" onclick="closeModal()">
<img id="modalImg">
</div>

<footer>
© 2026 Creative Portfolio
</footer>


<script>

function removeCard(btn){
btn.closest('.card').remove()
}

function createImageCard(src){

let card=document.createElement('div')

card.className='card'

card.innerHTML=`

<img src="${src}" onclick="openModal('${src}')">

<div class="info">
<div class="title">Design Work</div>
<div class="tag">Image</div>
</div>

<div class="card-footer">
<button class="delete-btn action-btn" onclick="removeCard(this)">🗑</button>
</div>
`

return card

}

function createVideoCard(src){

let card=document.createElement('div')

card.className='card'

card.innerHTML=`

<video controls>
<source src="${src}">
</video>

<div class="info">
<div class="title">Video Project</div>
<div class="tag">Video</div>
</div>

<div class="card-footer">
<button class="delete-btn action-btn" onclick="removeCard(this)">🗑</button>
</div>
`

return card

}

function addHeroImage(){

let file=document.getElementById('heroUpload').files[0]
if(!file) return

let url=URL.createObjectURL(file)

document.getElementById('heroImageContainer').innerHTML=`
<img src="${url}">
<button class="delete-btn action-btn"
style="position:absolute;top:10px;right:10px"
onclick="removeHero()">🗑</button>`
}

function removeHero(){
document.getElementById('heroImageContainer').innerHTML=''
}

function addExperience(){

let role=document.getElementById('expRole').value
let company=document.getElementById('expCompany').value
let time=document.getElementById('expTime').value

let item=document.createElement('div')

item.className='exp-item'

item.innerHTML=`

<div class="exp-role">${role}</div>
<div class="exp-company">${company}</div>
<div class="exp-time">${time}</div>

<div class="exp-actions">

<button class="edit-btn action-btn" onclick="editExperience(this)">✏</button>

<button class="delete-btn action-btn" onclick="deleteExperience(this)">🗑</button>

</div>
`

document.getElementById('experienceList').appendChild(item)

}

function deleteExperience(btn){
btn.closest('.exp-item').remove()
}

function editExperience(btn){

let item=btn.closest('.exp-item')

let role=item.querySelector('.exp-role').innerText
let company=item.querySelector('.exp-company').innerText
let time=item.querySelector('.exp-time').innerText

let newRole=prompt("Edit Role",role)
let newCompany=prompt("Edit Company",company)
let newTime=prompt("Edit Time",time)

if(newRole) item.querySelector('.exp-role').innerText=newRole
if(newCompany) item.querySelector('.exp-company').innerText=newCompany
if(newTime) item.querySelector('.exp-time').innerText=newTime

}

function addCatalogue(){
let file=document.getElementById('catalogueUpload').files[0]
if(!file) return
let url=URL.createObjectURL(file)
let card=createImageCard(url)
document.getElementById('catalogueGrid').appendChild(card)
}

function addPoster(){
let file=document.getElementById('posterUpload').files[0]
if(!file) return
let url=URL.createObjectURL(file)
let card=createImageCard(url)
document.getElementById('posterGrid').appendChild(card)
}

function addLogo(){
let file=document.getElementById('logoUpload').files[0]
if(!file) return
let url=URL.createObjectURL(file)
let card=createImageCard(url)
document.getElementById('logoGrid').appendChild(card)
}

function addVideo(){
let file=document.getElementById('videoUpload').files[0]
if(!file) return
let url=URL.createObjectURL(file)
let card=createVideoCard(url)
document.getElementById('videoGrid').appendChild(card)
}

function openModal(src){
let modal=document.getElementById('modal')
let img=document.getElementById('modalImg')
img.src=src
modal.classList.add('show')
}

function closeModal(){
document.getElementById('modal').classList.remove('show')
}

</script>

</body>
</html>
