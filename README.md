<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Elektroniczny Dziennik</title>

<style>
:root {
  --blue:#163b68;
  --blue2:#245b98;
  --light:#f1f5f9;
  --white:#ffffff;
  --text:#172033;
  --muted:#64748b;
  --border:#dbe3ed;
  --green:#159447;
  --orange:#e68a00;
  --red:#d62828;
}

* {
  box-sizing:border-box;
}

body {
  margin:0;
  font-family:Arial, Helvetica, sans-serif;
  background:var(--light);
  color:var(--text);
}

header {
  background:linear-gradient(135deg,var(--blue),var(--blue2));
  color:white;
  padding:22px;
  box-shadow:0 2px 8px #0003;
}

header h1 {
  margin:0 0 8px;
  font-size:25px;
}

header p {
  margin:4px 0;
  opacity:.95;
}

.student {
  font-weight:bold;
  font-size:15px;
}

nav {
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  padding:12px;
  background:white;
  border-bottom:1px solid var(--border);
  position:sticky;
  top:0;
  z-index:5;
}

nav button {
  border:0;
  background:#e7eef7;
  color:var(--blue);
  padding:10px 13px;
  border-radius:8px;
  cursor:pointer;
  font-weight:bold;
}

nav button.active,
nav button:hover {
  background:var(--blue);
  color:white;
}

main {
  max-width:1200px;
  margin:auto;
  padding:20px;
}

.section {
  display:none;
}

.section.active {
  display:block;
}

.cards {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:14px;
  margin-bottom:20px;
}

.card,
.panel {
  background:white;
  border:1px solid var(--border);
  border-radius:12px;
  padding:18px;
  box-shadow:0 2px 5px #0000000b;
}

.card strong {
  display:block;
  font-size:28px;
  color:var(--blue);
  margin-top:7px;
}

.card small,
.muted {
  color:var(--muted);
}

h2,
h3 {
  color:var(--blue);
}

table {
  width:100%;
  border-collapse:collapse;
  background:white;
  border-radius:10px;
  overflow:hidden;
}

th,
td {
  padding:11px;
  border-bottom:1px solid var(--border);
  text-align:left;
  vertical-align:middle;
}

th {
  background:#e9f0f8;
  color:var(--blue);
}

tr:hover td {
  background:#f8fbff;
}

.grades {
  display:flex;
  flex-wrap:wrap;
  gap:7px;
}

.grade {
  width:35px;
  height:35px;
  border:0;
  border-radius:7px;
  background:var(--blue2);
  color:white;
  font-weight:bold;
  cursor:pointer;
  transition:.2s;
}

.grade:hover {
  background:var(--green);
  transform:scale(1.08);
}

.no-grades {
  color:var(--muted);
  font-style:italic;
}

.average {
  font-weight:bold;
  color:var(--blue);
}

.schedule {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
  gap:15px;
}

.day {
  background:white;
  border:1px solid var(--border);
  border-radius:12px;
  padding:15px;
}

.day h3 {
  margin-top:0;
  border-bottom:1px solid var(--border);
  padding-bottom:8px;
}

.lesson {
  padding:10px;
  border-left:4px solid var(--blue2);
  background:#f8fbff;
  margin:7px 0;
  border-radius:5px;
}

.lesson time {
  display:block;
  color:var(--muted);
  font-size:13px;
  margin-bottom:4px;
}

.info-box {
  background:#f8fbff;
  border-left:4px solid var(--blue2);
  padding:13px;
  border-radius:6px;
  margin-top:15px;
}

footer {
  text-align:center;
  color:var(--muted);
  padding:25px;
  font-size:13px;
}

.modal {
  display:none;
  position:fixed;
  inset:0;
  background:#0008;
  z-index:20;
  align-items:center;
  justify-content:center;
  padding:20px;
}

.modal.show {
  display:flex;
}

.modal-content {
  width:100%;
  max-width:420px;
  background:white;
  border-radius:12px;
  padding:22px;
  box-shadow:0 5px 25px #0005;
}

.modal-content h2 {
  margin-top:0;
}

.modal-row {
  padding:9px 0;
  border-bottom:1px solid var(--border);
}

.close {
  width:100%;
  margin-top:18px;
  border:0;
  padding:11px;
  border-radius:7px;
  background:var(--blue);
  color:white;
  cursor:pointer;
  font-weight:bold;
}

@media(max-width:600px) {
  main {
    padding:12px;
  }

  th,
  td {
    padding:8px 5px;
    font-size:13px;
  }

  header h1 {
    font-size:21px;
  }

  .grade {
    width:32px;
    height:32px;
  }
}
</style>
</head>

<body>

<header>
  <h1>Elektroniczny Dziennik</h1>
  <p>Zespół Szkół Budowlano-Geodezyjnych</p>
  <p class="student">Uczeń: Adrian Szutko · Klasa 4F</p>
</header>

<nav>
  <button class="tab active" data-tab="start">Start</button>
  <button class="tab" data-tab="grades">Oceny</button>
  <button class="tab" data-tab="schedule">Plan lekcji</button>
  <button class="tab" data-tab="teachers">Nauczyciele</button>
</nav>

<main>

<section id="start" class="section active">
  <h2>Panel główny</h2>

  <div class="cards">
    <div class="card">
      Uczeń
      <strong style="font-size:21px;">Adrian Szutko</strong>
      <small>klasa 4F</small>
    </div>

    <div class="card">
      Średnia ocen
      <strong id="mainAverage">-</strong>
      <small>średnia ważona</small>
    </div>

    <div class="card">
      Przedmioty
      <strong id="subjectCount">0</strong>
      <small>na liście klasy 4F</small>
    </div>

    <div class="card">
      Oceny
      <strong id="gradeCount">0</strong>
      <small>wpisanych ocen</small>
    </div>
  </div>

  <div class="panel">
    <h3>Informacje o ocenach</h3>
    <p>
      Oceny są obliczane jako średnia ważona.
      Kliknij dowolny kwadrat z oceną, aby zobaczyć szczegóły.
    </p>

    <div class="info-box">
      <b>Wagi ocen:</b><br>
      Sprawdzian: 4<br>
      Kartkówka: 2<br>
      Odpowiedź ustna: 1<br>
      Praca na lekcji: 1
    </div>
  </div>
</section>

<section id="grades" class="section">
  <h2>Oceny</h2>

  <div class="panel">
    <p class="muted">
      Kliknij kwadrat z oceną, aby zobaczyć nauczyciela, rodzaj pracy i datę.
    </p>

    <table>
      <thead>
        <tr>
          <th>Przedmiot</th>
          <th>Oceny</th>
          <th>Średnia ważona</th>
        </tr>
      </thead>
      <tbody id="gradesTable"></tbody>
    </table>
  </div>
</section>

<section id="schedule" class="section">
  <h2>Plan lekcji</h2>
  <div id="scheduleBox" class="schedule"></div>
</section>

<section id="teachers" class="section">
  <h2>Nauczyciele</h2>

  <div class="panel">
    <table>
      <thead>
        <tr>
          <th>Przedmiot</th>
          <th>Nauczyciel</th>
        </tr>
      </thead>
      <tbody id="teachersTable"></tbody>
    </table>
  </div>
</section>

</main>

<footer>
  Elektroniczny Dziennik · Adrian Szutko · Klasa 4F
</footer>

<div id="gradeModal" class="modal">
  <div class="modal-content">
    <h2>Szczegóły oceny</h2>
    <div id="modalDetails"></div>
    <button class="close" onclick="closeModal()">Zamknij</button>
  </div>
</div>

<script>
const subjects = [
  "Język Polski",
  "Matematyka",
  "Język Angielski",
  "Język Angielski w Budownictwie",
  "Fizyka",
  "Fizyka Techniczna",
  "Geografia",
  "Historia",
  "Język Niemiecki",
  "Kształtowanie Kompetencji Zawodowych",
  "Obsługa Systemów Energetyki Odnawialnej",
  "Systemy Energii Odnawialnej",
  "Wychowanie Fizyczne",
  "Umiejętności Rynkowe - Przygotowanie do egzaminu na uprawnienia elektryczne G1"
];

const teachers = {
  "Matematyka":"Joanna Wasilewska",
  "Fizyka":"Paweł Klim",
  "Fizyka Techniczna":"Paweł Klim",
  "Język Angielski":"Anna Mróz",
  "Język Angielski w Budownictwie":"Anna Mróz",
  "Język Polski":"Dorota Puciłowska",
  "Geografia":"Nie podano",
  "Historia":"Nie podano",
  "Język Niemiecki":"Nie podano",
  "Systemy Energii Odnawialnej":"Beata Polonis",
  "Obsługa Systemów Energetyki Odnawialnej":"Beata Polonis",
  "Kształtowanie Kompetencji Zawodowych":"Beata Polonis",
  "Wychowanie Fizyczne":"Zbigniew Kulikowski",
  "Umiejętności Rynkowe - Przygotowanie do egzaminu na uprawnienia elektryczne G1":"Tomasz Rolak"
};

const gradeWeights = {
  "sprawdzian":4,
  "kartkówka":2,
  "kartkowka":2,
  "odpowiedź ustna":1,
  "odpowiedz ustna":1,
  "praca na lekcji":1
};

const grades = {
  "Język Polski": [
    {value:"3", type:"Kartkówka", date:"12.10.2026"}
  ],

  "Systemy Energii Odnawialnej": [
    {value:"3", type:"Kartkówka", date:"21.09.2026"},
    {value:"3", type:"Kartkówka", date:"09.10.2026"}
  ],

  "Wychowanie Fizyczne": [
    {value:"5", type:"Sprawdzian", date:"22.09.2026"},
    {value:"5-", type:"Praca na lekcji", date:"06.10.2026"}
  ],

  "Obsługa Systemów Energetyki Odnawialnej": [
    {value:"3", type:"Odpowiedź ustna", date:"10.09.2026"},
    {value:"4-", type:"Kartkówka", date:"17.09.2026"}
  ],

  "Język Angielski w Budownictwie": [
    {value:"6", type:"Kartkówka", date:"25.09.2026"}
  ],

  "Język Angielski": [
    {value:"4", type:"Kartkówka", date:"09.10.2026"}
  ],

  "Geografia": [
    {value:"3", type:"Sprawdzian", date:"04.10.2026"},
    {value:"3", type:"Kartkówka", date:"27.09.2026"}
  ],

  "Fizyka Techniczna": [
    {value:"4", type:"Praca na lekcji", date:"05.10.2026"},
    {value:"2", type:"Praca na lekcji", date:"12.10.2026"}
  ],

  "Fizyka": [
    {value:"4", type:"Kartkówka", date:"29.09.2026"},
    {value:"3", type:"Praca na lekcji", date:"30.09.2026"}
  ]
};

const schedule = {
  "Poniedziałek":[
    ["08:00 - 08:45","Język Polski"],
    ["08:55 - 09:40","Język Polski"],
    ["09:50 - 10:35","Matematyka"],
    ["10:45 - 11:30","Fizyka Techniczna"],
    ["11:45 - 12:30","Systemy Energii Odnawialnej"],
    ["12:40 - 13:25","Geografia"],
    ["13:35 - 14:20","Umiejętności Rynkowe"],
    ["14:30 - 15:15","Umiejętności Rynkowe"],
    ["15:20 - 16:05","Historia"]
  ],

  "Wtorek":[
    ["09:50 - 10:35","Systemy Energii Odnawialnej"],
    ["10:45 - 11:30","Systemy Energii Odnawialnej"],
    ["11:45 - 12:30","Matematyka"],
    ["12:40 - 13:25","Fizyka"],
    ["13:35 - 14:20","Wychowanie Fizyczne"],
    ["14:30 - 15:15","Język Angielski"]
  ],

  "Środa":[
    ["08:55 - 09:40","Fizyka"],
    ["09:50 - 10:35","Język Angielski w Budownictwie"],
    ["10:45 - 11:30","Zajęcia z wychowawcą"],
    ["11:45 - 12:30","Matematyka"],
    ["12:40 - 13:25","Kształtowanie Kompetencji Zawodowych"],
    ["13:35 - 14:20","Kształtowanie Kompetencji Zawodowych"]
  ],

  "Czwartek":[
    ["08:00 - 08:45","Język Polski"],
    ["08:55 - 09:40","Język Polski"],
    ["09:50 - 10:35","Fizyka"],
    ["10:45 - 11:30","Język Angielski"],
    ["11:45 - 12:30","Wychowanie Fizyczne"],
    ["12:40 - 13:25","Systemy Energii Odnawialnej"]
  ],

  "Piątek":[
    ["08:00 - 08:45","Geografia"],
    ["08:55 - 09:40","Matematyka"],
    ["09:50 - 10:35","Obsługa Systemów Energii Odnawialnej"],
    ["10:45 - 11:30","Obsługa Systemów Energii Odnawialnej"],
    ["11:45 - 12:30","Język Angielski w Budownictwie"]
  ]
};

function numericGrade(value) {
  if (value.endsWith("-")) {
    return parseFloat(value) - 0.25;
  }

  if (value.endsWith("+")) {
    return parseFloat(value) + 0.25;
  }

  return parseFloat(value);
}

function gradeAverage(subject) {
  const subjectGrades = grades[subject] || [];

  if (subjectGrades.length === 0) {
    return null;
  }

  let weightedSum = 0;
  let totalWeight = 0;

  subjectGrades.forEach(grade => {
    const type = grade.type.toLowerCase();
    const weight = gradeWeights[type] || 1;

    weightedSum += numericGrade(grade.value) * weight;
    totalWeight += weight;
  });

  return weightedSum / totalWeight;
}

function formatAverage(value) {
  if (value === null) {
    return "Brak ocen";
  }

  return value.toFixed(2).replace(".", ",");
}

function renderGrades() {
  const table = document.getElementById("gradesTable");
  table.innerHTML = "";

  subjects.forEach(subject => {
    const row = document.createElement("tr");
    const subjectGrades = grades[subject] || [];

    const gradeContainer = document.createElement("div");
    gradeContainer.className = "grades";

    if (subjectGrades.length === 0) {
      gradeContainer.innerHTML = '<span class="no-grades">Brak ocen</span>';
    } else {
      subjectGrades.forEach(grade => {
        const button = document.createElement("button");
        button.className = "grade";
        button.textContent = grade.value;

        button.addEventListener("click", () => {
          showGradeDetails(subject, grade);
        });

        gradeContainer.appendChild(button);
      });
    }

    const average = gradeAverage(subject);

    row.innerHTML = `
      <td>\({subject}</td>
      <td></td>
      <td class="average">\){formatAverage(average)}</td>
    `;

    row.children[1].appendChild(gradeContainer);
    table.appendChild(row);
  });
}

function showGradeDetails(subject, grade) {
  const teacher = teachers[subject] || "Nie podano";
  const weight = gradeWeights[grade.type.toLowerCase()] || 1;

  document.getElementById("modalDetails").innerHTML = `
    <div class="modal-row"><b>Przedmiot:</b><br>\({subject}</div>
    <div class="modal-row"><b>Ocena:</b><br>\){grade.value}</div>
    <div class="modal-row"><b>Nauczyciel:</b><br>\({teacher}</div>
    <div class="modal-row"><b>Rodzaj pracy:</b><br>\){grade.type}</div>
    <div class="modal-row"><b>Data:</b><br>\({grade.date}</div>
    <div class="modal-row"><b>Waga:</b><br>\){weight}</div>
  `;

  document.getElementById("gradeModal").classList.add("show");
}

function closeModal() {
  document.getElementById("gradeModal").classList.remove("show");
}

function renderTeachers() {
  const table = document.getElementById("teachersTable");
  table.innerHTML = "";

  subjects.forEach(subject => {
    const row = document.createElement("tr");

    row.innerHTML = `
      <td>\({subject}</td>
      <td>\){teachers[subject] || "Nie podano"}</td>
    `;

    table.appendChild(row);
  });
}

function renderSchedule() {
  const box = document.getElementById("scheduleBox");
  box.innerHTML = "";

  Object.entries(schedule).forEach(([day, lessons]) => {
    const dayBox = document.createElement("div");
    dayBox.className = "day";

    dayBox.innerHTML = `<h3>\({day}</h3>`;

    lessons.forEach(([time, subject]) => {
      dayBox.innerHTML += `
        <div class="lesson">
          <time>\){time}</time>
          ${subject}
        </div>
      `;
    });

    box.appendChild(dayBox);
  });
}

function updateStatistics() {
  let totalGrades = 0;
  let weightedSum = 0;
  let totalWeight = 0;

  Object.values(grades).forEach(subjectGrades => {
    totalGrades += subjectGrades.length;

    subjectGrades.forEach(grade => {
      const weight = gradeWeights[grade.type.toLowerCase()] || 1;

      weightedSum += numericGrade(grade.value) * weight;
      totalWeight += weight;
    });
  });

  const average = totalWeight > 0
    ? weightedSum / totalWeight
    : null;

  document.getElementById("subjectCount").textContent = subjects.length;
  document.getElementById("gradeCount").textContent = totalGrades;
  document.getElementById("mainAverage").textContent = formatAverage(average);
}

document.querySelectorAll(".tab").forEach(button => {
  button.addEventListener("click", () => {
    document.querySelectorAll(".tab").forEach(tab => {
      tab.classList.remove("active");
    });

    document.querySelectorAll(".section").forEach(section => {
      section.classList.remove("active");
    });

    button.classList.add("active");
    document.getElementById(button.dataset.tab).classList.add("active");
  });
});

document.getElementById("gradeModal").addEventListener("click", event => {
  if (event.target.id === "gradeModal") {
    closeModal();
  }
});

renderGrades();
renderTeachers();
renderSchedule();
updateStatistics();
</script>

</body>
</html>
