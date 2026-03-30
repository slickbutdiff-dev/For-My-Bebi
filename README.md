<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Scrolling Text Centered</title>
<style>
  html, body {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    font-family: Arial, sans-serif;
  }
  body {
    background-image: url('https://media.giphy.com/media/3ohA2ZD9EkeK2AyfdK/giphy.gif');
    background-size: cover;
    background-position: center;
  }
  .container {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
    width: 100%;
  }
  .scroll-container {
    width: 80%;
    margin: auto;
    overflow: hidden;
    white-space: nowrap;
    margin-bottom: 20px;
  }
  #scrollText {
    display: inline-block;
    color: red;
    font-size: 2em;
    font-weight: bold;
    padding-left: 100%;
    animation: scroll-left 10s linear infinite;
    text-shadow: 2px 2px 4px black;
  }
  @keyframes scroll-left {
    0% { transform: translateX(0%); }
    100% { transform: translateX(-100%); }
  }
  #yesBtn, #noBtn {
    padding: 12px 24px;
    font-size: 1.2em;
    border: none;
    border-radius: 8px;
    font-weight: bold;
    cursor: pointer;
    position: fixed;
    z-index: 10;
  }
  #yesBtn {
    background-color: pink;
    left: 45%;
    top: 70%;
  }
  #noBtn {
    background-color: lightgray;
    left: 55%;
    top: 70%;
  }
  .heart {
    position: absolute;
    color: red;
    font-size: 24px;
    animation: floatUp 3s linear forwards;
  }
  @keyframes floatUp {
    0% { transform: translateY(0) scale(1); opacity: 1; }
    100% { transform: translateY(-200px) scale(1.5); opacity: 0; }
  }
  #sadMessage, #sadMessage2 {
    position: fixed;
    left: 50%;
    transform: translateX(-50%);
    color: white;
    font-size: 2em;
    font-weight: bold;
    text-shadow: 2px 2px 4px black;
    display: none;
    pointer-events: none;
  }
  #sadMessage { bottom: 80px; }
  #sadMessage2 { top: 80px; }
</style>
</head>
<body>

<div class="container">
  <div class="scroll-container">
    <div id="scrollText">
      Bati Na Tayo Please &nbsp;&nbsp;&nbsp;Bati Na Tayo Please &nbsp;&nbsp;&nbsp;Bati Na Tayo Please &nbsp;&nbsp;&nbsp;Bati Na Tayo Please
    </div>
  </div>
</div>

<button id="yesBtn">Yes</button>
<button id="noBtn">No</button>

<div id="sadMessage">Please say yes na bebi ☹️</div>
<div id="sadMessage2">Dali na pooo! ☹️</div>

<script>
const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const text = document.getElementById("scrollText");
const sadMessage = document.getElementById("sadMessage");
const sadMessage2 = document.getElementById("sadMessage2");

let noHoverCount = 0;
let noClickCount = 0;

// Move No button randomly
function moveNoButton() {
  const yesRect = yesBtn.getBoundingClientRect();
  let x, y;
  do {
    x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
    y = Math.random() * (window.innerHeight - noBtn.offsetHeight - 50);
  } while (
    x + noBtn.offsetWidth > yesRect.left &&
    x < yesRect.right &&
    y + noBtn.offsetHeight > yesRect.top &&
    y < yesRect.bottom
  );
  noBtn.style.left = x + "px";
  noBtn.style.top = y + "px";
}

function handleNo() {
  noHoverCount++;
  const total = noHoverCount + noClickCount;

  if (total >= 3 && total < 6) {
    sadMessage.style.display = "block";
    sadMessage.style.fontSize = "2em";
  } else if (total >= 6) {
    sadMessage.style.display = "block";
    sadMessage.style.fontSize = (2 + (total - 6) * 0.3) + "em";
    sadMessage2.style.display = "block";
    sadMessage2.style.fontSize = (2 + (total - 6) * 0.3) + "em";
  }

  // Limit scroll text repetition
  const maxRepeats = 10;
  const baseText = "Bati Na Tayo Please &nbsp;&nbsp;&nbsp;";
  const repeats = text.innerHTML.split(baseText).length - 1;
  if (repeats < maxRepeats) text.innerHTML += baseText;

  moveNoButton();
}

noBtn.addEventListener("mouseover", handleNo);
noBtn.addEventListener("click", () => { noClickCount++; handleNo(); });

yesBtn.addEventListener("click", () => {
  sadMessage.style.display = "none";
  sadMessage2.style.display = "none";
  text.innerHTML = "YESYESYES!! I LOVE YOU SO MUCH BEBII!! &nbsp;&nbsp;&nbsp;YESYESYES!! I LOVE YOU SO MUCH BEBII!! &nbsp;&nbsp;&nbsp;YESYESYES!! I LOVE YOU SO MUCH BEBII!!";
  document.body.style.backgroundImage = "url('https://media.tenor.com/j3MVp-l8upYAAAAM/luvyou-love.gif')";
});
</script>

</body>
</html>
