# -0.-2
Ответственное мероприятие
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Свадьба Виктора и Анастасии</title>

<!-- PWA -->
<meta name="theme-color" content="#d4a373">

<style>
body {
  margin: 0;
  font-family: 'Georgia', serif;
  background: linear-gradient(to bottom, #fff, #f7efe5);
  text-align: center;
  color: #333;
}

.section {
  padding: 60px 20px;
  opacity: 0;
  transform: translateY(40px);
  transition: 1.2s;
}

.show {
  opacity: 1;
  transform: translateY(0);
}

h1 { font-size: 34px; }
h2 { font-size: 26px; }

img {
  width: 90%;
  max-width: 350px;
  border-radius: 20px;
  margin: 20px 0;
}

.timer {
  font-size: 26px;
}

.buttons {
  margin-top: 20px;
}

.btn {
  padding: 12px 25px;
  margin: 10px;
  border: none;
  border-radius: 25px;
  font-size: 16px;
  cursor: pointer;
}

.yes { background: #6dbf73; color: white; }
.no { background: #e57373; color: white; }

.result {
  margin-top: 15px;
  font-size: 18px;
}

iframe {
  width: 100%;
  height: 250px;
  border-radius: 20px;
}

.open-screen {
  position: fixed;
  width: 100%;
  height: 100%;
  background: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  z-index: 10;
}

.open-btn {
  padding: 15px 30px;
  background: #d4a373;
  color: white;
  border-radius: 30px;
  border: none;
  font-size: 18px;
}
</style>
</head>

<body>

<!-- экран открытия -->
<div class="open-screen" id="start">
  <h1>Приглашение на свадьбу 💍</h1>
  <button class="open-btn" onclick="openInvite()">Открыть</button>
</div>

<div id="content" style="display:none">

<div class="section">
  <h1>Мы долго к этому шли…</h1>
  <h1>И вот — это случилось!</h1>
</div>

<div class="section">
  <h2>Виктор & Анастасия</h2>
</div>

<div class="section">
  <img src="photo1.jpg">
  <img src="photo2.jpg">
</div>

<div class="section">
  <p>📍 ЗАГС, г. Липецк, ул. Зегеля</p>
  <p>📅 25.09.2026</p>
  <p>⏰ 11:00</p>
</div>

<div class="section">
  <h2>До свадьбы осталось:</h2>
  <div class="timer" id="timer"></div>
</div>

<div class="section">
  <iframe src="https://www.google.com/maps?q=ЗАГС+Липецк+Зегеля&output=embed"></iframe>
</div>

<!-- RSVP -->
<div class="section">
  <h2>Вы придёте?</h2>

  <div class="buttons">
    <button class="btn yes" onclick="answer('Буду! 🎉')">Я приду</button>
    <button class="btn no" onclick="answer('Не смогу 😔')">Не смогу</button>
  </div>

  <div class="result" id="result"></div>
</div>

<div class="section">
  <button onclick="playMusic()">Включить музыку 🎶</button>
</div>

</div>

<audio id="music" loop>
  <source src="https://www.bensound.com/bensound-music/bensound-romantic.mp3">
</audio>

<script>
// открытие
function openInvite() {
  document.getElementById('start').style.display = 'none';
  document.getElementById('content').style.display = 'block';
}

// анимации
const sections = document.querySelectorAll('.section');
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('show');
    }
  });
});
sections.forEach(sec => observer.observe(sec));

// таймер
const weddingDate = new Date("2026-09-25T11:00:00").getTime();

setInterval(() => {
  const now = new Date().getTime();
  const diff = weddingDate - now;

  const d = Math.floor(diff / (1000*60*60*24));
  const h = Math.floor((diff / (1000*60*60)) % 24);
  const m = Math.floor((diff / (1000*60)) % 60);

  document.getElementById("timer").innerHTML =
    d + " дней " + h + " часов " + m + " минут";
}, 1000);

// RSVP
function answer(text) {
  localStorage.setItem("weddingAnswer", text);
  document.getElementById("result").innerText = "Ваш ответ: " + text;
}

// загрузка ответа
window.onload = () => {
  const saved = localStorage.getItem("weddingAnswer");
  if (saved) {
    document.getElementById("result").innerText = "Ваш ответ: " + saved;
  }
}

// музыка
function playMusic() {
  document.getElementById('music').play();
}
</script>

</body>
</html>
