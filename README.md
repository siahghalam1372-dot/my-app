<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Nuovo Espresso Pro - Custom Vector UI</title>
  <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet" type="text/css" />
  <style>
    :root {
      --bg: #131F24;
      --card: #1F2F36;
      --card-hover: #283B44;
      --text: #FFFFFF;
      --muted: #8FA3AD;
      --border: #37464F;
      --green: #58CC02;
      --green-dark: #46A302;
      --blue: #1CB0F6;
      --purple: #CE82FF;
      --gold: #FFC800;
      --red: #FF4B4B;
      --orange: #FF9600;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Vazirmatn', system-ui, -apple-system, sans-serif; }
    body { background: var(--bg); color: var(--text); display: flex; justify-content: center; min-height: 100vh; }
    .app-shell { width: 100%; max-width: 480px; background: var(--bg); min-height: 100vh; display: flex; flex-direction: column; position: relative; padding-bottom: 84px; box-shadow: 0 0 40px rgba(0,0,0,0.7); }

    svg { display: inline-block; vertical-align: middle; flex-shrink: 0; }

    /* Top Status Header */
    header { background: rgba(19, 31, 36, 0.96); backdrop-filter: blur(8px); padding: 12px 16px; border-bottom: 2px solid var(--border); display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 30; }
    .flag-chip { display: flex; align-items: center; gap: 8px; font-weight: 800; font-size: 0.95rem; }
    .stats-row { display: flex; gap: 10px; align-items: center; font-weight: 800; font-size: 0.88rem; }
    .stat-item { display: flex; align-items: center; gap: 6px; background: var(--card); padding: 5px 10px; border-radius: 12px; border: 1.5px solid var(--border); }

    /* Views & Containers */
    .view-container { padding: 16px; flex: 1; }
    .card { background: var(--card); border-radius: 16px; padding: 16px; margin-bottom: 14px; border: 2px solid var(--border); }
    .title-lg { font-size: 1.08rem; font-weight: 800; margin-bottom: 8px; display: flex; align-items: center; gap: 8px; }
    .subtitle { font-size: 0.85rem; color: var(--muted); line-height: 1.65; margin-bottom: 14px; }

    /* Inputs & 3D Buttons */
    .input-box { width: 100%; padding: 13px 14px; border-radius: 14px; border: 2px solid var(--border); background: #131F24; color: var(--text); font-size: 0.92rem; margin-bottom: 10px; outline: none; }
    .input-box:focus { border-color: var(--blue); }
    .btn { width: 100%; padding: 12px 16px; border-radius: 14px; border: none; font-size: 0.94rem; font-weight: 800; cursor: pointer; transition: 0.1s; display: inline-flex; align-items: center; justify-content: center; gap: 8px; margin-top: 8px; }
    .btn:active { transform: translateY(3px); }
    .btn-green { background: var(--green); color: #fff; box-shadow: 0 4px 0 var(--green-dark); }
    .btn-blue { background: var(--blue); color: #fff; box-shadow: 0 4px 0 #1185BC; }
    .btn-purple { background: var(--purple); color: #131F24; box-shadow: 0 4px 0 #9D4EDD; }
    .btn-outline { background: transparent; border: 2px solid var(--border); color: var(--text); box-shadow: 0 3px 0 var(--border); }
    .btn-danger { background: transparent; border: 2px solid var(--border); color: var(--blue); font-weight: 800; letter-spacing: 0.5px; }

    /* Map Path & Custom Vector Nodes */
    .unit-header { border-radius: 16px; padding: 14px 16px; margin: 14px 0; color: #fff; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 4px 0 rgba(0,0,0,0.3); }
    .nodes-col { display: flex; flex-direction: column; align-items: center; gap: 18px; padding: 12px 0; }
    .map-node { width: 72px; height: 68px; border-radius: 50%; display: flex; align-items: center; justify-content: center; cursor: pointer; border: 4px solid rgba(255,255,255,0.2); background: var(--card); box-shadow: 0 7px 0 #0B1215, inset 0 3px 0 rgba(255,255,255,0.25); position: relative; transition: 0.15s; }
    .map-node:active { transform: translateY(5px); box-shadow: 0 2px 0 #0B1215; }
    .map-node.done { border-color: rgba(255,255,255,0.45); }
    .map-node.current { border-color: var(--gold); animation: floatNode 1.5s infinite ease-in-out; }
    .map-node.locked { opacity: 0.45; background: #1B282E; border-color: var(--border); box-shadow: 0 6px 0 #0B1215; }
    .node-label { font-size: 0.73rem; font-weight: 700; color: #E2E8F0; margin-top: 6px; background: var(--card); padding: 4px 10px; border-radius: 10px; border: 1.5px solid var(--border); text-align: center; }
    @keyframes floatNode { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-5px); } }

    /* Interactive Words & Exercises */
    .it-word { direction: ltr; display: inline-block; color: var(--blue); font-weight: 800; border-bottom: 2px dotted var(--blue); cursor: pointer; padding: 0 2px; font-family: system-ui, sans-serif; }
    .word-pop { background: #131F24; border: 2px solid var(--blue); border-radius: 12px; padding: 10px 12px; margin-bottom: 12px; font-size: 0.85rem; display: flex; justify-content: space-between; align-items: center; }
    .opt-btn { width: 100%; text-align: right; padding: 13px 14px; margin-bottom: 8px; border-radius: 14px; border: 2px solid var(--border); background: #131F24; color: var(--text); cursor: pointer; font-size: 0.92rem; font-weight: 700; box-shadow: 0 3px 0 var(--border); }
    .opt-btn.correct { background: rgba(88, 204, 2, 0.18); border-color: var(--green); color: var(--green); }
    .opt-btn.wrong { background: rgba(255, 75, 75, 0.18); border-color: var(--red); color: var(--red); }
    .feedback { padding: 12px; border-radius: 14px; font-size: 0.86rem; line-height: 1.6; margin-top: 10px; display: none; }
    .feedback.show { display: block; }
    .feedback.ok { background: rgba(88, 204, 2, 0.15); border: 2px solid var(--green); color: #A7F3D0; }
    .feedback.err { background: rgba(255, 75, 75, 0.15); border: 2px solid var(--red); color: #FECACA; }

    .audio-circle { background: var(--blue); border: none; width: 38px; height: 38px; border-radius: 12px; box-shadow: 0 3px 0 #1185BC; cursor: pointer; display: inline-flex; align-items: center; justify-content: center; }
    .audio-circle:active { transform: translateY(2px); box-shadow: 0 1px 0 #1185BC; }

    /* Sentence Builder */
    .sentence-slot { min-height: 54px; background: #131F24; border: 2px dashed var(--border); border-radius: 14px; padding: 12px; direction: ltr; text-align: left; font-weight: 800; color: var(--gold); margin-bottom: 10px; display: flex; flex-wrap: wrap; gap: 6px; align-items: center; }
    .chip-pool { display: flex; flex-wrap: wrap; gap: 8px; direction: ltr; margin: 10px 0; }
    .chip { background: #131F24; border: 2px solid var(--border); box-shadow: 0 3px 0 var(--border); color: var(--text); padding: 8px 13px; border-radius: 12px; font-weight: 800; cursor: pointer; font-family: system-ui, sans-serif; }

    /* Leitner 5-Box Grid */
    .leitner-boxes { display: grid; grid-template-columns: repeat(5, 1fr); gap: 6px; margin-bottom: 14px; }
    .l-box { background: #131F24; border: 2px solid var(--border); border-radius: 12px; padding: 8px 4px; text-align: center; }
    .l-box.active-box { border-color: var(--purple); background: rgba(206, 130, 255, 0.12); }
    .l-box-num { font-size: 0.72rem; color: var(--muted); font-weight: 700; }
    .l-box-cnt { font-size: 1.05rem; font-weight: 800; color: var(--text); margin-top: 2px; }

    /* Duolingo Settings List Style */
    .settings-group-title { font-size: 0.95rem; font-weight: 800; color: var(--text); margin: 16px 0 8px; }
    .settings-list { background: var(--card); border: 2px solid var(--border); border-radius: 16px; overflow: hidden; margin-bottom: 16px; }
    .settings-row { display: flex; justify-content: space-between; align-items: center; padding: 15px 16px; border-bottom: 1px solid var(--border); cursor: pointer; font-weight: 700; font-size: 0.94rem; transition: 0.15s; }
    .settings-row:last-child { border-bottom: none; }
    .settings-row:hover { background: var(--card-hover); }
    .settings-chevron { color: var(--muted); font-weight: 800; font-size: 1.1rem; }
    .footer-links { display: flex; flex-direction: column; gap: 10px; margin-top: 18px; padding: 0 4px; }
    .footer-link { color: var(--blue); font-weight: 800; font-size: 0.82rem; cursor: pointer; text-transform: uppercase; letter-spacing: 0.5px; }

    /* Leaderboard (Amethyst League) */
    .league-header { text-align: center; padding: 10px 0 18px; border-bottom: 2px solid var(--border); margin-bottom: 12px; }
    .league-trophies { display: flex; justify-content: center; align-items: center; gap: 16px; margin-bottom: 12px; }
    .leader-row { display: flex; justify-content: space-between; align-items: center; padding: 12px 14px; border-radius: 14px; margin-bottom: 6px; background: var(--card); border: 1.5px solid transparent; }
    .leader-row.me { background: rgba(88, 204, 2, 0.14); border-color: var(--green); }
    .leader-left { display: flex; align-items: center; gap: 12px; }
    .rank-badge { width: 28px; display: flex; justify-content: center; font-weight: 800; font-size: 0.95rem; }
    .avatar-circle { width: 42px; height: 42px; border-radius: 50%; background: #283B44; border: 2px solid var(--border); display: flex; align-items: center; justify-content: center; font-weight: 800; color: #fff; overflow: hidden; }

    /* Bottom Sheet Menu */
    .bottom-sheet-backdrop { position: fixed; inset: 0; background: rgba(0,0,0,0.65); z-index: 40; display: none; justify-content: center; align-items: flex-end; }
    .bottom-sheet-backdrop.show { display: flex; }
    .bottom-sheet { width: 100%; max-width: 480px; background: var(--card); border-top: 2px solid var(--border); border-top-left-radius: 20px; border-top-right-radius: 20px; padding: 10px 0 88px; }
    .sheet-item { display: flex; align-items: center; gap: 14px; padding: 14px 20px; border-bottom: 1px solid var(--border); cursor: pointer; font-weight: 800; font-size: 0.96rem; }
    .sheet-item:last-child { border-bottom: none; }

    /* Bottom Navigation Bar */
    .bottom-nav { position: fixed; bottom: 0; width: 100%; max-width: 480px; background: var(--bg); border-top: 2px solid var(--border); display: flex; justify-content: space-around; padding: 8px 0; z-index: 50; }
    .nav-item { background: none; border: 2px solid transparent; border-radius: 14px; padding: 6px 12px; cursor: pointer; position: relative; display: flex; align-items: center; justify-content: center; transition: 0.15s; }
    .nav-item.active { border-color: var(--blue); background: rgba(28, 176, 246, 0.12); }
    .nav-badge { position: absolute; top: 0px; right: 2px; background: var(--red); color: #fff; font-size: 0.65rem; font-weight: 800; padding: 1px 5px; border-radius: 10px; border: 1.5px solid var(--bg); }
  </style>
</head>
<body>

<div class="app-shell" id="app"></div>

<!-- Bottom Sheet Menu (Custom SVGs Matching Screenshot 2) -->
<div class="bottom-sheet-backdrop" id="moreSheet" onclick="closeMoreSheet()">
  <div class="bottom-sheet" onclick="event.stopPropagation()" id="moreSheetContent"></div>
</div>

<script>
/* ================= 1. CUSTOM MULTI-COLOR DUOLINGO-STYLE SVG ICON ENGINE ================= */
const ICONS = {
  // Bottom Nav 1: Colorful House (Orange roof, yellow door)
  navHome: `<svg width="32" height="32" viewBox="0 0 36 36" fill="none">
    <path d="M4 17L18 5L32 17V30C32 31.6569 30.6569 33 29 33H7C5.34315 33 4 31.6569 4 30V17Z" fill="#FFC800"/>
    <path d="M2 18L18 4L34 18" stroke="#FF4B4B" stroke-width="5" stroke-linecap="round" stroke-linejoin="round"/>
    <rect x="14" y="21" width="8" height="12" rx="3" fill="#8B572A"/>
    <circle cx="18" cy="14" r="3" fill="#FF9600"/>
  </svg>`,

  // Bottom Nav 2: Leitner Chest (Gold/Orange Chest)
  navChest: `<svg width="32" height="32" viewBox="0 0 36 36" fill="none">
    <rect x="4" y="9" width="28" height="20" rx="5" fill="#FF9600" stroke="#FFC800" stroke-width="2.5"/>
    <path d="M4 17H32" stroke="#8B572A" stroke-width="3"/>
    <rect x="15" y="14" width="6" height="7" rx="2" fill="#FFF" stroke="#8B572A" stroke-width="2"/>
  </svg>`,

  // Bottom Nav 3: Amethyst League Trophy (Purple Shield/Cup)
  navTrophy: `<svg width="32" height="32" viewBox="0 0 36 36" fill="none">
    <path d="M9 6H27V15C27 20.5 22.97 25 18 25C13.03 25 9 20.5 9 15V6Z" fill="#CE82FF"/>
    <path d="M9 9H5V13C5 15.5 7 17 9 17V9Z" fill="#A555EC"/>
    <path d="M27 9H31V13C31 15.5 29 17 27 17V9Z" fill="#A555EC"/>
    <rect x="15" y="24" width="6" height="5" fill="#A555EC"/>
    <rect x="11" y="29" width="14" height="4" rx="2" fill="#CE82FF"/>
    <path d="M14 11L18 16L22 11" stroke="#F3E8FF" stroke-width="2" stroke-linecap="round"/>
  </svg>`,

  // Bottom Nav 4: AI Live Tutor (Cyan/Purple Bot Mascot)
  navBot: `<svg width="32" height="32" viewBox="0 0 36 36" fill="none">
    <rect x="5" y="9" width="26" height="21" rx="8" fill="#1CB0F6"/>
    <circle cx="18" cy="5" r="2.5" fill="#CE82FF"/>
    <line x1="18" y1="6" x2="18" y2="9" stroke="#CE82FF" stroke-width="2.5"/>
    <circle cx="13" cy="18" r="3" fill="#FFF"/>
    <circle cx="23" cy="18" r="3" fill="#FFF"/>
    <circle cx="13" cy="18" r="1.3" fill="#131F24"/>
    <circle cx="23" cy="18" r="1.3" fill="#131F24"/>
    <path d="M14 24C15.5 25.8 20.5 25.8 22 24" stroke="#FFF" stroke-width="2.5" stroke-linecap="round"/>
  </svg>`,

  // Bottom Nav 5: Purple Circle More (...)
  navMore: `<svg width="32" height="32" viewBox="0 0 36 36" fill="none">
    <circle cx="18" cy="18" r="14" fill="#CE82FF"/>
    <circle cx="12" cy="18" r="2" fill="#FFF"/>
    <circle cx="18" cy="18" r="2" fill="#FFF"/>
    <circle cx="24" cy="18" r="2" fill="#FFF"/>
  </svg>`,

  // Header & Stats Icons
  flagIt: `<svg width="26" height="20" viewBox="0 0 30 22" fill="none">
    <rect width="30" height="22" rx="4" fill="#FFF"/>
    <path d="M0 4C0 1.79 1.79 0 4 0H10V22H4C1.79 22 0 20.21 0 18V4Z" fill="#008C45"/>
    <path d="M20 0H26C28.21 0 30 1.79 30 4V18C30 20.21 28.21 22 26 22H20V0Z" fill="#CD212A"/>
  </svg>`,
  flagDe: `<svg width="20" height="14" viewBox="0 0 24 18"><rect width="24" height="6" fill="#000"/><rect y="6" width="24" height="6" fill="#DD0000"/><rect y="12" width="24" height="6" fill="#FFCE00"/></svg>`,
  flagUs: `<svg width="20" height="14" viewBox="0 0 24 18"><rect width="24" height="18" rx="2" fill="#B22234"/><rect y="3" width="24" height="2" fill="#FFF"/><rect y="7" width="24" height="2" fill="#FFF"/><rect y="11" width="24" height="2" fill="#FFF"/><rect y="15" width="24" height="2" fill="#FFF"/><rect width="11" height="10" fill="#3C3B6E"/></svg>`,

  fire: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none">
    <path d="M12 2C12 2 6 8 6 13.5C6 17.09 8.69 20 12 20C15.31 20 18 17.09 18 13.5C18 11 16.5 8.5 15 7C15 9 13.5 10 12.5 9C11.5 8 12 4.5 12 2Z" fill="#FF9600"/>
    <path d="M12 11C12 11 9.5 13.5 9.5 15.5C9.5 17.15 10.62 18.5 12 18.5C13.38 18.5 14.5 17.15 14.5 15.5C14.5 13.5 12 11 12 11Z" fill="#FFC800"/>
  </svg>`,

  bolt: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none">
    <path d="M13 2L4 14H11L10 22L20 10H13L13 2Z" fill="#FFC800"/>
  </svg>`,

  cards: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none">
    <rect x="3" y="6" width="14" height="15" rx="3" fill="#A555EC"/>
    <rect x="7" y="3" width="14" height="15" rx="3" fill="#CE82FF" stroke="#131F24" stroke-width="1.5"/>
  </svg>`,

  // Map Node Vector Icons
  star: `<svg width="30" height="30" viewBox="0 0 24 24" fill="none">
    <path d="M12 2L14.9 8.26L21.8 9.27L16.8 14.14L17.98 21.02L12 17.77L6.02 21.02L7.2 14.14L2.2 9.27L9.1 8.26L12 2Z" fill="#FFF"/>
  </svg>`,
  check: `<svg width="30" height="30" viewBox="0 0 24 24" fill="none">
    <path d="M5 13L9 17L19 7" stroke="#FFF" stroke-width="3.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>`,
  lock: `<svg width="26" height="26" viewBox="0 0 24 24" fill="none">
    <rect x="5" y="11" width="14" height="10" rx="3" fill="#8FA3AD"/>
    <path d="M8 11V7C8 4.79 9.79 3 12 3C14.21 3 16 4.79 16 7V11" stroke="#8FA3AD" stroke-width="2.5"/>
  </svg>`,
  unlock: `<svg width="26" height="26" viewBox="0 0 24 24" fill="none">
    <rect x="5" y="11" width="14" height="10" rx="3" fill="#FFF"/>
    <path d="M8 11V7C8 4.79 9.79 3 12 3C13.8 3 15.3 4.2 15.8 5.8" stroke="#FFF" stroke-width="2.5" stroke-linecap="round"/>
  </svg>`,
  book: `<svg width="28" height="28" viewBox="0 0 24 24" fill="none">
    <path d="M4 19.5C4 18.1 5.1 17 6.5 17H20V4H6.5C5.1 4 4 5.1 4 6.5V19.5Z" fill="#FFF"/>
    <path d="M4 19.5C4 20.9 5.1 22 6.5 22H20V19H6.5C5.6 19 5 18.4 5 17.5" stroke="#FFF" stroke-width="2"/>
  </svg>`,
  dumbbell: `<svg width="28" height="28" viewBox="0 0 28 28" fill="none">
    <rect x="3" y="9" width="4" height="10" rx="2" fill="#1CB0F6"/>
    <rect x="7" y="6" width="4" height="16" rx="2" fill="#1CB0F6"/>
    <rect x="11" y="12" width="6" height="4" fill="#84D8FF"/>
    <rect x="17" y="6" width="4" height="16" rx="2" fill="#1CB0F6"/>
    <rect x="21" y="9" width="4" height="10" rx="2" fill="#1CB0F6"/>
  </svg>`,
  videoCall: `<svg width="28" height="28" viewBox="0 0 28 28" fill="none">
    <rect x="3" y="6" width="16" height="16" rx="4" fill="#CE82FF"/>
    <path d="M19 11L25 7V21L19 17V11Z" fill="#A555EC"/>
  </svg>`,
  profileBlue: `<svg width="28" height="28" viewBox="0 0 28 28" fill="none">
    <circle cx="14" cy="10" r="5" fill="#1CB0F6"/>
    <path d="M5 24C5 19.5 9 17 14 17C19 17 23 19.5 23 24" fill="#1CB0F6"/>
  </svg>`,
  gear: `<svg width="28" height="28" viewBox="0 0 24 24" fill="none">
    <circle cx="12" cy="12" r="4" stroke="#8FA3AD" stroke-width="2.5"/>
    <path d="M12 2V5M12 19V22M2 12H5M19 12H22M4.9 4.9L7 7M17 17L19.1 19.1M19.1 4.9L17 7M7 17L4.9 19.1" stroke="#8FA3AD" stroke-width="2.5" stroke-linecap="round"/>
  </svg>`,
  speaker: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none">
    <path d="M11 5L6 9H2V15H6L11 19V5Z" fill="#FFF"/>
    <path d="M15.5 8.5C16.8 9.8 16.8 14.2 15.5 15.5M18.5 5.5C21.5 8.5 21.5 15.5 18.5 18.5" stroke="#FFF" stroke-width="2.2" stroke-linecap="round"/>
  </svg>`,

  // Medals for League
  medal1: `<svg width="26" height="26" viewBox="0 0 24 24"><circle cx="12" cy="13" r="8" fill="#FFC800"/><text x="12" y="17" text-anchor="middle" fill="#8B572A" font-size="11" font-weight="900">1</text></svg>`,
  medal2: `<svg width="26" height="26" viewBox="0 0 24 24"><circle cx="12" cy="13" r="8" fill="#E2E8F0"/><text x="12" y="17" text-anchor="middle" fill="#475569" font-size="11" font-weight="900">2</text></svg>`,
  medal3: `<svg width="26" height="26" viewBox="0 0 24 24"><circle cx="12" cy="13" r="8" fill="#FF9600"/><text x="12" y="17" text-anchor="middle" fill="#7C2D12" font-size="11" font-weight="900">3</text></svg>`
};

/* ================= 2. DICTIONARY & 10 STAGES DATA ================= */
const WORD_DICT = {
  "ciao": { fa: "سلام / خداحافظ (دوستانه)", en: "Hi / Bye (informal)" },
  "buongiorno": { fa: "صبح بخیر / روز بخیر", en: "Good morning" },
  "arrivederla": { fa: "خداحافظ (محترمانه)", en: "Goodbye (formal)" },
  "io": { fa: "من", en: "I" },
  "mi": { fa: "خودم را", en: "myself" },
  "chiamo": { fa: "نام دارم", en: "am named" },
  "tu": { fa: "تو", en: "you" },
  "come": { fa: "چطور / چه", en: "how / what" },
  "ti": { fa: "خودت را", en: "yourself" },
  "chiami": { fa: "نام داری", en: "are named" },
  "lei": { fa: "شما (محترمانه) / او (مؤنث)", en: "You (formal) / She" },
  "si": { fa: "خودش را / خودتان را", en: "oneself" },
  "chiama": { fa: "نام دارد / نام دارید", en: "is named" },
  "piacere": { fa: "خوشبختم", en: "Nice to meet you" },
  "sono": { fa: "هستم / هستند (فعل essere)", en: "am / are" },
  "sei": { fa: "هستی (فعل essere)", en: "are (you)" },
  "è": { fa: "است / هستید محترمانه", en: "is / are (formal)" },
  "di": { fa: "اهلِ / از", en: "from / of" },
  "dove": { fa: "کجا", en: "where" },
  "abito": { fa: "زندگی می‌کنم", en: "I live" },
  "a": { fa: "در (برای شهرها)", en: "in (cities)" }
};

const LESSON_1_STAGES = [
  {
    step: 1, titleFa: "۱. الفبا و تلفظ C و G", titleEn: "1. Alphabet & C/G",
    introFa: "در ایتالیایی <b>C</b> قبل از <b>e / i</b> صدای «چ» می‌دهد (<i>Ciao</i>)، اما قبل از <b>a / o / u / h</b> صدای «ک» می‌دهد (<i>Caffè, Chiamo</i>).",
    introEn: "<b>C</b> before <b>e/i</b> sounds like 'ch' (<i>Ciao</i>), but before <b>a/o/u/h</b> sounds like 'k' (<i>Caffè, Chiamo</i>).",
    questions: [
      {
        id: "s1_q1", type: "mcq",
        qFa: "کلمه «Chiamo» (نام دارم) در ایتالیایی چطور تلفظ می‌شود؟",
        qEn: "How is 'Chiamo' pronounced in Italian?",
        options: [
          { text: "کیامو (با صدای ک)", ok: true, exp: "آفرین! ترکیب Ch همیشه صدای «ک» می‌دهد." },
          { text: "چیامو (با صدای چ)", ok: false, exp: "دقت کن! وجود حرف h بعد از C صدای آن را به «ک» تبدیل می‌کند." }
        ],
        leitnerCard: { id: "c_chiamo", it: "Io mi chiamo...", fa: "اسم من ... است (تلفظ: می کیامو)" }
      },
      {
        id: "s1_q2", type: "mcq",
        qFa: "کدام کلمه زیر با صدای «چ» شروع می‌شود؟",
        qEn: "Which word starts with a soft 'Ch' sound?",
        options: [
          { text: "Cinque (عدد ۵)", ok: true, exp: "عالی! چون بعد از C حرف i آمده، «چینکُوئه» خوانده می‌شود." },
          { text: "Come (چطور)", ok: false, exp: "چون بعد از C حرف o آمده، «کُمه» با صدای ک خوانده می‌شود." }
        ],
        leitnerCard: { id: "c_cinque", it: "Cinque (5)", fa: "پنج (تلفظ: چینکُوئه)" }
      }
    ]
  },
  {
    step: 2, titleFa: "۲. سلام و احوالپرسی رسمی و دوستانه", titleEn: "2. Greetings",
    introFa: "• <b>Ciao:</b> سلام و خداحافظ دوستانه<br>• <b>Buongiorno:</b> صبح/روز بخیر<br>• <b>ArrivederLa:</b> خداحافظی رسمی",
    introEn: "Ciao (Informal) | Buongiorno (Good morning) | ArrivederLa (Formal Goodbye)",
    questions: [
      {
        id: "s2_q1", type: "mcq",
        qFa: "هنگام خروج از اتاق یک استاد دانشگاه، کدام خداحافظی مناسب است؟",
        qEn: "When leaving a professor's office, which goodbye is appropriate?",
        options: [
          { text: "ArrivederLa, professore!", ok: true, exp: "کاملاً درست! ArrivederLa فرم رسمی خداحافظی است." },
          { text: "Ciao, professore!", ok: false, exp: "اشتباه! Ciao فقط برای دوستان و افراد صمیمی است." }
        ],
        leitnerCard: { id: "c_arrivederla", it: "ArrivederLa", fa: "خداحافظ (محترمانه و رسمی)" }
      },
      {
        id: "s2_q2", type: "sentence",
        qFa: "جمله «صبح بخیر آقای رُسی» را به ایتالیایی بساز یا تایپ کن:",
        qEn: "Build or type: 'Good morning Mr. Rossi'",
        words: ["Buongiorno", "signor", "Rossi", "Ciao"],
        accepted: ["Buongiorno signor Rossi", "Buongiorno, signor Rossi!"],
        leitnerCard: { id: "c_buongiorno", it: "Buongiorno, signor Rossi", fa: "صبح بخیر آقای رسی" }
      }
    ]
  },
  {
    step: 3, titleFa: "۳. دیالوگ اول و معرفی خود", titleEn: "3. Dialogue 1 & Introductions",
    introFa: "روی هر کلمه آبی کلیک کن تا معنی و تلفظش را ببینی:<br><div style='margin-top:8px; direction:ltr; text-align:left;'><b>Marco:</b> <span class='it-word' onclick='popWord(\"Ciao\")'>Ciao</span> <span class='it-word' onclick='popWord(\"io\")'>io</span> <span class='it-word' onclick='popWord(\"mi\")'>mi</span> <span class='it-word' onclick='popWord(\"chiamo\")'>chiamo</span> Marco.<br><b>Elena:</b> <span class='it-word' onclick='popWord(\"Piacere\")'>Piacere</span>, <span class='it-word' onclick='popWord(\"io\")'>io</span> <span class='it-word' onclick='popWord(\"sono\")'>sono</span> Elena.</div>",
    introEn: "Tap any blue word for instant translation:",
    questions: [
      {
        id: "s3_q1", type: "sentence",
        qFa: "جمله «سلام، اسم من مارکو است» را به ایتالیایی بساز (تمام حالات با Io یا بدون Io و با Sono یا Mi chiamo پذیرفته می‌شود):",
        qEn: "Write in Italian: 'Hi, my name is Marco'",
        words: ["Ciao", "io", "mi", "chiamo", "Marco", "sono"],
        accepted: [
          "Ciao io mi chiamo Marco", "Ciao mi chiamo Marco",
          "Io mi chiamo Marco", "Mi chiamo Marco",
          "Ciao io sono Marco", "Ciao sono Marco",
          "Io sono Marco", "Sono Marco"
        ],
        leitnerCard: { id: "c_michiamo", it: "(Io) mi chiamo Marco", fa: "اسم من مارکو است" }
      }
    ]
  },
  {
    step: 4, titleFa: "۴. گرامر: صرف فعل Chiamarsi", titleEn: "4. Grammar: Verb Chiamarsi",
    introFa: "• <b>(Io) mi chiamo</b> (نام دارم)<br>• <b>(Tu) ti chiami</b> (نام داری)<br>• <b>(Lei) si chiama</b> (نام دارید / او نام دارد)",
    introEn: "mi chiamo | ti chiami | si chiama",
    questions: [
      {
        id: "s4_q1", type: "sentence",
        qFa: "جمله «اسم شما (محترمانه) چیست؟» را به ایتالیایی بنویس یا بچین:",
        qEn: "Build or type: 'What is your name (formal)?'",
        words: ["Lei", "come", "si", "chiama", "ti", "chiami"],
        accepted: ["Lei come si chiama", "Come si chiama Lei", "Come si chiama"],
        leitnerCard: { id: "c_sichiama", it: "(Lei) come si chiama?", fa: "اسم شما چیست؟ (محترمانه)" }
      }
    ]
  },
  {
    step: 5, titleFa: "۵. ملیت‌ها و مذکر/مؤنث", titleEn: "5. Nationalities & Gender",
    introFa: "صفت‌های مختوم به <b>-o</b> در حالت مؤنث به <b>-a</b> تبدیل می‌شوند (<i>iraniano / iraniana</i>)، اما صفت‌های مختوم به <b>-e</b> (مثل <i>inglese, francese</i>) برای زن و مرد یکسان‌اند!",
    introEn: "-o changes to -a for feminine, while -e stays the same for both genders.",
    questions: [
      {
        id: "s5_q1", type: "mcq",
        qFa: "اگر «سارا» اهل فرانسه باشد، کدام جمله درست است؟",
        qEn: "If Sara is from France, which sentence is correct?",
        options: [
          { text: "Sara è francese.", ok: true, exp: "آفرین! صفت‌های مختوم به -e برای مذکر و مؤنث تغییر نمی‌کنند." },
          { text: "Sara è francesa.", ok: false, exp: "اشتباه! کلمه francese برای هر دو جنس به -e ختم می‌شود." }
        ],
        leitnerCard: { id: "c_francese", it: "Lui/Lei è francese", fa: "او فرانسوی است (یکسان برای زن و مرد)" }
      }
    ]
  },
  {
    step: 6, titleFa: "۶. گرامر: فعل Essere (بودن)", titleEn: "6. Grammar: Verb Essere",
    introFa: "• <b>Io sono</b> (من هستم) | <b>Tu sei</b> (تو هستی) | <b>Lui / Lei è</b> (او است / شما هستید)",
    introEn: "Io sono | Tu sei | Lui/Lei è",
    questions: [
      {
        id: "s6_q1", type: "sentence",
        qFa: "جمله «تو اهل کجایی؟» را به ایتالیایی بساز (با Tu یا بدون Tu پذیرفته می‌شود):",
        qEn: "Build or type: 'Where are you from?'",
        words: ["Di", "dove", "sei", "tu", "sono"],
        accepted: ["Di dove sei", "Tu di dove sei", "Di dove sei tu"],
        leitnerCard: { id: "c_didovesei", it: "Di dove sei?", fa: "اهل کجایی؟" }
      }
    ]
  },
  {
    step: 7, titleFa: "۷. اعداد ۰ تا ۲۰ (I Numeri)", titleEn: "7. Numbers 0 to 20",
    introFa: "1 uno | 2 due | 3 tre | 4 quattro | 5 cinque | 6 sei | 7 sette | 8 otto | 9 nove | 10 dieci | 12 dodici | 20 venti",
    introEn: "Numbers 0-20 in Italian",
    questions: [
      {
        id: "s7_q1", type: "mcq",
        qFa: "معادل ایتالیایی اعداد «۵ - ۸ - ۱۲» کدام است؟",
        qEn: "Which option is '5 - 8 - 12' in Italian?",
        options: [
          { text: "cinque - otto - dodici", ok: true, exp: "کاملاً درست!" },
          { text: "quattro - sette - undici", ok: false, exp: "این گزینه ۴، ۷ و ۱۱ است." }
        ],
        leitnerCard: { id: "c_numeri", it: "cinque (5), otto (8), dodici (12)", fa: "اعداد ۵، ۸ و ۱۲ به ایتالیایی" }
      }
    ]
  },
  {
    step: 8, titleFa: "۸. اصالت (di) در برابر سکونت (a)", titleEn: "8. Origin (di) vs Residence (a)",
    introFa: "• <b>Sono di + شهر</b> = اصالتاً اهلِ آن شهر هستم.<br>• <b>Abito a + شهر</b> = در آن شهر زندگی می‌کنم.",
    introEn: "Sono di + city (origin) vs Abito a + city (residence).",
    questions: [
      {
        id: "s8_q1", type: "mcq",
        qFa: "برای گفتن «در رم زندگی می‌کنم» کدام گزینه درست است؟",
        qEn: "How do you say 'I live in Rome'?",
        options: [
          { text: "Abito a Roma", ok: true, exp: "آفرین! بعد از فعل abitare برای شهرها همیشه از حرف اضافه a استفاده می‌کنیم." },
          { text: "Abito di Roma", ok: false, exp: "اشتباه! حرف اضافه di همراه با essere (Sono di Roma) می‌آید." }
        ],
        leitnerCard: { id: "c_abitoa", it: "Abito a Roma", fa: "در رم زندگی می‌کنم" }
      }
    ]
  },
  {
    step: 9, titleFa: "۹. کارگاه جمله‌سازی پیشرفته", titleEn: "9. Advanced Sentence Workshop",
    introFa: "روی کلمات ضربه بزن یا مستقیم در کادر تایپ کن. تمام فرم‌های صحیح ایتالیایی پذیرفته می‌شوند!",
    introEn: "Build or type the sentence. All valid Italian variations are accepted!",
    questions: [
      {
        id: "s9_q1", type: "sentence",
        qFa: "جمله «من اهل میلان هستم اما در رم زندگی می‌کنم» را بساز یا تایپ کن:",
        qEn: "Translate: 'I am from Milan, but I live in Rome'",
        words: ["Io", "sono", "di", "Milano", "ma", "abito", "a", "Roma"],
        accepted: [
          "Io sono di Milano ma abito a Roma",
          "Sono di Milano ma abito a Roma",
          "Io sono di Milano ma io abito a Roma",
          "Io abito a Roma ma sono di Milano",
          "Abito a Roma ma sono di Milano"
        ],
        leitnerCard: { id: "c_milanoroma", it: "(Io) sono di Milano, ma abito a Roma", fa: "اهل میلان هستم اما در رم زندگی می‌کنم" }
      }
    ]
  },
  {
    step: 10, titleFa: "۱۰. آزمون جامع پایان درس ۱", titleEn: "10. Unit 1 Final Check",
    introFa: "به سوال پایانی درس ۱ پاسخ بده تا قفل یونیت بعدی باز شود!",
    introEn: "Complete the final check of Unit 1!",
    questions: [
      {
        id: "s10_q1", type: "sentence",
        qFa: "جمله «من ایرانی هستم» (مذکر یا مؤنث) را به ایتالیایی بنویس:",
        qEn: "Write in Italian: 'I am Iranian'",
        words: ["Io", "sono", "iraniano", "iraniana"],
        accepted: ["Io sono iraniano", "Sono iraniano", "Io sono iraniana", "Sono iraniana"],
        leitnerCard: { id: "c_iraniano", it: "(Io) sono iraniano / iraniana", fa: "من ایرانی هستم" }
      }
    ]
  }
];

const UNITS_META = [
  { id: 1, color: "#58CC02", titleFa: "یونیت ۱: آشنایی و سلام (Primi contatti)", titleEn: "Unit 1: Primi contatti" },
  { id: 2, color: "#1CB0F6", titleFa: "یونیت ۲: من و دیگران (Io e gli altri)", titleEn: "Unit 2: Io e gli altri" },
  { id: 3, color: "#CE82FF", titleFa: "یونیت ۳: در کافه و رستوران (Buon appetito!)", titleEn: "Unit 3: Buon appetito!" },
  { id: 4, color: "#FF9600", titleFa: "یونیت ۴: اوقات فراغت (Tempo libero)", titleEn: "Unit 4: Tempo libero" },
  { id: 5, color: "#FF4B4B", titleFa: "یونیت ۵: در هتل و سفر (In albergo)", titleEn: "Unit 5: In albergo" }
];

/* ================= 3. STATE & LEITNER ENGINE ================= */
let state = {
  isLoggedIn: true,
  name: "erfan pourmirzaei",
  username: "erfan_pm",
  email: "erfanpourmirzaee@gmail.com",
  bio: "Learning Italian with Nuovo Espresso",
  lang: "fa",
  tab: "map",
  subpageTitle: "",
  unlockedUnit: 1,
  unlockedStage: 1,
  activeUnit: 1,
  activeStage: 1,
  xp: 754,
  streak: 11,
  geminiKey: "",
  soundEffects: true,
  leitnerCards: [
    { id: "c_michiamo", it: "(Io) mi chiamo Marco", fa: "اسم من مارکو است (Io اختیاری)", box: 1, ef: 2.5, interval: 0, due: 0 },
    { id: "c_didovesei", it: "Di dove sei?", fa: "اهل کجایی؟", box: 1, ef: 2.5, interval: 0, due: 0 },
    { id: "c_abitoa", it: "Abito a Roma", fa: "در رم زندگی می‌کنم", box: 2, ef: 2.5, interval: 1, due: 0 }
  ],
  chatHistory: [
    { role: "ai", text: "Ciao Erfan! من معلم هوشمند زنده زبان ایتالیایی تو هستم. هر سوالی درباره گرامر کتاب Nuovo Espresso، صرف افعال یا مکالمه داری ازم بپرس!" }
  ]
};

let stageSession = {
  queue: [], currentIndex: 0, mistakesCount: 0, pickedWords: [], typedInput: "", answeredCurrent: false
};
let leitnerFlipped = false;

function loadState() {
  try {
    const s = localStorage.getItem("espresso_svg_v5");
    if (s) state = { ...state, ...JSON.parse(s) };
  } catch (e) {}
}
function saveState() {
  try { localStorage.setItem("espresso_svg_v5", JSON.stringify(state)); } catch (e) {}
}
function t(fa, en) { return state.lang === "fa" ? fa : en; }

function speakIt(text) {
  if (!state.soundEffects || !('speechSynthesis' in window)) return;
  try {
    window.speechSynthesis.cancel();
    const u = new SpeechSynthesisUtterance(text.replace(/[()]/g, ""));
    u.lang = "it-IT";
    u.rate = 0.88;
    window.speechSynthesis.speak(u);
  } catch (e) {}
}

/* ================= 4. VALIDATOR & SM-2 LEITNER ================= */
function normalizeItalian(str) {
  return (str || "")
    .toLowerCase()
    .replace(/[.,?!;:'"«»()]/g, " ")
    .replace(/è|é|e'/g, "e")
    .replace(/ì|i'/g, "i")
    .replace(/ò|o'/g, "o")
    .replace(/ù|u'/g, "u")
    .replace(/à|a'/g, "a")
    .replace(/\s+/g, " ")
    .trim();
}

function isSentenceCorrect(userRaw, acceptedList) {
  const cleanUser = normalizeItalian(userRaw);
  if (!cleanUser) return false;
  const stripPronoun = (s) => s.replace(/\b(io|tu|lui|lei)\b/g, "").replace(/\s+/g, " ").trim();
  for (let acc of acceptedList) {
    const cleanAcc = normalizeItalian(acc);
    if (cleanUser === cleanAcc || stripPronoun(cleanUser) === stripPronoun(cleanAcc)) return true;
  }
  return false;
}

function autoAddToLeitner(cardObj, wasWrong = false) {
  if (!cardObj || !cardObj.id) return;
  const idx = state.leitnerCards.findIndex(c => c.id === cardObj.id);
  if (idx === -1) {
    state.leitnerCards.push({ id: cardObj.id, it: cardObj.it, fa: cardObj.fa, box: 1, ef: 2.5, interval: 0, due: 0 });
  } else if (wasWrong) {
    state.leitnerCards[idx].box = 1;
    state.leitnerCards[idx].interval = 0;
    state.leitnerCards[idx].due = 0;
  }
  saveState();
}

function rateLeitnerCard(cardId, ratingLevel) {
  const card = state.leitnerCards.find(c => c.id === cardId);
  if (!card) return;
  const now = Date.now();
  const DAY_MS = 86400000;

  if (ratingLevel === 0) {
    card.box = 1; card.interval = 0; card.ef = Math.max(1.3, (card.ef || 2.5) - 0.2); card.due = now;
  } else if (ratingLevel === 1) {
    card.box = 2; card.interval = 1; card.ef = Math.max(1.3, (card.ef || 2.5) - 0.15); card.due = now + DAY_MS;
  } else if (ratingLevel === 2) {
    card.box = Math.min(5, (card.box || 1) + 1);
    card.interval = card.interval === 0 ? 3 : Math.round(card.interval * (card.ef || 2.5));
    card.due = now + card.interval * DAY_MS;
  } else if (ratingLevel === 3) {
    card.box = Math.min(5, (card.box || 1) + 2);
    card.ef = (card.ef || 2.5) + 0.15;
    card.interval = card.interval === 0 ? 7 : Math.round(card.interval * card.ef * 1.3);
    card.due = now + card.interval * DAY_MS;
  }

  state.xp += 5;
  leitnerFlipped = false;
  saveState();
  render();
}

function getDueLeitnerCards() {
  const now = Date.now();
  return state.leitnerCards.filter(c => (c.due || 0) <= now);
}

/* ================= 5. RENDER ENGINE ================= */
function render() {
  const app = document.getElementById("app");
  document.documentElement.dir = state.lang === "fa" ? "rtl" : "ltr";

  // Populate Bottom Sheet with Custom Vector Icons
  document.getElementById("moreSheetContent").innerHTML = `
    <div class="sheet-item" onclick="openTab('profile')">${ICONS.profileBlue} <span>Profile</span></div>
    <div class="sheet-item" onclick="openTab('tutor')">${ICONS.videoCall} <span>Video Call / AI Tutor</span></div>
    <div class="sheet-item" onclick="openTab('leitner')">${ICONS.dumbbell} <span>Practice Hub (Leitner)</span></div>
    <div class="sheet-item" onclick="openTab('settings')">${ICONS.gear} <span>Settings</span></div>
  `;

  if (!state.isLoggedIn) {
    app.innerHTML = `
      <div class="view-container" style="display:flex; flex-direction:column; justify-content:center; min-height:92vh; text-align:center;">
        <div style="margin-bottom:14px;">${ICONS.flagIt}</div>
        <div class="title-lg" style="justify-content:center; font-size:1.5rem;">Nuovo Espresso Pro</div>
        <div class="subtitle">${t("ورود به حساب کاربری یا ساخت پروفایل جدید", "Sign in or create your profile")}</div>
        <input id="loginName" class="input-box" placeholder="Full Name" value="${state.name}" />
        <input id="loginUser" class="input-box" placeholder="Username" value="${state.username}" />
        <input id="loginEmail" class="input-box" placeholder="Email" value="${state.email}" />
        <div style="display:flex; gap:8px; margin:8px 0;">
          <button class="btn ${state.lang==='fa'?'btn-green':'btn-outline'}" onclick="state.lang='fa'; render();">فارسی</button>
          <button class="btn ${state.lang==='en'?'btn-green':'btn-outline'}" onclick="state.lang='en'; render();">English</button>
        </div>
        <button class="btn btn-green" onclick="doSignIn()">${t("ورود به برنامه", "SIGN IN")}</button>
      </div>
    `;
    return;
  }

  const dueCount = getDueLeitnerCards().length;

  let html = `
    <header>
      <div class="flag-chip">${ICONS.flagIt} <span>${state.unlockedUnit * 10 + state.unlockedStage}</span></div>
      <div class="stats-row">
        <div class="stat-item" style="color:var(--orange);">${ICONS.fire} <span>${state.streak}</span></div>
        <div class="stat-item" style="color:var(--gold);">${ICONS.bolt} <span>${state.xp}</span></div>
        <div class="stat-item" style="color:var(--purple); cursor:pointer;" onclick="openTab('leitner')">${ICONS.cards} <span>${dueCount}</span></div>
      </div>
    </header>
  `;

  if (state.tab === "map") html += renderMapView();
  else if (state.tab === "stage") html += renderStageView();
  else if (state.tab === "leitner") html += renderLeitnerView();
  else if (state.tab === "league") html += renderLeagueView();
  else if (state.tab === "tutor") html += renderTutorView();
  else if (state.tab === "settings") html += renderSettingsView();
  else if (state.tab === "profile") html += renderProfileView();
  else if (state.tab === "subpage") html += renderSubpageView();

  // Bottom Navigation Bar with 100% Designed Vector SVGs
  html += `
    <nav class="bottom-nav">
      <button class="nav-item ${state.tab==='map'||state.tab==='stage'?'active':''}" onclick="openTab('map')">${ICONS.navHome}</button>
      <button class="nav-item ${state.tab==='leitner'?'active':''}" onclick="openTab('leitner')">
        ${ICONS.navChest}
        ${dueCount > 0 ? `<span class="nav-badge">${dueCount}</span>` : ""}
      </button>
      <button class="nav-item ${state.tab==='league'?'active':''}" onclick="openTab('league')">${ICONS.navTrophy}</button>
      <button class="nav-item ${state.tab==='tutor'?'active':''}" onclick="openTab('tutor')">${ICONS.navBot}</button>
      <button class="nav-item ${['settings','profile','subpage'].includes(state.tab)?'active':''}" onclick="openMoreSheet()">${ICONS.navMore}</button>
    </nav>
  `;

  app.innerHTML = html;
}

/* ================= 6. TAB VIEWS ================= */
function renderMapView() {
  let out = `<div class="view-container">`;
  UNITS_META.forEach(u => {
    const unlocked = u.id <= state.unlockedUnit;
    out += `
      <div class="unit-header" style="background:${u.color};">
        <div>
          <div style="font-weight:800; font-size:1rem;">${t(u.titleFa, u.titleEn)}</div>
          <div style="font-size:0.78rem; opacity:0.9;">${t("۱۰ مرحله + همگام‌سازی خودکار با لایتنر", "10 Stages + Auto Leitner Sync")}</div>
        </div>
        <div>${unlocked ? ICONS.unlock : ICONS.lock}</div>
      </div>
      <div class="nodes-col">
    `;
    for (let s = 1; s <= 10; s++) {
      const stMeta = LESSON_1_STAGES[s - 1];
      const offset = Math.round(Math.sin(s * 0.9) * 58);
      let cls = "locked";
      let bg = "";
      let innerSvg = ICONS.lock;

      if (u.id < state.unlockedUnit || (u.id === state.unlockedUnit && s < state.unlockedStage)) {
        cls = "done";
        bg = `background:${u.color};`;
        innerSvg = ICONS.check;
      } else if (u.id === state.unlockedUnit && s === state.unlockedStage) {
        cls = "current";
        bg = `background:${u.color};`;
        innerSvg = s % 2 === 0 ? ICONS.book : ICONS.star;
      }

      out += `
        <div style="transform:translateX(${offset}px); display:flex; flex-direction:column; align-items:center;">
          <div class="map-node ${cls}" style="${bg}" onclick="startStage(${u.id}, ${s})">
            ${innerSvg}
          </div>
          <div class="node-label">${t(stMeta.titleFa, stMeta.titleEn)}</div>
        </div>
      `;
    }
    out += `</div>`;
  });
  out += `</div>`;
  return out;
}

function startStage(unitId, stageNum) {
  if (unitId > state.unlockedUnit || (unitId === state.unlockedUnit && stageNum > state.unlockedStage)) {
    alert(t("این مرحله قفل است! ابتدا مرحله فعلی را کامل کن.", "Complete the current stage first."));
    return;
  }
  state.activeUnit = unitId;
  state.activeStage = stageNum;
  const st = LESSON_1_STAGES[stageNum - 1];
  stageSession = {
    queue: st.questions.map(q => ({ ...q, isRetry: false })),
    currentIndex: 0,
    mistakesCount: 0,
    pickedWords: [],
    typedInput: "",
    answeredCurrent: false
  };
  state.tab = "stage";
  render();
  window.scrollTo(0, 0);
}

function renderStageView() {
  const st = LESSON_1_STAGES[state.activeStage - 1];
  const q = stageSession.queue[stageSession.currentIndex];

  if (!q) {
    return `
      <div class="view-container" style="text-align:center; padding-top:40px;">
        <div style="margin-bottom:14px;">${ICONS.navTrophy}</div>
        <div class="title-lg" style="justify-content:center;">${t("مرحله با موفقیت کامل شد!", "Stage Completed!")}</div>
        <div class="subtitle">
          ${t(`اشتباهات اصلاح‌شده در پایان مرحله: ${stageSession.mistakesCount} | لغات به جعبه لایتنر اضافه شدند.`, `Mistakes fixed: ${stageSession.mistakesCount} | Added to Leitner Box.`)}
        </div>
        <button class="btn btn-green" onclick="finishStageAndUnlock()">${t("دریافت امتیاز و ادامه", "Claim XP & Continue")}</button>
      </div>
    `;
  }

  let html = `
    <div class="view-container">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
        <button class="btn-outline" style="padding:6px 14px; border-radius:10px; cursor:pointer; font-weight:800;" onclick="openTab('map')">✕ ${t("خروج", "Exit")}</button>
        <span style="font-size:0.8rem; font-weight:800; color:${q.isRetry ? 'var(--orange)' : 'var(--green)'};">
          ${q.isRetry ? t("مرور سوالِ اشتباهِ آخر مرحله", "Mistake Review") : `سوال ${stageSession.currentIndex + 1} از ${stageSession.queue.length}`}
        </span>
      </div>

      <div class="card">
        <div class="title-lg">${ICONS.book} <span>${t(st.titleFa, st.titleEn)}</span></div>
        <div id="wordPopup" class="word-pop" style="display:none;"></div>
        <div class="subtitle" style="background:#131F24; padding:10px; border-radius:12px; border:1px solid var(--border);">${t(st.introFa, st.introEn)}</div>

        ${q.isRetry ? `<div style="background:rgba(255,150,0,0.15); border:1.5px solid var(--orange); color:var(--gold); padding:8px 12px; border-radius:10px; font-size:0.8rem; font-weight:800; margin-bottom:10px;">این سوال را قبلاً اشتباه زده بودی؛ دوباره پاسخ بده تا تثبیت شود!</div>` : ""}

        <div style="font-weight:800; font-size:0.96rem; margin-bottom:12px; color:#fff;">
          ${t(q.qFa, q.qEn)}
        </div>
  `;

  if (q.type === "mcq") {
    html += q.options.map((o, i) => `
      <button class="opt-btn" id="qOpt${i}" onclick="submitMcqAnswer(${i})">${o.text}</button>
    `).join("");
  } else if (q.type === "sentence") {
    const builtSentence = stageSession.pickedWords.join(" ");
    html += `
      <div class="sentence-slot">${builtSentence || t("روی کلمات زیر بزن یا در کادر پایین تایپ کن...", "Tap words below or type freely...")}</div>
      <div class="chip-pool">
        ${q.words.map(w => `<button class="chip" onclick="tapSentenceChip('${w}')">${w}</button>`).join("")}
      </div>
      <input class="input-box" style="direction:ltr; text-align:left;" placeholder="Type Italian sentence here..." value="${stageSession.typedInput}" oninput="stageSession.typedInput=this.value" />
      <div style="display:flex; gap:8px;">
        <button class="btn btn-outline" style="width:35%;" onclick="stageSession.pickedWords=[]; stageSession.typedInput=''; render();">${t("پاک کردن", "Clear")}</button>
        <button class="btn btn-green" style="width:65%;" onclick="submitSentenceAnswer()">${t("بررسی پاسخ", "Check Answer")}</button>
      </div>
    `;
  }

  html += `<div id="qFeedback" class="feedback"></div></div></div>`;
  return html;
}

function popWord(w) {
  speakIt(w);
  const box = document.getElementById("wordPopup");
  const entry = WORD_DICT[w.toLowerCase()];
  box.style.display = "flex";
  box.innerHTML = `
    <span><b style="color:var(--blue);">${w}</b> = ${entry ? t(entry.fa, entry.en) : w}</span>
    <button class="audio-circle" style="width:32px; height:32px;" onclick="speakIt('${w}')">${ICONS.speaker}</button>
  `;
}

function tapSentenceChip(w) {
  speakIt(w);
  stageSession.pickedWords.push(w);
  render();
}

function submitMcqAnswer(optIdx) {
  if (stageSession.answeredCurrent) return;
  stageSession.answeredCurrent = true;
  const q = stageSession.queue[stageSession.currentIndex];
  const chosen = q.options[optIdx];
  const btn = document.getElementById("qOpt" + optIdx);
  const fb = document.getElementById("qFeedback");

  if (chosen.ok) {
    btn.classList.add("correct");
    speakIt(chosen.text.split("(")[0]);
    autoAddToLeitner(q.leitnerCard, false);
    fb.className = "feedback show ok";
    fb.innerHTML = `${chosen.exp}<br><button class="btn btn-green" onclick="nextStageQuestion()">${t("ادامه", "Continue")}</button>`;
  } else {
    btn.classList.add("wrong");
    stageSession.mistakesCount++;
    autoAddToLeitner(q.leitnerCard, true);
    stageSession.queue.push({ ...q, isRetry: true });
    fb.className = "feedback show err";
    fb.innerHTML = `${chosen.exp}<br><small>این سوال به <b>جعبه لایتنر (خانه ۱)</b> رفت و در <b>پایان همین مرحله</b> هم تکرار می‌شود.</small><br><button class="btn btn-outline" onclick="nextStageQuestion()">${t("متوجه شدم (ادامه)", "Continue")}</button>`;
  }
}

function submitSentenceAnswer() {
  if (stageSession.answeredCurrent) return;
  const q = stageSession.queue[stageSession.currentIndex];
  const userText = (stageSession.typedInput.trim() || stageSession.pickedWords.join(" ")).trim();
  if (!userText) return;

  stageSession.answeredCurrent = true;
  const fb = document.getElementById("qFeedback");

  if (isSentenceCorrect(userText, q.accepted)) {
    speakIt(userText);
    autoAddToLeitner(q.leitnerCard, false);
    fb.className = "feedback show ok";
    fb.innerHTML = `${t("آفرین! جمله‌ات کاملاً درست است.", "Correct!")}<br><small>فرم‌های مجاز: <b style="direction:ltr; display:inline-block;">${q.accepted.slice(0,2).join(" / ")}</b></small><br><button class="btn btn-green" onclick="nextStageQuestion()">${t("ادامه", "Continue")}</button>`;
  } else {
    stageSession.mistakesCount++;
    autoAddToLeitner(q.leitnerCard, true);
    stageSession.queue.push({ ...q, isRetry: true });
    fb.className = "feedback show err";
    fb.innerHTML = `${t("جمله هنوز دقیق نیست!", "Not quite right!")}<br>فرم صحیح: <b style="direction:ltr; display:inline-block;">${q.accepted[0]}</b><br><button class="btn btn-outline" onclick="nextStageQuestion()">${t("ادامه", "Continue")}</button>`;
  }
}

function nextStageQuestion() {
  stageSession.currentIndex++;
  stageSession.pickedWords = [];
  stageSession.typedInput = "";
  stageSession.answeredCurrent = false;
  render();
}

function finishStageAndUnlock() {
  state.xp += 30;
  if (state.activeUnit === state.unlockedUnit && state.activeStage === state.unlockedStage) {
    if (state.unlockedStage < 10) state.unlockedStage++;
    else if (state.unlockedUnit < 5) { state.unlockedUnit++; state.unlockedStage = 1; }
  }
  state.tab = "map";
  saveState();
  render();
}

/* ================= 7. LEITNER BOX VIEW ================= */
function renderLeitnerView() {
  const counts = [1, 2, 3, 4, 5].map(b => state.leitnerCards.filter(c => c.box === b).length);
  const dueCards = getDueLeitnerCards();
  const currentCard = dueCards[0];

  let html = `
    <div class="view-container">
      <div class="card">
        <div class="title-lg">${ICONS.navChest} <span>${t("جعبه لایتنر هوشمند (پروتکل Anki SM-2)", "Smart Leitner Box")}</span></div>
        <div class="subtitle">${t("سوالات اشتباه و لغات درس‌ها به‌صورت خودکار وارد خانه ۱ می‌شوند:", "Mistakes & lesson words automatically enter Box 1:")}</div>
        
        <div class="leitner-boxes">
          ${[1,2,3,4,5].map((b, i) => `
            <div class="l-box ${counts[i] > 0 ? 'active-box' : ''}">
              <div class="l-box-num">خانه ${b}</div>
              <div class="l-box-cnt">${counts[i]}</div>
            </div>
          `).join("")}
        </div>
  `;

  if (!currentCard) {
    html += `
        <div style="text-align:center; padding:20px 10px;">
          <div style="margin-bottom:10px;">${ICONS.navTrophy}</div>
          <div style="font-weight:800; margin-bottom:6px;">${t("تمام کارت‌های موعدِ امروز مرور شدند!", "All due cards reviewed!")}</div>
          <button class="btn btn-purple" onclick="forceDueAllLeitner()">${t("مرور مجدد همه کارت‌ها", "Review All Cards Now")}</button>
        </div>
      </div>
    </div>`;
    return html;
  }

  html += `
        <div style="background:#131F24; border:2px solid var(--purple); border-radius:16px; padding:22px 14px; text-align:center; cursor:pointer;" onclick="leitnerFlipped=true; render();">
          <div style="font-size:0.75rem; color:var(--purple); font-weight:800; margin-bottom:6px;">
            خانه فعلی: ${currentCard.box} | ضریب آسانی (EF): ${(currentCard.ef || 2.5).toFixed(2)} | فاصله: ${currentCard.interval} روز
          </div>
          <div style="font-size:1.4rem; font-weight:800; color:var(--blue); direction:ltr; margin:12px 0;">${currentCard.it}</div>
          <button class="audio-circle" onclick="event.stopPropagation(); speakIt('${currentCard.it.replace(/'/g, "\\'")}')">${ICONS.speaker}</button>
          
          ${leitnerFlipped ? `
            <div style="margin-top:14px; padding-top:12px; border-top:1px dashed var(--border); font-size:1.05rem; font-weight:800; color:var(--green);">
              ${currentCard.fa}
            </div>
          ` : `<div style="margin-top:12px; font-size:0.82rem; color:var(--gold);">برای مشاهده پاسخ روی کارت ضربه بزن</div>`}
        </div>

        ${leitnerFlipped ? `
          <div style="display:grid; grid-template-columns:1fr 1fr; gap:8px; margin-top:12px;">
            <button class="btn" style="background:var(--green); color:#fff; margin:0;" onclick="rateLeitnerCard('${currentCard.id}', 3)">کاملاً بلدم<br><small>(پرش ۲ خانه)</small></button>
            <button class="btn" style="background:var(--blue); color:#fff; margin:0;" onclick="rateLeitnerCard('${currentCard.id}', 2)">بلدم<br><small>(خانه بعد)</small></button>
            <button class="btn" style="background:var(--orange); color:#fff; margin:0;" onclick="rateLeitnerCard('${currentCard.id}', 1)">تا حدی بلدم<br><small>(فردا - خانه ۲)</small></button>
            <button class="btn" style="background:var(--red); color:#fff; margin:0;" onclick="rateLeitnerCard('${currentCard.id}', 0)">بلد نیستم<br><small>(تکرار فوری - خانه ۱)</small></button>
          </div>
        ` : ""}
      </div>
    </div>
  `;
  return html;
}

function forceDueAllLeitner() {
  state.leitnerCards.forEach(c => c.due = 0);
  saveState();
  render();
}

/* ================= 8. AMETHYST LEAGUE VIEW (Custom Vector Trophies) ================= */
function renderLeagueView() {
  const players = [
    { name: "Farshid Asgarloo", flag: ICONS.flagDe + " 10", xp: 835, initials: "FA", color: "#1CB0F6", me: false },
    { name: state.name, flag: ICONS.flagIt + " " + state.streak, xp: state.xp, initials: "EP", color: "#58CC02", me: true },
    { name: "MELİH ALTUN", flag: ICONS.flagIt + " 12", xp: 489, initials: "MA", color: "#FF9600", me: false },
    { name: "Perrin", flag: ICONS.flagUs + " 8", xp: 372, initials: "PE", color: "#CE82FF", me: false },
    { name: "Ne olli1n", flag: ICONS.flagUs + " 6", xp: 339, initials: "NO", color: "#FF4B4B", me: false },
    { name: "capa", flag: ICONS.flagUs + " 14", xp: 176, initials: "CA", color: "#1CB0F6", me: false },
    { name: "hiroshi", flag: ICONS.flagUs + " 9", xp: 140, initials: "HI", color: "#58CC02", me: false }
  ].sort((a, b) => b.xp - a.xp);

  return `
    <div class="view-container" style="direction:ltr;">
      <div class="league-header">
        <div style="font-size:1.35rem; font-weight:800; text-align:left;">Amethyst League</div>
        <div style="font-size:0.8rem; color:var(--muted); text-align:left; margin-bottom:14px;">1 DAY REMAINING</div>
        <div class="league-trophies">
          <div style="opacity:0.5; transform:scale(0.85);">${ICONS.navChest}</div>
          <div style="transform:scale(1.45); filter:drop-shadow(0 0 12px rgba(206,130,255,0.5));">${ICONS.navTrophy}</div>
          <div style="opacity:0.4; transform:scale(0.85);">${ICONS.lock}</div>
        </div>
      </div>
      ${players.map((p, idx) => `
        <div class="leader-row ${p.me ? 'me' : ''}">
          <div class="leader-left">
            <div class="rank-badge">
              ${idx === 0 ? ICONS.medal1 : (idx === 1 ? ICONS.medal2 : (idx === 2 ? ICONS.medal3 : `<span style="color:var(--green);">${idx + 1}</span>`))}
            </div>
            <div class="avatar-circle" style="background:${p.color};">${p.initials}</div>
            <div>
              <div style="font-weight:800; font-size:0.95rem;">${p.name}</div>
              <div style="font-size:0.75rem; color:var(--muted); display:flex; align-items:center; gap:5px; margin-top:2px;">${p.flag}</div>
            </div>
          </div>
          <div style="font-weight:800; color:${p.me ? 'var(--green)' : 'var(--muted)'};">${p.xp} XP</div>
        </div>
      `).join("")}
    </div>
  `;
}

/* ================= 9. REAL LIVE AI TUTOR VIEW ================= */
function renderTutorView() {
  return `
    <div class="view-container">
      <div class="card">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
          <div class="title-lg" style="margin:0;">${ICONS.navBot} <span>${t("معلم هوشمند زنده (AI Tutor)", "Live AI Italian Tutor")}</span></div>
          <span style="font-size:0.72rem; background:rgba(88,204,2,0.18); color:var(--green); padding:3px 8px; border-radius:8px; font-weight:800;">ONLINE</span>
        </div>
        <div class="subtitle">${t("سوالات گرامری یا تمرین مکالمه درس‌های Nuovo Espresso را مستقیم از هوش مصنوعی بپرس:", "Ask anything about Nuovo Espresso or practice Italian conversation:")}</div>
        
        <div id="aiChatBox" style="max-height:320px; overflow-y:auto; display:flex; flex-direction:column; gap:10px; margin-bottom:12px; padding:6px;">
          ${state.chatHistory.map(m => `
            <div style="align-self:${m.role==='user'?'flex-start':'flex-end'}; max-width:88%; background:${m.role==='user'?'#283B44':'#131F24'}; border:1.5px solid ${m.role==='user'?'var(--blue)':'var(--green)'}; padding:10px 12px; border-radius:14px; font-size:0.88rem; line-height:1.6;">
              <b>${m.role === 'user' ? state.name : 'AI Tutor'}:</b><br>${m.text}
            </div>
          `).join("")}
        </div>

        <div style="display:flex; gap:8px;">
          <input id="aiPromptInp" class="input-box" style="margin:0;" placeholder="${t('سوالت را بنویس...', 'Ask in Persian, English, or Italian...')}" onkeydown="if(event.key==='Enter') sendLiveAIMessage()" />
          <button class="btn btn-green" style="width:90px; margin:0;" id="aiSendBtn" onclick="sendLiveAIMessage()">ارسال</button>
        </div>
      </div>
    </div>
  `;
}

async function sendLiveAIMessage() {
  const inp = document.getElementById("aiPromptInp");
  const btn = document.getElementById("aiSendBtn");
  const q = inp.value.trim();
  if (!q) return;

  state.chatHistory.push({ role: "user", text: q });
  inp.value = "";
  render();
  btn.disabled = true;
  btn.innerText = "...";

  const sysPrompt = "You are an expert Italian language teacher specializing in the book 'Nuovo Espresso'. Explain clearly in Persian with Italian examples.";

  try {
    let replyText = "";
    if (state.geminiKey && state.geminiKey.trim().length > 10) {
      const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${state.geminiKey.trim()}`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ contents: [{ parts: [{ text: sysPrompt + "\n\nUser: " + q }] }] })
      });
      const data = await res.json();
      replyText = data?.candidates?.[0]?.content?.parts?.[0]?.text || "";
    }
    if (!replyText) {
      const res = await fetch("https://text.pollinations.ai/", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          messages: [{ role: "system", content: sysPrompt }, { role: "user", content: q }],
          model: "openai"
        })
      });
      replyText = await res.text();
    }
    state.chatHistory.push({ role: "ai", text: replyText.replace(/\n/g, "<br>") });
  } catch (err) {
    state.chatHistory.push({ role: "ai", text: "اتصال به اینترنت برقرار نیست یا سرور پاسخ نداد." });
  }

  saveState();
  render();
}

/* ================= 10. SETTINGS & PROFILE VIEWS ================= */
function renderSettingsView() {
  return `
    <div class="view-container" style="direction:ltr;">
      <div style="display:flex; justify-content:space-between; align-items:center; padding-bottom:12px; border-bottom:2px solid var(--border);">
        <div style="font-size:1.15rem; font-weight:800; color:var(--muted); margin:0 auto;">Settings</div>
        <div style="color:var(--blue); font-weight:800; cursor:pointer;" onclick="openTab('map')">DONE</div>
      </div>

      <div class="settings-group-title">Account</div>
      <div class="settings-list">
        <div class="settings-row" onclick="openSettingsItem('Preferences')"><span>Preferences</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openTab('profile')"><span>Profile</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Notifications')"><span>Notifications</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Courses')"><span>Courses</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Score on LinkedIn')"><span>Score on LinkedIn</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Duolingo for Schools')"><span>Espresso for Schools</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Social accounts')"><span>Social accounts</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Privacy settings')"><span>Privacy settings</span><span class="settings-chevron">›</span></div>
      </div>

      <div class="settings-group-title">Support</div>
      <div class="settings-list">
        <div class="settings-row" onclick="openSettingsItem('Help Center')"><span>Help Center</span><span class="settings-chevron">›</span></div>
        <div class="settings-row" onclick="openSettingsItem('Feedback')"><span>Feedback</span><span class="settings-chevron">›</span></div>
      </div>

      <button class="btn btn-danger" style="margin-top:10px; padding:14px;" onclick="handleSignOut()">SIGN OUT</button>

      <div class="footer-links">
        <div class="footer-link" onclick="openSettingsItem('Terms')">TERMS</div>
        <div class="footer-link" onclick="openSettingsItem('Privacy Policy')">PRIVACY POLICY</div>
        <div class="footer-link" onclick="openSettingsItem('Acknowledgements')">ACKNOWLEDGEMENTS</div>
      </div>
    </div>
  `;
}

function renderProfileView() {
  return `
    <div class="view-container">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:14px;">
        <div class="title-lg" style="margin:0;">${ICONS.profileBlue} <span>${t("پروفایل کاربری", "Edit Profile")}</span></div>
        <button class="btn-outline" style="padding:6px 12px; border-radius:10px; cursor:pointer; font-weight:800;" onclick="openTab('settings')">Settings</button>
      </div>

      <div class="card">
        <div style="text-align:right; font-size:0.8rem; color:var(--muted); margin-bottom:4px;">نام کامل (Name):</div>
        <input id="profName" class="input-box" value="${state.name}" />
        <div style="text-align:right; font-size:0.8rem; color:var(--muted); margin-bottom:4px;">نام کاربری (Username):</div>
        <input id="profUser" class="input-box" value="${state.username}" />
        <div style="text-align:right; font-size:0.8rem; color:var(--muted); margin-bottom:4px;">ایمیل (Email):</div>
        <input id="profEmail" class="input-box" value="${state.email}" />
        <div style="text-align:right; font-size:0.8rem; color:var(--muted); margin-bottom:4px;">هدف آموزشی (Bio):</div>
        <input id="profBio" class="input-box" value="${state.bio}" />
        <button class="btn btn-green" onclick="saveProfileChanges()">${t("ذخیره تغییرات پروفایل", "Save Profile")}</button>
      </div>
    </div>
  `;
}

function saveProfileChanges() {
  state.name = document.getElementById("profName").value.trim() || state.name;
  state.username = document.getElementById("profUser").value.trim() || state.username;
  state.email = document.getElementById("profEmail").value.trim() || state.email;
  state.bio = document.getElementById("profBio").value.trim() || state.bio;
  saveState();
  openTab("settings");
}

function openSettingsItem(item) {
  state.subpageTitle = item;
  state.tab = "subpage";
  render();
}

function renderSubpageView() {
  const title = state.subpageTitle;
  let content = "";
  if (title === "Preferences") {
    content = `
      <div style="margin-bottom:14px;">
        <div style="font-weight:800; margin-bottom:8px;">زبان رابط کاربری (App Language):</div>
        <div style="display:flex; gap:8px;">
          <button class="btn ${state.lang==='fa'?'btn-green':'btn-outline'}" onclick="state.lang='fa'; saveState(); render();">فارسی</button>
          <button class="btn ${state.lang==='en'?'btn-green':'btn-outline'}" onclick="state.lang='en'; saveState(); render();">English</button>
        </div>
      </div>
      <div style="margin-bottom:14px;">
        <div style="font-weight:800; margin-bottom:6px;">کلید اختصاصی Gemini API (اختیاری):</div>
        <input class="input-box" placeholder="AIzaSy..." value="${state.geminiKey}" oninput="state.geminiKey=this.value; saveState();" />
      </div>
      <button class="btn btn-purple" onclick="state.unlockedStage=10; saveState(); openTab('map');">باز کردن قفل تمام مراحل درس ۱ (تست سریع)</button>
    `;
  } else {
    content = `<div class="subtitle">بخش <b>${title}</b> برای حساب کاربری (${state.email}) فعال است.</div>`;
  }

  return `
    <div class="view-container">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:14px;">
        <div class="title-lg" style="margin:0;">${title}</div>
        <button class="btn-outline" style="padding:6px 12px; border-radius:10px; cursor:pointer; font-weight:800;" onclick="openTab('settings')">Back</button>
      </div>
      <div class="card">${content}</div>
    </div>
  `;
}

function openTab(tName) {
  closeMoreSheet();
  state.tab = tName;
  render();
  window.scrollTo(0, 0);
}
function openMoreSheet() { document.getElementById("moreSheet").classList.add("show"); }
function closeMoreSheet() { document.getElementById("moreSheet").classList.remove("show"); }
function handleSignOut() {
  if (confirm("Sign out?")) { state.isLoggedIn = false; saveState(); render(); }
}
function doSignIn() {
  state.name = document.getElementById("loginName").value.trim() || "erfan pourmirzaei";
  state.username = document.getElementById("loginUser").value.trim() || "erfan_pm";
  state.email = document.getElementById("loginEmail").value.trim() || "erfanpourmirzaee@gmail.com";
  state.isLoggedIn = true;
  state.tab = "map";
  saveState();
  render();
}

loadState();
render();
</script>
</body>
</html>
