[index.html](https://github.com/user-attachments/files/30613474/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, viewport-fit=cover">
<title>ARCADE NOCTURNO</title>
<style>

body{margin:0; background:#05060f; font-family:Georgia,'Times New Roman',serif;}
#arcadeHome{min-height:100vh; padding:26px 14px 50px; color:#e9e4d8;
  background:radial-gradient(ellipse at 50% -10%, #1a1d3a 0%, #05060f 60%);}
#arcadeHome .ah-in{max-width:900px; margin:0 auto;}
#arcadeHome h1{text-align:center; margin:14px 0 2px; font-size:clamp(26px,6vw,44px);
  letter-spacing:.3em; font-weight:normal; color:#f3ecd9;
  text-shadow:0 0 24px rgba(150,140,255,.5);}
#arcadeHome .ah-sub{text-align:center; color:#8f8aa8; font-style:italic;
  font-size:.85rem; margin:0 0 26px;}
.ah-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:14px;}
.ah-card{background:rgba(16,18,36,.85); border:1px solid #262a4d; border-radius:14px;
  padding:18px 16px; text-align:center; transition:transform .15s, box-shadow .15s;
  cursor:pointer;}
.ah-card:active{transform:scale(.98);}
.ah-ic{font-size:2.2rem; margin-bottom:6px;}
.ah-card h2{margin:0; font-size:1rem; letter-spacing:.2em; font-weight:normal;}
.ah-card p{margin:6px 0 12px; font-size:.75rem; color:#8f8aa8; font-style:italic; min-height:2.2em;}
.ah-card button{padding:10px 34px; font-family:inherit; font-size:.85rem; letter-spacing:.2em;
  border-radius:8px; border:1px solid; background:transparent; cursor:pointer;}
.ah-md h2, .ah-md button{color:#d9a05c;} .ah-md button{border-color:#8e2f39; box-shadow:0 0 14px rgba(142,47,57,.35);}
.ah-fl h2, .ah-fl button{color:#3ee08a;} .ah-fl button{border-color:#1a5c3f; box-shadow:0 0 14px rgba(62,224,138,.25);}
.ah-nc h2, .ah-nc button{color:#b9a8ff;} .ah-nc button{border-color:#5c4fa8; box-shadow:0 0 14px rgba(150,140,255,.3);}
.ah-hm h2, .ah-hm button{color:#e8dcc0;} .ah-hm button{border-color:#8a7d66;}
.ah-c4 h2, .ah-c4 button{color:#ffd75e;} .ah-c4 button{border-color:#a8862a; box-shadow:0 0 14px rgba(255,215,94,.2);}
.ah-vt h2, .ah-vt button{color:#8fd8ff;} .ah-vt button{border-color:#2a6a8a; box-shadow:0 0 14px rgba(120,200,255,.25);}
.game-container{display:none; min-height:100vh;}
.game-container.active{display:block;}
#arcadeBack{position:fixed; top:10px; left:10px; z-index:300; display:none;
  width:40px; height:40px; border-radius:50%; border:1px solid rgba(255,255,255,.35);
  background:rgba(10,12,26,.7); color:#fff; font-size:18px; cursor:pointer;
  backdrop-filter:blur(3px);}
#arcadeBack.on{display:block;}
#game-md main, #game-fl main{padding-top:52px;}
#game-nc #nc_hud{left:60px;}

/* ===== MURDOKU ===== */
#game-md{
    --bg:#14100e; --panel:#1e1815; --line:#3a2e26;
    --cream:#e8dcc8; --dim:#a5988a; --wine:#8e2f39; --gold:#c9a35c;
  }
#game-md *{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}
#game-md{
    margin:0; background:var(--bg); color:var(--cream);
    font-family:Georgia,'Times New Roman',serif; line-height:1.5;
  }
#game-md main{max-width:640px; margin:0 auto; padding:16px 12px 60px;}
#game-md h1{
    text-align:center; letter-spacing:.35em; margin:10px 0 2px;
    font-size:1.9rem; color:var(--gold); font-weight:normal;
  }
#game-md .sub{text-align:center; color:var(--dim); font-style:italic; font-size:.85rem; margin:0 0 18px;}
#game-md section{
    background:var(--panel); border:1px solid var(--line);
    border-radius:8px; padding:14px; margin-bottom:14px;
  }
#game-md h2{
    font-size:.8rem; letter-spacing:.2em; text-transform:uppercase;
    color:var(--gold); margin:0 0 10px; font-weight:normal;
    border-bottom:1px solid var(--line); padding-bottom:6px;
  }
#game-md #md_intro{font-size:.95rem;}
#game-md ol#md_clues{margin:0; padding-left:22px; font-size:.92rem;}
#game-md ol#md_clues li{margin-bottom:6px; cursor:pointer;}
#game-md ol#md_clues li.done{opacity:.4; text-decoration:line-through;}
#game-md .hint{color:var(--dim); font-size:.78rem; margin:8px 0 0;}
#game-md table{border-collapse:collapse; width:100%; margin-bottom:16px;}
#game-md caption{
    text-align:left; font-size:.75rem; letter-spacing:.15em;
    text-transform:uppercase; color:var(--dim); padding-bottom:4px;
  }
#game-md th, #game-md td{border:1px solid var(--line); text-align:center;}
#game-md th{font-size:.62rem; font-weight:normal; color:var(--dim); padding:4px 2px; word-break:break-word;}
#game-md th.rowh{text-align:left; padding-left:6px; font-size:.72rem; color:var(--cream);}
#game-md td.cell{
    height:40px; min-width:40px; cursor:pointer; font-size:1.1rem;
    user-select:none;
  }
#game-md td.cell.x{color:var(--wine);}
#game-md td.cell.v{color:#7fae6f;}
#game-md textarea{
    width:100%; min-height:80px; background:var(--bg); color:var(--cream);
    border:1px solid var(--line); border-radius:6px; padding:8px;
    font-family:inherit; font-size:.9rem;
  }
#game-md select{
    width:100%; padding:9px; margin-bottom:8px; background:var(--bg);
    color:var(--cream); border:1px solid var(--line); border-radius:6px;
    font-family:inherit; font-size:.95rem;
  }
#game-md label{font-size:.75rem; color:var(--dim); text-transform:uppercase; letter-spacing:.1em;}
#game-md button{
    display:block; width:100%; padding:12px; margin-top:6px;
    background:var(--wine); color:var(--cream); border:none; border-radius:6px;
    font-family:inherit; font-size:1rem; letter-spacing:.08em; cursor:pointer;
  }
#game-md button.alt{background:transparent; border:1px solid var(--gold); color:var(--gold);}
#game-md button:active{transform:scale(.98);}
#game-md #md_verdict{margin-top:10px; padding:10px; border-radius:6px; display:none; font-size:.95rem;}
#game-md #md_verdict.bad{display:block; background:#2a1518; border:1px solid var(--wine);}
#game-md #md_verdict.good{display:block; background:#17231a; border:1px solid #4d6b45;}
#game-md #md_gen{ text-align:center; color:var(--dim); padding:30px 0; display:none; }
/* ===== HUNDIR LA FLOTA ===== */
#game-fl{
    --bg:#04080d; --panel:#081420; --line:#123047;
    --green:#3ee08a; --green-dim:#1a5c3f; --amber:#ffb648;
    --red:#ff4d4d; --blue:#3fa9f5; --text:#cfe8dd; --dim:#5f7d74;
  }
#game-fl *{box-sizing:border-box; -webkit-tap-highlight-color:transparent; user-select:none;}
#game-fl{margin:0; background:var(--bg); color:var(--text);
    font-family:"SF Mono",Menlo,Consolas,monospace; overflow-x:hidden;}
#game-fl::after{
    content:""; position:fixed; inset:0; pointer-events:none; z-index:50;
    background:repeating-linear-gradient(0deg, rgba(0,0,0,.18) 0 1px, transparent 1px 3px);
    mix-blend-mode:multiply;
  }
#game-fl main{max-width:520px; margin:0 auto; padding:10px 8px 40px;}
#game-fl .screen{display:none;}
#game-fl .screen.on{display:block; animation:fadein .4s;}
@keyframes fadein{from{opacity:0; transform:translateY(8px);} to{opacity:1;}}
#game-fl /* ---------- Menú ---------- */
  #fl_radarWrap{position:relative; width:210px; height:210px; margin:22px auto 8px;}
#game-fl #fl_radar{
    width:100%; height:100%; border-radius:50%;
    border:2px solid var(--green-dim);
    background:
      radial-gradient(circle, transparent 0 24%, rgba(62,224,138,.06) 25% 25.5%, transparent 26% 49%,
        rgba(62,224,138,.06) 50% 50.5%, transparent 51% 74%, rgba(62,224,138,.06) 75% 75.5%, transparent 76%),
      linear-gradient(0deg, transparent 49.6%, rgba(62,224,138,.1) 50%, transparent 50.4%),
      linear-gradient(90deg, transparent 49.6%, rgba(62,224,138,.1) 50%, transparent 50.4%),
      radial-gradient(circle, #0a1f16 0%, #050d09 80%);
    box-shadow:0 0 40px rgba(62,224,138,.15), inset 0 0 30px rgba(0,0,0,.6);
    position:relative; overflow:hidden;
  }
#game-fl #fl_radar::before{
    content:""; position:absolute; inset:0; border-radius:50%;
    background:conic-gradient(from 0deg, rgba(62,224,138,.55), transparent 70deg, transparent 360deg);
    animation:sweep 3.4s linear infinite;
  }
@keyframes sweep{to{transform:rotate(360deg);}}
#game-fl .blip{position:absolute; width:6px; height:6px; border-radius:50%;
    background:var(--green); box-shadow:0 0 8px var(--green);
    animation:blip 3.4s linear infinite;}
@keyframes blip{0%,8%{opacity:1;} 60%,100%{opacity:.05;}}
#game-fl h1{text-align:center; margin:6px 0 0; font-size:1.5rem; letter-spacing:.3em; color:var(--green);
     text-shadow:0 0 12px rgba(62,224,138,.5); font-weight:normal;}
#game-fl .tag{text-align:center; color:var(--dim); font-size:.72rem; margin:6px 14px 18px; font-style:italic;}
#game-fl button{
    display:block; width:100%; padding:13px; margin:9px 0;
    background:var(--panel); color:var(--green); border:1px solid var(--line);
    border-radius:4px; font-family:inherit; font-size:.95rem; letter-spacing:.15em;
    cursor:pointer; transition:all .15s;
  }
#game-fl button:active{transform:scale(.98); background:#0d2233;}
#game-fl button.primary{border-color:var(--green-dim); box-shadow:0 0 14px rgba(62,224,138,.12);}
#game-fl button.warn{color:var(--amber); border-color:#5c4218;}
#game-fl button.resume{color:var(--amber); border-color:#5c4218; animation:pulse 2s infinite;}
#game-fl button:disabled{opacity:.35;}
#game-fl .row{display:flex; gap:8px;}
#game-fl .row button{flex:1;}
#game-fl .panel{background:var(--panel); border:1px solid var(--line); border-radius:4px;
    padding:10px; margin-bottom:10px; position:relative;}
#game-fl .panel h2{margin:0 0 8px; font-size:.68rem; letter-spacing:.25em; color:var(--amber);
    font-weight:normal; border-bottom:1px solid var(--line); padding-bottom:5px;}
#game-fl .duo{display:flex; gap:8px; margin-bottom:10px; align-items:stretch;}
#game-fl .duo .panel{flex:1; margin-bottom:0; padding:8px; min-width:0;}
#game-fl .duo .panel h2{font-size:.58rem; letter-spacing:.15em;}
#game-fl .mini .board{gap:1px; padding:2px;}
#game-fl .mini .c.hit::after, #game-fl .mini .c.sunk::after{font-size:min(2.6vw,10px);}
#game-fl #fl_log{font-size:.62rem; max-height:150px; overflow-y:auto; line-height:1.6;}
#game-fl #fl_log div{border-left:2px solid var(--line); padding-left:7px; margin-bottom:2px;}
#game-fl #fl_log .g{border-color:var(--green); color:var(--green);}
#game-fl #fl_log .r{border-color:var(--red); color:#ff9a9a;}
#game-fl #fl_log .a{border-color:var(--amber); color:var(--amber);}
#game-fl /* ---------- Tableros ---------- */
  .boardwrap{display:grid; grid-template-columns:auto 1fr; gap:2px;}
#game-fl .collabels, #game-fl .rowlabels{display:grid; font-size:.55rem; color:var(--dim);}
#game-fl .collabels{grid-template-columns:repeat(10,1fr); grid-column:2; text-align:center; margin-bottom:2px;}
#game-fl .rowlabels{grid-template-rows:repeat(10,1fr); align-items:center; padding-right:3px; text-align:right;}
#game-fl .board{display:grid; grid-template-columns:repeat(10,1fr); gap:2px; aspect-ratio:1;
    background:#03121c; padding:3px; border:1px solid var(--line); border-radius:3px;}
#game-fl .c{position:relative; background:#07202f; border-radius:2px; min-height:0; cursor:pointer;
     transition:background .15s;}
#game-fl .board.enemy .c:not(.miss):not(.hit):not(.sunk):active{background:#0f3a52;}
#game-fl .c.ship{background:linear-gradient(135deg,#20515f,#153845); box-shadow:inset 0 0 0 1px #2e6e80;}
#game-fl .c.miss{background:#07202f;}
#game-fl .c.miss::after{content:""; position:absolute; inset:32%; border-radius:50%;
    background:var(--blue); opacity:.55; box-shadow:0 0 6px var(--blue);}
#game-fl .c.hit{background:#3a1010;}
#game-fl .c.hit::after{content:"✕"; position:absolute; inset:0; display:grid; place-items:center;
    color:var(--red); font-size:min(4vw,15px); text-shadow:0 0 8px var(--red);}
#game-fl .c.sunk{background:#571414; box-shadow:inset 0 0 0 1px var(--red);}
#game-fl .c.sunk::after{content:"✕"; position:absolute; inset:0; display:grid; place-items:center;
    color:#ffb0b0; font-size:min(4vw,15px);}
#game-fl .c.preview{background:#1c4d33;}
#game-fl .c .fx{position:absolute; inset:0; border-radius:50%; pointer-events:none;}
#game-fl .fx.splash{border:2px solid var(--blue); animation:ring .6s ease-out forwards;}
#game-fl .fx.boom{background:radial-gradient(circle,#ffd27a 0%,#ff5722 45%,transparent 70%);
    animation:boom .5s ease-out forwards;}
@keyframes ring{from{transform:scale(.2); opacity:1;} to{transform:scale(1.9); opacity:0;}}
@keyframes boom{0%{transform:scale(.2); opacity:1;} 60%{transform:scale(1.4); opacity:.9;}
    100%{transform:scale(1.8); opacity:0;}}
@keyframes shake{0%,100%{transform:translate(0);} 25%{transform:translate(-3px,1px);}
    50%{transform:translate(3px,-1px);} 75%{transform:translate(-2px,-1px);}}
#game-fl .shake{animation:shake .3s;}
#game-fl #fl_turnbar{display:flex; justify-content:space-between; align-items:center; gap:6px;
    padding:8px 10px; margin-bottom:10px; background:var(--panel);
    border:1px solid var(--line); border-radius:4px; font-size:.72rem;}
#game-fl #fl_turnState{letter-spacing:.1em; text-align:center; flex:1;}
#game-fl #fl_turnState.you{color:var(--green); text-shadow:0 0 8px rgba(62,224,138,.5);}
#game-fl #fl_turnState.foe{color:var(--amber); animation:pulse 1s infinite;}
@keyframes pulse{50%{opacity:.45;}}
#game-fl #fl_sndBtn{width:auto; margin:0; padding:5px 8px; font-size:.7rem;}
#game-fl .fleetlist{display:flex; flex-wrap:wrap; gap:6px;}
#game-fl .chip{padding:7px 10px; border:1px solid var(--line); border-radius:3px; font-size:.7rem;
    color:var(--text); cursor:pointer; background:#0a1a28;}
#game-fl .chip.sel{border-color:var(--green); color:var(--green); box-shadow:0 0 8px rgba(62,224,138,.25);}
#game-fl .chip.placed{opacity:.35; text-decoration:line-through;}
#game-fl .status{display:flex; flex-wrap:wrap; gap:5px; font-size:.62rem;}
#game-fl .st{padding:4px 7px; border:1px solid var(--line); border-radius:3px; color:var(--dim); cursor:pointer;}
#game-fl .st:active{background:#0d2233; border-color:var(--green-dim);}
#game-fl .st.dead{color:var(--red); border-color:#5c1818; text-decoration:line-through;}
#game-fl .shipcells{display:flex; gap:5px; justify-content:center; margin:6px 0 14px;}
#game-fl .shipcells span{width:30px; height:30px; border-radius:3px;
    background:linear-gradient(135deg,#20515f,#153845); box-shadow:inset 0 0 0 1px #2e6e80;}
#game-fl .shipcells span.dmg{background:#571414; box-shadow:inset 0 0 0 1px var(--red);}
#game-fl .h2sub{font-size:.62rem; color:var(--dim); margin:6px 0 0;}
#game-fl /* ---------- Overlays ---------- */
  .overlay{position:fixed; inset:0; display:none; place-items:center;
    background:rgba(2,6,10,.94); z-index:100; padding:20px;}
#game-fl .overlay.on{display:grid;}
#game-fl .obox{max-width:340px; width:100%; text-align:center; border:1px solid var(--line);
    background:var(--panel); border-radius:6px; padding:26px 20px; animation:fadein .5s;}
#game-fl .obox h2{font-size:1.1rem; letter-spacing:.25em; margin:0 0 10px; color:var(--amber);
    border:none; font-weight:normal;}
#game-fl .obox h2.win{color:var(--green); text-shadow:0 0 16px rgba(62,224,138,.7);}
#game-fl .obox h2.lose{color:var(--red); text-shadow:0 0 16px rgba(255,77,77,.6);}
#game-fl .obox p{font-size:.78rem; color:var(--dim); margin:0 0 16px; line-height:1.6;}
#game-fl .statrow{display:flex; justify-content:space-between; font-size:.78rem;
    padding:7px 4px; border-bottom:1px solid var(--line);}
#game-fl .statrow b{color:var(--green); font-weight:normal;}
/* ===== NOCTIS ===== */
#game-nc *{box-sizing:border-box; -webkit-tap-highlight-color:transparent; user-select:none; touch-action:none;}
#game-nc{margin:0; height:100%; background:#05060f; overflow:hidden;
    font-family:Georgia,'Times New Roman',serif; color:#e8e0d0;}
#game-nc #nc_cv{position:fixed; inset:0; width:100%; height:100%; display:block;}
#game-nc .ui{position:fixed; z-index:10;}
#game-nc #nc_hud{top:10px; left:14px; font-size:13px; letter-spacing:.08em; opacity:.92;
    text-shadow:0 2px 8px rgba(0,0,0,.8); pointer-events:none; line-height:1.5;}
#game-nc #nc_hud b{color:#ffc46b; font-weight:normal;}
#game-nc #nc_hud .hp{color:#ff6b6b;}
#game-nc #nc_hud .um{color:#b9a8ff;}
#game-nc #nc_sndBtn{top:8px; right:12px; background:rgba(10,12,26,.5); color:#e8e0d0;
    border:1px solid rgba(255,255,255,.15); border-radius:8px; padding:7px 12px;
    font-size:15px; z-index:11;}
#game-nc .pad{bottom:calc(14px + env(safe-area-inset-bottom)); width:74px; height:74px;
    border-radius:50%; background:rgba(20,24,48,.35); border:1.5px solid rgba(255,255,255,.22);
    color:rgba(255,255,255,.85); font-size:26px; display:grid; place-items:center;
    backdrop-filter:blur(2px);}
#game-nc .pad:active, #game-nc .pad.on{background:rgba(255,196,107,.25); border-color:#ffc46b;}
#game-nc #nc_btnL{left:calc(16px + env(safe-area-inset-left));}
#game-nc #nc_btnR{left:calc(104px + env(safe-area-inset-left));}
#game-nc #nc_btnC{left:calc(60px + env(safe-area-inset-left)); width:58px; height:58px; font-size:20px;
    bottom:calc(104px + env(safe-area-inset-bottom));}
#game-nc #nc_btnJ{right:calc(16px + env(safe-area-inset-right)); width:86px; height:86px; font-size:17px;
    letter-spacing:.1em;}
#game-nc #nc_btnA{right:calc(112px + env(safe-area-inset-right)); width:64px; height:64px; font-size:24px;
    bottom:calc(26px + env(safe-area-inset-bottom));}
#game-nc #nc_wheel{position:fixed; inset:0; z-index:15; display:none; background:rgba(3,4,10,.35);}
#game-nc #nc_wheel.on{display:block;}
#game-nc .wopt{position:fixed; width:58px; height:58px; border-radius:50%;
    background:rgba(20,24,48,.85); border:2px solid rgba(255,255,255,.3);
    color:#f5edda; font-size:23px; display:grid; place-items:center;
    transform:translate(-50%,-50%); transition:transform .08s, border-color .08s;}
#game-nc .wopt small{position:absolute; bottom:-17px; left:50%; transform:translateX(-50%);
    font-size:9px; letter-spacing:.1em; color:#b9b2cc; white-space:nowrap;}
#game-nc .wopt.sel{transform:translate(-50%,-50%) scale(1.25); border-color:#ffc46b;
    background:rgba(255,196,107,.3); box-shadow:0 0 20px rgba(255,196,107,.5);}
#game-nc .overlay{position:fixed; inset:0; z-index:20; display:none; place-items:center;
    background:rgba(3,4,10,.6); text-align:center; padding:16px;}
#game-nc .overlay.on{display:grid;}
#game-nc .overlay h1{font-size:clamp(28px,7vw,52px); letter-spacing:.35em; margin:0;
    color:#f5edda; text-shadow:0 0 30px rgba(160,150,255,.55); font-weight:normal;}
#game-nc .overlay h2{font-size:clamp(15px,3.2vw,22px); letter-spacing:.28em; margin:0 0 6px;
    color:#ffc46b; font-weight:normal; text-shadow:0 0 18px rgba(255,196,107,.6);}
#game-nc .overlay p{font-size:12.5px; color:#b9b2cc; margin:8px 0 16px; font-style:italic;
    line-height:1.55;}
#game-nc .overlay button{background:rgba(18,20,40,.75); color:#f5edda; border:1px solid rgba(255,196,107,.5);
    border-radius:10px; padding:12px 30px; margin:4px; font-family:inherit; font-size:15px;
    letter-spacing:.2em; cursor:pointer; box-shadow:0 0 24px rgba(255,196,107,.15);}
#game-nc .overlay button:active{transform:scale(.96);}
#game-nc .overlay button:disabled{opacity:.35;}
#game-nc .overlay .small{font-size:10.5px; opacity:.75; margin-top:12px;}
#game-nc /* tienda */
  #nc_shopItems{display:grid; grid-template-columns:1fr 1fr; gap:8px; max-width:560px; margin:0 auto;}
#game-nc .shopIt{background:rgba(18,20,40,.8); border:1px solid rgba(255,255,255,.2);
    border-radius:10px; padding:10px 8px; font-size:12px; cursor:pointer;}
#game-nc .shopIt b{display:block; color:#ffc46b; font-weight:normal; letter-spacing:.1em; font-size:12.5px;}
#game-nc .shopIt span{color:#b9b2cc; font-size:10.5px; font-style:italic;}
#game-nc .shopIt .cost{display:block; color:#a8f0ff; margin-top:4px;}
#game-nc .shopIt.off{opacity:.4; pointer-events:none;}
#game-nc .shopIt:active{transform:scale(.97);}
#game-nc #nc_rotate{z-index:40; background:#05060f;}
#game-nc #nc_rotate .phone{width:52px; height:88px; border:3px solid #ffc46b; border-radius:10px;
    margin:0 auto 18px; animation:rot 1.8s ease-in-out infinite;}
@keyframes rot{0%,25%{transform:rotate(0);} 55%,100%{transform:rotate(90deg);}}
@media (orientation:landscape){#game-nc #nc_rotate{display:none !important;}}
/* ===== AHORCADO ===== */

#game-hm{min-height:100vh; background:#efe7d6; color:#26211a;
  font-family:Georgia,'Times New Roman',serif; padding:54px 12px 40px;}
#game-hm .hm-wrap{max-width:520px; margin:0 auto; text-align:center;}
#game-hm h1{margin:0; font-size:1.6rem; letter-spacing:.3em; color:#26211a; font-weight:normal;}
#game-hm .hm-sub{font-size:.75rem; color:#8a7d66; font-style:italic; margin:4px 0 12px;}
#game-hm #hm_menu button{display:block; width:100%; padding:14px; margin:9px 0;
  font-family:inherit; font-size:.95rem; letter-spacing:.08em; background:#fbf6ea;
  border:1.5px solid #26211a; border-radius:8px; cursor:pointer; color:#26211a;}
#game-hm #hm_menu button small{display:block; font-size:.7rem; color:#8a7d66; font-style:italic;
  letter-spacing:0; margin-top:3px;}
#game-hm #hm_menu button:active{transform:scale(.98);}
#game-hm .hm-top{display:flex; justify-content:space-between; font-size:.78rem;
  color:#5c5344; margin-bottom:6px; border-bottom:2px solid #26211a; padding-bottom:6px; gap:8px;}
#game-hm #hm_info b{color:#7a2f1e; font-weight:normal;}
#game-hm svg{width:160px; height:160px; margin:4px auto;}
#game-hm .hm-ink{stroke:#26211a; stroke-width:4; stroke-linecap:round; fill:none;}
#game-hm .hm-part{opacity:0; transition:opacity .3s;}
#game-hm .hm-part.on{opacity:1;}
#game-hm #hm_word{font-size:1.6rem; letter-spacing:.3em; margin:8px 0 4px; min-height:2.1rem;
  word-break:break-word;}
#game-hm #hm_msg{min-height:1.4rem; font-size:.85rem; color:#7a4a1e; font-style:italic;}
#game-hm #hm_kb{display:grid; grid-template-columns:repeat(9,1fr); gap:5px; margin:10px 0;}
#game-hm #hm_kb button{padding:11px 0; font-family:inherit; font-size:1rem;
  background:#fbf6ea; border:1.5px solid #26211a; border-radius:5px; cursor:pointer; color:#26211a;}
#game-hm #hm_kb button:disabled{opacity:.25;}
#game-hm #hm_kb button.hm-ok{background:#cfe3c2;}
#game-hm #hm_kb button.hm-bad{background:#e8c4b8;}
#game-hm .hm-row{display:flex; gap:8px;}
#game-hm .hm-row button{flex:1; padding:12px 4px; font-family:inherit; font-size:.82rem;
  letter-spacing:.08em; background:#26211a; color:#efe7d6; border:none; border-radius:6px; cursor:pointer;}
#game-hm .hm-row button:disabled{opacity:.4;}

/* ===== CUATRO EN RAYA ===== */

#game-c4{min-height:100vh; background:#101322; color:#e8ecff;
  font-family:Georgia,'Times New Roman',serif; padding:54px 12px 40px;}
#game-c4 .c4-wrap{max-width:480px; margin:0 auto; text-align:center;}
#game-c4 h1{margin:0; font-size:1.5rem; letter-spacing:.25em; font-weight:normal; color:#ffd75e;}
#game-c4 .c4-sub{font-size:.75rem; color:#8b93b8; font-style:italic; margin:4px 0 16px;}
#game-c4 .c4-menu button{display:block; width:100%; padding:14px; margin:8px 0;
  font-family:inherit; font-size:1rem; letter-spacing:.12em; background:#1a1f38;
  color:#e8ecff; border:1px solid #333c66; border-radius:8px; cursor:pointer;}
#game-c4 .c4-menu button:active{transform:scale(.98);}
#game-c4 #c4_status{display:flex; justify-content:center; align-items:center; gap:10px;
  font-size:.9rem; margin-bottom:10px; min-height:34px;}
#game-c4 .c4-turn{width:26px; height:26px; border-radius:50%; display:inline-block;
  box-shadow:inset 0 -3px 6px rgba(0,0,0,.4);}
#game-c4 .c4-p1{background:radial-gradient(circle at 35% 30%,#ff8f8f,#d92b2b);}
#game-c4 .c4-p2{background:radial-gradient(circle at 35% 30%,#ffe89a,#e8b400);}
#game-c4 #c4_board{display:grid; grid-template-columns:repeat(7,1fr); gap:6px;
  background:#2244aa; padding:10px; border-radius:14px;
  box-shadow:0 8px 24px rgba(0,0,0,.5), inset 0 2px 0 rgba(255,255,255,.15);}
#game-c4 .c4-cell{aspect-ratio:1; background:#101322; border-radius:50%;
  box-shadow:inset 0 3px 8px rgba(0,0,0,.7); position:relative; cursor:pointer;}
#game-c4 .c4-disc{position:absolute; inset:7%; border-radius:50%;
  animation:c4drop .35s cubic-bezier(.5,0,.7,1);}
@keyframes c4drop{from{transform:translateY(var(--d,-300px));} to{transform:translateY(0);}}
#game-c4 .c4-disc.c4-p1, #game-c4 .c4-disc.c4-p2{position:absolute;}
#game-c4 .c4-winner{box-shadow:0 0 0 3px #fff, 0 0 18px #fff;}
#game-c4 .c4-row{display:flex; gap:8px; margin-top:14px;}
#game-c4 .c4-row button{flex:1; padding:12px; font-family:inherit; font-size:.85rem;
  letter-spacing:.1em; background:#1a1f38; color:#e8ecff; border:1px solid #333c66;
  border-radius:8px; cursor:pointer;}
#game-c4 #c4_score{font-size:.75rem; color:#8b93b8; margin-top:10px;}

/* ===== VÉRTIGO ===== */
#game-vt *{box-sizing:border-box; -webkit-tap-highlight-color:transparent; user-select:none; touch-action:none;}
#game-vt{margin:0; height:100%; background:#07090f; overflow:hidden;
    font-family:Georgia,'Times New Roman',serif; color:#e8e6dd;}
#game-vt #vt_cv{position:fixed; inset:0; width:100%; height:100%; display:block;}
#game-vt .ui{position:fixed; z-index:10;}
#game-vt #vt_hud{top:10px; left:14px; font-size:13px; letter-spacing:.08em; opacity:.92;
    text-shadow:0 2px 8px rgba(0,0,0,.85); pointer-events:none; line-height:1.5;}
#game-vt #vt_hud b{color:#ffd75e; font-weight:normal;}
#game-vt #vt_hud .hp{color:#ff6b6b;}
#game-vt #vt_hud .en{color:#6be2ff;}
#game-vt #vt_sndBtn{top:8px; right:12px; background:rgba(12,16,28,.55); color:#e8e6dd;
    border:1px solid rgba(255,255,255,.15); border-radius:8px; padding:7px 12px;
    font-size:15px; z-index:11;}
#game-vt .pad{bottom:calc(14px + env(safe-area-inset-bottom)); width:72px; height:72px;
    border-radius:50%; background:rgba(22,28,50,.38); border:1.5px solid rgba(255,255,255,.22);
    color:rgba(255,255,255,.85); font-size:25px; display:grid; place-items:center;
    backdrop-filter:blur(2px);}
#game-vt .pad:active, #game-vt .pad.on{background:rgba(255,215,94,.25); border-color:#ffd75e;}
#game-vt #vt_btnL{left:calc(16px + env(safe-area-inset-left));}
#game-vt #vt_btnR{left:calc(102px + env(safe-area-inset-left));}
#game-vt #vt_btnC{left:calc(58px + env(safe-area-inset-left)); width:56px; height:56px; font-size:19px;
    bottom:calc(100px + env(safe-area-inset-bottom));}
#game-vt #vt_btnJ{right:calc(16px + env(safe-area-inset-right)); width:84px; height:84px; font-size:16px;
    letter-spacing:.08em;}
#game-vt #vt_btnF{right:calc(110px + env(safe-area-inset-right)); width:62px; height:62px; font-size:23px;
    bottom:calc(22px + env(safe-area-inset-bottom));}
#game-vt #vt_btnH{right:calc(30px + env(safe-area-inset-right)); width:54px; height:54px; font-size:20px;
    bottom:calc(112px + env(safe-area-inset-bottom));}
#game-vt .overlay{position:fixed; inset:0; z-index:20; display:none; place-items:center;
    background:rgba(4,6,12,.66); text-align:center; padding:16px;}
#game-vt .overlay.on{display:grid;}
#game-vt .overlay h1{font-size:clamp(28px,7vw,52px); letter-spacing:.32em; margin:0;
    color:#f2f0e6; text-shadow:0 0 28px rgba(120,200,255,.5); font-weight:normal;}
#game-vt .overlay h2{font-size:clamp(15px,3.2vw,22px); letter-spacing:.26em; margin:0 0 6px;
    color:#ffd75e; font-weight:normal; text-shadow:0 0 16px rgba(255,215,94,.5);}
#game-vt .overlay p{font-size:12.5px; color:#aeb4c8; margin:8px 0 16px; font-style:italic; line-height:1.55;}
#game-vt .overlay button{background:rgba(20,26,46,.8); color:#f2f0e6; border:1px solid rgba(255,215,94,.5);
    border-radius:10px; padding:12px 30px; margin:4px; font-family:inherit; font-size:15px;
    letter-spacing:.18em; cursor:pointer;}
#game-vt .overlay button:active{transform:scale(.96);}
#game-vt .overlay .small{font-size:10.5px; opacity:.75; margin-top:12px;}
#game-vt #vt_shopItems{display:grid; grid-template-columns:1fr 1fr; gap:8px; max-width:540px; margin:0 auto;}
#game-vt .shopIt{background:rgba(20,26,46,.85); border:1px solid rgba(255,255,255,.2);
    border-radius:10px; padding:10px 8px; font-size:12px; cursor:pointer;}
#game-vt .shopIt b{display:block; color:#ffd75e; font-weight:normal; letter-spacing:.08em; font-size:12.5px;}
#game-vt .shopIt span{color:#aeb4c8; font-size:10.5px; font-style:italic;}
#game-vt .shopIt .cost{display:block; color:#8affd0; margin-top:4px;}
#game-vt .shopIt.off{opacity:.4; pointer-events:none;}
#game-vt #vt_rotate{z-index:40; background:#07090f;}
#game-vt #vt_rotate .phone{width:52px; height:88px; border:3px solid #ffd75e; border-radius:10px;
    margin:0 auto 18px; animation:rot 1.8s ease-in-out infinite;}
@keyframes rot{0%,25%{transform:rotate(0);} 55%,100%{transform:rotate(90deg);}}
@media (orientation:landscape){#game-vt #vt_rotate{display:none !important;}}
</style>
</head>
<body>

<div id="arcadeHome"><div class="ah-in">
  <h1>ARCADE NOCTURNO</h1>
  <p class="ah-sub">Seis mundos. Una sola partida más.</p>
  <div class="ah-grid">
    <div class="ah-card ah-md" data-g="md"><div class="ah-ic">🔍</div>
      <h2>MURDOKU</h2><p>Un asesinato. Una única verdad.</p><button>JUGAR</button></div>
    <div class="ah-card ah-fl" data-g="fl"><div class="ah-ic">🚢</div>
      <h2>HUNDIR LA FLOTA</h2><p>Encuentra al enemigo antes de que él te encuentre a ti.</p><button>JUGAR</button></div>
    <div class="ah-card ah-nc" data-g="nc"><div class="ah-ic">🌙</div>
      <h2>NOCTIS</h2><p>La noche recuerda cada decisión.</p><button>JUGAR</button></div>
    <div class="ah-card ah-hm" data-g="hm"><div class="ah-ic">✒️</div>
      <h2>AHORCADO</h2><p>Una palabra. Pocas oportunidades.</p><button>JUGAR</button></div>
    <div class="ah-card ah-c4" data-g="c4"><div class="ah-ic">🔴</div>
      <h2>CUATRO EN RAYA</h2><p>Cuatro fichas. Una línea. Ningún error.</p><button>JUGAR</button></div>
    <div class="ah-card ah-vt" data-g="vt"><div class="ah-ic">🗼</div>
      <h2>VÉRTIGO</h2><p>Sube. La ciudad entera es una pared.</p><button>JUGAR</button></div>
  </div>
</div></div>
<button id="arcadeBack">←</button>

<div class="game-container" id="game-md">
<main>
  <h1>MURDOKU</h1>
  <p class="sub">Cada pista elimina una posibilidad. Solo una historia puede ser verdad.</p>

  <div id="md_gen">Preparando el caso…</div>

  <div id="md_game" style="display:none">
    <section>
      <h2>Expediente del caso</h2>
      <p id="md_intro"></p>
    </section>

    <section>
      <h2>Pistas</h2>
      <ol id="md_clues"></ol>
      <p class="hint">Toca una pista para tacharla cuando ya la hayas usado.</p>
    </section>

    <section>
      <h2>Cuadrículas de deducción</h2>
      <p class="hint" style="margin:0 0 10px">Toca una casilla para cambiar: vacío → ✕ (imposible) → ✓ (confirmado).</p>
      <div id="md_grids"></div>
    </section>

    <section>
      <h2>Cuaderno del detective</h2>
      <textarea id="md_notes" placeholder="Apunta aquí tus deducciones…"></textarea>
    </section>

    <section>
      <h2>Acusación final</h2>
      <div id="md_accuse"></div>
      <button id="md_btnAccuse">Presentar acusación</button>
      <div id="md_verdict"></div>
    </section>

    <button class="alt" id="md_btnNew">Nueva investigación</button>
  </div>
</main>

</div>
<div class="game-container" id="game-fl">
<main>

  <!-- MENÚ -->
  <div class="screen on" id="fl_scrMenu">
    <div id="fl_radarWrap"><div id="fl_radar"></div>
      <div class="blip" style="top:32%; left:60%"></div>
      <div class="blip" style="top:64%; left:38%; animation-delay:1.4s"></div>
      <div class="blip" style="top:48%; left:74%; animation-delay:2.3s"></div>
    </div>
    <h1>HUNDIR LA FLOTA</h1>
    <p class="tag">«En el océano, encontrar al enemigo es tan importante como destruirlo.»</p>
    <button class="resume" id="fl_btnResume" style="display:none">⚓ REANUDAR OPERACIÓN</button>
    <button class="primary" id="fl_btnSolo">UN JUGADOR</button>
    <div id="fl_diffPanel" class="panel" style="display:none">
      <h2>NIVEL DEL ENEMIGO</h2>
      <div class="row">
        <button data-diff="cadete">CADETE</button>
        <button data-diff="capitan">CAPITÁN</button>
        <button data-diff="almirante">ALMIRANTE</button>
      </div>
    </div>
    <button class="primary" id="fl_btnDuel">DOS JUGADORES</button>
    <button id="fl_btnStats">ESTADÍSTICAS</button>
    <button id="fl_btnHow">CÓMO JUGAR</button>
    <div class="panel" id="fl_howPanel" style="display:none; font-size:.75rem; line-height:1.7;">
      Coloca tus 5 barcos en el tablero. Después, por turnos, se dispara a
      coordenadas del mapa rival.<br><br>
      ● azul = agua &nbsp;&nbsp; ✕ rojo = impacto &nbsp;&nbsp; rojo intenso = barco hundido<br><br>
      Gana quien hunda antes toda la flota enemiga.<br><br>
      <b>Regla arcade:</b> si aciertas, repites: sigues disparando hasta fallar (la IA y el rival también).<br><br>
      <b>Un jugador:</b> contra la IA, en tres niveles. La partida se guarda sola:
      si cierras, podrás reanudarla.<br><br>
      <b>Dos jugadores:</b> en el mismo móvil, pasándooslo. Una pantalla de cortesía
      evita que veáis la flota del rival.<br><br>
      El botón 🔊 activa o silencia los efectos de sonido.
    </div>
  </div>

  <!-- COLOCACIÓN -->
  <div class="screen" id="fl_scrPlace">
    <div class="panel">
      <h2 id="fl_placeTitle">DESPLIEGUE DE FLOTA</h2>
      <div class="fleetlist" id="fl_chips"></div>
      <p class="h2sub" id="fl_placeMsg">Elige un barco y toca el tablero para situar su proa.</p>
    </div>
    <div class="panel">
      <div class="boardwrap">
        <div></div><div class="collabels" id="fl_cl1"></div>
        <div class="rowlabels" id="fl_rl1"></div>
        <div class="board" id="fl_placeBoard"></div>
      </div>
    </div>
    <div class="row"><button id="fl_btnRot">⟳ ROTAR: HORIZONTAL</button></div>
    <div class="row">
      <button class="warn" id="fl_btnAuto">ALEATORIO</button>
      <button class="warn" id="fl_btnClear">REINICIAR</button>
    </div>
    <button class="primary" id="fl_btnStart" disabled>ZARPAR ⚓</button>
  </div>

  <!-- BATALLA -->
  <div class="screen" id="fl_scrBattle">
    <div id="fl_turnbar">
      <span id="fl_turnNum">T.1</span>
      <span id="fl_turnState" class="you">TU TURNO</span>
      <button id="fl_sndBtn" title="Activar o silenciar los efectos de sonido">🔊</button>
    </div>
    <div class="panel">
      <h2 id="fl_enemyTitle">MAPA TÁCTICO — FLOTA ENEMIGA</h2>
      <div class="boardwrap">
        <div></div><div class="collabels" id="fl_cl2"></div>
        <div class="rowlabels" id="fl_rl2"></div>
        <div class="board enemy" id="fl_enemyBoard"></div>
      </div>
      <div class="status" id="fl_enemyFleet" style="margin-top:8px"></div>
    </div>
    <div class="duo">
      <div class="panel mini">
        <h2>MI FLOTA</h2>
        <div class="board" id="fl_ownBoard"></div>
        <div class="status" id="fl_ownFleet" style="margin-top:6px"></div>
      </div>
      <div class="panel">
        <h2>OPERACIONES</h2>
        <div id="fl_log"></div>
      </div>
    </div>
    <button class="warn" id="fl_btnAbandon">VOLVER AL MENÚ</button>
  </div>

  <!-- ENTREGA DE MÓVIL (2 jugadores) -->
  <div class="overlay" id="fl_handoff"><div class="obox">
    <h2>CAMBIO DE TURNO</h2>
    <p id="fl_handMsg"></p>
    <button class="primary" id="fl_btnHand">ESTOY LISTO</button>
  </div></div>

  <!-- FIN -->
  <div class="overlay" id="fl_endModal"><div class="obox">
    <h2 id="fl_endTitle"></h2>
    <p id="fl_endMsg"></p>
    <button class="primary" id="fl_btnAgain">NUEVA OPERACIÓN</button>
    <button id="fl_btnMenu">MENÚ PRINCIPAL</button>
  </div></div>

  <!-- FICHA TÉCNICA DE BARCO -->
  <div class="overlay" id="fl_shipModal"><div class="obox">
    <h2 id="fl_shipTitle"></h2>
    <div class="shipcells" id="fl_shipCells"></div>
    <p id="fl_shipDesc" style="text-align:left"></p>
    <button id="fl_btnShipClose">CERRAR</button>
  </div></div>

  <!-- ESTADÍSTICAS -->
  <div class="overlay" id="fl_statsModal"><div class="obox">
    <h2>ESTADÍSTICAS</h2>
    <div id="fl_statsBody" style="text-align:left; margin-bottom:14px;"></div>
    <button id="fl_btnStatsClose">CERRAR</button>
  </div></div>

</main>

</div>
<div class="game-container" id="game-nc">
<canvas id="nc_cv"></canvas>

<div class="ui" id="nc_hud"></div>
<button class="ui" id="nc_sndBtn">🔊</button>
<div class="ui pad" id="nc_btnL">◀</div>
<div class="ui pad" id="nc_btnR">▶</div>
<div class="ui pad" id="nc_btnC">▼</div>
<div class="ui pad" id="nc_btnJ">SALTO</div>
<div class="ui pad" id="nc_btnA">✦</div>
<div id="nc_wheel"></div>

<div class="overlay on" id="nc_menu">
  <div>
    <h1>NOCTIS</h1>
    <p>El Sol desapareció hace trece años. El Cazador de Umbra<br>
    vigila Azhar desde su torre. Esta noche subirás hasta él.</p>
    <button id="nc_btnCont" style="display:none">⚓ CONTINUAR</button>
    <button id="nc_btnPlay">NUEVA HISTORIA</button>
    <button id="nc_btnEndless">MODO SIN FIN</button>
    <p class="small" id="nc_recLine"></p>
    <p class="small">◀ ▶ moverte · ▼ agacharte (en el aire: dash si lo compras) · SALTO<br>
    Toca el gadget para usarlo · MANTÉN y desliza = rueda: ✦ daga · 🪝 gancho · 💨 humo · 🌑 sombra<br>
    Las dagas se guían solas al enemigo más cercano por delante (¡también a los cuervos!).<br>
    💨 humo: todos te pierden de vista al instante — y REPELE a la bandada que te persiga.<br>
    Las lunas ☾ son moneda: gástalas en la tienda entre zonas.<br>
    (Teclado: AD/flechas, S, espacio, X usar, Q cambiar)</p>
  </div>
</div>

<div class="overlay" id="nc_inter">
  <div>
    <h2 id="nc_interTitle"></h2>
    <p id="nc_interMsg"></p>
    <div id="nc_shopItems"></div>
    <p class="small" id="nc_bankLine"></p>
    <button id="nc_btnNext">CONTINUAR</button>
  </div>
</div>

<div class="overlay" id="nc_rotate">
  <div>
    <div class="phone"></div>
    <h2>GIRA TU DISPOSITIVO</h2>
    <p>Noctis se juega en horizontal.</p>
  </div>
</div>

</div>
<div class="game-container" id="game-hm">
<div class="hm-wrap">
  <h1>AHORCADO</h1>
  <p class="hm-sub">Una palabra. Pocas oportunidades.</p>
  <div id="hm_menu">
    <button data-m="clasico">CLÁSICO<small>Encadena aciertos y bate tu racha. Sin prisa.</small></button>
    <button data-m="crono">CONTRARRELOJ<small>Empiezas con 75 s. Cada palabra suma tiempo, cada fallo resta.</small></button>
    <button data-m="vidas">SUPERVIVENCIA<small>3 vidas. Cada palabra fallada cuesta una. Cada 3 aciertos, recuperas.</small></button>
  </div>
  <div id="hm_play" style="display:none">
    <div class="hm-top"><span id="hm_cat"></span><span id="hm_info"></span></div>
    <svg id="hm_svg" viewBox="0 0 200 200">
      <path class="hm-ink" d="M20 185 H120"/>
      <path class="hm-ink" d="M50 185 V25 H130 V45"/>
      <path class="hm-ink" d="M50 60 L85 25"/>
      <circle class="hm-ink hm-part" id="hm_p0" cx="130" cy="62" r="17"/>
      <path class="hm-ink hm-part" id="hm_p1" d="M130 79 V130"/>
      <path class="hm-ink hm-part" id="hm_p2" d="M130 92 L105 115"/>
      <path class="hm-ink hm-part" id="hm_p3" d="M130 92 L155 115"/>
      <path class="hm-ink hm-part" id="hm_p4" d="M130 130 L110 165"/>
      <path class="hm-ink hm-part" id="hm_p5" d="M130 130 L150 165"/>
    </svg>
    <div id="hm_word"></div>
    <div id="hm_msg"></div>
    <div id="hm_kb"></div>
    <div class="hm-row">
      <button id="hm_hint">💡 LETRA</button>
      <button id="hm_new">NUEVA PALABRA</button>
      <button id="hm_exit">MODOS</button>
    </div>
  </div>
</div>
</div>
<div class="game-container" id="game-c4">
<div class="c4-wrap">
  <h1>CUATRO EN RAYA</h1>
  <p class="c4-sub">Cuatro fichas. Una línea. Ningún error.</p>
  <div class="c4-menu" id="c4_menu">
    <button data-mode="facil">1 JUGADOR · FÁCIL</button>
    <button data-mode="normal">1 JUGADOR · NORMAL</button>
    <button data-mode="dificil">1 JUGADOR · DIFÍCIL</button>
    <button data-mode="2p">2 JUGADORES</button>
  </div>
  <div id="c4_play" style="display:none">
    <div id="c4_status"></div>
    <div id="c4_board"></div>
    <div class="c4-row">
      <button id="c4_restart">REINICIAR</button>
      <button id="c4_back">CAMBIAR MODO</button>
    </div>
    <div id="c4_score"></div>
  </div>
</div>
</div>
<div class="game-container" id="game-vt">
<canvas id="vt_cv"></canvas>
<div class="ui" id="vt_hud"></div>
<button class="ui" id="vt_sndBtn">🔊</button>
<div class="ui pad" id="vt_btnL">◀</div>
<div class="ui pad" id="vt_btnR">▶</div>
<div class="ui pad" id="vt_btnC">▼</div>
<div class="ui pad" id="vt_btnJ">SALTO</div>
<div class="ui pad" id="vt_btnF">⚡</div>
<div class="ui pad" id="vt_btnH">🪝</div>

<div class="overlay on" id="vt_menu">
  <div>
    <h1>VÉRTIGO</h1>
    <p>Bajo la Torre Ossia hay doce plantas de tuberías y secretos.<br>
    Arriba, en la azotea, el CUSTODIO espera. Sube. Si puedes.</p>
    <button id="vt_btnCont" style="display:none">⚓ CONTINUAR</button>
    <button id="vt_btnPlay">🗼 TORRE</button>
    <button id="vt_btnTime">⏱ CONTRARRELOJ</button>
    <button id="vt_btnChase">🌑 PERSECUCIÓN</button>
    <button id="vt_btnEndless">♾ INFINITA</button><br>
    <button id="vt_btnLogros" style="font-size:13px;padding:8px 14px">🏆 LOGROS</button>
    <button id="vt_btnMute" style="font-size:13px;padding:8px 14px">🎵 MÚSICA: SÍ</button>
    <p class="small" id="vt_recLine"></p>
    <p class="small">◀ ▶ moverte · ▼ agacharte y colarte por conductos · SALTO<br>
    En el aire, empuja hacia una pared para AGARRARTE; SALTO rebota entre paredes.<br>
    ⚡ dispara (se autoapunta, la energía se recarga sola) · 🪝 cuerda en los aros<br>
    ¡OJO! En las salas de aros SOLO el gancho sube: engancha, balancéate con ◀ ▶,<br>
    suéltate con SALTO en lo alto y re-engancha el siguiente aro EN EL AIRE.<br>
    💾 chips = moneda para las máquinas de mejoras de los puntos de control.<br>
    (Teclado: AD/flechas, S, espacio, X disparo, C cuerda)</p>
  </div>
</div>

<div class="overlay" id="vt_inter">
  <div>
    <h2 id="vt_interTitle"></h2>
    <p id="vt_interMsg"></p>
    <div id="vt_shopItems"></div>
    <p class="small" id="vt_bankLine"></p>
    <button id="vt_btnNext">CONTINUAR</button>
    <button id="vt_btnAlt" style="display:none"></button>
  </div>
</div>

<div class="overlay" id="vt_logros">
  <div>
    <h2>🏆 LOGROS</h2>
    <div id="vt_logroList" style="text-align:left;max-width:340px;margin:10px auto;font-size:13px;line-height:1.9"></div>
    <button id="vt_btnLogrosBack">VOLVER</button>
  </div>
</div>

<div class="overlay" id="vt_rotate">
  <div>
    <div class="phone"></div>
    <h2>GIRA TU DISPOSITIVO</h2>
    <p>Vértigo se juega en horizontal.</p>
  </div>
</div>

</div>
<script>

let __arcadeAC=null, __arcadeMuted=false;
function ArcadeSnd(f,d,type,v,slide){
  if(__arcadeMuted) return;
  try{
    __arcadeAC=__arcadeAC||new (window.AudioContext||window.webkitAudioContext)();
    const o=__arcadeAC.createOscillator(), g=__arcadeAC.createGain();
    o.type=type||"sine"; o.frequency.value=f;
    if(slide) o.frequency.exponentialRampToValueAtTime(slide,__arcadeAC.currentTime+d);
    g.gain.setValueAtTime(v||.1,__arcadeAC.currentTime);
    g.gain.exponentialRampToValueAtTime(.001,__arcadeAC.currentTime+d);
    o.connect(g); g.connect(__arcadeAC.destination);
    o.start(); o.stop(__arcadeAC.currentTime+d);
  }catch(e){}
}
const Arcade={current:null};
const ARCADE_GAMES={};
function arcadeRegister(k,mod){ ARCADE_GAMES[k]=mod; }
function arcadeLaunch(k){
  Arcade.current=k;
  document.getElementById("arcadeHome").style.display="none";
  document.getElementById("game-"+k).classList.add("active");
  document.getElementById("arcadeBack").classList.add("on");
  const m=ARCADE_GAMES[k];
  if(m){
    if(m.start) m.start();
    if(k==="fl" && m.showMenu) m.showMenu();
  }
  window.scrollTo(0,0);
  ArcadeSnd(620,.08,"square",.06);
}
function arcadeBack(){
  const k=Arcade.current;
  if(k){
    const m=ARCADE_GAMES[k];
    if(m && m.stop) m.stop();
    document.getElementById("game-"+k).classList.remove("active");
  }
  Arcade.current=null;
  document.getElementById("arcadeBack").classList.remove("on");
  document.getElementById("arcadeHome").style.display="block";
  window.scrollTo(0,0);
}
document.getElementById("arcadeBack").onclick=arcadeBack;
document.querySelectorAll(".ah-card").forEach(c=>{
  c.onclick=()=>arcadeLaunch(c.dataset.g);
});

/* ===== MURDOKU ===== */
const GameMD=(function(){
const __exp={};
let __active=false;

"use strict";

/* ---------- Datos ---------- */
const POOLS = {
  suspect: ["Lucía","Marcos","Elena","Daniel","Sofía","Adrián","Clara","Bruno","Valeria","Hugo"],
  room:    [["Biblioteca","la biblioteca"],["Cocina","la cocina"],["Salón","el salón"],["Despacho","el despacho"],
            ["Invernadero","el invernadero"],["Bodega","la bodega"],["Comedor","el comedor"],["Galería","la galería"]],
  weapon:  [["Cuchillo","el cuchillo"],["Veneno","el veneno"],["Candelabro","el candelabro"],["Cuerda","la cuerda"],
            ["Revólver","el revólver"],["Estatuilla","la estatuilla"],["Hacha","el hacha"],["Tijeras","las tijeras"]],
  motive:  [["Celos","los celos"],["Herencia","la herencia"],["Venganza","la venganza"],["Chantaje","un chantaje"],
            ["Dinero","el dinero"],["Secreto","un secreto"],["Poder","el poder"],["Robo","un robo"]],
};
const HOURS = ["21:00","22:00","23:00","00:00"];
const VICTIMS = ["Octavio Valdemar","Beatriz Montero","Ricardo Alcázar","Camila Osorio","Tomás Ibáñez"];
const PLACES = ["la mansión","el hotel","el viejo museo","el palacio","el teatro"];
const N = 4;
const CATS = ["room","weapon","hour","motive"];
const CATLABEL = {room:"Habitación", weapon:"Arma", hour:"Hora", motive:"Motivo"};

/* ---------- Utilidades ---------- */
const rnd = n => Math.floor(Math.random()*n);
function shuffle(a){ a=a.slice(); for(let i=a.length-1;i>0;i--){const j=rnd(i+1);[a[i],a[j]]=[a[j],a[i]];} return a; }
function pick(pool,n){ return shuffle(pool).slice(0,n); }
function permutations(arr){
  if(arr.length<=1) return [arr];
  const out=[];
  arr.forEach((x,i)=>{
    permutations(arr.slice(0,i).concat(arr.slice(i+1))).forEach(p=>out.push([x,...p]));
  });
  return out;
}
const PERMS = permutations([0,1,2,3]);

/* ---------- Estado ---------- */
let G = null; // partida actual

/* ---------- Generación de pistas ----------
   Una asignación es {room,weapon,hour,motive}, cada una un array
   que indica, para el sospechoso i, el índice del elemento asignado. */
function makeCluePool(sol, names){
  const S=names.suspect, R=names.room, W=names.weapon, M=names.motive, H=names.hour;
  const pool=[];
  const add=(deps,test,text,direct)=>pool.push({deps,test,text,direct:!!direct});

  for(let s=0;s<N;s++) for(let i=0;i<N;i++){
    if(sol.room[s]!==i)   add(["room"],   a=>a.room[s]!==i,   `${S[s]} no estaba en ${R[i][1]}.`);
    if(sol.weapon[s]!==i) add(["weapon"], a=>a.weapon[s]!==i, `${S[s]} no tenía ${W[i][1]}.`);
    if(sol.motive[s]!==i) add(["motive"], a=>a.motive[s]!==i, `El móvil de ${S[s]} no era ${M[i][1]}.`);
    if(sol.hour[s]!==i)   add(["hour"],   a=>a.hour[s]!==i,   `${S[s]} no actuó a las ${H[i]}.`);
  }
  for(let s=0;s<N;s++){
    const w=sol.weapon[s], m=sol.motive[s];
    add(["weapon"], a=>a.weapon[s]===w, `${S[s]} tenía ${W[w][1]}.`, true);
    add(["motive"], a=>a.motive[s]===m, `El móvil de ${S[s]} era ${M[m][1]}.`, true);
  }
  for(let r=0;r<N;r++){
    const s=sol.room.indexOf(r);
    add(["room","weapon"], a=>a.weapon[a.room.indexOf(r)]===sol.weapon[s],
        `Quien estaba en ${R[r][1]} tenía ${W[sol.weapon[s]][1]}.`);
    add(["room","hour"], a=>a.hour[a.room.indexOf(r)]===sol.hour[s],
        `Quien estaba en ${R[r][1]} estuvo allí a las ${H[sol.hour[s]]}.`);
    add(["room","motive"], a=>a.motive[a.room.indexOf(r)]===sol.motive[s],
        `Quien estaba en ${R[r][1]} actuaba por ${M[sol.motive[s]][1]}.`);
  }
  for(let w=0;w<N;w++){
    const s=sol.weapon.indexOf(w);
    add(["weapon","hour"], a=>a.hour[a.weapon.indexOf(w)]===sol.hour[s],
        `Quien tenía ${W[w][1]} actuó a las ${H[sol.hour[s]]}.`);
  }
  for(let a1=0;a1<N;a1++) for(let a2=0;a2<N;a2++){
    if(sol.hour[a1]<sol.hour[a2])
      add(["hour"], a=>a.hour[a1]<a.hour[a2], `${S[a1]} actuó antes que ${S[a2]}.`);
  }
  return pool;
}

/* Solver: cuenta asignaciones compatibles (se detiene en `limit`). */
function countSolutions(clues, limit){
  const byLevel=[[],[],[],[]]; // room, +weapon, +hour, +motive
  const levelOf={room:0,weapon:1,hour:2,motive:3};
  clues.forEach(c=>byLevel[Math.max(...c.deps.map(d=>levelOf[d]))].push(c));
  let count=0;
  const a={room:null,weapon:null,hour:null,motive:null};
  for(const rp of PERMS){
    a.room=rp; if(!byLevel[0].every(c=>c.test(a))) continue;
    for(const wp of PERMS){
      a.weapon=wp; if(!byLevel[1].every(c=>c.test(a))) continue;
      for(const hp of PERMS){
        a.hour=hp; if(!byLevel[2].every(c=>c.test(a))) continue;
        for(const mp of PERMS){
          a.motive=mp; if(!byLevel[3].every(c=>c.test(a))) continue;
          if(++count>=limit) return count;
        }
      }
    }
  }
  return count;
}

function generateGame(){
  for(let attempt=0; attempt<25; attempt++){
    const names={
      suspect: pick(POOLS.suspect,N),
      room: pick(POOLS.room,N),
      weapon: pick(POOLS.weapon,N),
      motive: pick(POOLS.motive,N),
      hour: HOURS,
    };
    const sol={
      room: shuffle([0,1,2,3]),
      weapon: shuffle([0,1,2,3]),
      hour: shuffle([0,1,2,3]),
      motive: shuffle([0,1,2,3]),
    };
    const pool=shuffle(makeCluePool(sol,names));
    // Añadir pistas hasta que la solución sea única (máx. 2 pistas directas)
    let chosen=[], directs=0, ok=false;
    for(const c of pool){
      if(c.direct && directs>=2) continue;
      chosen.push(c);
      if(c.direct) directs++;
      if(chosen.length>=4 && countSolutions(chosen,2)===1){ ok=true; break; }
      if(chosen.length>22) break;
    }
    if(!ok) continue;
    // Poda: eliminar pistas redundantes
    for(let i=chosen.length-1;i>=0;i--){
      const test=chosen.slice(0,i).concat(chosen.slice(i+1));
      if(countSolutions(test,2)===1) chosen=test;
    }
    // El crimen: la habitación donde apareció el cuerpo señala al culpable
    const crimeRoom=rnd(N);
    const killer=sol.room.indexOf(crimeRoom);
    const victim=VICTIMS[rnd(VICTIMS.length)];
    const place=PLACES[rnd(PLACES.length)];
    const intro=`Una tormenta ha aislado ${place} del resto del mundo. Esta noche, el cuerpo de ${victim} `+
      `ha aparecido en ${names.room[crimeRoom][1]}. Las puertas están cerradas: nadie ha podido salir. `+
      `Los cuatro presentes —${names.suspect.join(", ")}— estuvieron cada uno en una habitación distinta, `+
      `a una hora distinta, con un objeto distinto y un motivo distinto. Quien estuvo en ${names.room[crimeRoom][1]} es el asesino. Descúbrelo todo.`;
    return { names, sol, clues:chosen.map(c=>c.text), crimeRoom, killer, intro,
             marks:{}, notes:"", usedClues:{} };
  }
  return null;
}

/* ---------- Interfaz ---------- */
function renderGame(){
  document.getElementById("md_intro").textContent=G.intro;

  const ol=document.getElementById("md_clues");
  ol.innerHTML="";
  G.clues.forEach((t,i)=>{
    const li=document.createElement("li");
    li.textContent=t;
    if(G.usedClues[i]) li.classList.add("done");
    li.onclick=()=>{ li.classList.toggle("done"); G.usedClues[i]=!G.usedClues[i]; };
    ol.appendChild(li);
  });

  const grids=document.getElementById("md_grids");
  grids.innerHTML="";
  CATS.forEach(cat=>{
    const tbl=document.createElement("table");
    const cap=document.createElement("caption");
    cap.textContent="Sospechosos × "+({room:"Habitaciones",weapon:"Armas",hour:"Horas",motive:"Motivos"})[cat];
    tbl.appendChild(cap);
    const head=document.createElement("tr");
    head.appendChild(document.createElement("th"));
    for(let j=0;j<N;j++){
      const th=document.createElement("th");
      th.textContent = cat==="hour" ? G.names.hour[j] : G.names[cat][j][0];
      head.appendChild(th);
    }
    tbl.appendChild(head);
    for(let i=0;i<N;i++){
      const tr=document.createElement("tr");
      const th=document.createElement("th");
      th.className="rowh"; th.textContent=G.names.suspect[i];
      tr.appendChild(th);
      for(let j=0;j<N;j++){
        const td=document.createElement("td");
        td.className="cell";
        const key=cat+"-"+i+"-"+j;
        applyMark(td, G.marks[key]||0);
        td.onclick=()=>{
          G.marks[key]=((G.marks[key]||0)+1)%3;
          applyMark(td, G.marks[key]);
        };
        tr.appendChild(td);
      }
      tbl.appendChild(tr);
    }
    grids.appendChild(tbl);
  });

  const notes=document.getElementById("md_notes");
  notes.value=G.notes;
  notes.oninput=()=>{ G.notes=notes.value; };

  const acc=document.getElementById("md_accuse");
  acc.innerHTML="";
  const mk=(id,label,opts)=>{
    const l=document.createElement("label"); l.textContent=label;
    const sel=document.createElement("select"); sel.id=id;
    sel.innerHTML='<option value="">— Elegir —</option>'+
      opts.map((o,i)=>`<option value="${i}">${o}</option>`).join("");
    acc.appendChild(l); acc.appendChild(sel);
  };
  mk("accS","Asesino", G.names.suspect);
  mk("accR","Habitación", G.names.room.map(r=>r[0]));
  mk("accW","Arma", G.names.weapon.map(w=>w[0]));
  mk("accH","Hora", G.names.hour);
  mk("accM","Motivo", G.names.motive.map(m=>m[0]));

  const v=document.getElementById("md_verdict");
  v.className=""; v.textContent="";
}

function applyMark(td, state){
  td.classList.remove("x","v");
  if(state===1){ td.textContent="✕"; td.classList.add("x"); }
  else if(state===2){ td.textContent="✓"; td.classList.add("v"); }
  else td.textContent="";
}

function checkAccusation(){
  const val=id=>document.getElementById(id).value;
  const s=val("accS"), r=val("accR"), w=val("accW"), h=val("accH"), m=val("accM");
  const v=document.getElementById("md_verdict");
  if([s,r,w,h,m].some(x=>x==="")){
    v.className="bad"; v.textContent="Completa todos los campos de la acusación.";
    return;
  }
  const k=G.killer, sol=G.sol;
  const ok = +s===k && +r===sol.room[k] && +w===sol.weapon[k] && +h===sol.hour[k] && +m===sol.motive[k];
  if(ok){
    v.className="good";
    v.textContent=`CASO RESUELTO. El asesino era ${G.names.suspect[k]}: cometió el crimen en `+
      `${G.names.room[sol.room[k]][1]}, utilizando ${G.names.weapon[sol.weapon[k]][1]}, a las `+
      `${G.names.hour[sol.hour[k]]}, motivado por ${G.names.motive[sol.motive[k]][1]}.`;
  } else {
    v.className="bad";
    v.textContent="La teoría no encaja con todas las pruebas. Revisa tus deducciones.";
  }
}

function newGame(){
  document.getElementById("md_game").style.display="none";
  document.getElementById("md_gen").style.display="block";
  setTimeout(()=>{
    G=generateGame();
    document.getElementById("md_gen").style.display="none";
    if(!G){ document.getElementById("md_gen").textContent="No se pudo generar el caso. Recarga la página."; return; }
    document.getElementById("md_game").style.display="block";
    renderGame();
    window.scrollTo(0,0);
  },30);
}

document.getElementById("md_btnAccuse").onclick=checkAccusation;
document.getElementById("md_btnNew").onclick=newGame;
__exp.start=()=>{ if(!G) newGame(); };

const __s=__exp.start;
__exp.start=function(){ __active=true; if(__s) __s(); };
return __exp;
})();

/* ===== HUNDIR LA FLOTA ===== */
const GameFL=(function(){
const __exp={};
let __active=false;

"use strict";
const N=10, LETTERS="ABCDEFGHIJ";
const SHIPDEFS=[
  {key:"pa", label:"PORTAAVIONES", len:5},
  {key:"ac", label:"ACORAZADO",   len:4},
  {key:"de", label:"DESTRUCTOR",  len:3},
  {key:"su", label:"SUBMARINO",   len:3},
  {key:"pt", label:"PATRULLERA",  len:2},
];
const NAMES=["Audacia","Tempestad","Vanguardia","Centinela","Leviatán","Victoria",
  "Tridente","Furia","Horizonte","Espectro","Poseidón","Invictus"];
const DIFFNAMES={cadete:"CADETE", capitan:"CAPITÁN", almirante:"ALMIRANTE"};
const rnd=n=>Math.floor(Math.random()*n);
const coord=(r,c)=>LETTERS[r]+(c+1);
const other=p=>p==="p1"?"p2":"p1";
function shuffle(a){for(let i=a.length-1;i>0;i--){const j=rnd(i+1);[a[i],a[j]]=[a[j],a[i]];}return a;}

/* ================= LÓGICA DE FLOTAS ================= */
function emptyGrid(fill=-1){ return Array.from({length:N},()=>Array(N).fill(fill)); }
function canPlace(grid,r,c,len,horiz){
  for(let i=0;i<len;i++){
    const rr=horiz?r:r+i, cc=horiz?c+i:c;
    if(rr>=N||cc>=N||grid[rr][cc]!==-1) return false;
  }
  return true;
}
function placeShip(grid,ships,def,r,c,horiz,name){
  const cells=[];
  for(let i=0;i<def.len;i++){
    const rr=horiz?r:r+i, cc=horiz?c+i:c;
    grid[rr][cc]=ships.length; cells.push([rr,cc]);
  }
  ships.push({def,name,cells,hits:0,sunk:false});
}
function randomFleet(){
  for(let tries=0;tries<200;tries++){
    const grid=emptyGrid(), ships=[], names=shuffle(NAMES.slice());
    let ok=true;
    for(const def of SHIPDEFS){
      let placed=false;
      for(let a=0;a<120 && !placed;a++){
        const horiz=Math.random()<.5, r=rnd(N), c=rnd(N);
        if(canPlace(grid,r,c,def.len,horiz)){
          placeShip(grid,ships,def,r,c,horiz,names.pop()); placed=true;
        }
      }
      if(!placed){ ok=false; break; }
    }
    if(ok) return {grid,ships};
  }
  return null;
}
function fireAt(fleet,r,c){
  const idx=fleet.grid[r][c];
  if(idx===-1) return {result:"miss"};
  const ship=fleet.ships[idx];
  ship.hits++;
  if(ship.hits>=ship.def.len){ ship.sunk=true; return {result:"sunk", ship}; }
  return {result:"hit", ship};
}
const fleetDestroyed=f=>f.ships.every(s=>s.sunk);

/* ================= IA =================
   shots: -1 sin disparar, 0 agua, 1 impacto sin resolver, 2 casilla de barco hundido.
   La IA solo usa esta información pública, nunca la flota oculta del jugador. */
function makeAI(diff){
  return { diff, shots:emptyGrid(), targets:[], lastHits:[], sunkLens:[] };
}
function aiValidTarget(ai){
  while(ai.targets.length){
    const [r,c]=ai.targets.pop();
    if(r>=0&&r<N&&c>=0&&c<N&&ai.shots[r][c]===-1) return [r,c];
  }
  return null;
}
function anyUnshot(ai){
  const all=[];
  for(let r=0;r<N;r++)for(let c=0;c<N;c++) if(ai.shots[r][c]===-1) all.push([r,c]);
  return all.length?all[rnd(all.length)]:null;
}
function aiNextShot(ai){
  if(ai.diff==="cadete"){
    // Persigue impactos solo a veces; busca al azar sin patrón.
    if(ai.targets.length && Math.random()<.7){
      const t=aiValidTarget(ai); if(t) return t;
    }
    return anyUnshot(ai);
  }
  if(ai.diff==="almirante") return densityShot(ai);
  // capitán: persecución + búsqueda por paridad
  const t=aiValidTarget(ai); if(t) return t;
  const cands=[];
  for(let r=0;r<N;r++)for(let c=0;c<N;c++)
    if(ai.shots[r][c]===-1 && (r+c)%2===0) cands.push([r,c]);
  return cands.length?cands[rnd(cands.length)]:anyUnshot(ai);
}
/* Almirante: mapa de densidad. Puntúa cada casilla según cuántas
   colocaciones posibles de los barcos restantes la atraviesan. */
function densityShot(ai){
  const remaining=SHIPDEFS.map(d=>d.len);
  ai.sunkLens.forEach(l=>{ const i=remaining.indexOf(l); if(i!==-1) remaining.splice(i,1); });
  const score=emptyGrid(0);
  for(const len of remaining){
    for(let horiz=0; horiz<2; horiz++){
      const maxR=horiz?N:N-len+1, maxC=horiz?N-len+1:N;
      for(let r=0;r<maxR;r++)for(let c=0;c<maxC;c++){
        let ok=true, hitBonus=0;
        for(let i=0;i<len;i++){
          const rr=horiz?r:r+i, cc=horiz?c+i:c, v=ai.shots[rr][cc];
          if(v===0||v===2){ ok=false; break; }
          if(v===1) hitBonus++;
        }
        if(!ok) continue;
        const w=1+hitBonus*60;
        for(let i=0;i<len;i++){
          const rr=horiz?r:r+i, cc=horiz?c+i:c;
          if(ai.shots[rr][cc]===-1) score[rr][cc]+=w;
        }
      }
    }
  }
  let best=-1, cands=[];
  for(let r=0;r<N;r++)for(let c=0;c<N;c++){
    if(ai.shots[r][c]!==-1) continue;
    if(score[r][c]>best){ best=score[r][c]; cands=[[r,c]]; }
    else if(score[r][c]===best) cands.push([r,c]);
  }
  return cands.length?cands[rnd(cands.length)]:anyUnshot(ai);
}
function aiRegister(ai,r,c,result,ship){
  ai.shots[r][c]=(result==="miss")?0:1;
  if(result==="hit"){
    ai.lastHits.push([r,c]);
    if(ai.lastHits.length>=2){
      const [[r1,c1]]=ai.lastHits, [r2]=ai.lastHits[ai.lastHits.length-1];
      ai.targets=[];
      if(r1===r2){
        const cs=ai.lastHits.map(h=>h[1]);
        ai.targets.push([r1,Math.min(...cs)-1],[r1,Math.max(...cs)+1]);
      } else {
        const rs=ai.lastHits.map(h=>h[0]);
        ai.targets.push([Math.min(...rs)-1,c1],[Math.max(...rs)+1,c1]);
      }
    } else {
      ai.targets.push(...shuffle([[r-1,c],[r+1,c],[r,c-1],[r,c+1]]));
    }
  }
  if(result==="sunk"){
    ai.lastHits=[]; ai.targets=[];
    ai.sunkLens.push(ship.def.len);
    ship.cells.forEach(([rr,cc])=>{ ai.shots[rr][cc]=2; });
  }
}

/* ================= SONIDO Y VIBRACIÓN ================= */
let audioCtx=null, muted=false;
function beep(freq,dur,type="sine",vol=.15,slide=0){
  if(muted||!__active) return;
  try{
    audioCtx=audioCtx||new (window.AudioContext||window.webkitAudioContext)();
    const o=audioCtx.createOscillator(), g=audioCtx.createGain();
    o.type=type; o.frequency.value=freq;
    if(slide) o.frequency.exponentialRampToValueAtTime(slide,audioCtx.currentTime+dur);
    g.gain.setValueAtTime(vol,audioCtx.currentTime);
    g.gain.exponentialRampToValueAtTime(.001,audioCtx.currentTime+dur);
    o.connect(g); g.connect(audioCtx.destination);
    o.start(); o.stop(audioCtx.currentTime+dur);
  }catch(e){}
}
const sndFire =()=>beep(220,.12,"square",.1,80);
const sndMiss =()=>beep(300,.25,"sine",.12,120);
const sndHit  =()=>{beep(90,.3,"sawtooth",.2,40); beep(700,.1,"square",.08);};
const sndSunk =()=>{beep(70,.6,"sawtooth",.25,30); setTimeout(()=>beep(500,.4,"sine",.1,100),150);};
const sndWin  =()=>[523,659,784,1046].forEach((f,i)=>setTimeout(()=>beep(f,.25,"triangle",.15),i*160));
const sndLose =()=>[400,330,262,196].forEach((f,i)=>setTimeout(()=>beep(f,.3,"sawtooth",.12),i*180));
function vib(p){ try{ if(navigator.vibrate) navigator.vibrate(p); }catch(e){} }

/* ================= LOCALSTORAGE ================= */
const SAVE_KEY="flota_save_v1", STATS_KEY="flota_stats_v1";
function lsGet(k){ try{ const v=localStorage.getItem(k); return v?JSON.parse(v):null; }catch(e){ return null; } }
function lsSet(k,v){ try{ localStorage.setItem(k,JSON.stringify(v)); }catch(e){} }
function lsDel(k){ try{ localStorage.removeItem(k); }catch(e){} }
function getStats(){
  return Object.assign({played:0,wins:0,losses:0,shots:0,hits:0,streak:0,best:0}, lsGet(STATS_KEY)||{});
}
function serializeFleet(f){
  return { grid:f.grid, ships:f.ships.map(s=>({key:s.def.key,name:s.name,cells:s.cells,hits:s.hits,sunk:s.sunk})) };
}
function reviveFleet(d){
  return { grid:d.grid, ships:d.ships.map(s=>({
    def:SHIPDEFS.find(x=>x.key===s.key), name:s.name, cells:s.cells, hits:s.hits, sunk:s.sunk })) };
}
function saveGame(){
  if(!G || G.mode!=="solo" || G.over) return;
  lsSet(SAVE_KEY,{
    diff:G.diff, turn:G.turn, sShots:G.sShots, sHits:G.sHits,
    fleets:{p1:serializeFleet(G.fleets.p1), p2:serializeFleet(G.fleets.p2)},
    shotsP1:G.shots.p1,
    ai:{diff:G.ai.diff, shots:G.ai.shots, targets:G.ai.targets,
        lastHits:G.ai.lastHits, sunkLens:G.ai.sunkLens},
  });
}
function loadGame(){
  const d=lsGet(SAVE_KEY);
  if(!d || !d.fleets || !d.ai) return null;
  try{
    return {
      mode:"solo", diff:d.diff||"capitan", turn:d.turn||1, over:false, busy:false,
      sShots:d.sShots||0, sHits:d.sHits||0, current:"p1",
      fleets:{p1:reviveFleet(d.fleets.p1), p2:reviveFleet(d.fleets.p2)},
      shots:{p1:d.shotsP1, p2:d.ai.shots},
      ai:{diff:d.ai.diff, shots:d.ai.shots, targets:d.ai.targets||[],
          lastHits:d.ai.lastHits||[], sunkLens:d.ai.sunkLens||[]},
    };
  }catch(e){ return null; }
}

/* ================= ESTADO / UI ================= */
let G=null, placing=null, pending=null; // pending: config previa a colocar
const $=id=>document.getElementById(id);
const show=id=>{document.querySelectorAll(".screen").forEach(s=>s.classList.remove("on")); $(id).classList.add("on");};

function buildLabels(colId,rowId){
  $(colId).innerHTML=Array.from({length:N},(_,i)=>`<span>${i+1}</span>`).join("");
  $(rowId).innerHTML=Array.from({length:N},(_,i)=>`<span>${LETTERS[i]}</span>`).join("");
}
function buildBoard(el,onTap){
  el.innerHTML="";
  for(let r=0;r<N;r++)for(let c=0;c<N;c++){
    const d=document.createElement("div");
    d.className="c"; d.dataset.r=r; d.dataset.c=c;
    if(onTap) d.addEventListener("click",()=>onTap(r,c,d));
    el.appendChild(d);
  }
}
const cellAt=(el,r,c)=>el.children[r*N+c];
function fx(cellEl,cls){
  const f=document.createElement("div"); f.className="fx "+cls;
  cellEl.appendChild(f); setTimeout(()=>f.remove(),700);
}
function log(msg,cls=""){
  const d=document.createElement("div"); d.textContent=msg; if(cls) d.className=cls;
  const l=$("fl_log"); l.prepend(d);
  while(l.children.length>40) l.lastChild.remove();
}

/* ---------- Colocación ---------- */
function startPlacement(){
  placing={grid:emptyGrid(), ships:[], sel:0, horiz:true, names:shuffle(NAMES.slice())};
  buildLabels("fl_cl1","fl_rl1");
  buildBoard($("fl_placeBoard"),onPlaceTap);
  renderChips(); renderPlaceBoard();
  $("fl_btnRot").textContent="⟳ ROTAR: HORIZONTAL";
  $("fl_btnStart").disabled=true;
  $("fl_placeMsg").textContent="Elige un barco y toca el tablero para situar su proa.";
  $("fl_placeTitle").textContent = pending.mode==="duel"
    ? `JUGADOR ${pending.placingFor==="p1"?1:2} — DESPLIEGUE`
    : `DESPLIEGUE DE FLOTA — VS ${DIFFNAMES[pending.diff]}`;
  show("fl_scrPlace");
}
function renderChips(){
  const box=$("fl_chips"); box.innerHTML="";
  SHIPDEFS.forEach((def,i)=>{
    const placed=placing.ships.some(s=>s.def.key===def.key);
    const d=document.createElement("div");
    d.className="chip"+(placed?" placed":"")+(i===placing.sel?" sel":"");
    d.textContent=`${def.label} (${def.len})`;
    d.onclick=()=>{ if(!placed){ placing.sel=i; renderChips(); } };
    box.appendChild(d);
  });
}
function renderPlaceBoard(){
  const b=$("fl_placeBoard");
  for(let r=0;r<N;r++)for(let c=0;c<N;c++)
    cellAt(b,r,c).className="c"+(placing.grid[r][c]!==-1?" ship":"");
}
function onPlaceTap(r,c){
  const def=SHIPDEFS[placing.sel];
  if(!def || placing.ships.some(s=>s.def.key===def.key)) return;
  if(!canPlace(placing.grid,r,c,def.len,placing.horiz)){
    $("fl_placeBoard").classList.add("shake");
    setTimeout(()=>$("fl_placeBoard").classList.remove("shake"),350);
    $("fl_placeMsg").textContent="Ahí no cabe: prueba otra casilla u orientación.";
    return;
  }
  placeShip(placing.grid,placing.ships,def,r,c,placing.horiz,placing.names.pop());
  beep(500,.06,"square",.08);
  const next=SHIPDEFS.findIndex(d=>!placing.ships.some(s=>s.def.key===d.key));
  placing.sel=next;
  renderChips(); renderPlaceBoard();
  if(next===-1){
    $("fl_btnStart").disabled=false;
    $("fl_placeMsg").textContent="Flota desplegada. ¡Lista para zarpar!";
  } else $("fl_placeMsg").textContent="Coloca el siguiente barco.";
}
$("fl_btnRot").onclick=()=>{
  placing.horiz=!placing.horiz;
  $("fl_btnRot").textContent="⟳ ROTAR: "+(placing.horiz?"HORIZONTAL":"VERTICAL");
};
$("fl_btnAuto").onclick=()=>{
  const f=randomFleet();
  placing.grid=f.grid; placing.ships=f.ships; placing.sel=-1;
  renderChips(); renderPlaceBoard();
  $("fl_btnStart").disabled=false;
  $("fl_placeMsg").textContent="Despliegue automático completado.";
  beep(650,.08,"square",.08);
};
$("fl_btnClear").onclick=startPlacement;
$("fl_btnStart").onclick=()=>{
  beep(700,.1,"square",.1);
  const fleet={grid:placing.grid, ships:placing.ships};
  if(pending.mode==="solo"){
    startSolo(fleet);
  } else if(pending.placingFor==="p1"){
    pending.fleetP1=fleet; pending.placingFor="p2";
    handoffMsg("Pásale el móvil al Jugador 2 para que despliegue su flota en secreto.",
      ()=>startPlacement());
  } else {
    startDuel(pending.fleetP1, fleet);
  }
};

/* ---------- Batalla común ---------- */
function initBattleUI(){
  buildLabels("fl_cl2","fl_rl2");
  buildBoard($("fl_enemyBoard"),onFire);
  buildBoard($("fl_ownBoard"),null);
  $("fl_log").innerHTML="";
  show("fl_scrBattle");
}
function renderBoards(){
  // Perspectiva del jugador activo (en solo siempre p1)
  const me=G.current, foe=other(me);
  const myFleet=G.fleets[me], foeFleet=G.fleets[foe];
  const myShots=G.shots[me], foeShots=G.shots[foe];
  const eb=$("fl_enemyBoard"), ob=$("fl_ownBoard");
  for(let r=0;r<N;r++)for(let c=0;c<N;c++){
    // tablero enemigo: solo lo descubierto
    let cls="c"; const v=myShots[r][c];
    if(v===0) cls+=" miss";
    else if(v===1){
      const idx=foeFleet.grid[r][c];
      cls+=(idx!==-1 && foeFleet.ships[idx].sunk)?" sunk":" hit";
    }
    cellAt(eb,r,c).className=cls;
    // tablero propio
    let cls2="c"; const idx2=myFleet.grid[r][c], v2=foeShots[r][c];
    if(idx2!==-1) cls2+=" ship";
    if(v2===0) cls2+=" miss";
    else if((v2===1||v2===2) && idx2!==-1) cls2+= myFleet.ships[idx2].sunk?" sunk":" hit";
    cellAt(ob,r,c).className=cls2;
  }
  renderFleetStatus();
}
function renderFleetStatus(){
  const me=G.current, foe=other(me);
  const mk=(ships,el,hideAlive)=>{
    el.innerHTML="";
    ships.forEach(s=>{
      const sp=document.createElement("span");
      sp.className="st"+(s.sunk?" dead":"");
      sp.textContent=s.def.label+(s.sunk||hideAlive?"":" "+(s.def.len-s.hits)+"/"+s.def.len);
      sp.onclick=()=>showShipInfo(s,hideAlive);
      el.appendChild(sp);
    });
  };
  mk(G.fleets[foe].ships,$("fl_enemyFleet"),true);
  mk(G.fleets[me].ships,$("fl_ownFleet"),false);
}
const SHIPDESCS={
  pa:"El coloso de la flota. Plataforma de mando y ojos en el cielo: imponente, pero difícil de esconder.",
  ac:"Artillería pesada de largo alcance. Lento de maniobrar, devastador cuando encuentra su blanco.",
  de:"Escolta rápida y agresiva. El cazador natural de submarinos.",
  su:"Invisible bajo la superficie. Golpea donde nadie mira.",
  pt:"Pequeña, veloz y escurridiza. El objetivo más difícil de acertar del tablero.",
};
function showShipInfo(s,isEnemy){
  $("fl_shipTitle").textContent=s.def.label;
  const cells=$("fl_shipCells"); cells.innerHTML="";
  for(let i=0;i<s.def.len;i++){
    const c=document.createElement("span");
    if(s.sunk || (!isEnemy && i<s.hits)) c.className="dmg";
    cells.appendChild(c);
  }
  const est = s.sunk ? "HUNDIDO"
    : isEnemy ? "EN SERVICIO — posición desconocida"
    : `OPERATIVO — integridad ${s.def.len-s.hits}/${s.def.len}`;
  $("fl_shipDesc").innerHTML =
    `${SHIPDESCS[s.def.key]}<br><br>`+
    `ESLORA: <b>${s.def.len} CASILLAS</b><br>ESTADO: <b>${est}</b>`+
    (isEnemy?"":`<br>NOMBRE: «${s.name}»`);
  $("fl_shipModal").classList.add("on");
  beep(520,.06,"square",.06);
}
function setTurnUI(youTxt,foeMode){
  $("fl_turnNum").textContent="T."+G.turn;
  const t=$("fl_turnState");
  t.textContent=youTxt;
  t.className=foeMode?"foe":"you";
}

/* ---------- Un jugador ---------- */
function startSolo(playerFleet){
  G={
    mode:"solo", diff:pending.diff, over:false, busy:false, current:"p1",
    fleets:{p1:playerFleet, p2:randomFleet()},
    ai:makeAI(pending.diff),
    shots:{p1:emptyGrid(), p2:null},
    turn:1, sShots:0, sHits:0,
  };
  G.shots.p2=G.ai.shots;
  initBattleUI();
  renderBoards(); setTurnUI("TU TURNO",false);
  log(`Operación iniciada. Enemigo: ${DIFFNAMES[G.diff]}.`,"a");
  saveGame();
}
function resumeSolo(saved){
  G=saved;
  initBattleUI();
  renderBoards(); setTurnUI("TU TURNO",false);
  log(`Operación reanudada en el turno ${G.turn}. Enemigo: ${DIFFNAMES[G.diff]}.`,"a");
}
function onFire(r,c,el){
  if(!G || G.over || G.busy) return;
  if(G.mode==="solo") soloFire(r,c,el);
  else duelFire(r,c,el);
}
function soloFire(r,c,el){
  if(G.shots.p1[r][c]!==-1) return;
  G.busy=true; sndFire();
  const res=fireAt(G.fleets.p2,r,c);
  G.shots.p1[r][c]=(res.result==="miss")?0:1;
  G.sShots++; if(res.result!=="miss") G.sHits++;
  setTimeout(()=>{
    showShotResult(el,r,c,res,true);
    renderBoards();
    if(fleetDestroyed(G.fleets.p2)) return endSolo(true);
    if(res.result!=="miss"){ G.busy=false; saveGame(); return; } // acierto: repites
    setTurnUI("FLOTA ENEMIGA EN MOVIMIENTO…",true);
    saveGame();
    setTimeout(aiTurn, 800);
  }, 220);
}
function showShotResult(el,r,c,res,mine){
  if(res.result==="miss"){
    fx(el,"splash"); sndMiss();
    log(`${coord(r,c)} — AGUA.`);
  } else if(res.result==="sunk"){
    fx(el,"boom"); sndSunk();
    log(`${coord(r,c)} — ¡${res.ship.def.label} «${res.ship.name}» HUNDIDO!`, mine?"g":"r");
  } else {
    fx(el,"boom"); sndHit();
    log(`${coord(r,c)} — IMPACTO CONFIRMADO.`, mine?"g":"r");
  }
}
function aiTurn(){
  if(!G || G.over) return;
  const [r,c]=aiNextShot(G.ai);
  const res=fireAt(G.fleets.p1,r,c);
  aiRegister(G.ai,r,c,res.result,res.ship);
  const el=cellAt($("fl_ownBoard"),r,c);
  if(res.result==="miss"){
    fx(el,"splash"); beep(260,.2,"sine",.08,110);
    log(`Enemigo dispara a ${coord(r,c)} — agua.`);
  } else {
    fx(el,"boom"); sndHit(); vib(res.result==="sunk"?[120,60,250]:180);
    document.querySelector("#game-fl main").classList.add("shake");
    setTimeout(()=>document.querySelector("#game-fl main").classList.remove("shake"),350);
    if(res.result==="sunk")
      log(`¡Nuestro ${res.ship.def.label} «${res.ship.name}» ha sido hundido!`,"r");
    else
      log(`Impacto enemigo en ${coord(r,c)} (${res.ship.def.label}).`,"r");
  }
  renderBoards();
  if(fleetDestroyed(G.fleets.p1)) return endSolo(false);
  if(res.result!=="miss"){ saveGame(); return setTimeout(aiTurn, 800); } // la IA también repite
  G.turn++; G.busy=false; setTurnUI("TU TURNO",false);
  saveGame();
}
function endSolo(win){
  G.over=true; lsDel(SAVE_KEY);
  const s=getStats();
  s.played++; s.shots+=G.sShots; s.hits+=G.sHits;
  if(win){ s.wins++; s.streak++; s.best=Math.max(s.best,s.streak); }
  else { s.losses++; s.streak=0; }
  lsSet(STATS_KEY,s);
  const acc=G.sShots?Math.round(100*G.sHits/G.sShots):0;
  finishScreen(win?"VICTORIA":"FLOTA PERDIDA", win,
    win ? `Flota ${DIFFNAMES[G.diff]} aniquilada en ${G.turn} turnos. Precisión: ${acc}%.`
        : `Nuestra flota descansa en el fondo del mar. Precisión: ${acc}%.`);
}

/* ---------- Dos jugadores ---------- */
function startDuel(f1,f2){
  G={
    mode:"duel", over:false, busy:false, current:"p1",
    fleets:{p1:f1,p2:f2},
    shots:{p1:emptyGrid(), p2:emptyGrid()},
    turn:1,
  };
  handoffMsg("Pásale el móvil al Jugador 1. Comienza la batalla.",()=>{
    initBattleUI();
    renderBoards(); duelTurnUI();
    log("Batalla iniciada. Jugador 1 abre fuego.","a");
  });
}
function duelTurnUI(){
  setTurnUI(`JUGADOR ${G.current==="p1"?1:2} — TU TURNO`,false);
  $("fl_enemyTitle").textContent=`MAPA TÁCTICO — FLOTA DEL JUGADOR ${G.current==="p1"?2:1}`;
}
function duelFire(r,c,el){
  const me=G.current, foe=other(me);
  if(G.shots[me][r][c]!==-1) return;
  G.busy=true; sndFire();
  const res=fireAt(G.fleets[foe],r,c);
  G.shots[me][r][c]=(res.result==="miss")?0:1;
  setTimeout(()=>{
    showShotResult(el,r,c,res,true);
    renderBoards();
    if(fleetDestroyed(G.fleets[foe])){
      G.over=true;
      return finishScreen(`VICTORIA DEL JUGADOR ${me==="p1"?1:2}`, true,
        `La flota del Jugador ${foe==="p1"?1:2} ha sido aniquilada en ${G.turn} turnos.`);
    }
    if(res.result!=="miss"){ G.busy=false; return; } // acierto: el mismo jugador repite
    setTimeout(()=>{
      G.current=foe; if(foe==="p1") G.turn++;
      handoffMsg(`Pásale el móvil al Jugador ${foe==="p1"?1:2}.`,()=>{
        renderBoards(); duelTurnUI();
        $("fl_log").innerHTML="";
        log(`Turno del Jugador ${foe==="p1"?1:2}.`,"a");
        G.busy=false;
      });
    }, 1300);
  }, 220);
}
function handoffMsg(msg,cb){
  $("fl_handMsg").textContent=msg;
  $("fl_handoff").classList.add("on");
  $("fl_btnHand").onclick=()=>{ $("fl_handoff").classList.remove("on"); beep(600,.08,"square",.08); cb(); };
}

/* ---------- Final y estadísticas ---------- */
function finishScreen(title,win,msg){
  setTimeout(()=>{
    $("fl_endTitle").textContent=title;
    $("fl_endTitle").className=win?"win":"lose";
    $("fl_endMsg").textContent=msg;
    $("fl_endModal").classList.add("on");
    win?sndWin():sndLose();
    if(win) vib([80,60,80,60,200]);
  }, 600);
}
function renderStats(){
  const s=getStats();
  const pct=s.played?Math.round(100*s.wins/s.played):0;
  const acc=s.shots?Math.round(100*s.hits/s.shots):0;
  $("fl_statsBody").innerHTML=`
    <div class="statrow"><span>Partidas (vs IA)</span><b>${s.played}</b></div>
    <div class="statrow"><span>Victorias</span><b>${s.wins}</b></div>
    <div class="statrow"><span>Derrotas</span><b>${s.losses}</b></div>
    <div class="statrow"><span>% de victorias</span><b>${pct}%</b></div>
    <div class="statrow"><span>Disparos</span><b>${s.shots}</b></div>
    <div class="statrow"><span>Precisión</span><b>${acc}%</b></div>
    <div class="statrow"><span>Racha actual</span><b>${s.streak}</b></div>
    <div class="statrow"><span>Mejor racha</span><b>${s.best}</b></div>`;
}

/* ---------- Menú y navegación ---------- */
function refreshMenu(){
  $("fl_btnResume").style.display = loadGame() ? "block" : "none";
  $("fl_diffPanel").style.display="none";
}
$("fl_btnSolo").onclick=()=>{
  const p=$("fl_diffPanel");
  p.style.display=p.style.display==="none"?"block":"none";
  beep(600,.06,"square",.06);
};
document.querySelectorAll("#fl_diffPanel [data-diff]").forEach(b=>{
  b.onclick=()=>{
    pending={mode:"solo", diff:b.dataset.diff};
    beep(700,.08,"square",.08);
    startPlacement();
  };
});
$("fl_btnDuel").onclick=()=>{
  pending={mode:"duel", placingFor:"p1"};
  beep(700,.08,"square",.08);
  startPlacement();
};
$("fl_btnResume").onclick=()=>{
  const saved=loadGame();
  if(saved) resumeSolo(saved); else refreshMenu();
};
$("fl_btnStats").onclick=()=>{ renderStats(); $("fl_statsModal").classList.add("on"); };
$("fl_btnStatsClose").onclick=()=>$("fl_statsModal").classList.remove("on");
$("fl_btnShipClose").onclick=()=>$("fl_shipModal").classList.remove("on");
$("fl_btnHow").onclick=()=>{
  const p=$("fl_howPanel"); p.style.display=p.style.display==="none"?"block":"none";
};
let abandonArmed=null;
$("fl_btnAbandon").onclick=()=>{
  const b=$("fl_btnAbandon");
  if(abandonArmed){
    clearTimeout(abandonArmed); abandonArmed=null;
    b.textContent="VOLVER AL MENÚ";
    refreshMenu(); show("fl_scrMenu");
  } else {
    b.textContent= G && G.mode==="solo" && !G.over
      ? "LA PARTIDA QUEDA GUARDADA — TOCA OTRA VEZ"
      : "¿SEGURO? TOCA OTRA VEZ";
    abandonArmed=setTimeout(()=>{
      abandonArmed=null; b.textContent="VOLVER AL MENÚ";
    },3000);
  }
};
$("fl_btnAgain").onclick=()=>{
  $("fl_endModal").classList.remove("on");
  if(G.mode==="duel") pending={mode:"duel", placingFor:"p1"};
  startPlacement();
};
$("fl_btnMenu").onclick=()=>{ $("fl_endModal").classList.remove("on"); refreshMenu(); show("fl_scrMenu"); };
$("fl_sndBtn").onclick=()=>{ muted=!muted; $("fl_sndBtn").textContent=muted?"🔇":"🔊"; };

refreshMenu();
__exp.showMenu=function(){ refreshMenu(); show("fl_scrMenu"); };

__exp.start=function(){ __active=true; };
__exp.stop=function(){ __active=false; };
return __exp;
})();

/* ===== NOCTIS ===== */
const GameNC=(function(){
const __exp={};
let __active=false;

"use strict";
const cv=document.getElementById("nc_cv"), ctx=cv.getContext("2d");
let W=0,H=0,DPR=1,ovl=null,ovx=null;
function resize(){
  DPR=Math.min(window.devicePixelRatio||1,2);
  W=window.innerWidth; H=window.innerHeight;
  cv.width=W*DPR; cv.height=H*DPR;
  ctx.setTransform(DPR,0,0,DPR,0,0);
  ovl=document.createElement("canvas"); ovl.width=W; ovl.height=H;
  ovx=ovl.getContext("2d");
  buildBackdrops();
}
window.addEventListener("resize",resize);
function mulberry(seed){ return function(){ let t=seed+=0x6D2B79F5;
  t=Math.imul(t^t>>>15,t|1); t^=t+Math.imul(t^t>>>7,t|61);
  return ((t^t>>>14)>>>0)/4294967296; }; }
const clamp=(v,a,b)=>v<a?a:v>b?b:v;
const sign=v=>v<0?-1:1;
function lsGet(k){ try{ const v=localStorage.getItem(k); return v?JSON.parse(v):null; }catch(e){ return null; } }
function lsSet(k,v){ try{ localStorage.setItem(k,JSON.stringify(v)); }catch(e){} }
function lsDel(k){ try{ localStorage.removeItem(k); }catch(e){} }

/* ---------- Sonido ---------- */
let AC=null, muted=false;
function beep(f,d,type="sine",v=.12,slide=0){
  if(muted||!__active) return;
  try{
    AC=AC||new (window.AudioContext||window.webkitAudioContext)();
    const o=AC.createOscillator(), g=AC.createGain();
    o.type=type; o.frequency.value=f;
    if(slide) o.frequency.exponentialRampToValueAtTime(slide,AC.currentTime+d);
    g.gain.setValueAtTime(v,AC.currentTime);
    g.gain.exponentialRampToValueAtTime(.001,AC.currentTime+d);
    o.connect(g); g.connect(AC.destination); o.start(); o.stop(AC.currentTime+d);
  }catch(e){}
}
const sJump=()=>beep(320,.18,"sine",.1,520);
const sOrb =()=>{beep(880,.12,"sine",.09,1320);};
const sDie =()=>beep(220,.5,"sawtooth",.14,60);
const sCheck=()=>{beep(520,.15,"triangle",.1); setTimeout(()=>beep(780,.25,"triangle",.1),120);};
const sWin =()=>[440,554,659,880].forEach((f,i)=>setTimeout(()=>beep(f,.3,"triangle",.12),i*170));
const sThrow=()=>beep(650,.08,"square",.07,300);
const sHitE =()=>{beep(180,.12,"square",.12,80);};
const sHurt =()=>beep(140,.3,"sawtooth",.16,60);
const sAlert=()=>beep(980,.12,"square",.09);
const sDraw =()=>beep(240,.25,"sine",.06,420);
const sArrow=()=>beep(500,.1,"square",.07,180);
const sCaw  =()=>{beep(760,.09,"square",.09,520);};
const sPick =()=>beep(560,.1,"triangle",.09,840);
const sHook =()=>beep(420,.14,"square",.09,900);
const sFail =()=>beep(180,.12,"sine",.07);
const sSmoke=()=>beep(120,.5,"sine",.1,60);
const sBuy  =()=>{beep(660,.1,"triangle",.1); setTimeout(()=>beep(990,.15,"triangle",.1),100);};
const sBlock=()=>beep(1400,.06,"square",.08);
const sShadow=()=>beep(200,.3,"sine",.09,60);
const sBoss =()=>{beep(90,.5,"sawtooth",.16,50); setTimeout(()=>beep(70,.6,"sawtooth",.14,40),260);};
const sSlash=()=>beep(300,.14,"sawtooth",.12,90);
document.getElementById("nc_sndBtn").onclick=e=>{
  muted=!muted; e.target.textContent=muted?"🔇":"🔊";
};

/* ---------- Paletas ---------- */
const ZONES=[
  { name:"LOS TEJADOS", sub:"La noche es el territorio del ladrón.",
    sky:["#070b1e","#101b3f","#27356b"], moon:"#f2ead2", glowc:"160,150,255",
    far:"#0b1230", mid:"#101940", roof:"#161f4a", roofTop:"#2c3a78",
    win:"#ffc46b", orb:"#a8f0ff", seed:11 },
  { name:"EL BARRIO BAJO", sub:"Faroles, vapor y arqueros en los balcones.",
    sky:["#160a08","#33150e","#5c2a17"], moon:"#ffd9a0", glowc:"255,170,90",
    far:"#220e0a", mid:"#301511", roof:"#3a1c14", roofTop:"#6b3a24",
    win:"#ffde8a", orb:"#ffd27a", seed:47 },
  { name:"LOS ACUEDUCTOS", sub:"Aquí anida la bandada. No dejes de correr.",
    sky:["#03140f","#07271f","#0e4436"], moon:"#d7fff0", glowc:"110,255,200",
    far:"#062019", mid:"#093026", roof:"#0d3d30", roofTop:"#1c6b54",
    win:"#a0ffe0", orb:"#8affd0", seed:83 },
  { name:"EL OBSERVATORIO", sub:"Los espejos guardan la última luz del mundo.",
    sky:["#0a0620","#1a1240","#332470"], moon:"#fff6da", glowc:"230,200,140",
    far:"#140c30", mid:"#1c1244", roof:"#241b52", roofTop:"#4a3a9e",
    win:"#ffe9b0", orb:"#ffe9a8", seed:129 },
];
const BOSSPAL={ name:"LA TORRE DEL CAZADOR", sub:"",
  sky:["#12050f","#2a0a1e","#4d1030"], moon:"#ffb9c8", glowc:"255,120,160",
  far:"#1c0714", mid:"#28091c", roof:"#320d22", roofTop:"#6b1c42",
  win:"#ff9fb4", orb:"#ffc46b", seed:200 };

/* ---------- Estado ---------- */
const GADGETS=["dg","hk","sm","sh"];
const GICON={dg:"✦", hk:"🪝", sm:"💨", sh:"🌑"};
const state={
  mode:"story", zone:0, pal:ZONES[0], lvl:null, running:false, bossMode:false,
  px:60, py:0, vx:0, vy:0, onGround:false, crouch:false, airJumps:0,
  coyote:0, jbuf:0, face:1, animT:0, dashT:0, dashCd:0,
  cam:0, deaths:0, orbsGot:0, kills:0, bank:0,
  hearts:3, invuln:0, kb:0,
  daggers:3, smoke:2, smokeT:0, throwCd:0,
  umbra:3, shadow:false,
  gadget:"dg", hook:null,
  up:{dbl:false,dash:false,maxHearts:3,dagCap:6,smokeMax:2,hookLen:310},
  chase:null, boss:null, dist:0,
  spawn:{x:60,y:0}, scarf:[], parts:[], shots:[], t:0,
  end:{x:0,y:0,seg:0,rng:null}, // cursor del modo sin fin
};
const rec=Object.assign({boss:0,endless:0}, lsGet("noctis_rec")||{});

/* ---------- Generación ---------- */
const SPEED=250, JUMPV=640, GRAV=1800;
function newLvl(){ return {plats:[],orbs:[],spikes:[],checks:[],deco:[],anchors:[],
  chests:[],hearts:[],steams:[],pends:[],enemies:[],pickups:[],door:null}; }

function addSegment(lvl,rng,cur,zi,swing,diff){
  const prevY=cur.y;
  let gap,w;
  if(swing){
    gap=210+rng()*45;
    cur.y=clamp(cur.y+rng()*50, H*0.28, H*0.78);
    w=150+rng()*110;
  } else {
    gap=60+rng()*80;
    cur.y=clamp(cur.y+(rng()*136)-80, H*0.28, H*0.78);
    w=110+rng()*160;
  }
  cur.x+=gap;
  const p={x:cur.x, y:cur.y, w, h:500};
  lvl.plats.push(p);
  if(swing){
    lvl.anchors.push({x:cur.x-gap/2, y:Math.min(prevY,cur.y)-145});
    if(cur.lastPlat) lvl.checks.push({x:cur.lastPlat.x+cur.lastPlat.w-40, y:prevY, done:false});
    lvl.orbs.push({x:cur.x-gap/2, y:Math.min(prevY,cur.y)-60, t:rng()*7, got:false});
  } else {
    if(rng()<.85) lvl.orbs.push({x:cur.x-gap/2, y:cur.y-70-rng()*40, t:rng()*7, got:false});
    if(w>200 && rng()<.5){
      lvl.spikes.push({x:cur.x+w/2-22, y:cur.y, w:44}); p.spiked=true;
    }
    if(rng()<.5){
      const d={x:cur.x+20+rng()*(w-40), y:cur.y, r:rng()};
      lvl.deco.push(d);
      lvl.anchors.push({x:d.x, y:d.y-6, lantern:true});  // farolillos enganchables
    }
    if(cur.seg>0 && cur.seg%8===0) lvl.checks.push({x:cur.x+w/2, y:cur.y, done:false});
    // trampas
    if(zi>=1 && !p.spiked && w>150 && rng()<.16+diff*.06)
      lvl.steams.push({x:cur.x+w*.6, y:cur.y, ph:rng()*3});
    if(zi>=2 && !p.spiked && w>150 && rng()<.14+diff*.05)
      lvl.pends.push({x:cur.x+w*.35, y:cur.y-170, len:95, ph:rng()*7});
    // cofres, corazones
    if(!p.spiked && w>170 && rng()<.14) lvl.chests.push({x:cur.x+w-40, y:cur.y-14, open:false});
    if(!p.spiked && rng()<.11) lvl.hearts.push({x:cur.x+30+rng()*(w-60), y:cur.y-40, got:false, t:rng()*7});
  }
  cur.lastPlat=p; cur.seg++;
  cur.x+=w;
  return p;
}
function addEnemiesFor(lvl,p,rng,zi,idx,counts,diff){
  if(idx<3) return;
  const m=1+diff;
  if(!p.spiked && p.w>175 && counts.h<Math.floor(zi/2)+ (zi>=2?1:0) && zi>=2 && rng()<.18*m){
    lvl.enemies.push({type:"h", plat:p, x:p.x+p.w/2, sx:p.x+p.w/2,
      x1:p.x+16, x2:p.x+p.w-16, dir:rng()<.5?-1:1,
      state:"patrol", t:0, hp:4, flash:0, dead:false});
    counts.h++; return;
  }
  if(!p.spiked && p.w>175 && counts.g<3+zi && rng()<(.30+zi*.07)*m){
    lvl.enemies.push({type:"g", plat:p, x:p.x+p.w/2, sx:p.x+p.w/2,
      x1:p.x+16, x2:p.x+p.w-16, dir:rng()<.5?-1:1,
      state:"patrol", t:0, hp:2, flash:0, dead:false});
    counts.g++; return;
  }
  if(zi>=1 && !p.spiked && p.w<=175 && counts.a<2+zi && rng()<.28*m){
    lvl.enemies.push({type:"a", plat:p, x:p.x+p.w/2, y:p.y,
      dir:-1, state:"idle", t:0, hp:1, flash:0, dead:false});
    counts.a++; return;
  }
  if(zi>=1 && counts.c<zi*2 && rng()<(zi>=2?.24:.10)*m){
    const by=p.y-170-rng()*40;
    lvl.enemies.push({type:"c", x:p.x, sx:p.x, y:by, baseY:by,
      x1:p.x-70, x2:p.x+p.w+70, dir:1,
      state:"fly", t:0, hp:1, flash:0, dead:false, vx:0, vy:0});
    counts.c++; return;
  }
  if(!p.spiked && rng()<.32 && lvl.pickups.length<7)
    lvl.pickups.push({x:p.x+30+rng()*(p.w-60), y:p.y-16, got:false, t:rng()*7});
}
function genLevel(zi){
  const z=ZONES[zi], rng=mulberry(z.seed*1000+7), erng=mulberry(z.seed*77+13);
  const lvl=newLvl();
  const cur={x:320, y:H*0.62, seg:0, lastPlat:null};
  lvl.plats.push({x:-200,y:cur.y,w:520,h:400});
  cur.lastPlat=lvl.plats[0];
  const counts={g:0,a:0,c:0,h:0};
  const plist=[];
  for(let i=0;i<26;i++){
    const p=addSegment(lvl,rng,cur,zi,(i%9===5),0);
    plist.push(p);
  }
  plist.forEach((p,idx)=>addEnemiesFor(lvl,p,erng,zi,idx+1,counts,0));
  lvl.door={x:cur.x+90, y:cur.y, w:54, h:96};
  lvl.plats.push({x:cur.x+40, y:cur.y, w:260, h:500});
  // persecución en los Acueductos
  if(zi===2 && plist[9]) lvl.chaseX=plist[9].x;
  return lvl;
}
function genBossLevel(){
  const lvl=newLvl();
  const gy=H*0.7;
  lvl.plats.push({x:-200, y:gy, w:1400, h:500});
  lvl.plats.push({x:150, y:gy-115, w:150, h:26});
  lvl.plats.push({x:760, y:gy-115, w:150, h:26});
  lvl.anchors.push({x:330, y:H*0.22});
  lvl.anchors.push({x:700, y:H*0.22});
  lvl.arena={x1:20, x2:1040, gy};
  return lvl;
}

/* ---------- Fondos ---------- */
let bgSky=null, bgFar=null, bgMid=null;
function buildBackdrops(){
  if(!W||!state.pal) return;
  const z=state.pal;
  const rng=mulberry(z.seed);
  bgSky=document.createElement("canvas");
  bgSky.width=W; bgSky.height=H;
  const s=bgSky.getContext("2d");
  const gr=s.createLinearGradient(0,0,0,H);
  gr.addColorStop(0,z.sky[0]); gr.addColorStop(.55,z.sky[1]); gr.addColorStop(1,z.sky[2]);
  s.fillStyle=gr; s.fillRect(0,0,W,H);
  for(let i=0;i<90;i++){
    s.globalAlpha=.25+rng()*.6;
    s.fillStyle="#fff"; s.beginPath(); s.arc(rng()*W,rng()*H*.7,rng()*1.3+.3,0,7); s.fill();
  }
  s.globalAlpha=1;
  const mx=W*.72, my=H*.24, mr=Math.min(W,H)*.13;
  const halo=s.createRadialGradient(mx,my,mr*.4,mx,my,mr*3.2);
  halo.addColorStop(0,`rgba(${z.glowc},.32)`); halo.addColorStop(1,"rgba(0,0,0,0)");
  s.fillStyle=halo; s.fillRect(0,0,W,H);
  s.fillStyle=z.moon; s.beginPath(); s.arc(mx,my,mr,0,7); s.fill();
  s.fillStyle="rgba(0,0,0,.08)";
  s.beginPath(); s.arc(mx-mr*.3,my-mr*.2,mr*.22,0,7); s.fill();
  bgFar=makeSkyline(W*2,H,z.far,.5,z,rng,true);
  bgMid=makeSkyline(W*2,H,z.mid,.75,z,rng,false);
}
function makeSkyline(w,h,color,base,z,rng,towers){
  const c=document.createElement("canvas"); c.width=w; c.height=h;
  const s=c.getContext("2d");
  let x=0;
  while(x<w){
    const bw=towers?(50+rng()*70):(70+rng()*110);
    const bh=h*(towers?(.35+rng()*.4):(.2+rng()*.3));
    const by=h*base+(towers?0:h*.12)-bh;
    s.fillStyle=color; s.fillRect(x,by,bw,h);
    if(towers&&rng()<.5){
      s.beginPath(); s.arc(x+bw/2,by,bw/2,Math.PI,0); s.fill();
      s.fillStyle=z.win; s.globalAlpha=.9;
      s.beginPath(); s.arc(x+bw/2,by-bw/2-16,3,0,7); s.fill();
      s.globalAlpha=1; s.fillStyle=color;
    }
    s.fillStyle=z.win;
    for(let wy=by+14; wy<h*base+h*.1; wy+=22)
      for(let wx=x+8; wx<x+bw-8; wx+=16)
        if(rng()<.16){ s.globalAlpha=.5+rng()*.5; s.fillRect(wx,wy,4,6); }
    s.globalAlpha=1;
    x+=bw+(towers?30+rng()*60:6+rng()*20);
  }
  return c;
}

/* ---------- Carga de zonas ---------- */
function loadZone(zi){
  state.mode="story"; state.zone=zi; state.pal=ZONES[zi]; state.bossMode=false;
  state.lvl=genLevel(zi);
  state.orbsGot=0;
  state.spawn={x:60, y:state.lvl.plats[0].y-60};
  state.hearts=state.up.maxHearts;
  state.daggers=Math.max(3,Math.min(state.daggers,state.up.dagCap));
  state.smoke=state.up.smokeMax; state.umbra=3;
  state.chase = state.lvl.chaseX ? {on:false, x:-9999} : null;
  state.boss=null;
  respawn(false);
  buildBackdrops();
  state.scarf=Array.from({length:12},()=>({x:state.px,y:state.py}));
  saveRun(); updateHUD();
}
function loadBoss(){
  state.mode="story"; state.pal=BOSSPAL; state.bossMode=true;
  state.lvl=genBossLevel();
  state.spawn={x:90, y:state.lvl.arena.gy-60};
  state.hearts=state.up.maxHearts; state.smoke=state.up.smokeMax; state.umbra=3;
  state.chase=null;
  state.boss={x:820, y:state.lvl.arena.gy-30, hp:24, maxHp:24, dir:-1,
    state:"walk", t:0, flash:0, atkCd:1.5, orbCd:2.2, tpCd:5, crowCd:3, fade:1};
  respawn(false);
  buildBackdrops();
  state.scarf=Array.from({length:12},()=>({x:state.px,y:state.py}));
  sBoss(); updateHUD();
}
function loadEndless(){
  state.mode="endless"; state.zone=0; state.pal=ZONES[0]; state.bossMode=false;
  state.lvl=newLvl();
  const y0=H*0.62;
  state.lvl.plats.push({x:-200,y:y0,w:520,h:400});
  state.end={x:320, y:y0, seg:0, lastPlat:state.lvl.plats[0],
    rng:mulberry((Date.now()&0xffff)+3), erng:mulberry((Date.now()&0xffff)+99),
    counts:{g:0,a:0,c:0,h:0}};
  state.spawn={x:60,y:y0-60};
  state.hearts=state.up.maxHearts; state.daggers=Math.max(3,state.daggers);
  state.smoke=state.up.smokeMax; state.umbra=3;
  state.orbsGot=0; state.dist=0; state.chase=null; state.boss=null;
  extendEndless();
  respawn(false);
  buildBackdrops();
  state.scarf=Array.from({length:12},()=>({x:state.px,y:state.py}));
  updateHUD();
}
function extendEndless(){
  const e=state.end, lvl=state.lvl;
  const diff=Math.min(1, state.px/5000);
  while(e.x < state.cam + W*2.5){
    const zi=Math.min(3, Math.floor(e.seg/14)%4);
    if(zi!==state.zone && e.seg%14===0){ state.zone=zi; state.pal=ZONES[zi]; buildBackdrops(); }
    const swing=(e.seg%9===5);
    const p=addSegment(lvl,e.rng,e,zi,swing,diff);
    addEnemiesFor(lvl,p,e.erng,zi,e.seg+3,e.counts,diff);
    if(e.seg%10===0){ e.counts={g:0,a:0,c:0,h:0}; }
  }
  // poda de lo que queda muy atrás
  const cut=state.cam-900;
  for(const k of ["plats","orbs","spikes","deco","anchors","chests","hearts","steams","pends","pickups","checks"])
    lvl[k]=lvl[k].filter(o=>(o.x+(o.w||0))>cut);
  lvl.enemies=lvl.enemies.filter(o=>o.x>cut-200 && !o.dead);
}

/* ---------- Guardado ---------- */
function saveRun(){
  if(state.mode!=="story") return;
  lsSet("noctis_save",{zone:state.zone, bank:state.bank, up:state.up,
    daggers:state.daggers, kills:state.kills, deaths:state.deaths});
}
function saveRec(){ lsSet("noctis_rec",rec); }

/* ---------- Respawn / HUD ---------- */
function respawn(died){
  state.px=state.spawn.x; state.py=state.spawn.y;
  state.vx=0; state.vy=0; state.kb=0; state.hook=null; state.smokeT=0;
  state.shadow=false; state.dashT=0;
  state.cam=Math.max(0,state.px-W*.35);
  state.shots.length=0;
  state.invuln=1.2;
  if(state.lvl) for(const e of state.lvl.enemies){
    if(e.dead) continue;
    if(e.type==="g"||e.type==="h"){ e.x=e.sx; e.state="patrol"; e.t=0; }
    if(e.type==="a"){ e.state="idle"; e.t=0; }
    if(e.type==="c"){ e.x=e.sx; e.y=e.baseY; e.state="fly"; e.t=0; }
  }
  if(state.chase && state.chase.on) state.chase.x=state.spawn.x-520;
  if(died){
    state.deaths++;
    if(state.mode==="endless") return endEndless();
    state.hearts=state.up.maxHearts; sDie(); updateHUD();
  }
}
function updateHUD(){
  const hp="❤".repeat(state.hearts)+"♡".repeat(Math.max(0,state.up.maxHearts-state.hearts));
  const um="▮".repeat(Math.round(state.umbra))+"▯".repeat(3-Math.round(state.umbra));
  const dg=state.bossMode?"∞":state.daggers;
  let line1=`<span class="hp">${hp}</span> · ✦<b>${dg}</b> · 💨<b>${state.smoke}</b> · <span class="um">🌑${um}</span> · <b>☾${state.bank}</b>`;
  let line2=state.mode==="endless"
    ? `SIN FIN — ${Math.floor(state.dist)} m (récord ${rec.endless})`
    : state.pal.name;
  document.getElementById("nc_hud").innerHTML=line1+"<br><span style='font-size:11px;opacity:.8'>"+line2+"</span>";
  document.getElementById("nc_btnA").textContent=GICON[state.gadget];
}

/* ---------- Entrada ---------- */
const keys={L:false,R:false,J:false,C:false};
let jPressed=false, cPressed=false;
function bindHold(id,down,up){
  const el=document.getElementById(id);
  const on=e=>{e.preventDefault(); el.classList.add("on"); down();};
  const off=e=>{e.preventDefault(); el.classList.remove("on"); up();};
  el.addEventListener("pointerdown",on);
  el.addEventListener("pointerup",off);
  el.addEventListener("pointercancel",off);
  el.addEventListener("pointerleave",off);
}
bindHold("nc_btnL",()=>keys.L=true,()=>keys.L=false);
bindHold("nc_btnR",()=>keys.R=true,()=>keys.R=false);
bindHold("nc_btnC",()=>{keys.C=true; cPressed=true;},()=>keys.C=false);
bindHold("nc_btnJ",()=>{keys.J=true; jPressed=true;},()=>keys.J=false);
(function(){
  const btn=document.getElementById("nc_btnA");
  const wheelEl=document.getElementById("nc_wheel");
  let holdTimer=null, wheelOpen=false, selIdx=-1, opts=[];
  function openWheel(){
    wheelOpen=true; selIdx=-1;
    wheelEl.innerHTML=""; opts=[];
    const r=btn.getBoundingClientRect();
    const cx=r.left+r.width/2, cy=r.top+r.height/2;
    const angles=[-165,-115,-65,-15];
    GADGETS.forEach((g,i)=>{
      const a=angles[i]*Math.PI/180;
      const o=document.createElement("div");
      o.className="wopt";
      const ox=cx+Math.cos(a)*100, oy=cy+Math.sin(a)*100;
      o.style.left=ox+"px"; o.style.top=oy+"px";
      o.innerHTML=GICON[g]+`<small>${{dg:"DAGA",hk:"GANCHO",sm:"HUMO",sh:"SOMBRA"}[g]}</small>`;
      wheelEl.appendChild(o);
      opts.push({el:o,g,x:ox,y:oy});
    });
    wheelEl.classList.add("on");
    beep(500,.06,"square",.06);
  }
  function trackSel(x,y){
    let best=-1,bd=95;
    opts.forEach((o,i)=>{ const d=Math.hypot(o.x-x,o.y-y); if(d<bd){bd=d;best=i;} });
    if(best!==selIdx){
      selIdx=best;
      opts.forEach((o,i)=>o.el.classList.toggle("sel",i===best));
      if(best>=0) beep(700,.04,"square",.04);
    }
  }
  btn.addEventListener("pointerdown",e=>{
    e.preventDefault(); btn.classList.add("on");
    btn.setPointerCapture(e.pointerId);
    holdTimer=setTimeout(openWheel,230);
  });
  btn.addEventListener("pointermove",e=>{ if(wheelOpen) trackSel(e.clientX,e.clientY); });
  const finish=e=>{
    e.preventDefault(); btn.classList.remove("on");
    clearTimeout(holdTimer);
    if(wheelOpen){
      if(selIdx>=0){ state.gadget=opts[selIdx].g; beep(760,.08,"triangle",.08); updateHUD(); }
      wheelEl.classList.remove("on"); wheelOpen=false;
    } else useGadget();
  };
  btn.addEventListener("pointerup",finish);
  btn.addEventListener("pointercancel",finish);
})();
window.addEventListener("keydown",e=>{
  if(!__active) return;
  if(e.repeat) return;
  if(e.key==="ArrowLeft"||e.key==="a"||e.key==="A") keys.L=true;
  if(e.key==="ArrowRight"||e.key==="d"||e.key==="D") keys.R=true;
  if(e.key==="ArrowDown"||e.key==="s"||e.key==="S"){ keys.C=true; cPressed=true; }
  if(e.key===" "||e.key==="ArrowUp"||e.key==="w"||e.key==="W"){ keys.J=true; jPressed=true; }
  if(e.key==="x"||e.key==="X"||e.key==="j"||e.key==="J") useGadget();
  if(e.key==="q"||e.key==="Q"){
    state.gadget=GADGETS[(GADGETS.indexOf(state.gadget)+1)%GADGETS.length];
    beep(760,.08,"triangle",.08); updateHUD();
  }
});
window.addEventListener("keyup",e=>{
  if(!__active) return;
  if(e.key==="ArrowLeft"||e.key==="a"||e.key==="A") keys.L=false;
  if(e.key==="ArrowRight"||e.key==="d"||e.key==="D") keys.R=false;
  if(e.key==="ArrowDown"||e.key==="s"||e.key==="S") keys.C=false;
  if(e.key===" "||e.key==="ArrowUp"||e.key==="w"||e.key==="W") keys.J=false;
});

/* ---------- Gadgets ---------- */
function useGadget(){
  if(!state.running) return;
  if(state.gadget==="dg"){
    const has = state.bossMode || state.daggers>0;
    if(has && state.throwCd<=0){
      if(!state.bossMode) state.daggers--;
      state.throwCd=.32;
      /* autoapuntado: la daga se guía al enemigo más cercano por delante */
      const ox=state.px+state.face*14, oy=state.py-(state.crouch?6:8);
      let vx=state.face*470, vy=0, best=null, bd=250;
      for(const e of state.lvl.enemies){
        if(e.dead) continue;
        const ey=e.type==="c"?e.y:e.plat.y-18;
        const dx=e.x-ox, dyy=ey-oy;
        if(sign(dx)!==state.face) continue;      // nunca hacia atrás
        const d=Math.hypot(dx,dyy);
        if(d<bd){ bd=d; best={dx,dyy,d}; }
      }
      if(!best && state.boss){
        const gy=state.lvl.arena.gy, dx=state.boss.x-ox, dyy=(gy-34)-oy;
        if(sign(dx)===state.face) best={dx,dyy,d:Math.hypot(dx,dyy)||1};
      }
      if(best){ vx=best.dx/best.d*470; vy=best.dyy/best.d*470; }
      state.shots.push({x:ox, y:oy, vx, vy, from:"p", type:"dg", life:1.4});
      sThrow(); updateHUD();
    } else if(!has) sFail();
  } else if(state.gadget==="hk"){
    if(state.hook){ state.hook=null; return; }
    let best=null, bd=state.up.hookLen;
    for(const a of state.lvl.anchors){
      const dx=a.x-state.px, dy=a.y-state.py;
      if(dy>-20) continue;
      const d=Math.hypot(dx,dy);
      if(d<bd && (sign(dx)===state.face || Math.abs(dx)<60)){ bd=d; best=a; }
    }
    if(best){ state.hook={ax:best.x, ay:best.y, L:Math.max(60,bd)}; sHook(); }
    else sFail();
  } else if(state.gadget==="sm"){
    if(state.smoke>0){
      state.smoke--; state.smokeT=4;
      for(const e of state.lvl.enemies){
        if(e.dead) continue;
        if(e.type==="g"||e.type==="h") e.state="patrol";
        if(e.type==="a") e.state="idle";
        if(e.type==="c" && e.state!=="dive") e.state="fly";
      }
      for(let i=0;i<26;i++)
        state.parts.push({x:state.px+(Math.random()-.5)*70, y:state.py+(Math.random()-.5)*50,
          vx:(Math.random()-.5)*40, vy:-20-Math.random()*30,
          life:1.2+Math.random(), max:2, color:"170,170,185"});
      sSmoke(); updateHUD();
      state.notice={txt:"💨 Los enemigos te han perdido de vista", t:2.4};
    } else sFail();
  } else { // sombra
    if(state.shadow){ state.shadow=false; return; }
    if(state.umbra>0.5){ state.shadow=true; sShadow(); }
    else sFail();
  }
}

/* ---------- Física ---------- */
const PW=22, PH=40, HBW=15;
function hbCY(){ return state.crouch? state.py+10 : state.py; }
function hbHH(){ return state.crouch? 10 : 16; }
function step(dt){
  state.t+=dt; state.animT+=dt;
  state.invuln=Math.max(0,state.invuln-dt);
  state.throwCd=Math.max(0,state.throwCd-dt);
  state.smokeT=Math.max(0,state.smokeT-dt);
  state.dashCd=Math.max(0,state.dashCd-dt);
  if(state.notice) state.notice.t-=dt;
  // umbra
  if(state.shadow){
    state.umbra-=dt;
    if(state.umbra<=0){ state.umbra=0; state.shadow=false; }
    if(Math.random()<.5)
      state.parts.push({x:state.px+(Math.random()-.5)*16, y:state.py+(Math.random()-.5)*24,
        vx:0, vy:-30, life:.5, max:.6, color:"140,110,230"});
  } else state.umbra=Math.min(3, state.umbra+dt*.4);

  const dir=(keys.R?1:0)-(keys.L?1:0);
  if(dir) state.face=dir;

  // dash aéreo con ▼
  if(cPressed){
    cPressed=false;
    if(!state.onGround && state.up.dash && state.dashCd<=0 && !state.hook){
      state.dashT=.17; state.dashCd=.9; state.vy=0;
      beep(520,.12,"square",.09,900);
    }
  }

  if(state.hook){
    state.vy+=GRAV*dt;
    state.vx+=dir*300*dt;
    state.px+=state.vx*dt; state.py+=state.vy*dt;
    const dx=state.px-state.hook.ax, dy=state.py-state.hook.ay;
    const d=Math.hypot(dx,dy);
    if(d>state.hook.L){
      const nx=dx/d, ny=dy/d;
      state.px=state.hook.ax+nx*state.hook.L;
      state.py=state.hook.ay+ny*state.hook.L;
      const dot=state.vx*nx+state.vy*ny;
      state.vx-=dot*nx; state.vy-=dot*ny;
    }
    if(jPressed){
      jPressed=false; state.hook=null;
      state.vy=Math.min(state.vy-280,-260);
      sJump();
    }
  } else if(state.dashT>0){
    state.dashT-=dt;
    state.px+=state.face*560*dt;
    state.parts.push({x:state.px-state.face*10, y:state.py, vx:0, vy:0,
      life:.3, max:.35, color:"255,255,255"});
  } else {
    state.crouch = keys.C && state.onGround;
    state.vx=dir*SPEED*(state.crouch?0.4:1)*(state.shadow?1.15:1);
    state.coyote-=dt; state.jbuf-=dt;
    if(jPressed){ state.jbuf=.12; jPressed=false; }
    if(state.jbuf>0 && !state.crouch){
      if(state.coyote>0){
        state.vy=-JUMPV; state.coyote=0; state.jbuf=0; sJump();
      } else if(state.airJumps>0){
        state.airJumps--; state.vy=-JUMPV*.92; state.jbuf=0; sJump();
        burst(state.px,state.py+PH/2,"200,180,255",8,90);
      }
    }
    if(!keys.J && state.vy<-200) state.vy=-200;
    state.vy+=GRAV*dt;
    state.kb*=Math.pow(.02,dt);
    state.px+=(state.vx+state.kb)*dt;
    state.py+=state.vy*dt;
  }

  state.onGround=false;
  for(const p of state.lvl.plats){
    if(state.px+PW/2>p.x && state.px-PW/2<p.x+p.w){
      if(state.vy>=0 && state.py+PH/2>p.y && state.py+PH/2<p.y+40){
        state.py=p.y-PH/2; state.vy=0; state.onGround=true;
      }
    }
  }
  if(state.onGround){
    state.coyote=.1;
    state.airJumps = state.up.dbl?1:0;
    if(state.hook) state.hook=null;
  }
  state.px=Math.max(state.px, PW/2);
  if(state.bossMode){
    state.px=clamp(state.px, state.lvl.arena.x1, state.lvl.arena.x2);
  }

  for(const s of state.lvl.spikes){
    if(state.px+HBW/2>s.x && state.px-HBW/2<s.x+s.w &&
       state.py+PH/2>s.y-16 && state.py+PH/2<s.y+8){
      if(state.invuln<=0){ damagePlayer(1, -state.face); state.vy=-380; }
    }
  }
  if(state.py>H+140) return respawn(true);

  for(const o of state.lvl.orbs){
    if(!o.got && Math.abs(o.x-state.px)<26 && Math.abs(o.y-state.py)<34){
      o.got=true; state.orbsGot++; state.bank++; sOrb(); updateHUD();
      burst(o.x,o.y,"170,240,255",12,110);
    }
  }
  for(const pk of state.lvl.pickups){
    if(!pk.got && Math.abs(pk.x-state.px)<24 && Math.abs(pk.y-state.py)<34){
      pk.got=true; state.daggers=Math.min(state.up.dagCap,state.daggers+2);
      sPick(); updateHUD(); burst(pk.x,pk.y,"255,255,255",8,90);
    }
  }
  for(const hh of state.lvl.hearts){
    if(!hh.got && Math.abs(hh.x-state.px)<24 && Math.abs(hh.y-state.py)<34){
      if(state.hearts<state.up.maxHearts){
        hh.got=true; state.hearts++; sPick(); updateHUD();
        burst(hh.x,hh.y,"255,120,140",10,100);
      }
    }
  }
  for(const ch of state.lvl.chests){
    if(!ch.open && Math.abs(ch.x-state.px)<26 && Math.abs(ch.y-state.py)<36){
      ch.open=true; openChest(ch);
    }
  }
  for(const c of state.lvl.checks){
    if(!c.done && Math.abs(c.x-state.px)<30 && Math.abs(c.y-(state.py+PH/2))<60){
      c.done=true; state.spawn={x:c.x, y:c.y-60}; sCheck();
      burst(c.x,c.y-40,"255,196,107",14,120);
    }
  }
  // trampas
  for(const st of state.lvl.steams){
    const cy=(state.t+st.ph)%3;
    if(cy>1.7&&cy<2.6){
      if(Math.abs(state.px-st.x)<16 && state.py>st.y-80 && state.py<st.y &&
         state.invuln<=0) damagePlayer(1, -state.face);
    }
  }
  for(const pd of state.lvl.pends){
    const a=Math.sin(state.t*1.6+pd.ph)*1.05;
    const bx=pd.x+Math.sin(a)*pd.len, by=pd.y+Math.cos(a)*pd.len;
    if(Math.hypot(bx-state.px,by-hbCY())<20 && state.invuln<=0)
      damagePlayer(1, sign(state.px-bx));
  }
  // puerta
  if(state.lvl.door){
    const d=state.lvl.door;
    if(state.px>d.x && state.px<d.x+d.w && state.py+PH/2>d.y-d.h-10 && state.py+PH/2<d.y+20)
      return finishZone();
  }
  // persecución
  if(state.chase){
    if(!state.chase.on && state.px>state.lvl.chaseX){
      state.chase.on=true; state.chase.x=state.px-520; state.chase.msg=4;
      sCaw(); setTimeout(sCaw,200); setTimeout(sCaw,420);
    }
    if(state.chase.on){
      state.chase.msg=Math.max(0,(state.chase.msg||0)-dt);
      const chSpd = state.smokeT>0 ? -160 : 190;   // el humo la repele
      state.chase.x+=chSpd*dt;
      if(Math.random()<.02) sCaw();
      if(state.chase.x>state.px-20 && state.invuln<=0){
        damagePlayer(1,1);
        state.chase.x=state.px-340;
      }
    }
  }
  updateEnemies(dt);
  if(state.boss) updateBoss(dt);
  updateShots(dt);

  if(state.mode==="endless"){
    state.dist=Math.max(state.dist, state.px/10);
    extendEndless();
  }

  const target=state.px-W*.38;
  state.cam+=(Math.max(0,target)-state.cam)*Math.min(1,dt*5);
  if(state.bossMode) state.cam=clamp(state.cam,0,Math.max(0,1060-W));
  let hx=state.px-state.face*10, hy=state.py-10;
  for(let i=0;i<state.scarf.length;i++){
    const s2=state.scarf[i];
    s2.x+=(hx-s2.x)*Math.min(1,dt*(16-i)); s2.y+=(hy-s2.y)*Math.min(1,dt*(16-i));
    s2.y+=Math.sin(state.t*6+i)*.4;
    hx=s2.x; hy=s2.y;
  }
  if(state.parts.length<48 && Math.random()<.3){
    state.parts.push({x:state.cam+Math.random()*W, y:Math.random()*H,
      vx:(Math.random()-.5)*20, vy:(Math.random()-.5)*14,
      life:4+Math.random()*4, max:8, amb:true});
  }
  for(let i=state.parts.length-1;i>=0;i--){
    const q=state.parts[i];
    q.x+=q.vx*dt; q.y+=q.vy*dt; q.life-=dt;
    if(q.amb){ q.vx+=(Math.random()-.5)*8*dt; q.vy+=(Math.random()-.5)*8*dt; }
    else q.vy+=300*dt;
    if(q.life<=0) state.parts.splice(i,1);
  }
}
function openChest(ch){
  const roll=Math.random();
  let msg;
  if(roll<.35){ state.bank+=4; msg="255,230,140"; }
  else if(roll<.6){ state.daggers=Math.min(state.up.dagCap,state.daggers+3); msg="255,255,255"; }
  else if(roll<.8){ state.smoke=Math.min(state.up.smokeMax+1,state.smoke+1); msg="170,170,190"; }
  else { state.hearts=Math.min(state.up.maxHearts,state.hearts+1); msg="255,120,140"; }
  burst(ch.x,ch.y-10,msg,16,130);
  sBuy(); updateHUD();
}
function burst(x,y,color,n,sp){
  for(let i=0;i<n;i++){
    const a=Math.random()*7, v=sp*(.4+Math.random()*.8);
    state.parts.push({x,y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-40,
      life:.5+Math.random()*.4, max:.9, color});
  }
}
function damagePlayer(n,fromDir){
  if(state.invuln>0||state.shadow) return;
  state.hearts-=n; state.invuln=1.2;
  state.kb=fromDir*230; state.vy=Math.min(state.vy,-220);
  state.hook=null; state.dashT=0;
  burst(state.px,state.py,"255,120,120",10,120);
  sHurt(); updateHUD();
  if(state.hearts<=0) respawn(true);
}

/* ---------- Enemigos ---------- */
function playerVisibleFrom(ex,ey,edir,dist,vTol){
  if(state.smokeT>0||state.shadow) return false;
  const effDist = state.crouch ? Math.min(dist,90) : dist;
  const dx=state.px-ex, dy=state.py-ey;
  return sign(dx)===edir && Math.abs(dx)<effDist && Math.abs(dy)<vTol;
}
function updateEnemies(dt){
  for(const e of state.lvl.enemies){
    if(e.dead) continue;
    e.flash=Math.max(0,e.flash-dt);
    if(Math.abs(e.x-state.cam-W/2)>W*1.2 && e.state!=="dive") continue;
    if(e.type==="g"||e.type==="h") updateGuard(e,dt);
    else if(e.type==="a") updateArcher(e,dt);
    else updateCrow(e,dt);
  }
}
function updateGuard(e,dt){
  const heavy=e.type==="h";
  const gy=e.plat.y, cy=gy-18;
  const dx=state.px-e.x;
  const pSpd=heavy?45:72, cSpd=heavy?110:165;
  if(e.state==="patrol"){
    e.x+=e.dir*pSpd*dt;
    if(e.x<e.x1){ e.x=e.x1; e.dir=1; }
    if(e.x>e.x2){ e.x=e.x2; e.dir=-1; }
    if(playerVisibleFrom(e.x,cy,e.dir,210,70)){ e.state="detect"; e.t=0; }
  } else if(e.state==="detect"){
    e.t+=dt; e.dir=sign(dx);
    if(!playerVisibleFrom(e.x,cy,e.dir,240,90)) e.state="patrol";
    else if(e.t>.4){ e.state="chase"; sAlert(); }
  } else if(e.state==="chase"){
    if(state.smokeT>0||state.shadow) e.state="patrol";
    else {
      e.dir=sign(dx);
      e.x=clamp(e.x+e.dir*cSpd*dt, e.x1, e.x2);
      if(Math.abs(dx)>420 || Math.abs(state.py-cy)>150) e.state="patrol";
    }
  }
  resolveBodyContact(e, e.x, cy, heavy?30:26, heavy?40:36);
}
function updateArcher(e,dt){
  const cy=e.y-18;
  const dx=state.px-e.x, dy=state.py-cy;
  const inRange=Math.abs(dx)<340 && Math.abs(dy)<130 && state.smokeT<=0 && !state.shadow &&
                (!state.crouch || Math.abs(dx)<90);
  if(e.state==="idle"){
    if(inRange){ e.dir=sign(dx); e.state="aim"; e.t=0; sDraw(); }
  } else if(e.state==="aim"){
    e.t+=dt; e.dir=sign(dx);
    if(!inRange) e.state="idle";
    else if(e.t>.7){
      state.shots.push({x:e.x+e.dir*16, y:e.plat.y-30, vx:e.dir*250, vy:0,
        from:"e", type:"ar", life:3});
      sArrow();
      e.state="cool"; e.t=0;
    }
  } else { e.t+=dt; if(e.t>1.5) e.state="idle"; }
  resolveBodyContact(e, e.x, cy, 24, 36);
}
function updateCrow(e,dt){
  if(e.state==="fly"){
    e.x+=e.dir*90*dt;
    if(e.x<e.x1){ e.x=e.x1; e.dir=1; }
    if(e.x>e.x2){ e.x=e.x2; e.dir=-1; }
    e.y=e.baseY+Math.sin(state.t*3+e.sx)*8;
    const dx=state.px-e.x, dy=state.py-e.y;
    if(state.smokeT<=0 && !state.shadow && Math.abs(dx)<150 && dy>-30 && dy<240){
      e.state="warn"; e.t=0; sCaw();
    }
  } else if(e.state==="warn"){
    e.t+=dt;
    if(e.t>.85){
      const dx=state.px-e.x, dy=state.py-e.y;
      const L=Math.hypot(dx,dy)||1;
      e.vx=dx/L*290; e.vy=dy/L*290;
      e.state="dive"; e.t=0;
    }
  } else if(e.state==="dive"){
    e.t+=dt; e.x+=e.vx*dt; e.y+=e.vy*dt;
    let hitWall=false;
    for(const p of state.lvl.plats)
      if(e.x>p.x&&e.x<p.x+p.w&&e.y>p.y&&e.y<p.y+p.h){ hitWall=true; break; }
    if(e.t>.85||hitWall) e.state="rise";
  } else {
    e.y-=210*dt;
    e.x+=(clamp(e.x,e.x1,e.x2)-e.x)*Math.min(1,dt*3);
    if(e.y<=e.baseY){ e.y=e.baseY; e.state="fly"; }
  }
  resolveBodyContact(e, e.x, e.y, 26, 20);
}
function resolveBodyContact(e,ex,ey,ew,eh){
  if(state.shadow) return;
  const overX=Math.abs(state.px-ex)<(HBW+ew)/2;
  const overY=Math.abs(hbCY()-ey)<(hbHH()*2+eh)/2;
  if(!overX||!overY) return;
  const playerBottom=state.py+PH/2;
  if(state.vy>140 && playerBottom<ey+6){
    if(e.type==="h"){ hitEnemy(e); hitEnemy(e); } else killEnemy(e);
    state.vy=-390; sJump();
    return;
  }
  damagePlayer(1, sign(state.px-ex));
}
function killEnemy(e){
  e.dead=true; state.kills++;
  burst(e.x, (e.type==="c"?e.y:e.plat.y-20), "200,180,255", 14, 140);
  sHitE();
}
function hitEnemy(e){
  e.hp--; e.flash=.15;
  if(e.hp<=0){ if(!e.dead) killEnemy(e); }
  else sHitE();
}

/* ---------- Jefe: EL CAZADOR DE UMBRA ---------- */
function bossPhase(){ const b=state.boss; return b.hp>16?1:(b.hp>8?2:3); }
function updateBoss(dt){
  const b=state.boss, gy=state.lvl.arena.gy;
  b.flash=Math.max(0,b.flash-dt);
  b.t+=dt; b.atkCd-=dt; b.orbCd-=dt; b.tpCd-=dt; b.crowCd-=dt;
  if(b.fade<1) b.fade=Math.min(1,b.fade+dt*2);
  const ph=bossPhase();
  const dx=state.px-b.x;
  const spd=[0,85,125,150][ph];
  if(b.state==="walk"){
    b.dir=sign(dx);
    if(Math.abs(dx)>56) b.x=clamp(b.x+b.dir*spd*dt, state.lvl.arena.x1+30, state.lvl.arena.x2-30);
    else if(b.atkCd<=0){ b.state="slash"; b.t=0; sSlash(); }
    if(b.orbCd<=0){
      const os=ph>=3?190:150;
      state.shots.push({x:b.x+b.dir*20, y:gy-42, vx:sign(dx)*os, vy:0,
        from:"e", type:"ob", life:5});
      b.orbCd=ph>=3?1.6:2.3;
      beep(220,.2,"sine",.1,80);
    }
    if(ph>=2 && b.tpCd<=0 && Math.abs(dx)<140){
      b.tpCd=5; b.fade=0;
      burst(b.x,gy-40,"255,120,160",14,140);
      b.x = state.px + (state.px<530?280:-280);
      b.x=clamp(b.x, state.lvl.arena.x1+40, state.lvl.arena.x2-40);
      beep(160,.3,"sine",.1,700);
    }
    if(ph>=3 && b.crowCd<=0){
      const alive=state.lvl.enemies.filter(e=>e.type==="c"&&!e.dead).length;
      if(alive<2){
        const by=gy-230;
        state.lvl.enemies.push({type:"c", x:b.x, sx:b.x, y:by, baseY:by,
          x1:state.lvl.arena.x1+40, x2:state.lvl.arena.x2-40, dir:sign(dx)||1,
          state:"fly", t:0, hp:1, flash:0, dead:false, vx:0, vy:0});
        sCaw();
      }
      b.crowCd=6;
    }
  } else if(b.state==="slash"){
    if(b.t>.5){
      if(Math.abs(state.px-b.x)<74 && Math.abs(state.py-(gy-30))<60)
        damagePlayer(1, sign(state.px-b.x));
      burst(b.x+b.dir*40, gy-36, "255,120,160", 10, 130);
      b.state="walk"; b.atkCd=1.4;
    }
  }
  // contacto
  if(!state.shadow && state.invuln<=0 &&
     Math.abs(state.px-b.x)<32 && Math.abs(hbCY()-(gy-30))<44){
    const playerBottom=state.py+PH/2;
    if(state.vy>140 && playerBottom<gy-40){
      bossHit(2); state.vy=-390; sJump();
    } else damagePlayer(1, sign(state.px-b.x));
  }
}
function bossHit(n){
  const b=state.boss;
  b.hp-=n; b.flash=.15; sHitE();
  if(b.hp<=0){
    burst(b.x, state.lvl.arena.gy-40, "255,160,190", 40, 220);
    burst(b.x, state.lvl.arena.gy-40, "255,230,150", 30, 160);
    state.boss=null; state.running=false;
    rec.boss++; saveRec(); lsDel("noctis_save");
    sWin(); setTimeout(sWin,500);
    showInter("EL CAZADOR HA CAÍDO",
      `Azhar respira por primera vez en trece años. Lunas: ${state.bank} · Derribos: ${state.kills} · Caídas: ${state.deaths}. Una leyenda blanca recorre los tejados… GRACIAS POR JUGAR.`,
      "VOLVER AL MENÚ", ()=>{ toMenu(); }, false);
  }
  updateHUD();
}

/* ---------- Proyectiles ---------- */
function updateShots(dt){
  for(let i=state.shots.length-1;i>=0;i--){
    const s=state.shots[i];
    s.x+=s.vx*dt; s.y+=s.vy*dt; s.life-=dt;
    let del=s.life<=0 || Math.abs(s.x-(state.cam+W/2))>W;
    if(!del && s.type!=="ob") for(const p of state.lvl.plats)
      if(s.x>p.x&&s.x<p.x+p.w&&s.y>p.y&&s.y<p.y+p.h){ del=true;
        burst(s.x,s.y,"200,200,200",4,60); break; }
    if(!del && s.from==="p"){
      for(const e of state.lvl.enemies){
        if(e.dead) continue;
        const ey=e.type==="c"?e.y:e.plat.y-18;
        if(Math.abs(s.x-e.x)<16 && Math.abs(s.y-ey)<20){
          if(e.type==="h" && sign(s.vx)===-e.dir){   // escudo frontal
            sBlock(); burst(s.x,s.y,"255,255,180",5,80);
          } else hitEnemy(e);
          del=true; break;
        }
      }
      if(!del && state.boss){
        const b=state.boss, gy=state.lvl.arena.gy;
        if(Math.abs(s.x-b.x)<22 && Math.abs(s.y-(gy-34))<34){ bossHit(1); del=true; }
      }
    }
    if(!del && s.from==="e" && !state.shadow){
      if(state.invuln<=0 &&
         Math.abs(s.x-state.px)<HBW/2+(s.type==="ob"?9:4) &&
         Math.abs(s.y-hbCY())<hbHH()+(s.type==="ob"?9:4)){
        damagePlayer(1, sign(s.vx)); del=true;
      }
    }
    if(del) state.shots.splice(i,1);
  }
}

/* ---------- Dibujo ---------- */
function draw(){
  const z=state.pal, cam=state.cam;
  ctx.clearRect(0,0,W,H);
  if(bgSky) ctx.drawImage(bgSky,0,0);
  if(bgFar){ const off=-(cam*.15)%bgFar.width;
    ctx.drawImage(bgFar,off,0); ctx.drawImage(bgFar,off+bgFar.width,0); }
  if(bgMid){ const off=-(cam*.35)%bgMid.width;
    ctx.drawImage(bgMid,off,0); ctx.drawImage(bgMid,off+bgMid.width,0); }
  ctx.save(); ctx.translate(-cam,0);
  for(const p of state.lvl.plats){
    if(p.x+p.w<cam-40||p.x>cam+W+40) continue;
    ctx.fillStyle=z.roof;
    ctx.fillRect(p.x,p.y,p.w,Math.min(p.h,H-p.y+20));
    ctx.fillStyle=z.roofTop; ctx.fillRect(p.x,p.y,p.w,7);
    ctx.fillStyle="rgba(0,0,0,.25)";
    for(let tx=p.x; tx<p.x+p.w-10; tx+=26) ctx.fillRect(tx+18,p.y,3,7);
    if(p.h>100){
      ctx.fillStyle=z.win;
      const wrng=mulberry(p.x|0);
      for(let wy=p.y+34; wy<Math.min(H-10,p.y+220); wy+=44)
        for(let wx=p.x+14; wx<p.x+p.w-16; wx+=38)
          if(wrng()<.28){ ctx.globalAlpha=.35+wrng()*.5;
            ctx.fillRect(wx,wy,9,13); ctx.globalAlpha=1; }
    }
  }
  for(const dcp of state.lvl.deco) drawLantern(dcp,z);
  drawAnchors(z);
  for(const st of state.lvl.steams) drawSteam(st);
  for(const pd of state.lvl.pends) drawPend(pd);
  for(const s of state.lvl.spikes){
    ctx.fillStyle="#0a0c18"; ctx.strokeStyle="rgba(255,255,255,.15)";
    ctx.beginPath();
    for(let sx=s.x; sx<s.x+s.w; sx+=11){
      ctx.moveTo(sx,s.y); ctx.lineTo(sx+5.5,s.y-16); ctx.lineTo(sx+11,s.y);
    }
    ctx.fill(); ctx.stroke();
  }
  for(const c of state.lvl.checks){
    ctx.strokeStyle="rgba(255,255,255,.4)"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.moveTo(c.x,c.y); ctx.lineTo(c.x,c.y-46); ctx.stroke();
    ctx.fillStyle=c.done?"#ffc46b":"rgba(255,255,255,.3)";
    ctx.beginPath(); ctx.moveTo(c.x,c.y-46); ctx.lineTo(c.x+16,c.y-40); ctx.lineTo(c.x,c.y-34);
    ctx.fill();
  }
  for(const ch of state.lvl.chests) drawChest(ch);
  for(const o of state.lvl.orbs){
    if(o.got) continue;
    const oy=o.y+Math.sin(state.t*2+o.t)*6;
    const g=ctx.createRadialGradient(o.x,oy,2,o.x,oy,18);
    g.addColorStop(0,z.orb); g.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(o.x,oy,18,0,7); ctx.fill();
    ctx.fillStyle="#fff"; ctx.beginPath(); ctx.arc(o.x,oy,5,0,7); ctx.fill();
  }
  for(const hh of state.lvl.hearts){
    if(hh.got) continue;
    const hy=hh.y+Math.sin(state.t*2.2+hh.t)*4;
    ctx.fillStyle="#ff6b7d"; ctx.font="16px Georgia"; ctx.textAlign="center";
    ctx.fillText("❤",hh.x,hy);
    const g=ctx.createRadialGradient(hh.x,hy-5,1,hh.x,hy-5,16);
    g.addColorStop(0,"rgba(255,110,130,.3)"); g.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(hh.x,hy-5,16,0,7); ctx.fill();
  }
  for(const pk of state.lvl.pickups){
    if(pk.got) continue;
    const py2=pk.y+Math.sin(state.t*2.4+pk.t)*4;
    ctx.save(); ctx.translate(pk.x,py2); ctx.rotate(state.t*1.5);
    ctx.fillStyle="#f5f2e8";
    ctx.beginPath(); ctx.moveTo(0,-9); ctx.lineTo(3,0); ctx.lineTo(0,9); ctx.lineTo(-3,0); ctx.fill();
    ctx.restore();
  }
  if(state.lvl.door) drawDoor(state.lvl.door,z);
  for(const e of state.lvl.enemies){ if(!e.dead) drawEnemy(e,z); }
  if(state.boss) drawBoss();
  for(const s of state.shots) drawShot(s,z);
  for(const q of state.parts){
    const a=clamp(q.life/q.max,0,1);
    ctx.fillStyle=q.color?`rgba(${q.color},${a})`:`rgba(${z.glowc},${a*.6})`;
    ctx.beginPath(); ctx.arc(q.x,q.y,q.color?2.4:1.8,0,7); ctx.fill();
  }
  if(state.hook){
    ctx.strokeStyle="rgba(255,220,150,.9)"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.moveTo(state.px,state.py-8);
    ctx.lineTo(state.hook.ax,state.hook.ay); ctx.stroke();
  }
  if(state.chase && state.chase.on) drawFlock();
  if(state.invuln<=0 || Math.floor(state.t*14)%2===0) drawPlayer(z);
  ctx.restore();
  // oscuridad de la fase 2 del jefe
  if(state.boss && bossPhase()>=2){
    ovx.clearRect(0,0,W,H);
    ovx.fillStyle="rgba(3,2,12,.8)"; ovx.fillRect(0,0,W,H);
    ovx.globalCompositeOperation="destination-out";
    const holes=[[state.px-state.cam,state.py,150],[state.boss.x-state.cam,state.lvl.arena.gy-40,120]];
    for(const [hx2,hy2,hr] of holes){
      const g=ovx.createRadialGradient(hx2,hy2,10,hx2,hy2,hr);
      g.addColorStop(0,"rgba(0,0,0,1)"); g.addColorStop(1,"rgba(0,0,0,0)");
      ovx.fillStyle=g; ovx.beginPath(); ovx.arc(hx2,hy2,hr,0,7); ovx.fill();
    }
    ovx.globalCompositeOperation="source-over";
    ctx.drawImage(ovl,0,0);
  }
  if(state.boss) drawBossBar();
  if(state.chase && state.chase.on && state.chase.msg>0){
    const al=Math.min(1,state.chase.msg);
    ctx.fillStyle="rgba(255,90,90,"+al+")";
    ctx.font="bold 26px Georgia"; ctx.textAlign="center";
    ctx.fillText("¡LA BANDADA! ¡CORRE!", W/2, H*0.28);
    ctx.fillStyle="rgba(232,224,208,"+al+")";
    ctx.font="13px Georgia";
    ctx.fillText("No se puede vencer: corre a la derecha · la bomba de humo 💨 la repele", W/2, H*0.28+24);
  }
  if(state.notice && state.notice.t>0){
    ctx.fillStyle="rgba(232,224,208,"+Math.min(1,state.notice.t)+")";
    ctx.font="14px Georgia"; ctx.textAlign="center";
    ctx.fillText(state.notice.txt, W/2, H*0.2);
  }
  const vg=ctx.createRadialGradient(W/2,H/2,H*.4,W/2,H/2,H);
  vg.addColorStop(0,"rgba(0,0,0,0)"); vg.addColorStop(1,"rgba(0,0,0,.45)");
  ctx.fillStyle=vg; ctx.fillRect(0,0,W,H);
}
function drawFlock(){
  const fx=state.chase.x;
  const g=ctx.createLinearGradient(fx-260,0,fx+40,0);
  g.addColorStop(0,"rgba(20,8,30,.95)"); g.addColorStop(1,"rgba(20,8,30,0)");
  ctx.fillStyle=g; ctx.fillRect(fx-260,0,300,H);
  for(let i=0;i<14;i++){
    const bx=fx-30-((i*53)%220), by=(i*97)%H;
    const flap=Math.sin(state.t*16+i);
    ctx.strokeStyle="#8a6cf0"; ctx.lineWidth=2.5; ctx.lineCap="round";
    ctx.beginPath();
    ctx.moveTo(bx-10,by-6*flap); ctx.quadraticCurveTo(bx,by-10*flap,bx,by);
    ctx.quadraticCurveTo(bx,by-10*flap,bx+10,by-6*flap);
    ctx.stroke();
  }
}
function drawSteam(st){
  const cy=(state.t+st.ph)%3;
  // boquilla
  ctx.fillStyle="#3a3f55"; ctx.fillRect(st.x-8,st.y-8,16,8);
  if(cy>1.2&&cy<1.7){ // aviso
    for(let i=0;i<2;i++)
      state.parts.length<60 && state.parts.push({x:st.x+(Math.random()-.5)*8,
        y:st.y-10, vx:0, vy:-40, life:.4, max:.5, color:"200,200,210"});
  } else if(cy>1.7&&cy<2.6){ // chorro
    const g=ctx.createLinearGradient(0,st.y,0,st.y-80);
    g.addColorStop(0,"rgba(230,230,240,.85)"); g.addColorStop(1,"rgba(230,230,240,0)");
    ctx.fillStyle=g;
    ctx.fillRect(st.x-10,st.y-80,20,80);
  }
}
function drawPend(pd){
  const a=Math.sin(state.t*1.6+pd.ph)*1.05;
  const bx=pd.x+Math.sin(a)*pd.len, by=pd.y+Math.cos(a)*pd.len;
  ctx.strokeStyle="rgba(200,200,210,.5)"; ctx.lineWidth=2;
  ctx.beginPath(); ctx.moveTo(pd.x,pd.y); ctx.lineTo(bx,by); ctx.stroke();
  ctx.save(); ctx.translate(bx,by); ctx.rotate(-a);
  ctx.fillStyle="#c7ccd8";
  ctx.beginPath(); ctx.moveTo(0,-14); ctx.lineTo(11,6); ctx.lineTo(-11,6); ctx.fill();
  ctx.restore();
}
function drawChest(ch){
  ctx.fillStyle=ch.open?"#4a3a26":"#7a5a2e";
  ctx.fillRect(ch.x-13,ch.y-10,26,16);
  ctx.fillStyle=ch.open?"#3a2c1c":"#9a7440";
  ctx.fillRect(ch.x-13,ch.y-16,26,7);
  ctx.fillStyle="#ffc46b";
  ctx.fillRect(ch.x-2,ch.y-8,4,5);
  if(!ch.open){
    const g=ctx.createRadialGradient(ch.x,ch.y-8,2,ch.x,ch.y-8,20);
    g.addColorStop(0,"rgba(255,196,107,.3)"); g.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(ch.x,ch.y-8,20,0,7); ctx.fill();
  }
}
function drawAnchors(z){
  for(const a of state.lvl.anchors){
    if(a.lantern) continue; // los farolillos ya se dibujan
    ctx.strokeStyle="rgba(255,220,150,.35)"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.moveTo(a.x,a.y-26); ctx.lineTo(a.x,a.y-8); ctx.stroke();
    const near = state.gadget==="hk" &&
      Math.hypot(a.x-state.px, a.y-state.py)<state.up.hookLen && a.y<state.py-20;
    const r = 9 + (near?Math.sin(state.t*6)*2+2:0);
    const g=ctx.createRadialGradient(a.x,a.y,2,a.x,a.y,r*2.6);
    g.addColorStop(0,"rgba(255,214,120,.55)"); g.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(a.x,a.y,r*2.6,0,7); ctx.fill();
    ctx.strokeStyle= near ? "#ffe6a8" : "#d9b566";
    ctx.lineWidth=3.5;
    ctx.beginPath(); ctx.arc(a.x,a.y,r,0,7); ctx.stroke();
  }
}
function drawLantern(dcp,z){
  const ly=dcp.y+14+Math.sin(state.t*1.5+dcp.r*7)*2;
  ctx.strokeStyle="rgba(255,255,255,.25)";
  ctx.beginPath(); ctx.moveTo(dcp.x,dcp.y); ctx.lineTo(dcp.x,ly); ctx.stroke();
  const g=ctx.createRadialGradient(dcp.x,ly+6,1,dcp.x,ly+6,22);
  g.addColorStop(0,`rgba(${z.glowc},.5)`); g.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=g; ctx.beginPath(); ctx.arc(dcp.x,ly+6,22,0,7); ctx.fill();
  ctx.fillStyle=z.win; ctx.fillRect(dcp.x-4,ly,8,12);
}
function drawDoor(d,z){
  const pul=Math.sin(state.t*2)*.15+.85;
  const g=ctx.createRadialGradient(d.x+d.w/2,d.y-d.h/2,4,d.x+d.w/2,d.y-d.h/2,d.h*pul);
  g.addColorStop(0,`rgba(${z.glowc},.7)`); g.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=g;
  ctx.fillRect(d.x-d.h,d.y-d.h*2,d.w+d.h*2,d.h*2.4);
  ctx.fillStyle="#f5edda";
  ctx.beginPath();
  ctx.moveTo(d.x,d.y); ctx.lineTo(d.x,d.y-d.h+d.w/2);
  ctx.arc(d.x+d.w/2,d.y-d.h+d.w/2,d.w/2,Math.PI,0);
  ctx.lineTo(d.x+d.w,d.y); ctx.fill();
}
function drawEnemy(e,z){
  if(e.type==="c") return drawCrow(e);
  const heavy=e.type==="h";
  const gy=e.plat.y, x=e.x, f=e.dir;
  const moving=(e.state==="patrol"||e.state==="chase");
  const ph=Math.sin(state.t*(e.state==="chase"?18:10)+x);
  const body = e.flash>0 ? "#ffffff" : (heavy?"#5f6b80":(e.type==="g" ? "#8e2f3f" : "#2e6f9e"));
  const trim = heavy?"#a8b6cc":(e.type==="g" ? "#d96a7c" : "#7ec3ef");
  const sc=heavy?1.25:1;
  const g=ctx.createRadialGradient(x,gy-26*sc,3,x,gy-26*sc,32*sc);
  g.addColorStop(0, heavy?"rgba(170,190,220,.16)":(e.type==="g"?"rgba(255,120,140,.18)":"rgba(120,195,255,.18)"));
  g.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=g; ctx.beginPath(); ctx.arc(x,gy-26*sc,32*sc,0,7); ctx.fill();
  ctx.save();
  ctx.translate(x,gy); ctx.scale(sc,sc); ctx.translate(-x,-gy);
  ctx.fillStyle=body;
  ctx.save(); ctx.translate(x,gy-12);
  const la=moving?ph*.6:0;
  ctx.fillRect(-6+Math.sin(la)*4, 2, 5, 11);
  ctx.fillRect( 2-Math.sin(la)*4, 2, 5, 11);
  ctx.restore();
  ctx.beginPath(); ctx.ellipse(x,gy-24,9,13,0,0,7); ctx.fill();
  ctx.beginPath(); ctx.arc(x+f*2,gy-38,7.5,0,7); ctx.fill();
  ctx.strokeStyle=trim; ctx.lineWidth=1.5;
  ctx.beginPath(); ctx.arc(x+f*2,gy-38,7.5,0,7); ctx.stroke();
  ctx.fillStyle = e.state==="chase" ? "#ff5b5b" : "#ffc46b";
  ctx.beginPath(); ctx.arc(x+f*5,gy-39,2,0,7); ctx.fill();
  if(heavy){ // escudo frontal
    ctx.fillStyle=e.flash>0?"#fff":"#8d9cb5";
    ctx.strokeStyle="#c9d6ea"; ctx.lineWidth=1.5;
    ctx.beginPath();
    ctx.ellipse(x+f*13, gy-24, 5, 15, 0, 0, 7);
    ctx.fill(); ctx.stroke();
  }
  if(e.type==="a"){
    ctx.strokeStyle="#e8d9a8"; ctx.lineWidth=2;
    const bend = e.state==="aim" ? .5+e.t*.5 : .5;
    ctx.beginPath();
    ctx.arc(x+f*10, gy-26, 12, -Math.PI/2*bend+(f<0?Math.PI:0), Math.PI/2*bend+(f<0?Math.PI:0));
    ctx.stroke();
  }
  ctx.restore();
  if(e.state==="detect"||e.state==="aim"){
    ctx.fillStyle="#ffc46b"; ctx.font="bold 15px Georgia"; ctx.textAlign="center";
    ctx.fillText(e.state==="detect"?"?":"!", x, gy-52*sc);
  } else if(e.state==="chase"){
    ctx.fillStyle="#ff5b5b"; ctx.font="bold 15px Georgia"; ctx.textAlign="center";
    ctx.fillText("!", x, gy-52*sc);
  }
}
function drawCrow(e){
  const flap=Math.sin(state.t*(e.state==="warn"?26:10)+e.sx)*(e.state==="dive"?.2:1);
  const body=e.flash>0?"#ffffff":"#6a4fd0";
  const wing=e.flash>0?"#ffffff":"#b9a8ff";
  const g=ctx.createRadialGradient(e.x,e.y,2,e.x,e.y,26);
  g.addColorStop(0,"rgba(170,140,255,.3)"); g.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=g; ctx.beginPath(); ctx.arc(e.x,e.y,26,0,7); ctx.fill();
  ctx.fillStyle=body;
  ctx.beginPath(); ctx.ellipse(e.x,e.y,9,6,0,0,7); ctx.fill();
  ctx.strokeStyle=wing; ctx.lineWidth=3; ctx.lineCap="round";
  ctx.beginPath();
  ctx.moveTo(e.x-3,e.y-2); ctx.quadraticCurveTo(e.x-14,e.y-10*flap-4,e.x-22,e.y-2*flap);
  ctx.moveTo(e.x+3,e.y-2); ctx.quadraticCurveTo(e.x+14,e.y-10*flap-4,e.x+22,e.y-2*flap);
  ctx.stroke();
  ctx.fillStyle=(e.state==="warn"||e.state==="dive")?"#ff4040":"#ffffff";
  ctx.beginPath(); ctx.arc(e.x+4,e.y-2,1.8,0,7); ctx.fill();
  if(e.state==="warn"){
    ctx.strokeStyle="rgba(255,90,90,"+(1-e.t)+")"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.arc(e.x,e.y,10+e.t*26,0,7); ctx.stroke();
  }
}
function drawBoss(){
  const b=state.boss, gy=state.lvl.arena.gy, x=b.x, f=b.dir;
  ctx.globalAlpha=b.fade;
  const g=ctx.createRadialGradient(x,gy-44,4,x,gy-44,60);
  g.addColorStop(0,"rgba(255,110,160,.28)"); g.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=g; ctx.beginPath(); ctx.arc(x,gy-44,60,0,7); ctx.fill();
  const body=b.flash>0?"#ffffff":"#3a1024";
  ctx.fillStyle=body;
  // capa amplia
  ctx.beginPath();
  ctx.moveTo(x,gy-70);
  ctx.quadraticCurveTo(x-26,gy-40,x-20,gy);
  ctx.lineTo(x+20,gy);
  ctx.quadraticCurveTo(x+26,gy-40,x,gy-70);
  ctx.fill();
  // cabeza con capucha puntiaguda
  ctx.beginPath();
  ctx.moveTo(x-10,gy-62); ctx.quadraticCurveTo(x,gy-92,x+10,gy-62); ctx.fill();
  // ribete
  ctx.strokeStyle="#ff6b93"; ctx.lineWidth=1.6;
  ctx.beginPath();
  ctx.moveTo(x-10,gy-62); ctx.quadraticCurveTo(x,gy-92,x+10,gy-62); ctx.stroke();
  // ojos gemelos
  ctx.fillStyle="#ff4d6d";
  ctx.beginPath(); ctx.arc(x+f*3-2,gy-66,2.2,0,7); ctx.fill();
  ctx.beginPath(); ctx.arc(x+f*3+3,gy-66,2.2,0,7); ctx.fill();
  // espada al atacar
  if(b.state==="slash"){
    ctx.save();
    ctx.translate(x+f*14,gy-40);
    ctx.rotate(f*(-1.6+b.t*4));
    ctx.strokeStyle="#ffd9e2"; ctx.lineWidth=3.5; ctx.lineCap="round";
    ctx.beginPath(); ctx.moveTo(0,0); ctx.lineTo(0,-46); ctx.stroke();
    ctx.restore();
  }
  ctx.globalAlpha=1;
}
function drawBossBar(){
  const b=state.boss;
  const bw=Math.min(W*.6,420), bx=(W-bw)/2, by=14;
  ctx.fillStyle="rgba(3,4,10,.7)";
  ctx.fillRect(bx-4,by-4,bw+8,20);
  ctx.strokeStyle="#ff6b93"; ctx.strokeRect(bx-4,by-4,bw+8,20);
  ctx.fillStyle="#ff4d6d";
  ctx.fillRect(bx,by,bw*(b.hp/b.maxHp),12);
  ctx.fillStyle="#ffd9e2"; ctx.font="10px Georgia"; ctx.textAlign="center";
  ctx.fillText("EL CAZADOR DE UMBRA — FASE "+bossPhase(), W/2, by+24);
}
function drawShot(s,z){
  if(s.type==="dg"){
    ctx.save(); ctx.translate(s.x,s.y); ctx.rotate(state.t*18*sign(s.vx));
    ctx.fillStyle="#f5f2e8";
    ctx.beginPath(); ctx.moveTo(0,-7); ctx.lineTo(2.4,0); ctx.lineTo(0,7); ctx.lineTo(-2.4,0); ctx.fill();
    ctx.restore();
  } else if(s.type==="ob"){
    const g=ctx.createRadialGradient(s.x,s.y,2,s.x,s.y,16);
    g.addColorStop(0,"#ff8fb0"); g.addColorStop(1,"rgba(255,80,140,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(s.x,s.y,16,0,7); ctx.fill();
    ctx.fillStyle="#ffdce6"; ctx.beginPath(); ctx.arc(s.x,s.y,6,0,7); ctx.fill();
  } else {
    ctx.strokeStyle="#ffc46b"; ctx.lineWidth=2.5; ctx.lineCap="round";
    ctx.beginPath(); ctx.moveTo(s.x-9*sign(s.vx),s.y); ctx.lineTo(s.x+7*sign(s.vx),s.y); ctx.stroke();
  }
}
function drawPlayer(z){
  const x=state.px, y=state.py, f=state.face;
  if(state.shadow){
    const g=ctx.createRadialGradient(x,y-8,2,x,y-8,26);
    g.addColorStop(0,"rgba(120,90,220,.85)"); g.addColorStop(1,"rgba(60,40,140,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(x,y-8,26,0,7); ctx.fill();
    ctx.fillStyle="#1a1030";
    ctx.beginPath(); ctx.ellipse(x,y-4,7,16,0,0,7); ctx.fill();
    ctx.fillStyle="#b9a8ff";
    ctx.beginPath(); ctx.arc(x+f*3,y-14,1.8,0,7); ctx.fill();
    return;
  }
  ctx.strokeStyle="#f2efe6"; ctx.lineCap="round";
  ctx.beginPath();
  for(let i=0;i<state.scarf.length;i++){
    const s=state.scarf[i];
    ctx.lineWidth=Math.max(1.5,11-i*.9);
    if(i===0) ctx.moveTo(s.x,s.y); else ctx.lineTo(s.x,s.y);
  }
  ctx.stroke();
  if(state.onGround){
    ctx.fillStyle="rgba(0,0,0,.35)";
    ctx.beginPath(); ctx.ellipse(x,y+PH/2+2,12,4,0,0,7); ctx.fill();
  }
  const run=state.onGround&&state.vx!==0;
  const ph=Math.sin(state.animT*14);
  const halo=ctx.createRadialGradient(x,y-8,4,x,y-8,34);
  halo.addColorStop(0,"rgba(255,255,255,.18)"); halo.addColorStop(1,"rgba(0,0,0,0)");
  ctx.fillStyle=halo; ctx.beginPath(); ctx.arc(x,y-8,34,0,7); ctx.fill();
  ctx.save();
  if(state.crouch){ ctx.translate(x,y+PH/2); ctx.scale(1,.68); ctx.translate(-x,-(y+PH/2)); }
  ctx.fillStyle="#f7f4ea";
  ctx.save(); ctx.translate(x,y+6);
  const la=run?ph*.6:(state.onGround?0:.5);
  ctx.fillRect(-5+Math.sin(la)*5, 4, 3.5, 13);
  ctx.fillRect( 2-Math.sin(la)*5, 4, 3.5, 13);
  ctx.restore();
  ctx.beginPath(); ctx.ellipse(x,y-2,6,14,0,0,7); ctx.fill();
  ctx.beginPath(); ctx.arc(x+f*1.5,y-17,6,0,7); ctx.fill();
  ctx.save();
  ctx.translate(x+f*1.5,y-21); ctx.rotate(f*-.12);
  ctx.fillStyle="#f7f4ea";
  ctx.beginPath(); ctx.ellipse(0,0,13,2.6,0,0,7); ctx.fill();
  ctx.fillRect(-5,-6,10,6);
  ctx.beginPath(); ctx.ellipse(0,-6,5,1.8,0,0,7); ctx.fill();
  ctx.fillStyle="#141628"; ctx.fillRect(-5,-2.3,10,2);
  ctx.restore();
  ctx.fillStyle="#141628";
  ctx.beginPath(); ctx.arc(x+f*4.5,y-17,1.9,0,7); ctx.fill();
  ctx.restore();
}

/* ---------- Tienda ---------- */
const SHOP=[
  {id:"heart", name:"+1 CORAZÓN", desc:"Vida máxima permanente (hasta 5)", cost:12,
   can:()=>state.up.maxHearts<5, buy:()=>{state.up.maxHearts++; state.hearts++;}},
  {id:"dbl", name:"DOBLE SALTO", desc:"Un segundo salto en el aire", cost:10,
   can:()=>!state.up.dbl, buy:()=>{state.up.dbl=true;}},
  {id:"dash", name:"DASH AÉREO", desc:"Pulsa ▼ en el aire: impulso relámpago", cost:10,
   can:()=>!state.up.dash, buy:()=>{state.up.dash=true;}},
  {id:"dag", name:"BANDOLERA", desc:"+2 dagas de capacidad máxima", cost:8,
   can:()=>state.up.dagCap<10, buy:()=>{state.up.dagCap+=2;}},
  {id:"smk", name:"MÁS HUMO", desc:"+1 bomba de humo por zona", cost:8,
   can:()=>state.up.smokeMax<4, buy:()=>{state.up.smokeMax++; state.smoke++;}},
  {id:"hook", name:"CUERDA LARGA", desc:"+60 de alcance del gancho", cost:6,
   can:()=>state.up.hookLen<430, buy:()=>{state.up.hookLen+=60;}},
];
function renderShop(){
  const box=document.getElementById("nc_shopItems");
  box.innerHTML="";
  SHOP.forEach(it=>{
    const d=document.createElement("div");
    const ok=it.can(), afford=state.bank>=it.cost;
    d.className="shopIt"+((ok&&afford)?"":" off");
    d.innerHTML=`<b>${it.name}</b><span>${ok?it.desc:"YA LO TIENES"}</span><span class="cost">☾ ${it.cost}</span>`;
    d.onclick=()=>{
      if(!it.can()||state.bank<it.cost) return;
      state.bank-=it.cost; it.buy(); sBuy();
      saveRun(); updateHUD(); renderShop();
    };
    box.appendChild(d);
  });
  document.getElementById("nc_bankLine").textContent=`Lunas disponibles: ☾ ${state.bank}`;
}
function showInter(title,msg,btnTxt,cb,shop){
  document.getElementById("nc_interTitle").textContent=title;
  document.getElementById("nc_interMsg").textContent=msg;
  document.getElementById("nc_btnNext").textContent=btnTxt;
  document.getElementById("nc_shopItems").style.display=shop?"grid":"none";
  document.getElementById("nc_bankLine").style.display=shop?"block":"none";
  if(shop) renderShop();
  document.getElementById("nc_inter").classList.add("on");
  document.getElementById("nc_btnNext").onclick=()=>{
    document.getElementById("nc_inter").classList.remove("on");
    cb();
  };
}

/* ---------- Flujo ---------- */
function finishZone(){
  state.running=false; sWin();
  if(state.zone>=ZONES.length-1){
    showInter("LA TORRE DEL CAZADOR",
      "Has cruzado todo Azhar. Arriba te espera el Cazador de Umbra. Tus dagas brillarán sin límite: esta noche termina aquí.",
      "ENTRAR", ()=>{ loadBoss(); state.running=true; }, true);
  } else {
    showInter(ZONES[state.zone+1].name,
      `${state.pal.name} queda atrás. ${ZONES[state.zone+1].sub} — Tienda del contrabandista:`,
      "CONTINUAR", ()=>{ loadZone(state.zone+1); state.running=true; }, true);
  }
}
function endEndless(){
  state.running=false;
  const m=Math.floor(state.dist);
  if(m>rec.endless){ rec.endless=m; saveRec(); }
  sDie();
  showInter("FIN DE LA CARRERA",
    `Has recorrido ${m} m bajo la noche eterna. Récord: ${rec.endless} m · Lunas: ${state.bank}`,
    "VOLVER AL MENÚ", ()=>toMenu(), false);
}
function toMenu(){
  state.running=false; state.lvl=null; state.boss=null;
  refreshMenu();
  document.getElementById("nc_menu").classList.add("on");
}
function refreshMenu(){
  const sv=lsGet("noctis_save");
  document.getElementById("nc_btnCont").style.display = sv? "inline-block":"none";
  document.getElementById("nc_recLine").textContent =
    `Cazadores derrotados: ${rec.boss} · Récord sin fin: ${rec.endless} m`;
}
document.getElementById("nc_btnPlay").onclick=()=>{
  document.getElementById("nc_menu").classList.remove("on");
  beep(520,.1,"triangle",.1);
  state.bank=0; state.kills=0; state.deaths=0;
  state.up={dbl:false,dash:false,maxHearts:3,dagCap:6,smokeMax:2,hookLen:310};
  state.daggers=3;
  loadZone(0); state.running=true;
};
document.getElementById("nc_btnCont").onclick=()=>{
  const sv=lsGet("noctis_save");
  if(!sv) return refreshMenu();
  document.getElementById("nc_menu").classList.remove("on");
  beep(520,.1,"triangle",.1);
  state.bank=sv.bank||0; state.up=Object.assign(state.up,sv.up||{});
  state.daggers=sv.daggers||3; state.kills=sv.kills||0; state.deaths=sv.deaths||0;
  loadZone(Math.min(sv.zone||0,ZONES.length-1)); state.running=true;
};
document.getElementById("nc_btnEndless").onclick=()=>{
  document.getElementById("nc_menu").classList.remove("on");
  beep(520,.1,"triangle",.1);
  loadEndless(); state.running=true;
};

/* ---------- Bucle ---------- */
let last=0;
function loop(ts){
  if(!__active) return;
  requestAnimationFrame(loop);
  const dt=Math.min(.033,(ts-last)/1000)||0; last=ts;
  if(state.running) step(dt);
  if(state.lvl) draw();
  else drawMenuBG(ts/1000);
}
function drawMenuBG(t){
  if(!bgSky) return;
  ctx.clearRect(0,0,W,H);
  ctx.drawImage(bgSky,0,0);
  if(bgFar){ const off=-(t*12)%bgFar.width;
    ctx.drawImage(bgFar,off,0); ctx.drawImage(bgFar,off+bgFar.width,0); }
  if(bgMid){ const off=-(t*26)%bgMid.width;
    ctx.drawImage(bgMid,off,0); ctx.drawImage(bgMid,off+bgMid.width,0); }
}
refreshMenu();
__exp.start=function(){ if(!__exp._i){ __exp._i=true; resize(); } __active=true; requestAnimationFrame(loop); };
__exp.stop=function(){ __active=false; };

return __exp;
})();

/* ===== AHORCADO ===== */

const GameHM=(function(){
const __exp={};
const BANK={
 "ANIMALES":["ELEFANTE","JIRAFA","DELFÍN","MURCIÉLAGO","CANGURO","BÚHO","TIBURÓN","ARDILLA","CAMALEÓN","PINGÜINO"],
 "PAÍSES":["MÉXICO","ARGENTINA","JAPÓN","ALEMANIA","MARRUECOS","CANADÁ","PORTUGAL","TAILANDIA","EGIPTO","AUSTRALIA"],
 "CIUDADES":["SEVILLA","PARÍS","LONDRES","ESTAMBUL","BARCELONA","ROMA","LISBOA","PRAGA","MOSCÚ","NUEVA YORK"],
 "COMIDA":["PAELLA","CROQUETA","GAZPACHO","TORTILLA","EMPANADA","CHURROS","LENTEJAS","SALMOREJO","ALBÓNDIGA","GUACAMOLE"],
 "CIENCIA":["MERCURIO","GRAVEDAD","MOLÉCULA","GALAXIA","NEURONA","VOLCÁN","OXÍGENO","ECLIPSE","BACTERIA","PÉNDULO"],
 "DEPORTES":["BALONCESTO","NATACIÓN","CICLISMO","ATLETISMO","ESGRIMA","BALONMANO","SENDERISMO","PIRAGÜISMO","AJEDREZ","VOLEIBOL"],
 "NATURALEZA":["CASCADA","TORMENTA","ACANTILADO","DESIERTO","GLACIAR","PRADERA","RELÁMPAGO","MANANTIAL","ARRECIFE","AMANECER"],
 "OBJETOS":["PARAGUAS","LINTERNA","BRÚJULA","TIJERAS","CANDADO","MOCHILA","ESPEJO","MARTILLO","TELESCOPIO","ABANICO"],
};
const KEYS="ABCDEFGHIJKLMNÑOPQRSTUVWXYZ".split("");
const ACC={"Á":"A","É":"E","Í":"I","Ó":"O","Ú":"U","Ü":"U"};
const norm=ch=>ACC[ch]||ch;
const $=id=>document.getElementById(id);
const REC_KEYS={clasico:"hm_best",crono:"hm_best_crono",vidas:"hm_best_vidas"};
function rec(m){ return parseInt(localStorage.getItem(REC_KEYS[m])||"0",10)||0; }
function setRec(m,v){ try{ localStorage.setItem(REC_KEYS[m],String(v)); }catch(e){} }

let mode=null, word="", cat="", revealed=null, errors=0, wordOver=false, runOver=false;
let hinted=false, lastWord="", streak=0, wordsRun=0, lives=3, time=75;
const tried=new Set();

function startMode(m){
  mode=m; runOver=false; streak=0; wordsRun=0; lives=3; time=75;
  $("hm_menu").style.display="none"; $("hm_play").style.display="block";
  $("hm_new").textContent = mode==="crono" ? "PASAR (−5 s)" : "NUEVA PALABRA";
  newWord();
}
function backToModes(){
  runOver=true; // detiene el reloj
  $("hm_play").style.display="none"; $("hm_menu").style.display="block";
}
function newWord(){
  const cats=Object.keys(BANK);
  do{
    cat=cats[Math.floor(Math.random()*cats.length)];
    word=BANK[cat][Math.floor(Math.random()*BANK[cat].length)];
  }while(word===lastWord);
  lastWord=word;
  revealed=word.split("").map(ch=>!/[A-ZÁÉÍÓÚÜÑ]/.test(ch));
  errors=0; wordOver=false; hinted=false;
  tried.clear();
  $("hm_msg").textContent=""; $("hm_hint").disabled=false;
  render();
}
function info(){
  if(mode==="clasico") return `RACHA <b>${streak}</b> · RÉCORD ${rec(mode)}`;
  if(mode==="crono")   return `⏱ <b>${Math.max(0,Math.ceil(time))} s</b> · ${wordsRun} · RÉCORD ${rec(mode)}`;
  return `${"♥".repeat(lives)}${"♡".repeat(Math.max(0,3-lives))} · <b>${wordsRun}</b> · RÉCORD ${rec(mode)}`;
}
function render(){
  $("hm_cat").textContent="CATEGORÍA: "+cat;
  $("hm_info").innerHTML=info();
  $("hm_word").textContent=word.split("").map((ch,i)=>
    revealed[i]?ch:(/[A-ZÁÉÍÓÚÜÑ]/.test(ch)?"_":ch)).join("");
  for(let i=0;i<6;i++) $("hm_p"+i).classList.toggle("on", i<errors);
  const kb=$("hm_kb");
  if(!kb.children.length){
    KEYS.forEach(k=>{
      const b=document.createElement("button");
      b.textContent=k; b.dataset.k=k;
      b.onclick=()=>guess(k);
      kb.appendChild(b);
    });
  }
  kb.querySelectorAll("button").forEach(b=>{
    if(!tried.has(b.dataset.k)){ b.disabled=wordOver||runOver; if(!wordOver&&!runOver) b.className=""; }
  });
}
function guess(k){
  if(wordOver||runOver||tried.has(k)) return;
  tried.add(k);
  const btn=[...$("hm_kb").children].find(b=>b.dataset.k===k);
  let hit=false;
  word.split("").forEach((ch,i)=>{ if(norm(ch)===k){ revealed[i]=true; hit=true; } });
  if(hit){ btn.classList.add("hm-ok"); ArcadeSnd(720,.08,"sine",.08); }
  else{
    errors++; btn.classList.add("hm-bad"); ArcadeSnd(200,.2,"sawtooth",.1,90);
    if(mode==="crono") time-=4;
  }
  btn.disabled=true;
  checkWord(); render();
  if(mode==="crono" && time<=0 && !runOver) endRun("¡Se acabó el tiempo!");
}
function checkWord(){
  if(revealed.every(Boolean)){
    wordOver=true; wordsRun++;
    if(mode==="clasico"){
      streak++;
      if(streak>rec(mode)) setRec(mode,streak);
      $("hm_msg").textContent="¡Correcto! "+word;
    } else if(mode==="crono"){
      time+=20;
      $("hm_msg").textContent="¡Correcto! +20 s";
    } else {
      if(wordsRun%3===0 && lives<3){ lives++; $("hm_msg").textContent="¡Correcto! Recuperas una vida ♥"; }
      else $("hm_msg").textContent="¡Correcto! "+word;
    }
    ArcadeSnd(523,.15,"triangle",.1); setTimeout(()=>ArcadeSnd(784,.25,"triangle",.1),140);
    if(mode!=="clasico") setTimeout(()=>{ if(!runOver) newWord(); },1000);
  } else if(errors>=6){
    wordOver=true;
    revealed=revealed.map(()=>true);
    ArcadeSnd(160,.5,"sawtooth",.12,60);
    if(mode==="clasico"){
      streak=0;
      $("hm_msg").textContent="La palabra era: "+word;
    } else if(mode==="crono"){
      $("hm_msg").textContent="Era: "+word;
      setTimeout(()=>{ if(!runOver) newWord(); },1200);
    } else {
      lives--;
      $("hm_msg").textContent="Era: "+word+" — pierdes una vida";
      if(lives<=0) endRun("Sin vidas.");
      else setTimeout(()=>{ if(!runOver) newWord(); },1200);
    }
  }
}
function endRun(reason){
  runOver=true; wordOver=true;
  if(wordsRun>rec(mode)) setRec(mode,wordsRun);
  revealed=revealed.map(()=>true);
  $("hm_msg").textContent=`${reason} Palabras: ${wordsRun} · Récord: ${rec(mode)}`;
  $("hm_new").textContent="VOLVER A JUGAR";
  ArcadeSnd(160,.6,"sawtooth",.12,60);
  render();
}
function hint(){
  if(wordOver||runOver||hinted) return;
  const opts=word.split("").map((ch,i)=>(!revealed[i]&&/[A-ZÁÉÍÓÚÜÑ]/.test(ch))?i:-1).filter(i=>i>=0);
  if(!opts.length) return;
  hinted=true; $("hm_hint").disabled=true;
  guess(norm(word[opts[Math.floor(Math.random()*opts.length)]]));
}
let bound=false, tickId=null;
__exp.start=function(){
  if(!bound){
    bound=true;
    document.querySelectorAll("#hm_menu [data-m]").forEach(b=>{
      b.onclick=()=>{ ArcadeSnd(600,.07,"square",.06); startMode(b.dataset.m); };
    });
    $("hm_exit").onclick=backToModes;
    $("hm_new").onclick=()=>{
      if(runOver){ startMode(mode); return; }
      if(mode==="crono"){ time-=5; if(time<=0) return endRun("¡Se acabó el tiempo!"); }
      newWord();
    };
    $("hm_hint").onclick=hint;
    window.addEventListener("keydown",e=>{
      if(Arcade.current!=="hm") return;
      const k=e.key.toUpperCase();
      if(KEYS.includes(k)) guess(k);
    });
    tickId=setInterval(()=>{
      if(Arcade.current!=="hm" || mode!=="crono" || runOver || $("hm_play").style.display==="none") return;
      time-=1;
      $("hm_info").innerHTML=info();
      if(time<=10 && time>0) ArcadeSnd(880,.05,"square",.04);
      if(time<=0) endRun("¡Se acabó el tiempo!");
    },1000);
  }
  // al volver al arcade siempre mostramos el menú de modos
  backToModes(); 
  $("hm_menu").style.display="block";
};
return __exp;
})();

/* ===== CUATRO EN RAYA ===== */

const GameC4=(function(){
const __exp={};

const C4R=6, C4C=7;
function c4New(){ return Array.from({length:C4R},()=>Array(C4C).fill(0)); }
function c4Drop(b,c){ for(let r=C4R-1;r>=0;r--) if(b[r][c]===0) return r; return -1; }
function c4Win(b){
  const dirs=[[0,1],[1,0],[1,1],[1,-1]];
  for(let r=0;r<C4R;r++)for(let c=0;c<C4C;c++){
    const v=b[r][c]; if(!v) continue;
    for(const [dr,dc] of dirs){
      const cells=[[r,c]];
      for(let k=1;k<4;k++){
        const rr=r+dr*k, cc=c+dc*k;
        if(rr<0||rr>=C4R||cc<0||cc>=C4C||b[rr][cc]!==v) break;
        cells.push([rr,cc]);
      }
      if(cells.length===4) return {p:v, cells};
    }
  }
  return null;
}
function c4Full(b){ return b[0].every(v=>v!==0); }
function c4Valid(b){ const v=[]; for(let c=0;c<C4C;c++) if(b[0][c]===0) v.push(c); return v; }
function c4Eval(b,me){
  const opp=3-me; let s=0;
  for(let r=0;r<C4R;r++) if(b[r][3]===me) s+=4;
  const win4=(a)=>{
    const m=a.filter(v=>v===me).length, o=a.filter(v=>v===opp).length;
    if(m>0&&o>0) return 0;
    if(m===4) return 100000; if(o===4) return -100000;
    if(m===3) return 60; if(o===3) return -70;
    if(m===2) return 8;  if(o===2) return -8;
    return 0;
  };
  for(let r=0;r<C4R;r++)for(let c=0;c<C4C;c++){
    if(c+3<C4C) s+=win4([b[r][c],b[r][c+1],b[r][c+2],b[r][c+3]]);
    if(r+3<C4R) s+=win4([b[r][c],b[r+1][c],b[r+2][c],b[r+3][c]]);
    if(r+3<C4R&&c+3<C4C) s+=win4([b[r][c],b[r+1][c+1],b[r+2][c+2],b[r+3][c+3]]);
    if(r+3<C4R&&c-3>=0)  s+=win4([b[r][c],b[r+1][c-1],b[r+2][c-2],b[r+3][c-3]]);
  }
  return s;
}
const C4ORDER=[3,2,4,1,5,0,6];
function c4Minimax(b,depth,alpha,beta,turn,me){
  const w=c4Win(b);
  if(w) return {score: w.p===me? 1000000+depth : -1000000-depth};
  if(c4Full(b)) return {score:0};
  if(depth===0) return {score:c4Eval(b,me)};
  let bestCol=-1;
  if(turn===me){
    let best=-Infinity;
    for(const c of C4ORDER){
      const r=c4Drop(b,c); if(r<0) continue;
      b[r][c]=turn;
      const sc=c4Minimax(b,depth-1,alpha,beta,3-turn,me).score;
      b[r][c]=0;
      if(sc>best){ best=sc; bestCol=c; }
      alpha=Math.max(alpha,best);
      if(alpha>=beta) break;
    }
    return {score:best,col:bestCol};
  } else {
    let best=Infinity;
    for(const c of C4ORDER){
      const r=c4Drop(b,c); if(r<0) continue;
      b[r][c]=turn;
      const sc=c4Minimax(b,depth-1,alpha,beta,3-turn,me).score;
      b[r][c]=0;
      if(sc<best){ best=sc; bestCol=c; }
      beta=Math.min(beta,best);
      if(alpha>=beta) break;
    }
    return {score:best,col:bestCol};
  }
}
function c4WinningCol(b,p){
  for(const c of c4Valid(b)){
    const r=c4Drop(b,c); b[r][c]=p;
    const w=c4Win(b); b[r][c]=0;
    if(w) return c;
  }
  return -1;
}
function c4AiMove(b,diff,me){
  const opp=3-me;
  let c=c4WinningCol(b,me); if(c>=0) return c;      // 1. ganar
  c=c4WinningCol(b,opp); if(c>=0) return c;          // 2. bloquear
  const valid=c4Valid(b);
  if(diff==="facil") return valid[Math.floor(Math.random()*valid.length)];
  // evitar regalar victoria al rival justo encima
  let safe=valid.filter(col=>{
    const r=c4Drop(b,col); b[r][col]=me;
    const bad=c4WinningCol(b,opp)>=0; b[r][col]=0;
    return !bad;
  });
  if(!safe.length) safe=valid;
  if(diff==="normal"){
    safe.sort((a,b2)=>Math.abs(a-3)-Math.abs(b2-3));
    return safe[Math.random()<.7?0:Math.floor(Math.random()*safe.length)];
  }
  // difícil: minimax
  const res=c4Minimax(b,7,-Infinity,Infinity,me,me);
  if(res.col>=0 && safe.includes(res.col)) return res.col;
  if(res.col>=0) return res.col;
  return safe[0];
}

let B=null, mode=null, turn=1, over=false, busy=false, aiSide=2;
const $=id=>document.getElementById(id);
function scores(){ 
  try{ return JSON.parse(localStorage.getItem("c4_scores"))||{}; }catch(e){ return {}; }
}
function addScore(key){
  const s=scores(); s[key]=(s[key]||0)+1;
  try{ localStorage.setItem("c4_scores",JSON.stringify(s)); }catch(e){}
}
function scoreLine(){
  const s=scores();
  if(mode==="2p") return `Jugador 1: ${s.p1_2p||0} · Jugador 2: ${s.p2_2p||0} · Empates: ${s.draw_2p||0}`;
  return `Tú: ${s["win_"+mode]||0} · IA: ${s["lose_"+mode]||0} · Empates: ${s["draw_"+mode]||0}`;
}
function startGame(m){
  mode=m; B=c4New(); over=false; busy=false; turn=1;
  $("c4_menu").style.display="none"; $("c4_play").style.display="block";
  renderBoard(); updateStatus(); $("c4_score").textContent=scoreLine();
}
function renderBoard(){
  const bd=$("c4_board"); bd.innerHTML="";
  for(let r=0;r<C4R;r++)for(let c=0;c<C4C;c++){
    const cell=document.createElement("div");
    cell.className="c4-cell"; cell.dataset.c=c;
    if(B[r][c]){
      const d=document.createElement("div");
      d.className="c4-disc c4-p"+B[r][c];
      cell.appendChild(d);
    }
    cell.onclick=()=>colTap(c);
    bd.appendChild(cell);
  }
}
function cellEl(r,c){ return $("c4_board").children[r*C4C+c]; }
function updateStatus(msg){
  const st=$("c4_status");
  if(msg){ st.innerHTML=msg; return; }
  const who = mode==="2p"
    ? (turn===1?"JUGADOR 1":"JUGADOR 2")
    : (turn===aiSide?"LA IA PIENSA…":"TU TURNO");
  st.innerHTML=`<span class="c4-turn c4-p${turn}"></span> ${who}`;
}
function colTap(c){
  if(over||busy) return;
  if(mode!=="2p" && turn===aiSide) return;
  if(!place(c)) return;
  afterMove();
}
function place(c){
  const r=c4Drop(B,c); if(r<0) return false;
  B[r][c]=turn;
  const cell=cellEl(r,c);
  const d=document.createElement("div");
  d.className="c4-disc c4-p"+turn;
  const ch=cell.offsetHeight||54;
  d.style.setProperty("--d", (-(r+1)*(ch+6))+"px");
  cell.appendChild(d);
  ArcadeSnd(300+r*30,.1,"sine",.09,180);
  return true;
}
function afterMove(){
  const w=c4Win(B);
  if(w) return finish(w);
  if(c4Full(B)) return finish(null);
  turn=3-turn; updateStatus();
  if(mode!=="2p" && turn===aiSide){
    busy=true;
    setTimeout(()=>{
      const col=c4AiMove(B,mode,aiSide);
      place(col); busy=false; afterMove();
    }, 420);
  }
}
function finish(w){
  over=true;
  if(w){
    w.cells.forEach(([r,c])=>{
      const disc=cellEl(r,c).querySelector(".c4-disc");
      if(disc) disc.classList.add("c4-winner");
    });
    if(mode==="2p"){
      addScore(w.p===1?"p1_2p":"p2_2p");
      updateStatus(`<span class="c4-turn c4-p${w.p}"></span> ¡VICTORIA DEL JUGADOR ${w.p}!`);
      ArcadeSnd(523,.2,"triangle",.12); setTimeout(()=>ArcadeSnd(784,.3,"triangle",.12),160);
    } else if(w.p===aiSide){
      addScore("lose_"+mode); updateStatus("DERROTA — la IA conecta cuatro.");
      ArcadeSnd(180,.6,"sawtooth",.12,60);
    } else {
      addScore("win_"+mode); updateStatus("¡VICTORIA! Cuatro en raya.");
      ArcadeSnd(523,.2,"triangle",.12); setTimeout(()=>ArcadeSnd(784,.3,"triangle",.12),160);
    }
  } else {
    addScore(mode==="2p"?"draw_2p":"draw_"+mode);
    updateStatus("EMPATE — tablero completo.");
  }
  $("c4_score").textContent=scoreLine();
}
let bound=false;
__exp.start=function(){
  if(!bound){
    bound=true;
    document.querySelectorAll("#c4_menu [data-mode]").forEach(b=>{
      b.onclick=()=>{ aiSide=2; startGame(b.dataset.mode); };
    });
    $("c4_restart").onclick=()=>startGame(mode);
    $("c4_back").onclick=()=>{ $("c4_play").style.display="none"; $("c4_menu").style.display="block"; };
  }
};
return __exp;
})();

/* ===== VÉRTIGO ===== */
const GameVT=(function(){
const __exp={};
let __active=false;

"use strict";
const SPR_DATA={"h_idle": "data:image/png;base64,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", "h_w0": "data:image/png;base64,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", "h_w1": "data:image/png;base64,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", "h_w2": "data:image/png;base64,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", "h_w3": "data:image/png;base64,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", "h_jump": "data:image/png;base64,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", "h_fall": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAACACAMAAADDApyIAAAABGdBTUEAALGPC/xhBQAAAwBQTFRFxINhzayN266HyKWGq21P2JdigLuLQ7x8X6iA5sWmAAAAy6uLw4Jj455n9NGwxoVQ4Z9nxqeHvIJN0pNh3ZtnN6tu1baa1pRcpnVd+PDt7syr+Pj46+vrMJphOaNs3L2e9vb227uapXJY1Ipm27yeQLB1t3tiMZti6MentHph68mqyqiK17mc04ll7fPv24xm9/b2OKJr06V58c2s9NCv0bGV2ZRns3lY1bWY0bOXw4ZQR6VvPK1zv35g9dKx0Yxmv4Bh7M600otktXta0bCTq3NY+NOwrnde4sOk6My0sndZ0LGU1pFipXBWpnNa0Ihk1phyt3pc58ep5s2x7c6upXBYtHpc4cCh149n25Bmq3Vbu4FjqXVdzqWBAAAAr4RmzH9SdXBKy8yhUYJRV7OEm5tz2a2YncGPibyIsdDAZope3LeTwp998uTe7NXIgHlSio1klcqu1Zx2OIhUfZFmdLeUv31bvMCUhbB/4L+q/unX4q2K1516tHRGxMSZQ7J04s6/0JV0kIFacJFiyYZNz5qBTJNg2N7b6cmp/dy9SKVtK5VcxoVj0K6NzYJeK5th1JFbxIBGwIFL78CZ4eDgxYBe+Myl5+fmyYNG14Zg1JVf/+LH88ag0oxPpnNZ15Rb36iD57SQtHhb7LyWuZl4pWxQsJBxWqRs8s+u4Zpf//XqtHVX58Wk8vHw7ezsHYRO0oZg4Jxj2qh+H49UyX1Z4bGEWqhv2rmbuXtdJKBfz5Bu6LeH1LWYyYxqyqeI0IBavnxDIptbrnRY1ZFXwnxWMKJmIJJW1oJbNapt////HopRomtSqmxPpW9VrHFV9fX1u3ZWIpZZundY6sShN65wOLFxoWZKt3RU17WWp2pNxX9CoGhN3bqZ2pRYNKVq78mm7Mek99CsuHRU8cyp+NOw37yc9M6qpGhMrm5Q2riY4r6dPLx535da+tKs/NSu24hgObV01LOU5sGf24tltnNTsXBS45pb24Vds3JTO7p3vHdWvnhXunVV/taw/9exv3lYTu7tHgAAAF90Uk5TWfe6+P3639+v7wdP3+/f38/f79/fT8/Pr4/fTx+nb6/Pz6+vv9Bf5Z+fv+/fz2TP7yN7z++fj6/vv7+MwL9fTz+P789kl79PTz/vjb/v330vf38vb79vH59fLx9fDwDvSTqxAAALf0lEQVRo3u2ad1xT5xrH+9fde/be2972dtm97NCrdS8ciELZ4fPp7R6u1i11l41oEVzI5hpZDUgapAmrhp1gAhEUBEIgAkqkKNcQMu7zvO/JSUDQnND8xy+MJJLf932e5z3Pe857fCDIxXpgCjAFmAJMAaYAU4ApwGgFuBjgu4DnUoDvLcELrgT43johEKx2HYD4CwQergKA/4nKSoFgpYsA1L+yRCCY5xLAG9S/sqTk0OOuAPjdunkH7AtKACAI+PEB6A8Ay0UDErx/dIDfLQSUGAwXjSMAeMtJQIDfGysX3KJ6yXe1x1j/EYPBaGwylBw65AyAt/olan3z1s2bN8mzBb4edv4FIwRwW3+h4JAHZ8Dcx9Eadcf2E95a6UfyT/1HIEOdt/X6grh5HAFzXyDud8DHThTx0mocf+UFCwU0AcAQt5oTYO4LghMnTtwZTzep7pRYLBZrhoaG9JwAAb7QXughVFBwwcLoQkFBSSVlwDf6W6wZGhqSWzgA5i44dKikBMwvjIxYxqqghDAKqD+ToaEeeZa3owDeW3FxBTBwo9FgGAeAkVRW0rDYAHp65OUOF/lX4G/p1N/unAjAyi4AAPg7ClgdZ8GiOQSwlhgAyx0/0BaWyyng4v0BTIbq5PIHHQfMKweCAwC7AADApdm9WV6udwxgLTGUgEu7Dkh1HEBKXFcnf5vTgrMmNcuBIgPAlqFATgDe8tSsJuN9AGwJIEFyd46L/lOFSgTcv8bWoyyQ61lFodJojPt8q0M1HpKXuwdxByiNEp16V9RE9kVR9oCl3AGFCDCZzGn5krvdJSn9ZnN8yudRZK0pL38zyBmA0qAzmVH9acn7iorYoQenkXfNJp1Ol4aArOUB3AHL7QATyASEfGNTVlaqtxPXB28VKg0UkDAxQacrAkDqwiBnAVACc5pFsqt/QsBWo1FZ6O8sYAQBwZj3fSljvGNBCSZTwkXwX+jENdqy6RIogSHeZO5nShsXbE2VrdomUwoCnuEOeFbDlyihUaQBIGUf45d8F8BsSjYolYXenAFPh7VrJEYKwFmaQo6EeAaQbAcoQsA8rgCv7I72hihs1gSQWV29bn23pMia/pQiUDIoxWwaQYAbV8DPszs6hAzABP45EMAOuwLvzMzM3EmeJUCzUEr487kBlmVndwjzJdhMU3Sm8OrqD7A37GT9w/dZ4tZVZ5JgoJ8qg7UTECYCrM3OHsyngGSd6VR19VeY8EwWsANeFVdXn4Knwdiwd6n5GjeOgL57AE6Rl9UkhCJsqPkJWs2zzgMgRcV4pO0098fHx/ePBpAlQSjUajSenGrQ0ZCfv68TAGnQrzOr14Hh+nBd2negNAr4igBiERAlFLZr+V4cALywsPbBfGGRRJKiw26XWb13x/pwc/x3RAlmrPl6UoNdCCgSChO0/LVcpul8jUaTJhT29+sIwBx+CgvabwWc+uCrvbTGyXhu+jkA1NwAvNf4Wm1DLPG3WxAS0D9WB1WA4yCcdDwE5AuFanXXHE6twvM1vlqNAZhMpnsuOMFFEgggtqury4dbs/P5DXwG/HX3AAAc/iBWKEzr7+pawnk9mLNkiX2GkvMT7rLHJVkXmxLfDwBPZzakltgyFA8TJ2pX/Ojhg/pRE1TgngDeKwRgiyA+P4qcrNiWexOxV6O2/cTtIS6AV/45u2r2GABOmeA4ds1h/NXqsN27P4w4v6m+/tEXeQ4D/lzV1tY2+6fX/zNmmkLzTLBLENhrtR8NnAd9XA96+W9ea914DgA8X5SCBq6PA7A7m6D+2XtUZWVl50NzcnLq63fCzOta4uVzb8A/Hq2vfw8GVXV94KMPP9y2ezd//AkK+YEWt72qDQBlublICIdqo6bPmRjw4ssY7CYMe3hgQCUtUygqIt+Pjo7+9NNPGxoaRgUA499eVSVVlJW9lwvKWafRkpKr+fy/Lxsf4EXs63NCEQD+jeCvqKg4F5L+2Wfp6f8l+qw4ffv27bt3b9u27aMIqFUM/MmWY8eAwNdotFqtGh4Q2rO8sQDefAgunPjn5EjLzpcBQBXxLvhXnDtXcyA93Ur45BtQTU3NuyFS8G9TVCgUm46Bwjra2zXIgB/t7WHTeaMBXq9h9tRd4J6Tm7sF8gr+qgM9G75AwLmams0Usfkb6v/FO5c+kSIBBlDx8dGjR/cONnQQRDvYd3RkZz9tD/CcTuxhXvBzwT93EwCqVKrG/XD1uIGEAJbvp6dv/ILxf+fSpUsb0F9aATGGgn/f4GADQaB9Q8Pg4KCnDTAHmyfaazXt/GO5x46FKhRlUgDIeoAQEkNjqAkJocmpUYSA/6UWzJAUShARGrq3tbuPQVD7vr6+tSwA1hctsddidGGY0AiF4nyjKgKur3tkOFMIIjIS3WsqYqTSlmugkLYnZ0+LjIzcErpX1NraTRDAwNH39XV3P2EF4HkimQBYnI6GwTDI6BYYWKPqAO5x7G9sZBBSKWAqYnDgGy6DDjT+ImjWtJiYn81/XiSyIsgD7LtFVgCcJ9L6k+JgdDuOHv0YAG2N+4dAB1SNiIhRgHMMsa+qqvrk8uW6uv2zaeeCxuiz4nlRbytloH1rq0jEpMgnOzubKU47zV53947Qo9KYSKkKdlz0+giYTo2EAWqrooqA2vTIZ9kvUTNEvb3IIOrtFYl8KOARkrgOogaavO5/eT308LSHZ53BLZ3EAZAK52wjIxV+Jfb0DGWNunR9XdTbDA+q5l7RI3Sa8vqY8jPFAfsnFjEf2YyAjcPDwwNEKqsQuHFIn5W62B7gEd3M6ofmZtEyCnADR1r+Qevw2Y+4lwPgzPDw9evDLIXR8Jmm22Ov/V4v/oFVs3gG0yrcrOVnatMqWsE2D9wz0u9BwHXKAAj5Ba/2NMHFZeGo7s97rjiaJYhXMABPkaiXlr+b1KZXbE1Q0FLcM9o/wADshZD9TamFhaP3D35ZXMwgxGKxj7XZwfTC0lD33mZRNLvDHfDUxnL95oFhljBMw6C/NytTn3lqzPX9IiAUPzdzBvivZdv1MhEpC84AVPRzdh94cs+ZPdYIGHdWe759cpzTqVdfxQR4LvKyWw9eF4ubsSw/4M/o4hV2fz/rDOpbVmdGvZ7l6L3Mv4jZ0kCE9qeAa7Jg4w4uE4zGi/Dd1HSbqKkTTuyNSuUaRwGeM8Q2/xV3bdwRALXXoyii06hc4OHo3dhlYjEWfubvx/gzgE4jPDqJ/RBpHpSgFPya5+jtXiiDeKbbBFuPTZgQ4j9ExRCMgrzf8Ry9n7xi5qJx9za3br1gFdlgxNTgRiR553Be3huTvGH9at7ZG/+junHjxtWr34OuXr0Kz8l7Z/PyAiYNODvGnyAYwtmzeb6TA3jYAVj/pFEh8CZ3T/9PeWdZ/6Skw0RJSUlIuAFvQgh+kwP4UQAmKCnppFUUgLpPjhy4E7iSEEgAf7VhT7P6fuWPASAVTjppa/xfHzly5crx4/B18N+TA/AOnibpwArYAEEEADpyZLIAv4PHj5+mU/TwH+0BpVco4evJAXi/BQAg0P+kLdtLy+t6viy9Ao9JAvwXZh05jgM9/j0AbG1hsbwOz7u+/LK09Os3JwHwX14u19Nklx48fHIuG1ei7PK1y0R1+sXOAwKXy+Vw7ovZLoWhLrD9gyzjGqOMjFU8ZwGBifI6FBBKEWBbvx6TZbTA2TslyBY7CXgmMVGWgUmoqyP+f2BHGpAoq0UAERD8nQMEgj9kgmQai2nbPfYGQG1LC2W01MredjpFNNWUYHeSGPjgKhlFENXKljpbZBICSXXGmDso/t6PrQJGLQW4OztNA2W1AMBqZoyTBn/vxe61KFligLMHGhAw1ddaMibIc0DgYvfERHfnWwVDaKm9RyEDApdOotn5r6J5ftu5//viwHpACS4EIAHkQgAQZDKZKwFASExc40pAkL97YJBLAc7r/zqGn5iToDxMAAAAAElFTkSuQmCC", "h_duck": "data:image/png;base64,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", "h_cl0": "data:image/png;base64,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", "h_cl1": "data:image/png;base64,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", "h_rope": "data:image/png;base64,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", "h_atk": "data:image/png;base64,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", "h_hurt": "data:image/png;base64,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", "z_idle": "data:image/png;base64,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", "z_w0": "data:image/png;base64,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", "z_w1": "data:image/png;base64,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", "z_w2": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAACACAMAAADDApyIAAAABGdBTUEAALGPC/xhBQAAAwBQTFRFRquSSLKWUVZcXGB+RkdKjaN405Zl1JVhSZGjYGKvaW3AopxxRG5kRYOYOJmAUlZccm+50Zl0NJyAU1WqT1OgTlCd3Jtj1ZZjWG+l1ZRcRLuqSbCTVVpgWWyoRUhKa2y7VVheUVZc4Jxl2KRxVGCnS7qdV1qrR0lLUFRYUlleNZ6D3ZtkO56ERrmbQkRGRq6USLWYUFJaOJ+H3pxjWFmoR7GXR7SaSrqdSUpOSbmdRKeOSbqdQ0VGUVVcUVZcY2S1UlVbRaqRRaiPR0hJOY15bG/BRrebXrCTRUVIPaWLS01TSrSYTVBUR7KZTLKaREZHQ6eNUFNZRq2UR0lLSUlaQbKTT1FVAAAAPWJuiHio78cHiZ93e41t7MUHv5NftJ1opYGOeW6on7g4a7FcVqiGO4aYnnuJ8ckIQl9fzJJxhbVKsISCWXy4Qq6iYm/BQqhzgXGjQllZOXCSk7hCKXxzQmZjXa9jNad8wL8lN1VQOUZGS12kQXFqY6J9U4mxL4yJOVyLL3OBPJuEwIx1Y2a4aWm5TJSqQWCazsMeWFqyO05MPpOAP4R2Xm671JJaRaWkPZ+b1ZVfKqiIVVetQESRRbCVW162M56DO3ttOmFZIIVr15FX2ZZdQKWLUlSqR0lL4pxj/ckAamzAM5Z+JJN4Io1yRLqc4pteM7OSLKOEIYlvMKaIPaiNQqiNMq+QPLGUP6+TPkBEQbOWPqOJRKuRRLaZOqyPLquLJ5x+2ZNYGX5kQkZNTlCnOqeLRr2fOqGHKKKCM6GFSEqgQbydNq+RNaaJ4plbTVJYZmnAQkWXQ0hPPbWYSkylNqGGREaa3JVZNjg6N7KSPquQPrmaREZIPT9CJph7KKWFUFVbNaeKN62QNKSIYmW+R01TRkidPLycX2K44JdaOLCS5ZpcYWS7KZ+BSk9WObiYRElQMzQ3/8wAP0FEODk8YmW9ZWjDOraXZmnFNDY4QUNGObSVNquNZGfCY2bAOTs9KaaGPL6dO7qaRUpROjw/Oz1APb+ePD5BW57AzAAAAFh0Uk5T7aPqScN/r7+/f7/vj+9/z9835+9f749nT9cPn+8v379vz78Pmp/fb99/v0OPz9/vrx8vfLzfT4+Pb+/vz7/vP6+/n6T9g78fv9MvL09/P+8/X19/Dw8/AKfin18AAAw8SURBVGje7Zp3XBNpGsf3n+tt621vt91de3d118KKVAWBfK7fba9usXcFRRREAUHwpKwoggQICSSsEIh0CGAISWiBYCQEDZBlAkkIM+SedyYJwU2AIedfx08BgfH3fZ/nedu8Mw8w7rMemAXMAmYBs4BZwCxgFjALmAX83wL8Wp7xu5+AgGdaWt7xvo+AN1qqqqpaXrhvAM+Wqp6OnqqWtQH3CfBiVc9o7WhHT8vrQfcFsAL8zYS5EAWxZqFdZYL83gj6HwC8W3o6NARBmHs7elCe/IKCwHntmhak110HeL5T1VFImJFqOyCIKtIYqt7Tg3jergLAv6fWbFHhKCAs6ugYHYW6rHUR4Af+o1IrwIyBJykw762thcpXBbgEeAE66KjGPC5N7Sip3l7wLyys7ejxdgEQsBb5Y+YJwmqtgEIsV4NJttIGLFxoSw/0n457/FGtSUBtba6hzyDFNtEGvN7T8oc1a9a8CD0FSvlTf3OuJUNmQ18foVlNF+CXnCwZhd6IumHHqAN/s7mXypABIsA1ErqATRJMo8EKqa7i0B96KwoAgwD66AOCkjHolYQ5txASkWt2DLBlaAaADRKpGcdxNDVgUvMkAMwAKQIA3SI/h0kJAwVwKgQoxFEAUOQNNAHJGjM+DUAhTgIMBEZzHARJNIRhKgD4ExaAFPOeEYCYFFCLEQRuKcHmALqA3CkBUvRbHPkbzA4zNL0InAdgtgAMBsJxAFMC8OkB+nCp4wAmAwQkYwQ+KeBUwikLADdjjgOYtJtuxmCc7XMKOBUhHBsbCXaLP4UbCGcBTArYhElxXMdxS3DoHjxGakSh2Is7D2CKqQJGWrBiZIQVHJ+wDyuUWhOT4MYcswoAkMZcydYZ7Iu2IoCbYmRMGH7gW1hZwsccaEShgwA0koAZAPwkGiker4j4lFp7Rw84BgSjyfC5mezsgpIBkKCw+jsDhBOE49VySsBCCQmIR+bfxgcLJxhzIsI5QhIQDwDJihntTVENCEV4x4FwrlqtVkwARJBBfbozIuIA4byTTg7wSs4FgG5kTM0zImXbIw5Y8tb7bQJOmDW/pQ8IfCU/wUzgRPCI2mjcfvfu3TAjzw6w07rr2gnDgJAGz3WnC9iYn58AUwXhpog27rqLtN2YPg4Qc8IjInbu7OiNx9F8wsp/O5AeYHksWxiP1pt4dXPzHhLwiTHavgrq9PTsdDUaBnBZDjt2Li2Aeyw7p20HAoRnNzeHkYC7RqN63D56965du3Y384LRbL0vM4cV608H8HQsS6kqSNiHx5sA8D7pH2YP4BkR9S+7BelowdwraxezltIBLBVzM2UFBeVqEwJ8/QkCfGAHSDd+AD/5/vvPBYK9ALggk3HFee40AHliboFMVlCuNZl0zUDYExa2C3rq2JgJRoRpbCzauAf5f79HoOKlul2TXb7cLs7zpQ/gAcAUDQSjZSREoy+8Mei5YRRApcrQZcoQgJlFE6ACQKYWcpRuBUQr0imQGgCfk4D3KcBl2oB1LHGrFaDIpgA89ZgFYALA7jAA/P1rVUFGowoAMj4zj06R/WNZORmyggyUIoVCzQOlo5kiPZoEQQ2MzZ9v375boCrgKVVUhtbTAQTOB0KrFTAycu8sDaFA4gQCgUrVqCy4LKtgMh3W2PlI9s1ns4XKRpQhRwAFzwrI1ilbW7lMcZ4Pzblo2dL8/KamJgpgMzZlq1SqTC0Qso0koFGry8lhsfLm+9CergNfKU5LK2uyz5DpynVSFxrRZJENMqmFQiE7Nnad14wOQ3x955bZZ0h23aILlg2FyQRBbvT1DZzxacvGsjI7AARQACm6dv26BaAAQJq/K8c5yycAeFdUZKZUPCtA0ZT2dqArAJ+yMoe9iAIAoqx4mSsHUu/+0jlgBEVQVuY/8xOvd5c8krT/zJkzZ8+eVTaCym1qO0sKfvfR/pdnBPjVkiVLYmKSioqqh/tPdnY21By9cuXatQsW7Th37lxNTUNSV3dcUVHSq+/OJIKXY5LAvihGr5cXIUDNORJx7QJ8HKX8Y7q65V11QIh59eVnaQK2zGk/vL+orq40Rq7XnywlCTVHdly5giBHkH1NaVxXV7f+ZB0Q9v/uWZoRrGRlZmSoTpSWlhb198vlXUmlnQ0kAgA7jiD7mqIu8JcPx9TVnTic0e5Ba6A9taA4LUOlOgz+pXXd3YCAVEMQiHH0KHJvgPSQ/sNJdXX7BRmZFR5PTR/gPre4rClTVQABdHZ2xgFBLu8nEYiRBB8NpSfBvls/PDxcBzoMhLQF0wZ4vQ3+TdkFh5F9Z2cSWPV/qUeIOiAWddV1widERf5yBPhOkKEtK/aZJmAZ6a/Vqr5D9g1gBm7CUP0wdKeTdaVx/XGlJyEkvX54AABdFCAbxnOx17QAK4uRv1qryzx8BGWkoRMlO1R9aHjgx4EBfZxer+8GY/QNfNHHnQB9FA1rRlnxxukAliN/k0mr1ZXDTuToEQgCpfu0Vnh64McJQgDowSqVQCWAVc/UVFa83GfKjResMMgfAtDBQi6TfVda+tirx451d4eaQgcshG32gCSwV6WbTCQhrXjpFIDlaWlNpL9W16iEzVTqicceZTxx7BiEIBRuIwHbzhyi7En/6kcyVAKeyWQlpK2cFOAPa7BQq0b+OqWyrSA1dQm6Nz0OIfQfMh0iQ/hqZJstgOrq6kc9MmDnpLYQYGlwnwTglc8WCrVIyJ/Lqvd4gvz588cBoD/zFbT6xzOKUKr9FOBBxqJ29H+AoIbCCYX5G50DApey2TqLoP05LOs26j0ScBqKMPCl4qttAwM2/0u/hm6X1oRaheIGAjvf1ynABzZaSiWybwR/rnidbVW4dLy/X4+G1bYmxZdWexLwHlq0hUKd1hJ4Dpu90RkgcD6Ly21TkipvA4CH7ZJL1QgAhFDTIdT5h0npLYBl+UJr4I1KuM3xcgLwh+300FBbWxu4tw0NccUc2yXPUwD9aVMoDGfoO4D44jh8JQFvWQEQeDlXzHraCWB9FpM/BAT4A+IPiUtsl7x3qVpOAg7p5XI5+c9/3f7suAXwMDtHaQscGjbfCWAdk1/R2jrUCu6tIL44dQIA2fbL+0nJ5d/cvn07BAAPvsQIvAGAchQ2CnyIL87zcgLI4le0t7eSqqio4Jc8bA8AU+TeTar/+EUA3P5CX/3nxYwt57lKizlqGp+Z5e8kRYn8+hvtVlXwU+eMby4uVev7SfsupO7ukMpKRPgs5LM/AaCVy7W4ky3L8nEM2JLFKam/cQMx4FP9+dS37AFg/+9vvvn44y9CQiJv3rpFAW5fTUGAG1xLWisgBfVOAYx1iSX1iACqry9JTV1ku+ShkJCoylu3bt28efMH0E0rofJqSgpj0flULhe5o8Bv1JdwsrY4G8keEMJ5EFwF/uMBMP6YctVi/x/QOIEEMOacr+fyKXvUskQPp3NR4HogIJVwUt1+P37FSylXK23+kZFUDJVAqLx6NeUhRuCc82ImBEBFzkn0n2S6fotTAuJwJlwTNO9vUVR2kH1kVNTFixfJECoR4E24YpGPmF9Btgz810+64Pgncjj3tGGFRLPvoK35Ty5e/OabT94DYDA8mHw+alqix7IplsxFq7JW2ft7rsbgBP7UwYMHs4aGPvxH5ONkTcZDSFlM3QjlZSWCFmyZxq5ii/0e7TU4XDb0iUR70TjiMrN+8xL66eMAoAhWAGNBXt6q9e60t+9r4SkU3icaFIkSqFmACs49CgAkAQ0E681c4AzuD7yTMTP4I8XDJGBbIqIuQkf6J0ygjlYwWnc4r0GGKMCgG5+5ytrIX0RF/nDzw0a0wOS7+Ex/gwYXDd4ZhL9E+CrbNPnzqMjIg+UwQQMg0MWXBlZLIYQ7d+6IDKfGp+Gf/RU6FSxN5UoW29dFQMA8SNKdO4Mig8buzlPMRNMnLKw5rJWuvvbguZnogwyJcLvT760avA/KIhKJ+qSrA1wEMLxRGQb7zHaAIAy3lF5kyJ3n6eqLG69Be0UGqd3xuicAIG1I8Pxvs6erb4ZskML5bK798TpGkJVH/UsEz7f8XH31ZHWueeL5/WYKgARZmpwwHUDAPAyT2L+5sskMRbYCEGGFiy/PeG5O3hAwcfz1DZJ1hokKPcVMDnINwPCe+IBjK5ZLPmkGwWdzLpbs5yLgJ7OgBIPXCShB+iTJTp+wMP4LQy5Gq0s899EAAAAASUVORK5CYII=", "z_w3": "data:image/png;base64,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", "m_idle": "data:image/png;base64,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", "m_atk": "data:image/png;base64,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", "f_idle": "data:image/png;base64,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", "f_atk": "data:image/png;base64,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", "r_idle": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAACACAMAAADDApyIAAAABGdBTUEAALGPC/xhBQAAAwBQTFRFrLzKTnueXpXBrb/PQ15zWYyyXI61gaO/wNDjwNHhwdTiR3WctsfWQllpRFVmRWZ+rcXORWeCc6HDTXeXXIuzUXueXpS/RFlsp7PApbW+wNTluszcRnCQWZG/UoeyWYy1XJO9wtXkvdbeP1VnRWV/tsjXqLrJSXmeWI24O1RmQlppUH+kwdPiw9flPVFjqrzLXZO9Q1hpTXyhRXactsfUQFpzT3yhVYasqLnFpbXBPVRnNU1erLzLXJW+T32iPFNlvc/bXJW+Vo20r8HPRnegWIqvW4+4WI+4VYKmOlBjTnqescLOQFlpT32kVomxqcPPWZW0qrrGAAAAeZGkZpW6XoaRpFB0W3WK/9g//9Ifhphs/+V/0bgpkbLMa09rQ0ddmLfPU0hg2GGOi1d52eXv//vv/++v/88PW5bEeqHAtMvez9/rx9nodZB84sAZUH6dt61AQWJ7TIGpYY6yhlFxSk9nx1uF8vb65+/1PVxzR3GTkqq9YJS9rL3Kl59dNFFo/WWXNFl3KD1OSYCrNk1gQVRj5FuJnLLE+GKUQ3CTV4u07V6N8mCRrsDPMU9nbaPNQlhqUoWuNFx8P2qMNlZvQGyQTISwUYGmNFNrP2SBO115S4KsT4awV5C9rb7MSnicUoy5WI64tcfWTIOuQG2RO2mMSH6pKT9RS3yiU4ixv9LjNkxcssXUSXujUY69PFBgTYe1Tom3U4u2Tou6R3ifOGKDO197sMLRTIazTn6kR3mgS3qfUIi0RXWaMkhZOWSGWpO/PWyRSoGtNU5iOF58SoKv/mWYO2F/O2eJS4SyVpLBo7PARXmiOVx3VJC/RnacMEpdPVVnP3CWM01gwdXkM0tepLXBprbDU5DARXihNElZPm6ULkNVPGqPOU5dRnukN1BjLkdbOVJkMUxgRHefLEVXQHGXv9PkL0lcRHigUpLEQ3WcLkZYK0NVQ3aeUI6/K0JUMUtfQnOa/8wAQnSbMk1hUY/AUpHDM05jUZDBMkxhMk1i////R3ymv9TlU5PF1RkKcAAAAFN0Uk5T2o9vr1+vb2+v389v788Pjx/vb49vX4+vn08/b8/P75+vfx+vf6/P79+PP4/vf1/vX1+fP48fz+9/v7+f3z+/319/H79/L7/vT7+/L39/Pw8PPwD3qLjnAAALzElEQVRo3u2ZeVhTVxrG+8w+033fN1u36rgvtaIioCAIgTtL21m6Tvda61o3qh2tHZyBEYGwbxKRgAQIAUJIWCQYZMtFjMgiWQghMYGQEJYAIfOde7OArSUJ9o95nrw8kNzDzfs731m/nHsX9hPrLjfADXAD3AA3wA1wA9wAN8ANcAPcADfg/xMw56kXfw960TPgJwF4/u6qTYtXzbnTgKcXX73a2zsJf65OTvbC39/MuZOAgN/2giZ7JwnBG0As9rxzAM/F2b3ZvRZ7KyM7e9WdAjyVDZpqjwi9QHjxTgCCg/yWft8fEbKzP/110JbZArzWxsaWvjO9fSyE7Ow9sbGxi2YJCIwtLTVFkgF8fuCrCaQDn5GEv+fmlsbGzhKwMTYrVywm/P8xYdNXnyPAJ2JxVmls0OwAsaXgH4kAByam6nMUgVgMMQTOCuBXmpXbIP6kd1r9iRhgvn0qBkLpmlkBFkEADeJ3oP0nbtEBCGGPuCE3qzR4NoA1KADxp5OTX90KmPgMdUKDODfLz2XA1iOVyU3XjSMjN80/rJsjI8brTcmVRza4BngM/IeNxtv62wHBrgE2A0D7IwGYb94cMQ4PA8HFJlpW2QQRjNy8LYAIAQC+LgI2VNb9WA/Y2qhy650CjBReRCocmUKYDQD7uK5uahcXmqzKnxLC9euVm2cBmBKA1mRXwRRAneuAZ+uu2wFG8P36i8HBwS++hnda+ziqq1vmKmArAGwBXAb/QVJAuGjvhLq6DS4BvB5bQHQBIz+/kAzgT4NW/cVkMqJOgX+hNqp7YZnzAD/fyromaCGtpcmhh78E648+nPjgo8EviKIC+I+YYSQm8wvBTgK2JCcTs2ykhuhUsznfZPobAP4Ky9yHg4PEQEL+4ovGYQaDkZz+gnOAYN/0tDRqDSxEx2cAHDcOF2TmpzHTNzsF2Az+iXITAIgIMm1N9OYHEx+8YWmiTASoMWrz+9VUJtM32BmAL5NJVcvboI2MF8FfS3TyDtS/H73xJtHJUKTNhAC0w1q22qDm0k/9ygnAllNMrkrdr0JLnZnBIJaGi2QISF+aTMfJpaMQFjvtRbVecZxL/6UTgKBTXK4BAIXG6RP5a+s0MBXaFruC2mKDXiFOom91EqAHgKnwlqVo544dO3bCK9s2zTIjdFHOA7ygieQAiD4axrAvzgzbUlRom8eKbp0uSq9XZCbRn3eqk08xawAgGBs/yrETjOxMNKQuG207WvxYtw5X6PV6ahL9EeeGKTMtQ44A46O1t99v9EMIoNYbapLoa50apsEL0tMYBZkxCHB7wvFxBIhryMyHUfqIk0uFbzKDoc0cQoBRHmH38X/tIrs+mgA0FqYxmaeed3axC34WUgoL4CjaX0yv21P37+JR33PGCUB8Wlp6+jIX9oMV3GEjCRgNM5sTRw/aAYdRibmRAHTHMJKf93JhP1goqx7SWQDRZnPY6Ojr31n0h9HRYrOZPUoAxloWupQ6Lm+WtHTruknAKNvMG50mAISNk03UIlviAuCV0zJJiw4BCALHzGicBoAFvJgE4C2S5lecBzzeLKse0+FWADQ5I77YrkSYBEeR/xguFVU3P+484DS0kC5aLxgnCWE/kJeC/9AoP1qKVzefdgEgq+7WKdQdUbW1FRUVRVGKKx1VVTfO1YLO3aiq6rhyRVFUVFHRcaVDirfIXAWo1LDSg/MNcK4oKuKfOfMN6MwZPvK2gBRxrgFeQwB5v0FvqzpJQAL/ogprJIpxZYvsNecBv0AAg5oAWELgR/QgRZxB9YcASECHVKmTPBPsNGBjMQzSc/2oiYgQblSMnz//T1IRFaj+524QgAoAJGRtdBawIosjwHX8fmsIVUU9AwPnrZJWnLP6K75RKgWsstIVzgH8SstY8tqIOOgEAxHDDV1P38AAYgych5cIwp4YSxGjtWohEPycAax+MD5eQFOr+/tRCHqFQhHXo+np6et7+8/vDvQhfVNF6+hA/nroJ0OMID7+wdUOA+7bDrNYhOPRAJADARC1Uo1Uo+nZe/Lkyb3Qz5oeaRWyB//5QrU6WomLqmXN2+9zEHAv6Y/jAuF8uZyIIlopVUrf3n8Saf+7Go1GyoewFHq10GeFUIArScK9jgGg/sVRUUU6HB9/ZiVLLper5HocPN76t1VvSaXKCD0EpmalrsSeqRYpdUVRUcUQg0OATbKDPGgXgVLUsh5jseT9qjaaTqfD9/7Hqr1QY7xf3S+HzoUKSUS4QG8w8A7KNjkEaJZF8QwGQwcuOrEN8+ew5AAYG+ru3nfsXxbt00Ey1KaSy1ll/hi2TdKC0yBx4UXJmh2MIB4BDKJqyTYsEIarSgUAWFTfu3Tp0jHQe93dsE43EIBAtKicEIG/Xh3vYAQvSeIU4C9okcgWYn5ZHJVcpScA718i9T7aaI5CBCoWOmlZ2CwRQRPpFXGSlxwC3C8RxfH50WhYrMaCYca1qRqODgFhnwWwD200jQCA6QVr0OrTEEI0nx8nktzvEGBNggjGDPJfThwYcQAgIELYjxro2H5ip6xtUKk4ZWvI3RuGNRqpCWscAuxMhYGta5FsIjbahw+FxcTQogiATUNDYzRaTEzYoYfJ/XsT9LMSF6TudASwpSyVR+ML4g+RU3872vu7x8aGpmsMZRMS68BffSi+mE/jpZZtcQDglyo0wAwtm2+ddlMBY0jky1QANr9MCFNHmOrnACAQAAYAbJwOsNjaNQ2wsQxqBYBAxwB6A09YtugWwK2aBlhUJuQZ9I4B/FN5MGuEZZZ7X961K6GxsTEB1GgX8T5h166XrbVCEeh5qf6OAdoyazJ2B1rP7ZqGtXAyiDRsEXmhHbaf4wTuzqjJbHMUsJvNzi9I8yWPUH42DaAFWQgEwHLMssE3rSCfnb/bIcCjpVw2ELjM9IcoaNTCwaAFQPojAgloqqskkgnKQ+lMbj58iFv6qCMTbQGXevkym13APHJ2LjzPWlDXpCUIyH8YDkgsBAR4Fj3emXv2CLOAzb58mcqlOzSTn0ui1iAEl3nh7NmnsWXJTQxkifybCBGtNIwA8M346bNnLzC5yL4Gvmg6MtG20Kk1ICqVzS0Bgifmn8tpa2toaGhr4+TC5NhoveSgS0/wL2GyqegzGVR60MwAyrzIjBo4usygspNKgHAPxZ/DUbWBYqJoLMh+VrBoUTHoGgj+lHvAv+SPSdQM+EhNRuQ8yoyAV0P3JB5PTMygJiVt/TkiePpwYD1VqQS67uqDMHYDD0JOKYACFYfj44n8PbYmASERtCf01RkBS1sPw50ZGZH057wwj5ILF+b6sGDvksfoIgQJMphYL8uiBRG6GChTsXzmXrhQEk7xeo4emYEIh1uXzgQIaG1tPbw2MpJOXwvt6Q0hePuwUO4iwGlyngy2rJdkPDkNF0DKJGf5eIO/B5ydrKXTIyPXHoYPB8wACGltvdZK8QoKCkJD3Ds8vMTbR9ivVqv5eIeQh9L012SHhB04H4r6hT7eJeHh3sTDtqAgLwp8tDVkRkD9tWvWiwdSwsPDV90tRDkAXzkeFydBAElc3LiSD0U84d2rSsJTUh6w3n/tWv2MAArcVG/tqXkpKSnhASt5aPXjQ7IlgjQDshSRUirlozSCtzIA/FPmWcdHPVSOMlMnr6uH29aR9VgVGprija3koey3USqVokQJ23ZCBG8bUeLIW4l5p4SGks9MQ9ZB1erXzTiKQuoRgYyU4hG6lIKtF5VrSOEkALdclovWY5SloR4Usm2Rf33IzDP5CXSfpSlDPAIIf5RPw295DgLklBMX6BoIAR4h1s4DPeHIWvSqLQKk9aRfH/z0aESQum0S2a/Lc9bbR8eUzpshfX9ynX04L0H+8IWjE/1o2k9g2Il2VICu+xBhiX0CrXvS+Qd1S7raNZ3EdydQn6Y9B8Ny2jXWggFAdi2ZzdPY5Xk55Z2dU+xIgLWkr7OzPCdv+SwA3wJA02lTeXsXhnW1l9tLoI3yvp0VAOzK263K6crDsLyunPYp6poV4PS3eXldduUhs+8Vnf5Ri/8BFq3UdLETBr0AAAAASUVORK5CYII=", "r_w0": "data:image/png;base64,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", "r_w1": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAACACAMAAADDApyIAAAABGdBTUEAALGPC/xhBQAAAwBQTFRFv9PjtsjYR3GSo7PDRHKWgKfDaZW7iq3ItcXWU4msq77LpL3OZo+yRVxsOldnvdDgprXAXZXCwdPjwtLiQl10QlxwOlJkUom0R3WaSHOUTHaZTnqdTX6kP1VlqLrFvc/dWpK9usvaXpG4XZG5X5a8QlhqXI2zPVJhwNLlvtHhvdbeW5PARGeCVIevUH2hobjFprbCuc7ZrLvIqsHMYJK+WZK9XJXBPFNlT32ip7rIUnufUX+kT4CmUH+jUX6lqrjIOlBiU4SqV422WpG7WYWqu8zZwNPiwNXiPVVnQFdnQldpQFVnqLbEqbvHp7fDSnKOprbDV4uzTnudO1NmVYq0WpXAVYWqP1ZlYZS7TnaTqLnFAAAATWd7gZms/+uf//XPZ4CTjJpn/9tP/9g/nLLEXo+1K0FTkVV36MIUQV92/+R3//G3XoaR+/r1tKxDdZu5MU1kR3uleafM82GRdVNy4+zzz1+Lv16I2+bw88cKl59dlK/FiarFZ1JufZR0Q3GVMk5la5W3ibPV+WOU/mWY0N/sflZ27fP3mVp+aYuG/9EVo6RTQmuMWI22WpG83+ny0bgpT32gSXujU4KmP1Jkn77XV1BrVm+DPmiJM1BoPFBgP1ZpVIu3NlVuN1lzT3+lWJPBSnmfO1JlrsLSUIOrVoeuVI67XJS/wNPjpMPdOWOEPVRmSYCrPWSDNFJqM1RtPGiMTISuV5C+OmWHMkteNU5iUIWuOFFkNUtcVImyVZLBQm6RSH6oNlZwRnKUprbEUYq3TH2jvtLjqcniq73MO2F+R3qjM0hZOU5eRneeToq5OFx5pLXBT4ezRXqjU4+/N09iPmuPS4SxNE1gQHGXMEpeK0JUwdXlo7PAT4u7qLnHS4GsTIe1SoGuTYi3QG+VTIazT429Mk1hLUVXLUNVMEldQ3aev9TkP22TRXihQXOZRHegLkZZUpHCQnWcL0hb/2aZUpHDMkxhUI6/UpLE/8wARXmiRnuk////UZDBM05jMUtfMk1iR3ymv9TlU5PFMZB03wAAAFx0Uk5T+PrfL69/358fX08f729Pn6+vb09Pj5/f75/Pf69vT3/vl1+PX68vnz+/H98vj68fyi/PD2+/v88/31+fby/fb6/v709PX++/339fv59/jx/vf7/vz3+/Pz8PPwCvpryUAAAJ/0lEQVRo3u2Zd1Rb1x3HczqT7rRp9t7DduLGjkc84r03W90jbXbIauKF7TaOd21sXJYI01ADApkhiSkoAiQhrIFihoTEEhrwZEkgIT09u797JZDMsXPyHup/+vpY6OjA93N/v9+9v3vv022s/7NuCwPCgDAgDAgDwoAwIAwIA8KAMCAMCAPCgJtp7mPr1l5BWrvukedDD1iz7krB8PAw+MNrwZV1vwgt4NnnCgqGrw0HVFDw3PMhBPy8AI1++NqkMGHtsyED/LSgcbgxYI8R8EnBmhAB1jSCbvS/dg19tnZuCACro6IO5oDZtekabmzM+VFU1OoZAradPftlQ16jP/+f/wvp88kQ8hq+PHt228wAd4B/YnwS9v90wq93PsUhJMUnAmHxzACvgr/LlQR+V76YCOiLK/BJkssFhFdnBljWkNjscqEAgv2BgJLkcjUnNiybEWApDuAgAD6euFEfQ44O4hCWzgSwBAJod+2F8k5MF5R6r6sdQljCGBATGRlRqVTq9R8cOpT03+lKOnToA71eqayMiIyMYQaYl3/q0uXL7lHb2PWba8w26r58+dKp/HkMI8hH/m7b2C0BYzY3IuTHMAc4viYAXwgO5gBW/tdnaCpH+bFMAZnT/R19INs0QmY+02n6QmbVDYCuIgpL6Q4GVGW+wBTwCgCCSqynptQ1VWYEeIUp4M7MqqAAJGC8//jx47vfhjfuwDyaASCyKgjgBtvT40if7acobRCgKpIhYNX8qtEAQElR74779NlRinJMAUar5q9iAnjy0cwqVGO9P+UU9TYyP/bmm8fG/0ZRevhIS8VTDpinVZcefZI24IlTl/Aq6IpHRbVd76Oo3cj/nYmJ346PH0U50lDxLlcRWssXLp16gibg8VMXLlyQwDrWY0AfAhwHwJ9QIx0f348A2ngAtLsdfbKu9PSTj9MCxK5MT++Ntzjc7mmAY+D/O38EWuTvhLVHmJRCwcpYOoAdJ4XCeMLQ5XY7IM9UEa7BUVSDP7711mQNJABwah19EsJMyGSCHXQAEQJZj5kw9Lrdow6tVm/DFfXP0nGUIYjp+lhXUY3S0delN5s7aioFEXQAJwUyEwIENVPI0Rn/OvgDRdWgNgHNGhKk15k7dAS3Mo8OQCCQGQCgDe7WaL7uPn369LuwCtAyQH0IAOKUjA6d0UwboIcIiORijdt2s14k8e82jr6yIatUZzSae3JpAaIEshqIoIy0F/cFuqmkxmevtfkbqVuSocYAhaknN4rWLIIcNROEgrTbU8SB9m/r0mg0vY7AblYL/iNlRoWuJzd3B811IBQWYYDXa7rFbuZ2F5MIkGwkinpyV9BaB6xVJ9PThb0a0t7v9XqoWwCakb/VWgT2uXmrafaiVSuhV1z2ATg4KdR/AqLwVlOCAUP6ysrKFatpd9On50OzY2OA5wT4J3uCLgeeBCiBmATAUHmGTJAX9TSzk93OXT4AB+aox/ObKf/fezgAkAJAXa5asGMHw2PLT9ZXeKHGAIAq9MDrr//t0xvwfsymsZPkULlKvpHp2XRjIa/C2+8DJFx3cDzBqh2ziQEAAeyKZQiIXZ/Nq7D7ASLIUTChVj9mO4EjkO9iej/4cRqvoj8IcF3SE5ADZqkUAJChQqaApwp5KntJLRZb1Nur0ej9gsWMJCphp5SrshlHsKlQrkpxtpsMhFkHzaa0tKzsIlZZWWmpwmjUdZiJ0vKK7KcYA7Ir7CJnu9NCQLs3GhUYgQT2Pn+zIblcnr2RMYCHAL4QOlAMiosZJSUlUuyv64DxEwaRSr6e8UX8NbmKrHWiEHwERckglvWib/iEwWBhq+TRDAF3redVqMj3TU4QIphL7SMDfmX4hm8xmTgq+YJYRoDoNCgxTEMFJkCWjGqrdcQnq/UijN4AsZnYHHn2LxkB1hfyCEOxlxSZEAHSVDIEsu47D93ZOmQ3W5ztcGQxWcSi7LRtDADRadnVYoOlQ1prQYR2lxGiIdUfffjhX9VqNUmKXHAkQgCDmF24gRGAJ4YsWIykxYJDyIAFbT/8D9An52GTS6HQsRQDMhgBYgvlyWiWlJIKTGhHHePw1av/BF39CDW/SYCZV8ikm8amyTlmg8HMsYswwAiA81f9OgKAYj8gIUPOqJsuPlFRfoDNTlGp2DCHfIBzk4B9UwAOSap4jGbRnCxRORRTVSHfdW8zEBDA+3c/wDMFgMKr3mD0vOhMllhkJ1Vy3t3bHkxshghQ2z7s8/8EA9DJ3QBdNiFrJwPAQgAQZkV13WLfAx2n2R7IESqBR4GvBhaYRYwAD5wREwQhzmrYhh5JoRA4gRydB/8DFuRvsljEzABzssSwvpqz8NOyFQ2JTmcxApw/cuTwPvD3ejnFxdLa2mRLfDMzwP0NMtixhEJcvwcbIALDAf/e6UH+Xm+/3W4nRQatRNjABHBGptHDtpiO7ywbsqGt2ic354A9SUoNBokwfQ4DgECGtl6Z8MK8GwFebD/pr2YTBFeYPps+IEYgU4KAEHE7i/UQ2hgmCX5/EvmrSwizViO8hzZgy55KrtZHOJnzCCuaB/4BQH+/VCpNVpxIcJrEZnM83C7pApY37eFqsZQyWU7OY9EQAPKsrhYXFSnhVoMufl0SSW+vtqPDqZT9ZTM9wA+7u7t7eop6eoDAPdiUk/N9oUTS1QdXcngwYhvF974+ZK/Ru3S6Gi73vaYf0AJs7a6vfw+f3rhc7p6mppxFvUIfAAjY34GHD49MCQSo/HP3r2gBXqqvr98ekZubC7eK2YuagHBPr2SSgPOD/DXwRFar0yVwK/fWd3e/SAdQX9/WtoU1e0Ve3rI7WA93A+F7QmGXD4D8EUApNlFOE1Gd8J2FMTCe7jhagLbOzqmyxXUD4btwHwRATU1NdXW1VMqWSg+MSI2g6rpZrBdhPPW0ANs7OztfmppRCDA3ZomIh2Y+iZcXulfWwtmxurruPihZW2dbPa0abAZA51ac1ZeXbwfAImjfIhWpxgjwfz/jolGH/b8Vy9oC8bb9jBYgDv6kE6qAEwQFbIK3d8lV5Wq/P4kefejAvu7eWd9uw78cR2+hbQ38DQSA5+Dd8hP9Q2okOHyVdOgSEhLq6u5fCoNBgK10W8Xmtsmsbgb/l+HnAnlCGTrZIX/riAjZ1z2AQoQZ4QuWXrNbvshf5TXbtyJ/VqG8nwMnRiu61lut5ZCenQtZPsD2h0PxVWO2agideUEj8I+fdt/kcTQuLiRfNUbz+OhkjdxBfP5rof7COjqVD3eDkQFwhx/81lmhBjzU2jJ1+Riw0grgmwE2tLYMwN1pYBC9jvCjQw54ht8y8BVocBD+D7SEPoJN/JHB17/ya7CF/0yoAQsA4Ce8PgiA1I0hBqTycQ18Gmjht54LMeBcK78lIH5r6q7QAqLTzqW2BpSaem7TNwf8D/PkRbd+H2UnAAAAAElFTkSuQmCC", "r_w2": "data:image/png;base64,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", "r_w3": "data:image/png;base64,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", "r_atk": "data:image/png;base64,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", "r_jump": "data:image/png;base64,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"};
const IMG={};
let toLoad=0, loaded=0;
for(const k in SPR_DATA){
  toLoad++;
  const im=new Image();
  im.onload=()=>{ loaded++; };
  im.src=SPR_DATA[k];
  IMG[k]=im;
}

const cv=document.getElementById("vt_cv"), ctx=cv.getContext("2d");
let W=0,H=0,DPR=1;
function resize(){
  DPR=Math.min(window.devicePixelRatio||1,2);
  W=window.innerWidth; H=window.innerHeight;
  cv.width=W*DPR; cv.height=H*DPR;
  ctx.setTransform(DPR,0,0,DPR,0,0);
  ctx.imageSmoothingEnabled=true;
}
window.addEventListener("resize",resize);
function mulberry(seed){ return function(){ let t=seed+=0x6D2B79F5;
  t=Math.imul(t^t>>>15,t|1); t^=t+Math.imul(t^t>>>7,t|61);
  return ((t^t>>>14)>>>0)/4294967296; }; }
const clamp=(v,a,b)=>v<a?a:v>b?b:v;
const sign=v=>v<0?-1:1;
function lsGet(k){ try{ const v=localStorage.getItem(k); return v?JSON.parse(v):null; }catch(e){ return null; } }
function lsSet(k,v){ try{ localStorage.setItem(k,JSON.stringify(v)); }catch(e){} }
function lsDel(k){ try{ localStorage.removeItem(k); }catch(e){} }

/* ---------- Sonido ---------- */
let AC=null, muted=false;
function beep(f,d,type="sine",v=.12,slide=0){
  if(!__active) return;
  if(muted) return;
  try{
    AC=AC||new (window.AudioContext||window.webkitAudioContext)();
    const o=AC.createOscillator(), g=AC.createGain();
    o.type=type; o.frequency.value=f;
    if(slide) o.frequency.exponentialRampToValueAtTime(slide,AC.currentTime+d);
    g.gain.setValueAtTime(v,AC.currentTime);
    g.gain.exponentialRampToValueAtTime(.001,AC.currentTime+d);
    o.connect(g); g.connect(AC.destination); o.start(); o.stop(AC.currentTime+d);
  }catch(e){}
}
const sJump=()=>beep(300,.16,"sine",.1,500);
const sWJ  =()=>beep(430,.14,"square",.09,760);
const sShot=()=>beep(720,.09,"square",.08,1200);
const sHitE=()=>beep(180,.12,"square",.12,80);
const sHurt=()=>beep(140,.3,"sawtooth",.16,60);
const sChip=()=>beep(900,.09,"sine",.08,1400);
const sDie =()=>beep(220,.5,"sawtooth",.14,60);
const sCheck=()=>{beep(520,.15,"triangle",.1); setTimeout(()=>beep(780,.25,"triangle",.1),120);};
const sBuy =()=>{state.bought=true; beep(660,.1,"triangle",.1); setTimeout(()=>beep(990,.15,"triangle",.1),100);};
const sHook=()=>{ beep(420,.14,"square",.09,900);
  if(!state.onGround){ state.airHooks++; if(state.airHooks>=3) logro("trapecista"); } };
const sFail=()=>beep(180,.12,"sine",.07);
const sTele=()=>beep(240,.3,"sine",.07,120);
const sBoss=()=>{beep(90,.5,"sawtooth",.16,50); setTimeout(()=>beep(70,.6,"sawtooth",.14,40),260);};
const sWave=()=>beep(120,.25,"sawtooth",.13,60);
const sWin =()=>[440,554,659,880].forEach((f,i)=>setTimeout(()=>beep(f,.3,"triangle",.12),i*170));
document.getElementById("vt_sndBtn").onclick=e=>{
  muted=!muted; e.target.textContent=muted?"🔇":"🔊";
};

/* ---------- Paletas de sector ---------- */
const SECTORS=[
  {name:"S-1 · LAS CLOACAS",    wall:"#17251f", panel:"#1e332a", pipe:"#2c4a3c", lamp:"140,230,180"},
  {name:"S-2 · SALA DE MÁQUINAS", wall:"#241a14", panel:"#32241a", pipe:"#553a24", lamp:"255,180,110"},
  {name:"S-3 · LAS OFICINAS",   wall:"#161a2c", panel:"#202742", pipe:"#38406b", lamp:"150,180,255"},
  {name:"S-4 · EL PENTHOUSE",   wall:"#221430", panel:"#301c46", pipe:"#533472", lamp:"220,160,255"},
];
const ROOF={name:"AZOTEA · EL CUSTODIO", wall:"#0a0d1e", panel:"#11162e", pipe:"#232c55", lamp:"255,120,150"};

/* ---------- Constantes del mundo ---------- */
const TW=760, WALL=36, CH=480, BH=560;
const SPEED=235, JUMPV=600, GRAV=1650, WALLSLIDE=75;
const PW=30, PH_S=58, PH_C=32;

/* ---------- Generación de la torre ----------
   Convención: y crece hacia abajo; la torre se apila de abajo arriba.
   Cada sala garantiza su ascenso con una "ruta de servicio": cornisas en
   zigzag (saltos de +84 px, alcance validado) que desembocan en el hueco
   del suelo de la sala superior. Pozos y conductos son rutas con premio. */
function genTower(endlessSeed){
  const rng=mulberry(endlessSeed||777);
  const L={solids:[],steams:[],anchors:[],chips:[],enemies:[],checks:[],
           terminals:[],chunks:[],zaps:[],lights:[],civs:[],vigia:null,summit:null};
  const pools=[
    ["shaft","office","ropes","office"],
    ["vent","ropes","steam","office"],
    ["ropes","vent","office","steam"],
    ["shaft","steam","ropes","vent"],
  ];
  let seq=["base"];
  if(endlessSeed){
    for(let s2=0;s2<12;s2++){
      const p=pools[s2%4].slice();
      if(rng()<.5) p.reverse();
      seq.push(...p);
      if(s2%2===1) seq.push("check");
    }
    seq.push("check","summit");
  } else {
    pools.forEach(p=>{ seq.push(...p); seq.push("check"); });
    seq.push("boss");
  }
  const N=seq.length;
  const TOTALH=(N-1)*CH+(seq[N-1]==="boss"?BH:CH)+40;
  L.totalH=TOTALH;
  const gxs=[190,380,570];
  // huecos de entrada de cada sala (el de la sala i es la salida de la i-1)
  const entry=[null];
  for(let i=1;i<N;i++){
    entry.push((seq[i]==="vent"||seq[i-1]==="vent")?190:gxs[Math.floor(rng()*3)]);
  }
  for(let i=0;i<N;i++){
    const type=seq[i];
    const hh=(type==="boss")?BH:CH;
    const top=TOTALH-40-(i+1)*CH-(type==="boss"?(BH-CH):0);
    const sector=endlessSeed?(Math.floor(Math.max(0,i-1)/4)%4):Math.min(3,Math.floor(Math.max(0,i-1)/5));
    L.chunks.push({type,top,bot:top+hh,sector});
    const S=(x,y,w,h,one)=>L.solids.push({x,y:top+y,w,h,one:!!one});
    S(0,0,WALL,hh); S(TW-WALL,0,WALL,hh);          // muros exteriores
    const gap=entry[i];                              // hueco de entrada (suelo propio)
    const exitX=(i<N-1)?entry[i+1]:null;             // hueco de salida (suelo de arriba)
    if(type==="base"){
      S(WALL,hh-36,TW-2*WALL,36);
      L.spawn={x:TW/2, y:top+hh-36-PH_S/2};
      L.baseY=L.spawn.y;
    } else {
      S(WALL,hh-36,gap-50-WALL,36);
      S(gap+50,hh-36,TW-WALL-(gap+50),36);
      S(gap-50,hh-36,100,10,true);        // trampilla sobre el hueco de entrada
    }
    const floorY=top+hh-36;
    /* ---- ruta de servicio hacia exitX ---- */
    if(exitX!==null && type!=="boss"){
      if(type!=="ropes"){
        const ys=[354,264,174,84], side0=rng()<.5?1:-1;
        ys.forEach((yy,k)=>{
          const sd=side0*(k%2?-1:1);
          S(exitX+sd*60-35, yy, 70, 16, true);       // estrechas: más habilidad
          if(sector===1&&(k===1||k===3)&&type!=="check")
            L.zaps.push({x1:exitX+sd*60-31,x2:exitX+sd*60+31,y:top+yy,ph:rng()*2.2});
        });
      }
      if(type==="ropes") S(exitX-110, 95, 220, 16, true); // recepción ancha del columpio
      S(exitX-45, 40, 90, 16, true);                 // cornisa final bajo el hueco
    }
    /* ---- interiores por tipo ---- */
    if(type==="shaft"){
      // dos columnas que flanquean la ruta: canal para rebotar en pared
      S(clamp(exitX-165,WALL+8,TW-80), 120, 30, 224);
      S(clamp(exitX+135,WALL+8,TW-70), 120, 30, 224);
      L.chips.push({x:exitX,y:top+150,got:false});
      if(sector>=1) addZombieOn(L,gap,floorY,rng);
    }
    if(type==="vent"){
      // conducto lateral (36 px de paso): botín al fondo
      S(300,352,TW-WALL-300,56);
      L.chips.push({x:430,y:top+428,got:false});
      L.chips.push({x:650,y:top+428,got:false});
      addZombieOn(L,gap,floorY,rng);
    }
    if(type==="ropes"){
      /* sala de aros: SIN escalera — el gancho es la única vía */
      const off=rng()<.5?1:-1;
      const A1={x:clamp(exitX+off*120,150,610), y:top+300};
      const A2={x:clamp(exitX-off*100,170,590), y:top+175};
      const A3={x:clamp(exitX+off*55,190,570),  y:top+50};
      L.anchors.push(A1,A2,A3);
      L.chips.push({x:A2.x,y:top+225,got:false});
      L.chips.push({x:A3.x,y:top+130,got:false});
      if(sector===3){                       // aros laterales: ruta de botín
        const B1={x:clamp(exitX-off*180,160,600),y:top+260,side:true};
        const B2={x:clamp(exitX-off*230,180,580),y:top+120,side:true};
        L.anchors.push(B1,B2);
        L.chips.push({x:B2.x,y:top+180,got:false});
        L.chips.push({x:B2.x-off*40,y:top+150,got:false});
        L.chips.push({x:B2.x+off*40,y:top+150,got:false});
      }
      addZombieOn(L,gap,floorY,rng);
    }
    if(type==="office"||type==="steam"){
      const my=type==="office"?280:300;
      const ex=exitX!==null?exitX:380;
      if(ex-120>WALL+40) S(WALL,my,ex-120-WALL,26,true);
      if(ex+120<TW-WALL-40) S(ex+120,my,TW-WALL-(ex+120),26,true);
      addZombieOn(L,gap,floorY,rng);
      const gx2=ex<380?TW-160:150;
      addGunner(L,gx2,top+my,(sector>=3?"f":"m"));
      L.chips.push({x:ex<380?600:160,y:top+my-40,got:false});
      if(type==="office"&&sector===2)
        L.lights.push({x:ex<380?520:240,y:top+34,ph:rng()*6.3});
      if(type==="office"&&sector>=1&&rng()<.55)
        L.civs.push({x:ex<380?660:110,y:top+my,v:sector>=2?"f":"m",saved:false});
      if(type==="steam"){
        L.steams.push({x:gap<380?560:200,y:floorY,ph:rng()*3});
        L.steams.push({x:ex<380?TW-260:260,y:top+my,ph:rng()*3+1.4});
        L.steams.push({x:gap<380?360:420,y:floorY,ph:rng()*3+.8});
      }
    }
    if(type==="check"){
      if(sector>=1) addGunner(L,TW/2+190,floorY,(sector>=2?"f":"m"));
      L.terminals.push({x:TW/2,y:floorY,idx:L.terminals.length,done:false,sector});
      L.chips.push({x:TW/2-140,y:top+390,got:false});
      L.chips.push({x:TW/2+140,y:top+390,got:false});
      if(!endlessSeed && i===10 && exitX!==null){   // EL VIGÍA custodia el paso
        L.vigia={x:TW/2,y:top+170,hp:14,maxHp:14,st:"hover",t:0,cool:2,dive:4,
                 flash:0,dead:false,top,gy:floorY,x1:WALL+40,x2:TW-WALL-40};
        L.solids.push({x:exitX-52,y:top-38,w:104,h:40,vg:true}); // puerta blindada
      }
    }
    if(type==="summit"){
      L.summit={x:TW/2,y:floorY};
      L.chips.push({x:TW/2-60,y:top+380,got:false});
      L.chips.push({x:TW/2+60,y:top+380,got:false});
    }
    if(type==="boss"){
      L.anchors.push({x:250,y:top+120});
      L.anchors.push({x:510,y:top+120});
      L.bossArena={x1:WALL+10,x2:TW-WALL-10,gy:floorY,top};
    }
  }
  return L;
}
function addZombieOn(L,gap,floorY,rng){
  // patrulla el tramo de suelo más grande junto al hueco de entrada
  const left=[WALL+22,gap-72], right=[gap+72,TW-WALL-22];
  const seg=(right[1]-right[0])>(left[1]-left[0])?right:left;
  const x=seg[0]+(seg[1]-seg[0])*(.3+rng()*.4);
  L.enemies.push({type:"z",x,sx:x,y:floorY,x1:seg[0],x2:seg[1],dir:rng()<.5?-1:1,
    state:"patrol",t:0,hp:2,flash:0,dead:false});
}
function addGunner(L,x,topY,variant){
  L.enemies.push({type:"g",v:variant,x,sx:x,y:topY,dir:x>TW/2?-1:1,
    state:"idle",t:0,cool:0,hp:1,flash:0,dead:false});
}

/* ---------- Estado ---------- */
const state={
  running:false, lvl:null, bossMode:false,
  px:0,py:0,vx:0,vy:0,onGround:false,crouch:false,face:1,
  wall:0, coyote:0, jbuf:0, airJumps:0, animT:0, t:0,
  hearts:3, invuln:0, kb:0, energy:5, chips:0, kills:0, deaths:0,
  hook:null, boss:null, notice:null, wallLock:{s:0,t:0}, groundOne:false,
  up:{maxHearts:3,dbl:false,dblShot:false,slide:false},
  spawn:null, spawnCk:-1, cam:{x:0,y:0}, parts:[], shots:[], prevVy:0,
  mode:"tower", runT:0, maxUp:0, bestFloor:null, shadowY:0,
  secNoDmg:true, airHooks:0, bought:false,
};
const rec=Object.assign({wins:0,bestTime:0,bestAlt:0,civs:0,logros:{}}, lsGet("vertigo_rec")||{});
function fmtT(t){ const m=Math.floor(t/60), ss=Math.floor(t%60); return m+":"+(ss<10?"0":"")+ss; }
/* ---------- Logros ---------- */
const LOGROS=[
  ["cumbre","El Custodio ha caído","Completa la Torre"],
  ["vigia","Cazadrones","Derrota al Vigía"],
  ["oro","Relámpago","Oro en Contrarreloj (≤10 min)"],
  ["sombra","Más rápido que la noche","Gana en Persecución"],
  ["cielo","Cabeza en las nubes","500 m en Infinita"],
  ["intacto","Ni un rasguño","Un sector entero sin daño"],
  ["trapecista","Trapecista","3 re-enganches sin tocar suelo"],
  ["salvador","Salvador","Rescata 6 civiles (total)"],
  ["espartano","Espartano","Gana la Torre sin comprar mejoras"],
];
function logro(id){
  if(rec.logros[id]) return;
  rec.logros[id]=1; lsSet("vertigo_rec",rec);
  const L2=LOGROS.find(l=>l[0]===id);
  state.notice={txt:"🏆 LOGRO: "+(L2?L2[1]:id), t:3.4};
  beep(660,.1,"triangle",.12); setTimeout(()=>beep(990,.14,"triangle",.12),110);
  setTimeout(()=>beep(1320,.2,"triangle",.12),240);
}
/* ---------- Música chiptune ---------- */
const MUS={on:lsGet("vertigo_mus")!==0};
const MSCALES=[
  [220,262,330,392,440,524],      // cloacas: menor
  [196,247,294,349,392,494],      // máquinas: sol
  [262,330,392,466,524,660],      // oficinas
  [233,294,349,440,466,588],      // penthouse
];
const MPATS=[
  [1,0,3,0, 2,0,1,0, 4,0,3,2, 1,0,2,0],
  [1,1,0,3, 0,2,2,0, 1,0,4,0, 3,2,1,0],
  [3,0,4,0, 5,0,4,3, 2,0,3,0, 1,0,0,0],
  [1,3,5,3, 4,0,2,0, 1,3,5,6, 4,3,2,0],
];
const MBOSS=[1,0,1,2, 0,1,0,3, 1,0,1,2, 4,3,2,1];
let mStep=0;
function mtick(){
  const bpm=state.bossMode?150:126;
  setTimeout(mtick, 60000/bpm/2);
  if(!MUS.on || !state.running || !state.lvl) return;
  const ck=state.lvl.chunks[chunkAt(state.py)];
  const sec=ck?ck.sector:0;
  const sc=MSCALES[sec], pat=state.bossMode?MBOSS:MPATS[sec];
  const n=pat[mStep%16]; mStep++;
  if(n) beep(sc[n-1],.14,"square",.035);
  if(mStep%4===1) beep(sc[0]/2,.22,"triangle",.05);
  if(state.bossMode&&mStep%8===5) beep(sc[0]/4,.2,"sawtooth",.045);
}
setTimeout(mtick,600);

function startGame(fromSave,mode){
  state.mode=mode||"tower";
  state.lvl=genTower(state.mode==="endless"?(1+Math.floor(Math.random()*1e9)):0);
  state.runT=0; state.maxUp=0; state.bestFloor=null;
  state.secNoDmg=true; state.airHooks=0; state.bought=false;
  state.hearts=state.up.maxHearts=3;
  state.up={maxHearts:3,dbl:false,dblShot:false,slide:false};
  state.chips=0; state.kills=0; state.deaths=0; state.energy=5;
  state.spawnCk=-1; state.spawn=state.lvl.spawn;
  if(fromSave){
    const sv=lsGet("vertigo_save");
    if(sv){
      state.up=Object.assign(state.up,sv.up||{});
      state.chips=sv.chips||0; state.kills=sv.kills||0; state.deaths=sv.deaths||0;
      state.hearts=state.up.maxHearts;
      const ck=state.lvl.terminals[sv.ck];
      if(ck){ state.spawnCk=sv.ck; state.spawn={x:ck.x,y:ck.y-PH_S/2};
        for(let i=0;i<=sv.ck;i++) state.lvl.terminals[i].done=true; }
    }
  }
  state.shadowY=state.spawn.y+420;
  respawn(false);
  state.running=true;
  updateHUD();
}
function respawn(died){
  state.px=state.spawn.x; state.py=state.spawn.y;
  state.vx=0; state.vy=0; state.kb=0; state.hook=null; state.wall=0;
  state.shots.length=0; state.invuln=1.2; state.energy=5;
  state.cam.y=state.py-H*.55;
  if(state.lvl) for(const e of state.lvl.enemies){
    if(e.dead) continue;
    e.x=e.sx; e.state=e.type==="z"?"patrol":"idle"; e.t=0;
  }
  if(state.boss && died){ /* el jefe conserva su vida: siempre se puede ganar */ }
  if(state.mode==="chase") state.shadowY=Math.max(state.shadowY,state.py+520);
  if(died){ state.deaths++; state.hearts=state.up.maxHearts; sDie(); updateHUD(); }
}
function updateHUD(){
  const hp="❤".repeat(state.hearts)+"♡".repeat(Math.max(0,state.up.maxHearts-state.hearts));
  const en=state.bossMode?"∞":"▮".repeat(Math.floor(state.energy))+"▯".repeat(5-Math.floor(state.energy));
  const ck=state.lvl?state.lvl.chunks[chunkAt(state.py)]:null;
  const sec=state.bossMode?ROOF:(ck?SECTORS[ck.sector]:SECTORS[0]);
  document.getElementById("vt_hud").innerHTML=
    `<span class="hp">${hp}</span> · <span class="en">⚡${en}</span> · 💾<b>${state.chips}</b><br>`+
    `<span style="font-size:11px;opacity:.8">${sec.name}</span>`;
}
function chunkAt(y){
  const c=state.lvl.chunks;
  for(let i=0;i<c.length;i++) if(y>=c[i].top && y<=c[i].bot) return i;
  return c.length-1;
}

/* ---------- Entrada ---------- */
const keys={L:false,R:false,J:false,C:false};
let jPressed=false;
function bindHold(id,down,up){
  const el=document.getElementById(id);
  const on=e=>{e.preventDefault(); el.classList.add("on"); down();};
  const off=e=>{e.preventDefault(); el.classList.remove("on"); up();};
  el.addEventListener("pointerdown",on);
  el.addEventListener("pointerup",off);
  el.addEventListener("pointercancel",off);
  el.addEventListener("pointerleave",off);
}
bindHold("vt_btnL",()=>keys.L=true,()=>keys.L=false);
bindHold("vt_btnR",()=>keys.R=true,()=>keys.R=false);
bindHold("vt_btnC",()=>keys.C=true,()=>keys.C=false);
bindHold("vt_btnJ",()=>{keys.J=true; jPressed=true;},()=>keys.J=false);
bindHold("vt_btnF",()=>fire(),()=>{});
bindHold("vt_btnH",()=>ropeToggle(),()=>{});
window.addEventListener("keydown",e=>{
  if(!__active) return;
  if(e.repeat) return;
  if(e.key==="ArrowLeft"||e.key==="a"||e.key==="A") keys.L=true;
  if(e.key==="ArrowRight"||e.key==="d"||e.key==="D") keys.R=true;
  if(e.key==="ArrowDown"||e.key==="s"||e.key==="S") keys.C=true;
  if(e.key===" "||e.key==="ArrowUp"||e.key==="w"||e.key==="W"){ keys.J=true; jPressed=true; }
  if(e.key==="x"||e.key==="X") fire();
  if(e.key==="c"||e.key==="C") ropeToggle();
});
window.addEventListener("keyup",e=>{
  if(!__active) return;
  if(e.key==="ArrowLeft"||e.key==="a"||e.key==="A") keys.L=false;
  if(e.key==="ArrowRight"||e.key==="d"||e.key==="D") keys.R=false;
  if(e.key==="ArrowDown"||e.key==="s"||e.key==="S") keys.C=false;
  if(e.key===" "||e.key==="ArrowUp"||e.key==="w"||e.key==="W") keys.J=false;
});

/* ---------- Acciones ---------- */
function fire(){
  if(!state.running) return;
  const cost=state.bossMode?0:1;
  if(state.energy<cost){ sFail(); return; }
  state.energy-=cost;
  const ox=state.px+state.face*16, oy=state.py-8;
  let vx=state.face*520, vy=0, best=null, bd=300;
  for(const e of state.lvl.enemies){
    if(e.dead) continue;
    const ey=e.type==="z"?e.y-30:e.y-30;
    const dx=e.x-ox, dyy=ey-oy;
    if(sign(dx)!==state.face) continue;
    const d=Math.hypot(dx,dyy);
    if(d<bd){ bd=d; best={dx,dyy,d}; }
  }
  if(!best && state.boss){
    const dx=state.boss.x-ox, dyy=(state.boss.y-46)-oy;
    if(sign(dx)===state.face) best={dx,dyy,d:Math.hypot(dx,dyy)||1};
  }
  if(best){ vx=best.dx/best.d*520; vy=best.dyy/best.d*520; }
  state.shots.push({x:ox,y:oy,vx,vy,from:"p",life:1.1});
  if(state.up.dblShot)
    state.shots.push({x:ox,y:oy-10,vx:vx*.96,vy:vy*.96-40,from:"p",life:1.1});
  sShot(); updateHUD();
}
function ropeToggle(){
  if(!state.running) return;
  if(state.hook){ state.hook=null; return; }
  let best=null, bd=310;
  for(const a of state.lvl.anchors){
    const dx=a.x-state.px, dy=a.y-state.py;
    if(dy>-20) continue;
    const d=Math.hypot(dx,dy);
    if(d<bd){ bd=d; best=a; }
  }
  if(best){ state.hook={ax:best.x,ay:best.y,L:Math.max(60,bd)}; sHook(); }
  else sFail();
}

/* ---------- Física con paredes sólidas ---------- */
function rectsAt(x,y,hw,hh){
  const out=[];
  for(const s of state.lvl.solids){
    if(x+hw>s.x && x-hw<s.x+s.w && y+hh>s.y && y-hh<s.y+s.h) out.push(s);
  }
  return out;
}
function halfH(){ return state.crouch?PH_C/2:PH_S/2; }
function step(dt){
  state.t+=dt; state.animT+=dt;
  state.invuln=Math.max(0,state.invuln-dt);
  if(!state.bossMode) state.energy=Math.min(5,state.energy+dt*.8);
  if(state.notice) state.notice.t-=dt;
  state.wallLock.t=Math.max(0,state.wallLock.t-dt);
  const dir=(keys.R?1:0)-(keys.L?1:0);
  if(dir) state.face=dir;

  if(state.hook){
    state.vy+=GRAV*dt;
    state.vx+=dir*520*dt;
    state.px+=state.vx*dt; state.py+=state.vy*dt;
    const dx=state.px-state.hook.ax, dy=state.py-state.hook.ay;
    const d=Math.hypot(dx,dy);
    if(d>state.hook.L){
      const nx=dx/d, ny=dy/d;
      state.px=state.hook.ax+nx*state.hook.L;
      state.py=state.hook.ay+ny*state.hook.L;
      const dot=state.vx*nx+state.vy*ny;
      state.vx-=dot*nx; state.vy-=dot*ny;
    }
    if(jPressed){ jPressed=false; state.hook=null;
      state.vy=Math.min(state.vy-430,-430); sJump(); }
  } else {
    // agacharse (con techo bajo, se mantiene)
    const wantC=keys.C&&state.onGround;
    const headBlocked=()=>rectsAt(state.px,state.py-(PH_S-PH_C)/2-(PH_S-PH_C)/2,PW/2-2,PH_S/2-1)
      .some(s=>!s.one);
    if(!state.crouch && wantC){
      state.crouch=true; state.py+=(PH_S-PH_C)/2;          // pies quietos
    } else if(state.crouch && !wantC){
      if(!headBlocked()){ state.crouch=false; state.py-=(PH_S-PH_C)/2; }
    }
    const spd=SPEED*(state.crouch?(state.up.slide?.95:.6):1);
    state.vx=dir*spd;
    state.coyote-=dt; state.jbuf-=dt;
    if(jPressed){ state.jbuf=.12; jPressed=false; }
    // salto normal / de pared / doble
    if(state.jbuf>0 && state.crouch && state.groundOne){
      state.py+=12; state.vy=160; state.jbuf=0; state.onGround=false;
    }
    if(state.jbuf>0){
      if(state.coyote>0 && !state.crouch){
        state.vy=-JUMPV; state.coyote=0; state.jbuf=0; sJump();
      } else if(state.wall!==0){
        state.vy=-560; state.kb=-state.wall*320; state.face=-state.wall;
        state.wallLock={s:state.wall,t:.55};
        state.wall=0; state.jbuf=0; sWJ();
        burst(state.px,state.py,"255,255,255",6,70);
      } else if(state.airJumps>0){
        state.airJumps--; state.vy=-JUMPV*.9; state.jbuf=0; sJump();
        burst(state.px,state.py+20,"140,220,255",8,90);
      }
    }
    if(!keys.J && state.vy<-200) state.vy=-200;
    state.vy+=GRAV*dt;
    if(state.wall!==0 && state.vy>WALLSLIDE) state.vy=WALLSLIDE;
    state.kb*=Math.pow(.02,dt);
  }

  // mover eje X y resolver
  const hh=halfH();
  state.px+=((state.hook?0:state.vx)+state.kb)*dt + (state.hook?0:0);
  if(state.hook){} else {
    for(const s of rectsAt(state.px,state.py,PW/2,hh-2)){
      if(s.one) continue;
      if(state.vx+state.kb>0) state.px=s.x-PW/2;
      else if(state.vx+state.kb<0) state.px=s.x+s.w+PW/2;
    }
  }
  // pegado a la pared: en el aire, empujando contra ella
  state.wall=0;
  if(!state.onGround && !state.hook && !state.crouch){
    if(dir>0 && rectsAt(state.px+PW/2+3,state.py,2,hh-6).some(s=>!s.one)) state.wall=1;
    if(dir<0 && rectsAt(state.px-PW/2-3,state.py,2,hh-6).some(s=>!s.one)) state.wall=-1;
    if(state.wallLock.t>0 && state.wall===state.wallLock.s) state.wall=0;
  }
  // mover eje Y y resolver
  state.prevVy=state.vy;
  const prevFeet=state.py+hh;
  state.py+=state.vy*dt;
  state.onGround=false; state.groundOne=false;
  for(const s of rectsAt(state.px,state.py,PW/2-3,hh)){
    if(s.one){
      // solo te sostiene si venías cayendo desde encima
      if(state.vy>=0 && prevFeet<=s.y+6){
        state.py=s.y-hh;
        if(state.prevVy>1320 && state.invuln<=0){ damage(1,0); }
        state.vy=0; state.onGround=true; state.groundOne=true;
      }
      continue;
    }
    if(state.vy>=0 && state.py-hh < s.y){
      state.py=s.y-hh;
      if(state.prevVy>1320 && state.invuln<=0){ damage(1,0); }   // caída muy larga
      state.vy=0; state.onGround=true;
    } else if(state.vy<0){
      state.py=s.y+s.h+hh; state.vy=0;
    }
  }
  if(state.onGround){
    state.coyote=.1;
    state.airJumps=state.up.dbl?1:0;
    if(state.hook) state.hook=null;
  }
  if(state.hook && state.onGround) state.hook=null;

  // chips
  for(const c of state.lvl.chips){
    if(!c.got && Math.abs(c.x-state.px)<26 && Math.abs(c.y-state.py)<34){
      c.got=true; state.chips++; sChip(); updateHUD();
      burst(c.x,c.y,"140,255,210",10,100);
    }
  }
  extras(dt);
  // terminales (punto de control + tienda)
  for(const tm of state.lvl.terminals){
    if(Math.abs(tm.x-state.px)<34 && Math.abs(tm.y-14-state.py)<50){
      if(state.spawnCk<tm.idx || !tm.done){
        tm.done=true; state.spawnCk=tm.idx;
        state.spawn={x:tm.x,y:tm.y-PH_S/2};
        sCheck(); saveRun();
        openShop(tm);
      }
    }
  }
  // vapor
  for(const st of state.lvl.steams){
    const cy2=(state.t+st.ph)%2.6;
    if(cy2>1.45&&cy2<2.25){
      if(Math.abs(state.px-st.x)<16 && state.py>st.y-80 && state.py<st.y && state.invuln<=0)
        damage(1,-state.face);
    }
  }
  // llegar a la azotea
  if(!state.bossMode && state.lvl.bossArena && state.py < state.lvl.bossArena.gy+10 &&
     state.py > state.lvl.bossArena.top){
    startBoss();
  }
  updateEnemies(dt);
  if(state.boss) updateBoss(dt);
  updateShots(dt);

  // cámara
  const targY=state.py-H*.55;
  state.cam.y+=(clamp(targY,-(200),state.lvl.totalH-H)-state.cam.y)*Math.min(1,dt*6);
  state.cam.x = (W>=TW)? -(W-TW)/2 : clamp(state.px-W/2,0,TW-W);

  for(let i=state.parts.length-1;i>=0;i--){
    const q=state.parts[i];
    q.x+=q.vx*dt; q.y+=q.vy*dt; q.life-=dt; q.vy+=260*dt;
    if(q.life<=0) state.parts.splice(i,1);
  }
}
function burst(x,y,color,n,sp){
  for(let i=0;i<n;i++){
    const a=Math.random()*7, v=sp*(.4+Math.random()*.8);
    state.parts.push({x,y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-40,
      life:.5+Math.random()*.4,max:.9,color});
  }
}
function damage(n,fromDir){
  if(state.invuln>0) return;
  state.hearts-=n; state.invuln=1.2;
  state.kb=fromDir*220; state.vy=Math.min(state.vy,-200);
  state.hook=null;
  burst(state.px,state.py,"255,120,120",10,120);
  sHurt(); updateHUD();
  if(state.hearts<=0) onDeath();
}

/* ---------- Enemigos ---------- */
function extras(dt){
  const lvl=state.lvl, hh=halfH(), feet=state.py+hh;
  const alt=lvl.baseY-state.py;
  if(alt>state.maxUp) state.maxUp=alt;
  if(state.onGround){
    state.airHooks=0;
    if(!state.bestFloor||state.py<state.bestFloor.y)
      state.bestFloor={x:state.px,y:state.py};
  }
  if(state.mode==="endless" && state.maxUp>=5000) logro("cielo");
  const ci=chunkAt(state.py), ck=lvl.chunks[ci];
  const sec=ck?ck.sector:0;
  if(state.curSector===undefined) state.curSector=sec;
  if(sec!==state.curSector){
    if(state.onGround && sec>state.curSector && state.secNoDmg &&
       state.mode!=="endless") logro("intacto");
    state.curSector=sec; state.secNoDmg=true;
  }
  if(ck&&ck.sector===3&&ck.type!=="check"&&ck.type!=="boss"&&!state.hook&&!state.onGround){
    const wc=(state.t+ci*1.9)%7;
    if(wc>1.5&&wc<2.9) state.px+=(ci%2?1:-1)*100*dt;
  }
  for(const z of lvl.zaps){
    if(Math.abs(z.y-state.py)>420) continue;
    const u=((state.t+z.ph)%2.2)/2.2;
    const sx=z.x1+(z.x2-z.x1)*(u<.5?u*2:2-u*2);
    if(state.invuln<=0 && Math.abs(feet-z.y)<8 && Math.abs(state.px-sx)<15)
      damage(1,-state.face);
  }
  for(const li of lvl.lights){
    if(Math.abs(li.y-state.py)>420){ li.hit=false; continue; }
    const ang=Math.sin(state.t*.55+li.ph)*.55;
    const dy=state.py-li.y;
    if(dy>10&&dy<330){
      const bx=li.x+Math.tan(ang)*dy;
      li.hit=Math.abs(state.px-bx)<26+dy*.12;
      if(li.hit&&state.invuln<=0){
        for(const e of lvl.enemies)
          if(e.type==="g"&&!e.dead&&Math.abs(e.y-li.y)<CH)
            e.cool=Math.min(e.cool,.12);
      }
    } else li.hit=false;
  }
  for(const cv2 of lvl.civs){
    if(cv2.saved||Math.abs(cv2.y-state.py)>200) continue;
    if(Math.abs(state.px-cv2.x)<44&&Math.abs(state.py-cv2.y)<70){
      cv2.saved=true; state.chips+=2; rec.civs=(rec.civs||0)+1;
      lsSet("vertigo_rec",rec);
      if(rec.civs>=6) logro("salvador");
      state.notice={txt:"CIVIL RESCATADO · +2 💾",t:2.2};
      sChip(); setTimeout(sChip,110);
      burst(cv2.x,cv2.y-40,"140,255,190",12,120); updateHUD();
    }
  }
  if(lvl.summit && Math.abs(state.px-lvl.summit.x)<46 &&
     Math.abs(state.py-lvl.summit.y)<70){
    state.running=false;
    const m=Math.round(state.maxUp/10);
    if(m>(rec.bestAlt||0)){ rec.bestAlt=m; }
    rec.wins++; lsSet("vertigo_rec",rec); logro("cielo");
    sWin(); setTimeout(sWin,500);
    showInter("LA CIMA DEL CIELO","Has coronado la Torre Infinita: "+m+" m. Nadie sube más alto.",
      "VOLVER AL MENÚ",()=>toMenu(),false);
  }
  if(state.mode==="chase"&&!state.bossMode){
    const gap=state.shadowY-state.py;
    let spd=26;
    if(gap>1100) spd=48; else if(gap<260) spd=18;
    state.shadowY-=spd*dt;
    if(state.lvl.bossArena) state.shadowY=Math.max(state.shadowY,state.lvl.bossArena.gy+140);
    if(gap<200 && Math.floor(state.t*2)!==Math.floor((state.t-dt)*2))
      beep(90,.12,"sawtooth",.09,30);
    if(state.py+hh>state.shadowY+6){
      state.running=false; sDie();
      showInter("LA SOMBRA TE TRAGÓ",
        "Subiste "+Math.round(state.maxUp/10)+" m con la noche mordiéndote los talones.",
        "VOLVER AL MENÚ",()=>toMenu(),false);
    }
  }
  if(state.lvl.vigia) updateVigia(dt);
}
function updateVigia(dt){
  const v=state.lvl.vigia;
  if(v.dead||Math.abs(state.py-(v.top+CH/2))>CH*1.2) return;
  v.t+=dt; v.flash=Math.max(0,v.flash-dt); v.cool-=dt; v.dive-=dt;
  if(v.st==="hover"){
    v.x=clamp(TW/2+Math.sin(v.t*.8)*220,v.x1,v.x2);
    v.y=v.top+150+Math.sin(v.t*1.7)*36;
    if(v.cool<=0){
      const a=Math.atan2(state.py-20-v.y,state.px-v.x);
      for(const o of [-0.22,0,0.22])
        state.shots.push({x:v.x,y:v.y+10,vx:Math.cos(a+o)*230,vy:Math.sin(a+o)*230,from:"e",life:3});
      v.cool=2.1; beep(500,.1,"square",.07,-200);
    }
    if(v.dive<=0){ v.st="tele"; v.t=0; sTele(); }
  } else if(v.st==="tele"){
    if(v.t>.5){ v.st="dive"; v.t=0;
      const a=Math.atan2(state.py-v.y,state.px-v.x);
      v.dvx=Math.cos(a)*430; v.dvy=Math.sin(a)*430; sWave(); }
  } else if(v.st==="dive"){
    v.x=clamp(v.x+v.dvx*dt,v.x1,v.x2); v.y+=v.dvy*dt;
    if(v.y>v.gy-40||v.y<v.top+70||v.t>1.1){ v.st="hover"; v.dive=4; }
  }
  if(state.invuln<=0&&Math.abs(state.px-v.x)<32&&Math.abs(state.py-v.y)<38)
    damage(1,sign(state.px-v.x));
}
function vigiaHit(){
  const v=state.lvl.vigia;
  v.hp--; v.flash=.15; sHitE();
  if(v.hp<=0&&!v.dead){
    v.dead=true;
    state.lvl.solids=state.lvl.solids.filter(r=>!r.vg);
    state.chips+=6; logro("vigia");
    state.notice={txt:"EL VIGÍA CAE · puerta abierta · +6 💾",t:3};
    burst(v.x,v.y,"255,120,120",26,200); burst(v.x,v.y,"200,230,255",18,150);
    sWin(); updateHUD();
  }
}
function onDeath(){
  state.running=false; sDie(); state.deaths++;
  if(state.mode==="endless"){
    const m=Math.round(state.maxUp/10);
    if(m>(rec.bestAlt||0)){ rec.bestAlt=m; lsSet("vertigo_rec",rec); }
    showInter("LA TORRE INFINITA TE ESCUPE",
      "Altura alcanzada: "+m+" m"+(m>=(rec.bestAlt||0)?" · ¡RÉCORD!":" · Récord: "+rec.bestAlt+" m"),
      "VOLVER AL MENÚ",()=>toMenu(),false);
    return;
  }
  const canLift=state.chips>=3 && state.bestFloor &&
    state.bestFloor.y < state.spawn.y - CH*0.9;
  showInter("HAS CAÍDO","¿Desde dónde retomas la escalada?",
    "⚓ PUNTO DE CONTROL (gratis)",
    ()=>{ state.hearts=state.up.maxHearts; respawn(true); state.deaths--; state.running=true; },
    false,
    canLift?{txt:"🛗 ASCENSOR — planta más alta (3 💾)",cb:()=>{
      state.chips-=3; state.hearts=state.up.maxHearts;
      state.px=state.bestFloor.x; state.py=state.bestFloor.y;
      state.vx=0;state.vy=0;state.kb=0;state.hook=null;state.wall=0;
      state.shots.length=0; state.invuln=1.4; state.energy=5;
      state.cam.y=state.py-H*.55; state.deaths--; state.deaths++;
      if(state.mode==="chase") state.shadowY=Math.max(state.shadowY,state.py+520);
      sTele(); state.running=true; updateHUD();
    }}:null);
}
function updateEnemies(dt){
  for(const e of state.lvl.enemies){
    if(e.dead) continue;
    e.flash=Math.max(0,e.flash-dt);
    if(Math.abs(e.y-state.py)>H*1.3) continue;
    if(e.type==="z") updateZombie(e,dt);
    else updateGunner(e,dt);
  }
}
function updateZombie(e,dt){
  if(Math.abs(e.y-state.py)>640) return;
  const dx=state.px-e.x, dy=state.py-(e.y-30);
  if(e.state==="patrol"){
    e.x+=e.dir*55*dt;
    if(e.x<e.x1){e.x=e.x1;e.dir=1;} if(e.x>e.x2){e.x=e.x2;e.dir=-1;}
    if(Math.abs(dx)<180 && Math.abs(dy)<60 && sign(dx)===e.dir){ e.state="chase"; sTele(); }
  } else {
    e.dir=sign(dx);
    e.x=clamp(e.x+e.dir*140*dt,e.x1,e.x2);
    if(Math.abs(dx)>320||Math.abs(dy)>110) e.state="patrol";
  }
  contact(e,e.x,e.y-30,26,52);
}
function updateGunner(e,dt){
  if(Math.abs(e.y-state.py)>640) return;
  const dx=state.px-e.x, dy=state.py-(e.y-30);
  e.cool-=dt;
  const see=Math.abs(dx)<430 && Math.abs(dy)<50;
  if(e.state==="idle"){
    if(see && e.cool<=0){ e.dir=sign(dx); e.state="aim"; e.t=0; sTele(); }
  } else if(e.state==="aim"){
    e.t+=dt; e.dir=sign(dx);
    if(!see){ e.state="idle"; }
    else if(e.t>.55){
      shootBolt(e); 
      if(e.v==="f") setTimeout(()=>{ if(!e.dead) shootBolt(e); },160);
      e.state="idle"; e.cool=1.35;
    }
  }
  contact(e,e.x,e.y-30,24,52);
}
function shootBolt(e){
  state.shots.push({x:e.x+e.dir*18,y:e.y-38,vx:e.dir*300,vy:0,from:"e",life:2.4});
  beep(480,.09,"square",.07,180);
}
function contact(e,ex,ey,ew,eh){
  const hh=halfH();
  if(Math.abs(state.px-ex)>=(PW+ew)/2 || Math.abs(state.py-ey)>=(hh*2+eh)/2) return;
  if(state.vy>140 && state.py+hh<ey+8){
    hitEnemy(e); if(!e.dead&&e.hp>0) hitEnemy(e);
    state.vy=-380; sJump(); return;
  }
  if(state.invuln<=0) damage(1,sign(state.px-ex));
}
function hitEnemy(e){
  e.hp--; e.flash=.15;
  if(e.hp<=0 && !e.dead){
    e.dead=true; state.kills++;
    state.chips++; sChip();
    burst(e.x,e.y-30,"200,230,255",14,140);
    updateHUD();
  } else sHitE();
}

/* ---------- Jefe: EL CUSTODIO ---------- */
function startBoss(){
  state.bossMode=true;
  const A=state.lvl.bossArena;
  state.boss={x:A.x2-90, y:A.gy, hp:26, maxHp:26, dir:-1,
    state:"walk", t:0, flash:0, chargeCd:2.5, orbCd:3, stompCd:5};
  sBoss(); updateHUD();
  state.notice={txt:"⚡ ENERGÍA INFINITA — ¡derriba al Custodio!", t:3};
}
function bossPhase(){ const b=state.boss; return b.hp>17?1:(b.hp>8?2:3); }
function updateBoss(dt){
  const b=state.boss, A=state.lvl.bossArena;
  b.flash=Math.max(0,b.flash-dt);
  b.t+=dt; b.chargeCd-=dt; b.orbCd-=dt; b.stompCd-=dt;
  const ph=bossPhase(), dx=state.px-b.x;
  if(b.state==="walk"){
    b.dir=sign(dx);
    b.x=clamp(b.x+b.dir*(60+ph*25)*dt, A.x1+40, A.x2-40);
    if(b.chargeCd<=0 && Math.abs(dx)>150){ b.state="tele"; b.t=0; sTele(); }
    else if(b.stompCd<=0 && Math.abs(dx)<170 && ph>=2){ b.state="stomp"; b.t=0; b.vy=-620; }
    if(b.orbCd<=0){
      state.shots.push({x:b.x+b.dir*24,y:b.y-52,vx:sign(dx)*(150+ph*25),vy:0,from:"e",ob:true,life:5});
      b.orbCd=Math.max(1.4,2.6-ph*.4);
      beep(220,.2,"sine",.1,80);
    }
  } else if(b.state==="tele"){          // telegrafía la embestida
    if(b.t>.55){ b.state="charge"; b.t=0; b.cdir=sign(dx); sWave(); }
  } else if(b.state==="charge"){
    b.x+=b.cdir*(380+ph*40)*dt;
    if(b.x<A.x1+40||b.x>A.x2-40||b.t>1.1){
      b.x=clamp(b.x,A.x1+40,A.x2-40);
      b.state="walk"; b.chargeCd=2.6-ph*.3;
    }
  } else if(b.state==="stomp"){
    b.vy+=GRAV*dt; b.y+=b.vy*dt;
    if(b.y>=A.gy){
      b.y=A.gy; b.state="walk"; b.stompCd=5;
      sWave();
      state.shots.push({x:b.x-30,y:A.gy-14,vx:-260,vy:0,from:"e",wave:true,life:2});
      state.shots.push({x:b.x+30,y:A.gy-14,vx:260,vy:0,from:"e",wave:true,life:2});
      burst(b.x,A.gy,"255,200,140",16,150);
    }
  }
  // contacto con el jefe
  const hh=halfH();
  if(state.invuln<=0 && Math.abs(state.px-b.x)<40 && Math.abs(state.py-(b.y-46))<(hh+52)/1){
    if(state.vy>140 && state.py+hh<b.y-60){ bossHit(2); state.vy=-400; sJump(); }
    else damage(1,sign(state.px-b.x));
  }
}
function bossHit(n){
  const b=state.boss;
  b.hp-=n; b.flash=.15; sHitE();
  if(b.hp<=0){
    burst(b.x,b.y-50,"255,190,150",40,220);
    burst(b.x,b.y-50,"180,230,255",30,160);
    state.boss=null; state.running=false;
    rec.wins++; lsDel("vertigo_save");
    let msg=`La Torre Ossia es tuya. Chips: ${state.chips} · Derribos: ${state.kills} · Caídas: ${state.deaths}.`;
    if(state.mode==="timer"){
      const t=state.runT;
      const medal=t<=600?"🥇 ORO":(t<=900?"🥈 PLATA":"🥉 BRONCE");
      if(!rec.bestTime||t<rec.bestTime) rec.bestTime=t;
      if(t<=600) logro("oro");
      msg="Tiempo: "+fmtT(t)+" · "+medal+
          (rec.bestTime?" · mejor: "+fmtT(rec.bestTime):"");
    } else if(state.mode==="chase"){
      logro("sombra");
      msg="Le ganaste la carrera a la noche. "+msg;
    } else {
      logro("cumbre");
      if(!state.bought) logro("espartano");
    }
    lsSet("vertigo_rec",rec);
    sWin(); setTimeout(sWin,500);
    showInter("EL CUSTODIO HA CAÍDO",msg,"VOLVER AL MENÚ",()=>toMenu(),false);
  }
  updateHUD();
}

/* ---------- Proyectiles ---------- */
function updateShots(dt){
  for(let i=state.shots.length-1;i>=0;i--){
    const s=state.shots[i];
    s.x+=s.vx*dt; s.y+=s.vy*dt; s.life-=dt;
    let del=s.life<=0;
    if(!del && !s.ob && !s.wave){
      for(const r of state.lvl.solids)
        if(s.x>r.x&&s.x<r.x+r.w&&s.y>r.y&&s.y<r.y+r.h){ del=true;
          burst(s.x,s.y,"200,210,230",4,60); break; }
    }
    if(!del && s.from==="p"){
      for(const e of state.lvl.enemies){
        if(e.dead) continue;
        if(Math.abs(s.x-e.x)<18 && Math.abs(s.y-(e.y-30))<30){
          hitEnemy(e); del=true; break;
        }
      }
      if(!del && state.boss){
        const b=state.boss;
        if(Math.abs(s.x-b.x)<30 && Math.abs(s.y-(b.y-46))<44){ bossHit(1); del=true; }
      }
      if(!del && state.lvl.vigia && !state.lvl.vigia.dead){
        const v=state.lvl.vigia;
        if(Math.abs(s.x-v.x)<28 && Math.abs(s.y-v.y)<26){ vigiaHit(); del=true; }
      }
    }
    if(!del && s.from==="e"){
      const hh=halfH();
      const pad=s.ob?9:(s.wave?4:4);
      if(state.invuln<=0 &&
         Math.abs(s.x-state.px)<PW/2+pad && Math.abs(s.y-state.py)<hh+pad){
        damage(1,sign(s.vx)); del=true;
      }
    }
    if(del) state.shots.splice(i,1);
  }
}

/* ---------- Dibujo ---------- */
function drawSprite(key,x,y,h,flip){
  const im=IMG[key]; if(!im||!im.complete) return;
  const w=h*im.width/im.height;
  ctx.save();
  ctx.translate(x,y);
  if(flip) ctx.scale(-1,1);
  ctx.drawImage(im,-w/2,-h,w,h);
  ctx.restore();
}
function draw(){
  const cam=state.cam;
  ctx.clearRect(0,0,W,H);
  drawInterior();
  ctx.save(); ctx.translate(-cam.x,-cam.y);
  drawWindowsPass();
  // sólidos
  for(const s of state.lvl.solids){
    if(s.y+s.h<cam.y-40||s.y>cam.y+H+40) continue;
    const ck=state.lvl.chunks[chunkAt(s.y+2)];
    const pal=state.bossMode&&ck&&ck.type==="boss"?ROOF:SECTORS[ck?ck.sector:0];
    ctx.fillStyle=pal.panel;
    ctx.fillRect(s.x,s.y,s.w,s.h);
    ctx.fillStyle="rgba(255,255,255,.07)";
    ctx.fillRect(s.x,s.y,s.w,4);
    ctx.fillStyle="rgba(0,0,0,.25)";
    for(let tx=s.x+8;tx<s.x+s.w-8;tx+=42) ctx.fillRect(tx,s.y+8,2,Math.max(0,s.h-16));
  }
  // vapor
  for(const st of state.lvl.steams){
    if(Math.abs(st.y-cam.y-H/2)>H) continue;
    const cy2=(state.t+st.ph)%2.6;
    ctx.fillStyle="#3a4155"; ctx.fillRect(st.x-9,st.y-8,18,8);
    if(cy2>1.0&&cy2<1.45){
      ctx.fillStyle="rgba(220,225,240,.4)";
      ctx.beginPath(); ctx.arc(st.x,st.y-14,4+Math.random()*3,0,7); ctx.fill();
    } else if(cy2>1.45&&cy2<2.25){
      const g=ctx.createLinearGradient(0,st.y,0,st.y-80);
      g.addColorStop(0,"rgba(235,238,250,.85)"); g.addColorStop(1,"rgba(235,238,250,0)");
      ctx.fillStyle=g; ctx.fillRect(st.x-10,st.y-80,20,80);
    }
  }
  // anclajes de cuerda
  for(const a of state.lvl.anchors){
    if(Math.abs(a.y-cam.y-H/2)>H) continue;
    const near=Math.hypot(a.x-state.px,a.y-state.py)<310 && a.y<state.py-20;
    const r=8+(near?Math.sin(state.t*6)*2+2:0);
    const g=ctx.createRadialGradient(a.x,a.y,2,a.x,a.y,r*2.4);
    g.addColorStop(0,"rgba(255,215,120,.55)"); g.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(a.x,a.y,r*2.4,0,7); ctx.fill();
    ctx.strokeStyle=near?"#ffe6a8":"#d9b566"; ctx.lineWidth=3;
    ctx.beginPath(); ctx.arc(a.x,a.y,r,0,7); ctx.stroke();
  }
  // chips
  for(const c of state.lvl.chips){
    if(c.got||Math.abs(c.y-cam.y-H/2)>H) continue;
    const cy2=c.y+Math.sin(state.t*2+c.x)*5;
    ctx.fillStyle="#8affd0";
    ctx.save(); ctx.translate(c.x,cy2); ctx.rotate(state.t*1.6);
    ctx.fillRect(-6,-6,12,12);
    ctx.fillStyle="#0d1f18"; ctx.fillRect(-3,-3,6,6);
    ctx.restore();
  }
  // terminales
  for(const tm of state.lvl.terminals){
    if(Math.abs(tm.y-cam.y-H/2)>H) continue;
    ctx.fillStyle=tm.done?"#1d4d38":"#333a55";
    ctx.fillRect(tm.x-16,tm.y-52,32,52);
    ctx.fillStyle=tm.done?"#8affd0":"#ffd75e";
    ctx.fillRect(tm.x-10,tm.y-44,20,14);
    if(!tm.done){
      const g=ctx.createRadialGradient(tm.x,tm.y-30,4,tm.x,tm.y-30,34);
      g.addColorStop(0,"rgba(255,215,94,.3)"); g.addColorStop(1,"rgba(0,0,0,0)");
      ctx.fillStyle=g; ctx.beginPath(); ctx.arc(tm.x,tm.y-30,34,0,7); ctx.fill();
    }
  }
  drawHazardsPass();
  // enemigos
  for(const e of state.lvl.enemies){
    if(e.dead||Math.abs(e.y-cam.y-H/2)>H) continue;
    drawEnemy(e);
  }
  if(state.boss) drawBossSpr();
  // proyectiles
  for(const s of state.shots){
    if(s.from==="p"){
      ctx.fillStyle="#9fe8ff";
      ctx.beginPath(); ctx.arc(s.x,s.y,4,0,7); ctx.fill();
      ctx.fillStyle="rgba(120,220,255,.35)";
      ctx.beginPath(); ctx.arc(s.x,s.y,8,0,7); ctx.fill();
    } else if(s.ob){
      const g=ctx.createRadialGradient(s.x,s.y,2,s.x,s.y,15);
      g.addColorStop(0,"#ff9fb4"); g.addColorStop(1,"rgba(255,90,130,0)");
      ctx.fillStyle=g; ctx.beginPath(); ctx.arc(s.x,s.y,15,0,7); ctx.fill();
    } else if(s.wave){
      ctx.fillStyle="rgba(255,190,120,.8)";
      ctx.fillRect(s.x-10,s.y-8,20,14);
    } else {
      ctx.strokeStyle="#ffd75e"; ctx.lineWidth=2.5; ctx.lineCap="round";
      ctx.beginPath(); ctx.moveTo(s.x-8*sign(s.vx),s.y); ctx.lineTo(s.x+7*sign(s.vx),s.y); ctx.stroke();
    }
  }
  for(const q of state.parts){
    const a=clamp(q.life/q.max,0,1);
    ctx.fillStyle=`rgba(${q.color},${a})`;
    ctx.beginPath(); ctx.arc(q.x,q.y,2.4,0,7); ctx.fill();
  }
  if(state.hook){
    ctx.strokeStyle="rgba(255,220,150,.9)"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.moveTo(state.px,state.py-10);
    ctx.lineTo(state.hook.ax,state.hook.ay); ctx.stroke();
  }
  if(state.invuln<=0||Math.floor(state.t*14)%2===0) drawHero();
  drawShadow();
  ctx.restore();
  drawMeters();
  if(state.boss) drawBossBar();
  if(state.notice&&state.notice.t>0){
    ctx.fillStyle="rgba(232,230,221,"+Math.min(1,state.notice.t)+")";
    ctx.font="15px Georgia"; ctx.textAlign="center";
    ctx.fillText(state.notice.txt,W/2,H*.2);
  }
  const vg=ctx.createRadialGradient(W/2,H/2,H*.45,W/2,H/2,H);
  vg.addColorStop(0,"rgba(0,0,0,0)"); vg.addColorStop(1,"rgba(0,0,0,.5)");
  ctx.fillStyle=vg; ctx.fillRect(0,0,W,H);
}
function drawWindowsPass(){
  const cam=state.cam, lvl=state.lvl;
  for(let ci=0;ci<lvl.chunks.length;ci++){
    const c=lvl.chunks[ci];
    if(c.bot<cam.y-40||c.top>cam.y+H+40) continue;
    if((c.type==="office"||c.type==="check"||c.type==="summit")&&c.sector>=2)
      drawWindow(TW-238,c.top+140,132,176,ci);
    if(c.type==="summit") drawWindow(WALL+70,c.top+140,132,176,ci+7);
  }
}
function drawWindow(x,y,w,h,ci){
  const cam=state.cam;
  const r=clamp(1-y/(state.lvl.totalH||10000),0,1);
  ctx.fillStyle="#0b0f1c"; ctx.fillRect(x-6,y-6,w+12,h+12);
  const g=ctx.createLinearGradient(0,y,0,y+h);
  const topC=r>.66?"#2b1e52":(r>.33?"#141a3e":"#0a1024");
  g.addColorStop(0,topC); g.addColorStop(1,"#05070c");
  ctx.fillStyle=g; ctx.fillRect(x,y,w,h);
  ctx.save(); ctx.beginPath(); ctx.rect(x,y,w,h); ctx.clip();
  for(let k=0;k<14;k++){
    ctx.fillStyle="rgba(255,255,255,"+(.2+((k+ci)%3)*.15)+")";
    ctx.fillRect(x+((ci*37+k*53)%w), y+((ci*91+k*71)%h),2,2);
  }
  if(r>.6){
    ctx.fillStyle="rgba(240,240,255,.85)";
    ctx.beginPath(); ctx.arc(x+w-30,y+26,12,0,7); ctx.fill();
    ctx.fillStyle=topC;
    ctx.beginPath(); ctx.arc(x+w-35,y+22,10,0,7); ctx.fill();
  }
  const oy=(cam.y*.14)%46;
  for(let k=0;k<5;k++){
    const bw=18+((ci+k)*29%26), bx=x+((k*61+ci*23)%(w-14));
    const bh2=30+((ci*13+k*47)%60);
    ctx.fillStyle="rgba(8,10,20,.92)";
    ctx.fillRect(bx,y+h-bh2+oy,bw,bh2+50);
    ctx.fillStyle="rgba(255,220,140,.45)";
    for(let wy=y+h-bh2+oy+6;wy<y+h;wy+=13) ctx.fillRect(bx+4,wy,3,4);
  }
  ctx.restore();
  ctx.fillStyle="rgba(160,200,255,.05)"; ctx.fillRect(x,y,w,h);
  ctx.strokeStyle="rgba(120,150,200,.35)"; ctx.lineWidth=2;
  ctx.strokeRect(x,y,w,h);
  ctx.beginPath(); ctx.moveTo(x+w/2,y); ctx.lineTo(x+w/2,y+h);
  ctx.moveTo(x,y+h/2); ctx.lineTo(x+w,y+h/2); ctx.stroke();
}
function drawHazardsPass(){
  const cam=state.cam, lvl=state.lvl;
  for(const z of lvl.zaps){
    if(z.y<cam.y-40||z.y>cam.y+H+40) continue;
    const u=((state.t+z.ph)%2.2)/2.2;
    const sx=z.x1+(z.x2-z.x1)*(u<.5?u*2:2-u*2);
    ctx.strokeStyle="rgba(255,230,120,.25)"; ctx.lineWidth=2;
    ctx.beginPath(); ctx.moveTo(z.x1,z.y-2); ctx.lineTo(z.x2,z.y-2); ctx.stroke();
    const g=ctx.createRadialGradient(sx,z.y-4,1,sx,z.y-4,14);
    g.addColorStop(0,"rgba(255,240,160,.95)"); g.addColorStop(1,"rgba(255,200,60,0)");
    ctx.fillStyle=g; ctx.beginPath(); ctx.arc(sx,z.y-4,14,0,7); ctx.fill();
    ctx.strokeStyle="#fff3c0"; ctx.lineWidth=1.5;
    ctx.beginPath();
    ctx.moveTo(sx-6,z.y-2); ctx.lineTo(sx-2,z.y-10); ctx.lineTo(sx+2,z.y-4); ctx.lineTo(sx+6,z.y-12);
    ctx.stroke();
  }
  for(const li of lvl.lights){
    if(li.y<cam.y-60||li.y>cam.y+H+380) continue;
    const ang=Math.sin(state.t*.55+li.ph)*.55;
    const len=330, hw=26+len*.12;
    const bx=li.x+Math.tan(ang)*len;
    ctx.fillStyle=li.hit?"rgba(255,120,110,.17)":"rgba(255,235,170,.12)";
    ctx.beginPath(); ctx.moveTo(li.x,li.y);
    ctx.lineTo(bx-hw,li.y+len); ctx.lineTo(bx+hw,li.y+len);
    ctx.closePath(); ctx.fill();
    ctx.fillStyle="#39405c"; ctx.fillRect(li.x-10,li.y-8,20,12);
    ctx.fillStyle=li.hit?"#ff8f86":"#ffe9a8";
    ctx.beginPath(); ctx.arc(li.x,li.y+4,5,0,7); ctx.fill();
  }
  for(const cv2 of lvl.civs){
    if(cv2.saved||cv2.y<cam.y-60||cv2.y>cam.y+H+60) continue;
    drawSprite(cv2.v+"_idle",cv2.x,cv2.y,58,cv2.x>TW/2);
    ctx.fillStyle="#8affd0"; ctx.font="bold 13px Georgia"; ctx.textAlign="center";
    ctx.fillText("¡AYUDA!",cv2.x,cv2.y-72+Math.sin(state.t*3)*3);
  }
  for(let ci=0;ci<lvl.chunks.length;ci++){
    const c=lvl.chunks[ci];
    if(c.sector!==3||c.type==="check"||c.type==="boss") continue;
    if(c.bot<cam.y-40||c.top>cam.y+H+40) continue;
    const wc=(state.t+ci*1.9)%7;
    if(wc>1.2&&wc<2.9){
      const d2=(ci%2?1:-1), a=wc<1.5?.14:.3;
      ctx.strokeStyle="rgba(220,230,255,"+a+")"; ctx.lineWidth=1.5;
      for(let k=0;k<7;k++){
        const per=CH-80, perx=TW-2*WALL-40;
        const yy=c.top+40+(((k*67+Math.floor(state.t*160)*d2)%per)+per)%per;
        const xx=WALL+20+(((k*131+Math.floor(state.t*260)*d2)%perx)+perx)%perx;
        ctx.beginPath(); ctx.moveTo(xx,yy); ctx.lineTo(xx+34*d2,yy+3); ctx.stroke();
      }
    }
  }
  if(lvl.summit){
    const smt=lvl.summit;
    ctx.fillStyle="#c9b28a"; ctx.fillRect(smt.x-3,smt.y-120,6,120);
    ctx.fillStyle="#ffd75e";
    ctx.beginPath(); ctx.moveTo(smt.x+3,smt.y-118);
    ctx.lineTo(smt.x+58+Math.sin(state.t*4)*5,smt.y-106);
    ctx.lineTo(smt.x+3,smt.y-92); ctx.closePath(); ctx.fill();
    const g2=ctx.createRadialGradient(smt.x,smt.y-60,10,smt.x,smt.y-60,90);
    g2.addColorStop(0,"rgba(255,220,120,.25)"); g2.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g2; ctx.beginPath(); ctx.arc(smt.x,smt.y-60,90,0,7); ctx.fill();
  }
  if(lvl.vigia&&!lvl.vigia.dead) drawVigia();
}
function drawVigia(){
  const v=state.lvl.vigia;
  ctx.save(); ctx.translate(v.x,v.y);
  ctx.fillStyle="#2a3350";
  ctx.beginPath(); ctx.ellipse(0,0,30,12,0,0,7); ctx.fill();
  ctx.fillStyle="#3c4a72";
  ctx.beginPath(); ctx.arc(0,-8,14,Math.PI,0); ctx.fill();
  ctx.fillStyle=v.st==="tele"?"#ff5b7d":(v.st==="dive"?"#ff8f60":"#ffd75e");
  ctx.beginPath(); ctx.arc(Math.sin(state.t*4)*8,-8,4.5,0,7); ctx.fill();
  ctx.strokeStyle="rgba(180,200,255,.7)"; ctx.lineWidth=2;
  const r=Math.sin(state.t*30)>0?2:-2;
  ctx.beginPath(); ctx.moveTo(-34,-2-r); ctx.lineTo(-22,-2+r);
  ctx.moveTo(22,-2+r); ctx.lineTo(34,-2-r); ctx.stroke();
  if(v.flash>0){ ctx.fillStyle="rgba(255,255,255,.5)";
    ctx.beginPath(); ctx.arc(0,-4,26,0,7); ctx.fill(); }
  if(v.st==="tele"){ ctx.fillStyle="#ff5b7d"; ctx.font="bold 18px Georgia";
    ctx.textAlign="center"; ctx.fillText("!",0,-36); }
  ctx.restore();
  ctx.fillStyle="rgba(0,0,0,.5)"; ctx.fillRect(v.x-26,v.y-38,52,5);
  ctx.fillStyle="#ff8f86"; ctx.fillRect(v.x-26,v.y-38,52*v.hp/v.maxHp,5);
}
function drawShadow(){
  if(state.mode!=="chase") return;
  const cam=state.cam, top=state.shadowY;
  if(top>cam.y+H+80) return;
  const g=ctx.createLinearGradient(0,top-70,0,top+140);
  g.addColorStop(0,"rgba(20,8,40,0)"); g.addColorStop(1,"rgba(12,4,26,.97)");
  ctx.fillStyle=g;
  ctx.beginPath();
  ctx.moveTo(-100,top+140);
  for(let x=-100;x<=TW+100;x+=24)
    ctx.lineTo(x,top+Math.sin(x*.045+state.t*3)*12+Math.sin(x*.013-state.t*1.7)*7);
  ctx.lineTo(TW+100,top+140);
  ctx.closePath(); ctx.fill();
  ctx.fillStyle="rgba(8,2,18,.98)";
  ctx.fillRect(-100,top+120,TW+200,Math.max(80,cam.y+H-top));
  for(let k=0;k<4;k++){
    if(Math.sin(state.t*2+k*2)<=.2) continue;
    const ex=((k*197+Math.floor(state.t/2)*61)%TW);
    ctx.fillStyle="rgba(200,120,255,.8)";
    ctx.fillRect(ex-5,top+60+k*17,4,3); ctx.fillRect(ex+3,top+60+k*17,4,3);
  }
}
function drawMeters(){
  const cur=Math.max(0,Math.round((state.lvl.baseY-state.py)/10));
  ctx.font="13px Georgia"; ctx.textAlign="left";
  ctx.fillStyle="rgba(232,230,221,.9)";
  ctx.fillText("⬆ "+cur+" m",12,H-14);
  if(state.mode==="timer"){
    ctx.textAlign="center"; ctx.font="bold 20px Georgia";
    ctx.fillStyle="#ffd75e";
    ctx.fillText(fmtT(state.runT),W/2,30);
  } else if(state.mode==="chase"&&!state.bossMode){
    const gap=Math.max(0,Math.round((state.shadowY-state.py)/10));
    ctx.textAlign="center"; ctx.font="bold 16px Georgia";
    ctx.fillStyle=gap<25?"#ff8f86":"#c9a0ff";
    ctx.fillText("🌑 a "+gap+" m",W/2,30);
    if(gap<25){
      const vg2=ctx.createRadialGradient(W/2,H/2,H*.3,W/2,H/2,H);
      vg2.addColorStop(0,"rgba(0,0,0,0)");
      vg2.addColorStop(1,"rgba(120,20,80,"+(0.25+Math.sin(state.t*6)*.12).toFixed(3)+")");
      ctx.fillStyle=vg2; ctx.fillRect(0,0,W,H);
    }
  } else if(state.mode==="endless"){
    const m=Math.max(0,Math.round(state.maxUp/10));
    ctx.textAlign="center"; ctx.font="bold 16px Georgia";
    ctx.fillStyle="#8affd0";
    ctx.fillText("♾ "+m+" m · récord "+(rec.bestAlt||0)+" m",W/2,30);
  }
}
function drawInterior(){
  const ck=state.lvl?state.lvl.chunks[chunkAt(state.py)]:null;
  const pal=state.bossMode?ROOF:(ck?SECTORS[ck.sector]:SECTORS[0]);
  const g=ctx.createLinearGradient(0,0,0,H);
  g.addColorStop(0,pal.wall); g.addColorStop(1,"#05070c");
  ctx.fillStyle=g; ctx.fillRect(0,0,W,H);
  // paneles horizontales que se desplazan con la cámara
  const off=-((state.cam?state.cam.y:0)*.5)%110;
  ctx.fillStyle="rgba(255,255,255,.03)";
  for(let y=off-110;y<H;y+=110) ctx.fillRect(0,y,W,54);
  // tuberías verticales
  ctx.fillStyle=pal.pipe; ctx.globalAlpha=.35;
  const px1=(W-TW)/2-60, px2=(W+TW)/2+30;
  if(px1>0){ ctx.fillRect(px1,0,14,H); ctx.fillRect(px2+16,0,10,H); }
  ctx.globalAlpha=1;
  // lámparas
  const loff=-((state.cam?state.cam.y:0))%CH;
  for(let y=loff-CH;y<H+CH;y+=CH){
    const g2=ctx.createRadialGradient(W/2,y+60,4,W/2,y+60,150);
    g2.addColorStop(0,`rgba(${pal.lamp},.14)`); g2.addColorStop(1,"rgba(0,0,0,0)");
    ctx.fillStyle=g2; ctx.fillRect(W/2-160,y-90,320,300);
  }
}
function heroPose(){
  if(state.hook) return "h_rope";
  if(state.wall!==0) return (Math.floor(state.animT*8)%2)?"h_cl1":"h_cl0";
  if(state.crouch) return "h_duck";
  if(!state.onGround) return state.vy<0?"h_jump":"h_fall";
  if(Math.abs(state.vx)>10) return "h_w"+(Math.floor(state.animT*10)%4);
  return "h_idle";
}
function drawHero(){
  const hh=halfH();
  const pose=heroPose();
  const hgt=state.crouch?44:64;
  const flip = state.wall!==0 ? state.wall<0 : state.face<0;
  drawSprite(pose,state.px,state.py+hh,hgt,flip);
}
function drawEnemy(e){
  if(e.type==="z"){
    const pose=(e.state==="chase"||true)?"z_w"+(Math.floor(state.t*8+e.sx)%4):"z_idle";
    drawSprite(pose,e.x,e.y,60,e.dir<0);
    if(e.state==="chase"){
      ctx.fillStyle="#ff5b5b"; ctx.font="bold 14px Georgia"; ctx.textAlign="center";
      ctx.fillText("!",e.x,e.y-68);
    }
  } else {
    const k=e.v+"_"+(e.state==="aim"?"atk":"idle");
    drawSprite(k,e.x,e.y,60,e.dir<0);
    if(e.state==="aim"){
      ctx.fillStyle="#ffd75e"; ctx.font="bold 14px Georgia"; ctx.textAlign="center";
      ctx.fillText("!",e.x,e.y-68);
    }
  }
  if(e.flash>0){
    ctx.fillStyle="rgba(255,255,255,.5)";
    ctx.beginPath(); ctx.arc(e.x,e.y-30,26,0,7); ctx.fill();
  }
}
function drawBossSpr(){
  const b=state.boss;
  let pose="r_idle";
  if(b.state==="charge") pose="r_w"+(Math.floor(state.t*14)%4);
  else if(b.state==="walk") pose="r_w"+(Math.floor(state.t*7)%4);
  else if(b.state==="tele") pose="r_atk";
  else if(b.state==="stomp") pose="r_jump";
  drawSprite(pose,b.x,b.y,96,b.dir<0||b.state==="charge"&&b.cdir<0);
  if(b.state==="tele"){
    ctx.fillStyle="#ff5b7d"; ctx.font="bold 18px Georgia"; ctx.textAlign="center";
    ctx.fillText("!",b.x,b.y-104);
  }
  if(b.flash>0){
    ctx.fillStyle="rgba(255,255,255,.5)";
    ctx.beginPath(); ctx.arc(b.x,b.y-48,44,0,7); ctx.fill();
  }
}
function drawBossBar(){
  const b=state.boss, bw=Math.min(W*.6,420), bx=(W-bw)/2, by=14;
  ctx.fillStyle="rgba(4,6,12,.7)"; ctx.fillRect(bx-4,by-4,bw+8,20);
  ctx.strokeStyle="#ff6b93"; ctx.strokeRect(bx-4,by-4,bw+8,20);
  ctx.fillStyle="#ff4d6d"; ctx.fillRect(bx,by,bw*(b.hp/b.maxHp),12);
  ctx.fillStyle="#ffd9e2"; ctx.font="10px Georgia"; ctx.textAlign="center";
  ctx.fillText("EL CUSTODIO — FASE "+bossPhase(),W/2,by+24);
}

/* ---------- Tienda ---------- */
const SHOP=[
  {name:"+1 CORAZÓN",desc:"Vida máxima (hasta 5)",cost:10,
   can:()=>state.up.maxHearts<5,buy:()=>{state.up.maxHearts++;state.hearts++;}},
  {name:"DOBLE SALTO",desc:"Un salto extra en el aire",cost:9,
   can:()=>!state.up.dbl,buy:()=>{state.up.dbl=true;}},
  {name:"DISPARO DOBLE",desc:"Cada tiro lanza dos proyectiles",cost:9,
   can:()=>!state.up.dblShot,buy:()=>{state.up.dblShot=true;}},
  {name:"BOTAS DE SIGILO",desc:"Agachado te mueves casi a plena velocidad",cost:7,
   can:()=>!state.up.slide,buy:()=>{state.up.slide=true;}},
];
function openShop(tm){
  state.running=false;
  showInter("PUNTO DE CONTROL — "+SECTORS[tm.sector].name,
    "Progreso guardado. La máquina expendedora acepta chips:",
    "SEGUIR ESCALANDO",()=>{ state.running=true; saveRun(); },true);
}
function renderShop(){
  const box=document.getElementById("vt_shopItems");
  box.innerHTML="";
  SHOP.forEach(it=>{
    const d=document.createElement("div");
    const ok=it.can(), afford=state.chips>=it.cost;
    d.className="shopIt"+((ok&&afford)?"":" off");
    d.innerHTML=`<b>${it.name}</b><span>${ok?it.desc:"YA LO TIENES"}</span><span class="cost">💾 ${it.cost}</span>`;
    d.onclick=()=>{
      if(!it.can()||state.chips<it.cost) return;
      state.chips-=it.cost; it.buy(); sBuy(); saveRun(); updateHUD(); renderShop();
    };
    box.appendChild(d);
  });
  document.getElementById("vt_bankLine").textContent=`Chips disponibles: 💾 ${state.chips}`;
}
function showInter(title,msg,btnTxt,cb,shop,alt){
  document.getElementById("vt_interTitle").textContent=title;
  document.getElementById("vt_interMsg").textContent=msg;
  document.getElementById("vt_btnNext").textContent=btnTxt;
  document.getElementById("vt_shopItems").style.display=shop?"grid":"none";
  document.getElementById("vt_bankLine").style.display=shop?"block":"none";
  if(shop) renderShop();
  const bA=document.getElementById("vt_btnAlt");
  bA.style.display=alt?"inline-block":"none";
  if(alt){ bA.textContent=alt.txt;
    bA.onclick=()=>{ document.getElementById("vt_inter").classList.remove("on"); alt.cb(); }; }
  document.getElementById("vt_inter").classList.add("on");
  document.getElementById("vt_btnNext").onclick=()=>{
    document.getElementById("vt_inter").classList.remove("on"); cb();
  };
}
function saveRun(){
  if(state.mode!=="tower") return;
  lsSet("vertigo_save",{ck:state.spawnCk, chips:state.chips, up:state.up,
    kills:state.kills, deaths:state.deaths});
}
function toMenu(){
  state.running=false; state.lvl=null; state.boss=null; state.bossMode=false;
  refreshMenu();
  document.getElementById("vt_menu").classList.add("on");
}
function refreshMenu(){
  const sv=lsGet("vertigo_save");
  document.getElementById("vt_btnCont").style.display=(sv&&sv.ck>=0)?"inline-block":"none";
  const parts=["Custodios: "+rec.wins];
  if(rec.bestTime) parts.push("⏱ mejor: "+fmtT(rec.bestTime));
  if(rec.bestAlt) parts.push("♾ récord: "+rec.bestAlt+" m");
  const nl=Object.keys(rec.logros||{}).length;
  parts.push("🏆 "+nl+"/"+LOGROS.length);
  document.getElementById("vt_recLine").textContent=parts.join(" · ");
  document.getElementById("vt_btnMute").textContent="🎵 MÚSICA: "+(MUS.on?"SÍ":"NO");
}
function launch(fromSave,mode){
  if(loaded<toLoad) return;
  document.getElementById("vt_menu").classList.remove("on");
  beep(520,.1,"triangle",.1);
  if(!fromSave && mode==="tower") lsDel("vertigo_save");
  startGame(fromSave,mode);
}
document.getElementById("vt_btnPlay").onclick=()=>launch(false,"tower");
document.getElementById("vt_btnCont").onclick=()=>launch(true,"tower");
document.getElementById("vt_btnTime").onclick=()=>launch(false,"timer");
document.getElementById("vt_btnChase").onclick=()=>launch(false,"chase");
document.getElementById("vt_btnEndless").onclick=()=>launch(false,"endless");
document.getElementById("vt_btnLogros").onclick=()=>{
  const el=document.getElementById("vt_logroList");
  el.innerHTML=LOGROS.map(l=>
    (rec.logros[l[0]]?"🏆 <b>"+l[1]+"</b>":"🔒 "+l[1])+
    " <span style='opacity:.6'>— "+l[2]+"</span>").join("<br>");
  document.getElementById("vt_logros").classList.add("on");
};
document.getElementById("vt_btnLogrosBack").onclick=()=>
  document.getElementById("vt_logros").classList.remove("on");
document.getElementById("vt_btnMute").onclick=function(){
  MUS.on=!MUS.on; lsSet("vertigo_mus",MUS.on?1:0);
  this.textContent="🎵 MÚSICA: "+(MUS.on?"SÍ":"NO");
};

/* ---------- Bucle ---------- */
let last=0;
function loop(ts){
  if(!__active) return;
  requestAnimationFrame(loop);
  const dt=Math.min(.03,(ts-last)/1000)||0; last=ts;
  const inInter=document.getElementById("vt_inter").classList.contains("on");
  if(state.running && !inInter){ step(dt); state.runT+=dt; }
  if(state.lvl) draw();
  else drawMenuBG();
}
function drawMenuBG(){
  const g=ctx.createLinearGradient(0,0,0,H);
  g.addColorStop(0,"#131a30"); g.addColorStop(1,"#05070c");
  ctx.fillStyle=g; ctx.fillRect(0,0,W,H);
  ctx.fillStyle="rgba(255,255,255,.04)";
  for(let y=(Date.now()/40)%110-110;y<H;y+=110) ctx.fillRect(0,y,W,54);
  if(loaded<toLoad){
    ctx.fillStyle="#8a93b0"; ctx.font="13px Georgia"; ctx.textAlign="center";
    ctx.fillText("Cargando sprites… "+loaded+"/"+toLoad, W/2, H-24);
  }
}
__exp.start=function(){ if(!__exp._i){ __exp._i=true; refreshMenu(); resize(); } __active=true; refreshMenu(); requestAnimationFrame(loop); };
__exp.stop=function(){ __active=false; };

return __exp;
})();


arcadeRegister("md",GameMD);
arcadeRegister("fl",GameFL);
arcadeRegister("nc",GameNC);
arcadeRegister("hm",GameHM);
arcadeRegister("c4",GameC4);
arcadeRegister("vt",GameVT);

</script>
</body>
</html>
