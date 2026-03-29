# Play-Reglement-Interieur
Logiciel pour maîtriser le règlement intérieur 

<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz Vie Scolaire</title>

<style>
body {
  font-family: Arial;
  background: linear-gradient(to right, #1e3c72, #2a5298);
  color: white;
  text-align: center;
  margin: 0;
}

.container {
  background: white;
  color: black;
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  border-radius: 10px;
}

.characters {
  font-size: 60px;
}

.good { color: green; transform: scale(1.2); }
.bad { color: red; transform: scale(1.2); }

button {
  display: block;
  width: 90%;
  margin: 10px auto;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.correct { background: green; color: white; }
.wrong { background: red; color: white; }

#restart {
  display: none;
  background: #3498db;
  color: white;
}
</style>
</head>

<body>

<h1>🎓 Quiz Règlement Intérieur Lycée Moderne de Treichville</h1>

<div class="characters">
  <span id="student">🧑‍🎓</span>
  <span>🧑‍🏫</span>
</div>

<div class="container">
  <p id="question"></p>

  <button onclick="checkAnswer(true)" id="btn1"></button>
  <button onclick="checkAnswer(false)" id="btn2"></button>

  <p id="feedback"></p>
  <p id="score">Score : 0</p>
  <p id="stats"></p>

  <button id="restart" onclick="restartGame()">🔄 Rejouer</button>
</div>

<script>
let score = 0;
let index = 0;
let correctCount = 0;
let wrongCount = 0;

const quiz = [

  // EXISTANTES
  {q:"Quelle est l'Heure de début des cours au LMT ?", a:"7h30", b:"8h30", correct:true},
  {q:"Que faire en cas de retard à la première heure ?", a:"Justifier chez l'Educateur", b:"attendre la deuxième pour rentrer", correct:true},
  {q:"La Bagarre est elle autorisée ?", a:"Oui, je dois me rendre justice", b:"Non,je dois aller me plaindre chez l'Educateur", correct:false},

  // NOUVELLES QUESTIONS
  {q:"Que faire en cas de retard à la première heure ?", a:"Aller en classe", b:"Prendre un billet chez l’éducateur", correct:false},
  {q:"Quel type de chaussures il faut porter au LMT ?", a:"Chaussures fermées", b:"Sandales", correct:true},
  {q:"Les foulards et képi sont-ils autorisés ?", a:"Oui", b:"Non", correct:false},
  {q:"Quelle est l'Importance du macaron au LMT ?", a:"Une meilleure identification des élèves du lycée", b:"Décoration simple de la tenue", correct:true},
  {q:"Les mèches sont-elles acceptées ?", a:"Oui", b:"Non", correct:false},
  {q:"Que faire après un retour d'absence ?", a:"Prendre un billet d'entrée chez l'Educateur", b:"Donner des explications au professeur", correct:false},
  {q:"Dans quel cas prendre un Billet d’annulation de zéro ?", a:" En cas de Retards", b:" En cas d'Absence justifiée", correct:false},
  {q:"Respect du personnel obligatoire ?", a:"Oui", b:"Non", correct:true},
  {q:"Les Anniversaires en classe sont autorisés ?", a:"Oui", b:"Non", correct:false},
  {q:"Les Parents peuvent entrer en classe pour voir leurs enfants ?", a:"Oui", b:"Non, ils doivent se rendre chez l'Educateur", correct:false},
  {q:"Les Aliments sont ils autorisés en classe ?", a:"Oui", b:"Non", correct:false}
];

function loadQuestion(){
  let q = quiz[index];
  document.getElementById("question").textContent = q.q;
  document.getElementById("btn1").textContent = q.a;
  document.getElementById("btn2").textContent = q.b;
}

function checkAnswer(choice){
  let student = document.getElementById("student");

  if(choice === quiz[index].correct){
    score += 10;
    correctCount++;
    document.getElementById("feedback").textContent = "✅ Bonne réponse";
    student.className = "good";
  } else {
    score -= 5;
    wrongCount++;
    document.getElementById("feedback").textContent = "❌ Mauvaise réponse";
    student.className = "bad";
  }

  document.getElementById("score").textContent = "Score : " + score;
  document.getElementById("stats").textContent =
    "✔️ Bonnes réponses: " + correctCount + " | ❌ Mauvaises: " + wrongCount;

  index++;

  if(index < quiz.length){
    setTimeout(()=>{
      student.className = "";
      loadQuestion();
    },1000);
  } else {
    endGame();
  }
}

function endGame(){
  let message = "";

  if(score >= 80){
    message = "🏆 Élève exemplaire";
  } else if(score >= 40){
    message = "👍 Élève moyen";
  } else {
    message = "⚠️ Remédiation nécessaire";
  }

  document.getElementById("question").textContent = message;
  document.getElementById("btn1").style.display = "none";
  document.getElementById("btn2").style.display = "none";
  document.getElementById("restart").style.display = "block";
}

function restartGame(){
  score = 0;
  index = 0;
  correctCount = 0;
  wrongCount = 0;

  document.getElementById("score").textContent = "Score : 0";
  document.getElementById("stats").textContent = "";
  document.getElementById("feedback").textContent = "";

  document.getElementById("btn1").style.display = "block";
  document.getElementById("btn2").style.display = "block";
  document.getElementById("restart").style.display = "none";

  loadQuestion();
}

loadQuestion();
</script>

</body>
</html>
