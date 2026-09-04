<!doctype html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <meta name="theme-color" content="#ff6b9d" />
  <title>文化祭 順番待ち案内</title>
  <style>
    :root {
      --pink: #ff5f96;
      --pink-dark: #e9447d;
      --coral: #ff8a65;
      --yellow: #ffd84d;
      --mint: #73e4c2;
      --ink: #3f2943;
      --muted: #856d82;
      --paper: #fffaf6;
      --white: #ffffff;
      --shadow: 0 18px 45px rgba(123, 52, 101, 0.17);
      --radius-xl: 32px;
      --radius-lg: 22px;
      --radius-md: 15px;
    }

    * { box-sizing: border-box; }

    html { min-height: 100%; }

    body {
      min-height: 100vh;
      margin: 0;
      color: var(--ink);
      font-family: -apple-system, BlinkMacSystemFont, "Hiragino Kaku Gothic ProN", "Yu Gothic", YuGothic, Meiryo, sans-serif;
      background:
        radial-gradient(circle at 9% 8%, rgba(255, 216, 77, 0.42) 0 44px, transparent 45px),
        radial-gradient(circle at 91% 23%, rgba(115, 228, 194, 0.43) 0 32px, transparent 33px),
        linear-gradient(145deg, #fff3f5 0%, #fffaf1 48%, #effcf8 100%);
      overflow-x: hidden;
    }

    body::before,
    body::after {
      position: fixed;
      z-index: -1;
      content: "";
      width: 180px;
      height: 180px;
      border-radius: 42% 58% 62% 38% / 48% 42% 58% 52%;
      opacity: 0.34;
      filter: blur(1px);
      pointer-events: none;
    }

    body::before {
      top: 62%;
      left: -70px;
      background: var(--yellow);
      transform: rotate(26deg);
    }

    body::after {
      top: 4%;
      right: -82px;
      background: var(--mint);
      transform: rotate(-25deg);
    }

    button,
    input { font: inherit; }

    button { cursor: pointer; }

    .app-shell {
      width: min(100% - 28px, 560px);
      margin: 0 auto;
      padding: 24px 0 34px;
    }

    .hero {
      position: relative;
      padding: 22px 24px 25px;
      color: var(--white);
      border-radius: var(--radius-xl);
      background: linear-gradient(135deg, var(--pink) 0%, #ff7b74 100%);
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .hero::after {
      position: absolute;
      right: -40px;
      bottom: -57px;
      width: 170px;
      height: 170px;
      border: 24px solid rgba(255, 255, 255, 0.17);
      border-radius: 50%;
      content: "";
    }

    .hero-topline {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }

    .festival-label {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      width: fit-content;
      padding: 7px 12px;
      border: 1px solid rgba(255, 255, 255, 0.45);
      border-radius: 999px;
      color: #fff;
      font-size: 0.76rem;
      font-weight: 800;
      letter-spacing: 0.08em;
      background: rgba(255, 255, 255, 0.16);
    }

    .staff-open {
      position: relative;
      z-index: 1;
      padding: 8px 11px;
      border: 1px solid rgba(255, 255, 255, 0.55);
      border-radius: 999px;
      color: #fff;
      font-size: 0.75rem;
      font-weight: 800;
      background: rgba(255, 255, 255, 0.14);
      transition: background 0.2s ease, transform 0.2s ease;
    }

    .staff-open.is-hidden { display: none; }

    .staff-open:hover,
    .staff-open:focus-visible { background: rgba(255, 255, 255, 0.28); transform: translateY(-1px); }

    h1 {
      position: relative;
      z-index: 1;
      margin: 23px 0 7px;
      font-size: clamp(1.7rem, 7vw, 2.35rem);
      line-height: 1.25;
      letter-spacing: 0.04em;
    }

    .hero-subtitle {
      position: relative;
      z-index: 1;
      margin: 0;
      color: rgba(255, 255, 255, 0.92);
      font-size: 0.9rem;
      font-weight: 600;
    }

    .ticket-card {
      position: relative;
      margin-top: 18px;
      padding: 24px 22px 23px;
      border: 3px solid rgba(255, 95, 150, 0.13);
      border-radius: var(--radius-xl);
      text-align: center;
      background: rgba(255, 255, 255, 0.89);
      box-shadow: var(--shadow);
      backdrop-filter: blur(8px);
    }

    .section-label {
      display: block;
      margin-bottom: 8px;
      color: var(--muted);
      font-size: 0.86rem;
      font-weight: 800;
      letter-spacing: 0.1em;
    }

    .ticket-number {
      display: block;
      color: var(--pink-dark);
      font-size: clamp(4.6rem, 23vw, 8rem);
      font-weight: 900;
      line-height: 0.98;
      letter-spacing: -0.05em;
    }

    .ticket-caption {
      margin: 12px 0 0;
      color: var(--muted);
      font-size: 0.85rem;
      font-weight: 700;
    }

    .status-message {
      margin: 15px 0 0;
      padding: 11px 14px;
      border-radius: var(--radius-md);
      color: #95640e;
      font-size: 0.85rem;
      font-weight: 800;
      background: #fff4c9;
    }

    .status-message.is-ready {
      color: #087b61;
      background: #d9faee;
    }

    .status-message.is-called {
      color: #fff;
      background: linear-gradient(135deg, var(--pink), var(--coral));
    }

    .ticket-entry {
      display: flex;
      gap: 8px;
      margin-top: 16px;
    }

    .ticket-entry .text-input { flex: 1; min-width: 0; }

    .ticket-entry-button {
      flex: 0 0 auto;
      min-height: 47px;
      padding: 10px 15px;
      border: 0;
      border-radius: var(--radius-md);
      color: #fff;
      font-weight: 900;
      background: linear-gradient(135deg, var(--pink), var(--coral));
    }

    .ticket-entry-help {
      margin: 8px 2px 0;
      color: var(--muted);
      font-size: 0.72rem;
      font-weight: 600;
      text-align: left;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 13px;
      margin-top: 16px;
    }

    .stat-card {
      min-width: 0;
      padding: 18px 13px 16px;
      border-radius: var(--radius-lg);
      text-align: center;
      background: var(--white);
      box-shadow: 0 9px 25px rgba(123, 52, 101, 0.1);
    }

    .stat-card.waiting {
      color: #a26800;
      background: #fff8dc;
    }

    .stat-card.current {
      color: #087b61;
      background: #e3fbf4;
    }

    .stat-label {
      display: block;
      min-height: 2.5em;
      color: inherit;
      font-size: 0.79rem;
      font-weight: 800;
      line-height: 1.35;
    }

    .stat-value {
      display: block;
      margin-top: 5px;
      color: var(--ink);
      font-size: clamp(2.2rem, 11vw, 3.9rem);
      font-weight: 900;
      line-height: 1;
    }

    .stat-unit {
      display: block;
      margin-top: 5px;
      color: var(--muted);
      font-size: 0.75rem;
      font-weight: 700;
    }

    .notice {
      display: flex;
      align-items: flex-start;
      gap: 10px;
      margin-top: 16px;
      padding: 14px 15px;
      border: 1px dashed rgba(63, 41, 67, 0.2);
      border-radius: var(--radius-md);
      color: var(--muted);
      font-size: 0.78rem;
      font-weight: 600;
      line-height: 1.6;
      background: rgba(255, 255, 255, 0.63);
    }

    .notice-icon {
      flex: 0 0 auto;
      width: 23px;
      height: 23px;
      border-radius: 50%;
      color: #fff;
      font-size: 0.82rem;
      font-weight: 900;
      line-height: 23px;
      text-align: center;
      background: var(--coral);
    }

    .footer-note {
      margin: 17px 0 0;
      color: var(--muted);
      font-size: 0.73rem;
      line-height: 1.7;
      text-align: center;
    }

    .footer-note code {
      padding: 2px 5px;
      border-radius: 5px;
      color: var(--pink-dark);
      background: #ffe7ee;
    }

    .modal-backdrop {
      position: fixed;
      inset: 0;
      z-index: 10;
      display: grid;
      place-items: center;
      padding: 18px;
      background: rgba(53, 31, 54, 0.48);
      opacity: 0;
      visibility: hidden;
      transition: opacity 0.2s ease, visibility 0.2s ease;
    }

    .modal-backdrop.is-open {
      opacity: 1;
      visibility: visible;
    }

    .modal {
      width: min(100%, 440px);
      max-height: min(88vh, 680px);
      overflow: auto;
      padding: 24px 20px 20px;
      border-radius: 26px;
      background: var(--paper);
      box-shadow: 0 24px 80px rgba(36, 17, 37, 0.3);
      transform: translateY(14px) scale(0.98);
      transition: transform 0.2s ease;
    }

    .modal-backdrop.is-open .modal { transform: translateY(0) scale(1); }

    .modal-header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 14px;
      margin-bottom: 20px;
    }

    .modal-title {
      margin: 0;
      font-size: 1.3rem;
      line-height: 1.4;
    }

    .modal-description {
      margin: 5px 0 0;
      color: var(--muted);
      font-size: 0.78rem;
      line-height: 1.6;
    }

    .modal-close {
      display: grid;
      flex: 0 0 auto;
      place-items: center;
      width: 34px;
      height: 34px;
      border: 0;
      border-radius: 50%;
      color: var(--ink);
      font-size: 1.2rem;
      background: #f7e9ed;
    }

    .field-label {
      display: block;
      margin: 0 0 7px;
      color: var(--muted);
      font-size: 0.78rem;
      font-weight: 800;
    }

    .password-row { display: flex; gap: 8px; }

    .text-input {
      width: 100%;
      min-height: 47px;
      padding: 10px 13px;
      border: 2px solid #eadbe1;
      border-radius: var(--radius-md);
      outline: none;
      color: var(--ink);
      background: #fff;
      transition: border-color 0.2s ease, box-shadow 0.2s ease;
    }

    .text-input:focus {
      border-color: var(--pink);
      box-shadow: 0 0 0 4px rgba(255, 95, 150, 0.14);
    }

    .primary-button,
    .secondary-button,
    .danger-button {
      min-height: 47px;
      padding: 10px 15px;
      border: 0;
      border-radius: var(--radius-md);
      font-weight: 900;
      transition: transform 0.2s ease, filter 0.2s ease;
    }

    .primary-button:hover,
    .secondary-button:hover,
    .danger-button:hover { filter: brightness(0.97); transform: translateY(-1px); }

    .primary-button { color: #fff; background: linear-gradient(135deg, var(--pink), var(--coral)); }
    .secondary-button { color: var(--ink); background: #f6e8ed; }
    .danger-button { color: #b23e5f; background: #ffe1e7; }

    .login-error {
      min-height: 1.3em;
      margin: 9px 0 0;
      color: #c4315d;
      font-size: 0.78rem;
      font-weight: 800;
    }

    .admin-panel { display: none; }
    .admin-panel.is-visible { display: block; }
    .login-box.is-hidden { display: none; }

    .admin-topline {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 17px;
    }

    .login-success {
      margin: 0;
      color: #087b61;
      font-size: 0.82rem;
      font-weight: 900;
    }

    .current-edit-card {
      padding: 17px;
      border-radius: var(--radius-lg);
      background: #fff;
    }

    .edit-label {
      display: block;
      margin-bottom: 8px;
      color: var(--muted);
      font-size: 0.8rem;
      font-weight: 800;
    }

    .number-edit-row {
      display: grid;
      grid-template-columns: 50px minmax(0, 1fr) 50px;
      gap: 8px;
    }

    .step-button {
      min-height: 50px;
      border: 0;
      border-radius: var(--radius-md);
      color: var(--pink-dark);
      font-size: 1.4rem;
      font-weight: 900;
      background: #ffe5ed;
    }

    .number-input {
      min-width: 0;
      border: 2px solid #eadbe1;
      border-radius: var(--radius-md);
      color: var(--ink);
      font-size: 1.45rem;
      font-weight: 900;
      text-align: center;
      outline: none;
    }

    .number-input:focus { border-color: var(--pink); }

    .admin-actions {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 9px;
      margin-top: 12px;
    }

    .admin-help {
      margin: 14px 0 0;
      color: var(--muted);
      font-size: 0.73rem;
      line-height: 1.65;
    }

    .toast {
      position: fixed;
      right: 18px;
      bottom: 18px;
      left: 18px;
      z-index: 20;
      width: fit-content;
      max-width: calc(100% - 36px);
      margin: 0 auto;
      padding: 12px 16px;
      border-radius: 999px;
      color: #fff;
      font-size: 0.8rem;
      font-weight: 800;
      text-align: center;
      background: var(--ink);
      box-shadow: 0 10px 30px rgba(63, 41, 67, 0.25);
      opacity: 0;
      visibility: hidden;
      transform: translateY(10px);
      transition: opacity 0.2s ease, visibility 0.2s ease, transform 0.2s ease;
    }

    .toast.is-visible {
      opacity: 1;
      visibility: visible;
      transform: translateY(0);
    }

    @media (min-width: 500px) {
      .app-shell { padding-top: 36px; }
      .hero { padding: 28px 30px 30px; }
      .ticket-card { padding: 30px; }
    }
  </style>
</head>
<body>
  <main class="app-shell">
    <section class="hero" aria-labelledby="page-title">
      <div class="hero-topline">
        <div class="festival-label"><span aria-hidden="true">★</span> CULTURE FESTIVAL</div>
        <button class="staff-open" id="openStaffButton" type="button">スタッフ用</button>
      </div>
      <h1 id="page-title">順番待ち案内</h1>
      <p class="hero-subtitle">あなたの順番をスマホでチェックできます</p>
    </section>

    <section class="ticket-card" aria-labelledby="ticket-heading">
      <span class="section-label" id="ticket-heading">あなたの受付番号</span>
      <strong class="ticket-number" id="ticketNumber" aria-live="polite">--</strong>
      <p class="ticket-caption" id="ticketCaption">URLの受付番号を読み込んでいます</p>
      <p class="status-message" id="statusMessage" role="status">受付番号を確認中です</p>
      <div class="ticket-entry">
        <input class="text-input" id="ticketNumberInput" type="number" min="1" step="1" inputmode="numeric" placeholder="受付番号を入力" aria-label="受付番号を入力" />
        <button class="ticket-entry-button" id="ticketNumberSaveButton" type="button">設定する</button>
      </div>
      <p class="ticket-entry-help">受付時に渡された番号を入力してください。URLの <code>?no=20</code> からも自動設定できます。</p>
    </section>

    <section class="stats-grid" aria-label="順番待ち状況">
      <div class="stat-card waiting">
        <span class="stat-label">あと何人待ち？</span>
        <strong class="stat-value" id="waitingCount" aria-live="polite">--</strong>
        <span class="stat-unit">人</span>
      </div>
      <div class="stat-card current">
        <span class="stat-label">現在の呼び出し番号</span>
        <strong class="stat-value" id="currentNumber" aria-live="polite">1</strong>
        <span class="stat-unit">番まで呼び出し中</span>
      </div>
    </section>

    <div class="notice">
      <span class="notice-icon" aria-hidden="true">i</span>
      <span>呼び出し番号があなたの受付番号に近づいたら、会場の近くでお待ちください。</span>
    </div>

    <p class="footer-note">
      このページは受付時に案内されたURLからご利用ください。<br />
      受付番号の例：<code>?no=20</code>
    </p>
  </main>

  <div class="modal-backdrop" id="staffModal" role="dialog" aria-modal="true" aria-labelledby="staffModalTitle">
    <section class="modal">
      <div class="modal-header">
        <div>
          <h2 class="modal-title" id="staffModalTitle">スタッフ用管理画面</h2>
          <p class="modal-description">呼び出し番号と待ち人数を運営側で更新できます。</p>
        </div>
          <button class="modal-close" id="closeStaffButton" type="button" aria-label="閉じる">×</button>
      </div>

      <div class="login-box" id="loginBox">
        <label class="field-label" for="passwordInput">スタッフ用パスワード</label>
        <div class="password-row">
          <input class="text-input" id="passwordInput" type="password" autocomplete="current-password" placeholder="パスワードを入力" />
          <button class="primary-button" id="loginButton" type="button">ログイン</button>
        </div>
        <p class="login-error" id="loginError" aria-live="polite"></p>
      </div>

      <div class="admin-panel" id="adminPanel">
        <div class="admin-topline">
          <p class="login-success">スタッフ管理モード</p>
          <button class="secondary-button" id="logoutButton" type="button">閉じる</button>
        </div>
        <div class="current-edit-card">
          <label class="edit-label" for="currentNumberInput">現在の呼び出し番号</label>
          <div class="number-edit-row">
            <button class="step-button" id="decreaseButton" type="button" aria-label="1減らす">−</button>
            <input class="number-input" id="currentNumberInput" type="number" min="1" step="1" inputmode="numeric" />
            <button class="step-button" id="increaseButton" type="button" aria-label="1増やす">＋</button>
          </div>
          <div class="admin-actions">
            <button class="primary-button" id="saveButton" type="button">番号を更新</button>
            <button class="danger-button" id="resetButton" type="button">1番に戻す</button>
          </div>
          <label class="edit-label" for="waitingNumberInput" style="margin-top: 17px;">あと何人待ちか（直接設定）</label>
          <div class="password-row">
            <input class="text-input" id="waitingNumberInput" type="number" min="0" step="1" inputmode="numeric" />
            <button class="primary-button" id="saveWaitingButton" type="button">待ち人数を更新</button>
          </div>
          <p class="admin-help">待ち人数を直接設定すると、自動計算よりもこちらの値が優先して表示されます。</p>
          <p class="admin-help">更新した番号と待ち人数はブラウザの保存領域に記録され、同じブラウザで開いている別タブにも反映されます。</p>
        </div>
      </div>
    </section>
  </div>

  <div class="toast" id="toast" role="status" aria-live="polite"></div>

  <script>
    // 平文パスワードではなくSHA-256ハッシュだけを保存します。
    const STAFF_PASSWORD_HASH = "90b1fcf4a9a8105d0a83f284c28abe74edc4de793798fdf12e4c3d623e96cb12";
    const STORAGE_KEY = "bunkasai-current-call-number";
    const TICKET_STORAGE_KEY = "bunkasai-ticket-number";
    const WAITING_STORAGE_KEY = "bunkasai-waiting-override";
    const DEFAULT_CURRENT_NUMBER = 1;

    const ticketNumberElement = document.getElementById("ticketNumber");
    const ticketCaptionElement = document.getElementById("ticketCaption");
    const ticketNumberInput = document.getElementById("ticketNumberInput");
    const ticketNumberSaveButton = document.getElementById("ticketNumberSaveButton");
    const currentNumberElement = document.getElementById("currentNumber");
    const waitingCountElement = document.getElementById("waitingCount");
    const statusMessageElement = document.getElementById("statusMessage");
    const openStaffButton = document.getElementById("openStaffButton");
    const closeStaffButton = document.getElementById("closeStaffButton");
    const staffModal = document.getElementById("staffModal");
    const passwordInput = document.getElementById("passwordInput");
    const loginButton = document.getElementById("loginButton");
    const loginBox = document.getElementById("loginBox");
    const loginError = document.getElementById("loginError");
    const adminPanel = document.getElementById("adminPanel");
    const logoutButton = document.getElementById("logoutButton");
    const currentNumberInput = document.getElementById("currentNumberInput");
    const waitingNumberInput = document.getElementById("waitingNumberInput");
    const saveWaitingButton = document.getElementById("saveWaitingButton");
    const decreaseButton = document.getElementById("decreaseButton");
    const increaseButton = document.getElementById("increaseButton");
    const saveButton = document.getElementById("saveButton");
    const resetButton = document.getElementById("resetButton");
    const toast = document.getElementById("toast");

    let isStaffAuthenticated = false;
    let currentNumber = readCurrentNumber();
    let ticketNumber = readTicketNumber();
    let waitingOverride = readWaitingOverride();
    let toastTimer;

    function readTicketNumber() {
      const raw = new URLSearchParams(window.location.search).get("no");
      const parsed = Number.parseInt(raw, 10);
      if (Number.isInteger(parsed) && parsed > 0) return parsed;
      const saved = Number.parseInt(localStorage.getItem(TICKET_STORAGE_KEY), 10);
      return Number.isInteger(saved) && saved > 0 ? saved : null;
    }

    function readWaitingOverride() {
      const saved = Number.parseInt(localStorage.getItem(WAITING_STORAGE_KEY), 10);
      return Number.isInteger(saved) && saved >= 0 ? saved : null;
    }

    function readCurrentNumber() {
      const saved = Number.parseInt(localStorage.getItem(STORAGE_KEY), 10);
      return Number.isInteger(saved) && saved > 0 ? saved : DEFAULT_CURRENT_NUMBER;
    }

    function render() {
      currentNumberElement.textContent = currentNumber;
      currentNumberInput.value = currentNumber;
      ticketNumberInput.value = ticketNumber ?? "";
      waitingNumberInput.value = waitingOverride ?? (ticketNumber === null ? "" : Math.max(ticketNumber - currentNumber, 0));

      if (ticketNumber === null) {
        ticketNumberElement.textContent = "--";
        waitingCountElement.textContent = "--";
        statusMessageElement.className = "status-message";
        return;
      }

      ticketNumberElement.textContent = ticketNumber;
      ticketCaptionElement.textContent = "あなたの受付番号です";

      const waiting = waitingOverride !== null ? waitingOverride : Math.max(ticketNumber - currentNumber, 0);
      waitingCountElement.textContent = waiting;

      if (currentNumber >= ticketNumber) {
        statusMessageElement.textContent = "あなたの順番です。スタッフの案内をご確認ください！";
        statusMessageElement.className = "status-message is-called";
      } else if (waiting <= 3) {
        statusMessageElement.textContent = "もうすぐ順番です。会場の近くでお待ちください";
        statusMessageElement.className = "status-message is-ready";
      } else {
        statusMessageElement.textContent = "順番まで、もうしばらくお待ちください";
        statusMessageElement.className = "status-message";
      }
    }

    function saveTicketNumber(nextNumber) {
      const normalized = Number.parseInt(nextNumber, 10);
      if (!Number.isInteger(normalized) || normalized < 1) {
        showToast("1以上の受付番号を入力してください");
        return false;
      }
      ticketNumber = normalized;
      localStorage.setItem(TICKET_STORAGE_KEY, String(ticketNumber));
      render();
      showToast(`受付番号を ${ticketNumber} 番に設定しました`);
      return true;
    }

    function saveWaitingNumber(nextNumber) {
      if (!isStaffAuthenticated) return false;
      const normalized = Number.parseInt(nextNumber, 10);
      if (!Number.isInteger(normalized) || normalized < 0) {
        showToast("0以上の待ち人数を入力してください");
        return false;
      }
      waitingOverride = normalized;
      localStorage.setItem(WAITING_STORAGE_KEY, String(waitingOverride));
      render();
      showToast(`待ち人数を ${waitingOverride} 人に更新しました`);
      return true;
    }

    function saveCurrentNumber(nextNumber) {
      if (!isStaffAuthenticated) return false;
      const normalized = Number.parseInt(nextNumber, 10);
      if (!Number.isInteger(normalized) || normalized < 1) {
        showToast("1以上の番号を入力してください");
        return false;
      }
      currentNumber = normalized;
      localStorage.setItem(STORAGE_KEY, String(currentNumber));
      render();
      showToast(`呼び出し番号を ${currentNumber} 番に更新しました`);
      return true;
    }

    function showToast(message) {
      toast.textContent = message;
      toast.classList.add("is-visible");
      window.clearTimeout(toastTimer);
      toastTimer = window.setTimeout(() => toast.classList.remove("is-visible"), 2600);
    }

    async function hashPassword(password) {
      const data = new TextEncoder().encode(password);
      const hashBuffer = await crypto.subtle.digest("SHA-256", data);
      return Array.from(new Uint8Array(hashBuffer)).map((byte) => byte.toString(16).padStart(2, "0")).join("");
    }

    function openStaffModal() {
      staffModal.classList.add("is-open");
      if (isStaffAuthenticated) {
        adminPanel.classList.add("is-visible");
        loginBox.classList.add("is-hidden");
        currentNumberInput.focus();
      } else {
        adminPanel.classList.remove("is-visible");
        loginBox.classList.remove("is-hidden");
        passwordInput.focus();
      }
    }

    function closeStaffModal() {
      staffModal.classList.remove("is-open");
      passwordInput.value = "";
      loginError.textContent = "";
    }

    async function login() {
      const enteredHash = await hashPassword(passwordInput.value);
      if (enteredHash === STAFF_PASSWORD_HASH) {
        isStaffAuthenticated = true;
        loginBox.classList.add("is-hidden");
        adminPanel.classList.add("is-visible");
        loginError.textContent = "";
        currentNumberInput.focus();
      } else {
        loginError.textContent = "パスワードが正しくありません";
        passwordInput.select();
      }
    }

    openStaffButton.addEventListener("click", openStaffModal);
    closeStaffButton.addEventListener("click", closeStaffModal);
    ticketNumberSaveButton.addEventListener("click", () => saveTicketNumber(ticketNumberInput.value));
    ticketNumberInput.addEventListener("keydown", (event) => {
      if (event.key === "Enter") saveTicketNumber(ticketNumberInput.value);
    });
    loginButton.addEventListener("click", login);
    passwordInput.addEventListener("keydown", (event) => {
      if (event.key === "Enter") login();
    });
    saveWaitingButton.addEventListener("click", () => saveWaitingNumber(waitingNumberInput.value));
    waitingNumberInput.addEventListener("keydown", (event) => {
      if (event.key === "Enter") saveWaitingNumber(waitingNumberInput.value);
    });
    logoutButton.addEventListener("click", closeStaffModal);
    saveButton.addEventListener("click", () => saveCurrentNumber(currentNumberInput.value));
    resetButton.addEventListener("click", () => {
      currentNumberInput.value = DEFAULT_CURRENT_NUMBER;
      saveCurrentNumber(DEFAULT_CURRENT_NUMBER);
    });
    decreaseButton.addEventListener("click", () => {
      currentNumberInput.value = Math.max(1, Number.parseInt(currentNumberInput.value || currentNumber, 10) - 1);
    });
    increaseButton.addEventListener("click", () => {
      currentNumberInput.value = Number.parseInt(currentNumberInput.value || currentNumber, 10) + 1;
    });

    currentNumberInput.addEventListener("keydown", (event) => {
      if (event.key === "Enter") saveCurrentNumber(currentNumberInput.value);
    });
    staffModal.addEventListener("click", (event) => {
      if (event.target === staffModal) closeStaffModal();
    });
    document.addEventListener("keydown", (event) => {
      if (event.key === "Escape" && staffModal.classList.contains("is-open")) closeStaffModal();
    });

    window.addEventListener("storage", (event) => {
      if ([STORAGE_KEY, WAITING_STORAGE_KEY, TICKET_STORAGE_KEY].includes(event.key)) {
        currentNumber = readCurrentNumber();
        waitingOverride = readWaitingOverride();
        ticketNumber = readTicketNumber();
        render();
      }
    });

    // 同じブラウザ内のタブ間で即時反映するための補助通信。
    if ("BroadcastChannel" in window) {
      const channel = new BroadcastChannel("bunkasai-queue-channel");
      channel.addEventListener("message", (event) => {
        if (event.data && ["current-number-updated", "waiting-number-updated", "ticket-number-updated"].includes(event.data.type)) {
          currentNumber = readCurrentNumber();
          waitingOverride = readWaitingOverride();
          ticketNumber = readTicketNumber();
          render();
        }
      });
      saveButton.addEventListener("click", () => channel.postMessage({ type: "current-number-updated" }));
      resetButton.addEventListener("click", () => channel.postMessage({ type: "current-number-updated" }));
      saveWaitingButton.addEventListener("click", () => channel.postMessage({ type: "waiting-number-updated" }));
      ticketNumberSaveButton.addEventListener("click", () => channel.postMessage({ type: "ticket-number-updated" }));
    }

    render();
  </script>
</body>
</html>

<!--
  使い方
  1. このファイルをWebサーバーに置き、受付番号ごとに ?no=20 のようなURLを案内します。
  2. 例：https://example.com/bunkasai_queue.html?no=20
  3. スタッフ用ボタンを押し、パスワードを入力して管理画面を開きます。
  4. パスワードを変更する場合は、パスワードのSHA-256ハッシュを生成して、script内の STAFF_PASSWORD_HASH を置き換えます。

  注意
  平文パスワードはHTML内に保存していませんが、静的HTMLではログイン判定がブラウザ側で行われます。
  そのため、本格的な認証や不正な更新の完全防止には、サーバー側の認証APIが必要です。
  また、localStorageを利用するため、呼び出し番号は基本的に同じブラウザ内で共有されます。
  異なるスマホへ安全に共有するには、FirebaseやSupabaseなどの共有データベース／APIが必要です。
-->
前回の指定どおり、外部ライブラリなしでCSSとJavaScriptもこのファイル内に含めています。
