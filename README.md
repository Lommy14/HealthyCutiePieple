<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>เกมคำนวณแคลอรี่ & การออกกำลังกาย</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: "Sarabun", system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      padding: 0;
      background: #f3f6fb;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
    }

    .container {
      max-width: 1100px;
      width: 100%;
      margin: 24px;
      background: #ffffff;
      border-radius: 16px;
      padding: 24px 28px 32px;
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
    }

    h1 {
      margin-top: 0;
      font-size: 26px;
      text-align: center;
      color: #1f3b70;
    }

    h2 {
      font-size: 20px;
      margin-bottom: 8px;
      color: #1f3b70;
    }

    p {
      margin: 4px 0 8px;
      font-size: 14px;
      color: #444;
    }

    .flex {
      display: flex;
      gap: 16px;
      flex-wrap: wrap;
    }

    .card {
      background: #f9fbff;
      border-radius: 12px;
      padding: 16px 18px;
      flex: 1 1 320px;
      min-width: 260px;
      border: 1px solid #e2e8f0;
    }

    label {
      font-size: 14px;
      font-weight: 600;
      color: #1e293b;
      display: block;
      margin-bottom: 6px;
    }

    select, input[type="number"] {
      width: 100%;
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid #cbd5e1;
      font-size: 14px;
      outline: none;
    }

    select:focus, input[type="number"]:focus {
      border-color: #2563eb;
      box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.18);
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 8px 16px;
      font-size: 14px;
      cursor: pointer;
      background: #2563eb;
      color: #ffffff;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 4px;
      margin-top: 8px;
    }

    button.small {
      padding: 6px 12px;
      font-size: 13px;
    }

    button:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    .badge {
      display: inline-block;
      padding: 3px 10px;
      border-radius: 999px;
      font-size: 12px;
      background: #e0edff;
      color: #1d4ed8;
      margin-right: 4px;
    }

    .age-info {
      font-size: 13px;
      margin-top: 6px;
      color: #475569;
    }

    .tabs {
      display: flex;
      margin-top: 16px;
      margin-bottom: 8px;
      border-radius: 999px;
      background: #e2e8f0;
      padding: 4px;
    }

    .tab {
      flex: 1;
      text-align: center;
      padding: 8px 10px;
      font-size: 14px;
      cursor: pointer;
      border-radius: 999px;
      transition: background 0.2s, color 0.2s;
      user-select: none;
    }

    .tab.active {
      background: #ffffff;
      color: #1d4ed8;
      font-weight: 600;
      box-shadow: 0 1px 4px rgba(15, 23, 42, 0.15);
    }

    .tab-content {
      margin-top: 12px;
    }

    .question-box {
      margin-top: 8px;
      padding: 12px;
      border-radius: 12px;
      background: #ffffff;
      border: 1px solid #e2e8f0;
    }

    .question-title {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 6px;
      color: #0f172a;
    }

    .question-sub {
      font-size: 13px;
      color: #64748b;
      margin-bottom: 8px;
    }

    .status-row {
      display: flex;
      justify-content: space-between;
      font-size: 13px;
      color: #475569;
      margin-top: 8px;
    }

    .result {
      margin-top: 8px;
      padding: 8px 10px;
      border-radius: 8px;
      font-size: 13px;
      background: #eff6ff;
      color: #1d4ed8;
    }

    .result.error {
      background: #fef2f2;
      color: #b91c1c;
    }

    .summary {
      margin-top: 10px;
      padding: 10px;
      border-radius: 10px;
      background: #f1f5f9;
      font-size: 13px;
      color: #0f172a;
    }

    .pill-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 4px;
    }

    .pill {
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 12px;
      background: #e5e7eb;
      color: #374151;
    }

    .hint {
      font-size: 12px;
      color: #6b7280;
      margin-top: 4px;
    }

    .disclaimer {
      margin-top: 16px;
      font-size: 11px;
      color: #6b7280;
      border-top: 1px dashed #cbd5e1;
      padding-top: 8px;
    }
  </style>
</head>

<body>
<div class="container">
  <h1>🎮 เกมคำนวณแคลอรี่ & การออกกำลังกายในชีวิตประจำวัน</h1>
  <p style="text-align:center;font-size:13px;color:#64748b;">
    เลือกช่วงอายุ → เล่นเกมทายแคลอรี่อาหาร → ดูว่าจะเผาผลาญด้วยการออกกำลังกายส่วนไหนของร่างกายได้บ้าง
  </p>

  <!-- เลือกช่วงอายุ -->
  <div class="card" style="margin-bottom:12px;">
    <h2>1️⃣ เลือกช่วงอายุ</h2>
    <label for="ageGroup">ช่วงอายุของผู้เล่น</label>
    <select id="ageGroup">
      <option value="teen">13–18 ปี (วัยรุ่น)</option>
      <option value="adult">19–59 ปี (ผู้ใหญ่)</option>
      <option value="child">7–12 ปี (เด็ก)</option>
      <option value="senior">60 ปีขึ้นไป (ผู้สูงอายุ)</option>
    </select>
    <div id="ageInfo" class="age-info"></div>
  </div>

  <!-- Tabs -->
  <div class="tabs">
    <div class="tab active" data-tab="food">โหมดที่ 1: เกมทายแคลอรี่อาหาร</div>
    <div class="tab" data-tab="exercise">โหมดที่ 2: เกมเลือกการออกกำลังกาย</div>
  </div>

  <div class="tab-content">
    <!-- FOOD TAB -->
    <div id="tab-food">
      <div class="flex">

        <!-- เกมทายอาหาร -->
        <div class="card">
          <h2>2️⃣ เกมทายแคลอรี่</h2>
          <p>ระบบจะสุ่มอาหาร/เครื่องดื่มมาให้ 1 อย่าง ให้ลองเดาว่ามีแคลอรี่ประมาณเท่าไร</p>

          <button id="btnNewQuestion">เริ่มคำถามใหม่ / เปลี่ยนเมนู</button>

          <div id="foodQuestionBox" class="question-box" style="display:none;">
            <div class="badge" id="foodIndexBadge">คำถามข้อ 1/5</div>
            <div class="question-title" id="foodName">ชื่ออาหาร</div>
            <div class="question-sub">ลองเดาแคลอรี่ (kcal)</div>

            <label for="calInput">กรอกแคลอรี่ที่คุณเดา</label>
            <input type="number" id="calInput" placeholder="เช่น 250" min="0">
            <button id="btnCheckFood" class="small">ตรวจคำตอบ</button>

            <div class="hint">จะถือว่าถูกถ้าเดาใกล้เคียง ±50 kcal</div>

            <div id="foodResult" class="result" style="display:none;"></div>

            <div class="status-row">
              <span>คะแนน: <strong id="scoreText">0</strong></span>
              <span>แคลอรี่สะสม: <strong id="totalEaten">0</strong> kcal</span>
            </div>
          </div>

          <div id="foodSummary" class="summary" style="display:none;"></div>
        </div>

        <!-- ตัวอย่างเมนู -->
        <div class="card">
          <h2>🍚 ตัวอย่างเมนูในเกม</h2>
          <p>อาหารไทยและเครื่องดื่มในชีวิตประจำวัน</p>
          <div class="pill-row" id="foodListPreview"></div>
        </div>
      </div>
    </div>

    <!-- EXERCISE TAB -->
    <div id="tab-exercise" style="display:none;">
      <div class="flex">

        <!-- แบบออกกำลังกาย -->
        <div class="card">
          <h2>3️⃣ เลือกส่วนของร่างกาย</h2>

          <label for="bodyPart">ส่วนของร่างกาย</label>
          <select id="bodyPart">
            <option value="legs">ขา / ระบบหัวใจ</option>
            <option value="arms">แขน / ไหล่</option>
            <option value="core">ลำตัว / หน้าท้อง</option>
            <option value="full">ทั้งตัว</option>
          </select>

          <label for="exerciseSelect" style="margin-top:10px;">ท่าออกกำลังกาย</label>
          <select id="exerciseSelect"></select>

          <label for="minutesInput" style="margin-top:10px;">ระยะเวลา (นาที)</label>
          <input type="number" id="minutesInput" value="30" min="5" step="5">

          <button id="btnCalcBurn">คำนวณแคลอรี่ที่เผาผลาญ</button>

          <div id="exerciseResult" class="result" style="display:none;"></div>
          <div class="summary" id="compareSummary" style="display:none;"></div>
        </div>

        <!-- ตัวอย่างท่าออกกำลังกาย -->
        <div class="card">
          <h2>🏃‍♀️ ตัวอย่างท่าออกกำลังกาย</h2>
          <ul style="font-size:13px;color:#475569;padding-left:18px;">
            <li>สควอท: ~6 kcal/นาที</li>
            <li>วิดพื้น: ~7 kcal/นาที</li>
            <li>Mountain Climber: ~8 kcal/นาที</li>
            <li>Jumping Jack: ~8 kcal/นาที</li>
            <li>Burpee: ~12 kcal/นาที</li>
            <li>กระโดดเชือก: ~10 kcal/นาที</li>
          </ul>
        </div>

      </div>
    </div>

  </div>

  <div class="disclaimer">
    ⚠️ เกมนี้ใช้ค่าประมาณเพื่อการศึกษาเท่านั้น ไม่ใช่คำแนะนำด้านโภชนาการจริง
  </div>

</div>

<script>
  /* -----------------------------------------------------
      1) ข้อมูลช่วงอายุ
  ----------------------------------------------------- */
  const ageGroups = {
    child: {
      label: "7–12 ปี (เด็ก)",
      recommend: "1,600–2,000 kcal/วัน"
    },
    teen: {
      label: "13–18 ปี (วัยรุ่น)",
      recommend: "2,000–2,400 kcal/วัน"
    },
    adult: {
      label: "19–59 ปี (ผู้ใหญ่)",
      recommend: "1,800–2,400 kcal/วัน"
    },
    senior: {
      label: "60 ปีขึ้นไป (ผู้สูงอายุ)",
      recommend: "1,600–2,000 kcal/วัน"
    }
  };

  /* -----------------------------------------------------
      2) อาหารตัวอย่าง (เพิ่มหลากหลาย)
  ----------------------------------------------------- */
  const foods = [
    { name: "ข้าวมันไก่", calories: 600 },
    { name: "ข้าวขาหมู", calories: 700 },
    { name: "ข้าวผัดหมู", calories: 680 },
    { name: "กะเพราไก่ + ไข่ดาว", calories: 650 },
    { name: "ข้าวไข่เจียว", calories: 450 },
    { name: "ก๋วยเตี๋ยวเรือ", calories: 320 },
    { name: "ก๋วยเตี๋ยวผัดไทย", calories: 550 },
    { name: "ส้มตำไทย", calories: 120 },
    { name: "ส้มตำปูปลาร้า", calories: 80 },
    { name: "ไก่ทอด 1 ชิ้น", calories: 350 },
    { name: "หมูปิ้ง 1 ไม้", calories: 90 },
    { name: "ลูกชิ้นปิ้ง 1 ไม้", calories: 70 },

    { name: "ขนมครก 2 ชิ้น", calories: 200 },
    { name: "บัวลอย", calories: 280 },
    { name: "เฉาก๊วย", calories: 180 },
    { name: "ไอศกรีม 1 ก้อน", calories: 140 },
    { name: "เครปญี่ปุ่น", calories: 330 },

    { name: "ชานมไข่มุก", calories: 300 },
    { name: "ชาไทยเย็น", calories: 250 },
    { name: "โอเลี้ยง", calories: 220 },
    { name: "โค้กกระป๋อง", calories: 140 },
    { name: "น้ำส้ม", calories: 110 },
    { name: "ลาเต้หวานน้อย", calories: 150 },
    { name: "นมจืด UHT", calories: 130 },

    { name: "ป๊อบคอร์นหวาน", calories: 300 },
    { name: "มันฝรั่งทอดซอง", calories: 500 },
    { name: "ขนมปังไส้ช็อกโกแลต", calories: 270 },
    { name: "เบอร์เกอร์หมู", calories: 550 },
    { name: "ไก่ทอด KFC (น่อง)", calories: 280 },

    { name: "กล้วยหอม 1 ผล", calories: 90 },
    { name: "แตงโม 1 ชิ้น", calories: 30 },
    { name: "ลำไย 10 เม็ด", calories: 60 },
    { name: "ทุเรียน 1 เม็ด", calories: 130 },
    { name: "มะม่วงสุก", calories: 135 },

    { name: "สลัดผัก + น้ำสลัดงา", calories: 90 },
    { name: "อกไก่ย่าง 100 กรัม", calories: 165 },
    { name: "ไข่ต้ม 1 ฟอง", calories: 70 },
    { name: "แซนวิชโฮลวีทไก่", calories: 240 }
  ];

  /* -----------------------------------------------------
      3) ท่าออกกำลังกายใหม่ (ครบทุกส่วน)
  ----------------------------------------------------- */
  const exercises = [
    // legs
    { part: "legs", name: "เดินเร็ว", burnPerMin: 4 },
    { part: "legs", name: "วิ่งเหยาะ", burnPerMin: 8 },
    { part: "legs", name: "อินเตอร์วัลรัน", burnPerMin: 9 },
    { part: "legs", name: "สควอท", burnPerMin: 6 },
    { part: "legs", name: "ลันจ์", burnPerMin: 6 },
    { part: "legs", name: "เตะขาเข้าต้นขา", burnPerMin: 5 },

    // arms
    { part: "arms", name: "วิดพื้น", burnPerMin: 7 },
    { part: "arms", name: "ดัมเบลเบาๆ", burnPerMin: 5 },
    { part: "arms", name: "Lateral Raise", burnPerMin: 4 },
    { part: "arms", name: "Wall Push-Up", burnPerMin: 4 },
    { part: "arms", name: "Arm Circle", burnPerMin: 3 },
    { part: "arms", name: "Triceps Dip", burnPerMin: 6 },

    // core
    { part: "core", name: "ซิทอัพ", burnPerMin: 5 },
    { part: "core", name: "แพลงก์", burnPerMin: 5 },
    { part: "core", name: "ครันช์", burnPerMin: 4 },
    { part: "core", name: "Russian Twist", burnPerMin: 6 },
    { part: "core", name: "Mountain Climber", burnPerMin: 8 },
    { part: "core", name: "Leg Raise", burnPerMin: 5 },

    // full
    { part: "full", name: "ปั่นจักรยาน", burnPerMin: 7 },
    { part: "full", name: "กระโดดเชือก", burnPerMin: 10 },
    { part: "full", name: "Burpee", burnPerMin: 12 },
    { part: "full", name: "Jumping Jack", burnPerMin: 8 },
    { part: "full", name: "โยคะเบา ๆ", burnPerMin: 3 },
    { part: "full", name: "เต้นแอโรบิก", burnPerMin: 7 },
    { part: "full", name: "เต้น K-Pop", burnPerMin: 9 }
  ];

  /* -----------------------------------------------------
      4) ระบบแสดงข้อมูลช่วงอายุ
  ----------------------------------------------------- */
  const ageGroupSelect = document.getElementById("ageGroup");
  const ageInfoDiv = document.getElementById("ageInfo");

  function updateAgeInfo() {
    const key = ageGroupSelect.value;
    const info = ageGroups[key];
    ageInfoDiv.innerHTML =
      `<span class="badge">${info.label}</span> ต้องการพลังงานประมาณ <strong>${info.recommend}</strong>`;
  }
  updateAgeInfo();
  ageGroupSelect.addEventListener("change", updateAgeInfo);

  /* -----------------------------------------------------
      5) ระบบแท็บ
  ----------------------------------------------------- */
  const tabs = document.querySelectorAll(".tab");
  const tabFood = document.getElementById("tab-food");
  const tabExercise = document.getElementById("tab-exercise");

  tabs.forEach(tab => {
    tab.addEventListener("click", () => {
      tabs.forEach(t => t.classList.remove("active"));
      tab.classList.add("active");

      if (tab.dataset.tab === "food") {
        tabFood.style.display = "block";
        tabExercise.style.display = "none";
      } else {
        tabFood.style.display = "none";
        tabExercise.style.display = "block";
      }
    });
  });

  /* -----------------------------------------------------
      6) แสดงตัวอย่างอาหาร
  ----------------------------------------------------- */
  const foodListPreview = document.getElementById("foodListPreview");

  function renderFoodPreview() {
    foodListPreview.innerHTML = "";
    foods.forEach(f => {
      const pill = document.createElement("div");
      pill.className = "pill";
      pill.textContent = `${f.name} ~ ${f.calories} kcal`;
      foodListPreview.appendChild(pill);
    });
  }
  renderFoodPreview();

  /* -----------------------------------------------------
      7) เกมอาหาร
  ----------------------------------------------------- */
  let currentFood = null;
  let questionIndex = 0;
  const maxQuestions = 5;
  let score = 0;
  let totalEatenCalories = 0;
  let gameFinished = false;

  const btnNewQuestion = document.getElementById("btnNewQuestion");
  const foodQuestionBox = document.getElementById("foodQuestionBox");
  const foodNameDiv = document.getElementById("foodName");
  const foodIndexBadge = document.getElementById("foodIndexBadge");
  const calInput = document.getElementById("calInput");
  const btnCheckFood = document.getElementById("btnCheckFood");
  const foodResult = document.getElementById("foodResult");
  const scoreText = document.getElementById("scoreText");
  const totalEaten = document.getElementById("totalEaten");
  const foodSummary = document.getElementById("foodSummary");

  function newFoodQuestion() {
    if (gameFinished) {
      questionIndex = 0;
      score = 0;
      totalEatenCalories = 0;
      gameFinished = false;
      foodSummary.style.display = "none";
      scoreText.textContent = 0;
      totalEaten.textContent = 0;
    }

    if (questionIndex >= maxQuestions) {
      showFoodSummary();
      return;
    }

    const randomIndex = Math.floor(Math.random() * foods.length);
    currentFood = foods[randomIndex];

    questionIndex++;
    foodIndexBadge.textContent = `คำถามข้อ ${questionIndex}/${maxQuestions}`;
    foodNameDiv.textContent = currentFood.name;

    calInput.value = "";
    foodResult.style.display = "none";
    foodQuestionBox.style.display = "block";
  }

  btnNewQuestion.addEventListener("click", newFoodQuestion);

  btnCheckFood.addEventListener("click", () => {
    const val = parseFloat(calInput.value);
    if (isNaN(val) || val < 0) {
      foodResult.textContent = "กรอกตัวเลขให้ถูกต้องก่อนนะ";
      foodResult.classList.add("error");
      foodResult.style.display = "block";
      return;
    }

    const diff = Math.abs(val - currentFood.calories);
    const tolerance = 50;

    if (diff <= tolerance) {
      score++;
      foodResult.classList.remove("error");
      foodResult.innerHTML =
        `✅ ใกล้เคียงดีมาก!<br>เฉลย: <strong>${currentFood.calories} kcal</strong>`;
    } else {
      foodResult.classList.add("error");
      foodResult.innerHTML =
        `❌ ห่างไปนิดนะ<br>เฉลย: <strong>${currentFood.calories} kcal</strong>`;
    }

    foodResult.style.display = "block";
    totalEatenCalories += currentFood.calories;
    totalEaten.textContent = totalEatenCalories;
    scoreText.textContent = score;

    if (questionIndex >= maxQuestions) {
      gameFinished = true;
      showFoodSummary();
    }
  });

  function showFoodSummary() {
    const ageKey = ageGroupSelect.value;
    const info = ageGroups[ageKey];

    foodSummary.style.display = "block";
    foodSummary.innerHTML =
      `<strong>🎉 สรุปคะแนน</strong><br>
       ตอบถูกใกล้เคียง: <strong>${score}/${maxQuestions}</strong><br>
       แคลอรี่รวมจากเกม: <strong>${totalEatenCalories} kcal</strong><br><br>
       เทียบกับช่วงอายุ: <strong>${info.label}</strong><br>
       ต้องการพลังงานต่อวันประมาณ: <strong>${info.recommend}</strong>`;
  }

  /* -----------------------------------------------------
      8) ระบบออกกำลังกาย
  ----------------------------------------------------- */
  const bodyPartSelect = document.getElementById("bodyPart");
  const exerciseSelect = document.getElementById("exerciseSelect");
  const minutesInput = document.getElementById("minutesInput");
  const btnCalcBurn = document.getElementById("btnCalcBurn");
  const exerciseResult = document.getElementById("exerciseResult");
  const compareSummary = document.getElementById("compareSummary");

  function populateExerciseOptions() {
    const part = bodyPartSelect.value;
    const options = exercises.filter(e => e.part === part);

    exerciseSelect.innerHTML = "";
    options.forEach(e => {
      const opt = document.createElement("option");
      opt.value = e.name;
      opt.textContent = `${e.name} (~${e.burnPerMin} kcal/นาที)`;
      exerciseSelect.appendChild(opt);
    });
  }
  populateExerciseOptions();

  bodyPartSelect.addEventListener("change", populateExerciseOptions);

  btnCalcBurn.addEventListener("click", () => {
    const minutes = parseFloat(minutesInput.value);
    if (isNaN(minutes) || minutes <= 0) {
      exerciseResult.textContent = "กรอกเวลาที่ถูกต้อง";
      exerciseResult.classList.add("error");
      exerciseResult.style.display = "block";
      return;
    }

    const exName = exerciseSelect.value;
    const ex = exercises.find(e => e.name === exName && e.part === bodyPartSelect.value);
    const burned = Math.round(ex.burnPerMin * minutes);

    exerciseResult.classList.remove("error");
    exerciseResult.style.display = "block";
    exerciseResult.innerHTML =
      `🔥 ท่า <strong>${ex.name}</strong> ${minutes} นาที<br>
       เผาผลาญประมาณ <strong>${burned} kcal</strong>`;

    if (totalEatenCalories > 0) {
      const ratio = (burned / totalEatenCalories * 100).toFixed(1);

      compareSummary.style.display = "block";
      compareSummary.innerHTML =
        `<strong>เปรียบเทียบกับการกินในเกม</strong><br>
         แคลอรี่ที่กิน: <strong>${totalEatenCalories} kcal</strong><br>
         แคลอรี่ที่เผาได้: <strong>${burned} kcal</strong> (${ratio}%)<br><br>
         ${
           burned >= totalEatenCalories
             ? "✅ เผาผลาญมากพอแล้ว ดีมาก!"
             : "ℹ️ เผาผลาญยังไม่เท่าที่กิน ลองเพิ่มเวลาอีกหน่อยนะ"
         }`;
    }
  });
</script>

</body>
</html>
