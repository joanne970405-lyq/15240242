<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>休息時間做什麼？</title>
<style>
*{box-sizing:border-box}
body{margin:0;min-height:100vh;padding:24px;display:grid;place-items:center;background:#edf1e9;color:#29312d;font-family:"Microsoft JhengHei",sans-serif}
.app{width:min(100%,570px);padding:clamp(24px,6vw,42px);background:#fffefa;border:1px solid #e5ece3;border-radius:24px;box-shadow:0 18px 48px #2b43331c}
.eyebrow{margin:0 0 9px;color:#568b78;font-size:.8rem;font-weight:bold;letter-spacing:.17em}
h1{margin:0;font-size:clamp(2rem,7vw,2.7rem)}
.intro{margin:11px 0 27px;color:#758078;line-height:1.75}
label{display:block;margin-bottom:9px;font-weight:bold}
textarea{display:block;width:100%;min-height:190px;padding:15px;border:1.5px solid #dfe9e1;border-radius:14px;outline:none;font:inherit;line-height:1.9;resize:vertical}
textarea:focus{border-color:#568b78;box-shadow:0 0 0 4px #568b7820}
.hint{margin:8px 0 20px;color:#758078;font-size:.85rem}
button{width:100%;padding:15px;border:0;border-radius:14px;background:#568b78;color:white;font:inherit;font-size:1.05rem;font-weight:bold;cursor:pointer}
button:hover{background:#3d705e}
.result{margin-top:22px;min-height:155px;padding:23px 18px;display:grid;place-items:center;text-align:center;border:1px dashed #b9d2c2;border-radius:16px;background:#edf5ef}
.result-label{margin:0 0 10px;color:#758078;font-size:.82rem;font-weight:bold;letter-spacing:.14em}
#resultText{margin:0;color:#3d705e;font-size:clamp(1.4rem,5.5vw,1.9rem);font-weight:900;line-height:1.45;overflow-wrap:anywhere}
#resultText.empty{color:#758078;font-size:1rem;font-weight:600}
.status{margin:14px 0 0;color:#758078;font-size:.85rem;text-align:center}
</style>
</head>
<body>
<main class="app">
<p class="eyebrow">A LITTLE BREAK PICKER</p>
<h1>休息時間做什麼？</h1>
<p class="intro">不必把每段空檔都安排得很完美，抽一件小事，讓腦袋換個頻道。</p>
<label for="options">今天可以做的事</label>
<textarea id="options" spellcheck="false">聽三首喜歡的歌
到窗邊看看外面
喝水，順便走動一下
整理桌面五分鐘
看一小段有趣的影片
讀幾頁想看的書
畫一張隨手塗鴉
寫下現在腦中的三件事
伸展肩頸和手腕
找朋友聊聊天
到戶外散步一圈
閉上眼睛休息一下</textarea>
<p class="hint">每行一個活動，可自行新增、刪除或替換。</p>
<button id="drawButton" type="button">幫我決定！</button>
<section class="result" aria-live="polite" aria-atomic="true">
<div><p class="result-label">YOUR LITTLE BREAK</p><p id="resultText" class="empty">等待靈感降落⋯</p></div>
</section>
<p id="status" class="status">準備好就抽一件小事吧！</p>
</main>
<script>
const optionsInput=document.getElementById("options");
const drawButton=document.getElementById("drawButton");
const resultText=document.getElementById("resultText");
const statusText=document.getElementById("status");

function getValidOptions(){
  const lines=optionsInput.value.split(/\r?\n/);
  return [...new Set(lines.map(item=>item.trim()).filter(item=>item.length>0))];
}

function drawActivity(){
  const options=getValidOptions();
  if(options.length===0){
    resultText.textContent="請先輸入至少一個活動";
    resultText.classList.add("empty");
    statusText.textContent="目前沒有可以抽選的活動。";
    return;
  }
  const randomIndex=Math.floor(Math.random()*options.length);
  resultText.textContent=options[randomIndex];
  resultText.classList.remove("empty");
  statusText.textContent=`本次從 ${options.length} 個有效活動中抽出，祝你休息愉快！`;
}
drawButton.addEventListener("click",drawActivity);
</script>
</body>
</html>
