<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>ระบบประกาศข้อมูลข่าวสารโรงเรียน (แชร์/มีสิทธิ์)</title>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#f7fbff;--card:#ffffff;--primary:#1e3a8a;--accent:#2563eb;--muted:#6b7280;--line:#e6eefc;
    }
    *{box-sizing:border-box;font-family:"Sarabun",system-ui,-apple-system,"Segoe UI",sans-serif}
    body{margin:0;background:var(--bg);padding:18px;display:flex;justify-content:center;color:#10243a}
    .container{width:100%;max-width:1200px;background:var(--card);border-radius:14px;padding:18px;border:1px solid var(--line);box-shadow:0 10px 30px rgba(16,36,58,0.06)}
    header{text-align:center;margin-bottom:12px}
    header h1{margin:0;color:var(--primary);font-size:26px}
    header p{margin:6px 0 0;color:var(--muted);font-size:13px}
    .layout{display:grid;grid-template-columns:420px 1fr;gap:16px}
    @media(max-width:980px){.layout{grid-template-columns:1fr}}
    .card{background:linear-gradient(180deg,#fbfeff,#f6fbff);border-radius:12px;padding:14px;border:1px solid var(--line)}
    label{display:block;font-size:13px;font-weight:600;margin-top:10px;color:#1f2937}
    input[type="text"],input[type="date"],select,textarea{width:100%;padding:10px 12px;border-radius:10px;border:1px solid #dbe9ff;background:#fff;margin-top:6px}
    textarea{min-height:100px;resize:vertical}
    .checkbox-row{display:flex;flex-wrap:wrap;gap:8px;margin-top:8px}
    .checkbox-row label{display:flex;align-items:center;gap:8px;font-weight:500}
    .btn-row{display:flex;gap:10px;margin-top:12px;align-items:center}
    .btn{padding:10px 14px;border-radius:999px;border:0;cursor:pointer;font-weight:700}
    .btn-primary{background:linear-gradient(90deg,var(--accent),#16a34a);color:#fff}
    .btn-ghost{background:#eef6ff;color:#10243a;border:1px solid #e6f0ff}
    .muted{color:var(--muted);font-size:13px;margin-top:6px}
    .filters{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:10px}
    .small-input{max-width:220px;padding:8px;border-radius:10px;border:1px solid #dbe9ff;background:#fff}
    .date-input{max-width:150px;padding:8px;border-radius:10px;border:1px solid #dbe9ff;background:#fff}
    .news-list{display:flex;flex-direction:column;gap:12px;max-height:560px;overflow:auto;padding-right:6px}
    .news-item{background:#fff;border-radius:10px;padding:12px;border:1px solid #eef6ff;box-shadow:0 6px 18px rgba(16,36,58,0.03)}
    .news-top{display:flex;justify-content:space-between;gap:8px;align-items:flex-start}
    .news-title{font-weight:800;color:#0b2b48;font-size:16px;margin-bottom:6px}
    .meta{font-size:13px;color:var(--muted)}
    .targets{margin-top:6px}
    .tag{display:inline-block;padding:4px 8px;border-radius:999px;background:#eef9ff;color:#0b58a5;margin-right:6px;font-weight:700;font-size:12px}
    .news-body{margin-top:8px;color:#203845;white-space:pre-line;font-size:14px}
    .actions{display:flex;gap:8px;justify-content:flex-end;margin-top:10px}
    .action-btn{padding:6px 10px;border-radius:8px;background:#f3f7ff;border:1px solid #e6f0ff;cursor:pointer;font-weight:700}
    .empty{text-align:center;color:var(--muted);padding:24px;border-radius:8px;border:1px dashed #e6eefc}
    .user-row{display:flex;gap:8px;align-items:center;justify-content:flex-end;margin-bottom:8px}
    .badge-admin{background:#fff7ed;color:#92400e;border-radius:999px;padding:6px 10px;font-weight:700}
    .hidden{display:none}
    .info{font-size:13px;color:var(--muted);margin-top:8px}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>ระบบประกาศข้อมูลข่าวสารโรงเรียน</h1>
      <p>ข่าวแชร์ร่วมกัน (Firestore) — ลงชื่อเข้าใช้เพื่อโพสต์/แก้ไข/ลบ (เฉพาะ admin)</p>
    </header>

    <div class="user-row" id="authRow">
      <!-- populated by JS: sign in/out and user info -->
    </div>

    <div class="layout">
      <!-- left: form -->
      <div class="card" id="formCard">
        <h2 id="formTitle">บันทึกข่าวสารใหม่</h2>

        <label>หัวข้อข่าว</label>
        <input id="title" type="text" placeholder="เช่น แจ้งกำหนดการประชุมผู้ปกครอง">

        <label>ชื่อผู้ลงประกาศ</label>
        <input id="publisher" type="text" placeholder="ชื่อ-นามสกุล">

        <label>วันที่ประกาศ</label>
        <input id="date" type="date">

        <label>หมวดหมู่ข่าว</label>
        <select id="category">
          <option value="ทั่วไป">ทั่วไป</option>
          <option value="การเรียนการสอน">การเรียนการสอน</option>
          <option value="กิจกรรม">กิจกรรม</option>
          <option value="ประชุม/อบรม">ประชุม/อบรม</option>
          <option value="งานวิชาการ">งานวิชาการ</option>
          <option value="อื่น ๆ">อื่น ๆ</option>
        </select>

        <label>กลุ่มเป้าหมาย</label>
        <div id="targets" class="checkbox-row">
          <label><input type="checkbox" value="นักเรียน"> นักเรียน</label>
          <label><input type="checkbox" value="ครู"> ครู</label>
          <label><input type="checkbox" value="ผู้ปกครอง"> ผู้ปกครอง</label>
          <label><input type="checkbox" value="บุคลากร"> บุคลากร</label>
          <label><input type="checkbox" value="บุคคลทั่วไป"> บุคคลทั่วไป</label>
        </div>

        <label>รายละเอียดข่าว</label>
        <textarea id="content" placeholder="รายละเอียด เช่น วัน เวลา สถานที่ เงื่อนไข"></textarea>

        <div class="btn-row" id="formButtons">
          <button id="saveBtn" class="btn btn-primary">บันทึกข่าว</button>
          <button id="cancelEditBtn" class="btn btn-ghost hidden">ยกเลิกการแก้ไข</button>
          <button id="clearBtn" class="btn btn-ghost">ล้างแบบฟอร์ม</button>
        </div>

        <div class="info">
          หากต้องการแชร์ข่าวให้คนอื่นเห็นจริง ๆ ให้ใช้ Firestore (ตั้งค่าใน script) — ตรวจสอบค่า <code>firebaseConfig</code> และ <code>ADMIN_EMAILS</code> ก่อนใช้งาน
        </div>
      </div>

      <!-- right: list -->
      <div class="card">
        <h2>รายการข่าวสาร</h2>

        <div class="filters">
          <input id="search" class="small-input" type="text" placeholder="ค้นหา หัวข้อหรือเนื้อหา" style="flex:1">
          <select id="filterCategory" class="small-input">
            <option value="">ทุกหมวดหมู่</option>
            <option>ทั่วไป</option>
            <option>การเรียนการสอน</option>
            <option>กิจกรรม</option>
            <option>ประชุม/อบรม</option>
            <option>งานวิชาการ</option>
            <option>อื่น ๆ</option>
          </select>

          <div style="display:flex;gap:6px;align-items:center">
            <label style="font-weight:700;margin-right:6px">กลุ่ม:</label>
            <label><input type="checkbox" class="filter-target" value="นักเรียน">นักเรียน</label>
            <label><input type="checkbox" class="filter-target" value="ครู">ครู</label>
            <label><input type="checkbox" class="filter-target" value="ผู้ปกครอง">ผู้ปกครอง</label>
            <label><input type="checkbox" class="filter-target" value="บุคลากร">บุคลากร</label>
            <label><input type="checkbox" class="filter-target" value="บุคคลทั่วไป">บุคคลทั่วไป</label>
          </div>

          <input id="fromDate" class="date-input" type="date" title="วันที่จาก">
          <input id="toDate" class="date-input" type="date" title="ถึง">

          <label style="margin-left:auto;display:flex;align-items:center;gap:8px">
            <input id="pinnedOnly" type="checkbox"> แสดงเฉพาะปักหมุด
          </label>

          <button id="clearAllBtn" class="btn btn-ghost">ลบข่าวทั้งหมด</button>
        </div>

        <div id="newsList" class="news-list"></div>
      </div>
    </div>
  </div>

  <!-- Firebase compat SDK (ง่ายต่อการนำโค้ดเดิมมาปรับ) -->
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore-compat.js"></script>

  <script>
    /************************************************************************
     *  CONFIGURATION: แก้ค่าส่วนนี้ให้เป็นค่าจาก Firebase Console ของคุณ
     *  และแก้ ADMIN_EMAILS ให้เป็นรายชื่ออีเมลของแอดมินของโรงเรียน
     ************************************************************************/
    const firebaseConfig = {
      /* TODO: REPLACE WITH YOUR CONFIG FROM FIREBASE */
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MSG_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    // รายชื่อผู้ที่มีสิทธิ์โพสต์/แก้ไข/ลบ (ตัวอย่าง)
    const ADMIN_EMAILS = [
      /* ใส่อีเมลของครู/แอดมิน เช่น */
      "admin1@example.com",
      "admin2@example.com"
    ];

    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    const db = firebase.firestore();

    // DOM
    const authRow = document.getElementById('authRow');
    const titleEl = document.getElementById('title');
    const publisherEl = document.getElementById('publisher');
    const dateEl = document.getElementById('date');
    const categoryEl = document.getElementById('category');
    const contentEl = document.getElementById('content');
    const targetsEl = document.getElementById('targets');
    const saveBtn = document.getElementById('saveBtn');
    const clearBtn = document.getElementById('clearBtn');
    const cancelEditBtn = document.getElementById('cancelEditBtn');
    const formTitle = document.getElementById('formTitle');

    const searchEl = document.getElementById('search');
    const filterCategoryEl = document.getElementById('filterCategory');
    const filterTargetCheckboxes = document.querySelectorAll('.filter-target');
    const fromDateEl = document.getElementById('fromDate');
    const toDateEl = document.getElementById('toDate');
    const pinnedOnlyEl = document.getElementById('pinnedOnly');
    const newsListDiv = document.getElementById('newsList');
    const clearAllBtn = document.getElementById('clearAllBtn');

    let currentUser = null;
    let isAdmin = false;
    let editId = null; // id of doc being edited

    // helper: set today's date
    function setToday(){
      const t = new Date();
      const yyyy = t.getFullYear();
      const mm = String(t.getMonth()+1).padStart(2,'0');
      const dd = String(t.getDate()).padStart(2,'0');
      dateEl.value = `${yyyy}-${mm}-${dd}`;
    }

    // auth UI
    function renderAuthUI(user) {
      authRow.innerHTML = '';
      const wrapper = document.createElement('div');
      wrapper.style.display = 'flex';
      wrapper.style.gap = '8px';
      wrapper.style.alignItems = 'center';
      wrapper.style.width = '100%';

      const left = document.createElement('div');
      left.style.flex = '1';
      if(user){
        const name = user.displayName || user.email || 'ผู้ใช้';
        const email = user.email || '';
        left.innerHTML = `<div style="font-weight:700">${escapeHtml(name)}</div><div style="color:var(--muted);font-size:13px">${escapeHtml(email)}</div>`;
        if(isAdmin){
          const b = document.createElement('span');
          b.className = 'badge-admin';
          b.textContent = 'ADMIN';
          left.appendChild(b);
        }
      } else {
        left.innerHTML = `<div style="color:var(--muted);font-size:13px">ไม่พบผู้ใช้งาน — กรุณาเข้าสู่ระบบเพื่อโพสต์/แก้ไข/ลบ</div>`;
      }

      const right = document.createElement('div');
      right.style.display = 'flex';
      right.style.gap = '8px';
      if(user){
        const outBtn = document.createElement('button');
        outBtn.className = 'btn btn-ghost';
        outBtn.textContent = 'ออกจากระบบ';
        outBtn.addEventListener('click', () => auth.signOut());
        right.appendChild(outBtn);
      } else {
        const inBtn = document.createElement('button');
        inBtn.className = 'btn btn-primary';
        inBtn.textContent = 'ลงชื่อเข้าใช้ด้วย Google';
        inBtn.addEventListener('click', signInWithGoogle);
        right.appendChild(inBtn);
      }

      wrapper.appendChild(left);
      wrapper.appendChild(right);
      authRow.appendChild(wrapper);

      // show/hide form depending on admin status
      document.getElementById('formCard').style.display = (user && isAdmin) ? 'block' : (user ? 'block' : 'block');
      // We allow form to be visible, but actions (save/delete) are checked on client and server.
      // If you prefer to hide entirely for non-admins, set display to 'none' when not admin.
    }

    // sign in with popup
    async function signInWithGoogle(){
      const provider = new firebase.auth.GoogleAuthProvider();
      try {
        await auth.signInWithPopup(provider);
      } catch (err) {
        console.error('Sign-in error', err);
        alert('เกิดข้อผิดพลาดขณะลงชื่อเข้าใช้');
      }
    }

    // check admin by email
    function checkAdmin(user){
      if(!user || !user.email) return false;
      return ADMIN_EMAILS.includes(user.email.toLowerCase());
    }

    // escape html
    function escapeHtml(s){ if(!s) return ''; return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

    // form helpers
    function getFormTargets(){
      const res = [];
      targetsEl.querySelectorAll('input[type="checkbox"]').forEach(cb => { if(cb.checked) res.push(cb.value); });
      return res;
    }

    function setFormTargets(arr){
      targetsEl.querySelectorAll('input[type="checkbox"]').forEach(cb => { cb.checked = arr.includes(cb.value); });
    }

    function clearForm(){
      titleEl.value = '';
      publisherEl.value = '';
      contentEl.value = '';
      categoryEl.value = 'ทั่วไป';
      setFormTargets([]);
      setToday();
      editId = null;
      formTitle.textContent = 'บันทึกข่าวสารใหม่';
      cancelEditBtn.classList.add('hidden');
      saveBtn.textContent = 'บันทึกข่าว';
    }

    // CRUD with Firestore
    async function addNewsToFirestore(data){
      await db.collection('schoolNews').add(data);
    }

    async function updateNewsInFirestore(id, data){
      await db.collection('schoolNews').doc(id).update(data);
    }

    async function deleteNewsFromFirestore(id){
      await db.collection('schoolNews').doc(id).delete();
    }

    async function togglePinFirestore(id, pinned){
      await db.collection('schoolNews').doc(id).update({ pinned: !pinned });
    }

    // save button handler (create or update)
    saveBtn.addEventListener('click', async () => {
      if(!currentUser) { alert('กรุณาลงชื่อเข้าใช้ก่อน'); return; }
      if(!isAdmin){ alert('เฉพาะผู้ดูแล (admin) เท่านั้นที่สามารถโพสต์หรือแก้ไขได้'); return; }

      const title = titleEl.value.trim();
      const publisher = publisherEl.value.trim() || (currentUser.displayName || currentUser.email || '');
      const date = dateEl.value;
      const category = categoryEl.value;
      const content = contentEl.value.trim();
      const targets = getFormTargets();

      if(!title){ alert('กรุณากรอกหัวข้อข่าว'); return; }

      const doc = {
        title, publisher, date, category, content, targets,
        pinned: false,
        updatedAt: Date.now(),
      };

      try {
        if(editId){
          // update
          await updateNewsInFirestore(editId, doc);
        } else {
          // create
          doc.createdAt = Date.now();
          await addNewsToFirestore(doc);
        }
        clearForm();
      } catch(err){
        console.error('Save error', err);
        alert('เกิดข้อผิดพลาดขณะบันทึก');
      }
    });

    // cancel edit
    cancelEditBtn.addEventListener('click', () => { clearForm(); });

    // clear form
    clearBtn.addEventListener('click', clearForm);

    // clear all (admin only)
    clearAllBtn.addEventListener('click', async () => {
      if(!currentUser || !isAdmin){ alert('เฉพาะผู้ดูแลเท่านั้นที่สามารถลบทั้งหมดได้'); return; }
      if(!confirm('ต้องการลบข่าวทั้งหมดหรือไม่?')) return;
      try {
        const snapshot = await db.collection('schoolNews').get();
        const batch = db.batch();
        snapshot.docs.forEach(doc => batch.delete(doc.ref));
        await batch.commit();
      } catch(err){
        console.error('clear all error', err);
        alert('เกิดข้อผิดพลาดขณะลบทั้งหมด');
      }
    });

    // realtime listener & render with filters
    let cached = [];
    function startRealtime(){
      db.collection('schoolNews')
        .orderBy('pinned','desc')
        .orderBy('createdAt','desc')
        .onSnapshot(snap => {
          cached = snap.docs.map(doc => ({ id: doc.id, ...doc.data() }));
          renderNewsList();
        }, err => {
          console.error('snapshot error', err);
        });
    }

    function getFilterTargets(){
      const res = [];
      document.querySelectorAll('.filter-target').forEach(cb => { if(cb.checked) res.push(cb.value); });
      return res;
    }

    function dateInRange(d, from, to){
      if(!d) return false;
      if(from && d < from) return false;
      if(to && d > to) return false;
      return true;
    }

    function renderNewsList(){
      newsListDiv.innerHTML = '';
      const keyword = (searchEl.value || '').trim().toLowerCase();
      const catFilter = filterCategoryEl.value;
      const selectedTargets = getFilterTargets();
      const from = fromDateEl.value;
      const to = toDateEl.value;
      const pinnedOnly = pinnedOnlyEl.checked;

      const items = cached.slice().filter(it => {
        if(pinnedOnly && !it.pinned) return false;
        const text = ((it.title||'') + ' ' + (it.content||'') + ' ' + (it.publisher||'') + ' ' + (it.targets||[]).join(' ')).toLowerCase();
        if(keyword && !text.includes(keyword)) return false;
        if(catFilter && it.category !== catFilter) return false;
        if(selectedTargets.length > 0){
          if(!Array.isArray(it.targets) || it.targets.length === 0) return false;
          const any = selectedTargets.some(t => it.targets.includes(t));
          if(!any) return false;
        }
        if((from || to) && !dateInRange(it.date || '', from, to)) return false;
        return true;
      });

      if(items.length === 0){
        const e = document.createElement('div'); e.className = 'empty'; e.textContent = 'ยังไม่มีข่าว หรือไม่พบข่าวตามเงื่อนไข'; newsListDiv.appendChild(e); return;
      }

      items.forEach(it => {
        const card = document.createElement('div'); card.className = 'news-item';

        const top = document.createElement('div'); top.className = 'news-top';
        const left = document.createElement('div');
        const title = document.createElement('div'); title.className = 'news-title'; title.textContent = it.title || '(ไม่มีหัวข้อ)';
        const meta = document.createElement('div'); meta.className = 'meta'; meta.innerHTML = `<strong>${escapeHtml(it.publisher || '')}</strong> &nbsp; • &nbsp; ${escapeHtml(it.date||'-')}`;

        left.appendChild(title); left.appendChild(meta);

        const right = document.createElement('div');
        if(it.pinned){
          const p = document.createElement('div'); p.className='badge-admin'; p.style.background='#fff7ed'; p.style.color='#92400e'; p.textContent = 'ปักหมุด'; right.appendChild(p);
        }

        top.appendChild(left); top.appendChild(right);

        const targetsLine = document.createElement('div'); targetsLine.className='targets';
        if(it.targets && it.targets.length){
          it.targets.forEach(t => {
            const tag = document.createElement('span'); tag.className='tag'; tag.textContent=t; targetsLine.appendChild(tag);
          });
        } else {
          const tag = document.createElement('span'); tag.className='tag'; tag.textContent='กลุ่มเป้าหมาย: ไม่ระบุ'; targetsLine.appendChild(tag);
        }

        const body = document.createElement('div'); body.className='news-body'; body.textContent = it.content || '';

        const actions = document.createElement('div'); actions.className='actions';
        const pinBtn = document.createElement('button'); pinBtn.className='action-btn'; pinBtn.textContent = it.pinned ? 'ยกเลิกปักหมุด' : 'ปักหมุด';
        pinBtn.addEventListener('click', async () => {
          if(!currentUser || !isAdmin){ alert('เฉพาะแอดมินเท่านั้น'); return; }
          try { await togglePinFirestore(it.id, it.pinned); } catch(err){ console.error(err); alert('ผิดพลาดขณะอัปเดตปักหมุด') }
        });
        const editBtn = document.createElement('button'); editBtn.className='action-btn'; editBtn.textContent='แก้ไข';
        editBtn.addEventListener('click', () => {
          if(!currentUser || !isAdmin){ alert('เฉพาะแอดมินเท่านั้น'); return; }
          // load doc into form for editing
          editId = it.id;
          titleEl.value = it.title || '';
          publisherEl.value = it.publisher || '';
          dateEl.value = it.date || '';
          categoryEl.value = it.category || 'ทั่วไป';
          contentEl.value = it.content || '';
          setFormTargets(it.targets || []);
          formTitle.textContent = 'แก้ไขข่าว';
          cancelEditBtn.classList.remove('hidden');
          saveBtn.textContent = 'บันทึกการแก้ไข';
          window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        const delBtn = document.createElement('button'); delBtn.className='action-btn'; delBtn.textContent='ลบ';
        delBtn.addEventListener('click', async () => {
          if(!currentUser || !isAdmin){ alert('เฉพาะแอดมินเท่านั้น'); return; }
          if(!confirm('ต้องการลบข่าวนี้หรือไม่?')) return;
          try { await deleteNewsFromFirestore(it.id); } catch(err){ console.error(err); alert('เกิดข้อผิดพลาดขณะลบ') }
        });

        actions.appendChild(pinBtn);
        actions.appendChild(editBtn);
        actions.appendChild(delBtn);

        card.appendChild(top);
        card.appendChild(targetsLine);
        card.appendChild(body);
        card.appendChild(actions);

        newsListDiv.appendChild(card);
      });
    }

    // listen auth state change
    auth.onAuthStateChanged(async user => {
      currentUser = user;
      isAdmin = checkAdmin(user || {});
      renderAuthUI(user);
    });

    // attach realtime after auth initialized
    startRealtime();

    // wire filters
    searchEl.addEventListener('input', renderNewsList);
    filterCategoryEl.addEventListener('change', renderNewsList);
    fromDateEl.addEventListener('change', renderNewsList);
    toDateEl.addEventListener('change', renderNewsList);
    pinnedOnlyEl.addEventListener('change', renderNewsList);
    document.querySelectorAll('.filter-target').forEach(cb => cb.addEventListener('change', renderNewsList));

    // helper wrapper functions calling firestore operations (with client-side check)
    async function addNewsToFirestore(data){
      if(!currentUser || !isAdmin) throw new Error('not authorized');
      return db.collection('schoolNews').add(data);
    }
    async function updateNewsInFirestore(id, data){
      if(!currentUser || !isAdmin) throw new Error('not authorized');
      return db.collection('schoolNews').doc(id).update(data);
    }
    async function deleteNewsFromFirestore(id){
      if(!currentUser || !isAdmin) throw new Error('not authorized');
      return db.collection('schoolNews').doc(id).delete();
    }
    async function togglePinFirestore(id, pinned){
      if(!currentUser || !isAdmin) throw new Error('not authorized');
      return db.collection('schoolNews').doc(id).update({ pinned: !pinned });
    }

    // initialize default date
    setToday();
  </script>
</body>
</html>
