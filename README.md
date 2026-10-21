<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Elektroniczny Dziennik 4F</title>

<style>
:root {
  --bg:#101722;
  --bg2:#172333;
  --panel:#1d2b3d;
  --panel2:#23354a;
  --text:#edf4fc;
  --muted:#9eafc2;
  --blue:#3d8bea;
  --blue-dark:#1d5da5;
  --green:#20ad62;
  --red:#dc4141;
  --orange:#d99124;
  --border:#33475e;
  --shadow:#0008;
}

* {
  box-sizing:border-box;
}

body {
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:var(--bg);
  color:var(--text);
}

header {
  padding:22px;
  background:linear-gradient(135deg,#102d50,#1f5d9d);
  box-shadow:0 2px 10px var(--shadow);
}

header h1 {
  margin:0 0 8px;
  font-size:25px;
}

header p {
  margin:4px 0;
  color:#dbeafe;
}

.student {
  font-weight:bold;
  font-size:16px;
}

nav {
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  padding:12px;
  background:var(--bg2);
  border-bottom:1px solid var(--border);
  position:sticky;
  top:0;
  z-index:5;
  box-shadow:0 2px 8px #0005;
}

nav button {
  border:0;
  background:#263a51;
  color:#dcecff;
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

h2, h3 {
  color:#8fc4ff;
}

.cards {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:14px;
  margin-bottom:20px;
}

.card,
.panel {
  background:var(--panel);
  border:1px solid var(--border);
  border-radius:12px;
  padding:18px;
  box-shadow:0 2px 8px #0004;
}

.card strong {
  display:block;
  font-size:28px;
  color:#8fc4ff;
  margin-top:7px;
}

.card small,
.muted {
  color:var(--muted);
}

table {
  width:100%;
  border-collapse:collapse;
  overflow:hidden;
}

th,
td {
  padding:12px 10px;
  border-bottom:1px solid var(--border);
  text-align:left;
  vertical-align:middle;
}

th {
  color:#a8d0ff;
  background:var(--panel2);
}

tr:hover td {
  background:#263a50;
}

.grade-list {
  display:flex;
  flex-wrap:wrap;
  gap:7px;
}

.grade-box {
  width:38px;
  height:38px;
  display:inline-flex;
  align-items:center;
  justify-content:center;
  border:0;
  border-radius:7px;
  background:var(--blue-dark);
  color:white;
  font-weight:bold;
  cursor:pointer;
  font-size:15px;
}

.grade-box:hover {
  background:#58a1f5;
  transform:scale(1.05);
}

.average {
  color:#8fc4ff;
  font-size:17px;
  font-weight:bold;
  white-space:nowrap;
}

.info-box {
  margin-top:10px;
  padding:12px;
  border-left:4px solid var(--blue);
  background:#16263a;
  color:#dcecff;
  border-radius:6px;
  line-height:1.5;
}

.schedule {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
  gap:15px;
}

.day {
  background:var(--panel);
  border:1px solid var(--border);
  border-radius:12px;
  padding:15px;
}

.day h3 {
  margin-top:0;
}

.lesson {
  padding:10px;
  border-left:4px solid var(--blue);
  background:#23354a;
  margin:8px 0;
  border-radius:5px;
}

.lesson time {
  display:block;
  color:var(--muted);
  font-size:13px;
  margin-bottom:4px;
}

.empty {
  color:var(--muted);
  font-style:italic;
}

footer {
  text-align:center;
  color:var(--muted);
  padding:25px;
  font-size:13px;
}

@media(max-width:600px) {
  main {
    padding:12px;
  }

  header {
    padding:18px;
  }

  header h1 {
    font-size:21px;
  }

  th,
  td {
    padding:9px 5px;
    font-size:12px;
  }

  .grade-box {
    width:34px;
    height:34px;
  }

  .average {
    font-size:14px;
  }
}
</style>
</head>

<body>

<header>
  <h1>Elektroniczny Dziennik</h1>
  <p>Zespół Szkół Budowlano-Geodezyjnych · Klasa 4F</p>
  <p class="student">Uczeń: Adrian Szutko</p>
</header>

<nav>
  <button class="tab active" data-tab="start">Start</button>
  <button class="tab" data-tab="grades">Oceny</button>
  <button class="tab" data-tab="attendance">Frekwencja</button>
  <button class="tab" data-tab="schedule">Plan lekcji</button>
  <button class="tab" data-tab="teachers">Nauczyciele</button>
  <button class="tab" data-tab="remarks">Uwagi</button>
  <button class="tab" data-tab="messages">Wiadomości</button>
</nav>

<main>

<section id="start" class="section active">
  <h2>Panel główny</h2>

  <div class="cards">
    <div class="card">
      Frekwencja
      <strong>100%</strong>
      <small>obecności</small>
    </div>

    <div class="card">
      Średnia ocen
      <strong id="average">-</strong>
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
    <h3>Informacje o uczniu</h3>
    <p><b>Imię i nazwisko:</b> Adrian Szutko</p>
    <p><b>Klasa:</b> 4F</p>
    <p><b>Szkoła:</b> Zespół Szkół Budowlano-Geodezyjnych</p>
  </div>
</section>

<section id="grades" class="section">
  <h2>Oceny</h2>

  <div class="panel">
    <p class="muted">
      Kliknij kwadrat z oceną, aby zobaczyć nauczyciela, rodzaj pracy,
      datę oraz wagę oceny.
    </p>

    <div class="info-box">
      Wagi: sprawdzian - 4, kartkówka - 2, odpowiedź ustna - 1,
      praca na lekcji - 1.
    </div>
  </div>

  <br>

  <div class="panel">
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

  <div id="gradeInfo"></div>
</section>

<section id="attendance" class="section">
  <h2>Frekwencja</h2>

  <div class="panel">
    <table>
      <thead>
        <tr>
          <th>Data</th>
          <th>Przedmiot</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td colspan="3" class="empty">Brak wpisów dotyczących nieobecności.</td>
        </tr>
      </tbody>
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

<section id="remarks" class="section">
  <h2>Uwagi</h2>

  <div class="panel">
    <p class="empty">Brak uwag.</p>
  </div>
</section>

<section id="messages" class="section">
  <h2>Wiadomości</h2>

  <div class="panel">
    <p class="empty">Brak wiadomości.</p>
  </div>
</section>

</main>

<footer>
  Elektroniczny Dziennik · Klasa 4F · Adrian Szutko
</footer>

<script>
const teachers = {
  "Matematyka":"Joanna Wasilewska",
  "Fizyka":"Paweł Klim",
  "Fizyka Techniczna":"Paweł Klim",
  "Język Angielski":"Anna Mróz",
  "Język Angielski w Budownictwie":"Anna Mróz",
  "Język Polski":"Dorota Puciłowska",
  "Geografia":"Marek Zieliński",
  "Historia":"Katarzyna Wójcik",
  "Systemy Energii Odnawialnej":"Beata Polonis",
  "Obsługa Systemów Energetyki Odnawialnej":"Beata Polonis",
  "Kształtowanie Kompetencji Zawodowych":"Beata Polonis",
  "Wychowanie Fizyczne":"Zbigniew Kulikowski",
  "Umiejętności Rynkowe":"Tomasz Rolak"
};

const grades = [
  {
    subject:"Język Polski",
    value:"3",
    type:"Kartkówka",
    date:"12.10.2026",
    weight:2
  },
  {
    subject:"Systemy Energii Odnawialnej",
    value:"3",
    type:"Kartkówka",
    date:"21.09.2026",
    weight:2
  },
  {
    subject:"Systemy Energii Odnawialnej",
    value:"3",
    type:"Kartkówka",
    date:"09.10.2026",
    weight:2
  },
  {
    subject:"Wychowanie Fizyczne",
    value:"5",
    type:"Sprawdzian",
    date:"22.09.2026",
    weight:4
  },
  {
    subject:"Wychowanie Fizyczne",
    value:"5-",
    type:"Praca na lekcji",
    date:"06.10.2026",
    weight:1
  },
  {
    subject:"Obsługa Systemów Energetyki Odnawialnej",
    value:"3",
    type:"Odpowiedź ustna",
    date:"10.09.2026",
    weight:1
  },
  {
    subject:"Obsługa Systemów Energetyki Odnawialnej",
    value:"4-",
    type:"Kartkówka",
    date:"17.09.2026",
    weight:2
  },
  {
    subject:"Język Angielski w Budownictwie",
    value:"6",
    type:"Kartkówka",
    date:"25.09.2026",
    weight:2
  },
  {
    subject:"Język Angielski",
    value:"4",
    type:"Kartkówka",
    date:"09.10.2026",
    weight:2
  },
  {
    subject:"Geografia",
    value:"3",
    type:"Sprawdzian",
    date:"04.10.2026",
    weight:4
  },
  {
    subject:"Geografia",
    value:"3",
    type:"Kartkówka",
    date:"27.09.2026",
    weight:2
  },
  {
    subject:"Fizyka Techniczna",
    value:"4",
    type:"Praca na lekcji",
    date:"05.10.2026",
    weight:1
  },
  {
    subject:"Fizyka Techniczna",
    value:"2",
    type:"Praca na lekcji",
    date:"12.10.2026",
    weight:1
  },
  {
    subject:"Fizyka",
    value:"4",
    type:"Kartkówka",
    date:"29.09.2026",
    weight:2
  },
  {
    subject:"Fizyka",
    value:"3",
    type:"Praca na lekcji",
    date:"30.09.2026",
    weight:1
  }
];

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
    ["08:00 - 08:45","Język Angielski"],
    ["08:55 - 09:40","Język Angielski"],
    ["09:50 - 10:35","Geografia"],
    ["10:45 - 11:30","Wychowanie Fizyczne"],
    ["11:45 - 12:30","Fizyka Techniczna"]
  ],
  "Piątek":[
    ["08:00 - 08:45","Język Polski"],
    ["08:55 - 09:40","Historia"],
    ["09:50 - 10:35","Systemy Energii Odnawialnej"],
    ["10:45 - 11:30","Obsługa Systemów Energetyki Odnawialnej"],
    ["11:45 - 12:30","Obsługa Systemów Energetyki Odnawialnej"]
  ]
};

function gradeToNumber(value) {
  if (value.endsWith("+")) {
    return Number(value[0]) + 0.25;
  }

  if (value.endsWith("-")) {
    return Number(value[0]) - 0.25;
  }

  return Number(value);
}

function weightedAverage(subject) {
  const subjectGrades = grades.filter(g => g.subject === subject);

  if (subjectGrades.length === 0) {
    return "-";
  }

  let total = 0;
  let weights = 0;

  subjectGrades.forEach(grade => {
    total += gradeToNumber(grade.value) * grade.weight;
    weights += grade.weight;
  });

  return (total / weights).toFixed(2);
}

function renderGrades() {
  const table = document.getElementById("gradesTable");
  const subjects = [...new Set(grades.map(grade => grade.subject))];

  table.innerHTML = "";

  subjects.forEach(subject => {
    const row = document.createElement("tr");

    const subjectCell = document.createElement("td");
    subjectCell.textContent = subject;

    const gradesCell = document.createElement("td");
    const gradeList = document.createElement("div");
    gradeList.className = "grade-list";

    grades
      .filter(grade => grade.subject === subject)
      .forEach(grade => {
        const button = document.createElement("button");
        button.className = "grade-box";
        button.textContent = grade.value;
        button.title = "Kliknij, aby zobaczyć szczegóły";

        button.addEventListener("click", () => {
          showGradeInfo(grade);
        });

        gradeList.appendChild(button);
      });

    gradesCell.appendChild(gradeList);

    const averageCell = document.createElement("td");
    averageCell.className = "average";
    averageCell.textContent = weightedAverage(subject);

    row.appendChild(subjectCell);
    row.appendChild(gradesCell);
    row.appendChild(averageCell);
    table.appendChild(row);
  });

  document.getElementById("subjectCount").textContent = subjects.length;
  document.getElementById("gradeCount").textContent = grades.length;

  const allAverage =
    grades.reduce((sum, grade) => {
      return sum + gradeToNumber(grade.value) * grade.weight;
    }, 0) /
    grades.reduce((sum, grade) => sum + grade.weight, 0);

  document.getElementById("average").textContent = allAverage.toFixed(2);
}

function showGradeInfo(grade) {
  const box = document.getElementById("gradeInfo");

  box.innerHTML = `
    <div class="panel info-box">
      <b>Szczegóły oceny \({grade.value}</b><br>
      Przedmiot: \){grade.subject}<br>
      Nauczyciel: \({teachers[grade.subject] || "Brak danych"}<br>
      Rodzaj pracy: \){grade.type}<br>
      Data: \({grade.date}<br>
      Waga: \){grade.weight}
    </div>
  `;

  box.scrollIntoView({
    behavior:"smooth",
    block:"center"
  });
}

function renderTeachers() {
  const table = document.getElementById("teachersTable");

  Object.entries(teachers).forEach(([subject, teacher]) => {
    const row = document.createElement("tr");

    row.innerHTML = `
      <td>\({subject}</td>
      <td>\){teacher}</td>
    `;

    table.appendChild(row);
  });
}

function renderSchedule() {
  const box = document.getElementById("scheduleBox");

  Object.entries(schedule).forEach(([day, lessons]) => {
    const dayBox = document.createElement("div");
    dayBox.className = "day";

    dayBox.innerHTML = `<h3>\({day}</h3>`;

    lessons.forEach(([time, subject]) => {
      const lesson = document.createElement("div");
      lesson.className = "lesson";

      lesson.innerHTML = `
        <time>\){time}</time>
        ${subject}
      `;

      dayBox.appendChild(lesson);
    });

    box.appendChild(dayBox);
  });
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
    document
      .getElementById(button.dataset.tab)
      .classList.add("active");
  });
});

renderGrades();
renderTeachers();
renderSchedule();
</script>

</body>
</html>
