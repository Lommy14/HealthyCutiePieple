<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>ระบบประกาศข่าวสารในโรงเรียน</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      font-family: "Sarabun", system-ui, -apple-system, "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      padding: 20px;
      background: #eef3ff;
      display: flex;
      justify-content: center;
    }

    .container {
      max-width: 1100px;
      width: 100%;
      background: #ffffff;
      border-radius: 16px;
      padding: 20px 22px 24px;
      box-shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
    }

    h1 {
      margin: 0;
      font-size: 22px;
      color: #1d4ed8;
      text-align: center;
    }

    p.desc {
      margin: 6px 0 18px;
      text-align: center;
      font-size: 14px;
      color: #6b7280;
    }

    .layout {
      display: grid;
      grid-template-columns: 320px 1fr;
      gap: 18px;
    }

    @media (max-width: 900px) {
      .layout {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: #f9fbff;
      border-radius: 12px;
      padding: 14px 16px 16px;
      border: 1px solid #e2e8f0;
    }

    h2 {
      margin: 0 0 10px;
      font-size: 18px;
      color: #1f2937;
    }

    label {
      display: block;
      font-size: 14px;
      font-weight: 600;
      color: #111827;
      margin-top: 8px;
      margin-bottom: 4px;
    }

    input[type="text"],
    input[type="date"],
    select,
    textarea {
      width: 100%;
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid #cbd5e1;
      font-size: 14px;
      outline: none;
      resize: vertical;
      min-height: 36px;
    }

    textarea {
      min-height: 80px;
    }

    input:focus,
    select:focus,
    textarea:focus {
      border-color: #2563eb;
      box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.15);
    }

    .btn {
      border: none;
      border-radius: 999px;
      padding: 8px 14px;
      font-size: 14px;
      cursor: pointer;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 4px;
      margin-top: 10px;
    }

    .btn-primary {
      background: #2563eb;
      color: #ffffff;
    }

    .btn-secondary {
      background: #64748b;
      color: #ffffff;
    }

    .btn-danger {
      background: #dc2626;
      color: #ffffff;
    }

    .badge {
      display: inline-block;
      padding: 3px 8px;
      border-radius: 999px;
      font-size: 11px;
      margin-right: 4px;
      margin-top: 2px;
    }

    .badge-type {
      background: #e0f2fe;
      color: #0369a1;
    }

    .badge-target {
      background: #dcfce7;
      color: #15803d;
    }

    .badge-date {
      background: #fef3c7;
      color: #b45309;
    }

    .announce-list {
      max-height: 540px;
      overflow-y: auto;
      padding-right: 4px;
    }

    .announce-item {
      background: #ffffff;
      border-radius: 10px;
      padding: 10px 12px;
      border: 1px solid #e5e7eb;
      margin-bottom: 8px;
    }

    .announce-title {
      font-size: 15px;
      font-weight: 700;
      color: #111827;
      margin-bottom: 4px;
    }

    .announce-meta {
      font-size: 12px;
      color: #6b7280;
      margin-bottom: 6px;
    }

    .announce-body {
      font-size: 13px;
      color: #374151;
      white-space: pre-line;
    }

    .announce-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 6px;
      font-size: 11px;
      color: #6b7280;
    }

    .filter-row {
      display: flex;
      gap: 6px;
      margin-bottom: 8px;
      flex-wrap: wrap;
      align-items: center;
    }

    .filter-row span {
      font-size: 13px;
      color: #4b5563;
    }

    .filter-row select,
    .filter-row input[type="text"] {
      flex: 1;
      min-width: 120px;
    }

    .muted {
      font-size: 12px;
      color: #6b7280;
      margin-top: 4px;
    }

    .empty-text {
      font-size: 13px;
      color: #9ca3af;
      text-align: center;
      margin-top: 18px;
    }
  </style>
</head>

<body>
<div class="container">
  <h1>📢 ระบบประกาศข่าวสารในโรงเรียน</h1>
  <p class="desc">บันทึกข่าวสาร / กิจกรรม / ประกาศด่วน แล้วแสดงเป็นบอร์ดข่าวในโรงเรียน</p>

  <div class="layout">
    <!-- ฟอร์มบันทึกข่าว -->
    <div class="card">
      <h2>ฟอร์มกรอกข่าวสาร</h2>

      <label for="title">หัวข้อข่าว / เรื่องที่ประกาศ</label>
      <input type="text" id="title" placeholder="เช่น แจ้งหยุดเรียนพิเศษวันศุกร์นี้">

      <label for="date">วันที่ประกาศ</label>
      <input type="date" id="date">

      <label for="type">ประเภทข่าว</label>
      <select id="type">
        <option value="ทั่วไป">ทั่วไป</option>
        <option value="กิจกรรม">กิจกรรม</option>
        <option value="ประกาศด่วน">ประกาศด่วน</option>
        <option value="ประชุม">ประชุม</option>
      </select>

      <label for="target">กลุ่มเป้าหมาย</label>
      <select id="target">
        <option value="นักเรียน">นักเรียน</option>
        <option value="ครู">ครู</option>
        <option value="ผู้ปกครอง">ผู้ปกครอง</option>
        <option value="ทุกคน">ทุกคน</option>
      </select>

      <label for="content">รายละเอียดข่าว</label>
      <textarea id="content" placeholder="พิมพ์รายละเอียดข่าวสารที่ต้องการประกาศ"></textarea>

      <button class="btn btn-primary" id="btnSave">บันทึกประกาศ</button>

      <p class="muted">
        * ข้อมูลจะถูกเก็บไว้ในเบราว์เซอร์เครื่องนี้ (localStorage)<br>
        ถ้าปิดหน้าแล้วกลับมาใหม่ ข่าวเดิมยังอยู่ เว้นแต่จะกดลบออก
      </p>
    </div>

    <!-- บอร์ดข่าว -->
    <div class="card">
      <h2>บอร์ดข่าวในโรงเรียน</h2>

      <div class="filter-row">
        <span>ค้นหา:</span>
        <input type="text" id="search" placeholder="ค้นหาจากหัวข้อหรือเนื้อหาข่าว">
      </div>
      <div class="filter-row">
        <span>ตัวกรอง:</span>
        <select id="filterType">
          <option value="">ทุกประเภท</option>
          <option value="ทั่วไป">ทั่วไป</option>
          <option value="กิจกรรม">กิจกรรม</option>
          <option value="ประกาศด่วน">ประกาศด่วน</option>
          <option value="ประชุม">ประชุม</option>
        </select>
        <select id="filterTarget">
          <option value="">ทุกกลุ่มเป้าหมาย</option>
          <option value="นักเรียน">นักเรียน</option>
          <option value="ครู">ครู</option>
          <option value="ผู้ปกครอง">ผู้ปกครอง</option>
          <option value="ทุกคน">ทุกคน</option>
        </select>
        <button class="btn btn-secondary small" id="btnClearFilter">ล้างตัวกรอง</button>
      </div>

      <div style="display:flex;justify-content:flex-end;gap:6px;margin-bottom:4px;">
        <button class="btn btn-danger small" id="btnClearAll">ลบข่าวทั้งหมด</button>
      </div>

      <div id="announceList" class="announce-list"></div>
      <div id="emptyText" class="empty-text" style="display:none;">ยังไม่มีข่าวประกาศในระบบ</div>
    </div>
  </div>
</div>

<script>
  // เก็บข่าวในหน่วยความจำ
  let announcements = [];

  const STORAGE_KEY = "school_announcements_v1";

  // อ้างอิง element
  const titleInput   = document.getElementById("title");
  const dateInput    = document.getElementById("date");
  const typeSelect   = document.getElementById("type");
  const targetSelect = document.getElementById("target");
  const contentInput = document.getElementById("content");

  const btnSave       = document.getElementById("btnSave");
  const announceList  = document.getElementById("announceList");
  const emptyText     = document.getElementById("emptyText");
  const searchInput   = document.getElementById("search");
  const filterType    = document.getElementById("filterType");
  const filterTarget  = document.getElementById("filterTarget");
  const btnClearFilter= document.getElementById("btnClearFilter");
  const btnClearAll   = document.getElementById("btnClearAll");

  // โหลดวันที่วันนี้ใส่ใน input date
  function setToday() {
    const today = new Date().toISOString().split("T")[0];
    dateInput.value = today;
  }

  // โหลดจาก localStorage
  function loadFromStorage() {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) {
      try {
        announcements = JSON.parse(raw) || [];
      } catch (e) {
        announcements = [];
      }
    } else {
      announcements = [];
    }
  }

  // บันทึกลง localStorage
  function saveToStorage() {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(announcements));
  }

  // ล้างฟอร์ม
  function clearForm() {
    titleInput.value = "";
    // dateInput ไม่ต้องล้างให้ ยังคงเป็นวันเดิม
    typeSelect.value = "ทั่วไป";
    targetSelect.value = "นักเรียน";
    contentInput.value = "";
  }

  // เพิ่มข่าวใหม่
  btnSave.addEventListener("click", () => {
    const title = titleInput.value.trim();
    const date = dateInput.value;
    const type = typeSelect.value;
    const target = targetSelect.value;
    const content = contentInput.value.trim();

    if (!title || !date || !content) {
      alert("กรุณากรอกหัวข้อ, วันที่ และรายละเอียดข่าว ให้ครบถ้วน");
      return;
    }

    const item = {
      id: Date.now(),
      title,
      date,
      type,
      target,
      content,
      createdAt: new Date().toISOString()
    };

    // ใส่ข่าวใหม่ไว้ด้านบน
    announcements.unshift(item);
    saveToStorage();
    renderList();
    clearForm();
  });

  // เรนเดอร์รายการข่าว
  function renderList() {
    announceList.innerHTML = "";

    // ตัวกรอง / ค้นหา
    const text = searchInput.value.toLowerCase();
    const tFilter = filterType.value;
    const gFilter = filterTarget.value;

    const filtered = announcements.filter(a => {
      const matchText =
        !text ||
        a.title.toLowerCase().includes(text) ||
        a.content.toLowerCase().includes(text);
      const matchType = !tFilter || a.type === tFilter;
      const matchTarget = !gFilter || a.target === gFilter;
      return matchText && matchType && matchTarget;
    });

    if (filtered.length === 0) {
      emptyText.style.display = "block";
      return;
    } else {
      emptyText.style.display = "none";
    }

    filtered.forEach(item => {
      const div = document.createElement("div");
      div.className = "announce-item";

      // แปลงวันที่เป็นแบบอ่านง่าย
      let showDate = item.date;
      try {
        const d = new Date(item.date);
        if (!isNaN(d)) {
          showDate = d.toLocaleDateString("th-TH", {
            year: "numeric",
            month: "short",
            day: "numeric"
          });
        }
      } catch(e) {}

      div.innerHTML = `
        <div class="announce-title">${item.title}</div>
        <div class="announce-meta">
          <span class="badge badge-type">${item.type}</span>
          <span class="badge badge-target">${item.target}</span>
          <span class="badge badge-date">ประกาศวันที่: ${showDate}</span>
        </div>
        <div class="announce-body">${item.content}</div>
        <div class="announce-footer">
          <span>บันทึกเมื่อ: ${new Date(item.createdAt).toLocaleString("th-TH")}</span>
          <button class="btn btn-danger small" data-id="${item.id}">ลบ</button>
        </div>
      `;

      announceList.appendChild(div);
    });

    // ผูก event ปุ่มลบ
    announceList.querySelectorAll("button[data-id]").forEach(btn => {
      btn.addEventListener("click", () => {
        const id = parseInt(btn.getAttribute("data-id"), 10);
        announcements = announcements.filter(a => a.id !== id);
        saveToStorage();
        renderList();
      });
    });
  }

  // ล้างตัวกรอง
  btnClearFilter.addEventListener("click", () => {
    searchInput.value = "";
    filterType.value = "";
    filterTarget.value = "";
    renderList();
  });

  // ลบข่าวทั้งหมด
  btnClearAll.addEventListener("click", () => {
    if (confirm("ต้องการลบข่าวทั้งหมดออกจากระบบหรือไม่?")) {
      announcements = [];
      saveToStorage();
      renderList();
    }
  });

  // ค้นหา / กรองแบบสด
  searchInput.addEventListener("input", renderList);
  filterType.addEventListener("change", renderList);
  filterTarget.addEventListener("change", renderList);

  // เริ่มต้น
  setToday();
  loadFromStorage();
  renderList();
</script>

</body>
</html>
