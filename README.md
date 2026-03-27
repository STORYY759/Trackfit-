




<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Lean Pro">
<title>Lean Pro</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
:root {
  --bg: #0a0a0a;
  --surface: #141414;
  --surface2: #1e1e1e;
  --border: rgba(255,255,255,0.07);
  --accent: #ff5c2a;
  --accent2: #ff8c5a;
  --text: #f0f0f0;
  --muted: #666;
  --green: #2dca72;
  --blue: #3a9eff;
}
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
html, body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100%;
  -webkit-text-size-adjust: 100%;
}
.header {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 12px 20px;
  padding-top: calc(12px + env(safe-area-inset-top));
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
}
.logo { font-family: 'Bebas Neue', sans-serif; font-size: 26px; letter-spacing: 2px; color: var(--accent); }
.logo span { color: var(--text); }
.streak { display: flex; align-items: center; gap: 6px; font-size: 13px; color: var(--muted); }
.streak strong { color: var(--accent2); font-size: 16px; }
main {
  max-width: 520px;
  margin: 0 auto;
  padding: 16px 14px;
  padding-bottom: calc(80px + env(safe-area-inset-bottom, 20px));
}
.section { display: none; }
.section.active { display: block; }
.card { background: var(--surface); border: 1px solid var(--border); border-radius: 14px; padding: 16px; margin-bottom: 12px; }
.card-title { font-size: 10px; font-weight: 600; letter-spacing: 1.5px; text-transform: uppercase; color: var(--muted); margin-bottom: 12px; }
.input-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.field { margin-bottom: 10px; }
.field label { display: block; font-size: 12px; color: var(--muted); margin-bottom: 5px; }
input, select {
  width: 100%;
  background: var(--surface2);
  border: 1px solid var(--border);
  border-radius: 8px;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 16px;
  padding: 10px 12px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
}
input:focus, select:focus { border-color: var(--accent); }
select { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%23666' stroke-width='1.5' fill='none'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 12px center; padding-right: 32px; }
select option { background: #1e1e1e; }
.btn { width: 100%; padding: 13px; border-radius: 10px; border: none; font-family: 'DM Sans', sans-serif; font-size: 15px; font-weight: 600; cursor: pointer; margin-top: 4px; }
.btn:active { opacity: 0.85; transform: scale(0.98); }
.btn-primary { background: var(--accent); color: white; }
.btn-secondary { background: var(--surface2); color: var(--text); border: 1px solid var(--border); }
.btn-sm { width: auto; padding: 10px 14px; font-size: 13px; border-radius: 8px; margin-top: 0; }
.stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 12px; }
.stat-card { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 14px; text-align: center; }
.stat-value { font-family: 'Bebas Neue', sans-serif; font-size: 30px; letter-spacing: 1px; color: var(--accent); line-height: 1; }
.stat-label { font-size: 10px; color: var(--muted); margin-top: 4px; text-transform: uppercase; letter-spacing: 1px; }
.progress-bar { background: var(--surface2); border-radius: 999px; height: 6px; overflow: hidden; margin-top: 8px; }
.progress-fill { height: 100%; border-radius: 999px; background: linear-gradient(90deg, var(--accent), var(--accent2)); transition: width 0.5s ease; }
.macros { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-top: 12px; }
.macro-box { background: var(--surface2); border-radius: 10px; padding: 10px; text-align: center; }
.macro-val { font-size: 17px; font-weight: 600; }
.macro-label { font-size: 10px; color: var(--muted); margin-top: 2px; text-transform: uppercase; letter-spacing: 1px; }
.macro-box.protein .macro-val { color: var(--accent); }
.macro-box.carbs .macro-val { color: var(--blue); }
.macro-box.fat .macro-val { color: #f5c518; }
.workout-item { display: flex; align-items: center; justify-content: space-between; padding: 10px 12px; background: var(--surface2); border-radius: 8px; margin-bottom: 6px; }
.ex-name { font-weight: 500; font-size: 14px; }
.ex-detail { color: var(--muted); font-size: 12px; margin-top: 2px; }
.delete-btn { background: none; border: none; color: var(--muted); cursor: pointer; font-size: 22px; padding: 0 4px; line-height: 1; }
.plan-item { display: flex; align-items: center; gap: 12px; padding: 12px 0; border-bottom: 1px solid var(--border); }
.plan-item:last-child { border-bottom: none; }
.plan-icon { width: 36px; height: 36px; border-radius: 10px; background: rgba(255,92,42,0.1); display: flex; align-items: center; justify-content: center; font-size: 18px; flex-shrink: 0; }
.plan-text { font-size: 14px; font-weight: 500; }
.plan-sub { font-size: 12px; color: var(--muted); margin-top: 2px; }
.ai-result { background: rgba(255,92,42,0.08); border: 1px solid rgba(255,92,42,0.2); border-radius: 10px; padding: 12px; margin-top: 10px; font-size: 14px; line-height: 1.6; display: none; }
.ai-result.visible { display: block; }
.ai-loader { display: none; text-align: center; padding: 14px; color: var(--muted); font-size: 13px; }
.ai-loader.visible { display: block; }
.habit-row { display: flex; align-items: center; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
.habit-row:last-child { border-bottom: none; }
.habit-name { font-size: 13px; flex: 1; padding-right: 8px; }
.habit-dots { display: flex; gap: 4px; }
.habit-dot { width: 24px; height: 24px; border-radius: 50%; border: 1.5px solid var(--border); background: var(--surface2); cursor: pointer; transition: background 0.15s; }
.habit-dot.done { background: var(--green); border-color: var(--green); }
.bottom-nav {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  background: rgba(14,14,14,0.97);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-top: 1px solid var(--border);
  display: flex;
  z-index: 200;
  padding-bottom: env(safe-area-inset-bottom, 0px);
}
.nav-btn {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 3px;
  padding: 10px 2px;
  background: none;
  border: none;
  color: var(--muted);
  font-family: 'DM Sans', sans-serif;
  font-size: 10px;
  font-weight: 500;
  cursor: pointer;
  min-height: 56px;
  -webkit-tap-highlight-color: transparent;
  transition: color 0.15s;
}
.nav-icon { font-size: 20px; line-height: 1; display: block; }
.nav-btn.active { color: var(--accent); }
.toast {
  position: fixed;
  bottom: calc(70px + env(safe-area-inset-bottom, 0px));
  left: 50%;
  transform: translateX(-50%) translateY(60px);
  background: var(--surface);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 10px;
  padding: 10px 18px;
  font-size: 13px;
  font-weight: 500;
  z-index: 999;
  transition: transform 0.3s ease, opacity 0.3s;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
}
.toast.show { transform: translateX(-50%) translateY(0); opacity: 1; }
</style>
</head>
<body>

<div class="header">
  <div class="logo">LEAN<span>PRO</span></div>
  <div class="streak">🔥 <strong id="streakVal">0</strong> j</div>
</div>

<main>

<!-- DASHBOARD -->
<div class="section active" id="sec-dashboard">
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-value" id="d-tdee">—</div><div class="stat-label">TDEE kcal</div></div>
    <div class="stat-card"><div class="stat-value" id="d-target">—</div><div class="stat-label">Objectif kcal</div></div>
    <div class="stat-card"><div class="stat-value" id="d-weight">—</div><div class="stat-label">Poids actuel</div></div>
    <div class="stat-card"><div class="stat-value" id="d-bf">—</div><div class="stat-label">Body fat %</div></div>
  </div>
  <div class="card">
    <div class="card-title">Profil & Calcul TDEE</div>
    <div class="input-row">
      <div class="field"><label>Poids (kg)</label><input id="poids" type="number" inputmode="decimal" placeholder="80"></div>
      <div class="field"><label>Body fat %</label><input id="bodyfat" type="number" inputmode="decimal" placeholder="18"></div>
    </div>
    <div class="input-row">
      <div class="field"><label>Pas / jour</label><input id="steps" type="number" inputmode="numeric" placeholder="8000"></div>
      <div class="field"><label>Âge</label><input id="age" type="number" inputmode="numeric" placeholder="25"></div>
    </div>
    <div class="field">
      <label>Objectif</label>
      <select id="goal">
        <option value="-500">Perte rapide (–500 kcal)</option>
        <option value="-300">Perte lente (–300 kcal)</option>
        <option value="0">Maintien</option>
        <option value="300">Prise de masse (+300 kcal)</option>
      </select>
    </div>
    <button class="btn btn-primary" onclick="calculate()">Calculer mon TDEE</button>
    <div id="result" style="margin-top:12px;"></div>
  </div>
</div>

<!-- CALORIES -->
<div class="section" id="sec-calories">
  <div class="card">
    <div class="card-title">Analyser un repas avec l'IA</div>
    <div class="field"><label>Décrivez votre repas</label><input id="meal" placeholder="Ex: 150g riz, 200g poulet, salade..."></div>
    <button class="btn btn-primary" onclick="analyzeMeal()">Analyser avec l'IA</button>
    <div class="ai-loader" id="mealLoader">Analyse en cours…</div>
    <div class="ai-result" id="mealResult"></div>
  </div>
  <div class="card">
    <div class="card-title">Journal du jour</div>
    <div id="mealLog" style="margin-bottom:12px;"></div>
    <div style="display:flex;gap:8px;">
      <input id="quickFood" placeholder="Aliment" style="flex:1;font-size:14px;">
      <input id="quickCal" type="number" inputmode="numeric" placeholder="kcal" style="width:75px;font-size:14px;">
      <button class="btn btn-secondary btn-sm" onclick="addQuickMeal()">+</button>
    </div>
    <div style="margin-top:14px;padding-top:12px;border-top:1px solid var(--border);">
      <div style="display:flex;justify-content:space-between;font-size:13px;">
        <span style="color:var(--muted);">Total consommé</span>
        <strong id="totalCal">0 kcal</strong>
      </div>
      <div class="progress-bar"><div class="progress-fill" id="calProgress" style="width:0%;"></div></div>
      <div style="font-size:11px;color:var(--muted);margin-top:5px;" id="calRemain">— kcal restantes</div>
    </div>
  </div>
</div>

<!-- MUSCU -->
<div class="section" id="sec-muscu">
  <div class="card">
    <div class="card-title">Ajouter une série</div>
    <div class="field">
      <label>Exercice</label>
      <select id="exerciseSelect" onchange="toggleCustomEx(this)">
        <option value="">-- Choisir --</option>
        <optgroup label="Poitrine"><option>Bench Press</option><option>Incline Press</option><option>Dips</option></optgroup>
        <optgroup label="Dos"><option>Deadlift</option><option>Pull-up</option><option>Row barbell</option></optgroup>
        <optgroup label="Épaules"><option>Overhead Press</option><option>Lateral Raise</option></optgroup>
        <optgroup label="Jambes"><option>Squat</option><option>Romanian Deadlift</option><option>Leg Press</option></optgroup>
        <optgroup label="Bras"><option>Curl Barbell</option><option>Tricep Pushdown</option></optgroup>
        <option value="custom">Autre (saisir)</option>
      </select>
    </div>
    <div id="customExField" style="display:none;" class="field">
      <label>Nom de l'exercice</label><input id="exercise" placeholder="Nom de l'exercice">
    </div>
    <div class="input-row">
      <div class="field"><label>Séries</label><input id="sets" type="number" inputmode="numeric" placeholder="3"></div>
      <div class="field"><label>Reps</label><input id="reps" type="number" inputmode="numeric" placeholder="10"></div>
    </div>
    <div class="input-row">
      <div class="field"><label>Poids (kg)</label><input id="weightLift" type="number" inputmode="decimal" placeholder="60"></div>
      <div class="field"><label>RIR</label>
        <select id="rir">
          <option value="0">0 – Échec</option><option value="1">1 – Proche</option>
          <option value="2" selected>2 – Normal</option><option value="3">3 – Facile</option>
        </select>
      </div>
    </div>
    <button class="btn btn-primary" onclick="addWorkout()">Ajouter la série</button>
  </div>
  <div class="card">
    <div class="card-title">Séances du jour</div>
    <div id="workoutList"></div>
    <div id="emptyWorkout" style="text-align:center;padding:20px;color:var(--muted);font-size:13px;">Aucun exercice enregistré</div>
    <div id="volumeInfo" style="display:none;margin-top:10px;padding-top:10px;border-top:1px solid var(--border);">
      <div style="display:flex;justify-content:space-between;font-size:13px;">
        <span style="color:var(--muted);">Volume total</span><strong id="totalVolume">0 kg</strong>
      </div>
    </div>
  </div>
</div>

<!-- POIDS -->
<div class="section" id="sec-poids">
  <div class="card">
    <div class="card-title">Ajouter une mesure</div>
    <div class="input-row">
      <div class="field"><label>Poids (kg)</label><input id="newWeight" type="number" inputmode="decimal" placeholder="80.5"></div>
      <div class="field"><label>Body fat % (opt.)</label><input id="newBF" type="number" inputmode="decimal" placeholder="18"></div>
    </div>
    <button class="btn btn-primary" onclick="addWeight()">Enregistrer</button>
  </div>
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-value" id="wCurrent">—</div><div class="stat-label">Poids actuel</div></div>
    <div class="stat-card"><div class="stat-value" id="wChange" style="font-size:22px;">—</div><div class="stat-label">Évolution</div></div>
  </div>
  <div class="card">
    <div class="card-title">Courbe de poids</div>
    <canvas id="chart" style="max-height:200px;"></canvas>
  </div>
  <div class="card">
    <div class="card-title">Historique</div>
    <div id="weightHistory"></div>
  </div>
</div>

<!-- HABITUDES -->
<div class="section" id="sec-habitudes">
  <div class="card">
    <div class="card-title">Habitudes de la semaine</div>
    <div id="habitTracker"></div>
  </div>
  <div class="card">
    <div class="card-title">Score hebdomadaire</div>
    <div style="display:flex;align-items:center;gap:14px;">
      <div style="font-family:'Bebas Neue';font-size:48px;color:var(--accent);line-height:1;" id="habitScore">0%</div>
      <div style="flex:1;">
        <div style="font-size:13px;" id="habitMsg">Commencez à cocher !</div>
        <div class="progress-bar" style="margin-top:8px;"><div class="progress-fill" id="habitProgress" style="width:0%;"></div></div>
      </div>
    </div>
  </div>
</div>

<!-- PLAN -->
<div class="section" id="sec-plan">
  <div class="card">
    <div class="card-title">Plan hebdomadaire</div>
    <div class="plan-item"><div class="plan-icon">🏋️</div><div><div class="plan-text">Musculation</div><div class="plan-sub">3× / semaine — Lun, Mer, Ven</div></div></div>
    <div class="plan-item"><div class="plan-icon">🏃</div><div><div class="plan-text">Cardio LISS</div><div class="plan-sub">2× / semaine — Mar, Sam (30–40 min)</div></div></div>
    <div class="plan-item"><div class="plan-icon">🚶</div><div><div class="plan-text">Marche active</div><div class="plan-sub">8 000+ pas / jour</div></div></div>
    <div class="plan-item"><div class="plan-icon">😴</div><div><div class="plan-text">Sommeil</div><div class="plan-sub">7h30 minimum — heure fixe</div></div></div>
    <div class="plan-item"><div class="plan-icon">💧</div><div><div class="plan-text">Hydratation</div><div class="plan-sub">35 ml × kg de poids corporel</div></div></div>
    <button class="btn btn-primary" style="margin-top:14px;" onclick="generateAIPlan()">Personnaliser avec l'IA ↗</button>
    <div class="ai-loader" id="planLoader">Génération en cours…</div>
    <div class="ai-result" id="aiPlanResult"></div>
  </div>
  <div class="card">
    <div class="card-title">Récupération</div>
    <div class="plan-item"><div class="plan-icon">🧘</div><div><div class="plan-text">Stretching post-séance</div><div class="plan-sub">10 min après chaque muscu</div></div></div>
    <div class="plan-item"><div class="plan-icon">🧊</div><div><div class="plan-text">Douche froide</div><div class="plan-sub">2 min post-cardio</div></div></div>
    <div class="plan-item"><div class="plan-icon">🍗</div><div><div class="plan-text">Repas post-entraînement</div><div class="plan-sub">Protéines + glucides en 60 min</div></div></div>
  </div>
</div>

</main>

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <button class="nav-btn active" id="btn-dashboard" onclick="switchTab('dashboard','btn-dashboard')">
    <span class="nav-icon">🏠</span>Accueil
  </button>
  <button class="nav-btn" id="btn-calories" onclick="switchTab('calories','btn-calories')">
    <span class="nav-icon">🍽️</span>Calories
  </button>
  <button class="nav-btn" id="btn-muscu" onclick="switchTab('muscu','btn-muscu')">
    <span class="nav-icon">🏋️</span>Muscu
  </button>
  <button class="nav-btn" id="btn-poids" onclick="switchTab('poids','btn-poids')">
    <span class="nav-icon">📊</span>Poids
  </button>
  <button class="nav-btn" id="btn-habitudes" onclick="switchTab('habitudes','btn-habitudes')">
    <span class="nav-icon">✅</span>Habits
  </button>
  <button class="nav-btn" id="btn-plan" onclick="switchTab('plan','btn-plan')">
    <span class="nav-icon">🎯</span>Plan
  </button>
</nav>

<div class="toast" id="toast"></div>

<script>
var weights = [], workouts = [], mealLog = [], habits = [], streak = 0, chart = null;
try { weights = JSON.parse(localStorage.getItem("lp_weights")) || []; } catch(e){}
try { workouts = JSON.parse(localStorage.getItem("lp_workouts")) || []; } catch(e){}
try { mealLog = JSON.parse(localStorage.getItem("lp_meals")) || []; } catch(e){}
try { habits = JSON.parse(localStorage.getItem("lp_habits")) || initHabits(); } catch(e){ habits = initHabits(); }
try { streak = parseInt(localStorage.getItem("lp_streak")) || 0; } catch(e){}

function initHabits() {
  return ["Musculation","Cardio","8000 pas","Sommeil 7h+","Eau suffisante","Pas de junk food"]
    .map(function(n){ return { name:n, days:[false,false,false,false,false,false,false] }; });
}

function switchTab(id, btnId) {
  document.querySelectorAll('.section').forEach(function(s){ s.classList.remove('active'); });
  document.querySelectorAll('.nav-btn').forEach(function(b){ b.classList.remove('active'); });
  var sec = document.getElementById('sec-' + id);
  if(sec) sec.classList.add('active');
  var btn = document.getElementById(btnId);
  if(btn) btn.classList.add('active');
  if(id === 'poids'){ updateChart(); updateWeightHistory(); }
  if(id === 'habitudes'){ renderHabits(); }
  if(id === 'dashboard'){ updateDashboard(); }
  window.scrollTo(0,0);
}

function showToast(msg) {
  var t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(function(){ t.classList.remove('show'); }, 2500);
}

function calculate() {
  var poids = parseFloat(document.getElementById("poids").value);
  var bf = parseFloat(document.getElementById("bodyfat").value);
  var steps = parseFloat(document.getElementById("steps").value);
  var goal = parseFloat(document.getElementById("goal").value);
  if(!poids||!bf||!steps){ showToast("⚠️ Remplissez tous les champs !"); return; }
  var lean = poids*(1-bf/100);
  var bmr = 370+(21.6*lean);
  var neat = steps*0.04;
  var tef = (bmr+neat)*0.1;
  var tdee = Math.round(bmr+neat+tef);
  var target = Math.round(tdee+goal);
  var protein = Math.round(lean*2.2);
  var fat = Math.round(poids*0.9);
  var carbs = Math.max(0, Math.round((target-protein*4-fat*9)/4));
  try{ localStorage.setItem("lp_tdee",tdee); localStorage.setItem("lp_target",target); localStorage.setItem("lp_poids",poids); localStorage.setItem("lp_bf",bf); }catch(e){}
  document.getElementById("result").innerHTML =
    '<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px;">'+
    '<div class="stat-card" style="margin:0;"><div class="stat-value">'+tdee+'</div><div class="stat-label">TDEE kcal</div></div>'+
    '<div class="stat-card" style="margin:0;"><div class="stat-value" style="color:var(--green);">'+target+'</div><div class="stat-label">Objectif kcal</div></div>'+
    '</div><div class="macros">'+
    '<div class="macro-box protein"><div class="macro-val">'+protein+'g</div><div class="macro-label">Protéines</div></div>'+
    '<div class="macro-box carbs"><div class="macro-val">'+carbs+'g</div><div class="macro-label">Glucides</div></div>'+
    '<div class="macro-box fat"><div class="macro-val">'+fat+'g</div><div class="macro-label">Lipides</div></div>'+
    '</div>';
  updateDashboard();
  showToast("✅ TDEE calculé !");
}

function updateDashboard() {
  var tdee=localStorage.getItem("lp_tdee"), target=localStorage.getItem("lp_target"),
      pds=localStorage.getItem("lp_poids"), bf=localStorage.getItem("lp_bf");
  if(tdee) document.getElementById("d-tdee").textContent=tdee;
  if(target) document.getElementById("d-target").textContent=target;
  if(pds) document.getElementById("d-weight").textContent=pds+" kg";
  if(bf) document.getElementById("d-bf").textContent=bf+"%";
  document.getElementById("streakVal").textContent=streak;
}

function analyzeMeal() {
  var meal = document.getElementById("meal").value.trim();
  if(!meal){ showToast("⚠️ Décrivez votre repas !"); return; }
  var loader=document.getElementById("mealLoader"), result=document.getElementById("mealResult");
  loader.classList.add("visible"); result.classList.remove("visible");
  fetch("https://api.anthropic.com/v1/messages",{
    method:"POST", headers:{"Content-Type":"application/json"},
    body:JSON.stringify({ model:"claude-sonnet-4-20250514", max_tokens:400,
      messages:[{role:"user",content:"Nutritionniste expert. Analyse ce repas : \""+meal+"\". HTML inline court : calories (fourchette), macros en g, qualité en 1 mot coloré, 1 conseil. Direct, sans intro."}]
    })
  }).then(function(r){return r.json();}).then(function(data){
    result.innerHTML=data.content.map(function(i){return i.text||"";}).join("");
    result.classList.add("visible"); loader.classList.remove("visible");
  }).catch(function(){ result.innerHTML="Erreur de connexion à l'IA."; result.classList.add("visible"); loader.classList.remove("visible"); });
}

function addQuickMeal() {
  var food=document.getElementById("quickFood").value.trim(), cal=parseInt(document.getElementById("quickCal").value);
  if(!food||!cal){ showToast("⚠️ Renseignez aliment et calories !"); return; }
  mealLog.push({food:food,cal:cal,time:new Date().toLocaleTimeString('fr-FR',{hour:'2-digit',minute:'2-digit'})});
  try{localStorage.setItem("lp_meals",JSON.stringify(mealLog));}catch(e){}
  document.getElementById("quickFood").value=""; document.getElementById("quickCal").value="";
  updateMealLog(); showToast("✅ Repas ajouté !");
}

function updateMealLog() {
  var log=document.getElementById("mealLog");
  var total=mealLog.reduce(function(s,m){return s+m.cal;},0);
  var target=parseInt(localStorage.getItem("lp_target"))||2000;
  log.innerHTML=mealLog.map(function(m,i){
    return '<div class="workout-item"><div><div class="ex-name">'+m.food+'</div><div class="ex-detail">'+m.time+'</div></div>'+
    '<div style="display:flex;align-items:center;gap:8px;"><span style="font-weight:600;font-size:13px;">'+m.cal+' kcal</span>'+
    '<button class="delete-btn" onclick="removeMeal('+i+')">×</button></div></div>';
  }).join("");
  document.getElementById("totalCal").textContent=total+" kcal";
  var pct=Math.min(100,Math.round((total/target)*100));
  document.getElementById("calProgress").style.width=pct+"%";
  var remain=target-total;
  document.getElementById("calRemain").textContent=remain>0?remain+" kcal restantes ("+pct+"% de l'objectif)":"⚠️ Dépassé de "+Math.abs(remain)+" kcal";
}

function removeMeal(i){ mealLog.splice(i,1); try{localStorage.setItem("lp_meals",JSON.stringify(mealLog));}catch(e){} updateMealLog(); }

function toggleCustomEx(sel){ document.getElementById("customExField").style.display=sel.value==="custom"?"block":"none"; }

function addWorkout() {
  var sel=document.getElementById("exerciseSelect");
  var exName=sel.value==="custom"?document.getElementById("exercise").value.trim():sel.value;
  var sets=parseInt(document.getElementById("sets").value)||1;
  var reps=parseInt(document.getElementById("reps").value);
  var weight=parseFloat(document.getElementById("weightLift").value);
  var rir=document.getElementById("rir").value;
  if(!exName||!reps||!weight){ showToast("⚠️ Remplissez tous les champs !"); return; }
  workouts.push({ex:exName,sets:sets,reps:reps,weight:weight,rir:rir,volume:sets*reps*weight});
  try{localStorage.setItem("lp_workouts",JSON.stringify(workouts));}catch(e){}
  displayWorkouts(); showToast("✅ Série ajoutée !");
}

function displayWorkouts() {
  var list=document.getElementById("workoutList"),empty=document.getElementById("emptyWorkout"),vi=document.getElementById("volumeInfo");
  if(workouts.length===0){list.innerHTML="";empty.style.display="block";vi.style.display="none";return;}
  empty.style.display="none"; vi.style.display="block";
  var totalVol=workouts.reduce(function(s,w){return s+(w.volume||0);},0);
  document.getElementById("totalVolume").textContent=Math.round(totalVol).toLocaleString('fr-FR')+" kg";
  list.innerHTML=workouts.map(function(w,i){
    return '<div class="workout-item"><div><div class="ex-name">'+w.ex+'</div><div class="ex-detail">'+w.sets+'×'+w.reps+' @ '+w.weight+'kg — RIR '+w.rir+'</div></div>'+
    '<button class="delete-btn" onclick="removeWorkout('+i+')">×</button></div>';
  }).join("");
}

function removeWorkout(i){ workouts.splice(i,1); try{localStorage.setItem("lp_workouts",JSON.stringify(workouts));}catch(e){} displayWorkouts(); }

function addWeight() {
  var w=parseFloat(document.getElementById("newWeight").value);
  var bf=parseFloat(document.getElementById("newBF").value)||null;
  if(!w){ showToast("⚠️ Entrez un poids valide !"); return; }
  weights.push({w:w,bf:bf,date:new Date().toLocaleDateString('fr-FR')});
  try{localStorage.setItem("lp_weights",JSON.stringify(weights));}catch(e){}
  document.getElementById("newWeight").value=""; document.getElementById("newBF").value="";
  streak++; try{localStorage.setItem("lp_streak",streak);}catch(e){}
  document.getElementById("streakVal").textContent=streak;
  updateChart(); updateWeightHistory(); showToast("✅ Poids enregistré !");
}

function updateChart() {
  var labels=weights.map(function(w){return w.date;}), data=weights.map(function(w){return w.w;});
  if(weights.length>0){
    var curr=weights[weights.length-1].w, first=weights[0].w, delta=Math.round((curr-first)*10)/10;
    document.getElementById("wCurrent").textContent=curr+" kg";
    document.getElementById("wChange").innerHTML='<span style="color:'+(delta<0?'var(--green)':delta>0?'#ff4444':'var(--muted)')+'">'+(delta>0?'+':'')+delta+' kg</span>';
  }
  var canvas=document.getElementById("chart"); if(!canvas)return;
  if(chart){chart.data.labels=labels;chart.data.datasets[0].data=data;chart.update();return;}
  chart=new Chart(canvas,{type:"line",data:{labels:labels,datasets:[{label:"Poids",data:data,borderColor:"#ff5c2a",backgroundColor:"rgba(255,92,42,0.08)",fill:true,tension:0.4,pointBackgroundColor:"#ff5c2a",pointRadius:4}]},
    options:{responsive:true,plugins:{legend:{display:false}},scales:{x:{ticks:{color:"#666",font:{size:10}},grid:{color:"rgba(255,255,255,0.04)"}},y:{ticks:{color:"#666",font:{size:10}},grid:{color:"rgba(255,255,255,0.04)"}}}}});
}

function updateWeightHistory() {
  var hist=document.getElementById("weightHistory"); if(!hist)return;
  if(weights.length===0){hist.innerHTML='<div style="color:var(--muted);font-size:13px;text-align:center;padding:16px;">Aucune mesure</div>';return;}
  hist.innerHTML=weights.slice().reverse().slice(0,10).map(function(w){
    return '<div style="display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border);">'+
    '<span style="font-size:13px;color:var(--muted);">'+w.date+'</span>'+
    '<div style="display:flex;gap:12px;align-items:center;">'+(w.bf?'<span style="font-size:12px;color:var(--muted);">'+w.bf+'% BF</span>':'')+
    '<span style="font-weight:600;">'+w.w+' kg</span></div></div>';
  }).join("");
}

var DAYS=["L","M","M","J","V","S","D"];
function renderHabits() {
  var c=document.getElementById("habitTracker"); if(!c)return;
  c.innerHTML=habits.map(function(h,hi){
    return '<div class="habit-row"><div class="habit-name">'+h.name+'</div><div class="habit-dots">'+
    h.days.map(function(done,di){return '<div class="habit-dot'+(done?' done':'')+'" onclick="toggleHabit('+hi+','+di+')"></div>';}).join("")+
    '</div></div>';
  }).join("");
  updateHabitScore();
}

function toggleHabit(hi,di){
  habits[hi].days[di]=!habits[hi].days[di];
  try{localStorage.setItem("lp_habits",JSON.stringify(habits));}catch(e){}
  renderHabits();
}

function updateHabitScore() {
  var total=habits.length*7, done=habits.reduce(function(s,h){return s+h.days.filter(Boolean).length;},0);
  var pct=Math.round((done/total)*100);
  document.getElementById("habitScore").textContent=pct+"%";
  document.getElementById("habitProgress").style.width=pct+"%";
  var msgs=["Commencez à cocher !","Bon début, continuez !","Sur la bonne voie !","Excellent rythme !","Performance max !"];
  document.getElementById("habitMsg").textContent=msgs[Math.min(4,Math.floor(pct/25))];
}

function generateAIPlan() {
  var poids=localStorage.getItem("lp_poids"), bf=localStorage.getItem("lp_bf");
  var goalEl=document.getElementById("goal"), goal=goalEl?goalEl.value:"0";
  var goalText=parseFloat(goal)>0?"Prise de masse":parseFloat(goal)<0?"Perte de graisse":"Maintien";
  var loader=document.getElementById("planLoader"), result=document.getElementById("aiPlanResult");
  loader.classList.add("visible"); result.classList.remove("visible");
  fetch("https://api.anthropic.com/v1/messages",{
    method:"POST",headers:{"Content-Type":"application/json"},
    body:JSON.stringify({model:"claude-sonnet-4-20250514",max_tokens:500,
      messages:[{role:"user",content:"Coach fitness expert. Plan personnalisé : Poids "+(poids||"?")+"kg, BF "+(bf||"?")+"%, Objectif : "+goalText+". HTML inline court, max 180 mots. Direct, sans intro."}]
    })
  }).then(function(r){return r.json();}).then(function(data){
    result.innerHTML=data.content.map(function(i){return i.text||"";}).join("");
    result.classList.add("visible"); loader.classList.remove("visible");
  }).catch(function(){ result.innerHTML="Erreur de connexion."; result.classList.add("visible"); loader.classList.remove("visible"); });
}

// INIT
updateDashboard();
displayWorkouts();
updateMealLog();
</script>
</body>
</html>
