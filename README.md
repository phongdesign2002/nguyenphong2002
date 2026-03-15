<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Creative Portfolio | Catalogue • Poster • Video</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<style>
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
z-index:1000;
border-bottom:1px solid rgba(255,255,255,.05);
}

.logo{font-weight:700;letter-spacing:2px;font-size:20px;color:var(--accent)}

nav a{margin-left:30px;text-decoration:none;color:#cfd6ff;font-size:14px;transition:.3s}
nav a:hover{color:var(--accent)}

.hero{height:85vh;display:flex;align-items:center;justify-content:center;text-align:center;padding:0 10%}

.hero h1{
font-size:60px;margin-bottom:20px;
background:linear-gradient(90deg,#4cc9f0,#7b9cff);
-webkit-background-clip:text;
-webkit-text-fill-color:transparent;
}

.hero p{color:var(--sub);font-size:18px}

.hero button{
margin-top:35px;padding:14px 32px;border:none;
background:linear-gradient(90deg,#4cc9f0,#4361ee);
color:white;border-radius:30px;font-size:15px;cursor:pointer;transition:.3s
}

.hero button:hover{transform:translateY(-3px)}

section{padding:90px 10%}

.section-title{font-size:34px;margin-bottom:50px;font-weight:600}

.about{max-width:800px;color:var(--sub);font-size:17px}

.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:30px}

.card{
background:var(--card);
border-radius:14px;
overflow:hidden;
transition:.35s;
position:relative;
border:1px solid rgba(255,255,255,.05);
display:flex;
flex-direction:column;
}

.card:hover{transform:translateY(-8px);box-shadow:0 20px 40px rgba(0,0,0,.5)}

.card img{width:100%;display:block}
.card video{width:100%}

.card .info{padding:18px}
.card .title{font-size:16px;margin-bottom:6px}
.card .tag{font-size:12px;color:var(--accent)}

/* DELETE FOOTER */

.card-footer{
display:flex;
justify-content:flex-end;
align-items:center;
padding:10px 15px;
border-top:1px solid rgba(255,255,255,.05);
}

.delete-btn{
background:none;
border:none;
color:var(--danger);
font-size:18px;
cursor:pointer;
transition:.2s;
display:flex;
align-items:center;
gap:6px;
}

.delete-btn:hover{
transform:scale(1.2);
}

.upload-panel{
margin-bottom:40px;
padding:25px;
background:#0f1629;
border-radius:10px;
border:1px solid rgba(255,255,255,.05);
}

.upload-panel h3{margin-bottom:10px;font-size:18px}

.upload-panel button{
padding:8px 16px;border:none;background:var(--accent);color:#000;border-radius:6px;cursor:pointer
}

.modal{
position:fixed;top:0;left:0;width:100%;height:100%;
background:rgba(0,0,0,.85);
display:none;align-items:center;justify-content:center;
padding:40px;z-index:2000
}

.modal img{max-width:90%;max-height:90%;border-radius:10px}
.modal.show{display:flex}

.contact-box{background:var(--card);padding:40px;border-radius:14px;max-width:600px}
.contact-box p{color:var(--sub)}

footer{margin-top:100px;padding:40px;text-align:center;color:#7d88b8;border-top:1px solid rgba(255,255,255,.05)}

</style>
</head>

<body>

<header>
<div class="logo">PORTFOLIO</div>
<nav>
<a href="#about">About</a>
<a href="#catalogue">Catalogue</a>
<a href="#poster">Poster</a>
<a href="#video">Video</a>
<a href="#contact">Contact</a>
</nav>
</header>

<section class="hero">
<div>
<h1>Creative Design Works</h1>
<p>Catalogue • Poster • Advertising • Video Production</p>
<button onclick="scrollToSection()">View Projects</button>
</div>
</section>

<section id="about">
<h2 class="section-title">About</h2>
<p class="about">Tôi chuyên thiết kế catalogue, poster quảng cáo và sản xuất video truyền thông.</p>
</section>

<section id="catalogue">
<h2 class="section-title">Catalogue Design</h2>

<div class="upload-panel">
<h3>Thêm hình catalogue</h3>
<input type="file" id="catalogueUpload" accept="image/*">
<button onclick="addCatalogue()">Add Image</button>
</div>

<div class="grid" id="catalogueGrid"></div>

</section>

<section id="poster">
<h2 class="section-title">Poster Design</h2>

<div class="upload-panel">
<h3>Thêm poster</h3>
<input type="file" id="posterUpload" accept="image/*">
<button onclick="addPoster()">Add Poster</button>
</div>

<div class="grid" id="posterGrid"></div>

</section>

<section id="video">
<h2 class="section-title">Video Projects</h2>

<div class="upload-panel">
<h3>Thêm video</h3>
<input type="file" id="videoUpload" accept="video/*">
<button onclick="addVideo()">Add Video</button>
</div>

<div class="grid" id="videoGrid"></div>

</section>

<section id="contact">
<h2 class="section-title">Contact</h2>
<div class="contact-box">
<p>Email: yourmail@email.com</p>
<p>Behance: behance.net/yourname</p>
<p>Instagram: instagram.com/yourname</p>
</div>
</section>

<div class="modal" id="modal" onclick="closeModal()">
<img id="modalImg">
</div>

<footer>
© 2026 Creative Portfolio
</footer>

<script>

function scrollToSection(){
document.querySelector('#catalogue').scrollIntoView({behavior:'smooth'})
}

function removeCard(btn){
let card = btn.closest('.card')
card.remove()
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
<button class="delete-btn" onclick="removeCard(this)">🗑</button>
</div>
`

return card
}

function createVideoCard(src){
let card=document.createElement('div')
card.className='card'

card.innerHTML=`
<video controls>
<source src="${src}" type="video/mp4">
</video>
<div class="info">
<div class="title">Video Project</div>
<div class="tag">Video</div>
</div>
<div class="card-footer">
<button class="delete-btn" onclick="removeCard(this)">🗑</button>
</div>
`

return card
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
