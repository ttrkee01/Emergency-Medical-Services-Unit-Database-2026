

<!DOCTYPE html>
<html lang="ar" dir="rtl" id="root">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KSUMC — لوحة الأداء التشغيلي 2026</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700;800;900&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --kb:#0084BD;--kb-dk:#005f8a;--kb-lt:#e6f4fb;--kb-mid:#3BAAD4;
  --kc:#E3E0D2;--kg:#748995;--kg-lt:#f0f2f3;
  --text:#1a1a1a;--text2:#4a5568;--text3:#748995;
  --bg:#f2f4f7;--card:#fff;--border:#dde3e8;
  --r:10px;--sh:0 2px 8px rgba(0,132,189,.09);
  --red:#ef4444;--red-lt:#fee2e2;
  --green:#16a34a;--green-lt:#dcfce7;
  --orange:#ea580c;--orange-lt:#ffedd5;
  --purple:#7c3aed;--purple-lt:#ede9fe;
  --teal:#0d9488;--teal-lt:#ccfbf1;
  --amber:#d97706;--amber-lt:#fef3c7;
  --emerald:#059669;--emerald-lt:#d1fae5;
}
[dir=ltr]{font-family:'Inter',sans-serif}
[dir=rtl]{font-family:'Cairo',sans-serif}
body{background:var(--bg);color:var(--text);min-height:100vh;direction:rtl}
[dir=ltr] body{direction:ltr}

/* ── STRIPE ── */
.stripe{height:4px;background:linear-gradient(90deg,#005f8a,#0084BD,#3BAAD4,#E3E0D2)}

/* ── HEADER ── */
.header{background:linear-gradient(135deg,#004d73 0%,#0084BD 55%,#3BAAD4 100%);color:#fff;padding:0 20px;position:sticky;top:0;z-index:300;box-shadow:0 4px 20px rgba(0,80,140,.28)}
.hdr-top{display:flex;align-items:center;justify-content:space-between;padding:11px 0 8px;flex-wrap:wrap;gap:8px}
.hdr-logo{display:flex;align-items:center;gap:12px}
.shield{width:48px;height:58px;background:rgba(255,255,255,.14);border-radius:4px 4px 24px 24px;display:flex;align-items:center;justify-content:center;border:1.5px solid rgba(255,255,255,.32);flex-shrink:0}
.lt1{font-size:15px;font-weight:800;color:#fff;line-height:1.2}
.lt2{font-size:10px;color:rgba(255,255,255,.75);font-weight:500}
.lt3{font-size:9px;color:rgba(255,255,255,.6);font-family:'Inter',sans-serif}
.hdr-center{text-align:center}
.hdr-center .yr{font-size:26px;font-weight:900;color:#fff;line-height:1}
.hdr-center .ys{font-size:10px;color:rgba(255,255,255,.7)}
.hdr-acts{display:flex;gap:5px;align-items:center;flex-wrap:wrap}
.abtn{background:rgba(255,255,255,.16);border:1.5px solid rgba(255,255,255,.28);color:#fff;padding:6px 11px;border-radius:18px;font-size:11px;font-weight:600;cursor:pointer;transition:all .18s;display:inline-flex;align-items:center;gap:4px;white-space:nowrap}
.abtn:hover{background:rgba(255,255,255,.26)}
.abtn svg{width:13px;height:13px;fill:currentColor;flex-shrink:0}
.abtn-admin{background:rgba(255,200,0,.18);border-color:rgba(255,200,0,.4)}
.abtn-admin.active{background:rgba(255,200,0,.3);border-color:gold}
.lang-sel{background:rgba(255,255,255,.16);border:1.5px solid rgba(255,255,255,.28);color:#fff;padding:5px 10px;border-radius:18px;font-size:11px;font-weight:600;cursor:pointer;font-family:'Cairo',sans-serif;appearance:none;-webkit-appearance:none}
.lang-sel option{color:#1a1a1a;background:#fff}

/* ── NAV ── */
.nav{display:flex;gap:1px;overflow-x:auto;padding-bottom:1px;scrollbar-width:none}
.nav::-webkit-scrollbar{display:none}
.nb{padding:8px 13px;font-size:11.5px;font-weight:600;color:rgba(255,255,255,.62);background:transparent;border:none;border-bottom:3px solid transparent;cursor:pointer;white-space:nowrap;transition:all .16s}
.nb.active,.nb:hover{color:#fff;border-bottom-color:#fff}

/* ── MAIN ── */
.main{max-width:1400px;margin:0 auto;padding:18px 16px}
.page{display:none}.page.active{display:block}

/* ── SECTION HEADER ── */
.sec{display:flex;align-items:center;gap:8px;margin-bottom:14px;padding-bottom:10px;border-bottom:2px solid var(--kb-lt)}
.sec::before{content:'';width:4px;height:22px;background:var(--kb);border-radius:2px;flex-shrink:0}
.sec-text{font-size:15px;font-weight:800;color:var(--kb)}

/* ── BANNER ── */
.banner{background:#fff;border:1.5px dashed var(--kb);border-radius:var(--r);padding:10px 14px;margin-bottom:16px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;font-size:12px;color:var(--text2)}
.banner strong{color:var(--kb)}

/* ── KPI CARDS ── */
.kpi5{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin-bottom:16px}
@media(max-width:1100px){.kpi5{grid-template-columns:repeat(3,1fr)}}
@media(max-width:650px){.kpi5{grid-template-columns:repeat(2,1fr)}}
@media(max-width:380px){.kpi5{grid-template-columns:1fr}}

.kpi{background:var(--card);border-radius:var(--r);padding:15px 17px;box-shadow:var(--sh);border-top:5px solid var(--c,var(--kb));position:relative;overflow:hidden;transition:transform .15s,box-shadow .15s}
.kpi::before{content:'';position:absolute;top:0;left:0;right:0;height:5px;background:linear-gradient(90deg,var(--c1,var(--c,#0084BD)),var(--c2,var(--c,#3BAAD4)))}
.kpi:hover{transform:translateY(-2px);box-shadow:0 6px 22px rgba(0,132,189,.14)}
.kpi-lbl{font-size:10.5px;color:var(--text2);font-weight:700;line-height:1.4;margin-bottom:7px}
.kpi-val{font-size:36px;font-weight:900;color:var(--c,var(--kb));line-height:1;margin-bottom:8px}
.kpi-row{display:flex;gap:5px;flex-wrap:wrap}
.kpi-bp{display:inline-flex;align-items:center;gap:4px;padding:2px 8px;border-radius:12px;font-size:10px;font-weight:700}
.kpi-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0}

/* ── CARD ── */
.card{background:var(--card);border-radius:var(--r);padding:16px;box-shadow:var(--sh);border:1px solid var(--border)}
.ch{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:11px;gap:8px;flex-wrap:wrap}
.ct{font-size:13px;font-weight:700;color:var(--text)}
.cs{font-size:10.5px;color:var(--text3);margin-top:2px}
.cw{position:relative}

/* ── GRIDS ── */
.g2{display:grid;grid-template-columns:3fr 2fr;gap:12px;margin-bottom:12px}
.g2b{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:12px}
.g4{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:12px}
.g5{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin-bottom:12px}
@media(max-width:1100px){.g5{grid-template-columns:repeat(3,1fr)}}
@media(max-width:900px){.g3,.g4{grid-template-columns:repeat(2,1fr)}}
@media(max-width:820px){.g2,.g2b{grid-template-columns:1fr}}
@media(max-width:640px){.g5{grid-template-columns:repeat(2,1fr)}}

/* ── EVAC BANNER ── */
.evac-banner{background:linear-gradient(135deg,#0f766e,#0d9488);border-radius:var(--r);padding:14px 18px;margin-bottom:12px;color:#fff;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px}
.evac-title{font-size:13px;font-weight:800}
.evac-sub{font-size:11px;opacity:.8;margin-top:2px}
.evac-num{font-size:40px;font-weight:900}
.evac-lbl{font-size:11px;opacity:.8}

/* ── MONTH HERO ── */
.mhero{border-radius:var(--r);padding:18px 20px;margin-bottom:14px;color:#fff}
.mht{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;flex-wrap:wrap;gap:10px}
.mht-title{font-size:18px;font-weight:900}
.mht-sub{font-size:11px;opacity:.8;margin-top:2px}
.mtot{background:rgba(255,255,255,.2);border-radius:9px;padding:9px 18px;text-align:center;border:1.5px solid rgba(255,255,255,.32)}
.mtot-n{font-size:30px;font-weight:900}
.mtot-l{font-size:10px;opacity:.8}
.mmetrics{display:grid;grid-template-columns:repeat(9,1fr);gap:7px}
@media(max-width:1100px){.mmetrics{grid-template-columns:repeat(5,1fr)}}
@media(max-width:600px){.mmetrics{grid-template-columns:repeat(3,1fr)}}
@media(max-width:380px){.mmetrics{grid-template-columns:repeat(2,1fr)}}
.mmc{background:rgba(255,255,255,.14);border-radius:7px;padding:10px;text-align:center;border:1px solid rgba(255,255,255,.2)}
.mmn{font-size:9.5px;font-weight:700;margin-bottom:4px;opacity:.9;line-height:1.3}
.mmv{font-size:22px;font-weight:900}

/* ── LEGEND ── */
.leg{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:9px;font-size:11px;color:var(--text2)}
.leg span{display:flex;align-items:center;gap:4px}
.lsq{width:10px;height:10px;border-radius:2px;flex-shrink:0}

/* ── PROGRESS ── */
.pr-row{display:flex;align-items:center;gap:8px;margin-bottom:8px}
.pr-lbl{font-size:11px;color:var(--text2);min-width:130px;text-align:right;font-weight:600}
[dir=ltr] .pr-lbl{text-align:left}
.pr-tr{flex:1;background:var(--kg-lt);border-radius:4px;height:8px;overflow:hidden}
.pr-fi{height:100%;border-radius:4px;transition:width 1.2s cubic-bezier(.4,0,.2,1)}
.pr-val{font-size:11px;font-weight:700;min-width:32px;color:var(--kb)}

/* ── TABLE ── */
.tw{overflow-x:auto;border-radius:8px;border:1px solid var(--border)}
table{width:100%;border-collapse:collapse;font-size:11px;min-width:600px}
th{background:var(--kb);color:#fff;padding:9px 10px;text-align:center;font-weight:700;font-size:10.5px;white-space:nowrap}
td{padding:7px 9px;text-align:center;border-bottom:1px solid var(--border);white-space:nowrap}
tr:last-child td{border-bottom:none}
tr:nth-child(even) td{background:var(--kg-lt)}
tr:hover td{background:var(--kb-lt)}
.pill{display:inline-block;padding:2px 9px;border-radius:20px;font-size:10.5px;font-weight:700}

/* ── BUTTONS ── */
.btnprim{background:var(--kb);color:#fff;border:none;padding:8px 16px;border-radius:8px;font-size:12.5px;font-weight:700;cursor:pointer;font-family:'Cairo',sans-serif;display:inline-flex;align-items:center;gap:5px;transition:background .15s}
.btnprim:hover{background:var(--kb-dk)}
.btnprim svg{width:14px;height:14px;fill:currentColor;flex-shrink:0}
.btnsec{background:#fff;color:var(--text2);border:1.5px solid var(--border);padding:8px 16px;border-radius:8px;font-size:12.5px;font-weight:600;cursor:pointer;font-family:'Cairo',sans-serif;transition:all .15s}
.btncanc:hover,.btnsec:hover{border-color:var(--kb);color:var(--kb)}

/* ── QUARTER TABS ── */
.qtabs{display:flex;gap:6px;margin-bottom:14px;flex-wrap:wrap}
.qtab{padding:7px 18px;border-radius:20px;border:1.5px solid var(--border);background:#fff;font-size:12px;font-weight:700;cursor:pointer;color:var(--text2);transition:all .15s;font-family:'Cairo',sans-serif}
.qtab.active{background:var(--kb);color:#fff;border-color:var(--kb)}

/* ── MODALS ── */
.modal-ov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.48);z-index:1000;align-items:center;justify-content:center;padding:12px}
.modal-ov.open{display:flex}
.modal{background:#fff;border-radius:14px;padding:24px;width:min(980px,98vw);max-height:92vh;overflow-y:auto;box-shadow:0 24px 64px rgba(0,0,0,.22)}
.modal-sm{background:#fff;border-radius:14px;padding:24px;width:min(500px,96vw);box-shadow:0 24px 64px rgba(0,0,0,.22)}
.mt-h{font-size:16px;font-weight:800;color:var(--kb);margin-bottom:4px}
.mt-s{font-size:11px;color:var(--text3);margin-bottom:16px}
.ed-sec{margin-bottom:16px}
.ed-sec-hd{font-size:12px;font-weight:800;padding:7px 12px;border-radius:7px;margin-bottom:9px;border-right:4px solid var(--edc,var(--kb));background:var(--edb,var(--kb-lt));color:var(--edc,var(--kb))}
[dir=ltr] .ed-sec-hd{border-right:none;border-left:4px solid var(--edc,var(--kb))}
.mgrid{display:grid;grid-template-columns:repeat(6,1fr);gap:7px}
@media(max-width:700px){.mgrid{grid-template-columns:repeat(3,1fr)}}
@media(max-width:420px){.mgrid{grid-template-columns:repeat(2,1fr)}}
.mf{display:flex;flex-direction:column;gap:3px}
.mf label{font-size:10px;font-weight:600;color:var(--text2);line-height:1.3}
.mf input{border:1.5px solid var(--border);border-radius:6px;padding:6px 8px;font-family:'Cairo',sans-serif;font-size:13px;font-weight:700;color:var(--kb);text-align:center;transition:border .15s;width:100%}
.mf input:focus{outline:none;border-color:var(--kb)}
.macts{display:flex;gap:8px;justify-content:flex-end;padding-top:12px;border-top:1px solid var(--border);margin-top:8px}

/* ── SHARE MODAL ── */
.surl{display:flex;gap:7px;margin:12px 0}
.surl input{flex:1;border:1.5px solid var(--border);border-radius:8px;padding:8px 10px;font-family:monospace;font-size:11px;color:var(--text2);background:var(--kg-lt)}
.scpy{background:var(--kb);color:#fff;border:none;padding:8px 14px;border-radius:8px;font-size:12px;font-weight:700;cursor:pointer;white-space:nowrap;font-family:'Cairo',sans-serif}
.smeth{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:12px}
.sbtn{padding:9px;border-radius:8px;border:1.5px solid var(--border);background:#fff;cursor:pointer;font-size:11px;font-weight:600;color:var(--text2);display:flex;flex-direction:column;align-items:center;gap:4px;transition:all .15s;font-family:'Cairo',sans-serif}
.sbtn:hover{border-color:var(--kb);color:var(--kb);background:var(--kb-lt)}
.sbtn svg{width:22px;height:22px;fill:currentColor}

/* ── TOAST ── */
.toast{position:fixed;bottom:22px;left:50%;transform:translateX(-50%);background:#1a1a1a;color:#fff;padding:10px 22px;border-radius:20px;font-size:12.5px;font-weight:600;opacity:0;transition:opacity .3s;pointer-events:none;z-index:3000;white-space:nowrap}
.toast.show{opacity:1}

/* ── FOOTER ── */
.footer{background:var(--kb);color:rgba(255,255,255,.7);text-align:center;padding:13px;font-size:11px}

/* ── PRINT ── */
@media print{
  .header .hdr-acts,.banner,.nb,.abtn,.btnprim,.btncanc,.btnprim,.qtabs{display:none!important}
  .header{position:relative}
  .page{display:block!important;page-break-after:always}
  .card,.kpi{box-shadow:none;border:1px solid #ddd}
}

/* ── RANK LIST ── */
.rank-item{display:flex;align-items:center;gap:8px;margin-bottom:7px;font-size:11.5px}
.rank-num{width:20px;height:20px;border-radius:50%;background:var(--kb);color:#fff;font-size:9px;font-weight:800;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.rank-bar{flex:1;background:var(--kg-lt);border-radius:4px;height:7px;overflow:hidden}
.rank-fill{height:100%;border-radius:4px}
.rank-val{font-size:11px;font-weight:700;min-width:28px;color:var(--text2)}

/* monthly gradients */
.mg0{background:linear-gradient(135deg,#005f8a,#0084BD)}
.mg1{background:linear-gradient(135deg,#006A9E,#0084BD)}
.mg2{background:linear-gradient(135deg,#0084BD,#3BAAD4)}
.mg3{background:linear-gradient(135deg,#006A9E,#3BAAD4)}
.mg4{background:linear-gradient(135deg,#3BAAD4,#0084BD)}
.mg5{background:linear-gradient(135deg,#4a7a9b,#16a34a)}
.mg6{background:linear-gradient(135deg,#ea580c,#d97706)}
.mg7{background:linear-gradient(135deg,#0084BD,#ea580c)}
.mg8{background:linear-gradient(135deg,#3BAAD4,#005f8a)}
.mg9{background:linear-gradient(135deg,#748995,#4a5568)}
.mg10{background:linear-gradient(135deg,#4a5568,#748995)}
.mg11{background:linear-gradient(135deg,#2c3e50,#4a5568)}
</style>
</head>
<body>
<div class="stripe"></div>

<!-- ═══════════ HEADER ═══════════ -->
<header class="header">
  <div class="hdr-top">
    <div class="hdr-logo">
      <div class="shield">
        <svg viewBox="0 0 40 48" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M5 5L35 5Q38 5 38 8L38 30Q38 44 20 48Q2 44 2 30L2 8Q2 5 5 5Z" fill="rgba(255,255,255,0.2)" stroke="rgba(255,255,255,0.45)" stroke-width="1.2"/>
          <text x="20" y="20" text-anchor="middle" font-family="Arial" font-size="10" font-weight="bold" fill="white">KSU</text>
          <text x="20" y="30" text-anchor="middle" font-family="Arial" font-size="5" fill="rgba(255,255,255,.85)">MEDICAL</text>
          <text x="20" y="39" text-anchor="middle" font-family="Arial" font-size="4.5" fill="rgba(255,255,255,.72)">CITY</text>
        </svg>
      </div>
      <div>
        <div class="lt1" data-i18n="hosp_name">المدينة الطبية الجامعية</div>
        <div class="lt2" data-i18n="hosp_sub">جامعة الملك سعود · الرياض</div>
        <div class="lt3">King Saud University Medical City — KSUMC</div>
      </div>
    </div>
    <div class="hdr-center">
      <div class="yr" id="yr-display">2026</div>
      <div class="ys" data-i18n="report_year">التقرير السنوي</div>
    </div>
    <div class="hdr-acts">
      <!-- Language Switch -->
      <select class="lang-sel" onchange="setLang(this.value)" id="langSel">
        <option value="ar">🌐 العربية</option>
        <option value="en">🌐 English</option>
      </select>
      <!-- Year select -->
      <select class="lang-sel" onchange="setYear(this.value)" id="yearSel">
        <option value="2024">2024</option>
        <option value="2025">2025</option>
        <option value="2026" selected>2026</option>
      </select>
      <!-- Admin -->
      <button class="abtn abtn-admin" id="loginBtn" onclick="adminLogin()">
        <svg viewBox="0 0 24 24"><path d="M12 2a4 4 0 014 4 4 4 0 01-4 4 4 4 0 01-4-4 4 4 0 014-4m0 10c4.42 0 8 1.79 8 4v2H4v-2c0-2.21 3.58-4 8-4z"/></svg>
        <span data-i18n="admin_login">دخول المسؤول</span>
      </button>
      <button class="abtn" id="editBtn" onclick="openEditor()" style="display:none">
        <svg viewBox="0 0 24 24"><path d="M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04a1 1 0 000-1.41l-2.34-2.34a1 1 0 00-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"/></svg>
        <span data-i18n="edit_data">تعديل البيانات</span>
      </button>
      <button class="abtn" onclick="openShare()">
        <svg viewBox="0 0 24 24"><path d="M18 16.08c-.76 0-1.44.3-1.96.77L8.91 12.7c.05-.23.09-.46.09-.7s-.04-.47-.09-.7l7.05-4.11A2.99 2.99 0 0018 8a3 3 0 000-6 3 3 0 00-3 3c0 .24.04.47.09.7L8.04 9.81A2.99 2.99 0 006 9a3 3 0 000 6c.79 0 1.5-.31 2.04-.81l7.12 4.16c-.05.21-.08.43-.08.65a2.92 2.92 0 102.92-2.92z"/></svg>
        <span data-i18n="share">مشاركة</span>
      </button>
      <button class="abtn" onclick="exportCSV()">
        <svg viewBox="0 0 24 24"><path d="M5 20h14v-2H5v2zm0-10h4v6h6v-6h4l-7-7-7 7z"/></svg>
        CSV
      </button>
      <button class="abtn" onclick="window.print()">
        <svg viewBox="0 0 24 24"><path d="M19 8H5c-1.66 0-3 1.34-3 3v6h4v4h12v-4h4v-6c0-1.66-1.34-3-3-3zm-3 11H8v-5h8v5zm3-7c-.55 0-1-.45-1-1s.45-1 1-1 1 .45 1 1-.45 1-1 1zm-1-9H6v4h12V3z"/></svg>
        <span data-i18n="print">طباعة</span>
      </button>
    </div>
  </div>
  <nav class="nav">
    <button class="nb active" onclick="showPage('ov',this)" data-i18n="nav_overview">نظرة عامة</button>
    <button class="nb" onclick="showPage('monthly',this)" data-i18n="nav_monthly">شهري</button>
    <button class="nb" onclick="showPage('quarterly',this)" data-i18n="nav_quarterly">ربعي</button>
    <button class="nb" onclick="showPage('cmp',this)" data-i18n="nav_compare">التحليل المقارن</button>
    <button class="nb" onclick="showPage('dtl',this)" data-i18n="nav_data">البيانات الكاملة</button>
  </nav>
</header>

<div class="main">

<!-- ══════════════════ OVERVIEW ══════════════════ -->
<div id="ov" class="page active">
  <div class="banner">
    <strong data-i18n="banner_edit_title">البيانات قابلة للتعديل</strong>
    <span data-i18n="banner_edit_desc"> — سجّل دخولك كمسؤول وعدّل الأرقام لتتحدث جميع الرسوم والمؤشرات فوراً، والرابط يحتفظ بالبيانات للمشاركة</span>
  </div>

  <!-- 5 Merged KPI -->
  <div class="kpi5" id="kpi-area"></div>

  <!-- Evac Banner -->
  <div class="evac-banner">
    <div>
      <div class="evac-title" data-i18n="evac_title">حالات الإخلاء الطبي</div>
      <div class="evac-sub" data-i18n="evac_sub">إجمالي حالات الإخلاء الطبي الموثقة خلال العام</div>
    </div>
    <div style="text-align:center">
      <div class="evac-num" id="evac_big">0</div>
      <div class="evac-lbl" data-i18n="evac_lbl">إجمالي الإخلاء</div>
    </div>
    <div class="cw" style="height:70px;width:280px;max-width:100%"><canvas id="evac_spark"></canvas></div>
  </div>

  <!-- Charts Row 1 -->
  <div class="g2">
    <div class="card">
      <div class="ch"><div><div class="ct" data-i18n="ch_monthly_cases">الأداء الشهري — الحالات الطارئة</div><div class="cs" data-i18n="ch_monthly_cases_sub">منقولة وغير منقولة لعام 2026</div></div></div>
      <div class="leg">
        <span><span class="lsq" style="background:#0084BD"></span><span data-i18n="leg_trans">منقولة</span></span>
        <span><span class="lsq" style="background:#ef4444"></span><span data-i18n="leg_nontrans">غير منقولة</span></span>
      </div>
      <div class="cw" style="height:230px"><canvas id="c1"></canvas></div>
    </div>
    <div class="card">
      <div class="ch"><div><div class="ct" data-i18n="ch_transport_dist">توزيع النقل الطبي</div><div class="cs" data-i18n="ch_transport_dist_sub">داخلي مقابل خارجي</div></div></div>
      <div class="cw" style="height:230px"><canvas id="c2"></canvas></div>
    </div>
  </div>

  <!-- Charts Row 2 -->
  <div class="g2b">
    <div class="card">
      <div class="ch"><div><div class="ct" data-i18n="ch_transport_monthly">النقل الطبي — شهري</div></div></div>
      <div class="leg">
        <span><span class="lsq" style="background:#16a34a"></span><span data-i18n="leg_internal">داخلي</span></span>
        <span><span class="lsq" style="background:#ea580c"></span><span data-i18n="leg_external">خارجي</span></span>
      </div>
      <div class="cw" style="height:185px"><canvas id="c3"></canvas></div>
    </div>
    <div class="card">
      <div class="ch"><div><div class="ct" data-i18n="ch_participation">المشاركات الطبية — شهري</div></div></div>
      <div class="leg">
        <span><span class="lsq" style="background:#7c3aed"></span><span data-i18n="leg_partin">داخلية</span></span>
        <span><span class="lsq" style="background:#748995"></span><span data-i18n="leg_partout">خارجية</span></span>
      </div>
      <div class="cw" style="height:185px"><canvas id="c4"></canvas></div>
    </div>
  </div>

  <!-- Training -->
  <div class="card" style="margin-bottom:12px">
    <div class="ch"><div><div class="ct" data-i18n="ch_training">البرامج التدريبية — المنحنى السنوي</div></div></div>
    <div class="leg">
      <span><span class="lsq" style="background:#d97706"></span><span data-i18n="leg_field">طلاب الكليات (ميداني)</span></span>
      <span><span class="lsq" style="background:#059669"></span><span data-i18n="leg_resident">طلاب الامتياز والمقيمين</span></span>
    </div>
    <div class="cw" style="height:185px"><canvas id="c_train"></canvas></div>
  </div>

  <!-- Summary Table -->
  <div class="card">
    <div class="ch"><div><div class="ct" data-i18n="ch_annual_summary">الملخص السنوي الشامل</div></div></div>
    <div class="tw"><table><thead><tr id="stb-head"></tr></thead><tbody id="stb"></tbody></table></div>
  </div>
</div>

<!-- ══════════════════ MONTHLY PAGE ══════════════════ -->
<div id="monthly" class="page">
  <div class="sec"><span class="sec-text" data-i18n="nav_monthly">عرض شهري</span></div>
  <!-- Month tabs built by JS -->
  <div class="qtabs" id="month-tabs"></div>
  <div id="month-content"></div>
</div>

<!-- ══════════════════ QUARTERLY PAGE ══════════════════ -->
<div id="quarterly" class="page">
  <div class="sec"><span class="sec-text" data-i18n="nav_quarterly">عرض ربعي</span></div>
  <div class="qtabs" id="q-tabs">
    <button class="qtab active" onclick="showQ(1,this)" data-i18n="q1">الربع الأول</button>
    <button class="qtab" onclick="showQ(2,this)" data-i18n="q2">الربع الثاني</button>
    <button class="qtab" onclick="showQ(3,this)" data-i18n="q3">الربع الثالث</button>
    <button class="qtab" onclick="showQ(4,this)" data-i18n="q4">الربع الرابع</button>
  </div>
  <div id="q-content"></div>
</div>

<!-- ══════════════════ COMPARE ══════════════════ -->
<div id="cmp" class="page">
  <div class="sec"><span class="sec-text" data-i18n="nav_compare">التحليل المقارن</span></div>
  <div class="g2b">
    <div class="card"><div class="ct" style="margin-bottom:10px" data-i18n="cc_cases">مقارنة الحالات الطارئة شهرياً</div><div class="cw" style="height:215px"><canvas id="cc1"></canvas></div></div>
    <div class="card"><div class="ct" style="margin-bottom:10px" data-i18n="cc_transport">مقارنة النقل الطبي شهرياً</div><div class="cw" style="height:215px"><canvas id="cc2"></canvas></div></div>
  </div>
  <div class="g2b">
    <div class="card"><div class="ct" style="margin-bottom:10px" data-i18n="cc_part">منحنى المشاركات السنوي</div><div class="cw" style="height:195px"><canvas id="cc3"></canvas></div></div>
    <div class="card"><div class="ct" style="margin-bottom:10px" data-i18n="cc_evac">منحنى الإخلاء الطبي</div><div class="cw" style="height:195px"><canvas id="cc4"></canvas></div></div>
  </div>
  <div class="card" style="margin-bottom:12px"><div class="ct" style="margin-bottom:10px" data-i18n="cc_train">منحنى البرامج التدريبية</div>
    <div class="cw" style="height:195px"><canvas id="cc5"></canvas></div></div>
  <div class="g3">
    <div class="card"><div class="ct" style="margin-bottom:12px" data-i18n="rank_cases">ترتيب الأشهر — الحالات الطارئة</div><div id="rank_crit"></div></div>
    <div class="card"><div class="ct" style="margin-bottom:12px" data-i18n="rank_transport">ترتيب الأشهر — النقل الطبي</div><div id="rank_tr"></div></div>
    <div class="card"><div class="ct" style="margin-bottom:12px" data-i18n="rank_evac">ترتيب الأشهر — الإخلاء</div><div id="rank_evac"></div></div>
  </div>
</div>

<!-- ══════════════════ DATA ══════════════════ -->
<div id="dtl" class="page">
  <div class="sec"><span class="sec-text" data-i18n="nav_data">البيانات التفصيلية الكاملة</span></div>
  <div class="card" style="margin-bottom:12px">
    <div class="ch"><div><div class="ct" data-i18n="dtl_table">جدول الأداء الشهري الكامل</div></div></div>
    <div class="tw"><table><thead><tr id="dtb-head"></tr></thead><tbody id="dtb"></tbody></table></div>
  </div>
  <div class="card">
    <div class="ct" style="margin-bottom:12px" data-i18n="export_title">تصدير البيانات</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap">
      <button class="btnprim" onclick="exportCSV()"><svg viewBox="0 0 24 24"><path d="M5 20h14v-2H5v2zm0-10h4v6h6v-6h4l-7-7-7 7z"/></svg><span data-i18n="export_csv">تنزيل CSV</span></button>
      <button class="btnprim" style="background:#005f8a" onclick="copyTbl()"><svg viewBox="0 0 24 24"><path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/></svg><span data-i18n="copy_excel">نسخ لـ Excel</span></button>
      <button class="btnprim" style="background:#748995" onclick="openShare()"><svg viewBox="0 0 24 24"><path d="M18 16.08c-.76 0-1.44.3-1.96.77L8.91 12.7c.05-.23.09-.46.09-.7s-.04-.47-.09-.7l7.05-4.11A2.99 2.99 0 0018 8a3 3 0 000-6 3 3 0 00-3 3c0 .24.04.47.09.7L8.04 9.81A2.99 2.99 0 006 9a3 3 0 000 6c.79 0 1.5-.31 2.04-.81l7.12 4.16c-.05.21-.08.43-.08.65a2.92 2.92 0 102.92-2.92z"/></svg><span data-i18n="share">مشاركة الرابط</span></button>
    </div>
  </div>
</div>

</div><!-- /main -->

<div class="footer" data-i18n="footer">المدينة الطبية الجامعية — جامعة الملك سعود · Riyadh, KSA · KSUMC Dashboard 2026 | جميع البيانات سرية للاستخدام الداخلي</div>
<div class="stripe"></div>

<!-- ═══════════ EDITOR MODAL ═══════════ -->
<div class="modal-ov" id="emod">
  <div class="modal">
    <div class="mt-h" data-i18n="edit_title">تعديل البيانات الشهرية</div>
    <div class="mt-s" data-i18n="edit_desc">أدخل بيانات كل شهر — ستتحدث جميع الرسوم والمؤشرات تلقائياً</div>
    <div id="editor-body"></div>
    <div class="macts">
      <button class="btncanc btnprim" style="background:#748995" onclick="closeEd()" data-i18n="cancel">إلغاء</button>
      <button class="btnprim" onclick="applyData()" data-i18n="apply">✅ تطبيق وتحديث اللوحة</button>
    </div>
  </div>
</div>

<!-- ═══════════ SHARE MODAL ═══════════ -->
<div class="modal-ov" id="smod">
  <div class="modal-sm">
    <div class="mt-h" data-i18n="share_title">مشاركة لوحة التحكم</div>
    <div class="mt-s" data-i18n="share_desc">الرابط يحتوي على البيانات — شاركه وسيرون نفس الأرقام</div>
    <div class="surl">
      <input type="text" id="surl_inp" readonly>
      <button class="scpy" onclick="cpyURL()" data-i18n="copy">نسخ</button>
    </div>
    <div class="smeth">
      <button class="sbtn" onclick="wa()">
        <svg viewBox="0 0 24 24" style="fill:#25d366"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
        <span data-i18n="whatsapp">واتساب</span>
      </button>
      <button class="sbtn" onclick="em()">
        <svg viewBox="0 0 24 24" style="fill:#0084BD"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
        <span data-i18n="email">بريد</span>
      </button>
      <button class="sbtn" onclick="window.print()">
        <svg viewBox="0 0 24 24" style="fill:#748995"><path d="M19 8H5c-1.66 0-3 1.34-3 3v6h4v4h12v-4h4v-6c0-1.66-1.34-3-3-3zm-3 11H8v-5h8v5zm3-7c-.55 0-1-.45-1-1s.45-1 1-1 1 .45 1 1-.45 1-1 1zm-1-9H6v4h12V3z"/></svg>
        <span data-i18n="print">طباعة</span>
      </button>
    </div>
    <div style="margin-top:14px;text-align:center"><button class="btncanc btnprim" style="background:#748995" onclick="closeShare()" data-i18n="close">إغلاق</button></div>
  </div>
</div>

<div class="toast" id="toast">✅</div>

<script>
/* ═══════════════════════════════════════════════════════
   TRANSLATIONS
═══════════════════════════════════════════════════════ */
const T = {
ar:{
  hosp_name:"المدينة الطبية الجامعية", hosp_sub:"جامعة الملك سعود · الرياض",
  report_year:"التقرير السنوي", admin_login:"دخول المسؤول", admin_out:"خروج المسؤول",
  edit_data:"تعديل البيانات", share:"مشاركة", print:"طباعة",
  nav_overview:"نظرة عامة", nav_monthly:"شهري", nav_quarterly:"ربعي",
  nav_compare:"التحليل المقارن", nav_data:"البيانات الكاملة",
  banner_edit_title:"البيانات قابلة للتعديل",
  banner_edit_desc:" — سجّل دخولك كمسؤول وعدّل الأرقام لتتحدث جميع الرسوم فوراً، والرابط يحتفظ بالبيانات",
  evac_title:"حالات الإخلاء الطبي", evac_sub:"إجمالي الحالات الموثقة خلال العام", evac_lbl:"إجمالي الإخلاء",
  ch_monthly_cases:"الأداء الشهري — الحالات الطارئة", ch_monthly_cases_sub:"منقولة وغير منقولة",
  ch_transport_dist:"توزيع النقل الطبي", ch_transport_dist_sub:"داخلي مقابل خارجي",
  ch_transport_monthly:"النقل الطبي — شهري", ch_participation:"المشاركات الطبية — شهري",
  ch_training:"البرامج التدريبية — المنحنى السنوي", ch_annual_summary:"الملخص السنوي الشامل",
  leg_trans:"منقولة", leg_nontrans:"غير منقولة", leg_internal:"داخلي", leg_external:"خارجي",
  leg_partin:"داخلية", leg_partout:"خارجية", leg_field:"ميداني", leg_resident:"امتياز/مقيم",
  q1:"الربع الأول", q2:"الربع الثاني", q3:"الربع الثالث", q4:"الربع الرابع",
  cc_cases:"مقارنة الحالات الطارئة شهرياً", cc_transport:"مقارنة النقل الطبي شهرياً",
  cc_part:"منحنى المشاركات السنوي", cc_evac:"منحنى الإخلاء الطبي", cc_train:"منحنى البرامج التدريبية",
  rank_cases:"ترتيب الأشهر — الحالات الطارئة", rank_transport:"ترتيب الأشهر — النقل الطبي", rank_evac:"ترتيب الأشهر — الإخلاء",
  dtl_table:"جدول الأداء الشهري الكامل", export_title:"تصدير البيانات",
  export_csv:"تنزيل CSV", copy_excel:"نسخ لـ Excel",
  edit_title:"تعديل البيانات الشهرية", edit_desc:"أدخل البيانات لكل شهر — ستتحدث كل الرسوم تلقائياً",
  cancel:"إلغاء", apply:"تطبيق", close:"إغلاق",
  share_title:"مشاركة لوحة التحكم", share_desc:"الرابط يحتوي على البيانات — شاركه وسيرون نفس الأرقام",
  copy:"نسخ", whatsapp:"واتساب", email:"بريد",
  footer:"المدينة الطبية الجامعية — جامعة الملك سعود · Riyadh, KSA · KSUMC Dashboard | جميع البيانات سرية للاستخدام الداخلي",
  toast_updated:"تم تحديث اللوحة بنجاح", toast_copied:"تم النسخ!", toast_url:"تم نسخ الرابط",
  toast_admin_in:"تم الدخول كمسؤول", toast_admin_out:"تم تسجيل الخروج", toast_wrong_pass:"كلمة المرور غير صحيحة",
  toast_need_admin:"يجب تسجيل الدخول كمسؤول أولاً",
  kpi_cases:"إجمالي الحالات الطارئة", kpi_trans:"منقولة", kpi_nontrans:"غير منقولة",
  kpi_transport:"إجمالي النقل الطبي", kpi_internal:"داخلي", kpi_external:"خارجي",
  kpi_part:"إجمالي المشاركات", kpi_partin:"داخلية", kpi_partout:"خارجية",
  kpi_evac:"حالات الإخلاء الطبي", kpi_train:"البرامج التدريبية", kpi_field:"ميداني", kpi_res:"امتياز/مقيم",
  th_month:"الشهر", th_trans:"طارئة منقولة", th_nontrans:"طارئة غير منقولة", th_crit:"إجمالي طارئة",
  th_trin:"نقل داخلي", th_trout:"نقل خارجي", th_tr:"إجمالي نقل",
  th_partin:"مشاركة داخلية", th_partout:"مشاركة خارجية", th_part:"إجمالي مشاركات",
  th_evac:"إخلاء طبي", th_field:"تدريب ميداني", th_res:"امتياز/مقيم", th_total:"الإجمالي",
  ed_trans:"الحالات الطارئة المنقولة", ed_nontrans:"الحالات الطارئة غير المنقولة",
  ed_trin:"النقل الطبي الداخلي", ed_trout:"النقل الطبي الخارجي",
  ed_partin:"المشاركات الداخلية", ed_partout:"المشاركات الخارجية",
  ed_evac:"حالات الإخلاء الطبي", ed_field:"التدريب الميداني", ed_res:"الامتياز والمقيمين",
  months:['يناير','فبراير','مارس','أبريل','مايو','يونيو','يوليو','أغسطس','سبتمبر','أكتوبر','نوفمبر','ديسمبر'],
  quarters:['الربع الأول','الربع الثاني','الربع الثالث','الربع الرابع'],
  q_insight:[
    "أطلق الربع الأول شرارة نشاط مؤسسي واعد؛ نمو تدريجي مطّرد من يناير حتى مارس يؤكد متانة البنية التشغيلية لمستشفيات المدينة الطبية الجامعية.",
    "شهد الربع الثاني تذبذباً لافتاً مع أعلى قمة شهرية في أبريل، يعكس إعادة توزيع الطاقات وتكيّف منظومة العمل مع التحديات الموسمية.",
    "انطلق النصف الثاني بثقة مدروسة؛ أغسطس قدّم قمة موسمية صيفية تكشف عن نمط فصلي منتظم يستدعي تعزيز الكوادر في هذا الشهر من كل عام.",
    "الربع الرابع — الأقوى أداءً طوال العام — يُبشّر بمنطلق قوي للعام القادم، مؤكداً الريادة الطبية الأكاديمية للمدينة الطبية الجامعية بجامعة الملك سعود."
  ]
},
en:{
  hosp_name:"University Medical City", hosp_sub:"King Saud University · Riyadh",
  report_year:"Annual Report", admin_login:"Admin Login", admin_out:"Admin Logout",
  edit_data:"Edit Data", share:"Share", print:"Print",
  nav_overview:"Overview", nav_monthly:"Monthly", nav_quarterly:"Quarterly",
  nav_compare:"Comparative Analysis", nav_data:"Full Data",
  banner_edit_title:"Data is editable",
  banner_edit_desc:" — Log in as admin to edit figures and all charts update instantly. The URL stores your data for sharing.",
  evac_title:"Medical Evacuation Cases", evac_sub:"Total documented evacuation cases", evac_lbl:"Total Evacuations",
  ch_monthly_cases:"Monthly Performance — Emergency Cases", ch_monthly_cases_sub:"Transported vs Non-Transported",
  ch_transport_dist:"Medical Transport Distribution", ch_transport_dist_sub:"Internal vs External",
  ch_transport_monthly:"Medical Transport — Monthly", ch_participation:"Medical Participation — Monthly",
  ch_training:"Training Programs — Annual Trend", ch_annual_summary:"Comprehensive Annual Summary",
  leg_trans:"Transported", leg_nontrans:"Non-Transported", leg_internal:"Internal", leg_external:"External",
  leg_partin:"Internal", leg_partout:"External", leg_field:"Field Training", leg_resident:"Intern/Resident",
  q1:"Q1", q2:"Q2", q3:"Q3", q4:"Q4",
  cc_cases:"Emergency Cases — Monthly Comparison", cc_transport:"Medical Transport — Monthly Comparison",
  cc_part:"Participation — Annual Trend", cc_evac:"Medical Evacuation — Annual Trend", cc_train:"Training Programs — Annual Trend",
  rank_cases:"Months Ranked — Emergency Cases", rank_transport:"Months Ranked — Medical Transport", rank_evac:"Months Ranked — Evacuation",
  dtl_table:"Full Monthly Performance Table", export_title:"Export Data",
  export_csv:"Download CSV", copy_excel:"Copy for Excel",
  edit_title:"Edit Monthly Data", edit_desc:"Enter values for each month — all charts and KPIs update instantly",
  cancel:"Cancel", apply:"Apply", close:"Close",
  share_title:"Share Dashboard", share_desc:"The URL includes your data — share it and recipients see the same figures",
  copy:"Copy", whatsapp:"WhatsApp", email:"Email",
  footer:"University Medical City — King Saud University · Riyadh, KSA · KSUMC Dashboard | Confidential — Internal Use Only",
  toast_updated:"Dashboard updated successfully", toast_copied:"Copied!", toast_url:"URL copied",
  toast_admin_in:"Logged in as admin", toast_admin_out:"Logged out", toast_wrong_pass:"Incorrect password",
  toast_need_admin:"Admin login required",
  kpi_cases:"Total Emergency Cases", kpi_trans:"Transported", kpi_nontrans:"Non-Transported",
  kpi_transport:"Total Medical Transport", kpi_internal:"Internal", kpi_external:"External",
  kpi_part:"Total Participation", kpi_partin:"Internal", kpi_partout:"External",
  kpi_evac:"Medical Evacuation", kpi_train:"Training Programs", kpi_field:"Field Training", kpi_res:"Intern/Resident",
  th_month:"Month", th_trans:"Transported", th_nontrans:"Non-Transported", th_crit:"Total Emergency",
  th_trin:"Int. Transport", th_trout:"Ext. Transport", th_tr:"Total Transport",
  th_partin:"Int. Participation", th_partout:"Ext. Participation", th_part:"Total Participation",
  th_evac:"Evacuation", th_field:"Field Training", th_res:"Intern/Res.", th_total:"Total",
  ed_trans:"Transported Emergency Cases", ed_nontrans:"Non-Transported Emergency Cases",
  ed_trin:"Internal Medical Transport", ed_trout:"External Medical Transport",
  ed_partin:"Internal Participation", ed_partout:"External Participation",
  ed_evac:"Medical Evacuation Cases", ed_field:"Field Training Students", ed_res:"Interns & Residents",
  months:['January','February','March','April','May','June','July','August','September','October','November','December'],
  quarters:['Q1','Q2','Q3','Q4'],
  q_insight:[
    "Q1 set a strong foundation with steady growth from January through March, demonstrating the operational resilience of KSUMC's hospital network.",
    "Q2 showed notable variation, with April peaking as the highest single month of H1, reflecting dynamic demand distribution across the university medical complex.",
    "H2 launched with measured confidence; August emerged as a summer seasonal peak, revealing a recurring pattern that warrants proactive staffing reinforcement.",
    "Q4 — the strongest quarter of the year — signals strong momentum heading into the next year, affirming KSUMC's position as a leading academic medical institution."
  ]
}};

/* ═══════════════════════════════════════════════════════
   DATA & STATE
═══════════════════════════════════════════════════════ */
let LANG = localStorage.getItem('ksulang') || 'ar';
let YEAR = '2026';
const ADMIN_PASS = 'KSUMC2026';
const ALL_KEYS = ['trans','nontrans','trin','trout','partin','partout','evac','trainstud','trainres'];

let DATA = {
  trans:     [50,66,77,90,70,40,60,80,55,50,67,90],
  nontrans:  [20,30,25,35,28,18,22,40,30,25,35,45],
  trin:      [30,40,35,50,42,25,38,55,40,35,48,60],
  trout:     [15,20,18,25,20,12,18,28,20,18,22,30],
  partin:    [10,15,12,18,14,8,12,20,14,12,16,22],
  partout:   [8,10,9,12,10,6,9,14,10,9,12,16],
  evac:      [5,8,6,11,9,4,7,13,8,6,10,14],
  trainstud: [12,18,15,22,20,10,14,25,18,15,20,28],
  trainres:  [8,12,10,15,13,7,10,17,12,10,14,19],
};

function t(k){ return (T[LANG]||T.ar)[k]||k; }
function MN(){ return t('months'); }
function isAdmin(){ return sessionStorage.getItem('admin')==='true'; }
function sum(a){ return a.reduce((x,y)=>x+y,0); }

/* ═══════════════════════════════════════════════════════
   LANG & YEAR
═══════════════════════════════════════════════════════ */
function setLang(lang){
  LANG=lang;
  localStorage.setItem('ksulang',lang);
  document.getElementById('root').lang=lang;
  document.getElementById('root').dir=lang==='ar'?'rtl':'ltr';
  document.getElementById('langSel').value=lang;
  document.querySelectorAll('[data-i18n]').forEach(el=>{
    const k=el.getAttribute('data-i18n');
    if(t(k)!==k) el.textContent=t(k);
  });
  renderAll();
}

function setYear(y){ YEAR=y; document.getElementById('yr-display').textContent=y; }

/* ═══════════════════════════════════════════════════════
   HASH / STORAGE
═══════════════════════════════════════════════════════ */
function saveHash(){
  try{ history.replaceState(null,'','#'+btoa(JSON.stringify({data:DATA,lang:LANG,year:YEAR}))); }catch(e){}
}
function loadHash(){
  try{
    const h=location.hash.slice(1);
    if(!h)return;
    const obj=JSON.parse(atob(h));
    if(obj.data) ALL_KEYS.forEach(k=>{ if(Array.isArray(obj.data[k])&&obj.data[k].length===12) DATA[k]=obj.data[k]; });
    if(obj.lang) LANG=obj.lang;
    if(obj.year) YEAR=obj.year;
  }catch(e){}
}

/* ═══════════════════════════════════════════════════════
   ADMIN
═══════════════════════════════════════════════════════ */
function adminLogin(){
  if(isAdmin()){
    if(confirm(LANG==='ar'?'هل تريد تسجيل الخروج؟':'Log out?')){
      sessionStorage.removeItem('admin');
      document.getElementById('editBtn').style.display='none';
      document.getElementById('loginBtn').querySelector('[data-i18n]').setAttribute('data-i18n','admin_login');
      document.getElementById('loginBtn').querySelector('[data-i18n]').textContent=t('admin_login');
      document.getElementById('loginBtn').classList.remove('active');
      toast(t('toast_admin_out'));
    }
    return;
  }
  const p=prompt(LANG==='ar'?'أدخل كلمة مرور المسؤول:':'Enter admin password:');
  if(p===ADMIN_PASS){
    sessionStorage.setItem('admin','true');
    document.getElementById('editBtn').style.display='inline-flex';
    document.getElementById('loginBtn').querySelector('[data-i18n]').textContent=t('admin_out');
    document.getElementById('loginBtn').classList.add('active');
    toast(t('toast_admin_in'));
  } else if(p!==null){ toast(t('toast_wrong_pass')); }
}

/* ═══════════════════════════════════════════════════════
   CHARTS ENGINE
═══════════════════════════════════════════════════════ */
const CHS={};
function dc(id){ if(CHS[id]){CHS[id].destroy();delete CHS[id];} }
function mk(id,cfg){
  dc(id);
  const el=document.getElementById(id);
  if(!el)return null;
  return CHS[id]=new Chart(el,cfg);
}

const BASE={
  responsive:true,maintainAspectRatio:false,
  plugins:{legend:{display:false}},
  scales:{
    x:{grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:10},color:'#748995',maxRotation:45}},
    y:{grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:10},color:'#748995'},beginAtZero:true}
  }
};
function noScale(){ return {responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{enabled:false}},scales:{x:{display:false},y:{display:false,beginAtZero:true}}}; }
function doughnutOpts(pos){ return {responsive:true,maintainAspectRatio:false,cutout:'58%',plugins:{legend:{display:true,position:pos||'bottom',labels:{font:{size:10},boxWidth:11,padding:7}}}}; }

/* ═══════════════════════════════════════════════════════
   RENDER ALL
═══════════════════════════════════════════════════════ */
function renderAll(){
  const d=DATA, mn=MN();
  const totTrans=sum(d.trans), totNt=sum(d.nontrans);
  const totTrin=sum(d.trin), totTrout=sum(d.trout);
  const totPin=sum(d.partin), totPout=sum(d.partout);
  const totEvac=sum(d.evac);
  const totStud=sum(d.trainstud), totRes=sum(d.trainres);

  // KPI area
  document.getElementById('kpi-area').innerHTML=`
    <div class="kpi" style="--c:#0084BD;--c1:#005f8a;--c2:#3BAAD4">
      <div class="kpi-lbl">${t('kpi_cases')}</div>
      <div class="kpi-val">${(totTrans+totNt).toLocaleString()}</div>
      <div class="kpi-row">
        <span class="kpi-bp" style="background:#e6f4fb;color:#005f8a"><span class="kpi-dot" style="background:#0084BD"></span>${t('kpi_trans')}: <b>${totTrans}</b></span>
        <span class="kpi-bp" style="background:#fee2e2;color:#b91c1c"><span class="kpi-dot" style="background:#ef4444"></span>${t('kpi_nontrans')}: <b>${totNt}</b></span>
      </div>
    </div>
    <div class="kpi" style="--c:#16a34a;--c1:#15803d;--c2:#22c55e">
      <div class="kpi-lbl">${t('kpi_transport')}</div>
      <div class="kpi-val">${(totTrin+totTrout).toLocaleString()}</div>
      <div class="kpi-row">
        <span class="kpi-bp" style="background:#dcfce7;color:#15803d"><span class="kpi-dot" style="background:#16a34a"></span>${t('kpi_internal')}: <b>${totTrin}</b></span>
        <span class="kpi-bp" style="background:#ffedd5;color:#c2410c"><span class="kpi-dot" style="background:#ea580c"></span>${t('kpi_external')}: <b>${totTrout}</b></span>
      </div>
    </div>
    <div class="kpi" style="--c:#7c3aed;--c1:#6d28d9;--c2:#a78bfa">
      <div class="kpi-lbl">${t('kpi_part')}</div>
      <div class="kpi-val">${(totPin+totPout).toLocaleString()}</div>
      <div class="kpi-row">
        <span class="kpi-bp" style="background:#ede9fe;color:#6d28d9"><span class="kpi-dot" style="background:#7c3aed"></span>${t('kpi_partin')}: <b>${totPin}</b></span>
        <span class="kpi-bp" style="background:#f1f5f9;color:#475569"><span class="kpi-dot" style="background:#748995"></span>${t('kpi_partout')}: <b>${totPout}</b></span>
      </div>
    </div>
    <div class="kpi" style="--c:#0d9488;--c1:#0f766e;--c2:#2dd4bf">
      <div class="kpi-lbl">${t('kpi_evac')}</div>
      <div class="kpi-val">${totEvac.toLocaleString()}</div>
      <div class="kpi-row">
        <span class="kpi-bp" style="background:#ccfbf1;color:#0f766e"><span class="kpi-dot" style="background:#0d9488"></span>${t('evac_lbl')}</span>
      </div>
    </div>
    <div class="kpi" style="--c:#d97706;--c1:#92400e;--c2:#f59e0b">
      <div class="kpi-lbl">${t('kpi_train')}</div>
      <div class="kpi-val">${(totStud+totRes).toLocaleString()}</div>
      <div class="kpi-row">
        <span class="kpi-bp" style="background:#fef3c7;color:#92400e"><span class="kpi-dot" style="background:#d97706"></span>${t('kpi_field')}: <b>${totStud}</b></span>
        <span class="kpi-bp" style="background:#d1fae5;color:#065f46"><span class="kpi-dot" style="background:#059669"></span>${t('kpi_res')}: <b>${totRes}</b></span>
      </div>
    </div>
  `;

  document.getElementById('evac_big').textContent=totEvac.toLocaleString();

  // Overview charts
  mk('c1',{type:'bar',data:{labels:mn,datasets:[
    {label:t('leg_trans'),data:d.trans,backgroundColor:'#0084BD',borderRadius:4,borderSkipped:false},
    {label:t('leg_nontrans'),data:d.nontrans,backgroundColor:'#ef4444',borderRadius:4,borderSkipped:false}
  ]},options:{...BASE}});
  mk('c2',{type:'doughnut',data:{labels:[t('leg_internal'),t('leg_external')],datasets:[{data:[totTrin,totTrout],backgroundColor:['#16a34a','#ea580c'],borderWidth:3,borderColor:'#fff',hoverOffset:6}]},options:doughnutOpts()});
  mk('c3',{type:'bar',data:{labels:mn,datasets:[
    {label:t('leg_internal'),data:d.trin,backgroundColor:'#16a34a',borderRadius:4},
    {label:t('leg_external'),data:d.trout,backgroundColor:'#ea580c',borderRadius:4}
  ]},options:{...BASE}});
  mk('c4',{type:'bar',data:{labels:mn,datasets:[
    {label:t('leg_partin'),data:d.partin,backgroundColor:'#7c3aed',borderRadius:4},
    {label:t('leg_partout'),data:d.partout,backgroundColor:'#748995',borderRadius:4}
  ]},options:{...BASE}});
  mk('c_train',{type:'line',data:{labels:mn,datasets:[
    {label:t('leg_field'),data:d.trainstud,borderColor:'#d97706',backgroundColor:'rgba(217,119,6,.12)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#d97706',pointBorderWidth:2,borderWidth:2.5},
    {label:t('leg_resident'),data:d.trainres,borderColor:'#059669',backgroundColor:'rgba(5,150,105,.1)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#059669',pointBorderWidth:2,borderWidth:2.5}
  ]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:11,padding:8}}}}});
  mk('evac_spark',{type:'bar',data:{labels:mn,datasets:[{data:d.evac,backgroundColor:'rgba(255,255,255,0.5)',borderRadius:3,borderSkipped:false}]},options:noScale()});

  renderSummaryTable(d,mn);
  renderMonthPage(0);
  renderMonthTabs(mn);
  showQ(1,null);
  renderCompare(d,mn);
  renderDetailTable(d,mn);
  saveHash();
}

/* ═══════════════════════════════════════════════════════
   SUMMARY TABLE
═══════════════════════════════════════════════════════ */
function renderSummaryTable(d,mn){
  const hd=document.getElementById('stb-head');
  if(hd) hd.innerHTML=`<th>${t('th_month')}</th><th>${t('th_trans')}</th><th>${t('th_nontrans')}</th><th>${t('th_crit')}</th><th>${t('th_trin')}</th><th>${t('th_trout')}</th><th>${t('th_tr')}</th><th>${t('th_partin')}</th><th>${t('th_partout')}</th><th>${t('th_part')}</th><th style="background:#0f766e">${t('th_evac')}</th><th style="background:#b45309">${t('th_field')}</th><th style="background:#065f46">${t('th_res')}</th>`;
  const sb=document.getElementById('stb');
  if(!sb)return;
  let tot={tr:0,nt:0,trin:0,trout:0,pin:0,pout:0,ev:0,stud:0,res:0};
  let html='';
  for(let i=0;i<12;i++){
    const crit=d.trans[i]+d.nontrans[i], tr=d.trin[i]+d.trout[i], part=d.partin[i]+d.partout[i];
    tot.tr+=d.trans[i];tot.nt+=d.nontrans[i];tot.trin+=d.trin[i];tot.trout+=d.trout[i];
    tot.pin+=d.partin[i];tot.pout+=d.partout[i];tot.ev+=d.evac[i];tot.stud+=d.trainstud[i];tot.res+=d.trainres[i];
    html+=`<tr><td><b>${mn[i]}</b></td><td style="color:#0084BD;font-weight:700">${d.trans[i]}</td><td style="color:#ef4444;font-weight:700">${d.nontrans[i]}</td><td><b>${crit}</b></td><td style="color:#16a34a;font-weight:700">${d.trin[i]}</td><td style="color:#ea580c;font-weight:700">${d.trout[i]}</td><td><b>${tr}</b></td><td style="color:#7c3aed;font-weight:700">${d.partin[i]}</td><td style="color:#748995;font-weight:700">${d.partout[i]}</td><td><b>${part}</b></td><td style="color:#0d9488;font-weight:800;background:#f0fdfa">${d.evac[i]}</td><td style="color:#b45309;font-weight:800;background:#fef9ee">${d.trainstud[i]}</td><td style="color:#065f46;font-weight:800;background:#f0fdf4">${d.trainres[i]}</td></tr>`;
  }
  const cTot=tot.tr+tot.nt, tTot=tot.trin+tot.trout, pTot=tot.pin+tot.pout;
  html+=`<tr style="background:#0084BD"><td style="color:#fff;font-weight:800">${t('th_total')}</td><td style="color:#fff;font-weight:800">${tot.tr}</td><td style="color:#fff;font-weight:800">${tot.nt}</td><td style="color:#fff;font-weight:800">${cTot}</td><td style="color:#fff;font-weight:800">${tot.trin}</td><td style="color:#fff;font-weight:800">${tot.trout}</td><td style="color:#fff;font-weight:800">${tTot}</td><td style="color:#fff;font-weight:800">${tot.pin}</td><td style="color:#fff;font-weight:800">${tot.pout}</td><td style="color:#fff;font-weight:800">${pTot}</td><td style="color:#fff;font-weight:800;background:#0f766e">${tot.ev}</td><td style="color:#fff;font-weight:800;background:#b45309">${tot.stud}</td><td style="color:#fff;font-weight:800;background:#065f46">${tot.res}</td></tr>`;
  sb.innerHTML=html;
}

/* ═══════════════════════════════════════════════════════
   MONTH PAGE
═══════════════════════════════════════════════════════ */
function renderMonthTabs(mn){
  const tabs=document.getElementById('month-tabs');
  if(!tabs)return;
  tabs.innerHTML=mn.map((m,i)=>`<button class="qtab${i===0?' active':''}" onclick="renderMonthPage(${i},this)">${m}</button>`).join('');
}

function renderMonthPage(idx,btnEl){
  const mn=MN();
  if(btnEl){
    document.querySelectorAll('#month-tabs .qtab').forEach(b=>b.classList.remove('active'));
    btnEl.classList.add('active');
  }
  const d=DATA;
  const i=idx;
  const crit=d.trans[i]+d.nontrans[i];
  const tr=d.trin[i]+d.trout[i];
  const part=d.partin[i]+d.partout[i];
  const allMax=Math.max(d.trans[i],d.nontrans[i],d.trin[i],d.trout[i],d.partin[i],d.partout[i],d.evac[i],d.trainstud[i],d.trainres[i])||1;
  const qn=t('quarters')[Math.floor(i/3)];

  document.getElementById('month-content').innerHTML=`
    <div class="mhero mg${i}">
      <div class="mht">
        <div><div class="mht-title">${mn[i]} ${YEAR}</div><div class="mht-sub">${qn} — ${t('nav_monthly')}</div></div>
        <div class="mtot"><div class="mtot-n">${crit}</div><div class="mtot-l">${t('kpi_cases')}</div></div>
      </div>
      <div class="mmetrics">
        <div class="mmc"><div class="mmn">${t('leg_trans')}</div><div class="mmv">${d.trans[i]}</div></div>
        <div class="mmc"><div class="mmn">${t('leg_nontrans')}</div><div class="mmv">${d.nontrans[i]}</div></div>
        <div class="mmc"><div class="mmn">${t('leg_internal')}</div><div class="mmv">${d.trin[i]}</div></div>
        <div class="mmc"><div class="mmn">${t('leg_external')}</div><div class="mmv">${d.trout[i]}</div></div>
        <div class="mmc"><div class="mmn">${t('leg_partin')}</div><div class="mmv">${d.partin[i]}</div></div>
        <div class="mmc"><div class="mmn">${t('leg_partout')}</div><div class="mmv">${d.partout[i]}</div></div>
        <div class="mmc" style="border:1.5px solid rgba(255,255,255,.5);background:rgba(255,255,255,.25)"><div class="mmn">${t('th_evac')}</div><div class="mmv">${d.evac[i]}</div></div>
        <div class="mmc" style="border:1.5px solid rgba(217,119,6,.6);background:rgba(217,119,6,.2)"><div class="mmn">${t('leg_field')}</div><div class="mmv">${d.trainstud[i]}</div></div>
        <div class="mmc" style="border:1.5px solid rgba(5,150,105,.6);background:rgba(5,150,105,.2)"><div class="mmn">${t('leg_resident')}</div><div class="mmv">${d.trainres[i]}</div></div>
      </div>
    </div>
    <div class="g5">
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_cases')}</div><div class="cw" style="height:145px"><canvas id="mc_crit"></canvas></div></div>
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_transport')}</div><div class="cw" style="height:145px"><canvas id="mc_tr"></canvas></div></div>
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_part')}</div><div class="cw" style="height:145px"><canvas id="mc_part"></canvas></div></div>
      <div class="card" style="border-top:3px solid #0d9488;text-align:center">
        <div class="ct" style="color:#0d9488;margin-bottom:6px">${t('th_evac')}</div>
        <div style="font-size:42px;font-weight:900;color:#0d9488;line-height:1.1">${d.evac[i]}</div>
        <div style="font-size:11px;color:#748995;margin-top:4px">${t('evac_lbl')}</div>
      </div>
      <div class="card" style="border-top:3px solid #d97706">
        <div class="ct" style="color:#b45309;margin-bottom:8px">${t('kpi_train')}</div>
        <div style="display:flex;justify-content:space-around;align-items:center">
          <div style="text-align:center"><div style="font-size:28px;font-weight:900;color:#d97706">${d.trainstud[i]}</div><div style="font-size:9px;color:#748995;margin-top:2px">${t('leg_field')}</div></div>
          <div style="width:1px;height:40px;background:#eee"></div>
          <div style="text-align:center"><div style="font-size:28px;font-weight:900;color:#059669">${d.trainres[i]}</div><div style="font-size:9px;color:#748995;margin-top:2px">${t('leg_resident')}</div></div>
        </div>
      </div>
    </div>
    <div class="card">
      <div class="ct" style="margin-bottom:13px">${mn[i]} ${YEAR} — ${t('dtl_table')}</div>
      ${[
        [d.trans[i],'#0084BD',t('leg_trans')],
        [d.nontrans[i],'#ef4444',t('leg_nontrans')],
        [d.trin[i],'#16a34a',t('leg_internal')],
        [d.trout[i],'#ea580c',t('leg_external')],
        [d.partin[i],'#7c3aed',t('leg_partin')],
        [d.partout[i],'#748995',t('leg_partout')],
        [d.evac[i],'#0d9488',t('th_evac')],
        [d.trainstud[i],'#d97706',t('leg_field')],
        [d.trainres[i],'#059669',t('leg_resident')],
      ].map(([v,c,l])=>`<div class="pr-row"><div class="pr-lbl">${l}</div><div class="pr-tr"><div class="pr-fi" style="background:${c};width:${Math.round(v/allMax*100)}%"></div></div><div class="pr-val" style="color:${c}">${v}</div></div>`).join('')}
    </div>
  `;
  setTimeout(()=>{
    mk('mc_crit',{type:'doughnut',data:{labels:[t('leg_trans'),t('leg_nontrans')],datasets:[{data:[d.trans[i],d.nontrans[i]],backgroundColor:['#0084BD','#ef4444'],borderWidth:2,borderColor:'#fff',hoverOffset:4}]},options:doughnutOpts()});
    mk('mc_tr',{type:'doughnut',data:{labels:[t('leg_internal'),t('leg_external')],datasets:[{data:[d.trin[i],d.trout[i]],backgroundColor:['#16a34a','#ea580c'],borderWidth:2,borderColor:'#fff',hoverOffset:4}]},options:doughnutOpts()});
    mk('mc_part',{type:'doughnut',data:{labels:[t('leg_partin'),t('leg_partout')],datasets:[{data:[d.partin[i],d.partout[i]],backgroundColor:['#7c3aed','#748995'],borderWidth:2,borderColor:'#fff',hoverOffset:4}]},options:doughnutOpts()});
  },50);
}

/* ═══════════════════════════════════════════════════════
   QUARTERLY PAGE
═══════════════════════════════════════════════════════ */
function showQ(qNum,btnEl){
  if(btnEl){
    document.querySelectorAll('#q-tabs .qtab').forEach(b=>b.classList.remove('active'));
    btnEl.classList.add('active');
  } else {
    document.querySelectorAll('#q-tabs .qtab').forEach((b,i)=>{ b.classList.toggle('active',i===0); });
  }
  const d=DATA, mn=MN(), q=qNum-1;
  const qMonths=[0,1,2].map(j=>q*3+j);
  const qData={};
  ALL_KEYS.forEach(k=>{ qData[k]=qMonths.map(j=>d[k][j]); });
  const totCrit=qMonths.reduce((a,j)=>a+d.trans[j]+d.nontrans[j],0);
  const qColors=['#0084BD','#005f8a','#3BAAD4'];
  const grad=['linear-gradient(135deg,#005f8a,#0084BD)','linear-gradient(135deg,#006A9E,#3BAAD4)','linear-gradient(135deg,#3BAAD4,#0084BD)','linear-gradient(135deg,#748995,#4a5568)'][q];
  const qLabel=t('quarters')[q];
  const monthLabels=qMonths.map(j=>mn[j]);
  const insight=t('q_insight')[q];

  document.getElementById('q-content').innerHTML=`
    <div class="mhero" style="background:${grad}">
      <div class="mht">
        <div><div class="mht-title">${qLabel} — ${YEAR}</div><div class="mht-sub">${monthLabels.join(' · ')}</div></div>
        <div class="mtot"><div class="mtot-n">${totCrit}</div><div class="mtot-l">${t('kpi_cases')}</div></div>
      </div>
      <div class="mmetrics" style="grid-template-columns:repeat(3,1fr)">
        ${qMonths.map(j=>`<div class="mmc"><div class="mmn">${mn[j]}</div><div class="mmv">${d.trans[j]+d.nontrans[j]}</div></div>`).join('')}
      </div>
    </div>
    <div class="card" style="margin-bottom:12px;border-right:4px solid #0084BD">
      <p style="font-size:13px;line-height:1.8;color:var(--text)">${insight}</p>
    </div>
    <div class="g2b">
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_cases')}</div>
        <div class="leg"><span><span class="lsq" style="background:#0084BD"></span>${t('leg_trans')}</span><span><span class="lsq" style="background:#ef4444"></span>${t('leg_nontrans')}</span></div>
        <div class="cw" style="height:195px"><canvas id="qq_crit"></canvas></div></div>
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_transport')}</div>
        <div class="leg"><span><span class="lsq" style="background:#16a34a"></span>${t('leg_internal')}</span><span><span class="lsq" style="background:#ea580c"></span>${t('leg_external')}</span></div>
        <div class="cw" style="height:195px"><canvas id="qq_tr"></canvas></div></div>
    </div>
    <div class="g3">
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_part')}</div><div class="cw" style="height:165px"><canvas id="qq_part"></canvas></div></div>
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('th_evac')}</div><div class="cw" style="height:165px"><canvas id="qq_evac"></canvas></div></div>
      <div class="card"><div class="ct" style="margin-bottom:9px">${t('kpi_train')}</div><div class="cw" style="height:165px"><canvas id="qq_train"></canvas></div></div>
    </div>
    <div class="card">
      <div class="ct" style="margin-bottom:13px">${qLabel} — ${t('dtl_table')}</div>
      ${['trans','nontrans','trin','trout','partin','partout','evac','trainstud','trainres'].map((k,ki)=>{
        const colors=['#0084BD','#ef4444','#16a34a','#ea580c','#7c3aed','#748995','#0d9488','#d97706','#059669'];
        const labels=[t('leg_trans'),t('leg_nontrans'),t('leg_internal'),t('leg_external'),t('leg_partin'),t('leg_partout'),t('th_evac'),t('leg_field'),t('leg_resident')];
        const vals=qMonths.map(j=>d[k][j]);
        const mx=Math.max(...vals)||1;
        return vals.map((v,vi)=>`<div class="pr-row"><div class="pr-lbl">${monthLabels[vi]} — ${labels[ki]}</div><div class="pr-tr"><div class="pr-fi" style="background:${colors[ki]};width:${Math.round(v/mx*100)}%"></div></div><div class="pr-val" style="color:${colors[ki]}">${v}</div></div>`).join('');
      }).join('')}
    </div>
  `;
  setTimeout(()=>{
    mk('qq_crit',{type:'bar',data:{labels:monthLabels,datasets:[{label:t('leg_trans'),data:qData.trans,backgroundColor:'#0084BD',borderRadius:6},{label:t('leg_nontrans'),data:qData.nontrans,backgroundColor:'#ef4444',borderRadius:6}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:10,padding:7}}}}});
    mk('qq_tr',{type:'bar',data:{labels:monthLabels,datasets:[{label:t('leg_internal'),data:qData.trin,backgroundColor:'#16a34a',borderRadius:6},{label:t('leg_external'),data:qData.trout,backgroundColor:'#ea580c',borderRadius:6}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:10,padding:7}}}}});
    mk('qq_part',{type:'doughnut',data:{labels:[t('leg_partin'),t('leg_partout')],datasets:[{data:[sum(qData.partin),sum(qData.partout)],backgroundColor:['#7c3aed','#748995'],borderWidth:2,borderColor:'#fff',hoverOffset:4}]},options:doughnutOpts()});
    mk('qq_evac',{type:'bar',data:{labels:monthLabels,datasets:[{data:qData.evac,backgroundColor:'#0d9488',borderRadius:6}]},options:{...BASE}});
    mk('qq_train',{type:'bar',data:{labels:monthLabels,datasets:[{label:t('leg_field'),data:qData.trainstud,backgroundColor:'#d97706',borderRadius:6},{label:t('leg_resident'),data:qData.trainres,backgroundColor:'#059669',borderRadius:6}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:10},boxWidth:9,padding:6}}}}});
  },50);
}

/* ═══════════════════════════════════════════════════════
   COMPARE
═══════════════════════════════════════════════════════ */
function renderCompare(d,mn){
  mk('cc1',{type:'bar',data:{labels:mn,datasets:[{label:t('leg_trans'),data:d.trans,backgroundColor:'#0084BD',borderRadius:4},{label:t('leg_nontrans'),data:d.nontrans,backgroundColor:'#ef4444',borderRadius:4}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:10},boxWidth:10,padding:6}}}}});
  mk('cc2',{type:'bar',data:{labels:mn,datasets:[{label:t('leg_internal'),data:d.trin,backgroundColor:'#16a34a',borderRadius:4},{label:t('leg_external'),data:d.trout,backgroundColor:'#ea580c',borderRadius:4}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:10},boxWidth:10,padding:6}}}}});
  mk('cc3',{type:'line',data:{labels:mn,datasets:[{label:t('leg_partin'),data:d.partin,borderColor:'#7c3aed',backgroundColor:'rgba(124,58,237,.1)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#7c3aed',pointBorderWidth:2,borderWidth:2.5},{label:t('leg_partout'),data:d.partout,borderColor:'#748995',backgroundColor:'rgba(116,137,149,.07)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#748995',pointBorderWidth:2,borderWidth:2}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:10,padding:8}}}}});
  mk('cc4',{type:'line',data:{labels:mn,datasets:[{label:t('th_evac'),data:d.evac,borderColor:'#0d9488',backgroundColor:'rgba(13,148,136,.14)',tension:.4,fill:true,pointRadius:5,pointBackgroundColor:'#fff',pointBorderColor:'#0d9488',pointBorderWidth:2.5,borderWidth:3}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:10,padding:8}}}}});
  mk('cc5',{type:'line',data:{labels:mn,datasets:[{label:t('leg_field'),data:d.trainstud,borderColor:'#d97706',backgroundColor:'rgba(217,119,6,.12)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#d97706',pointBorderWidth:2,borderWidth:2.5},{label:t('leg_resident'),data:d.trainres,borderColor:'#059669',backgroundColor:'rgba(5,150,105,.1)',tension:.4,fill:true,pointRadius:4,pointBackgroundColor:'#fff',pointBorderColor:'#059669',pointBorderWidth:2,borderWidth:2.5}]},options:{...BASE,plugins:{legend:{display:true,labels:{font:{size:11},boxWidth:10,padding:8}}}}});
  renderRank('rank_crit',d.trans.map((v,i)=>v+d.nontrans[i]),mn,'#0084BD');
  renderRank('rank_tr',d.trin.map((v,i)=>v+d.trout[i]),mn,'#16a34a');
  renderRank('rank_evac',d.evac,mn,'#0d9488');
}

function renderRank(id,arr,labels,color){
  const el=document.getElementById(id);
  if(!el)return;
  const mx=Math.max(...arr)||1;
  const sorted=[...arr].map((v,i)=>({v,i})).sort((a,b)=>b.v-a.v);
  el.innerHTML=sorted.map(({v,i},rank)=>`<div class="rank-item"><div class="rank-num">${rank+1}</div><div style="font-size:11px;min-width:60px">${labels[i]}</div><div class="rank-bar"><div class="rank-fill" style="background:${color};width:${Math.round(v/mx*100)}%"></div></div><div class="rank-val">${v}</div></div>`).join('');
}

/* ═══════════════════════════════════════════════════════
   DETAIL TABLE
═══════════════════════════════════════════════════════ */
function renderDetailTable(d,mn){
  const hd=document.getElementById('dtb-head');
  if(hd) hd.innerHTML=`<th>#</th><th>${t('th_month')}</th><th>${t('th_trans')}</th><th>${t('th_nontrans')}</th><th>${t('th_crit')}</th><th>${t('th_trin')}</th><th>${t('th_trout')}</th><th>${t('th_tr')}</th><th>${t('th_partin')}</th><th>${t('th_partout')}</th><th>${t('th_part')}</th><th style="background:#0f766e">${t('th_evac')}</th><th style="background:#b45309">${t('th_field')}</th><th style="background:#065f46">${t('th_res')}</th>`;
  const db=document.getElementById('dtb');
  if(!db)return;
  db.innerHTML=mn.map((m,i)=>{
    const crit=d.trans[i]+d.nontrans[i], tr=d.trin[i]+d.trout[i], part=d.partin[i]+d.partout[i];
    return `<tr><td>${i+1}</td><td><b>${m}</b></td><td style="color:#0084BD;font-weight:700">${d.trans[i]}</td><td style="color:#ef4444;font-weight:700">${d.nontrans[i]}</td><td><b>${crit}</b></td><td style="color:#16a34a;font-weight:700">${d.trin[i]}</td><td style="color:#ea580c;font-weight:700">${d.trout[i]}</td><td><b>${tr}</b></td><td style="color:#7c3aed;font-weight:700">${d.partin[i]}</td><td style="color:#748995;font-weight:700">${d.partout[i]}</td><td><b>${part}</b></td><td style="color:#0d9488;font-weight:800;background:#f0fdfa">${d.evac[i]}</td><td style="color:#b45309;font-weight:800;background:#fef9ee">${d.trainstud[i]}</td><td style="color:#065f46;font-weight:800;background:#f0fdf4">${d.trainres[i]}</td></tr>`;
  }).join('');
}

/* ═══════════════════════════════════════════════════════
   EDITOR
═══════════════════════════════════════════════════════ */
const ED_KEYS=[
  {k:'trans',color:'var(--kb-lt)',bc:'var(--kb)',tc:'var(--kb)'},
  {k:'nontrans',color:'#fee2e2',bc:'#ef4444',tc:'#ef4444'},
  {k:'trin',color:'#dcfce7',bc:'#16a34a',tc:'#15803d'},
  {k:'trout',color:'#ffedd5',bc:'#ea580c',tc:'#c2410c'},
  {k:'partin',color:'#ede9fe',bc:'#7c3aed',tc:'#6d28d9'},
  {k:'partout',color:'#f1f5f9',bc:'#748995',tc:'#475569'},
  {k:'evac',color:'#ccfbf1',bc:'#0d9488',tc:'#0f766e'},
  {k:'trainstud',color:'#fef3c7',bc:'#d97706',tc:'#92400e'},
  {k:'trainres',color:'#d1fae5',bc:'#059669',tc:'#065f46'},
];

function openEditor(){
  if(!isAdmin()){toast(t('toast_need_admin'));return;}
  const mn=MN();
  document.getElementById('editor-body').innerHTML=ED_KEYS.map(({k,color,bc,tc})=>`
    <div class="ed-sec">
      <div class="ed-sec-hd" style="--edb:${color};--edc:${tc}">${t('ed_'+k)}</div>
      <div class="mgrid">${mn.map((m,i)=>`<div class="mf"><label>${m}</label><input type="number" id="inp_${k}_${i}" value="${DATA[k][i]}" min="0" max="9999"></div>`).join('')}</div>
    </div>
  `).join('');
  document.getElementById('emod').classList.add('open');
}
function closeEd(){document.getElementById('emod').classList.remove('open');}
function applyData(){
  ED_KEYS.forEach(({k})=>{
    DATA[k]=DATA[k].map((_,i)=>{
      const el=document.getElementById('inp_'+k+'_'+i);
      return el?Math.max(0,Math.min(9999,parseInt(el.value)||0)):DATA[k][i];
    });
  });
  closeEd();
  renderAll();
  toast(t('toast_updated'));
}

/* ═══════════════════════════════════════════════════════
   SHARE & EXPORT
═══════════════════════════════════════════════════════ */
function openShare(){
  saveHash();
  document.getElementById('surl_inp').value=location.href;
  document.getElementById('smod').classList.add('open');
}
function closeShare(){document.getElementById('smod').classList.remove('open');}
function cpyURL(){
  const el=document.getElementById('surl_inp');
  try{navigator.clipboard.writeText(el.value);}catch(e){}
  el.select();document.execCommand('copy');
  toast(t('toast_url'));
}
function wa(){window.open('https://wa.me/?text='+encodeURIComponent('لوحة الأداء — المدينة الطبية الجامعية KSUMC '+YEAR+'\n'+location.href));}
function em(){window.open('mailto:?subject=KSUMC Dashboard '+YEAR+'&body='+encodeURIComponent(location.href));}

function exportCSV(){
  const mn=MN();
  const hdr=['Month','Transported','NonTransported','TotalEmergency','InternalTransport','ExternalTransport','TotalTransport','InternalParticipation','ExternalParticipation','TotalParticipation','Evacuation','FieldTraining','InternResident'];
  const rows=mn.map((m,i)=>[m,DATA.trans[i],DATA.nontrans[i],DATA.trans[i]+DATA.nontrans[i],DATA.trin[i],DATA.trout[i],DATA.trin[i]+DATA.trout[i],DATA.partin[i],DATA.partout[i],DATA.partin[i]+DATA.partout[i],DATA.evac[i],DATA.trainstud[i],DATA.trainres[i]]);
  const csv=[hdr,...rows].map(r=>r.join(',')).join('\n');
  const a=document.createElement('a');a.href='data:text/csv;charset=utf-8,\uFEFF'+encodeURIComponent(csv);a.download='KSUMC_'+YEAR+'.csv';a.click();
}
function copyTbl(){
  const mn=MN();
  const rows=mn.map((m,i)=>[m,DATA.trans[i],DATA.nontrans[i],DATA.trans[i]+DATA.nontrans[i],DATA.trin[i],DATA.trout[i],DATA.trin[i]+DATA.trout[i],DATA.partin[i],DATA.partout[i],DATA.partin[i]+DATA.partout[i],DATA.evac[i],DATA.trainstud[i],DATA.trainres[i]].join('\t')).join('\n');
  try{navigator.clipboard.writeText(rows);}catch(e){}
  toast(t('toast_copied')+' '+t('copy_excel'));
}

/* ═══════════════════════════════════════════════════════
   NAVIGATION & TOAST
═══════════════════════════════════════════════════════ */
function showPage(id,btn){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nb').forEach(b=>b.classList.remove('active'));
  const pg=document.getElementById(id);
  if(pg)pg.classList.add('active');
  if(btn)btn.classList.add('active');
}
function toast(m){
  const t_=document.getElementById('toast');
  t_.textContent=m;t_.classList.add('show');
  setTimeout(()=>t_.classList.remove('show'),2800);
}

/* ═══════════════════════════════════════════════════════
   INIT
═══════════════════════════════════════════════════════ */
window.addEventListener('DOMContentLoaded',()=>{
  loadHash();
  document.getElementById('root').lang=LANG;
  document.getElementById('root').dir=LANG==='ar'?'rtl':'ltr';
  document.getElementById('langSel').value=LANG;
  document.getElementById('yearSel').value=YEAR;
  document.getElementById('yr-display').textContent=YEAR;
  document.querySelectorAll('[data-i18n]').forEach(el=>{
    const k=el.getAttribute('data-i18n');
    if(t(k)!==k)el.textContent=t(k);
  });
  if(isAdmin()){
    document.getElementById('editBtn').style.display='inline-flex';
    document.getElementById('loginBtn').querySelector('[data-i18n]').textContent=t('admin_out');
    document.getElementById('loginBtn').classList.add('active');
  }
  renderAll();
});
</script>
</body>
</html>
