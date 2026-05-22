<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Probation Tracker — HR Operations</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,400&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0d0f14;
  --surface: #141720;
  --surface2: #1a1e2c;
  --surface3: #1f2436;
  --border: #262d40;
  --border2: #2e3650;
  --text: #e8ecf4;
  --text2: #9aa3b8;
  --text3: #5f6882;
  --accent: #4f7cff;
  --accent2: #7b5ea7;
  --success: #22c97a;
  --warning: #f5a623;
  --danger: #ff4f6a;
  --info: #38c4e8;
  --purple: #9b6dff;
  --teal: #00d4b4;
  --font-head: 'Syne', sans-serif;
  --font-body: 'DM Sans', sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --radius: 10px;
  --radius2: 6px;
  --shadow: 0 4px 24px rgba(0,0,0,0.4);
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{font-family:var(--font-body);background:var(--bg);color:var(--text);min-height:100vh;display:flex;font-size:14px}

/* Sidebar */
#sidebar{width:240px;min-width:240px;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;position:fixed;top:0;left:0;bottom:0;z-index:100;transition:transform .3s}
.sidebar-logo{padding:20px 20px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px}
.logo-icon{width:34px;height:34px;background:linear-gradient(135deg,var(--accent),var(--purple));border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0}
.logo-text{font-family:var(--font-head);font-size:15px;font-weight:700;line-height:1.2}
.logo-sub{font-size:11px;color:var(--text3);font-weight:400}
.sidebar-nav{flex:1;overflow-y:auto;padding:12px 0}
.nav-section{padding:4px 16px 2px;font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.1em;margin-top:6px}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 16px;cursor:pointer;transition:all .2s;color:var(--text2);border-left:2px solid transparent;font-size:13.5px;font-weight:500}
.nav-item:hover{color:var(--text);background:var(--surface2)}
.nav-item.active{color:var(--accent);background:rgba(79,124,255,.08);border-left-color:var(--accent)}
.nav-icon{width:18px;text-align:center;font-size:15px;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--danger);color:#fff;font-size:10px;font-family:var(--font-mono);padding:2px 6px;border-radius:10px;font-weight:600}
.sidebar-user{padding:14px 16px;border-top:1px solid var(--border);display:flex;align-items:center;gap:10px}
.user-avatar{width:32px;height:32px;border-radius:50%;background:linear-gradient(135deg,var(--accent2),var(--accent));display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;flex-shrink:0}
.user-info{flex:1;min-width:0}
.user-name{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.user-role{font-size:11px;color:var(--text3)}
.user-role-select{background:none;border:none;color:var(--accent);font-size:11px;cursor:pointer;font-family:var(--font-body);padding:0}

/* Main */
#main{margin-left:240px;flex:1;display:flex;flex-direction:column;min-height:100vh}
.topbar{background:var(--surface);border-bottom:1px solid var(--border);padding:0 24px;height:56px;display:flex;align-items:center;gap:16px;position:sticky;top:0;z-index:50}
.page-title{font-family:var(--font-head);font-size:18px;font-weight:700;flex:1}
.topbar-actions{display:flex;align-items:center;gap:8px}
.content{padding:24px;flex:1}

/* Buttons */
.btn{display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:var(--radius2);font-family:var(--font-body);font-size:13px;font-weight:600;cursor:pointer;transition:all .2s;border:none;text-decoration:none}
.btn-primary{background:var(--accent);color:#fff}
.btn-primary:hover{background:#3d68f0;transform:translateY(-1px)}
.btn-ghost{background:transparent;color:var(--text2);border:1px solid var(--border2)}
.btn-ghost:hover{color:var(--text);border-color:var(--text3);background:var(--surface2)}
.btn-success{background:var(--success);color:#0d1a10}
.btn-success:hover{opacity:.9}
.btn-danger{background:rgba(255,79,106,.15);color:var(--danger);border:1px solid rgba(255,79,106,.25)}
.btn-danger:hover{background:rgba(255,79,106,.25)}
.btn-sm{padding:5px 10px;font-size:12px}
.btn-xs{padding:3px 8px;font-size:11px}
.btn-icon{padding:6px;width:32px;justify-content:center}

/* Cards */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius)}
.card-header{padding:16px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
.card-title{font-family:var(--font-head);font-size:15px;font-weight:600}
.card-body{padding:20px}

/* Stats Grid */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:14px;margin-bottom:24px}
.stat-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:18px;position:relative;overflow:hidden;transition:transform .2s,border-color .2s}
.stat-card:hover{transform:translateY(-2px);border-color:var(--border2)}
.stat-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px}
.stat-card.blue::before{background:var(--accent)}
.stat-card.green::before{background:var(--success)}
.stat-card.orange::before{background:var(--warning)}
.stat-card.red::before{background:var(--danger)}
.stat-card.purple::before{background:var(--purple)}
.stat-card.teal::before{background:var(--teal)}
.stat-label{font-size:11px;color:var(--text3);font-weight:600;text-transform:uppercase;letter-spacing:.08em;margin-bottom:8px}
.stat-value{font-family:var(--font-head);font-size:28px;font-weight:800;line-height:1}
.stat-sub{font-size:11px;color:var(--text3);margin-top:4px}
.stat-icon{position:absolute;right:14px;top:14px;font-size:22px;opacity:.2}

/* Status Badges */
.badge{display:inline-flex;align-items:center;gap:4px;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:600;white-space:nowrap}
.badge::before{content:'';width:5px;height:5px;border-radius:50%;flex-shrink:0}
.badge-active{background:rgba(79,124,255,.15);color:var(--accent)}.badge-active::before{background:var(--accent)}
.badge-due{background:rgba(245,166,35,.15);color:var(--warning)}.badge-due::before{background:var(--warning)}
.badge-pending{background:rgba(155,109,255,.15);color:var(--purple)}.badge-pending::before{background:var(--purple)}
.badge-completed{background:rgba(34,201,122,.15);color:var(--success)}.badge-completed::before{background:var(--success)}
.badge-extended{background:rgba(255,79,106,.15);color:var(--danger)}.badge-extended::before{background:var(--danger)}
.badge-sent{background:rgba(56,196,232,.15);color:var(--info)}.badge-sent::before{background:var(--info)}
.badge-failed{background:rgba(255,79,106,.15);color:var(--danger)}.badge-failed::before{background:var(--danger)}
.badge-notrigger{background:rgba(95,104,130,.2);color:var(--text3)}.badge-notrigger::before{background:var(--text3)}

/* Table */
.table-wrap{overflow-x:auto;border-radius:var(--radius);border:1px solid var(--border)}
table{width:100%;border-collapse:collapse;font-size:13px}
thead tr{background:var(--surface2);border-bottom:1px solid var(--border)}
thead th{padding:10px 14px;text-align:left;font-family:var(--font-head);font-size:11px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;white-space:nowrap}
tbody tr{border-bottom:1px solid var(--border);transition:background .15s}
tbody tr:last-child{border-bottom:none}
tbody tr:hover{background:var(--surface2)}
tbody td{padding:11px 14px;vertical-align:middle}
.td-name{font-weight:600;color:var(--text)}
.td-sub{font-size:11px;color:var(--text3);margin-top:2px}
.td-mono{font-family:var(--font-mono);font-size:12px;color:var(--text2)}

/* Forms */
.form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:16px}
.form-grid-3{grid-template-columns:repeat(auto-fit,minmax(200px,1fr))}
.form-group{display:flex;flex-direction:column;gap:5px}
.form-group.full{grid-column:1/-1}
label{font-size:12px;font-weight:600;color:var(--text2)}
.required::after{content:' *';color:var(--danger)}
input,select,textarea{background:var(--surface2);border:1px solid var(--border2);border-radius:var(--radius2);padding:9px 12px;color:var(--text);font-family:var(--font-body);font-size:13px;width:100%;transition:border-color .2s}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--accent)}
input::placeholder,textarea::placeholder{color:var(--text3)}
select option{background:var(--surface2)}
.form-hint{font-size:11px;color:var(--text3)}
.auto-field{background:var(--surface3);border-color:var(--border);color:var(--text3);cursor:default}

/* Filter Bar */
.filter-bar{display:flex;gap:10px;flex-wrap:wrap;align-items:center;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:12px 16px;margin-bottom:16px}
.filter-bar input,.filter-bar select{flex:1;min-width:140px;max-width:200px;padding:7px 10px;font-size:12px}
.filter-bar .search-input{max-width:260px}

/* Modal */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:1000;display:flex;align-items:center;justify-content:center;padding:20px;backdrop-filter:blur(4px)}
.modal{background:var(--surface);border:1px solid var(--border);border-radius:12px;width:100%;max-width:700px;max-height:90vh;overflow-y:auto;animation:slideUp .25s ease}
.modal-lg{max-width:900px}
.modal-sm{max-width:460px}
@keyframes slideUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
.modal-header{padding:18px 22px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;background:var(--surface);z-index:1}
.modal-title{font-family:var(--font-head);font-size:16px;font-weight:700}
.modal-body{padding:22px}
.modal-footer{padding:16px 22px;border-top:1px solid var(--border);display:flex;gap:10px;justify-content:flex-end}
.btn-close{background:none;border:none;color:var(--text3);cursor:pointer;font-size:18px;padding:4px;display:flex;align-items:center;justify-content:center;border-radius:4px}
.btn-close:hover{color:var(--text);background:var(--surface2)}

/* Toast */
#toast-container{position:fixed;bottom:24px;right:24px;z-index:9999;display:flex;flex-direction:column;gap:8px}
.toast{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:12px 16px;display:flex;align-items:center;gap:10px;min-width:280px;max-width:380px;animation:toastIn .3s ease;box-shadow:var(--shadow)}
@keyframes toastIn{from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:translateX(0)}}
.toast-icon{font-size:16px;flex-shrink:0}
.toast-msg{font-size:13px;font-weight:500;flex:1}
.toast.success{border-left:3px solid var(--success)}
.toast.error{border-left:3px solid var(--danger)}
.toast.info{border-left:3px solid var(--accent)}
.toast.warning{border-left:3px solid var(--warning)}

/* Misc */
.section-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.section-title{font-family:var(--font-head);font-size:16px;font-weight:700}
.empty-state{text-align:center;padding:48px 24px;color:var(--text3)}
.empty-state .empty-icon{font-size:40px;margin-bottom:12px;opacity:.5}
.empty-state p{font-size:14px}
.dot{width:6px;height:6px;border-radius:50%;display:inline-block}
.divider{height:1px;background:var(--border);margin:16px 0}
.chip{display:inline-flex;align-items:center;background:var(--surface2);border:1px solid var(--border);border-radius:4px;padding:2px 7px;font-size:11px;font-family:var(--font-mono);color:var(--text2)}
.progress-bar{height:4px;background:var(--surface3);border-radius:2px;overflow:hidden}
.progress-fill{height:100%;border-radius:2px;transition:width .5s ease}
.info-row{display:flex;gap:6px;padding:8px 0;border-bottom:1px solid var(--border);font-size:13px}
.info-row:last-child{border-bottom:none}
.info-label{color:var(--text3);min-width:160px;font-weight:500}
.info-value{color:var(--text);font-weight:500}
.history-item{padding:12px;background:var(--surface2);border-radius:var(--radius2);margin-bottom:8px;border-left:3px solid var(--border2)}
.history-item.completed{border-left-color:var(--success)}
.history-item.extended{border-left-color:var(--danger)}
.history-item.pending{border-left-color:var(--purple)}
.history-item.active{border-left-color:var(--accent)}
.tab-bar{display:flex;gap:2px;background:var(--surface2);border-radius:var(--radius2);padding:3px;margin-bottom:20px;width:fit-content}
.tab{padding:7px 16px;border-radius:5px;cursor:pointer;font-size:13px;font-weight:500;color:var(--text3);transition:all .2s}
.tab.active{background:var(--surface);color:var(--text);box-shadow:0 2px 8px rgba(0,0,0,.3)}
.alert{padding:12px 16px;border-radius:var(--radius2);font-size:13px;display:flex;align-items:center;gap:8px;margin-bottom:16px}
.alert-warning{background:rgba(245,166,35,.12);border:1px solid rgba(245,166,35,.25);color:var(--warning)}
.alert-info{background:rgba(79,124,255,.1);border:1px solid rgba(79,124,255,.2);color:var(--accent)}
.days-count{font-family:var(--font-mono);font-size:12px}
.days-overdue{color:var(--danger)}
.days-soon{color:var(--warning)}
.days-ok{color:var(--success)}
.action-row{display:flex;gap:6px;align-items:center}
.notification-type{font-size:11px;padding:2px 7px;border-radius:4px;font-weight:600;background:var(--surface2)}
.notification-hrbp{color:var(--purple)}
.notification-recruiter{color:var(--info)}
.notification-referrer{color:var(--teal)}
.quick-actions{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;margin-bottom:24px}
.quick-action{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:16px;cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:12px}
.quick-action:hover{border-color:var(--accent);background:rgba(79,124,255,.05);transform:translateY(-1px)}
.qa-icon{width:40px;height:40px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.qa-label{font-size:13px;font-weight:600}
.qa-sub{font-size:11px;color:var(--text3)}
.status-flow{display:flex;align-items:center;gap:6px;flex-wrap:wrap;margin:12px 0}
.flow-step{padding:5px 12px;border-radius:20px;font-size:11px;font-weight:600;border:1px solid}
.flow-arrow{color:var(--text3);font-size:12px}

@media(max-width:900px){
  #sidebar{transform:translateX(-100%)}
  #sidebar.open{transform:translateX(0)}
  #main{margin-left:0}
}
</style>
</head>
<body>

<!-- Sidebar -->
<nav id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-icon">📋</div>
    <div>
      <div class="logo-text">ProbTrack</div>
      <div class="logo-sub">HR Operations</div>
    </div>
  </div>
  <div class="sidebar-nav">
    <div class="nav-section">Main</div>
    <div class="nav-item active" onclick="navigate('dashboard')"><span class="nav-icon">📊</span> Dashboard</div>
    <div class="nav-item" onclick="navigate('create')"><span class="nav-icon">➕</span> Create Candidate</div>
    <div class="nav-item" onclick="navigate('candidates')"><span class="nav-icon">👥</span> Candidate List</div>
    <div class="nav-section">Workflow</div>
    <div class="nav-item" onclick="navigate('pending')"><span class="nav-icon">⏳</span> Pending HRBP Action <span class="nav-badge" id="pendingBadge">0</span></div>
    <div class="nav-item" onclick="navigate('completed')"><span class="nav-icon">✅</span> Completed Probation</div>
    <div class="nav-item" onclick="navigate('extended')"><span class="nav-icon">📅</span> Extended Probation</div>
    <div class="nav-section">Logs</div>
    <div class="nav-item" onclick="navigate('notifications')"><span class="nav-icon">🔔</span> Notification Log</div>
    <div class="nav-section">Admin</div>
    <div class="nav-item" onclick="navigate('settings')"><span class="nav-icon">⚙️</span> Admin Settings</div>
  </div>
  <div class="sidebar-user">
    <div class="user-avatar" id="userAvatarSidebar">A</div>
    <div class="user-info">
      <div class="user-name">Admin User</div>
      <select class="user-role-select" id="roleSelector" onchange="changeRole(this.value)">
        <option value="Admin">Admin</option>
        <option value="Recruiter">Recruiter</option>
        <option value="HRBP">HRBP</option>
      </select>
    </div>
  </div>
</nav>

<!-- Main Content -->
<div id="main">
  <div class="topbar">
    <div class="page-title" id="pageTitle">Dashboard</div>
    <div class="topbar-actions">
      <button class="btn btn-ghost btn-sm" onclick="runDailyCheck()" title="Run daily probation check">🔄 Run Check</button>
      <button class="btn btn-primary btn-sm" onclick="navigate('create')">+ New Candidate</button>
    </div>
  </div>
  <div class="content" id="content"></div>
</div>

<!-- Toast Container -->
<div id="toast-container"></div>

<!-- Modal Container -->
<div id="modal-container"></div>

<script>
// =========================================================
// DATA STORE (localStorage)
// =========================================================
const DB = {
  get(key, def=[]) {
    try { return JSON.parse(localStorage.getItem('pt_'+key)) ?? def; } catch { return def; }
  },
  set(key, val) {
    localStorage.setItem('pt_'+key, JSON.stringify(val));
  },
  getObj(key, def={}) {
    try { return JSON.parse(localStorage.getItem('pt_'+key)) ?? def; } catch { return def; }
  }
};

// Seed demo data if empty
function seedData() {
  if (DB.get('seeded', false)) return;
  const today = new Date();
  const candidates = [
    { id:'C001', candidate_id:'EMP001', candidate_name:'Ananya Sharma', candidate_source:'LinkedIn', email_address:'ananya.sharma@company.com', referrer_name:'Rahul Verma', referrer_email:'rahul.verma@company.com', recruiter_name:'Priya Nair', recruiter_email:'priya.nair@company.com', hrbp_name:'Deepak Mehta', hrbp_email:'deepak.mehta@company.com', department_name:'Engineering', date_of_joining: daysAgo(today, 185), joining_location:'Hyderabad', probation_status:'Pending HRBP Confirmation', notification_status:'Sent', created_at: daysAgo(today, 185), created_by:'Admin', updated_at: daysAgo(today, 5), updated_by:'System' },
    { id:'C002', candidate_id:'EMP002', candidate_name:'Ravi Kumar', candidate_source:'Referral', email_address:'ravi.kumar@company.com', referrer_name:'Sneha Patel', referrer_email:'sneha.patel@company.com', recruiter_name:'Amit Joshi', recruiter_email:'amit.joshi@company.com', hrbp_name:'Kavya Reddy', hrbp_email:'kavya.reddy@company.com', department_name:'Product', date_of_joining: daysAgo(today, 180), joining_location:'Bangalore', probation_status:'Due for Review', notification_status:'Not Triggered', created_at: daysAgo(today, 180), created_by:'Admin', updated_at: daysAgo(today, 180), updated_by:'Admin' },
    { id:'C003', candidate_id:'EMP003', candidate_name:'Meena Iyer', candidate_source:'Naukri', email_address:'meena.iyer@company.com', referrer_name:'', referrer_email:'', recruiter_name:'Priya Nair', recruiter_email:'priya.nair@company.com', hrbp_name:'Deepak Mehta', hrbp_email:'deepak.mehta@company.com', department_name:'Design', date_of_joining: daysAgo(today, 200), joining_location:'Mumbai', probation_status:'Completed', notification_status:'Sent', completed_date: daysAgo(today, 20), recruiter_notified:true, referrer_notified: false, created_at: daysAgo(today, 200), created_by:'Admin', updated_at: daysAgo(today, 20), updated_by:'Deepak Mehta' },
    { id:'C004', candidate_id:'EMP004', candidate_name:'Arjun Nambiar', candidate_source:'Referral', email_address:'arjun.nambiar@company.com', referrer_name:'Kiran Pillai', referrer_email:'kiran.pillai@company.com', recruiter_name:'Amit Joshi', recruiter_email:'amit.joshi@company.com', hrbp_name:'Kavya Reddy', hrbp_email:'kavya.reddy@company.com', department_name:'Sales', date_of_joining: daysAgo(today, 210), joining_location:'Chennai', probation_status:'Extended', notification_status:'Sent', extension_reason:'Performance concerns', extended_till_date: daysFromDate(new Date(daysAgo(today, 210)), 270), remarks:'Needs mentoring for 3 more months', recruiter_notified:true, created_at: daysAgo(today, 210), created_by:'Admin', updated_at: daysAgo(today, 10), updated_by:'Kavya Reddy' },
    { id:'C005', candidate_id:'EMP005', candidate_name:'Pooja Gupta', candidate_source:'Campus', email_address:'pooja.gupta@company.com', referrer_name:'', referrer_email:'', recruiter_name:'Priya Nair', recruiter_email:'priya.nair@company.com', hrbp_name:'Deepak Mehta', hrbp_email:'deepak.mehta@company.com', department_name:'Finance', date_of_joining: daysAgo(today, 90), joining_location:'Delhi', probation_status:'Under Probation', notification_status:'Not Triggered', created_at: daysAgo(today, 90), created_by:'Admin', updated_at: daysAgo(today, 90), updated_by:'Admin' },
    { id:'C006', candidate_id:'EMP006', candidate_name:'Vikram Singh', candidate_source:'LinkedIn', email_address:'vikram.singh@company.com', referrer_name:'', referrer_email:'', recruiter_name:'Amit Joshi', recruiter_email:'amit.joshi@company.com', hrbp_name:'Kavya Reddy', hrbp_email:'kavya.reddy@company.com', department_name:'Engineering', date_of_joining: daysAgo(today, 45), joining_location:'Hyderabad', probation_status:'Under Probation', notification_status:'Not Triggered', created_at: daysAgo(today, 45), created_by:'Admin', updated_at: daysAgo(today, 45), updated_by:'Admin' },
  ];
  candidates.forEach(c => {
    const doj = new Date(c.date_of_joining);
    c.probation_start_date = c.date_of_joining;
    c.probation_end_date = daysFromDate(doj, 180);
  });
  DB.set('candidates', candidates);

  const statusHistory = [
    { id:'SH001', candidate_id:'C001', previous_status:'Under Probation', new_status:'Due for Review', remarks:'Auto-updated by system on 180th day', updated_by:'System', updated_at: daysAgo(today, 6) },
    { id:'SH002', candidate_id:'C001', previous_status:'Due for Review', new_status:'Pending HRBP Confirmation', remarks:'HRBP reminder sent', updated_by:'System', updated_at: daysAgo(today, 5) },
    { id:'SH003', candidate_id:'C003', previous_status:'Pending HRBP Confirmation', new_status:'Completed', remarks:'Candidate performed well throughout the period', updated_by:'Deepak Mehta', updated_at: daysAgo(today, 20) },
    { id:'SH004', candidate_id:'C004', previous_status:'Pending HRBP Confirmation', new_status:'Extended', remarks:'Needs mentoring for 3 more months', updated_by:'Kavya Reddy', updated_at: daysAgo(today, 10) },
  ];
  DB.set('status_history', statusHistory);

  const notifications = [
    { id:'N001', candidate_id:'C001', notification_type:'HRBP Reminder', recipient_name:'Deepak Mehta', recipient_email:'deepak.mehta@company.com', cc_email:'', subject:'Probation Review Required for Ananya Sharma', message_body:'Hi Deepak Mehta, Ananya Sharma has completed 180 days of probation. Kindly review and update the probation status.', sent_status:'Sent', error_message:'', sent_at: daysAgo(today, 5), triggered_by:'System' },
    { id:'N002', candidate_id:'C003', notification_type:'Recruiter Update', recipient_name:'Priya Nair', recipient_email:'priya.nair@company.com', cc_email:'', subject:'Probation Status Updated for Meena Iyer', message_body:'Hi Priya Nair, The probation status for Meena Iyer has been updated by HRBP as Completed.', sent_status:'Sent', error_message:'', sent_at: daysAgo(today, 20), triggered_by:'System' },
    { id:'N003', candidate_id:'C004', notification_type:'Recruiter Update', recipient_name:'Amit Joshi', recipient_email:'amit.joshi@company.com', cc_email:'', subject:'Probation Status Updated for Arjun Nambiar', message_body:'Hi Amit Joshi, The probation status for Arjun Nambiar has been updated by HRBP as Extended.', sent_status:'Sent', error_message:'', sent_at: daysAgo(today, 10), triggered_by:'System' },
    { id:'N004', candidate_id:'C002', notification_type:'HRBP Reminder', recipient_name:'Kavya Reddy', recipient_email:'kavya.reddy@company.com', cc_email:'', subject:'Probation Review Required for Ravi Kumar', message_body:'Hi Kavya Reddy, Ravi Kumar has completed 180 days of probation.', sent_status:'Failed', error_message:'SMTP timeout', sent_at: daysAgo(today, 1), triggered_by:'System' },
  ];
  DB.set('notifications', notifications);

  const users = [
    { id:'U001', user_name:'Admin User', email:'admin@company.com', role:'Admin', department:'HR', location:'Hyderabad', active_flag:true, created_at: daysAgo(today, 365) },
    { id:'U002', user_name:'Priya Nair', email:'priya.nair@company.com', role:'Recruiter', department:'TA', location:'Hyderabad', active_flag:true, created_at: daysAgo(today, 300) },
    { id:'U003', user_name:'Amit Joshi', email:'amit.joshi@company.com', role:'Recruiter', department:'TA', location:'Bangalore', active_flag:true, created_at: daysAgo(today, 280) },
    { id:'U004', user_name:'Deepak Mehta', email:'deepak.mehta@company.com', role:'HRBP', department:'HR', location:'Hyderabad', active_flag:true, created_at: daysAgo(today, 365) },
    { id:'U005', user_name:'Kavya Reddy', email:'kavya.reddy@company.com', role:'HRBP', department:'HR', location:'Bangalore', active_flag:true, created_at: daysAgo(today, 365) },
  ];
  DB.set('users', users);

  const templates = [
    { id:'T001', template_name:'HRBP Reminder', subject:'Probation Review Required for [Candidate Name]', body:'Hi [HRBP Name],\n\n[Candidate Name] has completed 180 days of probation as of [Probation End Date]. Kindly review and update the probation status as Completed or Extended in the Probation Tracker system.\n\nBest regards,\nHR Operations Team', is_active:true, updated_by:'Admin', updated_at: daysAgo(today, 30) },
    { id:'T002', template_name:'Recruiter Notification', subject:'Probation Status Updated for [Candidate Name]', body:'Hi [Recruiter Name],\n\nThe probation status for [Candidate Name] has been updated by HRBP as [Status]. Please check the Probation Tracker for further details.\n\nBest regards,\nHR Operations Team', is_active:true, updated_by:'Admin', updated_at: daysAgo(today, 30) },
    { id:'T003', template_name:'Referrer Email', subject:'Referral Claim Form Submission for [Candidate Name]', body:'Hi [Referrer Name],\n\nThanks for referring [Candidate Name] to our organization. We are pleased to inform you that your referral has successfully completed the probation period.\n\nKindly revert back to the recruiter [Recruiter Name] with the updated claim form to process your referral bonus.\n\nCC: [Recruiter Email]\n\nBest regards,\nHR Operations Team', is_active:true, updated_by:'Admin', updated_at: daysAgo(today, 30) },
  ];
  DB.set('email_templates', templates);

  const departments = ['Engineering','Product','Design','Sales','Finance','Marketing','Operations','HR','Legal'];
  const locations = ['Hyderabad','Bangalore','Mumbai','Chennai','Delhi','Pune','Kolkata'];
  DB.set('departments', departments);
  DB.set('locations', locations);
  DB.set('seeded', true);
}

function daysAgo(base, n) {
  const d = new Date(base);
  d.setDate(d.getDate() - n);
  return d.toISOString().split('T')[0];
}
function daysFromDate(base, n) {
  const d = new Date(base);
  d.setDate(d.getDate() + n);
  return d.toISOString().split('T')[0];
}
function daysBetween(d1, d2) {
  return Math.floor((new Date(d2) - new Date(d1)) / 86400000);
}
function fmtDate(d) {
  if (!d) return '—';
  return new Date(d).toLocaleDateString('en-IN', {day:'2-digit', month:'short', year:'numeric'});
}
function fmtDateTime(d) {
  if (!d) return '—';
  return new Date(d).toLocaleString('en-IN', {day:'2-digit', month:'short', year:'numeric', hour:'2-digit', minute:'2-digit'});
}
function uid() { return 'id_' + Date.now() + '_' + Math.random().toString(36).slice(2,6); }

// =========================================================
// STATE
// =========================================================
let currentPage = 'dashboard';
let currentRole = 'Admin';

// =========================================================
// NAVIGATION
// =========================================================
const PAGE_TITLES = {
  dashboard: 'Dashboard',
  create: 'Create Candidate',
  candidates: 'Candidate List',
  pending: 'Pending HRBP Action',
  completed: 'Completed Probation',
  extended: 'Extended Probation',
  notifications: 'Notification Log',
  settings: 'Admin Settings',
};

function navigate(page) {
  currentPage = page;
  document.getElementById('pageTitle').textContent = PAGE_TITLES[page] || page;
  document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(el => {
    if (el.getAttribute('onclick') && el.getAttribute('onclick').includes(`'${page}'`)) el.classList.add('active');
  });
  updateBadges();
  renderPage();
}

function updateBadges() {
  const candidates = DB.get('candidates');
  const pending = candidates.filter(c => c.probation_status === 'Pending HRBP Confirmation').length;
  const el = document.getElementById('pendingBadge');
  el.textContent = pending;
  el.style.display = pending > 0 ? '' : 'none';
}

// =========================================================
// RENDER PAGE
// =========================================================
function renderPage() {
  const content = document.getElementById('content');
  switch(currentPage) {
    case 'dashboard': content.innerHTML = renderDashboard(); break;
    case 'create': content.innerHTML = renderCreate(); break;
    case 'candidates': content.innerHTML = renderCandidates(); break;
    case 'pending': content.innerHTML = renderPending(); break;
    case 'completed': content.innerHTML = renderCompleted(); break;
    case 'extended': content.innerHTML = renderExtended(); break;
    case 'notifications': content.innerHTML = renderNotifications(); break;
    case 'settings': content.innerHTML = renderSettings(); break;
  }
}

// =========================================================
// DASHBOARD
// =========================================================
function renderDashboard() {
  const candidates = DB.get('candidates');
  const notifications = DB.get('notifications');
  const today = new Date().toISOString().split('T')[0];

  const total = candidates.length;
  const underProbation = candidates.filter(c => c.probation_status === 'Under Probation').length;
  const dueToday = candidates.filter(c => c.probation_end_date === today).length;
  const dueForReview = candidates.filter(c => c.probation_status === 'Due for Review').length;
  const pendingHRBP = candidates.filter(c => c.probation_status === 'Pending HRBP Confirmation').length;
  const completed = candidates.filter(c => c.probation_status === 'Completed').length;
  const extended = candidates.filter(c => c.probation_status === 'Extended').length;
  const notifSent = notifications.filter(n => n.sent_status === 'Sent').length;
  const notifFailed = notifications.filter(n => n.sent_status === 'Failed').length;

  const recentActivity = DB.get('status_history').slice(-5).reverse();

  return `
  <div class="stats-grid">
    <div class="stat-card blue"><div class="stat-icon">👥</div><div class="stat-label">Total Under Probation</div><div class="stat-value">${total}</div><div class="stat-sub">All active records</div></div>
    <div class="stat-card orange"><div class="stat-icon">📅</div><div class="stat-label">Due for Review</div><div class="stat-value">${dueForReview}</div><div class="stat-sub">180 days completed</div></div>
    <div class="stat-card purple"><div class="stat-icon">⏳</div><div class="stat-label">Pending HRBP Action</div><div class="stat-value">${pendingHRBP}</div><div class="stat-sub">Awaiting confirmation</div></div>
    <div class="stat-card green"><div class="stat-icon">✅</div><div class="stat-label">Completed</div><div class="stat-value">${completed}</div><div class="stat-sub">Probation passed</div></div>
    <div class="stat-card red"><div class="stat-icon">🔄</div><div class="stat-label">Extended</div><div class="stat-value">${extended}</div><div class="stat-sub">Period extended</div></div>
    <div class="stat-card teal"><div class="stat-icon">🔔</div><div class="stat-label">Notifications</div><div class="stat-value">${notifSent}</div><div class="stat-sub">${notifFailed} failed</div></div>
  </div>

  <div class="quick-actions">
    <div class="quick-action" onclick="navigate('create')">
      <div class="qa-icon" style="background:rgba(79,124,255,.15)">➕</div>
      <div><div class="qa-label">Add New Joiner</div><div class="qa-sub">Create probation record</div></div>
    </div>
    <div class="quick-action" onclick="navigate('pending')">
      <div class="qa-icon" style="background:rgba(155,109,255,.15)">⏳</div>
      <div><div class="qa-label">Pending Actions</div><div class="qa-sub">${pendingHRBP} awaiting HRBP</div></div>
    </div>
    <div class="quick-action" onclick="runDailyCheck()">
      <div class="qa-icon" style="background:rgba(0,212,180,.15)">🔄</div>
      <div><div class="qa-label">Run Daily Check</div><div class="qa-sub">Trigger auto-scheduler</div></div>
    </div>
    <div class="quick-action" onclick="navigate('notifications')">
      <div class="qa-icon" style="background:rgba(245,166,35,.15)">🔔</div>
      <div><div class="qa-label">Notification Log</div><div class="qa-sub">${notifFailed} failed to retry</div></div>
    </div>
  </div>

  <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
    <div class="card">
      <div class="card-header"><div class="card-title">Status Distribution</div></div>
      <div class="card-body">
        ${renderStatusBar('Under Probation', underProbation, total, 'var(--accent)')}
        ${renderStatusBar('Due for Review', dueForReview, total, 'var(--warning)')}
        ${renderStatusBar('Pending HRBP', pendingHRBP, total, 'var(--purple)')}
        ${renderStatusBar('Completed', completed, total, 'var(--success)')}
        ${renderStatusBar('Extended', extended, total, 'var(--danger)')}
      </div>
    </div>
    <div class="card">
      <div class="card-header"><div class="card-title">Recent Activity</div><button class="btn btn-ghost btn-xs" onclick="navigate('candidates')">View All</button></div>
      <div class="card-body" style="padding:12px">
        ${recentActivity.length === 0 ? '<div class="empty-state" style="padding:24px"><p>No recent activity</p></div>' :
          recentActivity.map(h => {
            const c = DB.get('candidates').find(x => x.id === h.candidate_id);
            return `<div class="history-item ${h.new_status.toLowerCase().replace(/ /g,'')}">
              <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px">
                <span style="font-weight:600;font-size:13px">${c ? c.candidate_name : h.candidate_id}</span>
                <span style="font-size:11px;color:var(--text3)">${fmtDate(h.updated_at)}</span>
              </div>
              <div style="font-size:12px;color:var(--text3)">${h.previous_status} → <span style="color:var(--text2)">${h.new_status}</span></div>
              <div style="font-size:11px;color:var(--text3);margin-top:2px">by ${h.updated_by}</div>
            </div>`;
          }).join('')}
      </div>
    </div>
  </div>

  <div style="margin-top:16px" class="card">
    <div class="card-header"><div class="card-title">Upcoming Probation Completions</div><span style="font-size:12px;color:var(--text3)">Next 30 days</span></div>
    <div class="card-body" style="padding:0">
      ${renderUpcomingTable()}
    </div>
  </div>`;
}

function renderStatusBar(label, val, total, color) {
  const pct = total > 0 ? Math.round(val/total*100) : 0;
  return `<div style="margin-bottom:12px">
    <div style="display:flex;justify-content:space-between;font-size:12px;margin-bottom:4px">
      <span style="color:var(--text2)">${label}</span>
      <span style="font-family:var(--font-mono);color:var(--text3)">${val} (${pct}%)</span>
    </div>
    <div class="progress-bar"><div class="progress-fill" style="width:${pct}%;background:${color}"></div></div>
  </div>`;
}

function renderUpcomingTable() {
  const today = new Date();
  const in30 = new Date(); in30.setDate(in30.getDate() + 30);
  const candidates = DB.get('candidates').filter(c => {
    const end = new Date(c.probation_end_date);
    return end >= today && end <= in30 && c.probation_status === 'Under Probation';
  }).sort((a,b) => new Date(a.probation_end_date) - new Date(b.probation_end_date));

  if (!candidates.length) return '<div class="empty-state" style="padding:24px"><div class="empty-icon">📅</div><p>No upcoming completions in next 30 days</p></div>';
  return `<table><thead><tr><th>Candidate</th><th>Department</th><th>HRBP</th><th>End Date</th><th>Days Left</th></tr></thead><tbody>
    ${candidates.map(c => {
      const days = daysBetween(today.toISOString().split('T')[0], c.probation_end_date);
      const cls = days <= 7 ? 'days-overdue' : days <= 14 ? 'days-soon' : 'days-ok';
      return `<tr><td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id}</div></td>
        <td>${c.department_name}</td><td>${c.hrbp_name}</td>
        <td class="td-mono">${fmtDate(c.probation_end_date)}</td>
        <td><span class="days-count ${cls}">${days}d</span></td></tr>`;
    }).join('')}
  </tbody></table>`;
}

// =========================================================
// CREATE CANDIDATE
// =========================================================
function renderCreate(prefill={}) {
  const depts = DB.get('departments', []);
  const locs = DB.get('locations', []);
  const users = DB.get('users', []);
  const hrbps = users.filter(u => u.role === 'HRBP');
  const recruiters = users.filter(u => u.role === 'Recruiter');

  return `
  <div class="card" style="max-width:900px">
    <div class="card-header">
      <div class="card-title">New Joiner / Probation Record</div>
      <div class="status-flow">
        <div class="flow-step" style="background:rgba(79,124,255,.12);color:var(--accent);border-color:rgba(79,124,255,.3)">Under Probation</div>
        <div class="flow-arrow">→</div><div class="flow-step" style="background:rgba(245,166,35,.1);color:var(--warning);border-color:rgba(245,166,35,.3)">Due</div>
        <div class="flow-arrow">→</div><div class="flow-step" style="background:rgba(155,109,255,.1);color:var(--purple);border-color:rgba(155,109,255,.3)">Pending</div>
        <div class="flow-arrow">→</div><div class="flow-step" style="background:rgba(34,201,122,.1);color:var(--success);border-color:rgba(34,201,122,.3)">Done</div>
      </div>
    </div>
    <div class="card-body">
      <form id="createForm" onsubmit="submitCreate(event)">
        <div style="margin-bottom:20px">
          <div style="font-size:12px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:12px">👤 Candidate Information</div>
          <div class="form-grid">
            <div class="form-group"><label class="required">Candidate Name</label><input type="text" name="candidate_name" required placeholder="Full name" value="${prefill.candidate_name||''}"></div>
            <div class="form-group"><label class="required">Employee / Candidate ID</label><input type="text" name="candidate_id" required placeholder="EMP001" value="${prefill.candidate_id||''}"><div class="form-hint">Must be unique</div></div>
            <div class="form-group"><label class="required">Email Address</label><input type="email" name="email_address" required placeholder="candidate@company.com" value="${prefill.email_address||''}"></div>
            <div class="form-group"><label class="required">Candidate Source</label>
              <select name="candidate_source" required>
                <option value="">Select source</option>
                <option value="LinkedIn">LinkedIn</option>
                <option value="Referral">Referral</option>
                <option value="Naukri">Naukri</option>
                <option value="Campus">Campus</option>
                <option value="Agency">Agency</option>
                <option value="Walk-in">Walk-in</option>
                <option value="Internal">Internal Transfer</option>
              </select></div>
            <div class="form-group"><label class="required">Department</label>
              <select name="department_name" required>
                <option value="">Select department</option>
                ${depts.map(d => `<option value="${d}">${d}</option>`).join('')}
              </select></div>
            <div class="form-group"><label class="required">Joining Location</label>
              <select name="joining_location" required>
                <option value="">Select location</option>
                ${locs.map(l => `<option value="${l}">${l}</option>`).join('')}
              </select></div>
            <div class="form-group"><label class="required">Date of Joining</label><input type="date" name="date_of_joining" required onchange="calcDates(this)" value="${prefill.date_of_joining||''}"></div>
            <div class="form-group"><label>Probation Start Date</label><input type="text" name="probation_start_date" readonly class="auto-field" placeholder="Auto-calculated" id="probStart"></div>
            <div class="form-group"><label>Probation End Date</label><input type="text" name="probation_end_date_disp" readonly class="auto-field" placeholder="Auto-calculated" id="probEnd"><input type="hidden" name="probation_end_date"></div>
          </div>
        </div>

        <div class="divider"></div>
        <div style="margin-bottom:20px">
          <div style="font-size:12px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:12px">🤝 Referrer Information</div>
          <div class="form-grid">
            <div class="form-group"><label>Referrer Name</label><input type="text" name="referrer_name" placeholder="Leave blank if not a referral" value="${prefill.referrer_name||''}"></div>
            <div class="form-group"><label>Referrer Email</label><input type="email" name="referrer_email" placeholder="referrer@email.com" value="${prefill.referrer_email||''}"></div>
          </div>
        </div>

        <div class="divider"></div>
        <div style="margin-bottom:20px">
          <div style="font-size:12px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:12px">🧑‍💼 Assigned Team</div>
          <div class="form-grid">
            <div class="form-group"><label class="required">Recruiter Name</label>
              <select name="recruiter_name" required onchange="fillRecruiterEmail(this)">
                <option value="">Select recruiter</option>
                ${recruiters.map(r => `<option value="${r.user_name}">${r.user_name}</option>`).join('')}
                <option value="__other__">Other (Enter manually)</option>
              </select></div>
            <div class="form-group"><label class="required">Recruiter Email</label><input type="email" name="recruiter_email" required id="recruiterEmail" placeholder="recruiter@company.com" value="${prefill.recruiter_email||''}"></div>
            <div class="form-group"><label class="required">HRBP Name</label>
              <select name="hrbp_name" required onchange="fillHRBPEmail(this)">
                <option value="">Select HRBP</option>
                ${hrbps.map(h => `<option value="${h.user_name}">${h.user_name}</option>`).join('')}
                <option value="__other__">Other (Enter manually)</option>
              </select></div>
            <div class="form-group"><label class="required">HRBP Email</label><input type="email" name="hrbp_email" required id="hrbpEmail" placeholder="hrbp@company.com" value="${prefill.hrbp_email||''}"></div>
          </div>
        </div>

        <div class="divider"></div>
        <div style="display:flex;gap:10px;justify-content:flex-end">
          <button type="button" class="btn btn-ghost" onclick="navigate('candidates')">Cancel</button>
          <button type="submit" class="btn btn-primary">✓ Create Record</button>
        </div>
      </form>
    </div>
  </div>`;
}

function calcDates(input) {
  const doj = input.value;
  if (!doj) return;
  const start = new Date(doj);
  const end = new Date(doj); end.setDate(end.getDate() + 180);
  document.getElementById('probStart').value = fmtDate(doj);
  document.getElementById('probEnd').value = fmtDate(end.toISOString().split('T')[0]);
  document.querySelector('[name="probation_end_date"]').value = end.toISOString().split('T')[0];
}

function fillRecruiterEmail(sel) {
  const users = DB.get('users');
  const u = users.find(x => x.user_name === sel.value);
  document.getElementById('recruiterEmail').value = u ? u.email : '';
  document.getElementById('recruiterEmail').readOnly = !!u;
}
function fillHRBPEmail(sel) {
  const users = DB.get('users');
  const u = users.find(x => x.user_name === sel.value);
  document.getElementById('hrbpEmail').value = u ? u.email : '';
  document.getElementById('hrbpEmail').readOnly = !!u;
}

function submitCreate(e) {
  e.preventDefault();
  const fd = new FormData(e.target);
  const data = Object.fromEntries(fd.entries());

  // Validation
  if (!data.probation_end_date) { toast('Please enter a valid Date of Joining to auto-calculate probation dates.', 'error'); return; }

  const candidates = DB.get('candidates');
  if (candidates.find(c => c.candidate_id === data.candidate_id)) {
    toast(`Employee ID "${data.candidate_id}" already exists. Use a unique ID.`, 'error'); return;
  }

  const today = new Date().toISOString().split('T')[0];
  const newCandidate = {
    id: 'C' + (candidates.length + 1).toString().padStart(3,'0'),
    candidate_id: data.candidate_id,
    candidate_name: data.candidate_name,
    candidate_source: data.candidate_source,
    email_address: data.email_address,
    referrer_name: data.referrer_name || '',
    referrer_email: data.referrer_email || '',
    recruiter_name: data.recruiter_name,
    recruiter_email: data.recruiter_email,
    hrbp_name: data.hrbp_name,
    hrbp_email: data.hrbp_email,
    department_name: data.department_name,
    date_of_joining: data.date_of_joining,
    joining_location: data.joining_location,
    probation_start_date: data.date_of_joining,
    probation_end_date: data.probation_end_date,
    probation_status: 'Under Probation',
    notification_status: 'Not Triggered',
    extended_till_date: '', extension_reason: '', remarks: '',
    recruiter_notified: false, referrer_notified: false,
    created_at: today, created_by: 'Admin User',
    updated_at: today, updated_by: 'Admin User'
  };
  candidates.push(newCandidate);
  DB.set('candidates', candidates);

  // Add status history
  const history = DB.get('status_history');
  history.push({ id: uid(), candidate_id: newCandidate.id, previous_status: '', new_status: 'Under Probation', remarks: 'Record created', updated_by: 'Admin User', updated_at: today });
  DB.set('status_history', history);

  toast(`✅ Record created for ${data.candidate_name}. Probation ends on ${fmtDate(data.probation_end_date)}.`, 'success');
  updateBadges();
  navigate('candidates');
}

// =========================================================
// CANDIDATE LIST
// =========================================================
function renderCandidates(filter={}) {
  let candidates = DB.get('candidates');

  return `
  <div class="filter-bar">
    <input type="text" class="search-input" placeholder="🔍 Search by name or ID..." oninput="filterCandidates()" id="searchInput" style="max-width:260px">
    <select onchange="filterCandidates()" id="fStatus">
      <option value="">All Status</option>
      <option>Under Probation</option><option>Due for Review</option>
      <option>Pending HRBP Confirmation</option><option>Completed</option><option>Extended</option>
    </select>
    <select onchange="filterCandidates()" id="fDept">
      <option value="">All Departments</option>
      ${[...new Set(candidates.map(c=>c.department_name))].map(d => `<option>${d}</option>`).join('')}
    </select>
    <select onchange="filterCandidates()" id="fSource">
      <option value="">All Sources</option>
      ${[...new Set(candidates.map(c=>c.candidate_source))].map(s => `<option>${s}</option>`).join('')}
    </select>
    <select onchange="filterCandidates()" id="fLocation">
      <option value="">All Locations</option>
      ${[...new Set(candidates.map(c=>c.joining_location))].map(l => `<option>${l}</option>`).join('')}
    </select>
    <button class="btn btn-ghost btn-sm" onclick="exportCSV()">⬇ Export CSV</button>
  </div>
  <div id="candidateTable">${renderCandidateTable(candidates)}</div>`;
}

function filterCandidates() {
  let candidates = DB.get('candidates');
  const q = document.getElementById('searchInput')?.value.toLowerCase() || '';
  const st = document.getElementById('fStatus')?.value || '';
  const dept = document.getElementById('fDept')?.value || '';
  const src = document.getElementById('fSource')?.value || '';
  const loc = document.getElementById('fLocation')?.value || '';
  if (q) candidates = candidates.filter(c => c.candidate_name.toLowerCase().includes(q) || c.candidate_id.toLowerCase().includes(q));
  if (st) candidates = candidates.filter(c => c.probation_status === st);
  if (dept) candidates = candidates.filter(c => c.department_name === dept);
  if (src) candidates = candidates.filter(c => c.candidate_source === src);
  if (loc) candidates = candidates.filter(c => c.joining_location === loc);
  document.getElementById('candidateTable').innerHTML = renderCandidateTable(candidates);
}

function renderCandidateTable(candidates) {
  if (!candidates.length) return '<div class="empty-state"><div class="empty-icon">🔍</div><p>No records found. Adjust filters or add a new candidate.</p></div>';
  const today = new Date().toISOString().split('T')[0];
  return `<div class="table-wrap"><table>
    <thead><tr><th>Candidate</th><th>Source</th><th>Department</th><th>Recruiter</th><th>HRBP</th><th>DOJ</th><th>End Date</th><th>Status</th><th>Actions</th></tr></thead>
    <tbody>${candidates.map(c => {
      const daysLeft = daysBetween(today, c.probation_end_date);
      const cls = daysLeft < 0 ? 'days-overdue' : daysLeft <= 14 ? 'days-soon' : 'days-ok';
      return `<tr>
        <td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id} · ${c.joining_location}</div></td>
        <td><span class="chip">${c.candidate_source}</span></td>
        <td>${c.department_name}</td>
        <td><div>${c.recruiter_name}</div><div class="td-sub">${c.recruiter_email}</div></td>
        <td><div>${c.hrbp_name}</div><div class="td-sub">${c.hrbp_email}</div></td>
        <td class="td-mono">${fmtDate(c.date_of_joining)}</td>
        <td><div class="td-mono">${fmtDate(c.probation_end_date)}</div><div class="td-sub days-count ${cls}">${daysLeft > 0 ? daysLeft+'d left' : daysLeft === 0 ? 'Today!' : Math.abs(daysLeft)+'d ago'}</div></td>
        <td>${statusBadge(c.probation_status)}</td>
        <td><div class="action-row">
          <button class="btn btn-ghost btn-xs" onclick="viewCandidate('${c.id}')">View</button>
          ${(c.probation_status === 'Pending HRBP Confirmation' || c.probation_status === 'Due for Review') && (currentRole === 'HRBP' || currentRole === 'Admin') ? `<button class="btn btn-xs" style="background:rgba(155,109,255,.15);color:var(--purple);border:1px solid rgba(155,109,255,.25)" onclick="updateStatusModal('${c.id}')">Update</button>` : ''}
        </div></td>
      </tr>`;
    }).join('')}
    </tbody></table></div>`;
}

function statusBadge(status) {
  const map = {
    'Under Probation': 'badge-active',
    'Due for Review': 'badge-due',
    'Pending HRBP Confirmation': 'badge-pending',
    'Completed': 'badge-completed',
    'Extended': 'badge-extended'
  };
  return `<span class="badge ${map[status]||'badge-active'}">${status}</span>`;
}

// =========================================================
// VIEW CANDIDATE DETAIL
// =========================================================
function viewCandidate(id) {
  const c = DB.get('candidates').find(x => x.id === id);
  if (!c) return;
  const history = DB.get('status_history').filter(h => h.candidate_id === id).reverse();
  const notifs = DB.get('notifications').filter(n => n.candidate_id === id);
  const today = new Date().toISOString().split('T')[0];
  const daysLeft = daysBetween(today, c.probation_end_date);

  const canUpdate = (c.probation_status === 'Pending HRBP Confirmation' || c.probation_status === 'Due for Review') && (currentRole === 'HRBP' || currentRole === 'Admin');

  openModal(`
  <div class="modal-header">
    <div>
      <div class="modal-title">${c.candidate_name}</div>
      <div style="font-size:12px;color:var(--text3);margin-top:2px">${c.candidate_id} · ${c.department_name} · ${c.joining_location}</div>
    </div>
    <button class="btn-close" onclick="closeModal()">✕</button>
  </div>
  <div class="modal-body">
    <div class="tab-bar">
      <div class="tab active" onclick="switchTab(event,'det-profile')">Profile</div>
      <div class="tab" onclick="switchTab(event,'det-history')">Status History</div>
      <div class="tab" onclick="switchTab(event,'det-notifs')">Notifications</div>
    </div>

    <div id="det-profile">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
        <div>
          <div style="font-size:11px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:8px">Candidate Info</div>
          <div class="info-row"><span class="info-label">Status</span><span class="info-value">${statusBadge(c.probation_status)}</span></div>
          <div class="info-row"><span class="info-label">Date of Joining</span><span class="info-value td-mono">${fmtDate(c.date_of_joining)}</span></div>
          <div class="info-row"><span class="info-label">Probation Start</span><span class="info-value td-mono">${fmtDate(c.probation_start_date)}</span></div>
          <div class="info-row"><span class="info-label">Probation End</span><span class="info-value td-mono">${fmtDate(c.probation_end_date)}</span></div>
          <div class="info-row"><span class="info-label">Days Remaining</span><span class="info-value"><span class="days-count ${daysLeft<0?'days-overdue':daysLeft<=14?'days-soon':'days-ok'}">${daysLeft > 0 ? daysLeft+' days' : daysLeft === 0 ? 'Today!' : Math.abs(daysLeft)+' days overdue'}</span></span></div>
          <div class="info-row"><span class="info-label">Source</span><span class="info-value"><span class="chip">${c.candidate_source}</span></span></div>
          <div class="info-row"><span class="info-label">Email</span><span class="info-value">${c.email_address}</span></div>
        </div>
        <div>
          <div style="font-size:11px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:8px">Team Assignment</div>
          <div class="info-row"><span class="info-label">Recruiter</span><span class="info-value">${c.recruiter_name}</span></div>
          <div class="info-row"><span class="info-label">Recruiter Email</span><span class="info-value">${c.recruiter_email}</span></div>
          <div class="info-row"><span class="info-label">HRBP</span><span class="info-value">${c.hrbp_name}</span></div>
          <div class="info-row"><span class="info-label">HRBP Email</span><span class="info-value">${c.hrbp_email}</span></div>
          <div class="info-row"><span class="info-label">Referrer</span><span class="info-value">${c.referrer_name || '—'}</span></div>
          <div class="info-row"><span class="info-label">Referrer Email</span><span class="info-value">${c.referrer_email || '—'}</span></div>
          ${c.probation_status === 'Extended' ? `
          <div class="info-row"><span class="info-label">Extended Till</span><span class="info-value td-mono">${fmtDate(c.extended_till_date)}</span></div>
          <div class="info-row"><span class="info-label">Extension Reason</span><span class="info-value">${c.extension_reason}</span></div>
          <div class="info-row"><span class="info-label">Remarks</span><span class="info-value">${c.remarks}</span></div>` : ''}
        </div>
      </div>
      <div class="divider"></div>
      <div style="font-size:11px;color:var(--text3)">Created by ${c.created_by} on ${fmtDateTime(c.created_at)} · Last updated by ${c.updated_by} on ${fmtDateTime(c.updated_at)}</div>
    </div>

    <div id="det-history" style="display:none">
      ${history.length === 0 ? '<div class="empty-state"><p>No status history yet</p></div>' :
        history.map(h => `
        <div class="history-item ${h.new_status.toLowerCase().replace(/ /g,'')}">
          <div style="display:flex;justify-content:space-between;margin-bottom:4px">
            <span style="font-weight:600">${h.new_status}</span>
            <span style="font-size:11px;color:var(--text3);font-family:var(--font-mono)">${fmtDateTime(h.updated_at)}</span>
          </div>
          ${h.previous_status ? `<div style="font-size:12px;color:var(--text3)">From: ${h.previous_status}</div>` : ''}
          ${h.remarks ? `<div style="font-size:12px;margin-top:4px">${h.remarks}</div>` : ''}
          <div style="font-size:11px;color:var(--text3);margin-top:4px">by ${h.updated_by}</div>
        </div>`).join('')}
    </div>

    <div id="det-notifs" style="display:none">
      ${notifs.length === 0 ? '<div class="empty-state"><p>No notifications sent yet</p></div>' :
        notifs.map(n => `
        <div style="padding:12px;background:var(--surface2);border-radius:var(--radius2);margin-bottom:8px">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px">
            <span class="notification-type notification-${n.notification_type.toLowerCase().includes('hrbp')?'hrbp':n.notification_type.toLowerCase().includes('recruiter')?'recruiter':'referrer'}">${n.notification_type}</span>
            <span class="badge badge-${n.sent_status.toLowerCase()}">${n.sent_status}</span>
          </div>
          <div style="font-size:13px;font-weight:500;margin-bottom:2px">${n.subject}</div>
          <div style="font-size:12px;color:var(--text3)">To: ${n.recipient_email} ${n.cc_email ? '· CC: '+n.cc_email : ''}</div>
          <div style="font-size:11px;color:var(--text3);margin-top:4px">${fmtDateTime(n.sent_at)} · by ${n.triggered_by}</div>
          ${n.error_message ? `<div style="font-size:12px;color:var(--danger);margin-top:4px">⚠ ${n.error_message}</div>` : ''}
        </div>`).join('')}
    </div>
  </div>
  <div class="modal-footer">
    ${canUpdate ? `<button class="btn btn-primary" onclick="closeModal();updateStatusModal('${c.id}')">Update Probation Status</button>` : ''}
    <button class="btn btn-ghost" onclick="closeModal()">Close</button>
  </div>`, 'modal-lg');
}

function switchTab(e, targetId) {
  const tabs = e.target.closest('.tab-bar').querySelectorAll('.tab');
  tabs.forEach(t => t.classList.remove('active'));
  e.target.classList.add('active');
  const modal = e.target.closest('.modal');
  modal.querySelectorAll('[id^="det-"]').forEach(el => el.style.display = 'none');
  document.getElementById(targetId).style.display = '';
}

// =========================================================
// UPDATE STATUS MODAL
// =========================================================
function updateStatusModal(id) {
  const c = DB.get('candidates').find(x => x.id === id);
  if (!c) return;
  openModal(`
  <div class="modal-header">
    <div>
      <div class="modal-title">Update Probation Status</div>
      <div style="font-size:12px;color:var(--text3);margin-top:2px">${c.candidate_name} · ${c.candidate_id}</div>
    </div>
    <button class="btn-close" onclick="closeModal()">✕</button>
  </div>
  <div class="modal-body">
    <div class="alert alert-info">📋 Current Status: ${statusBadge(c.probation_status)}</div>
    <form id="statusUpdateForm">
      <div class="form-grid" style="gap:14px">
        <div class="form-group full">
          <label class="required">New Probation Status</label>
          <select name="new_status" required onchange="toggleExtendFields(this)">
            <option value="">Select status</option>
            <option value="Completed">✅ Completed</option>
            <option value="Extended">🔄 Extended</option>
          </select>
        </div>
        <div id="extendFields" style="display:none;grid-column:1/-1">
          <div class="form-grid">
            <div class="form-group">
              <label class="required">Revised Probation End Date</label>
              <input type="date" name="extended_till_date" id="extDate">
            </div>
            <div class="form-group">
              <label class="required">Extension Reason</label>
              <select name="extension_reason">
                <option value="">Select reason</option>
                <option>Performance concerns</option>
                <option>Attendance issues</option>
                <option>Skill gap</option>
                <option>Behavioural concerns</option>
                <option>Project completion pending</option>
                <option>Other</option>
              </select>
            </div>
          </div>
        </div>
        <div class="form-group full">
          <label>HRBP Remarks</label>
          <textarea name="remarks" rows="3" placeholder="Add remarks or observations..."></textarea>
        </div>
        <div class="form-group full">
          <label>Updated By (HRBP Name)</label>
          <input type="text" name="updated_by" value="${c.hrbp_name}" placeholder="Your name">
        </div>
      </div>
    </form>
  </div>
  <div class="modal-footer">
    <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
    <button class="btn btn-primary" onclick="submitStatusUpdate('${id}')">Save & Notify</button>
  </div>`, 'modal-sm');
}

function toggleExtendFields(sel) {
  document.getElementById('extendFields').style.display = sel.value === 'Extended' ? '' : 'none';
  if (sel.value === 'Extended') {
    document.querySelector('[name="extended_till_date"]').required = true;
    document.querySelector('[name="extension_reason"]').required = true;
  } else {
    document.querySelector('[name="extended_till_date"]').required = false;
    document.querySelector('[name="extension_reason"]').required = false;
  }
}

function submitStatusUpdate(candidateId) {
  const form = document.getElementById('statusUpdateForm');
  const fd = new FormData(form);
  const data = Object.fromEntries(fd.entries());

  if (!data.new_status) { toast('Please select a status.', 'error'); return; }
  if (data.new_status === 'Extended') {
    if (!data.extended_till_date) { toast('Revised end date is required for extension.', 'error'); return; }
    if (!data.extension_reason) { toast('Extension reason is required.', 'error'); return; }
  }

  const candidates = DB.get('candidates');
  const idx = candidates.findIndex(c => c.id === candidateId);
  if (idx === -1) return;
  const prev = candidates[idx].probation_status;
  const today = new Date().toISOString().split('T')[0];
  const updatedBy = data.updated_by || candidates[idx].hrbp_name;

  candidates[idx].probation_status = data.new_status;
  candidates[idx].remarks = data.remarks;
  candidates[idx].updated_at = today;
  candidates[idx].updated_by = updatedBy;

  if (data.new_status === 'Extended') {
    candidates[idx].extended_till_date = data.extended_till_date;
    candidates[idx].extension_reason = data.extension_reason;
  }
  if (data.new_status === 'Completed') {
    candidates[idx].completed_date = today;
  }
  DB.set('candidates', candidates);

  // Add history
  const history = DB.get('status_history');
  history.push({ id: uid(), candidate_id: candidateId, previous_status: prev, new_status: data.new_status, remarks: data.remarks, updated_by: updatedBy, updated_at: today });
  DB.set('status_history', history);

  // Send recruiter notification
  sendNotification({
    candidate_id: candidateId,
    notification_type: 'Recruiter Update',
    recipient_name: candidates[idx].recruiter_name,
    recipient_email: candidates[idx].recruiter_email,
    cc_email: '',
    subject: `Probation Status Updated for ${candidates[idx].candidate_name}`,
    message_body: `Hi ${candidates[idx].recruiter_name},\n\nThe probation status for ${candidates[idx].candidate_name} has been updated by HRBP as ${data.new_status}. Please check the Probation Tracker for further details.`,
    triggered_by: updatedBy
  });
  candidates[idx].recruiter_notified = true;

  // Send referrer notification if completed and referrer exists
  if (data.new_status === 'Completed' && candidates[idx].referrer_email) {
    sendNotification({
      candidate_id: candidateId,
      notification_type: 'Referrer Email',
      recipient_name: candidates[idx].referrer_name,
      recipient_email: candidates[idx].referrer_email,
      cc_email: candidates[idx].recruiter_email,
      subject: `Referral Claim Form Submission for ${candidates[idx].candidate_name}`,
      message_body: `Hi ${candidates[idx].referrer_name},\n\nThanks for referring ${candidates[idx].candidate_name} to our organization. Your referral has successfully completed the probation period. Kindly revert back to the recruiter with the updated claim form to process your referral bonus.\n\nCC: ${candidates[idx].recruiter_email}`,
      triggered_by: 'System'
    });
    candidates[idx].referrer_notified = true;
  }
  DB.set('candidates', candidates);

  closeModal();
  toast(`Status updated to ${data.new_status}. Notifications sent.`, 'success');
  updateBadges();
  renderPage();
}

// =========================================================
// PENDING HRBP ACTION
// =========================================================
function renderPending() {
  const candidates = DB.get('candidates').filter(c =>
    c.probation_status === 'Pending HRBP Confirmation' || c.probation_status === 'Due for Review'
  );
  if (!candidates.length) return `<div class="empty-state" style="margin-top:60px"><div class="empty-icon">🎉</div><p style="font-size:15px;font-weight:600;color:var(--text)">All caught up!</p><p style="margin-top:6px">No pending HRBP actions at this time.</p></div>`;

  if (currentRole === 'Recruiter') {
    return `<div class="alert alert-warning">⚠ You have read-only access to this view. Only HRBPs and Admins can update probation status.</div>
    <div class="table-wrap"><table>
      <thead><tr><th>Candidate</th><th>Department</th><th>HRBP</th><th>End Date</th><th>Status</th><th>Reminder</th></tr></thead>
      <tbody>${candidates.map(c => `<tr>
        <td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id}</div></td>
        <td>${c.department_name}</td><td>${c.hrbp_name}</td>
        <td class="td-mono">${fmtDate(c.probation_end_date)}</td>
        <td>${statusBadge(c.probation_status)}</td>
        <td><span class="badge badge-${c.notification_status==='Sent'?'sent':'notrigger'}">${c.notification_status}</span></td>
      </tr>`).join('')}
      </tbody></table></div>`;
  }

  return `
  <div class="alert alert-warning">⏳ ${candidates.length} record${candidates.length>1?'s':''} require${candidates.length===1?'s':''} HRBP review. Please update the status for each candidate.</div>
  <div class="table-wrap"><table>
    <thead><tr><th>Candidate</th><th>Recruiter</th><th>HRBP</th><th>Probation End</th><th>Overdue By</th><th>Status</th><th>Reminder</th><th>Actions</th></tr></thead>
    <tbody>${candidates.map(c => {
      const today = new Date().toISOString().split('T')[0];
      const overdue = daysBetween(c.probation_end_date, today);
      const notif = DB.get('notifications').find(n => n.candidate_id === c.id && n.notification_type === 'HRBP Reminder');
      return `<tr>
        <td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id} · ${c.department_name}</div></td>
        <td><div>${c.recruiter_name}</div><div class="td-sub">${c.recruiter_email}</div></td>
        <td><div>${c.hrbp_name}</div><div class="td-sub">${c.hrbp_email}</div></td>
        <td class="td-mono">${fmtDate(c.probation_end_date)}</td>
        <td><span class="days-count ${overdue>0?'days-overdue':'days-ok'}">${overdue > 0 ? overdue+'d overdue' : 'Today'}</span></td>
        <td>${statusBadge(c.probation_status)}</td>
        <td>${notif ? `<span class="badge badge-${notif.sent_status.toLowerCase()}">${notif.sent_status}</span><div style="font-size:11px;color:var(--text3)">${fmtDate(notif.sent_at)}</div>` : '<span class="badge badge-notrigger">Not Sent</span>'}</td>
        <td><div class="action-row">
          <button class="btn btn-xs" style="background:rgba(155,109,255,.15);color:var(--purple);border:1px solid rgba(155,109,255,.25)" onclick="updateStatusModal('${c.id}')">Update Status</button>
          <button class="btn btn-ghost btn-xs" onclick="resendHRBPReminder('${c.id}')">Resend</button>
        </div></td>
      </tr>`;
    }).join('')}
    </tbody></table></div>`;
}

function resendHRBPReminder(candidateId) {
  const c = DB.get('candidates').find(x => x.id === candidateId);
  if (!c) return;
  sendNotification({
    candidate_id: candidateId,
    notification_type: 'HRBP Reminder',
    recipient_name: c.hrbp_name,
    recipient_email: c.hrbp_email,
    cc_email: '',
    subject: `Probation Review Required for ${c.candidate_name}`,
    message_body: `Hi ${c.hrbp_name},\n\n${c.candidate_name} has completed 180 days of probation. Kindly review and update the probation status as Completed or Extended in the Probation Tracker system.`,
    triggered_by: 'User'
  });
  toast(`HRBP reminder resent to ${c.hrbp_email}`, 'info');
}

// =========================================================
// COMPLETED PROBATION
// =========================================================
function renderCompleted() {
  const candidates = DB.get('candidates').filter(c => c.probation_status === 'Completed');
  if (!candidates.length) return '<div class="empty-state"><div class="empty-icon">✅</div><p>No completed probation records yet.</p></div>';
  const notifications = DB.get('notifications');
  return `<div class="table-wrap"><table>
    <thead><tr><th>Candidate</th><th>Department</th><th>Recruiter</th><th>DOJ</th><th>Probation End</th><th>Completed On</th><th>Recruiter Notified</th><th>Referrer Notified</th><th></th></tr></thead>
    <tbody>${candidates.map(c => {
      const rn = notifications.find(n => n.candidate_id === c.id && n.notification_type === 'Recruiter Update');
      const rfn = notifications.find(n => n.candidate_id === c.id && n.notification_type === 'Referrer Email');
      return `<tr>
        <td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id}</div></td>
        <td>${c.department_name}</td>
        <td>${c.recruiter_name}</td>
        <td class="td-mono">${fmtDate(c.date_of_joining)}</td>
        <td class="td-mono">${fmtDate(c.probation_end_date)}</td>
        <td class="td-mono">${fmtDate(c.completed_date||c.updated_at)}</td>
        <td>${rn ? `<span class="badge badge-${rn.sent_status.toLowerCase()}">${rn.sent_status}</span>` : '<span class="badge badge-notrigger">Not Sent</span>'}</td>
        <td>${c.referrer_email ? (rfn ? `<span class="badge badge-${rfn.sent_status.toLowerCase()}">${rfn.sent_status}</span>` : '<span class="badge badge-notrigger">N/A</span>') : '<span style="color:var(--text3);font-size:12px">No Referral</span>'}</td>
        <td><button class="btn btn-ghost btn-xs" onclick="viewCandidate('${c.id}')">View</button></td>
      </tr>`;
    }).join('')}
    </tbody></table></div>`;
}

// =========================================================
// EXTENDED PROBATION
// =========================================================
function renderExtended() {
  const candidates = DB.get('candidates').filter(c => c.probation_status === 'Extended');
  if (!candidates.length) return '<div class="empty-state"><div class="empty-icon">📅</div><p>No extended probation records.</p></div>';
  const notifications = DB.get('notifications');
  return `<div class="table-wrap"><table>
    <thead><tr><th>Candidate</th><th>Department</th><th>HRBP</th><th>Original End</th><th>Revised End</th><th>Extension Reason</th><th>Remarks</th><th>Recruiter Notified</th><th></th></tr></thead>
    <tbody>${candidates.map(c => {
      const rn = notifications.find(n => n.candidate_id === c.id && n.notification_type === 'Recruiter Update');
      return `<tr>
        <td><div class="td-name">${c.candidate_name}</div><div class="td-sub">${c.candidate_id}</div></td>
        <td>${c.department_name}</td>
        <td>${c.hrbp_name}</td>
        <td class="td-mono">${fmtDate(c.probation_end_date)}</td>
        <td class="td-mono" style="color:var(--warning)">${fmtDate(c.extended_till_date)}</td>
        <td><span class="chip">${c.extension_reason||'—'}</span></td>
        <td style="max-width:180px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;color:var(--text2)">${c.remarks||'—'}</td>
        <td>${rn ? `<span class="badge badge-${rn.sent_status.toLowerCase()}">${rn.sent_status}</span>` : '<span class="badge badge-notrigger">Not Sent</span>'}</td>
        <td><button class="btn btn-ghost btn-xs" onclick="viewCandidate('${c.id}')">View</button></td>
      </tr>`;
    }).join('')}
    </tbody></table></div>`;
}

// =========================================================
// NOTIFICATION LOG
// =========================================================
function renderNotifications() {
  let notifs = DB.get('notifications').reverse();
  const candidates = DB.get('candidates');

  return `
  <div class="filter-bar">
    <input type="text" placeholder="🔍 Search by candidate or email..." oninput="filterNotifs()" id="nSearch" style="max-width:260px">
    <select onchange="filterNotifs()" id="nType">
      <option value="">All Types</option>
      <option>HRBP Reminder</option><option>Recruiter Update</option><option>Referrer Email</option>
    </select>
    <select onchange="filterNotifs()" id="nStatus">
      <option value="">All Status</option>
      <option>Sent</option><option>Failed</option><option>Pending</option>
    </select>
    <button class="btn btn-ghost btn-sm" onclick="retryFailed()">🔁 Retry Failed</button>
  </div>
  <div id="notifTable">${renderNotifTable(notifs, candidates)}</div>`;
}

function filterNotifs() {
  let notifs = DB.get('notifications').reverse();
  const candidates = DB.get('candidates');
  const q = document.getElementById('nSearch')?.value.toLowerCase()||'';
  const t = document.getElementById('nType')?.value||'';
  const s = document.getElementById('nStatus')?.value||'';
  if (q) notifs = notifs.filter(n => {
    const c = candidates.find(x => x.id === n.candidate_id);
    return (c && c.candidate_name.toLowerCase().includes(q)) || n.recipient_email.toLowerCase().includes(q);
  });
  if (t) notifs = notifs.filter(n => n.notification_type === t);
  if (s) notifs = notifs.filter(n => n.sent_status === s);
  document.getElementById('notifTable').innerHTML = renderNotifTable(notifs, candidates);
}

function renderNotifTable(notifs, candidates) {
  if (!notifs.length) return '<div class="empty-state"><div class="empty-icon">🔔</div><p>No notifications found.</p></div>';
  return `<div class="table-wrap"><table>
    <thead><tr><th>Candidate</th><th>Type</th><th>Recipient</th><th>CC</th><th>Subject</th><th>Sent At</th><th>Status</th><th>Triggered By</th><th></th></tr></thead>
    <tbody>${notifs.map(n => {
      const c = candidates.find(x => x.id === n.candidate_id);
      const typeClass = n.notification_type.includes('HRBP') ? 'hrbp' : n.notification_type.includes('Recruiter') ? 'recruiter' : 'referrer';
      return `<tr>
        <td><div class="td-name">${c ? c.candidate_name : n.candidate_id}</div></td>
        <td><span class="notification-type notification-${typeClass}">${n.notification_type}</span></td>
        <td><div>${n.recipient_name}</div><div class="td-sub">${n.recipient_email}</div></td>
        <td style="font-size:12px;color:var(--text3)">${n.cc_email||'—'}</td>
        <td style="max-width:200px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:12px">${n.subject}</td>
        <td class="td-mono" style="font-size:11px">${fmtDateTime(n.sent_at)}</td>
        <td><span class="badge badge-${n.sent_status.toLowerCase()}">${n.sent_status}</span>${n.error_message?`<div style="font-size:11px;color:var(--danger)">${n.error_message}</div>`:''}</td>
        <td><span class="chip">${n.triggered_by}</span></td>
        <td>${n.sent_status === 'Failed' ? `<button class="btn btn-ghost btn-xs" onclick="retrySingleNotif('${n.id}')">Retry</button>` : ''}</td>
      </tr>`;
    }).join('')}
    </tbody></table></div>`;
}

function retryFailed() {
  const notifs = DB.get('notifications');
  let count = 0;
  notifs.forEach(n => {
    if (n.sent_status === 'Failed') {
      n.sent_status = 'Sent';
      n.error_message = '';
      n.sent_at = new Date().toISOString().split('T')[0];
      count++;
    }
  });
  DB.set('notifications', notifs);
  toast(`${count} failed notification${count!==1?'s':''} retried successfully.`, 'success');
  renderPage();
}

function retrySingleNotif(nid) {
  const notifs = DB.get('notifications');
  const n = notifs.find(x => x.id === nid);
  if (n) { n.sent_status = 'Sent'; n.error_message = ''; n.sent_at = new Date().toISOString().split('T')[0]; }
  DB.set('notifications', notifs);
  toast('Notification retried successfully.', 'success');
  renderPage();
}

// =========================================================
// ADMIN SETTINGS
// =========================================================
function renderSettings() {
  if (currentRole !== 'Admin') return '<div class="alert alert-warning" style="margin:0">⚠ Admin access required to view this page.</div>';

  const users = DB.get('users');
  const templates = DB.get('email_templates');
  const depts = DB.get('departments', []);
  const locs = DB.get('locations', []);

  return `
  <div class="tab-bar" id="settingsTabBar">
    <div class="tab active" onclick="switchSettingsTab(event,'st-users')">👥 Users</div>
    <div class="tab" onclick="switchSettingsTab(event,'st-templates')">✉ Email Templates</div>
    <div class="tab" onclick="switchSettingsTab(event,'st-masters')">📋 Masters</div>
  </div>

  <div id="st-users">
    <div class="section-header">
      <div class="section-title">User Management</div>
      <button class="btn btn-primary btn-sm" onclick="addUserModal()">+ Add User</button>
    </div>
    <div class="table-wrap"><table>
      <thead><tr><th>Name</th><th>Email</th><th>Role</th><th>Department</th><th>Location</th><th>Status</th><th>Actions</th></tr></thead>
      <tbody>${users.map(u => `<tr>
        <td><div class="td-name">${u.user_name}</div></td>
        <td style="font-size:12px">${u.email}</td>
        <td>${statusBadge2(u.role)}</td>
        <td>${u.department}</td>
        <td>${u.location}</td>
        <td><span class="badge ${u.active_flag ? 'badge-completed' : 'badge-extended'}">${u.active_flag ? 'Active' : 'Inactive'}</span></td>
        <td><div class="action-row">
          <button class="btn btn-ghost btn-xs" onclick="toggleUserStatus('${u.id}')">Toggle</button>
        </div></td>
      </tr>`).join('')}
      </tbody></table></div>
  </div>

  <div id="st-templates" style="display:none">
    <div class="section-title" style="margin-bottom:16px">Email Templates</div>
    ${templates.map(t => `
    <div class="card" style="margin-bottom:12px">
      <div class="card-header">
        <div><div class="card-title">${t.template_name}</div><div style="font-size:12px;color:var(--text3);margin-top:2px">Last updated by ${t.updated_by}</div></div>
        <span class="badge ${t.is_active ? 'badge-completed' : 'badge-extended'}">${t.is_active ? 'Active' : 'Inactive'}</span>
      </div>
      <div class="card-body">
        <div style="margin-bottom:8px"><span style="font-size:11px;color:var(--text3);font-weight:700">SUBJECT:</span> <span style="font-size:13px">${t.subject}</span></div>
        <div style="background:var(--surface2);border-radius:var(--radius2);padding:12px;font-size:12px;white-space:pre-wrap;color:var(--text2);font-family:var(--font-mono)">${t.body}</div>
      </div>
    </div>`).join('')}
  </div>

  <div id="st-masters" style="display:none">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
      <div class="card">
        <div class="card-header"><div class="card-title">Departments</div><button class="btn btn-ghost btn-xs" onclick="addMaster('dept')">+ Add</button></div>
        <div class="card-body" style="padding:12px">
          ${depts.map(d => `<div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);font-size:13px"><span>${d}</span><button class="btn btn-ghost btn-xs" onclick="removeMaster('dept','${d}')">×</button></div>`).join('')}
        </div>
      </div>
      <div class="card">
        <div class="card-header"><div class="card-title">Locations</div><button class="btn btn-ghost btn-xs" onclick="addMaster('loc')">+ Add</button></div>
        <div class="card-body" style="padding:12px">
          ${locs.map(l => `<div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);font-size:13px"><span>${l}</span><button class="btn btn-ghost btn-xs" onclick="removeMaster('loc','${l}')">×</button></div>`).join('')}
        </div>
      </div>
    </div>
  </div>`;
}

function statusBadge2(role) {
  const map = { Admin: 'badge-pending', Recruiter: 'badge-active', HRBP: 'badge-due' };
  return `<span class="badge ${map[role]||'badge-active'}">${role}</span>`;
}

function switchSettingsTab(e, targetId) {
  document.querySelectorAll('#settingsTabBar .tab').forEach(t => t.classList.remove('active'));
  e.target.classList.add('active');
  ['st-users','st-templates','st-masters'].forEach(id => {
    const el = document.getElementById(id);
    if (el) el.style.display = id === targetId ? '' : 'none';
  });
}

function toggleUserStatus(uid) {
  const users = DB.get('users');
  const u = users.find(x => x.id === uid);
  if (u) u.active_flag = !u.active_flag;
  DB.set('users', users);
  toast(`User ${u.user_name} is now ${u.active_flag ? 'Active' : 'Inactive'}.`, 'info');
  renderPage();
}

function addUserModal() {
  const depts = DB.get('departments', []);
  const locs = DB.get('locations', []);
  openModal(`
  <div class="modal-header"><div class="modal-title">Add New User</div><button class="btn-close" onclick="closeModal()">✕</button></div>
  <div class="modal-body">
    <form id="addUserForm">
      <div class="form-grid">
        <div class="form-group"><label class="required">Name</label><input type="text" name="user_name" required></div>
        <div class="form-group"><label class="required">Email</label><input type="email" name="email" required></div>
        <div class="form-group"><label class="required">Role</label><select name="role" required><option value="">Select</option><option>Admin</option><option>Recruiter</option><option>HRBP</option></select></div>
        <div class="form-group"><label>Department</label><select name="department"><option value="">Select</option>${depts.map(d=>`<option>${d}</option>`).join('')}</select></div>
        <div class="form-group"><label>Location</label><select name="location"><option value="">Select</option>${locs.map(l=>`<option>${l}</option>`).join('')}</select></div>
      </div>
    </form>
  </div>
  <div class="modal-footer">
    <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
    <button class="btn btn-primary" onclick="submitAddUser()">Add User</button>
  </div>`, 'modal-sm');
}

function submitAddUser() {
  const form = document.getElementById('addUserForm');
  const fd = new FormData(form);
  const data = Object.fromEntries(fd.entries());
  if (!data.user_name || !data.email || !data.role) { toast('Name, email, and role are required.', 'error'); return; }
  const users = DB.get('users');
  users.push({ id: uid(), user_name: data.user_name, email: data.email, role: data.role, department: data.department, location: data.location, active_flag: true, created_at: new Date().toISOString().split('T')[0] });
  DB.set('users', users);
  closeModal();
  toast('User added successfully.', 'success');
  renderPage();
}

function addMaster(type) {
  const label = type === 'dept' ? 'Department' : 'Location';
  openModal(`
  <div class="modal-header"><div class="modal-title">Add ${label}</div><button class="btn-close" onclick="closeModal()">✕</button></div>
  <div class="modal-body">
    <div class="form-group"><label class="required">${label} Name</label><input type="text" id="masterInput" placeholder="Enter ${label.toLowerCase()}..."></div>
  </div>
  <div class="modal-footer">
    <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
    <button class="btn btn-primary" onclick="saveMaster('${type}')">Save</button>
  </div>`, 'modal-sm');
}

function saveMaster(type) {
  const val = document.getElementById('masterInput').value.trim();
  if (!val) { toast('Please enter a value.', 'error'); return; }
  const key = type === 'dept' ? 'departments' : 'locations';
  const list = DB.get(key, []);
  if (list.includes(val)) { toast('Already exists.', 'error'); return; }
  list.push(val);
  DB.set(key, list);
  closeModal();
  toast(`${val} added.`, 'success');
  renderPage();
}

function removeMaster(type, val) {
  const key = type === 'dept' ? 'departments' : 'locations';
  const list = DB.get(key, []).filter(x => x !== val);
  DB.set(key, list);
  toast(`${val} removed.`, 'info');
  renderPage();
}

// =========================================================
// DAILY CHECK / SCHEDULER
// =========================================================
function runDailyCheck() {
  const today = new Date().toISOString().split('T')[0];
  const candidates = DB.get('candidates');
  let updated = 0, reminders = 0;

  candidates.forEach(c => {
    if (c.probation_status !== 'Under Probation' && c.probation_status !== 'Due for Review') return;
    const end = c.probation_end_date;
    const days = daysBetween(today, end);

    if (days <= 0 && c.probation_status === 'Under Probation') {
      c.probation_status = 'Due for Review';
      c.updated_at = today;
      c.updated_by = 'System';
      const history = DB.get('status_history');
      history.push({ id: uid(), candidate_id: c.id, previous_status: 'Under Probation', new_status: 'Due for Review', remarks: 'Auto-updated by daily scheduler', updated_by: 'System', updated_at: today });
      DB.set('status_history', history);
      updated++;
    }

    if (days <= 0 && c.probation_status === 'Due for Review' && c.notification_status !== 'Sent') {
      sendNotification({
        candidate_id: c.id,
        notification_type: 'HRBP Reminder',
        recipient_name: c.hrbp_name,
        recipient_email: c.hrbp_email,
        cc_email: '',
        subject: `Probation Review Required for ${c.candidate_name}`,
        message_body: `Hi ${c.hrbp_name},\n\n${c.candidate_name} has completed 180 days of probation. Kindly review and update the probation status.`,
        triggered_by: 'System'
      });
      c.notification_status = 'Sent';
      c.probation_status = 'Pending HRBP Confirmation';
      c.updated_at = today;
      c.updated_by = 'System';
      const history = DB.get('status_history');
      history.push({ id: uid(), candidate_id: c.id, previous_status: 'Due for Review', new_status: 'Pending HRBP Confirmation', remarks: 'HRBP reminder triggered by scheduler', updated_by: 'System', updated_at: today });
      DB.set('status_history', history);
      reminders++;
    }
  });

  DB.set('candidates', candidates);
  updateBadges();
  toast(`Daily check complete. ${updated} status updates, ${reminders} reminders sent.`, 'success');
  if (currentPage === 'dashboard' || currentPage === 'pending') renderPage();
}

// =========================================================
// NOTIFICATIONS
// =========================================================
function sendNotification(params) {
  const notifs = DB.get('notifications');
  const isFail = Math.random() < 0.05; // 5% chance of simulated failure
  notifs.push({
    id: uid(),
    candidate_id: params.candidate_id,
    notification_type: params.notification_type,
    recipient_name: params.recipient_name,
    recipient_email: params.recipient_email,
    cc_email: params.cc_email || '',
    subject: params.subject,
    message_body: params.message_body,
    sent_status: isFail ? 'Failed' : 'Sent',
    error_message: isFail ? 'SMTP timeout' : '',
    sent_at: new Date().toISOString().split('T')[0],
    triggered_by: params.triggered_by || 'System'
  });
  DB.set('notifications', notifs);
}

// =========================================================
// EXPORT
// =========================================================
function exportCSV() {
  const candidates = DB.get('candidates');
  const headers = ['Candidate ID','Name','Source','Email','Department','Location','Date of Joining','Probation Start','Probation End','Status','Recruiter','HRBP','Referrer'];
  const rows = candidates.map(c => [c.candidate_id,c.candidate_name,c.candidate_source,c.email_address,c.department_name,c.joining_location,c.date_of_joining,c.probation_start_date,c.probation_end_date,c.probation_status,c.recruiter_name,c.hrbp_name,c.referrer_name||'']);
  const csv = [headers, ...rows].map(r => r.map(v => `"${v}"`).join(',')).join('\n');
  const blob = new Blob([csv], {type:'text/csv'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'probation_tracker_export.csv';
  a.click();
  toast('CSV exported successfully.', 'success');
}

// =========================================================
// MODAL
// =========================================================
function openModal(html, cls='') {
  const container = document.getElementById('modal-container');
  container.innerHTML = `<div class="modal-overlay" onclick="handleOverlayClick(event)"><div class="modal ${cls}">${html}</div></div>`;
}
function closeModal() { document.getElementById('modal-container').innerHTML = ''; }
function handleOverlayClick(e) { if (e.target.classList.contains('modal-overlay')) closeModal(); }

// =========================================================
// TOAST
// =========================================================
function toast(msg, type='info') {
  const icons = {success:'✅', error:'❌', info:'ℹ️', warning:'⚠️'};
  const container = document.getElementById('toast-container');
  const el = document.createElement('div');
  el.className = `toast ${type}`;
  el.innerHTML = `<span class="toast-icon">${icons[type]||'ℹ️'}</span><span class="toast-msg">${msg}</span>`;
  container.appendChild(el);
  setTimeout(() => { el.style.opacity='0'; el.style.transform='translateX(20px)'; el.style.transition='all .3s'; setTimeout(()=>el.remove(), 300); }, 4000);
}

// =========================================================
// ROLE SWITCH
// =========================================================
function changeRole(role) {
  currentRole = role;
  const initials = { Admin:'A', Recruiter:'R', HRBP:'H' };
  document.getElementById('userAvatarSidebar').textContent = initials[role] || 'U';
  toast(`Switched to ${role} view.`, 'info');
  renderPage();
}

// =========================================================
// INIT
// =========================================================
seedData();
updateBadges();
renderPage();

// Auto-run daily check on load
setTimeout(() => {
  runDailyCheck();
}, 500);
</script>
</body>
</html>
