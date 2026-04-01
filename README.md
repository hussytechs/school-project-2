<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ROMA AETERNA — The Ancient Rome Quiz</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700;900&family=Cinzel:wght@400;600;700&family=EB+Garamond:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #C9A84C;
    --gold-light: #E8D08A;
    --gold-dark: #8B6914;
    --marble: #F4EFE6;
    --marble-dark: #D9CFBF;
    --crimson: #8B1A1A;
    --crimson-light: #C0392B;
    --dark: #1A1208;
    --parchment: #F2E8D0;
    --stone: #5C5240;
    --shadow: rgba(0,0,0,0.5);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'EB Garamond', serif;
    background: var(--dark);
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
  }

  /* Mosaic background pattern */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(45deg, rgba(201,168,76,0.03) 25%, transparent 25%),
      linear-gradient(-45deg, rgba(201,168,76,0.03) 25%, transparent 25%),
      linear-gradient(45deg, transparent 75%, rgba(201,168,76,0.03) 75%),
      linear-gradient(-45deg, transparent 75%, rgba(201,168,76,0.03) 75%);
    background-size: 20px 20px;
    background-position: 0 0, 0 10px, 10px -10px, -10px 0px;
    pointer-events: none;
    z-index: 0;
  }

  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background: radial-gradient(ellipse at 50% 0%, rgba(139,26,26,0.15) 0%, transparent 60%),
                radial-gradient(ellipse at 50% 100%, rgba(201,168,76,0.08) 0%, transparent 60%);
    pointer-events: none;
    z-index: 0;
  }

  .wrapper {
    position: relative;
    z-index: 1;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  /* ── SCREENS ─────────────────────────────────── */
  .screen { display: none; width: 100%; max-width: 780px; }
  .screen.active { display: block; }

  /* ── CARD ─────────────────────────────────────── */
  .card {
    background: linear-gradient(160deg, #2A1F0E 0%, #1A1208 50%, #221810 100%);
    border: 1px solid var(--gold-dark);
    border-radius: 4px;
    padding: 50px 52px;
    box-shadow:
      0 0 0 1px rgba(201,168,76,0.2),
      0 0 40px rgba(0,0,0,0.8),
      inset 0 1px 0 rgba(201,168,76,0.15);
    position: relative;
    overflow: hidden;
  }

  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, transparent, var(--gold), var(--crimson), var(--gold), transparent);
  }

  /* ── CORNER ORNAMENTS ──────────────────────────── */
  .corner { position: absolute; width: 36px; height: 36px; opacity: 0.6; }
  .corner svg { width: 100%; height: 100%; }
  .corner-tl { top: 14px; left: 14px; }
  .corner-tr { top: 14px; right: 14px; transform: scaleX(-1); }
  .corner-bl { bottom: 14px; left: 14px; transform: scaleY(-1); }
  .corner-br { bottom: 14px; right: 14px; transform: scale(-1); }

  /* ── TYPOGRAPHY ────────────────────────────────── */
  .title-main {
    font-family: 'Cinzel Decorative', serif;
    font-size: 3.2rem;
    font-weight: 900;
    color: var(--gold);
    text-align: center;
    letter-spacing: 0.08em;
    text-shadow: 0 0 40px rgba(201,168,76,0.4), 0 2px 8px rgba(0,0,0,0.8);
    line-height: 1.1;
    margin-bottom: 6px;
  }

  .title-sub {
    font-family: 'Cinzel', serif;
    font-size: 0.85rem;
    color: var(--gold-dark);
    text-align: center;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    margin-bottom: 28px;
  }

  .divider {
    display: flex;
    align-items: center;
    gap: 16px;
    margin: 24px 0;
  }
  .divider-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--gold-dark), transparent);
  }
  .divider-dot {
    width: 6px; height: 6px;
    background: var(--gold);
    transform: rotate(45deg);
    box-shadow: 0 0 8px var(--gold);
  }

  .intro-text {
    font-size: 1.1rem;
    color: var(--marble-dark);
    line-height: 1.85;
    text-align: center;
    font-style: italic;
    margin-bottom: 32px;
  }

  /* ── BUTTONS ───────────────────────────────────── */
  .btn-primary {
    display: block;
    margin: 0 auto;
    background: linear-gradient(135deg, #8B1A1A 0%, #C0392B 50%, #8B1A1A 100%);
    color: var(--gold-light);
    font-family: 'Cinzel', serif;
    font-size: 1rem;
    font-weight: 700;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    border: 1px solid var(--gold-dark);
    padding: 16px 48px;
    cursor: pointer;
    border-radius: 2px;
    position: relative;
    transition: all 0.2s ease;
    box-shadow: 0 4px 20px rgba(139,26,26,0.4), inset 0 1px 0 rgba(255,255,255,0.1);
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 28px rgba(139,26,26,0.6), 0 0 20px rgba(201,168,76,0.2);
    border-color: var(--gold);
    color: #fff;
  }
  .btn-primary:active { transform: translateY(0); }

  /* ── PROGRESS BAR ─────────────────────────────── */
  .progress-wrap {
    margin-bottom: 28px;
  }
  .progress-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
  }
  .era-label {
    font-family: 'Cinzel', serif;
    font-size: 0.72rem;
    color: var(--gold);
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }
  .q-counter {
    font-family: 'Cinzel', serif;
    font-size: 0.72rem;
    color: var(--stone);
    letter-spacing: 0.1em;
  }
  .progress-bar-bg {
    height: 4px;
    background: rgba(255,255,255,0.05);
    border-radius: 2px;
    overflow: hidden;
  }
  .progress-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--crimson), var(--gold));
    border-radius: 2px;
    transition: width 0.5s ease;
  }

  /* ── SCORE BAR ────────────────────────────────── */
  .score-bar {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 8px;
    margin-bottom: 6px;
  }
  .score-label {
    font-family: 'Cinzel', serif;
    font-size: 0.72rem;
    color: var(--stone);
    letter-spacing: 0.1em;
  }
  .score-value {
    font-family: 'Cinzel Decorative', serif;
    font-size: 1rem;
    color: var(--gold);
  }

  /* ── QUESTION ─────────────────────────────────── */
  .question-era {
    font-family: 'Cinzel', serif;
    font-size: 0.7rem;
    color: var(--crimson-light);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .question-text {
    font-size: 1.35rem;
    color: var(--marble);
    line-height: 1.6;
    margin-bottom: 28px;
    font-weight: 600;
    min-height: 70px;
  }

  /* ── ANSWER OPTIONS ───────────────────────────── */
  .options-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 24px;
  }

  .option-btn {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(201,168,76,0.2);
    border-radius: 3px;
    padding: 16px 20px;
    cursor: pointer;
    transition: all 0.2s ease;
    display: flex;
    align-items: flex-start;
    gap: 14px;
    text-align: left;
    position: relative;
    overflow: hidden;
  }
  .option-btn::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(201,168,76,0.05), transparent);
    opacity: 0;
    transition: opacity 0.2s;
  }
  .option-btn:hover:not(:disabled) {
    border-color: var(--gold-dark);
    background: rgba(201,168,76,0.06);
    transform: translateY(-1px);
    box-shadow: 0 4px 16px rgba(0,0,0,0.3);
  }
  .option-btn:hover:not(:disabled)::before { opacity: 1; }

  .option-btn:disabled { cursor: default; }

  .option-btn.correct {
    border-color: #4CAF50;
    background: rgba(76,175,80,0.12);
    box-shadow: 0 0 16px rgba(76,175,80,0.2);
  }
  .option-btn.wrong {
    border-color: var(--crimson);
    background: rgba(139,26,26,0.15);
  }
  .option-btn.reveal-correct {
    border-color: #4CAF50;
    background: rgba(76,175,80,0.08);
  }

  .option-letter {
    font-family: 'Cinzel', serif;
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--gold-dark);
    min-width: 22px;
    height: 22px;
    border: 1px solid var(--gold-dark);
    border-radius: 2px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    margin-top: 1px;
  }
  .option-btn.correct .option-letter { border-color: #4CAF50; color: #4CAF50; }
  .option-btn.wrong .option-letter { border-color: var(--crimson); color: var(--crimson-light); }

  .option-text {
    font-size: 0.95rem;
    color: var(--marble-dark);
    line-height: 1.45;
  }

  /* ── FEEDBACK ─────────────────────────────────── */
  .feedback-box {
    border-radius: 3px;
    padding: 16px 20px;
    margin-bottom: 20px;
    display: none;
    animation: fadeSlide 0.3s ease;
  }
  .feedback-box.show { display: block; }
  .feedback-box.correct-fb {
    background: rgba(76,175,80,0.1);
    border: 1px solid rgba(76,175,80,0.3);
  }
  .feedback-box.wrong-fb {
    background: rgba(139,26,26,0.1);
    border: 1px solid rgba(139,26,26,0.3);
  }
  .feedback-title {
    font-family: 'Cinzel', serif;
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 6px;
  }
  .correct-fb .feedback-title { color: #4CAF50; }
  .wrong-fb .feedback-title { color: var(--crimson-light); }
  .feedback-text {
    font-size: 0.92rem;
    color: var(--marble-dark);
    line-height: 1.6;
    font-style: italic;
  }

  @keyframes fadeSlide {
    from { opacity: 0; transform: translateY(-8px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── NEXT BUTTON ──────────────────────────────── */
  .btn-next {
    display: none;
    margin: 0 auto;
    background: linear-gradient(135deg, var(--gold-dark), var(--gold), var(--gold-dark));
    color: var(--dark);
    font-family: 'Cinzel', serif;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    border: none;
    padding: 13px 40px;
    cursor: pointer;
    border-radius: 2px;
    transition: all 0.2s ease;
    box-shadow: 0 4px 16px rgba(201,168,76,0.3);
  }
  .btn-next.show { display: block; }
  .btn-next:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(201,168,76,0.4); }

  /* ── RESULTS ──────────────────────────────────── */
  .results-title {
    font-family: 'Cinzel Decorative', serif;
    font-size: 2.2rem;
    font-weight: 900;
    color: var(--gold);
    text-align: center;
    text-shadow: 0 0 30px rgba(201,168,76,0.4);
    margin-bottom: 8px;
  }

  .results-score-display {
    text-align: center;
    margin: 28px 0;
  }
  .score-big {
    font-family: 'Cinzel Decorative', serif;
    font-size: 5rem;
    color: var(--gold);
    line-height: 1;
    text-shadow: 0 0 40px rgba(201,168,76,0.5);
  }
  .score-total {
    font-family: 'Cinzel', serif;
    font-size: 1.2rem;
    color: var(--stone);
    margin-top: 4px;
  }

  .rank-badge {
    text-align: center;
    margin: 20px 0;
  }
  .rank-title {
    font-family: 'Cinzel', serif;
    font-size: 0.75rem;
    letter-spacing: 0.3em;
    color: var(--stone);
    text-transform: uppercase;
    margin-bottom: 6px;
  }
  .rank-name {
    font-family: 'Cinzel Decorative', serif;
    font-size: 1.6rem;
    color: var(--crimson-light);
    text-shadow: 0 0 20px rgba(192,57,43,0.4);
  }
  .rank-desc {
    font-size: 1rem;
    color: var(--marble-dark);
    font-style: italic;
    margin-top: 8px;
  }

  .review-list {
    margin: 28px 0;
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-height: 280px;
    overflow-y: auto;
    padding-right: 4px;
  }
  .review-list::-webkit-scrollbar { width: 4px; }
  .review-list::-webkit-scrollbar-track { background: rgba(255,255,255,0.03); }
  .review-list::-webkit-scrollbar-thumb { background: var(--gold-dark); border-radius: 2px; }

  .review-item {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 10px 14px;
    border-radius: 3px;
    font-size: 0.88rem;
  }
  .review-item.r-correct { background: rgba(76,175,80,0.08); border-left: 2px solid #4CAF50; }
  .review-item.r-wrong { background: rgba(139,26,26,0.08); border-left: 2px solid var(--crimson); }
  .review-icon { font-size: 1rem; flex-shrink: 0; }
  .review-q { color: var(--marble-dark); line-height: 1.4; }
  .review-a { font-size: 0.8rem; color: var(--stone); margin-top: 2px; }

  /* ── BIBLIOGRAPHY ─────────────────────────────── */
  .bib-section {
    margin-top: 32px;
    padding-top: 24px;
    border-top: 1px solid rgba(201,168,76,0.15);
  }
  .bib-title {
    font-family: 'Cinzel', serif;
    font-size: 0.75rem;
    letter-spacing: 0.25em;
    color: var(--gold-dark);
    text-transform: uppercase;
    margin-bottom: 14px;
  }
  .bib-list { list-style: none; display: flex; flex-direction: column; gap: 7px; }
  .bib-list li { font-size: 0.82rem; color: var(--stone); }
  .bib-list a {
    color: var(--gold-dark);
    text-decoration: none;
    transition: color 0.2s;
    word-break: break-all;
  }
  .bib-list a:hover { color: var(--gold); text-decoration: underline; }

  /* ── EAGLE ICON ───────────────────────────────── */
  .eagle {
    text-align: center;
    font-size: 3.5rem;
    margin-bottom: 16px;
    filter: drop-shadow(0 0 12px rgba(201,168,76,0.4));
    animation: float 3s ease-in-out infinite;
  }
  @keyframes float {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-6px); }
  }

  /* ── RESPONSIVE ───────────────────────────────── */
  @media (max-width: 560px) {
    .card { padding: 32px 24px; }
    .title-main { font-size: 2rem; }
    .options-grid { grid-template-columns: 1fr; }
    .score-big { font-size: 3.5rem; }
  }
</style>
</head>
<body>
<div class="wrapper">

  <!-- ════════════════ INTRO SCREEN ════════════════ -->
  <div class="screen active" id="screen-intro">
    <div class="card">
      <div class="corner corner-tl"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-tr"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-bl"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-br"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>

      <div class="eagle">🦅</div>
      <div class="title-main">ROMA AETERNA</div>
      <div class="title-sub">The History of the Eternal City</div>

      <div class="divider"><div class="divider-line"></div><div class="divider-dot"></div><div class="divider-line"></div></div>

      <p class="intro-text">
        From the she-wolf of Romulus to the fall of the last emperor,<br>
        test your knowledge of one of history's greatest civilizations.<br><br>
        <strong style="color:var(--gold); font-style:normal;">20 questions · 4 eras of Roman history</strong>
      </p>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:32px;">
        <div style="text-align:center;padding:16px;border:1px solid rgba(201,168,76,0.15);border-radius:3px;">
          <div style="font-family:'Cinzel',serif;font-size:0.65rem;letter-spacing:0.2em;color:var(--stone);text-transform:uppercase;margin-bottom:6px;">Era I</div>
          <div style="font-family:'Cinzel',serif;font-size:0.9rem;color:var(--gold-dark);">The Kingdom</div>
          <div style="font-size:0.78rem;color:var(--stone);margin-top:4px;font-style:italic;">753 – 509 BC</div>
        </div>
        <div style="text-align:center;padding:16px;border:1px solid rgba(201,168,76,0.15);border-radius:3px;">
          <div style="font-family:'Cinzel',serif;font-size:0.65rem;letter-spacing:0.2em;color:var(--stone);text-transform:uppercase;margin-bottom:6px;">Era II</div>
          <div style="font-family:'Cinzel',serif;font-size:0.9rem;color:var(--gold-dark);">The Republic</div>
          <div style="font-size:0.78rem;color:var(--stone);margin-top:4px;font-style:italic;">509 – 44 BC</div>
        </div>
        <div style="text-align:center;padding:16px;border:1px solid rgba(201,168,76,0.15);border-radius:3px;">
          <div style="font-family:'Cinzel',serif;font-size:0.65rem;letter-spacing:0.2em;color:var(--stone);text-transform:uppercase;margin-bottom:6px;">Era III</div>
          <div style="font-family:'Cinzel',serif;font-size:0.9rem;color:var(--gold-dark);">The Empire</div>
          <div style="font-size:0.78rem;color:var(--stone);margin-top:4px;font-style:italic;">27 BC – 284 AD</div>
        </div>
        <div style="text-align:center;padding:16px;border:1px solid rgba(201,168,76,0.15);border-radius:3px;">
          <div style="font-family:'Cinzel',serif;font-size:0.65rem;letter-spacing:0.2em;color:var(--stone);text-transform:uppercase;margin-bottom:6px;">Era IV</div>
          <div style="font-family:'Cinzel',serif;font-size:0.9rem;color:var(--gold-dark);">The Fall</div>
          <div style="font-size:0.78rem;color:var(--stone);margin-top:4px;font-style:italic;">284 – 476 AD</div>
        </div>
      </div>

      <button class="btn-primary" onclick="startGame()">⚔ BEGIN THE TRIAL ⚔</button>
    </div>
  </div>

  <!-- ════════════════ QUIZ SCREEN ════════════════ -->
  <div class="screen" id="screen-quiz">
    <div class="card">
      <div class="corner corner-tl"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-tr"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>

      <div class="score-bar">
        <span class="score-label">SCORE</span>
        <span class="score-value" id="score-display">0</span>
      </div>

      <div class="progress-wrap">
        <div class="progress-info">
          <span class="era-label" id="era-label">Era I: The Kingdom</span>
          <span class="q-counter" id="q-counter">1 / 20</span>
        </div>
        <div class="progress-bar-bg">
          <div class="progress-bar-fill" id="progress-fill" style="width:5%"></div>
        </div>
      </div>

      <div class="question-era" id="question-era">THE KINGDOM · 753–509 BC</div>
      <div class="question-text" id="question-text">Loading question…</div>

      <div class="options-grid" id="options-grid"></div>

      <div class="feedback-box" id="feedback-box">
        <div class="feedback-title" id="feedback-title">Correct!</div>
        <div class="feedback-text" id="feedback-text"></div>
      </div>

      <button class="btn-next" id="btn-next" onclick="nextQuestion()">Onward →</button>
    </div>
  </div>

  <!-- ════════════════ RESULTS SCREEN ════════════════ -->
  <div class="screen" id="screen-results">
    <div class="card">
      <div class="corner corner-tl"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-tr"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-bl"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>
      <div class="corner corner-br"><svg viewBox="0 0 36 36"><path d="M2 2 L18 2 L2 18 Z" fill="none" stroke="#C9A84C" stroke-width="1.5"/><circle cx="18" cy="18" r="3" fill="#C9A84C"/></svg></div>

      <div class="results-title">TABULA FINALIS</div>
      <div class="title-sub" style="margin-bottom:0">Your Final Score</div>

      <div class="divider"><div class="divider-line"></div><div class="divider-dot"></div><div class="divider-line"></div></div>

      <div class="results-score-display">
        <div class="score-big" id="final-score">0</div>
        <div class="score-total" id="final-total">out of 20</div>
      </div>

      <div class="rank-badge">
        <div class="rank-title">Your Roman Rank</div>
        <div class="rank-name" id="rank-name">Citizen</div>
        <div class="rank-desc" id="rank-desc"></div>
      </div>

      <div class="divider"><div class="divider-line"></div><div class="divider-dot"></div><div class="divider-line"></div></div>

      <div class="review-list" id="review-list"></div>

      <button class="btn-primary" onclick="restartGame()" style="margin-bottom:24px;">⚔ Play Again ⚔</button>

      <!-- BIBLIOGRAPHY -->
      <div class="bib-section">
        <div class="bib-title">📜 Bibliography — Sources Used</div>
        <ul class="bib-list">
          <li>• Wikipedia — <a href="https://en.wikipedia.org/wiki/Ancient_Rome" target="_blank">Ancient Rome</a></li>
          <li>• Wikipedia — <a href="https://en.wikipedia.org/wiki/Timeline_of_Roman_history" target="_blank">Timeline of Roman History</a></li>
          <li>• Britannica — <a href="https://www.britannica.com/place/Timeline-of-the-Roman-Empire" target="_blank">Timeline of the Roman Empire</a></li>
          <li>• Milwaukee Public Museum — <a href="https://www.mpm.edu/research-collections/anthropology/anthropology-collections-research/mediterranean-oil-lamps/roman-empire-brief-history" target="_blank">The Roman Empire: A Brief History</a></li>
          <li>• World History Encyclopedia — <a href="https://www.worldhistory.org/timeline/Rome/" target="_blank">Rome Timeline</a></li>
          <li>• History Cooperative — <a href="https://historycooperative.org/roman-empire-timeline/" target="_blank">The Complete Roman Empire Timeline</a></li>
          <li>• Madaïn Project — <a href="https://madainproject.com/timeline_of_ancient_rome" target="_blank">Timeline of Ancient Rome</a></li>
          <li>• Ducksters — <a href="https://www.ducksters.com/history/ancient_rome_timeline.php" target="_blank">Ancient Rome Timeline for Kids</a></li>
          <li>• History Hit — <a href="https://www.historyhit.com/a-concise-chronology-of-ancient-rome-1229-years-of-significant-events/" target="_blank">1,229 Years of Significant Events</a></li>
          <li>• UTEP Layers of Rome — <a href="https://layersofrome.utep.edu/roman-timeline" target="_blank">Roman Timeline (Interactive)</a></li>
        </ul>
      </div>
    </div>
  </div>

</div>

<script>
const QUESTIONS = [
  // ── ERA I: THE KINGDOM (753–509 BC) ──────────────────────────────
  {
    era: "Era I: The Kingdom",
    eraTag: "THE KINGDOM · 753–509 BC",
    question: "According to Roman legend, who founded the city of Rome on April 21, 753 BC?",
    options: ["Julius Caesar", "Romulus", "Augustus", "Numa Pompilius"],
    answer: 1,
    fact: "Legend says twin brothers Romulus and Remus, sons of the war god Mars, founded Rome. After a dispute over who would rule, Romulus killed Remus and named the city after himself, becoming its first king."
  },
  {
    era: "Era I: The Kingdom",
    eraTag: "THE KINGDOM · 753–509 BC",
    question: "According to myth, who nursed the twin founders of Rome after they were abandoned as infants?",
    options: ["A priestess of Vesta", "A she-wolf", "The goddess Juno", "A Trojan refugee"],
    answer: 1,
    fact: "The famous myth holds that Romulus and Remus were suckled by a she-wolf (lupa) on the banks of the Tiber. The iconic 'Capitoline Wolf' bronze sculpture commemorates this legend."
  },
  {
    era: "Era I: The Kingdom",
    eraTag: "THE KINGDOM · 753–509 BC",
    question: "How many kings ruled Rome during the Regal Period before the Republic was established?",
    options: ["Five", "Six", "Seven", "Nine"],
    answer: 2,
    fact: "Seven legendary kings ruled Rome: Romulus, Numa Pompilius, Tullus Hostilius, Ancus Marcius, Lucius Tarquinius Priscus, Servius Tullius, and finally the tyrannical Tarquinius Superbus (Tarquin the Proud)."
  },
  {
    era: "Era I: The Kingdom",
    eraTag: "THE KINGDOM · 753–509 BC",
    question: "Which king was overthrown in 509 BC, ending the Roman Kingdom and beginning the Republic?",
    options: ["Numa Pompilius", "Servius Tullius", "Lucius Tarquinius Superbus", "Ancus Marcius"],
    answer: 2,
    fact: "Tarquinius Superbus (Tarquin the Proud) was deposed in 509 BC. His tyranny and his son's assault on the noblewoman Lucretia sparked the rebellion led by Lucius Junius Brutus, who expelled the king and established the Republic."
  },

  // ── ERA II: THE REPUBLIC (509–44 BC) ──────────────────────────────
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "After the kings were expelled in 509 BC, Rome was governed by two annually-elected officials called what?",
    options: ["Tribunes", "Praetors", "Consuls", "Censors"],
    answer: 2,
    fact: "The Roman Republic replaced the king with two consuls elected annually. This prevented any one person from gaining too much power. The first consuls were Lucius Junius Brutus and Lucius Tarquinius Collatinus."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "The 'Twelve Tables,' Rome's first written legal code, was established around which year?",
    options: ["509 BC", "451 BC", "338 BC", "264 BC"],
    answer: 1,
    fact: "Around 451 BC, the Romans created the Twelve Tables — a standardized code covering public, private, and political law. This was a major victory for the plebeians, who demanded that laws be written down so they couldn't be manipulated by the patrician judges."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "During the Punic Wars (264–146 BC), Rome's greatest enemy was which North African power?",
    options: ["Egypt", "Carthage", "Numidia", "The Seleucid Empire"],
    answer: 1,
    fact: "Rome fought three Punic Wars against Carthage (modern Tunisia). These wars were existential for Rome — especially when the Carthaginian general Hannibal invaded Italy. Rome ultimately won, destroyed Carthage in 146 BC, and became the dominant Mediterranean power."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "Which Carthaginian general famously crossed the Alps with war elephants to invade Italy in 218 BC?",
    options: ["Hamilcar Barca", "Hasdrubal", "Hannibal Barca", "Scipio Africanus"],
    answer: 2,
    fact: "Hannibal Barca made one of history's most audacious military moves — crossing the Alps with about 37 war elephants and 38,000 troops. He devastated Roman armies at battles like Trebia, Lake Trasimene, and Cannae, but never directly attacked Rome itself."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "Julius Caesar crossed which river in 49 BC, declaring 'The die is cast' and starting a civil war?",
    options: ["The Tiber", "The Po", "The Rubicon", "The Rhine"],
    answer: 2,
    fact: "The Rubicon was a small river in northern Italy that marked the boundary of Italy proper. Roman law forbade generals from crossing it with their army. When Caesar crossed it in 49 BC, it was an act of war against the Senate — making 'crossing the Rubicon' a phrase for a point of no return."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "Julius Caesar was assassinated on the 'Ides of March' — what date is that?",
    options: ["March 1, 44 BC", "March 15, 44 BC", "March 25, 44 BC", "March 31, 44 BC"],
    answer: 1,
    fact: "On March 15, 44 BC — the 'Ides of March' — Julius Caesar was stabbed 23 times by a group of senators including Marcus Brutus and Gaius Cassius Longinus. The conspirators feared he would make himself king and destroy the Republic."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "Which Roman general and statesman was Caesar's great rival, whom Caesar defeated in civil war?",
    options: ["Crassus", "Mark Antony", "Pompey the Great", "Cicero"],
    answer: 2,
    fact: "Gnaeus Pompeius Magnus (Pompey the Great) was once Caesar's ally in the First Triumvirate along with Crassus. After Crassus died, the two rivals clashed. Caesar defeated Pompey at the Battle of Pharsalus in 48 BC. Pompey fled to Egypt, where he was assassinated."
  },
  {
    era: "Era II: The Republic",
    eraTag: "THE REPUBLIC · 509–44 BC",
    question: "The First Triumvirate — an unofficial political alliance — consisted of Caesar, Pompey, and which third man?",
    options: ["Cicero", "Crassus", "Mark Antony", "Brutus"],
    answer: 1,
    fact: "Marcus Licinius Crassus, the wealthiest man in Rome, joined Caesar and Pompey in 60 BC to form the First Triumvirate. Crassus died in 53 BC at the disastrous Battle of Carrhae against the Parthians, where Roman legions were decimated."
  },

  // ── ERA III: THE EMPIRE (27 BC – 284 AD) ──────────────────────────
  {
    era: "Era III: The Empire",
    eraTag: "THE EMPIRE · 27 BC – 284 AD",
    question: "Who became Rome's first emperor in 27 BC, beginning the Imperial period?",
    options: ["Julius Caesar", "Mark Antony", "Caesar Augustus", "Tiberius"],
    answer: 2,
    fact: "Gaius Octavius Thurinus, Caesar's adopted son, defeated Mark Antony and Cleopatra at the Battle of Actium in 31 BC. In 27 BC, the Senate granted him the title 'Augustus' (meaning 'the revered one'), making him Rome's first emperor."
  },
  {
    era: "Era III: The Empire",
    eraTag: "THE EMPIRE · 27 BC – 284 AD",
    question: "The 'Pax Romana' — a period of relative peace and prosperity — lasted roughly how long?",
    options: ["About 50 years", "About 100 years", "About 200 years", "About 300 years"],
    answer: 2,
    fact: "The Pax Romana ('Roman Peace') lasted approximately 206 years, from the reign of Augustus (27 BC) through the reign of Marcus Aurelius (180 AD). During this period Rome saw massive expansion, architectural achievements, and relative stability."
  },
  {
    era: "Era III: The Empire",
    eraTag: "THE EMPIRE · 27 BC – 284 AD",
    question: "The Colosseum in Rome, completed around 80 AD, could seat approximately how many spectators?",
    options: ["10,000", "30,000", "50,000", "100,000"],
    answer: 2,
    fact: "The Flavian Amphitheatre (the Colosseum) was completed under Emperor Titus around 80 AD and could hold an estimated 50,000–80,000 spectators. Emperor Titus opened it with 100 days of gladiatorial games. Emperor Vespasian had begun its construction in 72 AD."
  },
  {
    era: "Era III: The Empire",
    eraTag: "THE EMPIRE · 27 BC – 284 AD",
    question: "Which volcano erupted in 79 AD, burying the Roman cities of Pompeii and Herculaneum in ash?",
    options: ["Mount Etna", "Mount Vesuvius", "Stromboli", "Mount Olympus"],
    answer: 1,
    fact: "Mount Vesuvius erupted catastrophically in August 79 AD, burying Pompeii under 4–6 meters of volcanic ash and pumice. The preserved ruins give us an extraordinary snapshot of daily Roman life, including bakeries, brothels, homes, and graffiti."
  },
  {
    era: "Era III: The Empire",
    eraTag: "THE EMPIRE · 27 BC – 284 AD",
    question: "Emperor Hadrian built a famous wall across northern Britain around 122 AD. What was its primary purpose?",
    options: ["To mark Rome's border and control movement", "To protect against Scottish tribes only", "As a aqueduct system", "To house Roman legions permanently"],
    answer: 0,
    fact: "Hadrian's Wall stretched 118 km across northern Britain, built starting in 122 AD. It marked the northern frontier of the Roman Empire and controlled movement of people and goods. It had forts, milecastles, and turrets along its entire length."
  },

  // ── ERA IV: THE FALL (284–476 AD) ─────────────────────────────────
  {
    era: "Era IV: The Fall",
    eraTag: "THE FALL · 284–476 AD",
    question: "Emperor Constantine made Christianity the favoured religion of Rome. In which year did he issue the Edict of Milan granting religious tolerance?",
    options: ["284 AD", "313 AD", "380 AD", "410 AD"],
    answer: 1,
    fact: "In 313 AD, Constantine and co-emperor Licinius issued the Edict of Milan, granting religious tolerance throughout the empire. Constantine was the first Roman emperor to convert to Christianity. He also moved the capital to Byzantium, renaming it Constantinople."
  },
  {
    era: "Era IV: The Fall",
    eraTag: "THE FALL · 284–476 AD",
    question: "In 395 AD, the Roman Empire was permanently divided. What were the two halves called?",
    options: ["Northern and Southern Empires", "Latin and Greek Empires", "Western and Eastern Roman Empires", "Continental and Mediterranean Empires"],
    answer: 2,
    fact: "Upon the death of Emperor Theodosius I in 395 AD, the empire was split between his two sons. The Western Roman Empire (capital: Ravenna/Rome) and the Eastern Roman Empire (capital: Constantinople) — later known as the Byzantine Empire — went their separate ways."
  },
  {
    era: "Era IV: The Fall",
    eraTag: "THE FALL · 284–476 AD",
    question: "In 410 AD, Rome was sacked for the first time in 800 years. Which Germanic group led by Alaric I was responsible?",
    options: ["The Vandals", "The Huns", "The Visigoths", "The Ostrogoths"],
    answer: 2,
    fact: "The Visigoths under Alaric I sacked Rome in 410 AD — a devastating psychological blow to the empire. It was the first time a foreign enemy had taken Rome since the Gauls under Brennus in 390 BC. Saint Augustine cited this event as inspiration for writing 'The City of God.'"
  },
  {
    era: "Era IV: The Fall",
    eraTag: "THE FALL · 284–476 AD",
    question: "The Western Roman Empire officially fell in 476 AD when the last emperor was deposed. What was his name?",
    options: ["Constantine XI", "Romulus Augustulus", "Honorius", "Valentinian III"],
    answer: 1,
    fact: "Romulus Augustulus, ironically named after Rome's founder (Romulus) and first emperor (Augustus), was deposed by the Germanic chieftain Odoacer in 476 AD. This event traditionally marks the end of Ancient Rome and the beginning of the Middle Ages in Western Europe."
  }
];

let currentQ = 0;
let score = 0;
let answers = [];

function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function startGame() {
  currentQ = 0;
  score = 0;
  answers = [];
  showScreen('screen-quiz');
  renderQuestion();
}

function renderQuestion() {
  const q = QUESTIONS[currentQ];
  const pct = ((currentQ + 1) / QUESTIONS.length) * 100;

  document.getElementById('era-label').textContent = q.era;
  document.getElementById('q-counter').textContent = `${currentQ + 1} / ${QUESTIONS.length}`;
  document.getElementById('progress-fill').style.width = pct + '%';
  document.getElementById('score-display').textContent = score;
  document.getElementById('question-era').textContent = q.eraTag;
  document.getElementById('question-text').textContent = q.question;

  const grid = document.getElementById('options-grid');
  grid.innerHTML = '';
  const letters = ['A','B','C','D'];
  q.options.forEach((opt, i) => {
    const btn = document.createElement('button');
    btn.className = 'option-btn';
    btn.innerHTML = `<span class="option-letter">${letters[i]}</span><span class="option-text">${opt}</span>`;
    btn.onclick = () => selectAnswer(i);
    grid.appendChild(btn);
  });

  const fb = document.getElementById('feedback-box');
  fb.className = 'feedback-box';
  document.getElementById('btn-next').className = 'btn-next';
}

function selectAnswer(idx) {
  const q = QUESTIONS[currentQ];
  const btns = document.querySelectorAll('.option-btn');
  btns.forEach(b => b.disabled = true);

  const isCorrect = idx === q.answer;
  if (isCorrect) score++;

  answers.push({ q: q.question, correct: isCorrect, answer: q.options[q.answer] });

  btns[idx].classList.add(isCorrect ? 'correct' : 'wrong');
  if (!isCorrect) btns[q.answer].classList.add('reveal-correct');

  const fb = document.getElementById('feedback-box');
  fb.className = `feedback-box show ${isCorrect ? 'correct-fb' : 'wrong-fb'}`;
  document.getElementById('feedback-title').textContent = isCorrect ? '✓ Correct!' : '✗ Not quite…';
  document.getElementById('feedback-text').textContent = q.fact;

  document.getElementById('score-display').textContent = score;
  document.getElementById('btn-next').className = 'btn-next show';
}

function nextQuestion() {
  currentQ++;
  if (currentQ >= QUESTIONS.length) {
    showResults();
  } else {
    renderQuestion();
  }
}

function showResults() {
  showScreen('screen-results');
  document.getElementById('final-score').textContent = score;
  document.getElementById('final-total').textContent = `out of ${QUESTIONS.length}`;

  const pct = score / QUESTIONS.length;
  let rank, desc;
  if (pct >= 0.95) { rank = 'Imperator'; desc = 'Supreme commander — you know Rome as well as Caesar himself.'; }
  else if (pct >= 0.85) { rank = 'Consul'; desc = 'Highest office of the Republic — an exceptional showing!'; }
  else if (pct >= 0.70) { rank = 'Centurion'; desc = 'Battle-hardened and knowledgeable — a fine Roman soldier.'; }
  else if (pct >= 0.55) { rank = 'Legionary'; desc = 'A member of the legions — keep studying and you will rise.'; }
  else if (pct >= 0.40) { rank = 'Plebeian'; desc = 'A free citizen — but the Senate awaits those who study harder.'; }
  else { rank = 'Barbarian'; desc = 'Not yet worthy of Rome — but the Eternal City welcomes all who learn!'; }

  document.getElementById('rank-name').textContent = rank;
  document.getElementById('rank-desc').textContent = desc;

  const reviewList = document.getElementById('review-list');
  reviewList.innerHTML = '';
  answers.forEach((a, i) => {
    const div = document.createElement('div');
    div.className = `review-item ${a.correct ? 'r-correct' : 'r-wrong'}`;
    div.innerHTML = `
      <span class="review-icon">${a.correct ? '✓' : '✗'}</span>
      <div>
        <div class="review-q">Q${i+1}: ${a.q}</div>
        ${!a.correct ? `<div class="review-a">Answer: ${a.answer}</div>` : ''}
      </div>`;
    reviewList.appendChild(div);
  });
}

function restartGame() {
  startGame();
}
</script>
</body>
</html>
