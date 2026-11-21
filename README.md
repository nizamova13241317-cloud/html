
<!DOCTYPE html>
<html lang="uk" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>HTML Тренажер</title>
  <style>
    :root {
      --bg: #0b1120;
      --bg-elevated: #111827;
      --surface: #172033;
      --surface-2: #1e293b;
      --border: #2a3952;
      --text: #f1f5f9;
      --text-muted: #94a3b8;
      --accent: #38bdf8;
      --accent-strong: #0284c7;
      --accent-soft: rgba(56, 189, 248, 0.14);
      --orange: #fb923c;
      --success: #22c55e;
      --success-soft: rgba(34, 197, 94, 0.14);
      --warning: #f59e0b;
      --warning-soft: rgba(245, 158, 11, 0.14);
      --danger: #f87171;
      --danger-soft: rgba(248, 113, 113, 0.14);
      --code-bg: #080d1a;
      --shadow: 0 8px 24px rgba(0, 0, 0, 0.32);
      --radius: 14px;
      --mono: ui-monospace, 'SFMono-Regular', 'JetBrains Mono', 'Roboto Mono', Menlo, Consolas, monospace;
      --sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Noto Sans', sans-serif;
    }

    html[data-theme="light"] {
      --bg: #f1f5f9;
      --bg-elevated: #ffffff;
      --surface: #ffffff;
      --surface-2: #e2e8f0;
      --border: #cbd5e1;
      --text: #0f172a;
      --text-muted: #475569;
      --accent: #0284c7;
      --accent-strong: #0369a1;
      --accent-soft: rgba(2, 132, 199, 0.12);
      --orange: #ea580c;
      --success: #16a34a;
      --success-soft: rgba(22, 163, 74, 0.12);
      --warning: #d97706;
      --warning-soft: rgba(217, 119, 6, 0.12);
      --danger: #dc2626;
      --danger-soft: rgba(220, 38, 38, 0.12);
      --code-bg: #0f172a;
      --shadow: 0 4px 16px rgba(15, 23, 42, 0.08);
    }

    *, *::before, *::after {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      max-width: 100vw;
      overflow-x: hidden;
      background-color: var(--bg);
      color: var(--text);
      font-family: var(--sans);
      font-size: 15px;
      line-height: 1.5;
      -webkit-text-size-adjust: 100%;
    }

    body {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      user-select: none;
      -webkit-user-select: none;
    }

    button, input, textarea {
      font-family: inherit;
    }

    button {
      touch-action: manipulation;
      cursor: pointer;
      border: none;
      background: none;
      color: inherit;
    }

    /* Sticky Top App Bar + Level Switcher */
    .topbar {
      position: sticky;
      top: 0;
      z-index: 30;
      background: var(--bg-elevated);
      border-bottom: 1px solid var(--border);
      padding: 10px 14px 10px;
      box-shadow: var(--shadow);
    }

    .topbar-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 10px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      min-width: 0;
    }

    .brand-badge {
      width: 36px;
      height: 36px;
      border-radius: 10px;
      background: linear-gradient(135deg, var(--accent-strong), var(--orange));
      color: #ffffff;
      display: grid;
      place-items: center;
      font-family: var(--mono);
      font-weight: 800;
      font-size: 14px;
      flex-shrink: 0;
      letter-spacing: -0.5px;
    }

    .brand-text {
      min-width: 0;
    }

    .brand-title {
      font-size: 16px;
      font-weight: 700;
      line-height: 1.2;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .brand-sub {
      font-size: 12px;
      color: var(--text-muted);
      line-height: 1.2;
    }

    .topbar-actions {
      display: flex;
      align-items: center;
      gap: 8px;
      flex-shrink: 0;
    }

    .progress-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 6px 10px;
      border-radius: 999px;
      background: var(--accent-soft);
      color: var(--accent);
      font-size: 12px;
      font-weight: 700;
      border: 1px solid rgba(56, 189, 248, 0.28);
    }

    .icon-btn {
      width: 40px;
      height: 40px;
      border-radius: 10px;
      background: var(--surface);
      border: 1px solid var(--border);
      display: grid;
      place-items: center;
      font-size: 17px;
      transition: transform 0.12s ease, background-color 0.15s ease;
    }

    .icon-btn:active {
      transform: scale(0.95);
    }

    .progress-track {
      width: 100%;
      height: 5px;
      background: var(--surface-2);
      border-radius: 999px;
      overflow: hidden;
      margin-bottom: 10px;
    }

    .progress-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, var(--accent), var(--success));
      border-radius: 999px;
      transition: width 0.3s ease;
    }

    .level-strip {
      display: flex;
      gap: 8px;
      overflow-x: auto;
      padding-bottom: 2px;
      scrollbar-width: none;
      -ms-overflow-style: none;
    }

    .level-strip::-webkit-scrollbar {
      display: none;
    }

    .level-tab {
      flex: 0 0 auto;
      min-width: 58px;
      min-height: 42px;
      padding: 6px 12px;
      border-radius: 11px;
      background: var(--surface);
      border: 1.5px solid var(--border);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      font-size: 13px;
      font-weight: 700;
      color: var(--text-muted);
      transition: all 0.15s ease;
    }

    .level-tab.active {
      background: var(--accent-soft);
      border-color: var(--accent);
      color: var(--text);
    }

    .level-tab.done {
      border-color: rgba(34, 197, 94, 0.55);
      color: var(--success);
    }

    .level-tab.active.done {
      background: var(--success-soft);
      border-color: var(--success);
      color: var(--text);
    }

    .level-check {
      width: 16px;
      height: 16px;
      border-radius: 50%;
      display: grid;
      place-items: center;
      font-size: 10px;
      font-weight: 800;
      background: var(--surface-2);
      color: var(--text-muted);
    }

    .level-tab.done .level-check {
      background: var(--success);
      color: #ffffff;
    }

    /* Main Content Container */
    .container {
      width: 100%;
      max-width: 780px;
      margin: 0 auto;
      padding: 12px 14px 28px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      min-width: 0;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 14px;
      min-width: 0;
    }

    .task-header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 8px;
    }

    .task-kicker {
      font-size: 11px;
      font-weight: 800;
      text-transform: uppercase;
      letter-spacing: 0.7px;
      color: var(--accent);
      margin-bottom: 2px;
    }

    .task-title {
      margin: 0;
      font-size: 18px;
      font-weight: 800;
      line-height: 1.25;
    }

    .status-chip {
      flex-shrink: 0;
      padding: 4px 9px;
      border-radius: 999px;
      font-size: 11px;
      font-weight: 700;
      background: var(--surface-2);
      color: var(--text-muted);
    }

    .status-chip.done {
      background: var(--success-soft);
      color: var(--success);
    }

    /* Collapsible Theory */
    .theory-toggle {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 12px;
      border-radius: 10px;
      background: var(--surface-2);
      font-size: 13px;
      font-weight: 700;
      color: var(--text);
      margin-top: 8px;
      min-height: 44px;
    }

    .theory-body {
      margin-top: 10px;
      font-size: 14px;
      color: var(--text);
      user-select: text;
      -webkit-user-select: text;
    }

    .theory-body.collapsed {
      display: none;
    }

    .theory-body p {
      margin: 0 0 10px;
      color: var(--text-muted);
    }

    .theory-body code {
      font-family: var(--mono);
      font-size: 13px;
      background: var(--surface-2);
      color: var(--accent);
      padding: 1px 5px;
      border-radius: 5px;
    }

    .syntax-box {
      background: var(--code-bg);
      color: #e2e8f0;
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 10px 12px;
      font-family: var(--mono);
      font-size: 13px;
      line-height: 1.45;
      overflow-x: auto;
      white-space: pre-wrap;
      word-break: break-word;
      margin: 0;
      user-select: text;
      -webkit-user-select: text;
    }

    .goal-box {
      margin-top: 12px;
      padding: 11px 12px;
      border-radius: 10px;
      background: var(--accent-soft);
      border-left: 3px solid var(--accent);
    }

    .goal-label {
      font-size: 12px;
      font-weight: 800;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: var(--accent);
      margin-bottom: 4px;
    }

    .goal-text {
      margin: 0 0 8px;
      font-size: 14px;
      font-weight: 600;
    }

    .criteria-list {
      margin: 0;
      padding-left: 18px;
      font-size: 13px;
      color: var(--text-muted);
    }

    .criteria-list li {
      margin-bottom: 3px;
    }

    .criteria-list code {
      font-family: var(--mono);
      color: var(--text);
      background: rgba(148, 163, 184, 0.16);
      padding: 1px 4px;
      border-radius: 4px;
      font-size: 12px;
    }

    /* Editor Card */
    .editor-card {
      padding: 0;
      overflow: hidden;
    }

    .editor-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 14px;
      border-bottom: 1px solid var(--border);
      background: var(--surface-2);
    }

    .editor-title {
      font-size: 13px;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .dot-row {
      display: flex;
      gap: 5px;
    }

    .dot {
      width: 9px;
      height: 9px;
      border-radius: 50%;
    }

    .dot-r { background: #ef4444; }
    .dot-y { background: #f59e0b; }
    .dot-g { background: #22c55e; }

    .editor-meta {
      font-size: 11px;
      color: var(--text-muted);
      font-family: var(--mono);
    }

    /* Quick Insert Bar */
    .quick-bar {
      display: flex;
      align-items: center;
      gap: 6px;
      padding: 8px 10px;
      overflow-x: auto;
      background: var(--bg-elevated);
      border-bottom: 1px solid var(--border);
      scrollbar-width: none;
    }

    .quick-bar::-webkit-scrollbar {
      display: none;
    }

    .chip-btn {
      flex: 0 0 auto;
      min-height: 38px;
      padding: 6px 10px;
      border-radius: 8px;
      background: var(--surface-2);
      border: 1px solid var(--border);
      color: var(--text);
      font-family: var(--mono);
      font-size: 13px;
      font-weight: 700;
      white-space: nowrap;
      transition: transform 0.1s ease, border-color 0.15s ease;
    }

    .chip-btn:active {
      transform: scale(0.94);
      border-color: var(--accent);
      background: var(--accent-soft);
    }

    .chip-btn.special {
      border-color: rgba(251, 146, 60, 0.5);
      color: var(--orange);
    }

    .chip-btn.svg-chip {
      border-color: rgba(56, 189, 248, 0.55);
      color: var(--accent);
    }

    /* Monospace Editor */
    .editor-wrap {
      position: relative;
      background: var(--code-bg);
    }

    .code-input {
      display: block;
      width: 100%;
      min-height: 185px;
      max-height: 340px;
      padding: 12px 14px;
      margin: 0;
      border: none;
      outline: none;
      resize: vertical;
      background: var(--code-bg);
      color: #f8fafc;
      font-family: var(--mono);
      font-size: 16px;
      line-height: 1.5;
      tab-size: 2;
      caret-color: var(--accent);
      user-select: text;
      -webkit-user-select: text;
    }

    .code-input::placeholder {
      color: #64748b;
    }

    /* Action Buttons */
    .action-row {
      display: grid;
      grid-template-columns: 1.4fr 1fr 1fr;
      gap: 8px;
      padding: 10px 12px;
      background: var(--surface);
      border-top: 1px solid var(--border);
    }

    .btn {
      min-height: 48px;
      border-radius: 11px;
      padding: 10px 12px;
      font-size: 14px;
      font-weight: 700;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: transform 0.12s ease, opacity 0.15s ease;
    }

    .btn:active {
      transform: scale(0.97);
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--accent), var(--accent-strong));
      color: #ffffff;
    }

    .btn-secondary {
      background: var(--surface-2);
      border: 1px solid var(--border);
      color: var(--text);
    }

    .btn-reset {
      background: var(--danger-soft);
      border: 1px solid rgba(248, 113, 113, 0.35);
      color: var(--danger);
    }

    /* Hint & Feedback Panels */
    .panel {
      border-radius: var(--radius);
      padding: 12px 14px;
      font-size: 14px;
      display: none;
      animation: fadeSlide 0.2s ease;
    }

    .panel.visible {
      display: block;
    }

    @keyframes fadeSlide {
      from { opacity: 0; transform: translateY(-4px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .hint-panel {
      background: var(--warning-soft);
      border: 1px solid rgba(245, 158, 11, 0.4);
    }

    .hint-title {
      font-weight: 800;
      font-size: 13px;
      color: var(--warning);
      margin-bottom: 4px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .hint-text {
      margin: 0;
      color: var(--text);
      user-select: text;
      -webkit-user-select: text;
    }

    .feedback-panel.pass {
      background: var(--success-soft);
      border: 1px solid rgba(34, 197, 94, 0.45);
    }

    .feedback-panel.fail {
      background: var(--surface);
      border: 1px solid var(--warning);
    }

    .feedback-head {
      font-weight: 800;
      font-size: 15px;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .feedback-panel.pass .feedback-head {
      color: var(--success);
    }

    .feedback-panel.fail .feedback-head {
      color: var(--warning);
    }

    .feedback-list {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .feedback-item {
      display: flex;
      align-items: flex-start;
      gap: 8px;
      font-size: 13.5px;
      line-height: 1.4;
    }

    .fb-mark {
      flex-shrink: 0;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      display: grid;
      place-items: center;
      font-size: 11px;
      font-weight: 800;
      margin-top: 1px;
    }

    .fb-mark.ok {
      background: var(--success);
      color: #ffffff;
    }

    .fb-mark.miss {
      background: var(--warning-soft);
      border: 1.5px solid var(--warning);
      color: var(--warning);
    }

    .next-btn {
      margin-top: 12px;
      width: 100%;
      min-height: 48px;
      border-radius: 11px;
      background: var(--success);
      color: #ffffff;
      font-size: 14px;
      font-weight: 800;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }

    .all-done-banner {
      margin-top: 10px;
      padding: 10px 12px;
      border-radius: 10px;
      background: rgba(34, 197, 94, 0.18);
      font-weight: 700;
      font-size: 13.5px;
      text-align: center;
    }

    /* Live Preview */
    .preview-card {
      padding: 0;
      overflow: hidden;
    }

    .preview-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 14px;
      background: var(--surface-2);
      border-bottom: 1px solid var(--border);
    }

    .preview-title {
      font-size: 13px;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .live-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--success);
      box-shadow: 0 0 0 3px rgba(34, 197, 94, 0.25);
    }

    .preview-frame {
      display: block;
      width: 100%;
      min-height: 210px;
      height: 230px;
      border: none;
      background: #ffffff;
    }

    .footer-tools {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      padding: 4px 2px 10px;
      font-size: 12px;
      color: var(--text-muted);
    }

    .text-link-btn {
      font-size: 12px;
      font-weight: 700;
      color: var(--text-muted);
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid var(--border);
      min-height: 36px;
    }

    @media (max-width: 390px) {
      .action-row {
        grid-template-columns: 1fr 1fr;
      }
      .btn-primary {
        grid-column: 1 / -1;
      }
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="topbar-row">
      <div class="brand">
        <div class="brand-badge">&lt;/&gt;</div>
        <div class="brand-text">
          <div class="brand-title">HTML Тренажер</div>
          <div class="brand-sub">Інтерактивний курс • 6 рівнів</div>
        </div>
      </div>
      <div class="topbar-actions">
        <div class="progress-pill" id="progressPill">0 / 6</div>
        <button class="icon-btn" id="themeBtn" type="button" aria-label="Змінити тему" title="Змінити тему">☀️</button>
      </div>
    </div>
    <div class="progress-track" aria-hidden="true">
      <div class="progress-fill" id="progressFill"></div>
    </div>
    <nav class="level-strip" id="levelStrip" aria-label="Рівні завдань"></nav>
  </header>

  <main class="container">
    <section class="card" aria-labelledby="taskTitle">
      <div class="task-header">
        <div>
          <div class="task-kicker" id="taskKicker">Завдання 1 з 6</div>
          <h1 class="task-title" id="taskTitle">Заголовок сторінки та абзац</h1>
        </div>
        <span class="status-chip" id="taskStatusChip">В процесі</span>
      </div>

      <button class="theory-toggle" id="theoryToggle" type="button" aria-expanded="true">
        <span>📘 Коротка теорія та синтаксис</span>
        <span id="theoryArrow">▲</span>
      </button>
      <div class="theory-body" id="theoryBody">
        <p id="theoryText"></p>
        <pre class="syntax-box" id="theoryExample"></pre>
      </div>

      <div class="goal-box">
        <div class="goal-label">🎯 Ваша задача</div>
        <p class="goal-text" id="goalText"></p>
        <ul class="criteria-list" id="criteriaList"></ul>
      </div>
    </section>

    <section class="card editor-card">
      <div class="editor-head">
        <div class="editor-title">
          <span class="dot-row" aria-hidden="true">
            <span class="dot dot-r"></span>
            <span class="dot dot-y"></span>
            <span class="dot dot-g"></span>
          </span>
          <span>index.html</span>
        </div>
        <span class="editor-meta" id="editorMeta">0 рядків</span>
      </div>

      <div class="quick-bar" id="quickBar" aria-label="Швидка вставка HTML-тегів"></div>

      <div class="editor-wrap">
        <textarea
          id="codeEditor"
          class="code-input"
          spellcheck="false"
          autocomplete="off"
          autocapitalize="off"
          autocorrect="off"
          aria-label="Редактор HTML-коду"
          placeholder="Введіть ваш HTML-код тут..."></textarea>
      </div>

      <div class="action-row">
        <button class="btn btn-primary" id="checkBtn" type="button">✓ Перевірити</button>
        <button class="btn btn-secondary" id="hintBtn" type="button">💡 Підказка</button>
        <button class="btn btn-reset" id="resetBtn" type="button">↺ Скинути</button>
      </div>
    </section>

    <section class="panel hint-panel" id="hintPanel" aria-live="polite">
      <div class="hint-title">
        <span id="hintLabel">Підказка 1/3</span>
        <span id="hintMoreNote">Натисніть ще раз для наступної</span>
      </div>
      <p class="hint-text" id="hintText"></p>
    </section>

    <section class="panel feedback-panel" id="feedbackPanel" aria-live="polite">
      <div class="feedback-head" id="feedbackHead"></div>
      <ul class="feedback-list" id="feedbackList"></ul>
      <button class="next-btn" id="nextBtn" type="button" style="display:none;">Наступне завдання →</button>
      <div class="all-done-banner" id="allDoneBanner" style="display:none;">
        🎉 Вітаємо! Усі 6 рівнів успішно пройдено!
      </div>
    </section>

    <section class="card preview-card">
      <div class="preview-head">
        <div class="preview-title">
          <span class="live-dot" aria-hidden="true"></span>
          <span>Живий результат (Preview)</span>
        </div>
        <span class="editor-meta">HTML5</span>
      </div>
      <iframe
        id="previewFrame"
        class="preview-frame"
        title="Попередній перегляд HTML-коду"
        sandbox="allow-scripts"></iframe>
    </section>

    <div class="footer-tools">
      <span>Прогрес зберігається автоматично</span>
      <button class="text-link-btn" id="resetProgressBtn" type="button">Очистити весь прогрес</button>
    </div>
  </main>

  <script>
    (function () {
      'use strict';

      var SAMPLE_SVG_URI =
        'data:image/svg+xml;utf8,' +
        '%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%20240%20140%22%3E' +
        '%3Cdefs%3E%3ClinearGradient%20id%3D%22g%22%20x1%3D%220%22%20y1%3D%220%22%20x2%3D%221%22%20y2%3D%221%22%3E' +
        '%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%230284c7%22%2F%3E' +
        '%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%236366f1%22%2F%3E' +
        '%3C%2FlinearGradient%3E%3C%2Fdefs%3E' +
        '%3Crect%20width%3D%22240%22%20height%3D%22140%22%20rx%3D%2216%22%20fill%3D%22url(%23g)%22%2F%3E' +
        '%3Ccircle%20cx%3D%22190%22%20cy%3D%2238%22%20r%3D%2218%22%20fill%3D%22%23fde047%22%2F%3E' +
        '%3Cpath%20d%3D%22M16%20120l58-50%2040%2034%2034-26%2076%2042z%22%20fill%3D%22%230f172a%22%20opacity%3D%220.42%22%2F%3E' +
        '%3Ctext%20x%3D%2222%22%20y%3D%2242%22%20fill%3D%22%23ffffff%22%20font-family%3D%22sans-serif%22%20font-size%3D%2218%22%20font-weight%3D%22bold%22%3EHTML5%3C%2Ftext%3E' +
        '%3C%2Fsvg%3E';

      var STORAGE_KEY = 'html_trainer_state_v1';

      function createStorage() {
        var memory = {};
        try {
          var testKey = '__html_trainer_test__';
          window.localStorage.setItem(testKey, '1');
          window.localStorage.removeItem(testKey);
          return {
            get: function (k) { return window.localStorage.getItem(k); },
            set: function (k, v) { window.localStorage.setItem(k, v); }
          };
        } catch (e) {
          return {
            get: function (k) { return Object.prototype.hasOwnProperty.call(memory, k) ? memory[k] : null; },
            set: function (k, v) { memory[k] = String(v); }
          };
        }
      }

      var store = createStorage();

      function stripComments(html) {
        return html.replace(/<!--[\s\S]*?-->/g, '');
      }

      function findUnclosedTags(html) {
        var clean = stripComments(html);
        var checkable = ['h1', 'h2', 'h3', 'p', 'strong', 'em', 'mark', 'ul', 'ol', 'li', 'a', 'article', 'section', 'div'];
        var issues = [];
        checkable.forEach(function (tag) {
          var openRe = new RegExp('<' + tag + '(?:\\s[^>]*)?>', 'gi');
          var closeRe = new RegExp('<\\/' + tag + '\\s*>', 'gi');
          var opens = (clean.match(openRe) || []).length;
          var closes = (clean.match(closeRe) || []).length;
          if (opens > closes) {
            issues.push('Тег <' + tag + '> відкрито, але не закрито (додайте </' + tag + '>)');
          } else if (closes > opens) {
            issues.push('Зайвий закривальний тег </' + tag + '> без відкривального <' + tag + '>');
          }
        });
        return issues;
      }

      function parseUserHtml(raw) {
        var clean = stripComments(raw);
        var parser = new DOMParser();
        var doc = parser.parseFromString('<!DOCTYPE html><html><body>' + clean + '</body></html>', 'text/html');
        return {
          body: doc.body,
          clean: clean,
          tagIssues: findUnclosedTags(raw)
        };
      }

      function textLen(el) {
        return el ? el.textContent.replace(/\s+/g, ' ').trim().length : 0;
      }

      var TASKS = [
        {
          id: 1,
          shortTitle: '<h1> і <p>',
          title: 'Заголовок сторінки та абзац',
          theoryHtml:
            'Тег <code>&lt;h1&gt;</code> задає головний заголовок сторінки — зазвичай він один і коротко описує тему. Тег <code>&lt;p&gt;</code> створює звичайний текстовий абзац із відступами зверху та знизу. Парні теги завжди мають відкривальну та закривальну частини.',
          syntax: '<h1>Привіт, світе!</h1>\n<p>Це мій перший абзац на вебсторінці.</p>',
          goal: 'Створіть головний заголовок сторінки та один абзац тексту під ним.',
          criteria: [
            'Додайте тег <code>&lt;h1&gt;...&lt;/h1&gt;</code> з текстом (від 2 символів).',
            'Додайте тег <code>&lt;p&gt;...&lt;/p&gt;</code> з реченням або описом (від 5 символів).'
          ],
          starter: '<!-- Впишіть текст усередину тегів нижче -->\n<h1></h1>\n<p></p>',
          hints: [
            'Помістіть курсор між <h1> та </h1> і напишіть коротку назву сторінки.',
            'Нижче між <p> та </p> додайте речення з кількох слів (мінімум 5 символів).',
            'Перевірте, чи обидва теги мають закривальний слеш: </h1> та </p>.'
          ],
          validate: function (parsed) {
            var h1s = Array.from(parsed.body.querySelectorAll('h1'));
            var ps = Array.from(parsed.body.querySelectorAll('p'));
            var validH1 = h1s.some(function (el) { return textLen(el) >= 2; });
            var validP = ps.some(function (el) { return textLen(el) >= 5; });
            return [
              {
                ok: validH1,
                pass: 'Додано головний заголовок <h1> з текстом.',
                fail: h1s.length === 0
                  ? 'Додайте тег заголовка <h1>...</h1>.'
                  : 'Заповніть заголовок <h1> текстом (щонайменше 2 символи).'
              },
              {
                ok: validP,
                pass: 'Додано текстовий абзац <p>.',
                fail: ps.length === 0
                  ? 'Додайте тег абзацу <p>...</p>.'
                  : 'Додайте текст усередину <p> (щонайменше 5 символів).'
              }
            ];
          }
        },
        {
          id: 2,
          shortTitle: '<strong> / <em>',
          title: 'Виділення тексту в абзаці',
          theoryHtml:
            'Для змістового виділення фрагментів усередині тексту використовують вбудовані теги. <code>&lt;strong&gt;</code> позначає важливий текст (жирним), <code>&lt;em&gt;</code> додає логічний наголос (курсивом), а <code>&lt;mark&gt;</code> підсвічує слова як жовтий маркер.',
          syntax: '<p>Вивчати <strong>HTML</strong> — це <mark>просто</mark> і <em>цікаво</em>.</p>',
          goal: 'Виділіть усередині абзацу важливе слово тегом <strong> і ще одне слово тегом <em> або <mark>.',
          criteria: [
            'Створіть заповнений абзац <code>&lt;p&gt;...&lt;/p&gt;</code>.',
            'Усередині <code>&lt;p&gt;</code> додайте хоча б один тег <code>&lt;strong&gt;</code> із текстом.',
            'Усередині <code>&lt;p&gt;</code> додайте тег <code>&lt;em&gt;</code> або <code>&lt;mark&gt;</code> із текстом.'
          ],
          starter: '<p>Вивчати HTML дуже цікаво та корисно щодня.</p>',
          hints: [
            'Оберіть ключове слово в абзаці (наприклад, HTML) і обгорніть його: <strong>HTML</strong>.',
            'Ще одне слово (наприклад, цікаво) обгорніть у <em>цікаво</em> або <mark>цікаво</mark>.',
            'Стежте, щоб теги виділення були всередині <p>...</p>, а не за його межами.'
          ],
          validate: function (parsed) {
            var ps = Array.from(parsed.body.querySelectorAll('p'));
            var hasP = ps.some(function (el) { return textLen(el) >= 5; });
            var hasStrong = ps.some(function (p) {
              return Array.from(p.querySelectorAll('strong')).some(function (s) { return textLen(s) >= 1; });
            });
            var hasEmOrMark = ps.some(function (p) {
              return Array.from(p.querySelectorAll('em, mark')).some(function (m) { return textLen(m) >= 1; });
            });
            return [
              {
                ok: hasP,
                pass: 'Створено абзац <p> з текстом.',
                fail: 'Додайте абзац <p>...</p> із текстом.'
              },
              {
                ok: hasStrong,
                pass: 'Усередині <p> є виділення важливого тексту через <strong>.',
                fail: 'Додайте тег <strong>...</strong> із текстом усередині <p>.'
              },
              {
                ok: hasEmOrMark,
                pass: 'Усередині <p> є акцент або підсвічування через <em> чи <mark>.',
                fail: 'Додайте всередині <p> ще один тег виділення: <em>...</em> або <mark>...</mark>.'
              }
            ];
          }
        },
        {
          id: 3,
          shortTitle: '<ul> / <ol>',
          title: 'Маркований або нумерований список',
          theoryHtml:
            'Тег <code>&lt;ul&gt;</code> створює маркований список із крапками, а <code>&lt;ol&gt;</code> — нумерований список із цифрами. Кожен окремий пункт списку обов’язково записується в тег <code>&lt;li&gt;</code> всередині контейнера списку.',
          syntax: '<ul>\n  <li>Кава</li>\n  <li>Чай</li>\n  <li>Сік</li>\n</ul>',
          goal: 'Додайте список <ul> або <ol>, у якому буде щонайменше 3 заповнені пункти <li>.',
          criteria: [
            'Створіть контейнер списку <code>&lt;ul&gt;</code> або <code>&lt;ol&gt;</code>.',
            'Вкладіть усередину списку принаймні 3 пункти <code>&lt;li&gt;...&lt;/li&gt;</code> із текстом.'
          ],
          starter: '<h2>Мої плани</h2>\n<ul>\n  <li>Опанувати основи HTML</li>\n  \n</ul>',
          hints: [
            'Зараз у списку <ul> є лише один пункт <li>. Додайте під ним нові рядки з <li>...</li>.',
            'На панелі швидкої вставки натисніть <li> — пара тегів вставиться автоматично.',
            'Перевірте, щоб усі 3 пункти <li> були саме між <ul> (або <ol>) і закривальним тегом.'
          ],
          validate: function (parsed) {
            var lists = Array.from(parsed.body.querySelectorAll('ul, ol'));
            var bestItemsCount = 0;
            lists.forEach(function (list) {
              var items = Array.from(list.querySelectorAll('li')).filter(function (li) {
                return textLen(li) >= 1;
              });
              if (items.length > bestItemsCount) {
                bestItemsCount = items.length;
              }
            });
            return [
              {
                ok: lists.length > 0,
                pass: 'Знайдено контейнер списку (<ul> або <ol>).',
                fail: 'Додайте тег списку <ul>...</ul> або <ol>...</ol>.'
              },
              {
                ok: bestItemsCount >= 3,
                pass: 'У списку є щонайменше 3 заповнені пункти <li> (' + bestItemsCount + ').',
                fail: bestItemsCount === 0
                  ? 'Додайте всередину списку <ul>/<ol> принаймні 3 пункти <li>...</li>.'
                  : 'Зараз заповнених пунктів: ' + bestItemsCount + '. Додайте ще ' + (3 - bestItemsCount) + ' пункт(и) <li>.'
              }
            ];
          }
        },
        {
          id: 4,
          shortTitle: '<a href>',
          title: 'Гіперпосилання',
          theoryHtml:
            'Тег <code>&lt;a&gt;</code> перетворює текст на клікабельне посилання. Куди саме веде посилання, визначає атрибут <code>href="..."</code> у відкривальному тегу, а між <code>&lt;a&gt;</code> і <code>&lt;/a&gt;</code> пишуть видимий текст.',
          syntax: '<a href="https://developer.mozilla.org">Документація MDN</a>',
          goal: 'Створіть робоче посилання <a> з заповненим атрибутом href та зрозумілим текстом.',
          criteria: [
            'Додайте тег <code>&lt;a&gt;...&lt;/a&gt;</code>.',
            'Вкажіть непустий атрибут <code>href="..."</code> (наприклад, <code>https://example.com</code> або <code>#top</code>).',
            'Напишіть видимий текст посилання всередині <code>&lt;a&gt;</code> (від 2 символів).'
          ],
          starter: '<p>Натисніть нижче, щоб відкрити довідник:</p>\n<a href="">Довідник HTML</a>',
          hints: [
            'Знайдіть href="" у тегу <a> і впишіть адресу між подвійними лапками.',
            'Підійде будь-яка коректна адреса, наприклад https://example.com або якір #info.',
            'Переконайтеся, що лапки навколо адреси закриті, а між <a> і </a> є текст.'
          ],
          validate: function (parsed) {
            var links = Array.from(parsed.body.querySelectorAll('a'));
            var hasHref = links.some(function (a) {
              var h = a.getAttribute('href');
              return h !== null && h.trim().length >= 2;
            });
            var hasText = links.some(function (a) {
              return textLen(a) >= 2;
            });
            return [
              {
                ok: links.length > 0,
                pass: 'Тег посилання <a> додано.',
                fail: 'Додайте тег <a href="...">Текст</a>.'
              },
              {
                ok: hasHref,
                pass: 'Атрибут href заповнено коректною адресою.',
                fail: 'Вкажіть непустий атрибут href="..." (наприклад, href="https://example.com").'
              },
              {
                ok: hasText,
                pass: 'Посилання має видимий текст для користувача.',
                fail: 'Додайте видимий текст між <a> та </a> (щонайменше 2 символи).'
              }
            ];
          }
        },
        {
          id: 5,
          shortTitle: '<img src>',
          title: 'Зображення на сторінці',
          theoryHtml:
            'Тег <code>&lt;img&gt;</code> вставляє зображення і є одинарним (не потребує <code>&lt;/img&gt;</code>). Атрибут <code>src</code> вказує джерело картинки (файл або SVG data-URI для офлайну), а <code>alt</code> задає текстовий опис для читалок екрана.',
          syntax: '<img src="data:image/svg+xml;utf8,..." alt="Логотип HTML5">',
          goal: 'Вставте зображення <img> із джерелом src (можна локальний SVG) та описовим атрибутом alt.',
          criteria: [
            'Додайте одинарний тег <code>&lt;img&gt;</code>.',
            'Задайте непустий <code>src="..."</code> — натисніть кнопку <code>SVG</code> на панелі, щоб вставити офлайн-картинку.',
            'Заповніть атрибут <code>alt="..."</code> описом зображення (від 3 символів).'
          ],
          starter: '<h2>Моя ілюстрація</h2>\n<img src="" alt="">',
          hints: [
            'Поставте курсор усередині лапок src="" і натисніть кнопку «SVG» на панелі швидкої вставки.',
            'Знайдіть alt="" і впишіть короткий опис картинки, наприклад: alt="Пейзаж HTML5".',
            'Закривальний тег </img> не потрібен — достатньо одного <img src="..." alt="...">.'
          ],
          validate: function (parsed) {
            var imgs = Array.from(parsed.body.querySelectorAll('img'));
            var hasSrc = imgs.some(function (img) {
              var s = img.getAttribute('src');
              return s !== null && s.trim().length >= 5;
            });
            var hasAlt = imgs.some(function (img) {
              var a = img.getAttribute('alt');
              return a !== null && a.trim().length >= 3;
            });
            return [
              {
                ok: imgs.length > 0,
                pass: 'Тег <img> присутній у розмітці.',
                fail: 'Додайте тег <img src="..." alt="...">.'
              },
              {
                ok: hasSrc,
                pass: 'Атрибут src задано — картинка підключена.',
                fail: 'Заповніть src="..." (поставте курсор у src="" і натисніть кнопку SVG).'
              },
              {
                ok: hasAlt,
                pass: 'Додано змістовний альтернативний текст alt.',
                fail: 'Додайте атрибут alt="..." з описом зображення (від 3 символів).'
              }
            ];
          }
        },
        {
          id: 6,
          shortTitle: 'Картка',
          title: 'Комплексне завдання: HTML-картка',
          theoryHtml:
            'На справжніх сайтах споріднені елементи об’єднують у спільний блок — семантичний тег <code>&lt;article&gt;</code>, <code>&lt;section&gt;</code> або універсальний <code>&lt;div&gt;</code>. Усередині такої картки зазвичай розміщують заголовок, список характеристик і посилання для дії.',
          syntax:
            '<article>\n  <h2>Назва картки</h2>\n  <ul>\n    <li>Пункт 1</li>\n    <li>Пункт 2</li>\n  </ul>\n  <a href="https://example.com">Детальніше</a>\n</article>',
          goal: 'Зберіть повноцінний блок-картку (<article>, <section> або <div>), що містить заголовок, список і посилання.',
          criteria: [
            'Створіть контейнер <code>&lt;article&gt;</code>, <code>&lt;section&gt;</code> або <code>&lt;div&gt;</code>.',
            'Усередині контейнера додайте заголовок (<code>&lt;h1&gt;</code>, <code>&lt;h2&gt;</code> або <code>&lt;h3&gt;</code>).',
            'Усередині контейнера додайте список <code>&lt;ul&gt;</code> або <code>&lt;ol&gt;</code> з щонайменше 2 пунктами <code>&lt;li&gt;</code>.',
            'Усередині контейнера додайте посилання <code>&lt;a href="..."&gt;</code> з адресою та текстом.'
          ],
          starter:
            '<article>\n  <h2>Стартовий курс HTML</h2>\n  <!-- Додайте <ul> з 2+ пунктами <li> та посилання <a href="..."> -->\n  \n</article>',
          hints: [
            'Усередині <article>...</article> під <h2> додайте список <ul> з мінімум двома пунктами <li>.',
            'Після </ul> (але перед </article>) додайте <a href="https://example.com">Перейти</a>.',
            'Переконайтеся, що і заголовок, і список, і посилання знаходяться всередині одного блока картки.'
          ],
          validate: function (parsed) {
            var cards = Array.from(parsed.body.querySelectorAll('article, section, div'));
            var hasCard = cards.length > 0;

            var cardWithHeading = cards.some(function (card) {
              return Array.from(card.querySelectorAll('h1, h2, h3')).some(function (h) {
                return textLen(h) >= 2;
              });
            });

            var cardWithList = cards.some(function (card) {
              return Array.from(card.querySelectorAll('ul, ol')).some(function (list) {
                var items = Array.from(list.querySelectorAll('li')).filter(function (li) {
                  return textLen(li) >= 1;
                });
                return items.length >= 2;
              });
            });

            var cardWithLink = cards.some(function (card) {
              return Array.from(card.querySelectorAll('a')).some(function (a) {
                var h = a.getAttribute('href');
                return h !== null && h.trim().length >= 2 && textLen(a) >= 2;
              });
            });

            return [
              {
                ok: hasCard,
                pass: 'Створено контейнер картки (<article>, <section> або <div>).',
                fail: 'Додайте зовнішній блок картки: <article>...</article>, <section>...</section> або <div>...</div>.'
              },
              {
                ok: cardWithHeading,
                pass: 'Усередині картки є заголовок.',
                fail: 'Додайте всередину картки заголовок <h1>, <h2> або <h3> з текстом.'
              },
              {
                ok: cardWithList,
                pass: 'Усередині картки є список із 2+ пунктів <li>.',
                fail: 'Додайте всередину картки список <ul> або <ol> із щонайменше 2 пунктами <li>.'
              },
              {
                ok: cardWithLink,
                pass: 'Усередині картки є коректне посилання <a href="...">.',
                fail: 'Додайте всередину картки посилання <a href="...">Текст</a> із непорожнім href.'
              }
            ];
          }
        }
      ];

      var QUICK_ITEMS = [
        { label: '<h1>', type: 'pair', open: '<h1>', close: '</h1>' },
        { label: '<p>', type: 'pair', open: '<p>', close: '</p>' },
        { label: '<strong>', type: 'pair', open: '<strong>', close: '</strong>' },
        { label: '<em>', type: 'pair', open: '<em>', close: '</em>' },
        { label: '<mark>', type: 'pair', open: '<mark>', close: '</mark>' },
        { label: '<ul>', type: 'block', open: '<ul>\n  ', close: '\n</ul>' },
        { label: '<ol>', type: 'block', open: '<ol>\n  ', close: '\n</ol>' },
        { label: '<li>', type: 'pair', open: '<li>', close: '</li>' },
        { label: '<a>', type: 'snippet', text: '<a href=""></a>', cursorBack: 6 },
        { label: '<img>', type: 'snippet', text: '<img src="" alt="">', cursorBack: 9 },
        { label: 'SVG', type: 'svg', text: SAMPLE_SVG_URI, special: 'svg-chip' },
        { label: '<article>', type: 'block', open: '<article>\n  ', close: '\n</article>' },
        { label: '</>', type: 'closeLast', special: 'special' },
        { label: '<>', type: 'snippet', text: '<>', cursorBack: 1 },
        { label: '/', type: 'snippet', text: '/', cursorBack: 0 },
        { label: '=', type: 'snippet', text: '=', cursorBack: 0 },
        { label: '"', type: 'snippet', text: '""', cursorBack: 1 }
      ];

      var VOID_TAGS = { img: true, br: true, hr: true, input: true, meta: true, link: true };

      // Load or initialize state
      function loadState() {
        var fallback = {
          currentId: 1,
          completed: [],
          codeByTask: {},
          theme: 'dark'
        };
        try {
          var raw = store.get(STORAGE_KEY);
          if (!raw) return fallback;
          var parsed = JSON.parse(raw);
          return {
            currentId: typeof parsed.currentId === 'number' && parsed.currentId >= 1 && parsed.currentId <= TASKS.length ? parsed.currentId : 1,
            completed: Array.isArray(parsed.completed) ? parsed.completed : [],
            codeByTask: parsed.codeByTask && typeof parsed.codeByTask === 'object' ? parsed.codeByTask : {},
            theme: parsed.theme === 'light' ? 'light' : 'dark'
          };
        } catch (e) {
          return fallback;
        }
      }

      var state = loadState();
      var hintIndex = 0;

      function saveState() {
        try {
          store.set(STORAGE_KEY, JSON.stringify(state));
        } catch (e) {}
      }

      // DOM refs
      var el = {
        html: document.documentElement,
        themeBtn: document.getElementById('themeBtn'),
        progressPill: document.getElementById('progressPill'),
        progressFill: document.getElementById('progressFill'),
        levelStrip: document.getElementById('levelStrip'),
        taskKicker: document.getElementById('taskKicker'),
        taskTitle: document.getElementById('taskTitle'),
        taskStatusChip: document.getElementById('taskStatusChip'),
        theoryToggle: document.getElementById('theoryToggle'),
        theoryArrow: document.getElementById('theoryArrow'),
        theoryBody: document.getElementById('theoryBody'),
        theoryText: document.getElementById('theoryText'),
        theoryExample: document.getElementById('theoryExample'),
        goalText: document.getElementById('goalText'),
        criteriaList: document.getElementById('criteriaList'),
        quickBar: document.getElementById('quickBar'),
        codeEditor: document.getElementById('codeEditor'),
        editorMeta: document.getElementById('editorMeta'),
        checkBtn: document.getElementById('checkBtn'),
        hintBtn: document.getElementById('hintBtn'),
        resetBtn: document.getElementById('resetBtn'),
        hintPanel: document.getElementById('hintPanel'),
        hintLabel: document.getElementById('hintLabel'),
        hintMoreNote: document.getElementById('hintMoreNote'),
        hintText: document.getElementById('hintText'),
        feedbackPanel: document.getElementById('feedbackPanel'),
        feedbackHead: document.getElementById('feedbackHead'),
        feedbackList: document.getElementById('feedbackList'),
        nextBtn: document.getElementById('nextBtn'),
        allDoneBanner: document.getElementById('allDoneBanner'),
        previewFrame: document.getElementById('previewFrame'),
        resetProgressBtn: document.getElementById('resetProgressBtn')
      };

      function getCurrentTask() {
        return TASKS.find(function (t) { return t.id === state.currentId; }) || TASKS[0];
      }

      function applyTheme(theme) {
        state.theme = theme;
        el.html.setAttribute('data-theme', theme);
        el.themeBtn.textContent = theme === 'dark' ? '☀️' : '🌙';
        saveState();
      }

      function renderHeaderAndLevels() {
        var doneCount = state.completed.length;
        el.progressPill.textContent = doneCount + ' / ' + TASKS.length;
        el.progressFill.style.width = Math.round((doneCount / TASKS.length) * 100) + '%';

        el.levelStrip.innerHTML = '';
        TASKS.forEach(function (task) {
          var isDone = state.completed.indexOf(task.id) !== -1;
          var isActive = task.id === state.currentId;
          var btn = document.createElement('button');
          btn.type = 'button';
          btn.className = 'level-tab' + (isActive ? ' active' : '') + (isDone ? ' done' : '');
          btn.setAttribute('aria-current', isActive ? 'step' : 'false');

          var badge = document.createElement('span');
          badge.className = 'level-check';
          badge.textContent = isDone ? '✓' : String(task.id);

          var label = document.createElement('span');
          label.textContent = task.shortTitle;

          btn.appendChild(badge);
          btn.appendChild(label);
          btn.addEventListener('click', function () {
            selectTask(task.id);
          });
          el.levelStrip.appendChild(btn);

          if (isActive && typeof btn.scrollIntoView === 'function') {
            setTimeout(function () {
              btn.scrollIntoView({ behavior: 'smooth', inline: 'center', block: 'nearest' });
            }, 30);
          }
        });
      }

      function sanitizePreviewHtml(rawHtml) {
        return rawHtml
          .replace(/<script\b[\s\S]*?>[\s\S]*?<\/script>/gi, '')
          .replace(/\son[a-z]+\s*=\s*(?:"[^"]*"|'[^']*'|[^\s>]+)/gi, '');
      }

      function updatePreview() {
        var safeHtml = sanitizePreviewHtml(el.codeEditor.value);
        var srcdoc =
          '<!DOCTYPE html><html lang="uk"><head><meta charset="UTF-8">' +
          '<meta name="viewport" content="width=device-width,initial-scale=1">' +
          '<style>' +
          '*{box-sizing:border-box;}' +
          'body{margin:0;padding:14px;font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,sans-serif;font-size:15px;line-height:1.5;color:#0f172a;background:#ffffff;word-wrap:break-word;}' +
          'h1,h2,h3{margin:0 0 10px;line-height:1.25;color:#0f172a;}' +
          'h1{font-size:22px;} h2{font-size:18px;} h3{font-size:16px;}' +
          'p{margin:0 0 10px;}' +
          'ul,ol{margin:0 0 10px;padding-left:22px;}' +
          'li{margin-bottom:4px;}' +
          'a{color:#0284c7;text-decoration:underline;font-weight:600;}' +
          'mark{background:#fde047;color:#0f172a;padding:1px 4px;border-radius:4px;}' +
          'img{max-width:100%;height:auto;border-radius:10px;display:block;margin:6px 0;}' +
          'article,section,div{border:1px solid #cbd5e1;border-radius:12px;padding:12px;background:#f8fafc;margin-bottom:8px;}' +
          '#linkToast{position:fixed;left:10px;right:10px;bottom:10px;background:#0f172a;color:#f8fafc;padding:8px 12px;border-radius:8px;font-size:12px;display:none;box-shadow:0 4px 12px rgba(0,0,0,.25);}' +
          '</style></head><body>' +
          safeHtml +
          '<div id="linkToast"></div>' +
          '<script>' +
          'document.addEventListener("click",function(e){' +
          'var a=e.target.closest("a");' +
          'if(a){e.preventDefault();var t=document.getElementById("linkToast");' +
          'var h=a.getAttribute("href")||"(порожній href)";' +
          't.textContent="🔗 Посилання веде на: "+h;t.style.display="block";' +
          'clearTimeout(window.__tt);window.__tt=setTimeout(function(){t.style.display="none";},2400);}' +
          '});' +
          '<\/script></body></html>';
        el.previewFrame.srcdoc = srcdoc;
      }

      function updateLineCount() {
        var lines = el.codeEditor.value.split('\n').length;
        el.editorMeta.textContent = lines + (lines === 1 ? ' рядок' : lines < 5 ? ' рядки' : ' рядків');
      }

      function renderTask() {
        var task = getCurrentTask();
        var isDone = state.completed.indexOf(task.id) !== -1;

        el.taskKicker.textContent = 'Завдання ' + task.id + ' з ' + TASKS.length;
        el.taskTitle.textContent = task.title;
        el.taskStatusChip.textContent = isDone ? 'Виконано ✓' : 'В процесі';
        el.taskStatusChip.className = 'status-chip' + (isDone ? ' done' : '');

        el.theoryText.innerHTML = task.theoryHtml;
        el.theoryExample.textContent = task.syntax;
        el.goalText.textContent = task.goal;

        el.criteriaList.innerHTML = '';
        task.criteria.forEach(function (c) {
          var li = document.createElement('li');
          li.innerHTML = c;
          el.criteriaList.appendChild(li);
        });

        var savedCode = Object.prototype.hasOwnProperty.call(state.codeByTask, String(task.id))
          ? state.codeByTask[String(task.id)]
          : task.starter;

        el.codeEditor.value = savedCode;
        hintIndex = 0;
        el.hintPanel.classList.remove('visible');
        el.feedbackPanel.classList.remove('visible', 'pass', 'fail');
        el.nextBtn.style.display = 'none';
        el.allDoneBanner.style.display = 'none';

        updateLineCount();
        updatePreview();
        renderHeaderAndLevels();
      }

      function selectTask(taskId) {
        state.currentId = taskId;
        saveState();
        renderTask();
      }

      function findLastUnclosedTag(textBeforeCursor) {
        var clean = stripComments(textBeforeCursor);
        var stack = [];
        var tagRe = /<\/?([a-zA-Z][a-zA-Z0-9]*)\b[^>]*>/g;
        var match;
        while ((match = tagRe.exec(clean)) !== null) {
          var full = match[0];
          var name = match[1].toLowerCase();
          if (VOID_TAGS[name] || full.slice(-2) === '/>') continue;
          if (full.indexOf('</') === 0) {
            for (var i = stack.length - 1; i >= 0; i--) {
              if (stack[i] === name) {
                stack.splice(i, 1);
                break;
              }
            }
          } else {
            stack.push(name);
          }
        }
        return stack.length ? stack[stack.length - 1] : null;
      }

      function insertIntoEditor(item) {
        var ta = el.codeEditor;
        var start = ta.selectionStart;
        var end = ta.selectionEnd;
        var val = ta.value;
        var selected = val.slice(start, end);
        var inserted = '';
        var newCursor = start;

        if (item.type === 'pair' || item.type === 'block') {
          inserted = item.open + selected + item.close;
          newCursor = selected.length > 0
            ? start + inserted.length
            : start + item.open.length;
        } else if (item.type === 'closeLast') {
          var unclosed = findLastUnclosedTag(val.slice(0, start));
          inserted = unclosed ? '</' + unclosed + '>' : '</>';
          newCursor = unclosed ? start + inserted.length : start + 2;
        } else {
          inserted = item.text;
          newCursor = start + inserted.length - (item.cursorBack || 0);
        }

        ta.value = val.slice(0, start) + inserted + val.slice(end);
        ta.focus();
        ta.setSelectionRange(newCursor, newCursor);
        onEditorInput();
      }

      function renderQuickBar() {
        el.quickBar.innerHTML = '';
        QUICK_ITEMS.forEach(function (item) {
          var btn = document.createElement('button');
          btn.type = 'button';
          btn.className = 'chip-btn' + (item.special ? ' ' + item.special : '');
          btn.textContent = item.label;
          btn.addEventListener('click', function () {
            insertIntoEditor(item);
          });
          el.quickBar.appendChild(btn);
        });
      }

      function onEditorInput(evt) {
        if (evt && evt.inputType === 'insertText') {
          var ta = el.codeEditor;
          var pos = ta.selectionStart;
          var val = ta.value;

          if (evt.data === '"') {
            var nextChar = val.charAt(pos);
            if (nextChar !== '"') {
              ta.value = val.slice(0, pos) + '"' + val.slice(pos);
              ta.setSelectionRange(pos, pos);
            }
          } else if (evt.data === '>') {
            var before = val.slice(0, pos);
            var after = val.slice(pos);
            var openMatch = before.match(/<([a-zA-Z][a-zA-Z0-9]*)(?:\s[^<>]*)?>$/);
            if (openMatch) {
              var tag = openMatch[1].toLowerCase();
              if (!VOID_TAGS[tag] && !after.toLowerCase().startsWith('</' + tag + '>')) {
                var closeTag = '</' + tag + '>';
                ta.value = before + closeTag + after;
                ta.setSelectionRange(pos, pos);
              }
            }
          }
        }

        var task = getCurrentTask();
        state.codeByTask[String(task.id)] = el.codeEditor.value;
        saveState();
        updateLineCount();
        updatePreview();
      }

      function runValidation() {
        var task = getCurrentTask();
        var rawCode = el.codeEditor.value;
        var parsed = parseUserHtml(rawCode);
        var results = task.validate(parsed);

        parsed.tagIssues.forEach(function (issue) {
          results.push({ ok: false, pass: '', fail: issue });
        });

        var allPassed = results.every(function (r) { return r.ok; });

        el.feedbackPanel.className = 'panel feedback-panel visible ' + (allPassed ? 'pass' : 'fail');
        el.feedbackHead.textContent = allPassed
          ? 'Чудово! Завдання виконано правильно!'
          : 'Майже готово — перевірте деталі нижче:';

        el.feedbackList.innerHTML = '';
        results.forEach(function (r) {
          var li = document.createElement('li');
          li.className = 'feedback-item';

          var mark = document.createElement('span');
          mark.className = 'fb-mark ' + (r.ok ? 'ok' : 'miss');
          mark.textContent = r.ok ? '✓' : '!';

          var msg = document.createElement('span');
          msg.textContent = r.ok ? r.pass : r.fail;

          li.appendChild(mark);
          li.appendChild(msg);
          el.feedbackList.appendChild(li);
        });

        if (allPassed) {
          if (state.completed.indexOf(task.id) === -1) {
            state.completed.push(task.id);
            saveState();
          }
          el.taskStatusChip.textContent = 'Виконано ✓';
          el.taskStatusChip.className = 'status-chip done';
          renderHeaderAndLevels();

          if (task.id < TASKS.length) {
            el.nextBtn.style.display = 'flex';
            el.allDoneBanner.style.display = 'none';
          } else {
            el.nextBtn.style.display = 'none';
            el.allDoneBanner.style.display = state.completed.length === TASKS.length ? 'block' : 'none';
          }
        } else {
          el.nextBtn.style.display = 'none';
          el.allDoneBanner.style.display = 'none';
        }

        el.feedbackPanel.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
      }

      function showNextHint() {
        var task = getCurrentTask();
        var total = task.hints.length;
        var currentStep = hintIndex % total;
        el.hintLabel.textContent = 'Підказка ' + (currentStep + 1) + '/' + total;
        el.hintMoreNote.textContent = currentStep + 1 < total ? 'Натисніть ще раз для наступної' : 'Остання підказка';
        el.hintText.textContent = task.hints[currentStep];
        el.hintPanel.classList.add('visible');
        hintIndex = (hintIndex + 1) % total;
      }

      function resetCurrentTask() {
        var task = getCurrentTask();
        delete state.codeByTask[String(task.id)];
        saveState();
        el.codeEditor.value = task.starter;
        hintIndex = 0;
        el.hintPanel.classList.remove('visible');
        el.feedbackPanel.classList.remove('visible', 'pass', 'fail');
        el.nextBtn.style.display = 'none';
        el.allDoneBanner.style.display = 'none';
        updateLineCount();
        updatePreview();
      }

      // Wire events
      el.themeBtn.addEventListener('click', function () {
        applyTheme(state.theme === 'dark' ? 'light' : 'dark');
      });

      el.theoryToggle.addEventListener('click', function () {
        var collapsed = el.theoryBody.classList.toggle('collapsed');
        el.theoryToggle.setAttribute('aria-expanded', String(!collapsed));
        el.theoryArrow.textContent = collapsed ? '▼' : '▲';
      });

      el.codeEditor.addEventListener('input', onEditorInput);
      el.checkBtn.addEventListener('click', runValidation);
      el.hintBtn.addEventListener('click', showNextHint);
      el.resetBtn.addEventListener('click', resetCurrentTask);

      el.nextBtn.addEventListener('click', function () {
        var nextId = state.currentId + 1;
        if (nextId <= TASKS.length) {
          selectTask(nextId);
          window.scrollTo({ top: 0, behavior: 'smooth' });
        }
      });

      el.resetProgressBtn.addEventListener('click', function () {
        state.completed = [];
        state.codeByTask = {};
        state.currentId = 1;
        saveState();
        renderTask();
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });

      // Init
      applyTheme(state.theme);
      renderQuickBar();
      renderTask();
    })();
  </script>
</body>
</html>