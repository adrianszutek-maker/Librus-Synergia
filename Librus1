<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Elektroniczny Dziennik</title>

<style>
:root {
  --bg: #0d1421;
  --panel: #172235;
  --panel-light: #1e2d46;
  --border: #2b3b57;
  --text: #f1f5f9;
  --muted: #9aa9bd;
  --blue: #2563eb;
  --red: #dc3545;
  --orange: #e89216;
  --green: #159447;
  --purple: #7655c9;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: Arial, Helvetica, sans-serif;
}

header {
  padding: 18px;
  background: #14233a;
  border-bottom: 1px solid var(--border);
}

.header-title {
  font-size: 21px;
  font-weight: bold;
}

.student {
  margin-top: 6px;
  color: var(--muted);
  font-size: 14px;
}

nav {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding: 12px;
  background: #111b2c;
  border-bottom: 1px solid var(--border);
  position: sticky;
  top: 0;
  z-index: 5;
}

nav button {
  padding: 9px 12px;
  border: 1px solid var(--border);
  border-radius: 7px;
  background: var(--panel);
  color: var(--muted);
  font-weight: bold;
  cursor: pointer;
}

nav button.active,
nav button:hover {
  background: var(--blue);
  color: white;
  border-color: var(--blue);
}

main {
  max-width: 950px;
  margin: auto;
  padding: 18px;
}

.section {
  display: none;
}

.section.active {
  display: block;
}

h2 {
  margin: 0 0 15px;
  font-size: 21px;
}

.panel,
.stat-card,
.day-card {
  margin-bottom: 15px;
  padding: 16px;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 12px;
}

.stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(145px, 1fr));
  gap: 12px;
  margin-bottom: 16px;
}

.stat-card span {
  display: block;
  color: var(--muted);
  font-size: 13px;
}

.stat-card strong {
  display: block;
  margin-top: 6px;
  color: white;
  font-size: 25px;
}

.subject-row {
  padding: 14px 0;
  border-bottom: 1px solid var(--border);
}

.subject-row:last-child {
  border-bottom: 0;
}

.subject-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  margin-bottom: 9px;
}

.subject-name {
  font-weight: bold;
}

.average {
  color: #62b5ff;
  font-size: 14px;
  white-space: nowrap;
}

.grades {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
}

.grade {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border: 1px solid #ffffff55;
  border-radius: 7px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.15s;
}

.grade:hover {
  transform: scale(1.08);
}

.sprawdzian {
  background: var(--red);
}

.kartkowka {
  background: var(--orange);
}

.odpowiedz {
  background: var(--green);
}

.praca {
  background: var(--purple);
}

.no-grades,
.muted {
  color: var(--muted);
  font-size: 13px;
  font-style: italic;
}

.lesson {
  display: flex;
  gap: 12px;
  padding: 8px 0;
  border-bottom: 1px solid var(--border);
  font-size: 14px;
}

.lesson:last-child {
  border-bottom: 0;
}

.time {
  flex-shrink: 0;
  width: 105px;
  color: var(--muted);
  font-family: monospace;
}

.day-title {
  padding-bottom: 9px;
  border-bottom: 1px solid var(--border);
  color: #67aafc;
  font-weight: bold;
}

.info-item {
  padding: 12px 0;
  border-bottom: 1px solid var(--border);
}

.info-item:last-child {
  border-bottom: 0;
}

.info-item b {
  display: block;
  margin-bottom: 4px;
}

.info-item span {
  color: var(--muted);
  font-size: 14px;
}

.present {
  color: #35d477 !important;
  font-style: normal;
}

.modal {
  display: none;
  position: fixed;
  inset: 0;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: #000b;
  z-index: 10;
}

.modal-box {
  width: 100%;
  max-width: 340px;
  padding: 20px;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 13px;
}

.modal-box h3 {
  margin-top: 0;
}

.modal-box p {
  color: var(--muted);
  font-size: 14px;
}

.modal-box b {
  color: white;
}

.close {
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  border: 0;
  border-radius: 7px;
  background: var(--blue);
  color: white;
  font-weight: bold;
  cursor: pointer;
}

footer {
  padding: 20px;
  color: var(--muted);
  text-align: center;
  font-size: 12px;
}

@media (max-width: 600px) {
  main {
    padding: 12px;
  }

  .subject-header {
    align-items: flex-start;
    flex-direction: column;
  }

  nav button {
    padding: 8px 10px;
    font-size: 12px;
  }
}
</style>
</head>

<body>

<header>
  <div class="header-title">Elektroniczny Dziennik</div>
  <div class="student">Adrian Szutko · klasa 4F · uczeń</div>
</header>

<nav>
  <button class="active" onclick="showTab('start', this)">Start</button>
  <button onclick="showTab('grades', this)">Oceny</button>
  <button onclick="showTab('attendance', this)">Frekwencja</button>
  <button onclick="showTab('schedule', this)">Plan lekcji</button>
  <button onclick="showTab('teachers', this)">Nauczyciele</button>
  <button onclick="showTab('remarks', this)">Uwagi</button>
  <button onclick="showTab('messages', this)">Wiadomości</button>
</nav>

<main>

<section id="start" class="section active">
  <h2>Panel główny</h2>

  <div class="stats">
    <div class="stat-card">
      <span>Średnia ważona</span>
      <strong id="generalAverage">-</strong>
    </div>

    <div class="stat-card">
      <span>Frekwencja</span>
      <strong id="attendanceAverage">-</strong>
    </div>

    <div class="stat-card">
      <span>Uczeń</span>
      <strong>4F</strong>
    </div>
  </div>

  <div class="panel">
    <h2>Najbliższe zajęcia</h2>
    <div id="nextLessons"></div>
  </div>
</section>

<section id="grades" class="section">
  <h2>Oceny</h2>
  <div class="panel">
    <div id="gradesContainer"></div>
  </div>
</section>

<section id="attendance" class="section">
  <h2>Frekwencja</h2>

  <div class="panel">
    <p id="attendanceSummary"></p>
    <div id="attendanceContainer"></div>
  </div>
</section>

<section id="schedule" class="section">
  <h2>Plan lekcji</h2>
  <div id="scheduleContainer"></div>
</section>

<section id="teachers" class="section">
  <h2>Nauczyciele</h2>
  <div class="panel" id="teachersContainer"></div>
</section>

<section id="remarks" class="section">
  <h2>Uwagi</h2>

  <div class="panel">
    <div class="info-item">
      <b class="present">Pozytywna - aktywność na zajęciach zawodowych</b>
      <span>
        Wzorowe przygotowanie stanowiska pomiarowego podczas ćwiczeń z fotowoltaiki.
        Wpisała: Beata Polonis.
      </span>
    </div>

    <div class="info-item">
      <b>Informacyjna - udział w konkursie</b>
      <span>
        Zgłoszenie do etapu szkolnego olimpiady wiedzy technicznej.
        Wpisał: Paweł Klim.
      </span>
    </div>
  </div>
</section>

<section id="messages" class="section">
  <h2>Wiadomości</h2>

  <div class="panel">
    <div class="info-item">
      <b>Tomasz Rolak - materiały na uprawnienia G1</b>
      <span>
        Zestaw pytań egzaminacyjnych z ochrony przeciwporażeniowej
        został udostępniony na dysku szkolnym.
      </span>
    </div>
  </div>
</section>

</main>

<footer>
  Elektroniczny Dziennik · Adrian Szutko · Klasa 4F
</footer>

<div id="gradeModal" class="modal" onclick="closeModal(event)">
  <div class="modal-box">
    <h3 id="modalSubject"></h3>
    <p>Ocena: <b id="modalGrade"></b></p>
    <p>Rodzaj pracy: <b id="modalType"></b></p>
    <p>Waga: <b id="modalWeight"></b></p>
    <p>Data: <b id="modalDate"></b></p>
    <p>Nauczyciel: <b id="modalTeacher"></b></p>
    <button class="close" onclick="closeGradeModal()">Zamknij</button>
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
  "Umiejętności Rynkowe - przygotowanie do egzaminu G1"
];

const teachers = {
  "Język Polski": "Dorota Puciłowska",
  "Matematyka": "Joanna Wasilewska",
  "Język Angielski": "Anna Mróz",
  "Język Angielski w Budownictwie": "Anna Mróz",
  "Fizyka": "Paweł Klim",
  "Fizyka Techniczna": "Paweł Klim",
  "Geografia": "Wiesława Kolosa",
  "Historia": "Robert Jan Peciak",
  "Język Niemiecki": "Dorota Cyrulik",
  "Kształtowanie Kompetencji Zawodowych": "Beata Polonis",
  "Obsługa Systemów Energetyki Odnawialnej": "Beata Polonis",
  "Systemy Energii Odnawialnej": "Beata Polonis",
  "Wychowanie Fizyczne": "Zbigniew Kulikowski",
  "Umiejętności Rynkowe - przygotowanie do egzaminu G1": "Tomasz Rolak"
};

const gradesData = {
  "Język Polski": [
    { value: "3", type: "Kartkówka", date: "12.10.2026" }
  ],

  "Systemy Energii Odnawialnej": [
    { value: "3", type: "Kartkówka", date: "21.09.2026" },
    { value: "3", type: "Kartkówka", date: "09.10.2026" }
  ],

  "Wychowanie Fizyczne": [
    { value: "5", type: "Sprawdzian", date: "22.09.2026" },
    { value: "5-", type: "Praca na lekcji", date: "06.10.2026" }
  ],

  "Obsługa Systemów Energetyki Odnawialnej": [
    { value: "3", type: "Odpowiedź ustna", date: "10.09.2026" },
    { value: "4-", type: "Kartkówka", date: "17.09.2026" }
  ],

  "Język Angielski w Budownictwie": [
    { value: "6", type: "Kartkówka", date: "25.09.2026" }
  ],

  "Język Angielski": [
    { value: "4", type: "Kartkówka", date: "09.10.2026" }
  ],

  "Geografia": [
    { value: "3", type: "Sprawdzian", date: "04.10.2026" },
    { value: "3", type: "Kartkówka", date: "27.09.2026" }
  ],

  "Fizyka Techniczna": [
    { value: "4", type: "Praca na lekcji", date: "05.10.2026" },
    { value: "2", type: "Praca na lekcji", date: "12.10.2026" }
  ],

  "Fizyka": [
    { value: "4", type: "Kartkówka", date: "29.09.2026" },
    { value: "3", type: "Praca na lekcji", date: "30.09.2026" }
  ]
};

const weights = {
  "Sprawdzian": 4,
  "Kartkówka": 2,
  "Odpowiedź ustna": 1,
  "Praca na lekcji": 1
};

const lessonSchedule = {
  "Poniedziałek": [
    ["08:00 - 08:45", "Język Polski"],
    ["08:55 - 09:40", "Język Polski"],
    ["09:50 - 10:35", "Matematyka"],
    ["10:45 - 11:30", "Fizyka Techniczna"],
    ["11:45 - 12:30", "Systemy Energii Odnawialnej"],
    ["12:40 - 13:25", "Geografia"],
    ["13:35 - 14:20", "Umiejętności Rynkowe - przygotowanie do egzaminu G1"],
    ["14:30 - 15:15", "Umiejętności Rynkowe - przygotowanie do egzaminu G1"],
    ["15:20 - 16:05", "Historia"]
  ],

  "Wtorek": [
    ["09:50 - 10:35", "Systemy Energii Odnawialnej"],
    ["10:45 - 11:30", "Systemy Energii Odnawialnej"],
    ["11:45 - 12:30", "Matematyka"],
    ["12:40 - 13:25", "Fizyka"],
    ["13:35 - 14:20", "Wychowanie Fizyczne"],
    ["14:30 - 15:15", "Język Angielski"]
  ],

  "Środa": [
    ["08:55 - 09:40", "Fizyka"],
    ["09:50 - 10:35", "Język Angielski w Budownictwie"],
    ["10:45 - 11:30", "Zajęcia z wychowawcą"],
    ["11:45 - 12:30", "Matematyka"],
    ["12:40 - 13:25", "Kształtowanie Kompetencji Zawodowych"]
  ],

  "Czwartek": [
    ["08:00 - 08:45", "Geografia"],
    ["08:55 - 09:40", "Obsługa Systemów Energetyki Odnawialnej"],
    ["09:50 - 10:35", "Obsługa Systemów Energetyki Odnawialnej"],
    ["10:45 - 11:30", "Obsługa Systemów Energetyki Odnawialnej"],
    ["11:45 - 12:30", "Obsługa Systemów Energetyki Odnawialnej"],
    ["12:40 - 13:25", "Obsługa Systemów Energetyki Odnawialnej"],
    ["13:35 - 14:20", "Obsługa Systemów Energetyki Odnawialnej"]
  ],

  "Piątek": [
    ["08:55 - 09:40", "Wychowanie Fizyczne"],
    ["09:50 - 10:35", "Wychowanie Fizyczne"],
    ["10:45 - 11:30", "Matematyka"],
    ["11:45 - 12:30", "Język Angielski"],
    ["12:40 - 13:25", "Systemy Energii Odnawialnej"],
    ["13:35 - 14:20", "Język Polski"],
    ["14:30 - 15:15", "Język Angielski"]
  ]
};

const dayNames = [
  "Niedziela",
  "Poniedziałek",
  "Wtorek",
  "Środa",
  "Czwartek",
  "Piątek",
  "Sobota"
];

function gradeToNumber(value) {
  if (value.endsWith("+")) {
    return Number(value[0]) + 0.25;
  }

  if (value.endsWith("-")) {
    return Number(value[0]) - 0.25;
  }

  return Number(value);
}

function typeClass(type) {
  if (type === "Sprawdzian") return "sprawdzian";
  if (type === "Kartkówka") return "kartkowka";
  if (type === "Odpowiedź ustna") return "odpowiedz";
  return "praca";
}

function subjectAverage(grades) {
  if (!grades || grades.length === 0) {
    return "-";
  }

  let sum = 0;
  let weightSum = 0;

  grades.forEach(grade => {
    const weight = weights[grade.type] || 1;
    sum += gradeToNumber(grade.value) * weight;
    weightSum += weight;
  });

  return (sum / weightSum).toFixed(2);
}

function renderGrades() {
  const container = document.getElementById("gradesContainer");
  container.innerHTML = "";

  let totalSum = 0;
  let totalWeights = 0;

  subjects.forEach(subject => {
    const grades = gradesData[subject] || [];

    const row = document.createElement("div");
    row.className = "subject-row";

    const header = document.createElement("div");
    header.className = "subject-header";

    const name = document.createElement("div");
    name.className = "subject-name";
    name.textContent = subject;

    const average = document.createElement("div");
    average.className = "average";
    average.textContent = "Średnia: " + subjectAverage(grades);

    header.appendChild(name);
    header.appendChild(average);
    row.appendChild(header);

    if (grades.length === 0) {
      const empty = document.createElement("div");
      empty.className = "no-grades";
      empty.textContent = "Brak ocen";
      row.appendChild(empty);
    } else {
      const gradesBox = document.createElement("div");
      gradesBox.className = "grades";

      grades.forEach(grade => {
        const box = document.createElement("div");
        box.className = "grade " + typeClass(grade.type);
        box.textContent = grade.value;

        box.onclick = function() {
          openGradeModal(subject, grade);
        };

        gradesBox.appendChild(box);

        const weight = weights[grade.type] || 1;
        totalSum += gradeToNumber(grade.value) * weight;
        totalWeights += weight;
      });

      row.appendChild(gradesBox);
    }

    container.appendChild(row);
  });

  const generalAverage = totalWeights > 0
    ? (totalSum / totalWeights).toFixed(2)
    : "-";

  document.getElementById("generalAverage").textContent = generalAverage;
}

function renderSchedule() {
  const container = document.getElementById("scheduleContainer");
  container.innerHTML = "";

  Object.entries(lessonSchedule).forEach(([day, lessons]) => {
    const card = document.createElement("div");
    card.className = "day-card";

    const title = document.createElement("div");
    title.className = "day-title";
    title.textContent = day;
    card.appendChild(title);

    lessons.forEach(([time, subject]) => {
      const lesson = document.createElement("div");
      lesson.className = "lesson";

      const timeBox = document.createElement("span");
      timeBox.className = "time";
      timeBox.textContent = time;

      const subjectBox = document.createElement("span");
      subjectBox.textContent = subject;

      lesson.appendChild(timeBox);
      lesson.appendChild(subjectBox);
      card.appendChild(lesson);
    });

    container.appendChild(card);
  });
}

function renderNextLessons() {
  const container = document.getElementById("nextLessons");
  container.innerHTML = "";

  const lessons = lessonSchedule["Poniedziałek"].slice(0, 3);

  lessons.forEach(([time, subject]) => {
    const lesson = document.createElement("div");
    lesson.className = "lesson";

    const timeBox = document.createElement("span");
    timeBox.className = "time";
    timeBox.textContent = time;

    const subjectBox = document.createElement("span");
    subjectBox.textContent = subject;

    lesson.appendChild(timeBox);
    lesson.appendChild(subjectBox);
    container.appendChild(lesson);
  });
}

function renderTeachers() {
  const container = document.getElementById("teachersContainer");
  container.innerHTML = "";

  subjects.forEach(subject => {
    const item = document.createElement("div");
    item.className = "info-item";

    const teacher = document.createElement("b");
    teacher.textContent = teachers[subject] || "Nie podano";

    const name = document.createElement("span");
    name.textContent = subject;

    item.appendChild(teacher);
    item.appendChild(name);
    container.appendChild(item);
  });
}

function formatDate(date) {
  const day = String(date.getDate()).padStart(2, "0");
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const year = date.getFullYear();

  return day + "." + month + "." + year;
}

function renderAttendance() {
  const container = document.getElementById("attendanceContainer");
  const summary = document.getElementById("attendanceSummary");

  container.innerHTML = "";

  const startDate = new Date(2026, 8, 2);
  const endDate = new Date(2026, 9, 21);

  let totalLessons = 0;

  for (
    let date = new Date(startDate);
    date <= endDate;
    date.setDate(date.getDate() + 1)
  ) {
    const dayName = dayNames[date.getDay()];
    const lessons = lessonSchedule[dayName];

    if (!lessons) {
      continue;
    }

    lessons.forEach(([time, subject]) => {
      totalLessons++;

      const item = document.createElement("div");
      item.className = "info-item";

      const title = document.createElement("b");
      title.textContent = formatDate(date) + " - " + subject;

      const status = document.createElement("span");
      status.className = "present";
      status.textContent = "Obecność";

      item.appendChild(title);
      item.appendChild(status);
      container.appendChild(item);
    });
  }

  summary.textContent =
    "Obecności: " + totalLessons +
    " / " + totalLessons +
    " lekcji. Frekwencja: 100%.";

  document.getElementById("attendanceAverage").textContent = "100%";
}

function openGradeModal(subject, grade) {
  document.getElementById("modalSubject").textContent = subject;
  document.getElementById("modalGrade").textContent = grade.value;
  document.getElementById("modalType").textContent = grade.type;
  document.getElementById("modalWeight").textContent =
    weights[grade.type] || 1;
  document.getElementById("modalDate").textContent = grade.date;
  document.getElementById("modalTeacher").textContent =
    teachers[subject] || "Nie podano";

  document.getElementById("gradeModal").style.display = "flex";
}

function closeGradeModal() {
  document.getElementById("gradeModal").style.display = "none";
}

function closeModal(event) {
  if (event.target.id === "gradeModal") {
    closeGradeModal();
  }
}

function showTab(id, button) {
  document.querySelectorAll(".section").forEach(section => {
    section.classList.remove("active");
  });

  document.querySelectorAll("nav button").forEach(navButton => {
    navButton.classList.remove("active");
  });

  document.getElementById(id).classList.add("active");
  button.classList.add("active");
}

renderGrades();
renderSchedule();
renderNextLessons();
renderTeachers();
renderAttendance();
</script>

</body>
</html>
