<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>E-dziennik 4F</title>

<style>
:root {
  --blue:#163b68;
  --blue2:#245b98;
  --light:#f1f5f9;
  --white:#fff;
  --text:#172033;
  --muted:#64748b;
  --green:#159447;
  --red:#d62828;
  --orange:#e68a00;
  --border:#dbe3ed;
}

* { box-sizing:border-box; }

body {
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
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
  margin:0 0 6px;
  font-size:24px;
}

header p {
  margin:0;
  opacity:.9;
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

.section { display:none; }
.section.active { display:block; }

.cards {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:14px;
  margin-bottom:20px;
}

.card, .panel {
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

.card small, .muted {
  color:var(--muted);
}

h2, h3 {
  color:var(--blue);
}

table {
  width:100%;
  border-collapse:collapse;
  background:white;
  border-radius:10px;
  overflow:hidden;
}

th, td {
  padding:11px;
  border-bottom:1px solid var(--border);
  text-align:left;
  vertical-align:top;
}

th {
  background:#e9f0f8;
  color:var(--blue);
}

tr:hover td {
  background:#f8fbff;
}

.badge {
  display:inline-block;
  padding:5px 8px;
  border-radius:6px;
  font-weight:bold;
  color:white;
  margin:2px;
}

.grade { background:var(--blue2); }
.present { background:var(--green); }
.absent { background:var(--red); }
.late { background:var(--orange); }

button, input, select, textarea {
  font:inherit;
}

.action {
  border:0;
  border-radius:7px;
  padding:8px 11px;
  cursor:pointer;
  background:var(--blue);
  color:white;
}

.action.red { background:var(--red); }
.action.green { background:var(--green); }

.form {
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  margin:12px 0;
}

.form input, .form select, .form textarea {
  padding:9px;
  border:1px solid var(--border);
  border-radius:7px;
}

.form textarea {
  min-width:260px;
  min-height:80px;
}

.schedule {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
  gap:15px;
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

.message, .remark {
  padding:13px;
  border:1px solid var(--border);
  border-radius:8px;
  margin:9px 0;
  background:#fbfdff;
}

.message b, .remark b {
  color:var(--blue);
}

footer {
  text-align:center;
  color:var(--muted);
  padding:25px;
  font-size:13px;
}

@media(max-width:600px) {
  main { padding:12px; }
  th, td { padding:8px 5px; font-size:13px; }
  header h1 { font-size:20px; }
}
</style>
</head>

<body>

<header>
  <h1>Fikcyjny e-dziennik szkolny</h1>
  <p>Zespół Szkół Budowlano-Geodezyjnych · Klasa 4F</p>
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
      <strong id="attendancePercent">100%</strong>
      <small>obecności</small>
    </div>

    <div class="card">
      Średnia ocen
      <strong id="average">-</strong>
      <small>na podstawie wpisanych ocen</small>
    </div>

    <div class="card">
      Przedmioty
      <strong id="subjectCount">0</strong>
      <small>na liście klasy 4F</small>
    </div>

    <div class="card">
      Wiadomości
      <strong id="messageCount">0</strong>
      <small>zapisanych lokalnie</small>
    </div>
  </div>

  <div class="panel">
    <h3>Informacja</h3>
    <p>
      To prywatna, fikcyjna symulacja e-dziennika. Wszystkie dane są zapisywane
      wyłącznie na tym urządzeniu w pamięci przeglądarki.
    </p>
    <button class="action red" onclick="clearData()">Usuń wszystkie zapisane dane</button>
  </div>
</section>

<section id="grades" class="section">
  <h2>Oceny</h2>

  <div class="panel">
    <div class="form">
      <select id="gradeSubject"></select>
      <input id="gradeValue" placeholder="Ocena, np. 4+" maxlength="3">
      <input id="gradeType" placeholder="Rodzaj, np. sprawdzian">
      <button class="action green" onclick="addGrade()">Dodaj ocenę</button>
    </div>
  </div>

  <div class="panel">
    <table>
      <thead>
        <tr>
          <th>Przedmiot</th>
          <th>Oceny</th>
          <th>Średnia</th>
        </tr>
      </thead>
      <tbody id="gradesTable"></tbody>
    </table>
  </div>
</section>

<section id="attendance" class="section">
  <h2>Frekwencja</h2>

  <div class="panel">
    <div class="form">
      <input type="date" id="attendanceDate">
      <select id="attendanceType">
        <option value="present">Obecność</option>
        <option value="absent">Nieobecność</option>
        <option value="late">Spóźnienie</option>
      </select>
      <input id="attendanceSubject" placeholder="Przedmiot">
      <button class="action green" onclick="addAttendance()">Dodaj wpis</button>
    </div>
  </div>

  <div class="panel">
    <table>
      <thead>
        <tr>
          <th>Data</th>
          <th>Przedmiot</th>
          <th>Status</th>
          <th>Akcja</th>
        </tr>
      </thead>
      <tbody id="attendanceTable"></tbody>
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
    <div class="form">
      <select id="remarkType">
        <option value="Pozytywna">Pozytywna</option>
        <option value="Negatywna">Negatywna</option>
      </select>
      <input id="remarkTitle" placeholder="Tytuł uwagi">
      <textarea id="remarkText" placeholder="Treść uwagi"></textarea>
      <button class="action green" onclick="addRemark()">Dodaj uwagę</button>
    </div>
  </div>

  <div id="remarksBox"></div>
</section>

<section id="messages" class="section">
  <h2>Wiadomości</h2>

  <div class="panel">
    <div class="form">
      <input id="messageSender" placeholder="Nadawca">
      <input id="messageTitle" placeholder="Temat wiadomości">
      <textarea id="messageText" placeholder="Treść wiadomości"></textarea>
      <button class="action green" onclick="addMessage()">Dodaj wiadomość</button>
    </div>
  </div>

  <div id="messagesBox"></div>
</section>

</main>

<footer>
  Fikcyjny e-dziennik · Dane lokalne · Klasa 4F
</footer>

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
  "Systemy Energii Odnawialnej":"Beata Polonis",
  "Obsługa Systemów Energetyki Odnawialnej":"Beata Polonis",
  "Kształtowanie Kompetencji Zawodowych":"Beata Polonis",
  "Wychowanie Fizyczne":"Zbigniew Kulikowski",
  "Umiejętności Rynkowe - Przygotowanie do egzaminu na uprawnienia elektryczne G1":"Tomasz Rolak"
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
    ["08:00 - 08:45","Geografia"],
    ["08:55 - 09:40","Obsługa Systemów Energetyki Odnawialnej"],
    ["09:50 - 10:35","Obsługa Systemów Energetyki Odnawialnej"],
    ["10:45 - 11:30","Obsługa Systemów Energetyki Odnawialnej"],
    ["11:45 - 12:30","Obsługa Systemów Energetyki Odnawialnej"],
    ["12:40 - 13:25","Obsługa Systemów Energetyki Odnawialnej"],
    ["13:35 - 14:20","Obsługa Systemów Energetyki Odnawialnej"]
  ],
  "Piątek":[
    ["08:55 - 09:40","Wychowanie Fizyczne"],
    ["09:50 - 10:35","Wychowanie Fizyczne"],
    ["10:45 - 11:30","Matematyka"],
    ["11:45 - 12:30","Język Angielski"],
    ["12:40 - 13:25","Systemy Energii Odnawialnej"],
    ["13:35 - 14:20","Język Polski"],
    ["14:30 - 15:15","Język Angielski"]
  ]
};

let data = JSON.parse(localStorage.getItem("edziennik4F")) || {
  grades:[],
  attendance:[],
  remarks:[],
  messages:[]
};

function save() {
  localStorage.setItem("edziennik4F", JSON.stringify(data));
  render();
}

function fillSubjects() {
  const select = document.getElementById("gradeSubject");
  select.innerHTML = subjects.map(function(s) {
    return "<option>" + s + "</option>";
  }).join("");
}

function addGrade() {
  const subject = document.getElementById("gradeSubject").value;
  const value = document.getElementById("gradeValue").value.trim();
  const type = document.getElementById("gradeType").value.trim() || "Ocena";

  if (!value) return alert("Wpisz ocenę.");

  data.grades.push({subject: subject, value: value, type: type});
  document.getElementById("gradeValue").value = "";
  document.getElementById("gradeType").value = "";
  save();
}

function gradeNumber(value) {
  const match = value.replace(",", ".").match(/[1-6]/);
  return match ? Number(match[0]) : null;
}

function deleteGrade(index) {
  data.grades.splice(index, 1);
  save();
}

function renderGrades() {
  const table = document.getElementById("gradesTable");

  table.innerHTML = subjects.map(function(subject) {
    const list = data.grades.filter(function(g) { return g.subject === subject; });
    const numbers = list.map(function(g) { return gradeNumber(g.value); }).filter(Boolean);
    const avg = numbers.length
      ? (numbers.reduce(function(a, b) { return a + b; }, 0) / numbers.length).toFixed(2)
      : "-";

    const html = list.map(function(g) {
      const index = data.grades.indexOf(g);
      return '<span class="badge grade" title="' + g.type + '">' +
        g.value + ' <button onclick="deleteGrade(' + index + ')" style="border:0;background:none;color:white;cursor:pointer">×</button></span>';
    }).join("");

    return "<tr><td>" + subject + "</td><td>" + (html || '<span class="muted">Brak ocen</span>') + "</td><td>" + avg + "</td></tr>";
  }).join("");
}

function addAttendance() {
  const date = document.getElementById("attendanceDate").value;
  const type = document.getElementById("attendanceType").value;
  const subject = document.getElementById("attendanceSubject").value.trim() || "Nie podano";

  if (!date) return alert("Wybierz datę.");

  data.attendance.push({date: date, type: type, subject: subject});
  document.getElementById("attendanceSubject").value = "";
  save();
}

function deleteAttendance(index) {
  data.attendance.splice(index, 1);
  save();
}

function renderAttendance() {
  const names = {
    present: "Obecność",
    absent: "Nieobecność",
    late: "Spóźnienie"
  };

  document.getElementById("attendanceTable").innerHTML =
    data.attendance.map(function(a, i) {
      return "<tr><td>" + a.date + "</td><td>" + a.subject + "</td><td><span class=\"badge " + a.type + "\">" + names[a.type] + "</span></td><td><button class=\"action red\" onclick=\"deleteAttendance(" + i + ")\">Usuń</button></td></tr>";
    }).join("") || "<tr><td colspan=\"4\" class=\"muted\">Brak wpisów.</td></tr>";
}

function renderSchedule() {
  document.getElementById("scheduleBox").innerHTML =
    Object.entries(schedule).map(function(entry) {
      const day = entry[0];
      const lessons = entry[1];
      const items = lessons.map(function(l) {
        return "<div class=\"lesson\"><time>" + l[0] + "</time>" + l[1] + "</div>";
      }).join("");
      return "<div class=\"panel\"><h3>" + day + "</h3>" + items + "</div>";
    }).join("");
}

function renderTeachers() {
  document.getElementById("teachersTable").innerHTML =
    subjects.map(function(subject) {
      return "<tr><td>" + subject + "</td><td>" + (teachers[subject] || "Nie przypisano") + "</td></tr>";
    }).join("");
}

function addRemark() {
  const type = document.getElementById("remarkType").value;
  const title = document.getElementById("remarkTitle").value.trim();
  const text = document.getElementById("remarkText").value.trim();

  if (!title || !text) return alert("Uzupełnij tytuł i treść uwagi.");

  data.remarks.push({
    type: type,
    title: title,
    text: text,
    date: new Date().toLocaleDateString("pl-PL")
  });

  document.getElementById("remarkTitle").value = "";
  document.getElementById("remarkText").value = "";
  save();
}

function deleteRemark(index) {
  data.remarks.splice(index, 1);
  save();
}

function renderRemarks() {
  document.getElementById("remarksBox").innerHTML =
    data.remarks.map(function(r, i) {
      return "<div class=\"remark\"><b>" + r.type + ": " + r.title + "</b><small class=\"muted\"> · " + r.date + "</small><p>" + r.text + "</p><button class=\"action red\" onclick=\"deleteRemark(" + i + ")\">Usuń</button></div>";
    }).join("") || "<p class=\"muted\">Brak uwag.</p>";
}

function addMessage() {
  const sender = document.getElementById("messageSender").value.trim();
  const title = document.getElementById("messageTitle").value.trim();
  const text = document.getElementById("messageText").value.trim();

  if (!sender || !title || !text) return alert("Uzupełnij wszystkie pola.");

  data.messages.push({
    sender: sender,
    title: title,
    text: text,
    date: new Date().toLocaleDateString("pl-PL")
  });

  document.getElementById("messageSender").value = "";
  document.getElementById("messageTitle").value = "";
  document.getElementById("messageText").value = "";
  save();
}

function deleteMessage(index) {
  data.messages.splice(index, 1);
  save();
}

function renderMessages() {
  document.getElementById("messagesBox").innerHTML =
    data.messages.map(function(m, i) {
      return "<div class=\"message\"><b>" + m.title + "</b><small class=\"muted\"> · " + m.date + "</small><p><strong>Nadawca:</strong> " + m.sender + "</p><p>" + m.text + "</p><button class=\"action red\" onclick=\"deleteMessage(" + i + ")\">Usuń</button></div>";
    }).join("") || "<p class=\"muted\">Brak wiadomości.</p>";
}

function renderDashboard() {
  const numbers = data.grades
    .map(function(g) { return gradeNumber(g.value); })
    .filter(Boolean);

  const average = numbers.length
    ? (numbers.reduce(function(a, b) { return a + b; }, 0) / numbers.length).toFixed(2)
    : "-";

  const total = data.attendance.length;
  const present = data.attendance.filter(function(a) { return a.type === "present"; }).length;
  const percent = total ? Math.round((present / total) * 100) : 100;

  document.getElementById("average").textContent = average;
  document.getElementById("attendancePercent").textContent = percent + "%";
  document.getElementById("subjectCount").textContent = subjects.length;
  document.getElementById("messageCount").textContent = data.messages.length;
}

function render() {
  renderGrades();
  renderAttendance();
  renderSchedule();
  renderTeachers();
  renderRemarks();
  renderMessages();
  renderDashboard();
}

function clearData() {
  if (confirm("Czy na pewno usunąć wszystkie lokalne dane?")) {
    data = {
      grades:[],
      attendance:[],
      remarks:[],
      messages:[]
    };
    save();
  }
}

document.querySelectorAll(".tab").forEach(function(button) {
  button.addEventListener("click", function() {
    document.querySelectorAll(".tab").forEach(function(b) { b.classList.remove("active"); });
    document.querySelectorAll(".section").forEach(function(s) { s.classList.remove("active"); });

    button.classList.add("active");
    document.getElementById(button.dataset.tab).classList.add("active");
  });
});

fillSubjects();
render();
</script>

</body>
</html>
