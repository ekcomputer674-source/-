<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>ঋণ গ্রহণের অঙ্গীকারনামা — Entry, Dashboard & Report (Stamp as per Demo.pdf)</title>
<style>
  :root{
    --bg:#f6f7fb; --card:#ffffff; --pri:#2563eb; --muted:#6b7280;
    --ok:#16a34a; --warn:#d97706; --danger:#dc2626; --border:#e5e7eb; --hl:#fff6a5;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:Segoe UI, Noto Sans Bengali, SolaimanLipi, Arial, sans-serif;background:var(--bg);color:#111827}
  header{background:linear-gradient(135deg,#0ea5e9 0%, #2563eb 60%, #1e40af 100%);color:#fff;padding:24px 16px 12px 16px;position:sticky;top:0;z-index:9}
  .brand{display:flex;align-items:center;gap:12px;flex-wrap:wrap}
  .brand h1{margin:0;font-size:20px}
  .tabs{display:flex;gap:8px;margin-top:12px;flex-wrap:wrap}
  .tab-btn{border:none;background:#fff;color:#111827;padding:10px 14px;border-radius:8px;cursor:pointer;box-shadow:0 1px 2px rgba(0,0,0,.08)}
  .tab-btn.active{background:var(--ok);color:#fff}
  main{padding:18px;max-width:1200px;margin:0 auto}
  .grid{display:grid;gap:12px}
  @media(min-width:860px){ .grid.cols-3{grid-template-columns:repeat(3,1fr)} }
  .card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:16px}
  .muted{color:var(--muted)}
  .kpi{display:flex;gap:12px}
  .kpi .val{font-weight:700;font-size:24px}
  .hl{background:var(--hl);padding:0 4px;border-radius:3px}
  label{font-weight:600;margin-bottom:6px;display:block}
  input,select,textarea{width:100%;padding:10px;border:1px solid var(--border);border-radius:8px;background:#fff}
  .row{display:grid;gap:10px}
  @media(min-width:720px){ .row.cols-2{grid-template-columns:1fr 1fr} .row.cols-3{grid-template-columns:repeat(3,1fr)} }
  .actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
  button{padding:10px 14px;border:none;border-radius:8px;background:var(--pri);color:#fff;cursor:pointer}
  button.secondary{background:#e5e7eb;color:#111827}
  button.warn{background:var(--warn);color:#fff}
  button.danger{background:var(--danger);color:#fff}
  table{width:100%;border-collapse:collapse}
  th,td{border-bottom:1px solid var(--border);padding:10px;text-align:left;vertical-align:top}
  tr:hover{background:#fafafa}
  .sticky-actions{position:sticky;bottom:0;background:#fff;border-top:1px solid var(--border);padding:10px;border-bottom-left-radius:12px;border-bottom-right-radius:12px}
  .badge{background:#dbeafe;color:#1e40af;border:1px solid #bfdbfe;padding:2px 8px;border-radius:999px;font-size:12px}
  .note{font-size:12px;color:#374151}

  /* Stamp-style print layout */
  .stamp-hl{background:#fff59d;padding:0 3px;border-radius:2px}
  @media print{
    .no-print{display:none!important}
    header,.tabs,.sticky-actions{display:none!important}
    @page{ size:A4; margin:12mm }
  }
</style>
</head>
<body>
<header>
  <div class="brand">
    <h1>ঋণ গ্রহণের অঙ্গীকারনামা — ডাটা এন্ট্রি ও রিপোর্ট</h1>
    <small>Full: Entry · Dashboard · Report · Stamp Print (as per Demo.pdf)</small>
  </div>
  <div class="tabs">
    <button class="tab-btn active" data-tab="dashboard">ড্যাশবোর্ড</button>
    <button class="tab-btn" data-tab="entry">ডাটা এন্ট্রি</button>
    <button class="tab-btn" data-tab="report">রিপোর্ট</button>
    <button class="tab-btn" data-tab="settings">সেটিংস</button>
  </div>
</header>

<main>
  <!-- DASHBOARD -->
  <section id="dashboard" class="tab card">
    <h3>ড্যাশবোর্ড</h3>
    <p class="muted">সারাংশ দেখুন</p>
    <div class="grid cols-3">
      <div class="card kpi"><div><div class="val" id="kpi_total">0</div><div class="muted">মোট আবেদন</div></div></div>
      <div class="card kpi"><div><div class="val" id="kpi_today">0</div><div class="muted">আজকের এন্ট্রি</div></div></div>
      <div class="card kpi"><div><div class="val" id="kpi_amount">৳0</div><div class="muted">মোট ঋণ</div></div></div>
    </div>
  </section>

  <!-- ENTRY -->
  <section id="entry" class="tab card" style="display:none;">
    <h3>ডাটা এন্ট্রি ফর্ম <span class="badge">সমিতি: <span id="orgNameBadge"></span></span></h3>

    <form id="loanForm" onsubmit="return false;">
      <input type="hidden" id="id">

      <div class="row cols-2">
        <div>
          <label>সমিতির নাম</label>
          <input id="org_name" disabled>
        </div>
        <div>
          <label>সমিতির ঠিকানা</label>
          <input id="org_addr" disabled>
        </div>
      </div>

      <h4>২য় পক্ষ ঋণগ্রহীতা</h4>
      <div class="row cols-3">
        <div><label>নাম <span class="hl">হাইলাইট</span></label><input id="b_name" required></div>
        <div><label>পিতা/স্বামী</label><input id="b_fh" required></div>
        <div><label>মাতার নাম</label><input id="b_mother"></div>
      </div>
      <div class="row cols-3">
        <div><label>পেশা</label><input id="b_profession"></div>
        <div><label>গ্রাম/ঠিকানা</label><input id="b_village"></div>
        <div><label>পোস্ট/থানা/জেলা</label><input id="b_ps_dist"></div>
      </div>
      <div class="row cols-3">
        <div>
          <label>মোবাইল (বাংলাদেশ)</label>
          <input id="b_mobile" type="tel" placeholder="01XXXXXXXXX" inputmode="numeric" pattern="01\d{9}">
          <div class="note">না হলে ফাঁকা রাখুন</div>
        </div>
        <div><label>NID/জন্ম নিবন্ধন</label><input id="b_nid"></div>
        <div><label>জন্ম তারিখ</label><input type="date" id="b_dob"></div>
      </div>

      <h4>জামিনদার</h4>
      <!-- Only Guarantor‑1 (as per Demo.pdf) -->
      <div class="row cols-3">
        <div><label>নাম</label><input id="g1_name"></div>
        <div><label>পিতা/স্বামী</label><input id="g1_fh"></div>
        <div><label>মাতার নাম</label><input id="g1_mother"></div>
      </div>
      <div class="row cols-3">
        <div><label>পেশা</label><input id="g1_profession"></div>
        <div><label>গ্রাম/ঠিকানা</label><input id="g1_village"></div>
        <div><label>পোস্ট/থানা/জেলা</label><input id="g1_ps_dist"></div>
      </div>
      <div class="row cols-3">
        <div><label>মোবাইল</label><input id="g1_mobile" type="tel" placeholder="01XXXXXXXXX" inputmode="numeric" pattern="01\d{9}"></div>
        <div><label>NID</label><input id="g1_nid"></div>
        <div><label>জন্ম তারিখ</label><input type="date" id="g1_dob"></div>
      </div>

      <h4>ঋণের বিবরণ</h4>
      <div class="row cols-3">
        <div><label>আবেদনের তারিখ</label><input type="date" id="loan_date" required></div>
        <div><label>কিস্তি শুরুর তারিখ</label><input type="date" id="inst_start"></div>
        <div><label>ঋণের পরিমাণ (৳)</label><input type="number" id="loan_amount" min="1" step="1" required></div>
      </div>
      <div class="row cols-3">
        <div><label>কিস্তি সংখ্যা</label><input type="number" id="inst_count" min="1" step="1"></div>
        <div><label>কিস্তি প্রতি পরিমাণ (৳)</label><input type="number" id="inst_amount" min="0" step="1"></div>
        <div><label>বিশেষ শর্ত/নোট</label><input id="note" placeholder="ঐচ্ছিক"></div>
      </div>

      <div class="sticky-actions">
        <div class="actions">
          <button type="button" id="saveBtn">Save</button>
          <button type="button" class="secondary" id="resetBtn">Reset</button>
          <button type="button" class="warn" id="printPreviewBtn">Print Preview</button>
          <button type="button" class="warn" id="stampPrintBtn">Stamp‑style Print</button>
        </div>
      </div>
    </form>
  </section>

  <!-- REPORT -->
  <section id="report" class="tab card" style="display:none;">
    <h3>রিপোর্ট</h3>
    <div class="actions" style="margin:8px 0;flex-wrap:wrap;">
      <input id="q" placeholder="নাম/মোবাইল/NID..." style="flex:1;min-width:220px;max-width:320px">
      <input type="date" id="from">
      <input type="date" id="to">
      <button id="filterBtn">Filter</button>
      <button class="secondary" id="clearFilterBtn">Clear</button>
      <button class="warn" id="printBtn">Print</button>
      <button class="secondary" id="exportBtn">Export CSV</button>
    </div>

    <div class="card">
      <div style="text-align:center;margin-bottom:8px;">
        <div style="font-weight:800" id="ph_name"></div>
        <div class="muted" id="ph_addr"></div>
        <div class="muted">ঋণ রিপোর্ট</div>
      </div>
      <table id="tbl">
        <thead>
          <tr>
            <th>#</th><th>তারিখ</th><th>ঋণগ্রহীতা</th><th>মোবাইল</th><th>NID</th><th>পরিমাণ (৳)</th><th>গ্যারান্টর</th><th>কিস্তি</th><th>নোট</th><th>অ্যাকশন</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
      <div class="muted" style="margin-top:8px;">মোট রেকর্ড: <span id="totalRows">0</span>, মোট ঋণ: <span id="sumAmount">৳0</span></div>
    </div>
  </section>

  <!-- SETTINGS -->
  <section id="settings" class="tab card" style="display:none;">
    <h3>সেটিংস</h3>
    <div class="row cols-2">
      <div><label>সমিতির নাম</label><input id="s_org_name" placeholder="যেমন: নক্ষত্র সমবায় সমিতি"></div>
      <div><label>ঠিকানা</label><input id="s_org_addr" placeholder="যেমন: বাটাজার, ভালুকা, ময়মনসিংহ"></div>
    </div>
    <div class="actions" style="margin-top:12px;">
      <button id="saveSettings">Save Settings</button>
      <button class="secondary" id="resetAll">⚠️ Reset All Data</button>
    </div>
  </section>
</main>

<!-- Hidden Iframe for print (no popup) -->
<iframe id="printFrame" style="width:0;height:0;border:0;position:absolute;left:-9999px;"></iframe>

<!-- GENERIC PRINT TEMPLATE -->
<template id="printTemplate">
  <div style="font-family:SolaimanLipi, Noto Sans Bengali, Arial; padding:20px;color:#111">
    <div style="text-align:center;margin-bottom:10px;">
      <div style="font-size:18px;font-weight:800" data-bind="org_name"></div>
      <div style="color:#555" data-bind="org_addr"></div>
      <div style="margin-top:6px;font-weight:700;">ঋণ গ্রহণের অঙ্গীকারনামা</div>
    </div>
    <div style="margin:10px 0;">
      আবেদন তারিখ: <strong data-bind="loan_date"></strong> | ঋণের পরিমাণ: <strong data-bind="loan_amount"></strong> টাকা
    </div>
    <hr>
    <h4>২য় পক্ষ ঋণগ্রহীতা</h4>
    <div>নাম: <strong data-bind="b_name"></strong></div>
    <div>পিতা/স্বামী: <strong data-bind="b_fh"></strong> | মাতা: <span data-bind="b_mother"></span></div>
    <div>পেশা: <span data-bind="b_profession"></span></div>
    <div>ঠিকানা: <span data-bind="b_village"></span>, <span data-bind="b_ps_dist"></span></div>
    <div>মোবাইল: <span data-bind="b_mobile"></span> | NID: <span data-bind="b_nid"></span> | জন্ম তারিখ: <span data-bind="b_dob"></span></div>

    <h4 style="margin-top:10px;">জামিনদার</h4>
    <div style="border:1px dashed #ddd;padding:8px;border-radius:8px;">
      নাম: <span data-bind="g1_name"></span><br>
      পিতা/স্বামী: <span data-bind="g1_fh"></span> | মাতা: <span data-bind="g1_mother"></span><br>
      পেশা: <span data-bind="g1_profession"></span><br>
      ঠিকানা: <span data-bind="g1_village"></span>, <span data-bind="g1_ps_dist"></span><br>
      মোবাইল: <span data-bind="g1_mobile"></span> | NID: <span data-bind="g1_nid"></span> | জন্ম: <span data-bind="g1_dob"></span>
    </div>

    <h4 style="margin-top:10px;">ঋণের শর্তাবলী</h4>
    <div>কিস্তি শুরু: <span data-bind="inst_start"></span> | কিস্তি সংখ্যা: <span data-bind="inst_count"></span> | কিস্তি প্রতি: <span data-bind="inst_amount"></span></div>
    <div>নোট: <span data-bind="note"></span></div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:30px;">
      <div>২য় পক্ষ ঋণগ্রহীতার স্বাক্ষর: ____________________<br><br>তারিখ: ____________</div>
      <div>জামিনদারের স্বাক্ষর: ____________________<br><br>তারিখ: ____________</div>
    </div>
  </div>
</template>

<!-- STAMP-STYLE PRINT TEMPLATE (as per Demo.pdf) -->
<template id="stampStyleTemplate">
  <div class="page" style="font-family:SolaimanLipi, Noto Sans Bengali, Arial; color:#111; position:relative;">
    <!-- Stamp box -->
    <div style="position:absolute;right:0;top:0;width:45mm;height:30mm;border:1px dashed #333;border-radius:3px;
                display:flex;align-items:center;justify-content:center;text-align:center;font-size:12px;">
      <div>
        <div style="font-weight:700">STAMP</div>
        <div style="font-size:11px;color:#555">নন‑জুডিশিয়াল স্ট্যাম্প<br/>এখানে লাগান</div>
      </div>
    </div>

    <!-- Header -->
    <div style="text-align:center;margin-bottom:10px;">
      <div style="font-size:18px;font-weight:800" data-bind="org_name"></div>
      <div style="color:#555" data-bind="org_addr"></div>
      <div style="margin-top:8px;font-size:16px;font-weight:800;">ঋণ গ্রহণের অঙ্গীকারনামা</div>
    </div>

    <!-- Intro / Parties -->
    <div style="display:flex;justify-content:space-between;color:#444;margin-bottom:8px;">
      <div>১ম পক্ষ/ঋণদাতা: <span data-bind="org_name"></span></div>
      <div>তারিখ: <span data-bind="loan_date"></span></div>
    </div>

    <!-- Declaration paragraph (adapted from Demo.pdf) -->
    <div style="margin-top:8px;line-height:1.6;text-align:justify;">
      আমি, ২য় পক্ষ/ঋণগ্রহীতা <span class="stamp-hl" data-bind="b_name"></span>, আমার ব্যবসায়িক প্রয়োজনে
      <span class="stamp-hl" data-bind="org_name"></span> কর্তৃক অনুমোদিত
      <span class="stamp-hl" data-bind="loan_date"></span> তারিখে
      <span class="stamp-hl" data-bind="loan_amount"></span> (টাকা) ঋণ গ্রহণ করিলাম।
      এই ঋণের বিপরীতে আমি প্রতি মাসে <span class="stamp-hl" data-bind="inst_amount"></span> টাকা করে মোট
      <span class="stamp-hl" data-bind="inst_count"></span> (বার) কিস্তিতে
      <span class="stamp-hl" data-bind="repay_total"></span> টাকা পরিশোধ করিতে বাধ্য থাকিব।
      শর্ত ভঙ্গ হলে সমিতির বিধিমোতাবেক **জামিনদারসহ** সমুদয় দায়ভার বহন করিব এবং
      সমিতি প্রয়োজনবোধে আইনানুগ ব্যবস্থা গ্রহণ করিতে পারিবে। (বিশেষ শর্ত/মন্তব্য: <span class="stamp-hl" data-bind="note"></span>)
    </div>

    <!-- Borrower & Guarantor blocks -->
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:12px;">
      <!-- Borrower -->
      <div>
        <div style="font-weight:700;margin-bottom:6px;">২য় পক্ষ/ঋণগ্রহীতা</div>
        <div>নাম: <span class="stamp-hl" data-bind="b_name"></span></div>
        <div>পিতা/স্বামী: <span class="stamp-hl" data-bind="b_fh"></span></div>
        <div>মাতা: <span class="stamp-hl" data-bind="b_mother"></span></div>
        <div>পেশা: <span class="stamp-hl" data-bind="b_profession"></span></div>
        <div>ঠিকানা: <span class="stamp-hl" data-bind="b_village"></span>, <span class="stamp-hl" data-bind="b_ps_dist"></span></div>
        <div>মোবাইল: <span class="stamp-hl" data-bind="b_mobile"></span></div>
        <div>NID/জন্ম নিবন্ধন: <span class="stamp-hl" data-bind="b_nid"></span></div>
        <div>জন্ম তারিখ: <span class="stamp-hl" data-bind="b_dob"></span></div>
      </div>

      <!-- Guarantor (single) -->
      <div>
        <div style="font-weight:700;margin-bottom:6px;">জামিনদার</div>
        <div style="border:1px solid #ddd;border-radius:6px;padding:8px;">
          <div>নাম: <span class="stamp-hl" data-bind="g1_name"></span></div>
          <div>পিতা/স্বামী: <span class="stamp-hl" data-bind="g1_fh"></span></div>
          <div>মাতা: <span class="stamp-hl" data-bind="g1_mother"></span></div>
          <div>পেশা: <span class="stamp-hl" data-bind="g1_profession"></span></div>
          <div>ঠিকানা: <span class="stamp-hl" data-bind="g1_village"></span>, <span class="stamp-hl" data-bind="g1_ps_dist"></span></div>
          <div>মোবাইল: <span class="stamp-hl" data-bind="g1_mobile"></span></div>
          <div>NID: <span class="stamp-hl" data-bind="g1_nid"></span></div>
          <div>জন্ম তারিখ: <span class="stamp-hl" data-bind="g1_dob"></span></div>
        </div>
      </div>
    </div>

    <!-- Witnesses -->
    <div style="margin-top:14px;">
      <div style="font-weight:700;margin-bottom:6px;">সাক্ষীগণের স্বাক্ষর</div>
      <div>১) ________________________________</div>
      <div>২) ________________________________</div>
      <div>৩) ________________________________</div>
      <div>৪) ________________________________</div>
    </div>

    <!-- Signatures -->
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-top:18px;">
      <div>
        <div>২য় পক্ষ/ঋণগ্রহীতার স্বাক্ষর: ____________________</div>
      </div>
      <div>
        <div>জামিনদারের স্বাক্ষর: ____________________</div>
      </div>
    </div>
  </div>
</template>

<script>
document.addEventListener('DOMContentLoaded', function(){
  const $ = sel => document.querySelector(sel);
  const $$ = sel => Array.from(document.querySelectorAll(sel));

  const storeKey = 'loan_records_v1';
  const orgKey = 'org_info_v1';
  const state = {
    list: [],
    editingId: null,
    org: { name:'নক্ষত্র সমবায় সমিতি', addr:'বাটাজার, ভালুকা, ময়মনসিংহ' } // Demo.pdf অনুকরণে ডিফল্ট [1](https://raidhacollectionslimited-my.sharepoint.com/personal/khairul_planning_raidhacollectionsbd_com/Documents/Microsoft%20Copilot%20Chat%20Files/Demo.pdf)
  };

  // helpers
  function todayStr(){ return new Date().toISOString().slice(0,10); }
  function bdt(n){ n = Number(n||0); return '৳' + n.toLocaleString('bn-BD'); }
  function escapeHtml(s){ return (s||'').replace(/[&<>\"']/g, m=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;' }[m])) }

  // storage
  function load(){
    try{
      const raw = localStorage.getItem(storeKey);
      state.list = raw ? JSON.parse(raw) : [];
      const o = localStorage.getItem(orgKey);
      state.org = o ? JSON.parse(o) : state.org;
    }catch(e){ state.list=[]; }
    bindOrg();
  }
  function save(){ localStorage.setItem(storeKey, JSON.stringify(state.list)); refreshKPIs(); renderTable(); }
  function saveOrg(){ localStorage.setItem(orgKey, JSON.stringify(state.org)); bindOrg(); }

  // tabs
  $$('.tab-btn').forEach(b=>{
    b.addEventListener('click', ()=>{
      $$('.tab-btn').forEach(x=>x.classList.remove('active'));
      b.classList.add('active');
      const id = b.dataset.tab;
      $$('.tab').forEach(sec=>sec.style.display = (sec.id===id)?'block':'none');
      if(id==='report'){ renderTable(); }
      if(id==='dashboard'){ refreshKPIs(); }
      if(id==='entry'){ fillOrgForm(); ensureDefaultDates(); }
    });
  });

  // org bindings
  function bindOrg(){
    $('#ph_name').textContent = state.org.name || '';
    $('#ph_addr').textContent = state.org.addr || '';
    $('#orgNameBadge').textContent = state.org.name || '';
    fillOrgForm();
    if($('#s_org_name')) $('#s_org_name').value = state.org.name || '';
    if($('#s_org_addr')) $('#s_org_addr').value = state.org.addr || '';
  }
  function fillOrgForm(){
    if($('#org_name')) $('#org_name').value = state.org.name || '';
    if($('#org_addr')) $('#org_addr').value = state.org.addr || '';
  }

  // KPIs
  function refreshKPIs(){
    $('#kpi_total').textContent = state.list.length.toLocaleString('bn-BD');
    const t = todayStr();
    $('#kpi_today').textContent = state.list.filter(x=>x.loan_date===t).length.toLocaleString('bn-BD');
    const sum = state.list.reduce((s,x)=>s + Number(x.loan_amount||0), 0);
    $('#kpi_amount').textContent = bdt(sum);
  }

  // form
  function ensureDefaultDates(){ if(!$('#loan_date').value) $('#loan_date').value = todayStr(); }
  function nextId(){ return state.list.reduce((m,x)=>Math.max(m, x.id||0), 0) + 1; }
  function getForm(){
    const d = {
      id: state.editingId || nextId(),
      org_name: state.org.name, org_addr: state.org.addr,

      // Borrower
      b_name: $('#b_name').value.trim(),
      b_fh: $('#b_fh').value.trim(),
      b_mother: $('#b_mother').value.trim(),
      b_profession: $('#b_profession').value.trim(),
      b_village: $('#b_village').value.trim(),
      b_ps_dist: $('#b_ps_dist').value.trim(),
      b_mobile: $('#b_mobile').value.trim(),
      b_nid: $('#b_nid').value.trim(),
      b_dob: $('#b_dob').value,

      // Guarantor (one only)
      g1_name: $('#g1_name').value.trim(),
      g1_fh: $('#g1_fh').value.trim(),
      g1_mother: $('#g1_mother').value.trim(),
      g1_profession: $('#g1_profession').value.trim(),
      g1_village: $('#g1_village').value.trim(),
      g1_ps_dist: $('#g1_ps_dist').value.trim(),
      g1_mobile: $('#g1_mobile').value.trim(),
      g1_nid: $('#g1_nid').value.trim(),
      g1_dob: $('#g1_dob').value,

      // Loan
      loan_date: $('#loan_date').value,
      inst_start: $('#inst_start').value,
      loan_amount: Number($('#loan_amount').value||0),
      inst_count: $('#inst_count').value ? Number($('#inst_count').value) : '',
      inst_amount: $('#inst_amount').value ? Number($('#inst_amount').value) : '',
      note: $('#note').value.trim(),

      created_at: state.editingId ? undefined : new Date().toISOString(),
      updated_at: new Date().toISOString()
    };
    return d;
  }
  function validate(d){
    const errs = [];
    if(!d.b_name) errs.push('ঋণগ্রহীতার নাম দিন');
    if(!d.b_fh) errs.push('পিতা/স্বামীর নাম দিন');
    if(!d.loan_date) errs.push('আবেদনের তারিখ দিন');
    if(!(d.loan_amount>0)) errs.push('ঋণের পরিমাণ সঠিক দিন');
    const mob = s=> /^01\d{9}$/.test(s);
    if(d.b_mobile && !mob(d.b_mobile)) errs.push('ঋণগ্রহীতার মোবাইল 01XXXXXXXXX অথবা ফাঁকা');
    if(d.g1_mobile && !mob(d.g1_mobile)) errs.push('জামিনদারের মোবাইল 01XXXXXXXXX অথবা ফাঁকা');
    return errs;
  }
  function resetForm(){ $('#loanForm').reset(); state.editingId = null; $('#id').value=''; ensureDefaultDates(); }

  $('#resetBtn').addEventListener('click', resetForm);

  $('#saveBtn').addEventListener('click', ()=>{
    const data = getForm();
    const errs = validate(data);
    if(errs.length){ alert('ত্রুটি:\n- ' + errs.join('\n- ')); return; }

    if(state.editingId){
      const i = state.list.findIndex(x=>x.id===state.editingId);
      if(i>-1) state.list[i] = {...state.list[i], ...data};
      state.editingId = null;
    }else{
      state.list.push(data);
    }
    save();
    alert('সফলভাবে সংরক্ষণ হয়েছে');
    resetForm();
  });

  // load to form (Edit)
  function loadToForm(id){
    const x = state.list.find(r=>r.id===id); if(!x) return;
    state.editingId = x.id;
    [
      'b_name','b_fh','b_mother','b_profession','b_village','b_ps_dist','b_mobile','b_nid','b_dob',
      'g1_name','g1_fh','g1_mother','g1_profession','g1_village','g1_ps_dist','g1_mobile','g1_nid','g1_dob',
      'loan_date','inst_start','loan_amount','inst_count','inst_amount','note'
    ].forEach(k=>{ const el = document.getElementById(k); if(el) el.value = (x[k]??''); });
    document.querySelector('[data-tab="entry"]').click();
  }

  // report table
  function filters(){ return { q: $('#q').value.trim().toLowerCase(), f: $('#from').value, t: $('#to').value }; }
  function applyFilter(arr){
    const {q,f,t} = filters();
    let a = arr.slice();
    if(q) a = a.filter(x=>[x.b_name,x.b_mobile,x.b_nid].join(' ').toLowerCase().includes(q));
    if(f) a = a.filter(x=>!x.loan_date || x.loan_date>=f);
    if(t) a = a.filter(x=>!x.loan_date || x.loan_date<=t);
    return a;
  }
  function rowHtml(x,i){
    const g = [x.g1_name].filter(Boolean).join(', ');
    const inst = [x.inst_count||'', x.inst_amount?('x '+x.inst_amount):''].filter(Boolean).join(' ');
    return `<tr>
      <td>${i+1}</td><td>${x.loan_date||''}</td>
      <td><strong>${escapeHtml(x.b_name||'')}</strong><br><span class="muted">${escapeHtml(x.b_village||'')}</span></td>
      <td>${escapeHtml(x.b_mobile||'')}</td><td>${escapeHtml(x.b_nid||'')}</td>
      <td>${bdt(x.loan_amount||0)}</td>
      <td>${escapeHtml(g)}</td><td>${escapeHtml(inst)}</td>
      <td>${escapeHtml(x.note||'')}</td>
      <td>
        <button data-act="edit" data-id="${x.id}">Edit</button>
        <button class="danger" data-act="del" data-id="${x.id}">Delete</button>
        <button class="warn" data-act="stamp" data-id="${x.id}">Stamp</button>
      </td>
    </tr>`;
  }
  function renderTable(){
    $('#ph_name').textContent = state.org.name||'';
    $('#ph_addr').textContent = state.org.addr||'';
    const body = $('#tbl tbody');
    const arr = applyFilter(state.list);
    body.innerHTML = arr.map(rowHtml).join('');
    $('#totalRows').textContent = arr.length.toLocaleString('bn-BD');
    const sum = arr.reduce((s,x)=>s+Number(x.loan_amount||0),0);
    $('#sumAmount').textContent = bdt(sum);

    body.querySelectorAll('button').forEach(btn=>{
      btn.addEventListener('click', ()=>{
        const act = btn.dataset.act, id = Number(btn.dataset.id);
        if(act==='edit') loadToForm(id);
        if(act==='del'){ if(confirm('নিশ্চিতভাবে ডিলিট করবেন?')){ state.list = state.list.filter(x=>x.id!==id); save(); } }
        if(act==='stamp'){
          const rec = state.list.find(r=>r.id===id);
          if(rec){ const html = buildStampPrintHTML(rec, state.org); printViaIframe(html); }
        }
      });
    });
  }
  $('#filterBtn').addEventListener('click', renderTable);
  $('#clearFilterBtn').addEventListener('click', ()=>{ $('#q').value=''; $('#from').value=''; $('#to').value=''; renderTable(); });

  // CSV Export (without G2)
  $('#exportBtn').addEventListener('click', ()=>{
    const rows = [['ID','Date','Borrower','Mobile','NID','Amount','Guarantor','Installments','Note']];
    const arr = applyFilter(state.list);
    arr.forEach(x=>{
      rows.push([x.id,x.loan_date,x.b_name,x.b_mobile,x.b_nid,x.loan_amount,x.g1_name||'',(x.inst_count||'')+(x.inst_amount?(' x '+x.inst_amount):''),x.note||'']);
    });
    const csv = rows.map(r=>r.map(s=>`"${String(s??'').replace(/"/g,'""')}"`).join(',')).join('\n');
    const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
    const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download='loan_report.csv'; a.click(); URL.revokeObjectURL(a.href);
  });

  // PRINT – no popup (iframe)
  function printViaIframe(html){
    let iframe = document.getElementById('printFrame');
    if(!iframe){ iframe = document.createElement('iframe'); iframe.id='printFrame'; iframe.style.cssText='width:0;height:0;border:0;position:absolute;left:-9999px;'; document.body.appendChild(iframe); }
    const doc = iframe.contentDocument || iframe.contentWindow.document;
    doc.open(); doc.write(html); doc.close();
    setTimeout(()=>{ iframe.contentWindow.focus(); iframe.contentWindow.print(); }, 150);
  }

  function buildSinglePrintHTML(data){
    const wrap = document.createElement('div');
    const tpl = document.querySelector('#printTemplate').content.cloneNode(true);
    tpl.querySelectorAll('[data-bind]').forEach(el=>{
      const k = el.getAttribute('data-bind');
      el.textContent = (data[k]??'');
    });
    wrap.appendChild(tpl);
    const html = `
      <html><head><meta charset="utf-8"><title>Print</title>
      <style>
        body{font-family:SolaimanLipi, Noto Sans Bengali, Arial; padding:18px; color:#111}
        h4{margin:8px 0 4px 0}
        @page{ size:A4; margin:12mm }
      </style></head><body>${wrap.innerHTML}</body></html>`;
    return html;
  }

  function buildStampPrintHTML(data, org){
    // Bengali currency for loan_amount + computed repay_total if possible
    const dataClone = {...data};
    const count = Number(data.inst_count||0);
    const per   = Number(data.inst_amount||0);
    const total = (count>0 && per>0) ? (count*per) : '';
    dataClone.loan_amount = (data.loan_amount?('৳'+Number(data.loan_amount).toLocaleString('bn-BD')):'');
    dataClone.repay_total = total? ('৳'+Number(total).toLocaleString('bn-BD')) : '';

    const wrap = document.createElement('div');
    const tpl = document.querySelector('#stampStyleTemplate').content.cloneNode(true);

    // bind org first
    tpl.querySelectorAll('[data-bind="org_name"]').forEach(el=> el.textContent = org.name||'');
    tpl.querySelectorAll('[data-bind="org_addr"]').forEach(el=> el.textContent = org.addr||'');

    // bind fields
    tpl.querySelectorAll('[data-bind]').forEach(el=>{
      const k = el.getAttribute('data-bind');
      if(k==='org_name' || k==='org_addr') return;
      el.textContent = (dataClone[k]??'');
    });

    wrap.appendChild(tpl);
    const html = `
      <html><head><meta charset="utf-8"><title>Stamp Print</title>
      <style>
        body{font-family:SolaimanLipi, Noto Sans Bengali, Arial; padding:12mm; color:#111}
        .stamp-hl{background:#fff59d;padding:0 3px;border-radius:2px}
        @page{ size:A4; margin:12mm }
      </style></head><body>${wrap.innerHTML}</body></html>`;
    return html;
  }

  function buildTablePrintHTML(arr){
    const rows = arr.map((x,i)=>`
      <tr>
        <td>${i+1}</td><td>${x.loan_date||''}</td><td>${x.b_name||''}</td>
        <td>${x.b_mobile||''}</td><td>${x.b_nid||''}</td><td>${x.loan_amount||0}</td>
        <td>${[x.g1_name].filter(Boolean).join(', ')}</td>
        <td>${(x.inst_count||'') + (x.inst_amount?(' x '+x.inst_amount):'')}</td>
        <td>${x.note||''}</td>
      </tr>`).join('');
    const html = `
      <html><head><meta charset="utf-8"><title>Report</title>
      <style>
        body{font-family:SolaimanLipi, Noto Sans Bengali, Arial; padding:12mm}
        h3{text-align:center;margin:0 0 6px 0}
        table{width:100%;border-collapse:collapse}
        th,td{border:1px solid #ddd;padding:6px;font-size:12px}
        @page{ size:A4; margin:10mm }
      </style></head>
      <body>
        <h3>${state.org.name}</h3>
        <div style="text-align:center;color:#555">${state.org.addr}</div>
        <div style="text-align:center;margin:6px 0 10px 0;">ঋণ রিপোর্ট</div>
        <table>
          <thead><tr>
            <th>#</th><th>তারিখ</th><th>ঋণগ্রহীতা</th><th>মোবাইল</th><th>NID</th><th>পরিমাণ</th><th>গ্যারান্টর</th><th>কিস্তি</th><th>নোট</th>
          </tr></thead>
          <tbody>${rows}</tbody>
        </table>
      </body></html>`;
    return html;
  }

  // Buttons: preview/print
  $('#printPreviewBtn').addEventListener('click', ()=>{
    const data = getForm();
    if(!data.b_name){ alert('প্রিভিউর জন্য নাম দিন'); return; }
    if(!data.loan_date) data.loan_date = todayStr();
    const html = buildSinglePrintHTML(data);
    printViaIframe(html);
  });

  $('#stampPrintBtn').addEventListener('click', ()=>{
    const d = getForm();
    if(!d.b_name){ alert('নাম দিন (প্রিভিউর জন্য)'); return; }
    if(!d.loan_date){ d.loan_date = todayStr(); }
    const html = buildStampPrintHTML(d, state.org);
    printViaIframe(html);
  });

  $('#printBtn').addEventListener('click', ()=>{
    const arr = applyFilter(state.list);
    if(!arr.length){ alert('প্রিন্ট করার জন্য কোনো রেকর্ড নেই'); return; }
    const html = buildTablePrintHTML(arr);
    printViaIframe(html);
  });

  // settings
  $('#saveSettings').addEventListener('click', ()=>{
    state.org.name = $('#s_org_name').value.trim() || 'সমবায় সমিতি';
    state.org.addr = $('#s_org_addr').value.trim() || '';
    saveOrg();
    alert('সেটিংস সেভ হয়েছে');
  });
  $('#resetAll').addEventListener('click', ()=>{
    if(!confirm('⚠️ সব ডাটা মুছে যাবে। নিশ্চিত?')) return;
    localStorage.removeItem(storeKey); localStorage.removeItem(orgKey);
    load(); save(); alert('রিসেট সম্পন্ন');
  });

  // init
  load();
  refreshKPIs();
  setTimeout(()=>{ if($('#loan_date')) $('#loan_date').value = todayStr(); }, 0);
});
</script>
</body>
</html>
