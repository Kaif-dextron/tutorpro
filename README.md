[index.html](https://github.com/user-attachments/files/30399590/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#1a365d">
    <meta name="apple-mobile-web-app-title" content="TutorPro">
    <meta name="author" content="Mr Kaif">
    <meta name="developer" content="Mr Kaif - kaifalam522@gmail.com">
    <meta name="copyright" content="Copyright © 2026 Mr Kaif. All rights reserved.">
    <meta name="description" content="Professional tutoring management with attendance tracking, automatic fee receipts, and UPI payment integration">
    <title>TutorPro v2.0 | © Mr Kaif</title>
    
    <style>
        :root {
            --primary: #1a365d;
            --primary-light: #2b6cb0;
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
            --info: #3b82f6;
            --purple: #8b5cf6;
            --orange: #f97316;
            --gray: #6b7280;
            --bg: #f1f5f9;
            --card: #ffffff;
            --text: #1e293b;
            --text-light: #64748b;
            --border: #e2e8f0;
            --radius: 16px;
            --shadow: 0 2px 8px rgba(0,0,0,0.06);
            --shadow-lg: 0 8px 24px rgba(0,0,0,0.10);
            --safe-bottom: env(safe-area-inset-bottom, 16px);
        }

        * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #e2e8f0;
            color: var(--text);
            min-height: 100vh;
            min-height: 100dvh;
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
            display: flex;
            justify-content: center;
        }

        .app-container {
            width: 100%;
            max-width: 480px;
            min-height: 100vh;
            min-height: 100dvh;
            background: var(--bg);
            position: relative;
            padding-bottom: 90px;
        }

        .app-header {
            background: var(--primary);
            color: white;
            padding: 14px 18px;
            padding-top: max(14px, env(safe-area-inset-top));
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }
        .app-header h1 { font-size: 19px; font-weight: 700; letter-spacing: -0.3px; }
        .header-actions { display:flex; gap:8px; }
        .icon-btn {
            background: rgba(255,255,255,0.12);
            border: none; color: white; width: 34px; height: 34px;
            border-radius: 50%; font-size: 16px; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
            transition: all 0.2s; position: relative;
        }
        .icon-btn:active { background: rgba(255,255,255,0.25); transform: scale(0.92); }
        .badge-dot {
            position: absolute; top: 4px; right: 4px;
            width: 8px; height: 8px; border-radius: 50%;
            background: var(--danger); border: 1.5px solid white;
        }

        .student-switcher {
            background: white; margin: 10px 14px; border-radius: var(--radius);
            padding: 12px 14px; box-shadow: var(--shadow);
            display: flex; align-items: center; gap: 10px; cursor: pointer;
            transition: all 0.2s; border: 2px solid transparent;
        }
        .student-switcher:active { transform: scale(0.98); background: #fafcfd; }
        .student-avatar {
            width: 42px; height: 42px; border-radius: 50%;
            background: var(--primary); color: white;
            display: flex; align-items: center; justify-content: center;
            font-weight: 700; font-size: 17px; flex-shrink: 0;
        }
        .student-info { flex:1; min-width:0; }
        .student-name-display { font-weight: 700; font-size: 14px; }
        .student-subtitle { font-size: 11px; color: var(--text-light); }
        .dropdown-arrow { color: var(--text-light); font-size: 12px; transition: transform 0.3s; }
        .dropdown-arrow.open { transform: rotate(180deg); }

        .summary-row {
            display: grid; grid-template-columns: 1fr 1fr 1fr;
            gap: 8px; margin: 0 14px 10px;
        }
        .summary-card {
            background: white; border-radius: 12px; padding: 12px 10px;
            text-align: center; box-shadow: var(--shadow);
            transition: transform 0.2s;
        }
        .summary-card:active { transform: scale(0.96); }
        .summary-card .s-value { font-size: 22px; font-weight: 800; color: var(--primary); }
        .summary-card .s-label { font-size: 10px; color: var(--text-light); font-weight: 600; text-transform: uppercase; margin-top: 2px; }
        .summary-card.pending-card { background: #fef3c7; }
        .summary-card.pending-card .s-value { color: #92400e; font-size: 15px; }

        .status-card {
            margin: 0 14px 10px; background: white;
            border-radius: var(--radius); padding: 14px; box-shadow: var(--shadow);
        }
        .today-status { display:flex; align-items:center; gap:12px; }
        .status-indicator {
            width: 50px; height: 50px; border-radius: 50%;
            display:flex; align-items:center; justify-content:center; font-size:24px; flex-shrink:0;
            transition: all 0.3s;
        }
        .status-indicator.working { background:#d1fae5; animation: pulse 2s infinite; }
        .status-indicator.leave { background:#fee2e2; }
        .status-indicator.pending { background:#fef3c7; }
        @keyframes pulse { 0%,100%{transform:scale(1);} 50%{transform:scale(1.05);} }
        .status-text h3 { font-size:15px; font-weight:700; }
        .status-text p { font-size:11px; color:var(--text-light); margin-top:1px; }
        .session-timer { font-size:20px; font-weight:700; color:var(--success); margin-top:3px; font-variant-numeric: tabular-nums; }

        .quick-actions {
            display: grid; grid-template-columns: 1fr 1fr;
            gap: 8px; margin: 0 14px 10px;
        }
        .action-btn {
            background: white; border: none; padding: 12px;
            border-radius: 12px; font-weight: 600; font-size: 12px;
            cursor: pointer; box-shadow: var(--shadow);
            display: flex; align-items: center; gap: 6px;
            transition: all 0.2s; color: var(--text);
        }
        .action-btn:active { transform: scale(0.96); box-shadow: var(--shadow-lg); }
        .action-btn .btn-icon { font-size: 20px; }
        .action-btn.check-in { background:#d1fae5; color:#065f46; }
        .action-btn.check-out { background:#fee2e2; color:#991b1b; }
        .action-btn.manual { background:#fef3c7; color:#92400e; }
        .action-btn.receipt { background:#dbeafe; color:#1e40af; }
        .action-btn.payments { background:#f3e8ff; color:#6b21a8; }

        .mini-calendar {
            margin: 0 14px 10px; background: white;
            border-radius: var(--radius); padding: 14px; box-shadow: var(--shadow);
        }
        .calendar-header { display:flex; justify-content:space-between; align-items:center; margin-bottom:10px; }
        .month-title { font-weight:700; font-size:15px; }
        .month-nav { display:flex; gap:4px; }
        .month-nav button {
            width:32px; height:32px; border-radius:50%;
            border:1px solid var(--border); background:white;
            cursor:pointer; font-size:13px; display:flex;
            align-items:center; justify-content:center; transition:all 0.2s;
        }
        .month-nav button:active { background:var(--bg); }
        .weekdays {
            display:grid; grid-template-columns:repeat(7,1fr);
            text-align:center; font-size:10px; font-weight:600;
            color:var(--text-light); margin-bottom:4px;
        }
        .days-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:2px; text-align:center; }
        .day-cell {
            aspect-ratio:1; display:flex; align-items:center; justify-content:center;
            border-radius:50%; font-size:12px; font-weight:500; cursor:pointer; 
            transition:all 0.15s; position:relative;
        }
        .day-cell:active { transform:scale(0.85); }
        .day-cell.today { border:2px solid var(--purple); font-weight:700; }
        .day-cell.working { background:#d1fae5; color:#065f46; font-weight:600; }
        .day-cell.leave { background:#fee2e2; color:#991b1b; }
        .day-cell.partial { background:#fef3c7; color:#92400e; }
        .day-cell.canceled { background:#ffedd5; color:#9a3412; }
        .day-cell.holiday { background:#dbeafe; color:#1e40af; }
        .day-cell.future { color:#cbd5e1; }
        .day-cell.other-student { opacity:0.3; }
        .legend { display:flex; flex-wrap:wrap; gap:6px; margin-top:8px; font-size:9px; }
        .legend-item { display:flex; align-items:center; gap:3px; }
        .legend-dot { width:8px; height:8px; border-radius:50%; flex-shrink:0; }

        .app-footer {
            text-align:center; padding:12px; padding-bottom:100px;
            font-size:9px; color:var(--text-light); border-top:1px solid var(--border);
            margin: 10px 14px 0;
        }
        .app-footer .copyright { font-weight:600; color:var(--text); }

        .bottom-nav {
            position:fixed; bottom:0; left:50%; transform:translateX(-50%);
            width:100%; max-width:480px; background:white;
            border-top:1px solid var(--border); display:flex;
            padding:6px 6px; padding-bottom:max(6px, var(--safe-bottom));
            z-index:100; box-shadow:0 -2px 8px rgba(0,0,0,0.04);
        }
        .nav-item {
            flex:1; display:flex; flex-direction:column; align-items:center;
            gap:2px; padding:5px; border:none; background:transparent;
            cursor:pointer; color:var(--text-light); font-size:9px;
            font-weight:500; transition:all 0.2s; border-radius:8px;
            position:relative;
        }
        .nav-item.active { color:var(--primary); background:#eff6ff; }
        .nav-item .nav-icon { font-size:20px; }
        .nav-item .nav-badge {
            position:absolute; top:2px; right:8px;
            background:var(--danger); color:white; font-size:9px;
            min-width:16px; height:16px; border-radius:8px;
            display:flex; align-items:center; justify-content:center;
            font-weight:700;
        }

        /* Modal Styles */
        .modal-overlay {
            display:none; position:fixed; inset:0;
            background:rgba(0,0,0,0.55); z-index:200;
            justify-content:center; align-items:flex-end;
            backdrop-filter:blur(3px); animation: fadeIn 0.2s;
        }
        @keyframes fadeIn { from{opacity:0;} to{opacity:1;} }
        .modal-overlay.active { display:flex; }
        .modal-sheet {
            background:white; width:100%; max-width:480px;
            max-height:88vh; border-radius:20px 20px 0 0;
            overflow-y:auto; animation:slideUp 0.3s cubic-bezier(0.16,1,0.3,1);
            padding:18px; padding-bottom:max(18px, var(--safe-bottom));
        }
        @keyframes slideUp { from{transform:translateY(100%);} to{transform:translateY(0);} }
        .modal-handle { width:36px; height:4px; background:#d1d5db; border-radius:2px; margin:0 auto 14px; }
        .modal-title { font-size:17px; font-weight:700; margin-bottom:14px; text-align:center; }

        .form-group { margin-bottom:12px; }
        .form-label { font-size:11px; font-weight:600; color:var(--text-light); text-transform:uppercase; letter-spacing:0.5px; margin-bottom:4px; display:block; }
        .form-input, .form-select {
            width:100%; padding:11px 13px; border:2px solid var(--border);
            border-radius:10px; font-size:14px; font-weight:500;
            background:#f8fafc; transition:all 0.2s; font-family:inherit; color:var(--text);
        }
        .form-input:focus, .form-select:focus { outline:none; border-color:var(--primary-light); background:white; box-shadow:0 0 0 3px rgba(43,108,176,0.1); }
        .form-hint { font-size:10px; color:var(--text-light); margin-top:3px; }

        .btn {
            width:100%; padding:13px; border:none; border-radius:12px;
            font-weight:700; font-size:14px; cursor:pointer;
            transition:all 0.2s; letter-spacing:0.2px;
        }
        .btn:active { transform:scale(0.97); }
        .btn-primary { background:var(--primary); color:white; }
        .btn-success { background:var(--success); color:white; }
        .btn-danger { background:var(--danger); color:white; }
        .btn-warning { background:var(--warning); color:#1e293b; }
        .btn-outline { background:white; border:2px solid var(--border); color:var(--text); }
        .btn-sm { padding:8px 14px; font-size:12px; width:auto; border-radius:8px; }
        .btn-xs { padding:5px 10px; font-size:10px; width:auto; border-radius:6px; }

        .upload-area {
            border:2px dashed var(--border); border-radius:12px;
            padding:20px; text-align:center; cursor:pointer;
            transition:all 0.2s; background:#fafcfd;
        }
        .upload-area:active { border-color:var(--primary-light); background:#f0f6ff; }
        .upload-preview { width:100%; max-height:120px; object-fit:contain; border-radius:8px; margin-top:8px; }
        .upload-preview.signature { max-height:60px; }

        /* Student Card with Actions */
        .student-card {
            background:white; border-radius:12px; padding:12px 14px; margin-bottom:6px;
            box-shadow:var(--shadow); display:flex; align-items:center; gap:10px;
            cursor:pointer; transition:all 0.2s; border:2px solid transparent;
        }
        .student-card:active { transform:scale(0.98); }
        .student-card.active { border-color:var(--primary); background:#eff6ff; }
        .student-card-actions { display:flex; gap:4px; flex-shrink:0; }
        .student-card-actions button {
            width:30px; height:30px; border-radius:50%; border:none;
            cursor:pointer; font-size:13px; transition:all 0.2s;
            display:flex; align-items:center; justify-content:center;
        }
        .btn-edit { background:#dbeafe; color:#1e40af; }
        .btn-delete { background:#fee2e2; color:#991b1b; }
        .btn-edit:active { background:#bfdbfe; }
        .btn-delete:active { background:#fecaca; }

        /* Confirm Dialog */
        .confirm-dialog {
            background:white; border-radius:16px; padding:20px; text-align:center;
            max-width:340px; margin:auto;
        }
        .confirm-dialog h3 { margin-bottom:8px; }
        .confirm-dialog p { font-size:13px; color:var(--text-light); margin-bottom:16px; }
        .confirm-dialog .btn-row { display:flex; gap:8px; }

        /* Receipt & Tracker Items */
        .receipt-item {
            background:white; border-radius:12px; padding:12px 14px; margin-bottom:8px;
            box-shadow:var(--shadow); cursor:pointer; transition:all 0.2s;
            display:flex; align-items:center; gap:10px;
        }
        .receipt-item:active { transform:scale(0.98); }
        .receipt-dot { width:10px; height:10px; border-radius:50%; flex-shrink:0; }
        .receipt-dot.paid { background:var(--success); }
        .receipt-dot.unpaid { background:var(--danger); }
        .receipt-info { flex:1; min-width:0; }
        .receipt-info .r-id { font-weight:700; font-size:13px; }
        .receipt-info .r-detail { font-size:11px; color:var(--text-light); }
        .receipt-amount { font-weight:700; font-size:14px; text-align:right; white-space:nowrap; }

        .filter-bar { display:flex; gap:6px; margin-bottom:10px; flex-wrap:wrap; }
        .filter-chip {
            padding:6px 12px; border-radius:20px; font-size:11px;
            font-weight:600; border:1px solid var(--border);
            background:white; cursor:pointer; transition:all 0.2s;
        }
        .filter-chip.active { background:var(--primary); color:white; border-color:var(--primary); }

        .tracker-student-card {
            background:white; border-radius:12px; padding:14px; margin-bottom:10px;
            box-shadow:var(--shadow);
        }
        .tracker-student-card .ts-header {
            display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;
        }
        .tracker-item {
            display:flex; align-items:center; gap:8px; padding:8px 0;
            border-bottom:1px solid var(--border); font-size:12px;
        }
        .tracker-item:last-child { border-bottom:none; }

        .rate-override-active { border-color:var(--warning) !important; background:#fffdf5 !important; }
        
        .storage-bar {
            height:4px; background:#e2e8f0; border-radius:2px; margin-top:4px; overflow:hidden;
        }
        .storage-bar-fill { height:100%; background:var(--success); border-radius:2px; transition:width 0.5s; }
        .storage-bar-fill.warning { background:var(--warning); }
        .storage-bar-fill.danger { background:var(--danger); }

        .toast {
            position:fixed; bottom:100px; left:50%; transform:translateX(-50%);
            background:#1e293b; color:white; padding:11px 20px;
            border-radius:30px; font-size:12px; font-weight:600;
            z-index:300; opacity:0; pointer-events:none;
            transition:opacity 0.3s; box-shadow:var(--shadow-lg); white-space:nowrap;
        }
        .toast.show { opacity:1; }
        .toast.undo { background:#1e293b; cursor:pointer; pointer-events:all; }
        .toast.undo:active { background:#374151; }

        .empty-state {
            text-align:center; padding:40px 20px; color:var(--text-light);
        }
        .empty-state .empty-icon { font-size:48px; margin-bottom:12px; }

        @media print {
            body { background:white; }
            .app-header,.bottom-nav,.quick-actions,.status-card,
            .student-switcher,.mini-calendar,.toast,.modal-overlay,
            .app-footer,.summary-row,.filter-bar,.no-print { display:none !important; }
            .app-container { max-width:100%; padding:0; }
        }
    </style>
</head>
<body>

<div class="app-container" id="app">
    <header class="app-header">
        <h1>📚 TutorPro</h1>
        <div class="header-actions">
            <button class="icon-btn" onclick="showTutorProfile()" title="Profile">👤</button>
            <button class="icon-btn" onclick="showSettings()" title="Settings">⚙️</button>
        </div>
    </header>

    <div class="student-switcher" onclick="showStudentSwitcher()">
        <div class="student-avatar" id="currentAvatar">R</div>
        <div class="student-info">
            <div class="student-name-display" id="currentStudentName">Rahul Sharma</div>
            <div class="student-subtitle" id="currentStudentDetails">10th Standard • Math, Science</div>
        </div>
        <span class="dropdown-arrow" id="dropdownArrow">▼</span>
    </div>

    <div class="summary-row no-print" id="summaryRow">
        <div class="summary-card"><div class="s-value" id="sumWorking">0</div><div class="s-label">Working</div></div>
        <div class="summary-card"><div class="s-value" id="sumLeaves">0</div><div class="s-label">Leaves</div></div>
        <div class="summary-card"><div class="s-value" id="sumEarning">₹0</div><div class="s-label">This Month</div></div>
    </div>

    <div class="summary-row no-print" id="pendingAlert" style="display:none;">
        <div class="summary-card pending-card" style="grid-column:1/-1;" onclick="showPaymentTracker()">
            <div class="s-value" id="pendingCount">⚠️ 0 Pending</div>
            <div class="s-label">Tap to view Payment Tracker</div>
        </div>
    </div>

    <div class="status-card" id="statusCard">
        <div class="today-status">
            <div class="status-indicator pending" id="statusIndicator">⏳</div>
            <div class="status-text">
                <h3 id="statusTitle">No Session Yet</h3>
                <p id="statusSubtitle">Today's status for <span id="statusStudentName">student</span></p>
                <div class="session-timer" id="sessionTimer" style="display:none;"></div>
            </div>
        </div>
    </div>

    <div class="quick-actions no-print">
        <button class="action-btn check-in" onclick="manualCheckIn()"><span class="btn-icon">📍</span> Check In</button>
        <button class="action-btn check-out" onclick="manualCheckOut()"><span class="btn-icon">🚪</span> Check Out</button>
        <button class="action-btn manual" onclick="showDayOverride()"><span class="btn-icon">✏️</span> Override</button>
        <button class="action-btn receipt" onclick="showReceiptGenerator()"><span class="btn-icon">🧾</span> Receipt</button>
        <button class="action-btn payments" onclick="showPaymentTracker()" style="grid-column:1/-1;"><span class="btn-icon">💳</span> Payment Tracker</button>
    </div>

    <div class="mini-calendar">
        <div class="calendar-header">
            <span class="month-title" id="monthTitle">Loading...</span>
            <div class="month-nav">
                <button onclick="changeMonth(-1)">◀</button>
                <button onclick="goToToday()">Today</button>
                <button onclick="changeMonth(1)">▶</button>
            </div>
        </div>
        <div class="weekdays"><span>Sun</span><span>Mon</span><span>Tue</span><span>Wed</span><span>Thu</span><span>Fri</span><span>Sat</span></div>
        <div class="days-grid" id="daysGrid"></div>
        <div class="legend">
            <div class="legend-item"><div class="legend-dot" style="background:#d1fae5;"></div> Working</div>
            <div class="legend-item"><div class="legend-dot" style="background:#fee2e2;"></div> Leave</div>
            <div class="legend-item"><div class="legend-dot" style="background:#fef3c7;"></div> Partial</div>
            <div class="legend-item"><div class="legend-dot" style="background:#ffedd5;"></div> Canceled</div>
            <div class="legend-item"><div class="legend-dot" style="background:#dbeafe;"></div> Holiday</div>
        </div>
    </div>

    <div class="app-footer no-print">
        <div class="copyright">© 2026 TutorPro v2.0 | Developed by Mr Kaif</div>
        <div style="font-size:8px;">📧 kaifalam522@gmail.com | 📱 +91 9142840785</div>
    </div>

    <nav class="bottom-nav no-print">
        <button class="nav-item active" onclick="switchTab('home')"><span class="nav-icon">🏠</span>Home</button>
        <button class="nav-item" onclick="switchTab('calendar')"><span class="nav-icon">📅</span>Calendar</button>
        <button class="nav-item" onclick="switchTab('receipts')"><span class="nav-icon">🧾</span>Receipts</button>
        <button class="nav-item" id="paymentsNav" onclick="switchTab('payments')"><span class="nav-icon">💳</span>Payments</button>
        <button class="nav-item" onclick="switchTab('students')"><span class="nav-icon">👥</span>Students</button>
    </nav>
</div>

<div class="toast" id="toast"></div>

<!-- All Modals are dynamically generated by JS for cleaner code -->
<div id="modalContainer"></div>
<input type="file" id="importFile" accept=".json" style="display:none;" onchange="importData(event)">

<script>
/*
 * ============================================
 * TutorPro v2.0 - Advanced Tutoring Manager
 * Developer: Mr Kaif
 * Email: kaifalam522@gmail.com
 * Phone: +91 9142840785
 * Copyright © 2026 Mr Kaif. All Rights Reserved.
 * ============================================
 */

// ==================== APP STATE ====================
const APP = {
    tutorProfile: {
        name: 'Mr Kaif', businessName: 'Smart Education Services',
        email: 'kaifalam522@gmail.com', phone: '+91 9142840785',
        upiId: '9142840785@airtel', logo: null, signature: null,
    },
    students: [],
    currentStudentId: null,
    currentMonth: new Date().getMonth(),
    currentYear: new Date().getFullYear(),
    settings: { minSessionTime: 15, geofenceRadius: 150, defaultHourlyRate: 200, defaultSessionMins: 90 },
    activeSession: null, // { studentId, startTime }
    sessionHistory: {},  // { 'YYYY-MM-DD': { studentId, entries, status, note } }
    receipts: [],
    paymentFilter: 'all',
    receiptRateOverride: null,
    undoTimeout: null,
};

// ==================== DATA PERSISTENCE ====================
function loadData() {
    try {
        const saved = localStorage.getItem('tutorpro_v5_data');
        if (saved) {
            const data = JSON.parse(saved);
            if (data.tutorProfile) APP.tutorProfile = { ...APP.tutorProfile, ...data.tutorProfile };
            if (data.students) APP.students = data.students;
            if (data.currentStudentId) APP.currentStudentId = data.currentStudentId;
            if (data.settings) APP.settings = { ...APP.settings, ...data.settings };
            if (data.sessionHistory) APP.sessionHistory = data.sessionHistory;
            if (data.receipts) APP.receipts = data.receipts;
        }
    } catch(e) {
        localStorage.removeItem('tutorpro_v5_data');
    }
    if (APP.students.length === 0) {
        APP.students.push({
            id: 's1', name: 'Rahul Sharma', class: '10th Standard',
            subjects: 'Mathematics, Science', sessionMins: 90, hourlyRate: 200,
            parentName: 'Mr. Amit Sharma', parentPhone: '+91 9876543210',
            parentEmail: 'amit.sharma@email.com', location: null,
        });
    }
    if (!APP.currentStudentId || !APP.students.find(s => s.id === APP.currentStudentId)) {
        APP.currentStudentId = APP.students[0]?.id || null;
    }
    if (!APP.tutorProfile.logo) APP.tutorProfile.logo = generateDefaultLogo();
}

function saveData() {
    try {
        const json = JSON.stringify({
            tutorProfile: APP.tutorProfile, students: APP.students,
            currentStudentId: APP.currentStudentId, settings: APP.settings,
            sessionHistory: APP.sessionHistory, receipts: APP.receipts,
        });
        if (new Blob([json]).size > 4.5 * 1024 * 1024) {
            compressImage(APP.tutorProfile.logo, 0.4, (c) => { APP.tutorProfile.logo = c; saveData(); });
            return false;
        }
        localStorage.setItem('tutorpro_v5_data', json);
        return true;
    } catch(e) { return false; }
}

function compressImage(base64, quality, callback) {
    if (!base64 || base64.length < 500) { callback(base64); return; }
    const img = new Image();
    img.onload = () => {
        const canvas = document.createElement('canvas');
        const maxW = 400;
        if (img.width > maxW) { canvas.width = maxW; canvas.height = (img.height / img.width) * maxW; }
        else { canvas.width = img.width; canvas.height = img.height; }
        canvas.getContext('2d').drawImage(img, 0, 0, canvas.width, canvas.height);
        callback(canvas.toDataURL('image/jpeg', quality));
    };
    img.src = base64;
}

function generateDefaultLogo() {
    const canvas = document.createElement('canvas');
    canvas.width = 200; canvas.height = 80;
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = '#1a365d'; ctx.beginPath(); ctx.roundRect(10, 10, 180, 60, 12); ctx.fill();
    ctx.fillStyle = '#ffffff'; ctx.font = 'bold 22px sans-serif'; ctx.textAlign = 'center';
    ctx.fillText('📚 TutorPro', 100, 48);
    return canvas.toDataURL('image/png');
}

// ==================== HELPERS ====================
function getStudent(id) { return APP.students.find(s => s.id === id) || null; }
function getCurrentStudent() { return getStudent(APP.currentStudentId); }
function getTodayKey() { const d = new Date(); return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`; }

// ✅ FIXED: Filter by current student
function getDayStatus(dateKey) {
    const e = APP.sessionHistory[dateKey];
    if (!e) return 'future';
    if (e.studentId !== APP.currentStudentId) return 'other-student';
    return e.status || 'pending';
}

function getTotalMinutes(dateKey) {
    const e = APP.sessionHistory[dateKey];
    if (!e || e.studentId !== APP.currentStudentId || !e.entries) return 0;
    return e.entries.reduce((s, en) => s + (en.out ? (new Date(en.out) - new Date(en.in)) / 60000 : 0), 0);
}

function getCalculatedPerSessionRate() {
    const s = getCurrentStudent();
    if (!s) return APP.settings.defaultHourlyRate * (APP.settings.defaultSessionMins / 60);
    return s.hourlyRate * (s.sessionMins / 60);
}

function showToast(msg, isUndo = false, undoCallback = null) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.className = 'toast show' + (isUndo ? ' undo' : '');
    t.onclick = isUndo ? undoCallback : null;
    if (APP.undoTimeout) clearTimeout(APP.undoTimeout);
    APP.undoTimeout = setTimeout(() => { t.classList.remove('show'); t.onclick = null; }, isUndo ? 5000 : 2500);
}

// ==================== SESSION MANAGEMENT ====================
function manualCheckIn() {
    const s = getCurrentStudent();
    if (!s) return showToast('⚠️ Please add a student first');
    
    // Auto-checkout from previous student if any
    if (APP.activeSession && APP.activeSession.studentId !== APP.currentStudentId) {
        autoCheckoutPrevious();
    }
    
    const tk = getTodayKey();
    if (!APP.sessionHistory[tk]) {
        APP.sessionHistory[tk] = { studentId: APP.currentStudentId, entries: [], status: 'pending', note: '' };
    } else if (APP.sessionHistory[tk].studentId !== APP.currentStudentId) {
        // Another student has session today - create new entry for current student
        // Actually, let's allow multiple students on same day
        if (!APP.sessionHistory[tk + '_' + APP.currentStudentId]) {
            const newKey = tk + '_' + APP.currentStudentId;
            APP.sessionHistory[newKey] = { studentId: APP.currentStudentId, entries: [], status: 'pending', note: '' };
        }
    }
    
    const entryKey = (APP.sessionHistory[tk]?.studentId === APP.currentStudentId) ? tk : (tk + '_' + APP.currentStudentId);
    if (!APP.sessionHistory[entryKey]) {
        APP.sessionHistory[entryKey] = { studentId: APP.currentStudentId, entries: [], status: 'pending', note: '' };
    }
    
    APP.sessionHistory[entryKey].entries.push({ in: new Date().toISOString(), out: null });
    APP.activeSession = { studentId: APP.currentStudentId, startTime: new Date().toISOString(), entryKey: entryKey };
    updateDayStatus(entryKey);
    saveData();
    refreshUI();
    showToast('✅ Checked in at ' + new Date().toLocaleTimeString([], {hour:'2-digit',minute:'2-digit'}));
}

function autoCheckoutPrevious() {
    if (!APP.activeSession) return;
    const entryKey = APP.activeSession.entryKey;
    if (entryKey && APP.sessionHistory[entryKey]) {
        const lastEntry = APP.sessionHistory[entryKey].entries[APP.sessionHistory[entryKey].entries.length - 1];
        if (lastEntry && !lastEntry.out) {
            lastEntry.out = new Date().toISOString();
            updateDayStatus(entryKey);
        }
    }
    APP.activeSession = null;
}

function manualCheckOut() {
    if (!APP.activeSession) return showToast('⚠️ No active session');
    const entryKey = APP.activeSession.entryKey;
    if (!entryKey || !APP.sessionHistory[entryKey]) return showToast('⚠️ Session data missing');
    
    const lastEntry = APP.sessionHistory[entryKey].entries[APP.sessionHistory[entryKey].entries.length - 1];
    if (lastEntry.out) return showToast('⚠️ Already checked out');
    
    lastEntry.out = new Date().toISOString();
    updateDayStatus(entryKey);
    const mins = Math.round((new Date(lastEntry.out) - new Date(lastEntry.in)) / 60000);
    APP.activeSession = null;
    saveData();
    refreshUI();
    showToast(`🚪 Checked out • ${mins} minutes`);
}

function updateDayStatus(dateKey) {
    const e = APP.sessionHistory[dateKey];
    if (!e) return;
    const mins = getTotalMinutes(dateKey);
    if (mins >= APP.settings.minSessionTime) e.status = 'working';
    else if (mins > 0) e.status = 'partial';
    else if (e.entries.length > 0 && e.entries.some(en => en.out)) e.status = 'partial';
    else e.status = 'pending';
}

// ==================== CALENDAR (STUDENT-SPECIFIC) ====================
function renderCalendar() {
    const grid = document.getElementById('daysGrid');
    const months = ['January','February','March','April','May','June','July','August','September','October','November','December'];
    document.getElementById('monthTitle').textContent = `${months[APP.currentMonth]} ${APP.currentYear}`;
    
    const firstDay = new Date(APP.currentYear, APP.currentMonth, 1).getDay();
    const daysInMonth = new Date(APP.currentYear, APP.currentMonth + 1, 0).getDate();
    const today = new Date();
    const todayKey = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
    
    let h = '';
    for (let i = 0; i < firstDay; i++) h += '<div class="day-cell"></div>';
    
    for (let d = 1; d <= daysInMonth; d++) {
        const dk = `${APP.currentYear}-${String(APP.currentMonth+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
        const st = getDayStatus(dk);
        const isToday = dk === todayKey;
        
        let cls = 'day-cell';
        if (isToday) cls += ' today';
        
        // ✅ FIXED: Color based on current student's attendance only
        if (st === 'working') cls += ' working';
        else if (st === 'leave') cls += ' leave';
        else if (st === 'partial') cls += ' partial';
        else if (st === 'canceled') cls += ' canceled';
        else if (st === 'holiday') cls += ' holiday';
        else if (st === 'other-student') cls += ' other-student';
        else if (st === 'future' && dk > todayKey) cls += ' future';
        else if (dk <= todayKey) cls += ' leave';
        
        h += `<div class="${cls}" onclick="showDayDetail('${dk}')">${d}</div>`;
    }
    
    grid.innerHTML = h;
    updateSummaryCards();
    updatePendingAlert();
    updatePaymentsBadge();
}

function changeMonth(d) {
    APP.currentMonth += d;
    if (APP.currentMonth > 11) { APP.currentMonth = 0; APP.currentYear++; }
    if (APP.currentMonth < 0) { APP.currentMonth = 11; APP.currentYear--; }
    renderCalendar();
}

function goToToday() {
    APP.currentMonth = new Date().getMonth();
    APP.currentYear = new Date().getFullYear();
    renderCalendar();
}

// ✅ FIXED: Summary for current student only
function updateSummaryCards() {
    const now = new Date();
    let wd = 0, ld = 0;
    const student = getCurrentStudent();
    const rate = getCalculatedPerSessionRate();
    
    for (let d = 1; d <= new Date(now.getFullYear(), now.getMonth()+1, 0).getDate(); d++) {
        const dk = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
        const st = getDayStatus(dk);
        if (st === 'working' || st === 'partial') wd++;
        else if (st === 'leave' || st === 'canceled') ld++;
        else if (st === 'pending' && d <= now.getDate()) ld++;
    }
    
    document.getElementById('sumWorking').textContent = wd;
    document.getElementById('sumLeaves').textContent = ld;
    document.getElementById('sumEarning').textContent = '₹' + (wd * rate).toLocaleString('en-IN');
}

function updatePendingAlert() {
    const unpaid = APP.receipts.filter(r => r.paymentStatus === 'unpaid');
    const alert = document.getElementById('pendingAlert');
    if (unpaid.length > 0) {
        alert.style.display = 'block';
        document.getElementById('pendingCount').textContent = `⚠️ ${unpaid.length} Pending`;
    } else {
        alert.style.display = 'none';
    }
}

function updatePaymentsBadge() {
    const unpaid = APP.receipts.filter(r => r.paymentStatus === 'unpaid');
    const badge = document.getElementById('paymentsNav')?.querySelector('.nav-badge');
    if (unpaid.length > 0) {
        if (!badge) {
            const b = document.createElement('span');
            b.className = 'nav-badge';
            b.textContent = unpaid.length;
            document.getElementById('paymentsNav')?.appendChild(b);
        } else {
            badge.textContent = unpaid.length;
        }
    } else if (badge) {
        badge.remove();
    }
}

// ==================== DAY DETAILS & OVERRIDE ====================
function showDayDetail(dk) {
    const e = APP.sessionHistory[dk];
    const belongsToCurrent = e && e.studentId === APP.currentStudentId;
    
    let title = '📅 ' + dk;
    let content = '';
    
    if (!e || !belongsToCurrent) {
        content = `
            <div class="empty-state">
                <div class="empty-icon">📭</div>
                <p>No session data for ${getCurrentStudent()?.name || 'this student'}</p>
                <button class="btn btn-primary" style="margin-top:12px;" onclick="closeModal('dayModal');showDayOverride('${dk}')">✏️ Override This Day</button>
            </div>`;
    } else {
        const tm = getTotalMinutes(dk);
        content = `
            <div style="margin-bottom:12px;">
                <div class="session-detail-row"><span class="detail-label">Status</span><span class="detail-value" style="color:${e.status==='working'?'var(--success)':e.status==='leave'?'var(--danger)':'var(--warning)'}">${e.status.toUpperCase()}</span></div>
                <div class="session-detail-row"><span class="detail-label">Total Time</span><span class="detail-value">${Math.floor(tm/60)}h ${Math.round(tm%60)}m</span></div>
                ${e.entries.map((en, i) => `
                    <div class="session-detail-row"><span class="detail-label">Session ${i+1}</span><span class="detail-value">${new Date(en.in).toLocaleTimeString([], {hour:'2-digit',minute:'2-digit'})} → ${en.out ? new Date(en.out).toLocaleTimeString([], {hour:'2-digit',minute:'2-digit'}) : 'Active...'}</span></div>
                `).join('')}
                ${e.note ? `<div class="session-detail-row"><span class="detail-label">Note</span><span class="detail-value">${e.note}</span></div>` : ''}
            </div>
            <button class="btn btn-outline" style="margin-bottom:6px;" onclick="closeModal('dayModal');showDayOverride('${dk}')">✏️ Override / Edit</button>`;
    }
    
    showModal('dayModal', title, content);
}

function showDayOverride(dk) {
    if (!dk) dk = getTodayKey();
    
    const opts = [
        { l: '🟢 Working Day', v: 'working' },
        { l: '🔴 Leave / Absent', v: 'leave' },
        { l: '🟡 Partial Session', v: 'partial' },
        { l: '🟠 Student Canceled', v: 'canceled' },
        { l: '🔵 Planned Holiday', v: 'holiday' },
    ];
    
    let content = '<p style="margin-bottom:8px;font-size:12px;color:var(--text-light);">Select status for <b>' + dk + '</b>:</p>';
    opts.forEach(o => {
        content += `<button class="btn btn-outline" style="margin-bottom:5px;text-align:left;" onclick="overrideDay('${dk}','${o.v}')">${o.l}</button>`;
    });
    content += `
        <div class="form-group" style="margin-top:8px;">
            <label class="form-label">Note</label>
            <input type="text" class="form-input" id="dayNoteInput" placeholder="Optional note">
        </div>
        <button class="btn btn-primary" onclick="saveDayOverride('${dk}')">💾 Save</button>`;
    
    showModal('dayModal', '✏️ Override: ' + dk, content);
    
    setTimeout(() => {
        const ni = document.getElementById('dayNoteInput');
        if (ni && APP.sessionHistory[dk]) ni.value = APP.sessionHistory[dk].note || '';
    }, 150);
}

function overrideDay(dk, st) {
    if (!APP.sessionHistory[dk]) {
        APP.sessionHistory[dk] = { studentId: APP.currentStudentId, entries: [], status: st, note: '' };
    } else {
        APP.sessionHistory[dk].status = st;
        APP.sessionHistory[dk].studentId = APP.currentStudentId;
    }
    saveData();
    refreshUI();
    showToast('✅ Day marked as ' + st);
}

function saveDayOverride(dk) {
    const note = document.getElementById('dayNoteInput')?.value || '';
    if (!APP.sessionHistory[dk]) {
        APP.sessionHistory[dk] = { studentId: APP.currentStudentId, entries: [], status: 'pending', note: '' };
    }
    APP.sessionHistory[dk].note = note;
    APP.sessionHistory[dk].studentId = APP.currentStudentId;
    saveData();
    closeAllModals();
    refreshUI();
    showToast('✅ Saved');
}

// ==================== STUDENT MANAGEMENT (WITH EDIT & DELETE) ====================
function showStudentSwitcher() {
    let content = APP.students.map(s => `
        <div class="student-card ${s.id === APP.currentStudentId ? 'active' : ''}">
            <div class="student-avatar" style="width:38px;height:38px;font-size:15px;">${s.name.charAt(0).toUpperCase()}</div>
            <div class="student-info" onclick="switchStudent('${s.id}')">
                <div class="student-name-display">${s.name}</div>
                <div class="student-subtitle">${s.class} • ${s.subjects}</div>
            </div>
            <div class="student-card-actions">
                <button class="btn-edit" onclick="event.stopPropagation();editStudent('${s.id}')" title="Edit">✏️</button>
                <button class="btn-delete" onclick="event.stopPropagation();confirmDeleteStudent('${s.id}')" title="Delete">🗑️</button>
            </div>
        </div>
    `).join('');
    
    content += '<button class="btn btn-primary" style="margin-top:8px;" onclick="closeAllModals();addNewStudent()">+ Add New Student</button>';
    
    showModal('studentModal', '👥 Manage Students', content);
}

function switchStudent(id) {
    if (APP.activeSession && APP.activeSession.studentId !== id) {
        autoCheckoutPrevious();
        saveData();
    }
    APP.currentStudentId = id;
    saveData();
    refreshUI();
    closeAllModals();
    showToast('✅ Switched to ' + (getStudent(id)?.name || 'student'));
}

function editStudent(id) {
    closeAllModals();
    const s = getStudent(id);
    if (!s) return;
    
    let content = `
        <input type="hidden" id="sEditId" value="${s.id}">
        <div class="form-group"><label class="form-label">Student Name</label><input type="text" class="form-input" id="sName" value="${s.name}"></div>
        <div class="form-group"><label class="form-label">Class / Grade</label><input type="text" class="form-input" id="sClass" value="${s.class}"></div>
        <div class="form-group"><label class="form-label">Subjects</label><input type="text" class="form-input" id="sSubjects" value="${s.subjects}"></div>
        <div class="form-group"><label class="form-label">Session Duration (mins)</label><input type="number" class="form-input" id="sSessionMins" value="${s.sessionMins}"></div>
        <div class="form-group"><label class="form-label">Per Hour Rate (₹)</label><input type="number" class="form-input" id="sHourlyRate" value="${s.hourlyRate}"></div>
        <hr style="border:0.5px solid var(--border);margin:12px 0;">
        <p style="font-size:11px;font-weight:600;color:var(--text-light);margin-bottom:8px;">👨‍👩‍👦 Parent Details</p>
        <div class="form-group"><label class="form-label">Parent Name</label><input type="text" class="form-input" id="sParentName" value="${s.parentName||''}"></div>
        <div class="form-group"><label class="form-label">Parent Phone</label><input type="tel" class="form-input" id="sParentPhone" value="${s.parentPhone||''}"></div>
        <div class="form-group"><label class="form-label">Parent Email</label><input type="email" class="form-input" id="sParentEmail" value="${s.parentEmail||''}"></div>
        <hr style="border:0.5px solid var(--border);margin:12px 0;">
        <div class="form-group"><label class="form-label">Home Location</label>
            <button class="btn btn-outline btn-sm" onclick="pinLocation()">📍 Pin Current Location</button>
            <input type="text" class="form-input" id="sLocation" value="${s.location||''}" readonly style="margin-top:6px;">
        </div>
        <button class="btn btn-success" onclick="saveStudent()">💾 Update Student</button>
        <button class="btn btn-outline" style="margin-top:6px;" onclick="closeAllModals();showStudentSwitcher()">Cancel</button>`;
    
    showModal('studentModal', '✏️ Edit Student', content);
}

function addNewStudent() {
    let content = `
        <input type="hidden" id="sEditId" value="">
        <div class="form-group"><label class="form-label">Student Name</label><input type="text" class="form-input" id="sName" placeholder="Full name"></div>
        <div class="form-group"><label class="form-label">Class / Grade</label><input type="text" class="form-input" id="sClass" placeholder="e.g. 10th Standard"></div>
        <div class="form-group"><label class="form-label">Subjects</label><input type="text" class="form-input" id="sSubjects" placeholder="Math, Science"></div>
        <div class="form-group"><label class="form-label">Session Duration (mins)</label><input type="number" class="form-input" id="sSessionMins" value="${APP.settings.defaultSessionMins}"></div>
        <div class="form-group"><label class="form-label">Per Hour Rate (₹)</label><input type="number" class="form-input" id="sHourlyRate" value="${APP.settings.defaultHourlyRate}"></div>
        <hr style="border:0.5px solid var(--border);margin:12px 0;">
        <p style="font-size:11px;font-weight:600;color:var(--text-light);margin-bottom:8px;">👨‍👩‍👦 Parent Details</p>
        <div class="form-group"><label class="form-label">Parent Name</label><input type="text" class="form-input" id="sParentName" placeholder="Parent name"></div>
        <div class="form-group"><label class="form-label">Parent Phone</label><input type="tel" class="form-input" id="sParentPhone" placeholder="+91 98765 43210"></div>
        <div class="form-group"><label class="form-label">Parent Email</label><input type="email" class="form-input" id="sParentEmail" placeholder="parent@email.com"></div>
        <hr style="border:0.5px solid var(--border);margin:12px 0;">
        <div class="form-group"><label class="form-label">Home Location</label>
            <button class="btn btn-outline btn-sm" onclick="pinLocation()">📍 Pin Current Location</button>
            <input type="text" class="form-input" id="sLocation" placeholder="Lat, Lng" readonly style="margin-top:6px;">
        </div>
        <button class="btn btn-success" onclick="saveStudent()">💾 Save Student</button>
        <button class="btn btn-outline" style="margin-top:6px;" onclick="closeAllModals();showStudentSwitcher()">Cancel</button>`;
    
    showModal('studentModal', '➕ Add New Student', content);
}

function saveStudent() {
    const eid = document.getElementById('sEditId')?.value;
    const data = {
        id: eid || 's' + Date.now(),
        name: document.getElementById('sName')?.value || '',
        class: document.getElementById('sClass')?.value || '',
        subjects: document.getElementById('sSubjects')?.value || '',
        sessionMins: parseInt(document.getElementById('sSessionMins')?.value) || 90,
        hourlyRate: parseInt(document.getElementById('sHourlyRate')?.value) || 200,
        parentName: document.getElementById('sParentName')?.value || '',
        parentPhone: document.getElementById('sParentPhone')?.value || '',
        parentEmail: document.getElementById('sParentEmail')?.value || '',
        location: document.getElementById('sLocation')?.value || null,
    };
    
    if (!data.name) return showToast('⚠️ Student name is required');
    
    if (eid) {
        const idx = APP.students.findIndex(s => s.id === eid);
        if (idx >= 0) APP.students[idx] = data;
    } else {
        APP.students.push(data);
    }
    
    if (!APP.currentStudentId || APP.currentStudentId === eid) {
        APP.currentStudentId = data.id;
    }
    
    saveData();
    refreshUI();
    closeAllModals();
    showToast('✅ Student saved!');
}

function confirmDeleteStudent(id) {
    const s = getStudent(id);
    if (!s) return;
    if (APP.students.length <= 1) return showToast('⚠️ Cannot delete the last student');
    
    const receiptCount = APP.receipts.filter(r => r.studentId === id).length;
    
    let content = `
        <div style="text-align:center;">
            <div style="font-size:48px;margin-bottom:8px;">⚠️</div>
            <h3>Delete "${s.name}"?</h3>
            <p style="font-size:13px;color:var(--text-light);margin:8px 0;">
                📊 Attendance records will be removed<br>
                🧾 ${receiptCount} receipt(s) will be kept<br>
                ⚠️ This cannot be undone
            </p>
            <div class="btn-row" style="display:flex;gap:8px;">
                <button class="btn btn-outline" onclick="closeAllModals();showStudentSwitcher()">Cancel</button>
                <button class="btn btn-danger" onclick="deleteStudent('${id}')">🗑️ Delete</button>
            </div>
        </div>`;
    
    showModal('studentModal', '⚠️ Confirm Delete', content);
}

function deleteStudent(id) {
    const s = getStudent(id);
    if (!s || APP.students.length <= 1) return;
    
    // Remove student
    APP.students = APP.students.filter(st => st.id !== id);
    
    // Clean up session history for this student
    Object.keys(APP.sessionHistory).forEach(key => {
        if (APP.sessionHistory[key].studentId === id) {
            delete APP.sessionHistory[key];
        }
    });
    
    // Switch to another student
    if (APP.currentStudentId === id) {
        APP.currentStudentId = APP.students[0]?.id || null;
    }
    
    // Clear active session if it was for deleted student
    if (APP.activeSession?.studentId === id) {
        APP.activeSession = null;
    }
    
    saveData();
    refreshUI();
    closeAllModals();
    showToast(`🗑️ "${s.name}" deleted`, true, () => {
        // Undo delete
        APP.students.push(s);
        APP.currentStudentId = s.id;
        saveData();
        refreshUI();
        showToast('✅ Student restored!');
    });
}

function pinLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
            p => {
                const field = document.getElementById('sLocation');
                if (field) field.value = `${p.coords.latitude.toFixed(6)}, ${p.coords.longitude.toFixed(6)}`;
                showToast('📍 Location pinned');
            },
            () => showToast('⚠️ Location access denied')
        );
    } else {
        showToast('⚠️ Geolocation not supported');
    }
}

// ==================== RECEIPTS ====================
function getReceiptStats(from, to, rateOverride) {
    const student = getCurrentStudent();
    if (!student) return { workingDays: 0, avgMins: 0, leaveDays: 0, estimatedTotal: 0, perSessionRate: 0 };
    
    const f = new Date(from), t = new Date(to);
    let wd = 0, tm = 0, ld = 0;
    
    for (let d = new Date(f); d <= t; d.setDate(d.getDate() + 1)) {
        const dk = `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
        const st = getDayStatus(dk);
        if (st === 'working' || st === 'partial') { wd++; tm += getTotalMinutes(dk); }
        else if (st === 'leave' || st === 'canceled') ld++;
        else if (st === 'pending' && d <= new Date()) ld++;
    }
    
    const avg = wd > 0 ? Math.round(tm / wd) : student.sessionMins;
    const effectiveRate = rateOverride !== null ? rateOverride : getCalculatedPerSessionRate();
    return { workingDays: wd, avgMins: avg, leaveDays: ld, estimatedTotal: wd * effectiveRate, perSessionRate: effectiveRate };
}

function showReceiptGenerator() {
    if (!getCurrentStudent()) return showToast('⚠️ Please add a student first');
    const today = new Date();
    const firstDay = new Date(today.getFullYear(), today.getMonth(), 1);
    
    APP.receiptRateOverride = null;
    
    let content = `
        <div class="form-group"><label class="form-label">From Date</label><input type="date" class="form-input" id="rFromDate" value="${firstDay.toISOString().split('T')[0]}"></div>
        <div class="form-group"><label class="form-label">To Date</label><input type="date" class="form-input" id="rToDate" value="${today.toISOString().split('T')[0]}"></div>
        <div class="form-group">
            <label class="form-label">Per Session Rate (₹)</label>
            <input type="number" class="form-input" id="rPerSessionRate" value="${getCalculatedPerSessionRate()}" min="0" step="10" oninput="onRateOverride()">
            <div class="form-hint" id="rateHint">Auto-calculated from student profile</div>
        </div>
        <div id="receiptSummary" style="background:#f8fafc;padding:12px;border-radius:10px;margin-bottom:10px;font-size:12px;"></div>
        <button class="btn btn-success" onclick="generateReceipt()">📄 Generate Receipt</button>`;
    
    showModal('receiptModal', '🧾 Generate Fee Receipt', content);
    
    document.getElementById('rFromDate').addEventListener('input', updateReceiptSummary);
    document.getElementById('rToDate').addEventListener('input', updateReceiptSummary);
    updateReceiptSummary();
}

function onRateOverride() {
    const val = document.getElementById('rPerSessionRate')?.value;
    const calc = getCalculatedPerSessionRate();
    if (val === '' || parseFloat(val) === calc) {
        APP.receiptRateOverride = null;
        document.getElementById('rPerSessionRate')?.classList.remove('rate-override-active');
        const hint = document.getElementById('rateHint');
        if (hint) { hint.textContent = 'Auto-calculated from student profile'; hint.style.color = '#64748b'; }
    } else {
        APP.receiptRateOverride = parseFloat(val) || 0;
        document.getElementById('rPerSessionRate')?.classList.add('rate-override-active');
        const hint = document.getElementById('rateHint');
        if (hint) { hint.textContent = '✏️ Custom rate applied'; hint.style.color = '#92400e'; }
    }
    updateReceiptSummary();
}

function updateReceiptSummary() {
    const from = document.getElementById('rFromDate')?.value;
    const to = document.getElementById('rToDate')?.value;
    const summary = document.getElementById('receiptSummary');
    if (!from || !to || !summary) return;
    
    const st = getReceiptStats(from, to, APP.receiptRateOverride);
    summary.innerHTML = `
        📅 Working: <b>${st.workingDays} days</b> | 
        ⏱️ Avg: <b>${st.avgMins} mins</b> | 
        🔴 Leaves: <b>${st.leaveDays}</b> | 
        💰 Total: <b>₹${st.estimatedTotal.toLocaleString('en-IN')}</b>`;
}

function generateReceipt() {
    const student = getCurrentStudent();
    if (!student) return;
    const from = document.getElementById('rFromDate')?.value;
    const to = document.getElementById('rToDate')?.value;
    if (!from || !to) return showToast('⚠️ Select date range');
    
    const stats = getReceiptStats(from, to, APP.receiptRateOverride);
    const now = new Date();
    const receiptNo = `TUT-${now.getFullYear()}${String(now.getMonth()+1).padStart(2,'0')}${String(now.getDate()).padStart(2,'0')}-${Math.floor(100+Math.random()*900)}`;
    
    APP._lastReceipt = {
        id: receiptNo, studentId: student.id, from, to, stats,
        perSessionRate: stats.perSessionRate,
        date: now.toLocaleDateString('en-IN', { day: 'numeric', month: 'long', year: 'numeric' }),
        paymentStatus: 'unpaid', paymentMethod: '', paymentDate: null, generatedAt: now.toISOString(),
    };
    
    APP.receipts.unshift(APP._lastReceipt);
    saveData();
    showReceiptPreview();
    APP.receiptRateOverride = null;
}

function showReceiptPreview() {
    const r = APP._lastReceipt;
    if (!r) return;
    const tp = APP.tutorProfile;
    const student = getStudent(r.studentId);
    const logoHtml = tp.logo ? `<img src="${tp.logo}" style="max-height:50px;max-width:150px;" alt="Logo">` : '📚 TutorPro';
    const sigHtml = tp.signature ? `<img src="${tp.signature}" style="max-height:40px;" alt="Signature"><br>` : '';
    const upiUrl = `upi://pay?pa=${encodeURIComponent(tp.upiId)}&pn=${encodeURIComponent(tp.name)}&am=${r.stats.estimatedTotal.toFixed(2)}&cu=INR&tn=Tutoring%20Fee`;
    
    let content = `
        <div style="border:2px solid #1a365d;border-radius:10px;padding:18px;background:white;font-family:Arial;">
            <div style="text-align:center;margin-bottom:12px;">${logoHtml}</div>
            <div style="text-align:center;border-bottom:2px dashed #e2e8f0;padding-bottom:10px;margin-bottom:10px;">
                <h2 style="color:#1a365d;font-size:16px;">${tp.businessName}</h2>
                <p style="font-weight:700;font-size:15px;">FEE RECEIPT</p>
                <p style="font-size:10px;color:#64748b;">No: ${r.id}</p>
            </div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;font-size:11px;margin-bottom:10px;">
                <div><strong>Student:</strong> ${student?.name||'N/A'}<br>Class: ${student?.class||''}<br>Subjects: ${student?.subjects||''}<br>Period: ${r.from} to ${r.to}</div>
                <div><strong>Tutor:</strong> ${tp.name}<br>📧 ${tp.email}<br>📱 ${tp.phone}<br>Date: ${r.date}</div>
            </div>
            <table style="width:100%;border-collapse:collapse;font-size:11px;margin-bottom:8px;">
                <tr style="background:#1a365d;color:white;"><th style="padding:6px;">Description</th><th>Days</th><th>Rate</th><th style="text-align:right;">Amount</th></tr>
                <tr><td style="padding:6px;">Tutoring (${r.stats.avgMins}m avg)</td><td style="text-align:center;">${r.stats.workingDays}</td><td>₹${r.perSessionRate.toFixed(0)}/sess</td><td style="text-align:right;">₹${r.stats.estimatedTotal.toLocaleString('en-IN')}</td></tr>
                <tr style="background:#fff7ed;"><td style="padding:6px;">Leaves</td><td style="text-align:center;">${r.stats.leaveDays}</td><td>-</td><td style="text-align:right;">-</td></tr>
            </table>
            <div style="text-align:right;background:#f7fafc;padding:10px;border:2px solid #1a365d;border-radius:6px;font-size:14px;font-weight:700;">Total: ₹${r.stats.estimatedTotal.toLocaleString('en-IN')}</div>
            <div style="margin-top:8px;background:#f0fdf4;padding:10px;border-radius:6px;text-align:center;font-size:11px;">
                <p style="font-weight:600;">💳 Pay via UPI</p><p style="font-weight:700;">${tp.upiId}</p>
                <a href="${upiUrl}" style="display:inline-block;background:#10b981;color:white;padding:8px 16px;border-radius:20px;text-decoration:none;font-weight:700;font-size:12px;margin-top:4px;">📱 Pay ₹${r.stats.estimatedTotal.toLocaleString('en-IN')}</a>
            </div>
            <div style="text-align:right;margin-top:16px;border-top:1px solid #4a5568;padding-top:6px;width:150px;margin-left:auto;text-align:center;">${sigHtml}<span style="font-size:11px;font-weight:600;">${tp.name} (Tutor)</span></div>
            <p style="font-size:8px;color:#94a3b8;text-align:center;margin-top:8px;">Generated by TutorPro v2.0 | © ${new Date().getFullYear()} ${tp.name}</p>
        </div>`;
    
    showModal('receiptPreviewModal', '🧾 Receipt Preview', content + `
        <button class="btn btn-primary" style="margin-top:10px;" onclick="printReceipt()">🖨️ Print / Save PDF</button>
        <button class="btn btn-success" style="margin-top:6px;" onclick="shareReceipt()">📤 Share Receipt</button>`);
}

function printReceipt() {
    const content = document.getElementById('receiptPreviewContent')?.innerHTML || '';
    const w = window.open('', '_blank', 'width=800,height=600');
    w.document.write(`<html><head><title>Fee Receipt</title><style>body{font-family:sans-serif;padding:15px;max-width:700px;margin:auto;}@media print{body{padding:0;}}table{border-collapse:collapse;width:100%;}th,td{border:1px solid #ddd;padding:5px;}th{background:#1a365d;color:white;}</style></head><body>${content}<script>window.print();setTimeout(()=>window.close(),500);<\/script></body></html>`);
    w.document.close();
}

function shareReceipt() {
    const r = APP._lastReceipt;
    if (!r) return;
    const student = getStudent(r.studentId);
    const text = `Fee Receipt\n${student?.name}\n${r.from} to ${r.to}\nDays: ${r.stats.workingDays}\nTotal: ₹${r.stats.estimatedTotal.toLocaleString('en-IN')}\nPay: ${APP.tutorProfile.upiId}`;
    if (navigator.share) navigator.share({ title: 'Fee Receipt', text });
    else { navigator.clipboard.writeText(text); showToast('📋 Copied'); }
}

// ==================== RECEIPT HISTORY & PAYMENT TRACKER ====================
function showReceiptHistory() {
    const receipts = APP.receipts;
    let content = '';
    
    if (receipts.length === 0) {
        content = '<div class="empty-state"><div class="empty-icon">📭</div><p>No receipts yet</p></div>';
    } else {
        content = receipts.map(r => {
            const s = getStudent(r.studentId);
            return `<div class="receipt-item" onclick="viewReceipt('${r.id}')">
                <div class="receipt-dot ${r.paymentStatus}"></div>
                <div class="receipt-info">
                    <div class="r-id">📄 ${r.id}</div>
                    <div class="r-detail">${s?.name||'Unknown'} • ${r.from} → ${r.to}</div>
                </div>
                <div class="receipt-amount">₹${r.stats.estimatedTotal.toLocaleString('en-IN')}</div>
            </div>`;
        }).join('');
    }
    
    showModal('receiptHistoryModal', '🧾 Receipt History', content);
}

function viewReceipt(rid) {
    const r = APP.receipts.find(x => x.id === rid);
    if (r) { APP._lastReceipt = r; showReceiptPreview(); }
}

function showPaymentTracker() {
    APP.paymentFilter = 'all';
    renderPaymentTracker();
    showModal('paymentTrackerModal', '💳 Payment Tracker', `
        <div class="filter-bar">
            <button class="filter-chip active" onclick="filterPayments('all',this)">All</button>
            <button class="filter-chip" onclick="filterPayments('unpaid',this)">❌ Unpaid</button>
            <button class="filter-chip" onclick="filterPayments('paid',this)">✅ Paid</button>
        </div>
        <div id="paymentTrackerContent"></div>`);
    renderPaymentTracker();
}

function filterPayments(f, el) {
    APP.paymentFilter = f;
    document.querySelectorAll('#paymentTrackerModal .filter-chip').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
    renderPaymentTracker();
}

function renderPaymentTracker() {
    const content = document.getElementById('paymentTrackerContent');
    if (!content) return;
    
    let receipts = APP.receipts;
    if (APP.paymentFilter === 'paid') receipts = receipts.filter(r => r.paymentStatus === 'paid');
    else if (APP.paymentFilter === 'unpaid') receipts = receipts.filter(r => r.paymentStatus === 'unpaid');
    
    if (receipts.length === 0) {
        content.innerHTML = '<div class="empty-state"><div class="empty-icon">🎉</div><p>No receipts found</p></div>';
        return;
    }
    
    const grouped = {};
    receipts.forEach(r => {
        if (!grouped[r.studentId]) grouped[r.studentId] = [];
        grouped[r.studentId].push(r);
    });
    
    let totalPending = 0, html = '';
    Object.entries(grouped).forEach(([sid, recs]) => {
        const student = getStudent(sid);
        const pending = recs.filter(r => r.paymentStatus === 'unpaid').reduce((s,r) => s + r.stats.estimatedTotal, 0);
        totalPending += pending;
        
        html += `<div class="tracker-student-card">
            <div class="ts-header">
                <span class="ts-name">👤 ${student?.name||'Unknown'}</span>
                ${pending>0 ? `<span style="color:var(--danger);font-weight:700;">₹${pending.toLocaleString('en-IN')}</span>` : '<span style="color:var(--success);">Paid ✅</span>'}
            </div>`;
        
        recs.forEach(r => {
            html += `<div class="tracker-item">
                <div class="receipt-dot ${r.paymentStatus}"></div>
                <div style="flex:1;font-size:11px;">📄 ${r.id}<br><small>${r.from} → ${r.to} • ${r.stats.workingDays}d</small></div>
                <div style="font-weight:700;text-align:right;">₹${r.stats.estimatedTotal.toLocaleString('en-IN')}<br>
                    <small>${r.paymentStatus==='paid'?'✅ Paid':'❌ Unpaid'}</small></div>
                ${r.paymentStatus==='unpaid' ? `
                    <button class="btn btn-sm btn-success" style="margin-left:6px;" onclick="event.stopPropagation();markPaid('${r.id}','upi')">💳</button>
                    <button class="btn btn-sm btn-warning" style="margin-left:3px;" onclick="event.stopPropagation();markPaid('${r.id}','cash')">💵</button>` : ''}
            </div>`;
        });
        
        html += '</div>';
    });
    
    html += `<div style="background:${totalPending>0?'#fef3c7':'#d1fae5'};padding:14px;border-radius:12px;margin-top:8px;text-align:center;font-weight:700;">
        ${totalPending>0 ? `Total Pending: ₹${totalPending.toLocaleString('en-IN')}` : '🎉 All receipts are paid!'}
    </div>`;
    
    content.innerHTML = html;
}

function markPaid(rid, method) {
    const r = APP.receipts.find(x => x.id === rid);
    if (r) {
        r.paymentStatus = 'paid';
        r.paymentMethod = method;
        r.paymentDate = new Date().toISOString();
        if (APP._lastReceipt?.id === rid) APP._lastReceipt = r;
        saveData();
        renderPaymentTracker();
        updatePendingAlert();
        updatePaymentsBadge();
        showToast(`✅ Paid via ${method}`);
    }
}

// ==================== TUTOR PROFILE ====================
function showTutorProfile() {
    const tp = APP.tutorProfile;
    let content = `
        <div class="form-group"><label class="form-label">Logo</label>
            <div class="upload-area" onclick="document.getElementById('tLogoInput').click()">
                <div id="tLogoPreview">${tp.logo ? '' : '📚<br><small>Tap to upload</small>'}</div>
                <img id="tLogoImg" class="upload-preview" src="${tp.logo||''}" style="${tp.logo?'':'display:none;'}">
            </div>
            <input type="file" id="tLogoInput" accept="image/*" style="display:none;" onchange="handleFileUpload(this,'tLogoImg','tLogoPreview','logo')">
        </div>
        <div class="form-group"><label class="form-label">Name</label><input type="text" class="form-input" id="tName" value="${tp.name}"></div>
        <div class="form-group"><label class="form-label">Business</label><input type="text" class="form-input" id="tBusiness" value="${tp.businessName}"></div>
        <div class="form-group"><label class="form-label">Email</label><input type="email" class="form-input" id="tEmail" value="${tp.email}"></div>
        <div class="form-group"><label class="form-label">Phone</label><input type="tel" class="form-input" id="tPhone" value="${tp.phone}"></div>
        <div class="form-group"><label class="form-label">UPI ID</label><input type="text" class="form-input" id="tUpi" value="${tp.upiId}"></div>
        <div class="form-group"><label class="form-label">Signature</label>
            <div class="upload-area" onclick="document.getElementById('tSigInput').click()">
                <div id="tSigPreview">${tp.signature ? '' : '✍️<br><small>Tap to upload</small>'}</div>
                <img id="tSigImg" class="upload-preview signature" src="${tp.signature||''}" style="${tp.signature?'':'display:none;'}">
            </div>
            <input type="file" id="tSigInput" accept="image/*" style="display:none;" onchange="handleFileUpload(this,'tSigImg','tSigPreview','signature')">
        </div>
        <button class="btn btn-success" onclick="saveTutorProfile()">💾 Save Profile</button>`;
    
    showModal('tutorProfileModal', '👤 Tutor Profile', content);
}

function saveTutorProfile() {
    APP.tutorProfile.name = document.getElementById('tName')?.value || 'Mr Kaif';
    APP.tutorProfile.businessName = document.getElementById('tBusiness')?.value || '';
    APP.tutorProfile.email = document.getElementById('tEmail')?.value || '';
    APP.tutorProfile.phone = document.getElementById('tPhone')?.value || '';
    APP.tutorProfile.upiId = document.getElementById('tUpi')?.value || '';
    if (!APP.tutorProfile.logo) APP.tutorProfile.logo = generateDefaultLogo();
    saveData();
    closeAllModals();
    refreshUI();
    showToast('✅ Profile saved');
}

function handleFileUpload(input, imgId, previewId, type) {
    const file = input.files[0];
    if (!file) return;
    const maxSize = type === 'logo' ? 500000 : 200000;
    if (file.size > maxSize) return showToast('⚠️ File too large');
    
    const reader = new FileReader();
    reader.onload = e => {
        compressImage(e.target.result, 0.6, compressed => {
            const img = document.getElementById(imgId);
            if (img) { img.src = compressed; img.style.display = 'block'; }
            const preview = document.getElementById(previewId);
            if (preview) preview.style.display = 'none';
            if (type === 'logo') APP.tutorProfile.logo = compressed;
            else APP.tutorProfile.signature = compressed;
            saveData();
        });
    };
    reader.readAsDataURL(file);
}

// ==================== SETTINGS ====================
function showSettings() {
    let used = 0;
    for (let key in localStorage) { if (localStorage.hasOwnProperty(key)) used += localStorage[key].length * 2; }
    const pct = Math.round((used / (5*1024*1024)) * 100);
    
    let content = `
        <div class="form-group"><label class="form-label">Min Session (mins)</label><input type="number" class="form-input" id="setMinTime" value="${APP.settings.minSessionTime}"></div>
        <div class="form-group"><label class="form-label">Geofence (meters)</label><input type="number" class="form-input" id="setRadius" value="${APP.settings.geofenceRadius}"></div>
        <div class="form-group"><label class="form-label">Default Rate/hr (₹)</label><input type="number" class="form-input" id="setDefaultRate" value="${APP.settings.defaultHourlyRate}"></div>
        <div class="form-group"><label class="form-label">Default Session (mins)</label><input type="number" class="form-input" id="setDefaultSession" value="${APP.settings.defaultSessionMins}"></div>
        <div style="font-size:10px;color:var(--text-light);margin-bottom:4px;">Storage: ${(used/1024/1024).toFixed(1)}MB / 5MB (${pct}%)</div>
        <div class="storage-bar"><div class="storage-bar-fill ${pct>80?'danger':pct>60?'warning':''}" style="width:${pct}%;"></div></div>
        <button class="btn btn-success" onclick="saveSettings()" style="margin-top:12px;">💾 Save Settings</button>
        <button class="btn btn-primary" style="margin-top:8px;" onclick="installApp()">📲 Install App</button>
        <button class="btn btn-danger" style="margin-top:8px;" onclick="exportData()">📤 Export Backup</button>
        <button class="btn btn-outline" style="margin-top:6px;" onclick="importDataPrompt()">📥 Import Backup</button>
        <div style="text-align:center;margin-top:12px;padding-top:10px;border-top:1px solid var(--border);font-size:9px;color:#94a3b8;">
            TutorPro v2.0 | © 2026 Mr Kaif<br>kaifalam522@gmail.com
        </div>`;
    
    showModal('settingsModal', '⚙️ Settings', content);
}

function saveSettings() {
    APP.settings.minSessionTime = parseInt(document.getElementById('setMinTime')?.value) || 15;
    APP.settings.geofenceRadius = parseInt(document.getElementById('setRadius')?.value) || 150;
    APP.settings.defaultHourlyRate = parseInt(document.getElementById('setDefaultRate')?.value) || 200;
    APP.settings.defaultSessionMins = parseInt(document.getElementById('setDefaultSession')?.value) || 90;
    saveData();
    closeAllModals();
    showToast('✅ Settings saved');
}

function exportData() {
    const blob = new Blob([JSON.stringify({
        tutorProfile: APP.tutorProfile, students: APP.students,
        currentStudentId: APP.currentStudentId, settings: APP.settings,
        sessionHistory: APP.sessionHistory, receipts: APP.receipts,
        _meta: { app:'TutorPro', version:'2.0', developer:APP.tutorProfile.name, exported:new Date().toISOString() }
    }, null, 2)], { type:'application/json' });
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = `tutorpro_backup_${new Date().toISOString().split('T')[0]}.json`;
    a.click();
    showToast('📤 Backup downloaded');
}

function importDataPrompt() { document.getElementById('importFile').click(); }

function importData(e) {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = ev => {
        try {
            const d = JSON.parse(ev.target.result);
            if (d.tutorProfile) APP.tutorProfile = { ...APP.tutorProfile, ...d.tutorProfile };
            if (d.students) APP.students = d.students;
            if (d.currentStudentId) APP.currentStudentId = d.currentStudentId;
            if (d.settings) APP.settings = { ...APP.settings, ...d.settings };
            if (d.sessionHistory) APP.sessionHistory = d.sessionHistory;
            if (d.receipts) APP.receipts = d.receipts;
            saveData();
            refreshUI();
            showToast('📥 Imported successfully');
        } catch { showToast('⚠️ Invalid file'); }
    };
    reader.readAsText(file);
    e.target.value = '';
}

// ==================== MODAL SYSTEM ====================
function showModal(id, title, content) {
    const container = document.getElementById('modalContainer');
    const existing = document.getElementById(id);
    if (existing) existing.remove();
    
    const overlay = document.createElement('div');
    overlay.className = 'modal-overlay active';
    overlay.id = id;
    overlay.onclick = function(e) { if (e.target === overlay) closeModal(id); };
    
    overlay.innerHTML = `
        <div class="modal-sheet">
            <div class="modal-handle"></div>
            <div class="modal-title">${title}</div>
            <div id="${id}Content">${content}</div>
        </div>`;
    
    container.appendChild(overlay);
    document.body.style.overflow = 'hidden';
}

function closeModal(id) {
    const el = document.getElementById(id);
    if (el) el.remove();
    if (!document.querySelector('.modal-overlay')) {
        document.body.style.overflow = '';
    }
}

function closeAllModals() {
    document.querySelectorAll('.modal-overlay').forEach(m => m.remove());
    document.body.style.overflow = '';
}

// ==================== INSTALL ====================
let deferredPrompt = null;
window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
});

function installApp() {
    if (deferredPrompt) {
        deferredPrompt.prompt();
        deferredPrompt.userChoice.then(() => { deferredPrompt = null; });
    } else if (window.matchMedia('(display-mode: standalone)').matches) {
        showToast('✅ Already installed!');
    } else {
        showToast('📱 Open in Chrome → Menu → Install App');
    }
}

// ==================== UI ====================
function refreshUI() {
    const s = getCurrentStudent();
    if (s) {
        document.getElementById('currentAvatar').textContent = s.name.charAt(0).toUpperCase();
        document.getElementById('currentStudentName').textContent = s.name;
        document.getElementById('currentStudentDetails').textContent = `${s.class} • ${s.subjects}`;
        document.getElementById('statusStudentName').textContent = s.name;
    }
    
    const tk = getTodayKey();
    const st = getDayStatus(tk);
    const ind = document.getElementById('statusIndicator');
    ind.className = 'status-indicator';
    const timer = document.getElementById('sessionTimer');
    timer.style.display = 'none';
    
    if (st === 'working') {
        ind.classList.add('working'); ind.textContent = '✅';
        document.getElementById('statusTitle').textContent = 'Session Completed';
    } else if (st === 'leave') {
        ind.classList.add('leave'); ind.textContent = '🔴';
        document.getElementById('statusTitle').textContent = 'Leave / Absent';
    } else if (st === 'partial') {
        ind.classList.add('pending'); ind.textContent = '⚠️';
        document.getElementById('statusTitle').textContent = 'Partial Session';
    } else {
        ind.classList.add('pending'); ind.textContent = '⏳';
        document.getElementById('statusTitle').textContent = 'No Session Yet';
    }
    
    if (APP.activeSession) { timer.style.display = 'block'; updateTimer(); }
    renderCalendar();
}

function updateTimer() {
    if (!APP.activeSession) return;
    const d = Math.floor((new Date() - new Date(APP.activeSession.startTime)) / 1000);
    const h = Math.floor(d / 3600), m = Math.floor((d % 3600) / 60), s = d % 60;
    document.getElementById('sessionTimer').textContent = 
        `⏱️ ${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    if (APP.activeSession) setTimeout(updateTimer, 1000);
}

function switchTab(tab) {
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    const m = { home:0, calendar:1, receipts:2, payments:3, students:4 };
    const tabs = document.querySelectorAll('.nav-item');
    if (tabs[m[tab]]) tabs[m[tab]].classList.add('active');
    
    if (tab === 'receipts') showReceiptHistory();
    else if (tab === 'payments') showPaymentTracker();
    else if (tab === 'students') showStudentSwitcher();
}

// ==================== INIT ====================
function init() {
    loadData();
    if (!APP.tutorProfile.logo) APP.tutorProfile.logo = generateDefaultLogo();
    refreshUI();
    updatePaymentsBadge();
    
    if (APP.activeSession) updateTimer();
    
    // Service Worker
    if ('serviceWorker' in navigator) {
        const swCode = `
            const C='tutorpro-v2';
            self.addEventListener('install',e=>self.skipWaiting());
            self.addEventListener('activate',e=>e.waitUntil(clients.claim()));
            self.addEventListener('fetch',e=>{
                e.respondWith(
                    caches.match(e.request).then(r=>r||fetch(e.request).then(res=>{
                        if(res.ok){const cl=res.clone();caches.open(C).then(c=>c.put(e.request,cl));}
                        return res;
                    }).catch(()=>caches.match(e.request)))
                );
            });
        `;
        const blob = new Blob([swCode], { type: 'application/javascript' });
        navigator.serviceWorker.register(URL.createObjectURL(blob), { scope: '/' }).catch(() => {});
    }
    
    // Manifest
    const manifest = {
        name: 'TutorPro - Smart Tutoring Manager',
        short_name: 'TutorPro',
        start_url: '.',
        display: 'standalone',
        orientation: 'portrait',
        background_color: '#ffffff',
        theme_color: '#1a365d',
        icons: [
            { src: generateDefaultLogo(), sizes: '192x192', type: 'image/png' }
        ]
    };
    const mBlob = new Blob([JSON.stringify(manifest)], { type: 'application/json' });
    const link = document.createElement('link');
    link.rel = 'manifest';
    link.href = URL.createObjectURL(mBlob);
    document.head.appendChild(link);
    
    console.log('%c🚀 TutorPro v2.0 %c| %c© '+new Date().getFullYear()+' Mr Kaif',
        'color:#1a365d;font-weight:bold;font-size:16px;','','color:#64748b;');
}

init();
</script>
</body>
</html>
