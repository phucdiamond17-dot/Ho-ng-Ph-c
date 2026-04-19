<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>🔥 TOOL GPT Baccarat VIP</title>

<style>
body{
  background:linear-gradient(#081421,#0d2b4d);
  color:#fff;
  font-family:Arial;
  text-align:center;
}

/* HEADER */
.header{
  background:linear-gradient(to right,#0d2b4d,#1f4f7a);
  padding:15px;
  font-size:22px;
  font-weight:bold;
}

/* BUTTON */
.btn{
  padding:15px;
  margin:8px;
  font-size:16px;
  border:none;
  border-radius:12px;
  width:110px;
  color:#fff;
  box-shadow:0 3px 8px rgba(0,0,0,0.4);
}
.b{background:#1976D2}
.p{background:#D32F2F}
.t{background:#388E3C}

/* BAR */
.bar{
  width:85%;
  height:18px;
  margin:15px auto;
  background:#333;
  border-radius:20px;
}
.fill{
  height:100%;
  background:linear-gradient(to right,red,blue);
  width:50%;
  border-radius:20px;
}

/* CARD */
.card{
  background:#0f2238;
  margin:12px;
  padding:12px;
  border-radius:12px;
  box-shadow:0 0 10px rgba(0,0,0,0.5);
}

/* GRID (cầu) */
.grid{
  display:grid;
  grid-template-columns: repeat(12, 24px);
  gap:6px;
  justify-content:center;
  margin-top:10px;
}
.cell{
  width:24px;
  height:24px;
  border-radius:50%;
}

/* ALERT */
.warn{
  background:#ff9800;
  padding:10px;
  border-radius:8px;
  margin-top:8px;
  color:#000;
}
.good{
  background:#4CAF50;
  padding:10px;
  border-radius:8px;
  margin-top:8px;
}

/* RESET */
.reset{
  margin-top:15px;
  padding:10px 20px;
  border:none;
  border-radius:8px;
}
</style>
</head>

<body>

<div class="header">🔥 TOOL GPT Baccarat VIP</div>

<div>
  <button class="btn b" onclick="add('B')">BANKER</button>
  <button class="btn t" onclick="add('T')">TIE</button>
  <button class="btn p" onclick="add('P')">PLAYER</button>
</div>

<div class="bar"><div id="bar" class="fill"></div></div>
<div id="percent">P 50% - B 50%</div>

<div class="card">
  <div id="suggest">👉 Đang phân tích...</div>
  <div id="warn"></div>
</div>

<div class="card">
  <div>📊 Bảng cầu</div>
  <div class="grid" id="grid"></div>
</div>

<button class="reset" onclick="reset()">RESET</button>

<script>
let data = JSON.parse(localStorage.getItem("bac")||"[]");

function save(){
  localStorage.setItem("bac",JSON.stringify(data));
}

function add(x){
  data.push(x);
  if(data.length>100)data.shift();
  save();
  render();
}

function reset(){
  data=[];
  save();
  render();
}

/* AI */
function analyze(){
  let last=data.slice(-20);

  let b=last.filter(x=>x=="B").length;
  let p=last.filter(x=>x=="P").length;
  let total=b+p;

  if(total==0)return [50,50,"CHỜ",""];

  let pb=Math.round((p/total)*100);
  let bb=100-pb;

  let streak=1;
  for(let i=data.length-1;i>0;i--){
    if(data[i]==data[i-1]) streak++;
    else break;
  }

  let suggest="BỎ";
  let warn="";

  if(streak>=4){
    warn="⚠️ Cầu bệt " + streak;
  }

  if(pb>65){
    suggest="🔥 NÊN PLAYER";
  }else if(bb>65){
    suggest="🔥 NÊN BANKER";
  }else if(streak>=3){
    suggest="⚡ Theo cầu: " + data[data.length-1];
  }

  return [pb,bb,suggest,warn];
}

function render(){
  let [p,b,s,w]=analyze();

  percent.innerText=`P ${p}% - B ${b}%`;
  bar.style.width=p+"%";
  suggest.innerText=s;

  let warnBox=document.getElementById("warn");
  if(w){
    warnBox.className="warn";
    warnBox.innerText=w;
  }else{
    warnBox.className="";
    warnBox.innerText="";
  }

  let grid=document.getElementById("grid");
  grid.innerHTML="";

  data.forEach(x=>{
    let d=document.createElement("div");
    d.className="cell";

    if(x=="B") d.style.background="#2196F3";
    if(x=="P") d.style.background="#f44336";
    if(x=="T") d.style.background="#4CAF50";

    grid.appendChild(d);
  });
}

render();
</script>

</body>
</html>
