<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Soft Life Calculator — What Does Your Dream Life Actually Cost?</title>
  <meta name="description" content="Design your dream lifestyle and discover exactly what it costs. Calculate your Soft Life Number — the monthly income you need to live the life you actually want." />
  <meta property="og:title" content="Soft Life Calculator" />
  <meta property="og:description" content="What does your dream life actually cost? Find out in 60 seconds." />
  <meta property="og:type" content="website" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #080810;
      --surface: #10101e;
      --surface2: #16162a;
      --border: rgba(255,255,255,0.07);
      --gold: #c9a84c;
      --gold-light: #e8c97a;
      --gold-dim: rgba(201,168,76,0.15);
      --purple: #7c5cbf;
      --purple-light: #a07de0;
      --text: #f0f0f0;
      --text-dim: #888;
      --text-muted: #555;
      --green: #34d399;
      --red: #f87171;
      --radius: 16px;
    }
    html { scroll-behavior: smooth; }
    body {
      font-family: 'Inter', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      overflow-x: hidden;
    }
    /* ── Background ── */
    .bg-orbs {
      position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden;
    }
    .orb {
      position: absolute; border-radius: 50%; filter: blur(120px); opacity: 0.15;
      animation: drift 20s ease-in-out infinite alternate;
    }
    .orb-1 { width: 600px; height: 600px; background: var(--purple); top: -200px; left: -200px; animation-delay: 0s; }
    .orb-2 { width: 500px; height: 500px; background: var(--gold); bottom: -150px; right: -100px; animation-delay: -8s; }
    .orb-3 { width: 300px; height: 300px; background: #2563eb; top: 40%; left: 50%; animation-delay: -4s; }
    @keyframes drift {
      from { transform: translate(0, 0) scale(1); }
      to   { transform: translate(40px, 30px) scale(1.1); }
    }
    /* ── App Shell ── */
    #app {
      position: relative; z-index: 1;
      max-width: 780px; margin: 0 auto;
      padding: 0 20px 80px;
    }
    /* ── Header ── */
    header {
      text-align: center;
      padding: 60px 20px 0;
    }
    .badge {
      display: inline-block;
      background: var(--gold-dim);
      border: 1px solid rgba(201,168,76,0.3);
      color: var(--gold-light);
      font-size: 11px; font-weight: 600; letter-spacing: 2px;
      text-transform: uppercase;
      padding: 6px 16px; border-radius: 100px;
      margin-bottom: 24px;
    }
    h1 {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2.2rem, 6vw, 3.8rem);
      line-height: 1.1;
      background: linear-gradient(135deg, #fff 0%, var(--gold-light) 60%, var(--purple-light) 100%);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 16px;
    }
    .subtitle {
      font-size: 1.05rem; color: var(--text-dim); line-height: 1.6;
      max-width: 480px; margin: 0 auto 40px;
    }
    /* ── Progress ── */
    .progress-wrap {
      display: flex; align-items: center; gap: 8px;
      margin-bottom: 40px; padding: 0 4px;
    }
    .progress-track {
      flex: 1; height: 3px; background: var(--surface2); border-radius: 100px; overflow: hidden;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--purple), var(--gold));
      border-radius: 100px;
      transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .progress-label {
      font-size: 11px; color: var(--text-muted); white-space: nowrap; font-weight: 500;
    }
    /* ── Step ── */
    .step {
      display: none; animation: fadeSlide 0.4s ease;
    }
    .step.active { display: block; }
    @keyframes fadeSlide {
      from { opacity: 0; transform: translateY(18px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    .step-header {
      margin-bottom: 28px;
    }
    .step-icon {
      font-size: 2rem; margin-bottom: 12px; display: block;
    }
    .step-title {
      font-size: 1.5rem; font-weight: 700; margin-bottom: 8px;
    }
    .step-desc {
      color: var(--text-dim); font-size: 0.9rem;
    }
    /* ── Option Cards ── */
    .options-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 12px;
    }
    .option-card {
      background: var(--surface);
      border: 1.5px solid var(--border);
      border-radius: var(--radius);
      padding: 18px 16px;
      cursor: pointer;
      transition: all 0.2s ease;
      position: relative; overflow: hidden;
      -webkit-tap-highlight-color: transparent;
    }
    .option-card::before {
      content: '';
      position: absolute; inset: 0;
      background: linear-gradient(135deg, var(--purple), var(--gold));
      opacity: 0; transition: opacity 0.2s;
    }
    .option-card:hover { border-color: rgba(201,168,76,0.4); transform: translateY(-2px); }
    .option-card.selected {
      border-color: var(--gold);
      background: var(--surface2);
    }
    .option-card.selected::before { opacity: 0.07; }
    .option-emoji { font-size: 1.6rem; margin-bottom: 10px; display: block; position: relative; }
    .option-name {
      font-weight: 600; font-size: 0.9rem; margin-bottom: 4px; position: relative;
    }
    .option-price {
      font-size: 0.78rem; color: var(--gold-light); font-weight: 500; position: relative;
    }
    .option-note {
      font-size: 0.72rem; color: var(--text-muted); margin-top: 4px; position: relative;
    }
    .check-badge {
      position: absolute; top: 10px; right: 10px;
      width: 20px; height: 20px; border-radius: 50%;
      background: var(--gold);
      display: flex; align-items: center; justify-content: center;
      font-size: 10px; opacity: 0; transition: opacity 0.2s;
    }
    .option-card.selected .check-badge { opacity: 1; }
    /* ── Nav Buttons ── */
    .nav-row {
      display: flex; justify-content: space-between; align-items: center;
      margin-top: 32px; gap: 12px;
    }
    .btn {
      padding: 14px 28px; border-radius: 100px; font-size: 0.9rem;
      font-weight: 600; font-family: 'Inter', sans-serif; cursor: pointer;
      border: none; transition: all 0.2s ease; letter-spacing: 0.3px;
    }
    .btn-primary {
      background: linear-gradient(135deg, var(--purple), var(--gold));
      color: #fff;
      box-shadow: 0 4px 20px rgba(124,92,191,0.3);
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 28px rgba(124,92,191,0.45); }
    .btn-primary:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }
    .btn-ghost {
      background: transparent; color: var(--text-dim);
      border: 1.5px solid var(--border);
    }
    .btn-ghost:hover { border-color: rgba(255,255,255,0.2); color: var(--text); }
    /* ── Running Total ── */
    .running-total {
      display: flex; align-items: center; justify-content: center; gap: 8px;
      font-size: 0.8rem; color: var(--text-muted);
    }
    .running-total span { color: var(--gold-light); font-weight: 600; font-size: 0.9rem; }
    /* ── Results ── */
    #step-result {
      display: none;
    }
    #step-result.active { display: block; }
    .result-hero {
      text-align: center; padding: 50px 20px 40px; position: relative;
    }
    .result-label {
      font-size: 0.8rem; letter-spacing: 2px; text-transform: uppercase;
      color: var(--text-muted); font-weight: 600; margin-bottom: 16px;
    }
    .result-number {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3.5rem, 12vw, 6rem);
      background: linear-gradient(135deg, #fff, var(--gold-light), var(--purple-light));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      background-clip: text;
      line-height: 1; margin-bottom: 8px;
      animation: countUp 1.5s ease forwards;
    }
    .result-per { font-size: 1rem; color: var(--text-dim); margin-bottom: 30px; }
    @keyframes countUp {
      from { opacity: 0; transform: scale(0.8); }
      to   { opacity: 1; transform: scale(1); }
    }
    .result-context {
      display: flex; gap: 16px; justify-content: center; flex-wrap: wrap;
      margin-bottom: 40px;
    }
    .context-chip {
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 100px;
      padding: 8px 16px;
      font-size: 0.8rem; color: var(--text-dim);
    }
    .context-chip strong { color: var(--text); }
    /* ── Breakdown ── */
    .breakdown {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      overflow: hidden; margin-bottom: 24px;
    }
    .breakdown-header {
      padding: 16px 20px;
      border-bottom: 1px solid var(--border);
      font-size: 0.8rem; font-weight: 600;
      letter-spacing: 1px; text-transform: uppercase; color: var(--text-muted);
      display: flex; justify-content: space-between;
    }
    .breakdown-row {
      display: flex; justify-content: space-between; align-items: center;
      padding: 14px 20px; border-bottom: 1px solid var(--border);
      transition: background 0.15s;
    }
    .breakdown-row:last-child { border-bottom: none; }
    .breakdown-row:hover { background: var(--surface2); }
    .breakdown-cat { display: flex; align-items: center; gap: 10px; font-size: 0.88rem; }
    .breakdown-icon { font-size: 1.1rem; }
    .breakdown-label { color: var(--text-dim); font-size: 0.78rem; margin-top: 2px; }
    .breakdown-val { font-weight: 600; color: var(--gold-light); font-size: 0.9rem; }
    /* ── Income gap ── */
    .gap-card {
      background: linear-gradient(135deg, rgba(124,92,191,0.15), rgba(201,168,76,0.1));
      border: 1px solid rgba(201,168,76,0.2);
      border-radius: var(--radius);
      padding: 28px; margin-bottom: 24px; text-align: center;
    }
    .gap-title { font-size: 0.8rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 12px; }
    .gap-number { font-size: 2.4rem; font-weight: 800; color: var(--text); margin-bottom: 8px; }
    .gap-desc { font-size: 0.85rem; color: var(--text-dim); line-height: 1.5; }
    /* ── Affiliate section ── */
    .affiliate-section {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 28px; margin-bottom: 24px;
    }
    .affiliate-heading {
      font-size: 1.1rem; font-weight: 700; margin-bottom: 6px;
    }
    .affiliate-sub { font-size: 0.85rem; color: var(--text-dim); margin-bottom: 20px; line-height: 1.5; }
    .affiliate-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
    @media (max-width: 500px) { .affiliate-cards { grid-template-columns: 1fr; } }
    .affiliate-card {
      background: var(--surface2);
      border: 1.5px solid var(--border);
      border-radius: 12px; padding: 18px 16px;
      text-decoration: none; color: var(--text);
      transition: all 0.2s ease; display: block;
    }
    .affiliate-card:hover { border-color: var(--gold); transform: translateY(-2px); }
    .aff-name { font-weight: 700; font-size: 0.95rem; margin-bottom: 4px; }
    .aff-desc { font-size: 0.78rem; color: var(--text-dim); line-height: 1.4; }
    .aff-cta {
      margin-top: 10px; font-size: 0.75rem; color: var(--gold-light);
      font-weight: 600; display: flex; align-items: center; gap: 4px;
    }
    /* ── Share ── */
    .share-section { text-align: center; margin-bottom: 40px; }
    .share-label { font-size: 0.85rem; color: var(--text-muted); margin-bottom: 14px; }
    .share-btns { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
    .share-btn {
      padding: 10px 20px; border-radius: 100px; font-size: 0.82rem; font-weight: 600;
      cursor: pointer; border: 1.5px solid var(--border); background: var(--surface);
      color: var(--text); font-family: 'Inter', sans-serif;
      display: flex; align-items: center; gap: 8px; transition: all 0.2s;
    }
    .share-btn:hover { border-color: rgba(255,255,255,0.25); background: var(--surface2); }
    .share-btn.copied { border-color: var(--green); color: var(--green); }
    .restart-btn {
      display: block; margin: 0 auto 20px; padding: 12px 28px;
      background: transparent; border: 1.5px solid var(--border);
      border-radius: 100px; color: var(--text-dim); font-size: 0.85rem;
      font-family: 'Inter', sans-serif; cursor: pointer; transition: all 0.2s;
    }
    .restart-btn:hover { border-color: rgba(255,255,255,0.2); color: var(--text); }
    /* ── City grid ── */
    .city-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
      gap: 10px;
    }
    .city-card {
      background: var(--surface);
      border: 1.5px solid var(--border);
      border-radius: 12px; padding: 14px 12px;
      cursor: pointer; transition: all 0.2s; text-align: center;
      position: relative; overflow: hidden;
    }
    .city-card:hover { border-color: rgba(201,168,76,0.4); transform: translateY(-2px); }
    .city-card.selected { border-color: var(--gold); background: var(--surface2); }
    .city-emoji { font-size: 1.4rem; display: block; margin-bottom: 6px; }
    .city-name { font-size: 0.82rem; font-weight: 600; }
    .city-vibe { font-size: 0.7rem; color: var(--text-muted); margin-top: 2px; }
    .city-card .check-badge { top: 8px; right: 8px; width: 16px; height: 16px; font-size: 8px; }
    /* ── Tooltips/Info ── */
    .info-note {
      font-size: 0.75rem; color: var(--text-muted);
      border-left: 2px solid var(--gold-dim);
      padding: 8px 12px; margin-top: 16px;
      background: rgba(201,168,76,0.04); border-radius: 0 8px 8px 0;
    }
    /* ── Income input step ── */
    .income-wrap {
      background: var(--surface);
      border: 1.5px solid var(--border);
      border-radius: var(--radius); padding: 24px;
    }
    .income-label { font-size: 0.85rem; color: var(--text-dim); margin-bottom: 8px; }
    .income-input-row {
      display: flex; align-items: center; gap: 12px;
    }
    .currency-sign { font-size: 1.4rem; font-weight: 700; color: var(--gold-light); }
    .income-input {
      background: var(--surface2); border: 1.5px solid var(--border);
      border-radius: 10px; padding: 14px 16px;
      color: var(--text); font-size: 1.3rem; font-weight: 700;
      font-family: 'Inter', sans-serif; width: 100%;
      transition: border-color 0.2s;
      -moz-appearance: textfield;
    }
    .income-input::-webkit-outer-spin-button,
    .income-input::-webkit-inner-spin-button { -webkit-appearance: none; }
    .income-input:focus { outline: none; border-color: var(--gold); }
    .income-skip { display: block; text-align: center; margin-top: 12px; font-size: 0.8rem; color: var(--text-muted); cursor: pointer; text-decoration: underline; }
    .income-skip:hover { color: var(--text-dim); }
    /* ── Footer ── */
    footer {
      text-align: center; padding: 40px 20px 20px;
      font-size: 0.75rem; color: var(--text-muted);
      border-top: 1px solid var(--border);
    }
    footer a { color: var(--text-muted); }
    /* ── Animations ── */
    @keyframes barFill {
      from { width: 0; }
    }
    .bar-animate { animation: barFill 1s ease forwards; }
    /* Responsive */
    @media (max-width: 500px) {
      .options-grid { grid-template-columns: 1fr 1fr; }
      .city-grid { grid-template-columns: repeat(3, 1fr); }
    }
  </style>
</head>
<body>
<div class="bg-orbs">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>
</div>
<div id="app">
  <header>
    <div class="badge">✦ The Soft Life Calculator</div>
    <h1>What does your<br/>dream life actually cost?</h1>
    <p class="subtitle">Design your ideal lifestyle — city, home, travel, and more — and get your real number in 60 seconds.</p>
  </header>
  <!-- Progress -->
  <div class="progress-wrap" id="progress-wrap" style="display:none;">
    <div class="progress-track">
      <div class="progress-fill" id="progress-fill" style="width:0%"></div>
    </div>
    <div class="progress-label" id="progress-label">1 / 7</div>
  </div>
  <!-- ════ STEP 0: Start ════ -->
  <div class="step active" id="step-0">
    <div style="text-align:center; padding: 20px 0 40px;">
      <div style="font-size: 3rem; margin-bottom: 20px;">✨</div>
      <p style="color: var(--text-dim); max-width: 400px; margin: 0 auto 32px; font-size: 0.95rem; line-height: 1.6;">
        Most people have a vague idea of the life they want. This tool makes the number concrete — no fantasy, no fluff.
      </p>
      <button class="btn btn-primary" onclick="nextStep()" style="font-size: 1rem; padding: 16px 40px;">
        Calculate My Number →
      </button>
      <p style="margin-top: 16px; font-size: 0.75rem; color: var(--text-muted);">Takes about 60 seconds · No sign-up required</p>
    </div>
  </div>
  <!-- ════ STEP 1: City ════ -->
  <div class="step" id="step-1">
    <div class="step-header">
      <span class="step-icon">🏙️</span>
      <div class="step-title">Where do you want to live?</div>
      <div class="step-desc">Your city is the single biggest factor in your Soft Life Number.</div>
    </div>
    <div class="city-grid" id="city-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-1">—</span>/mo</div>
      <button class="btn btn-primary" id="next-1" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 2: Home ════ -->
  <div class="step" id="step-2">
    <div class="step-header">
      <span class="step-icon">🏠</span>
      <div class="step-title">Your home situation</div>
      <div class="step-desc">Rent in your chosen city, averaged across neighborhoods.</div>
    </div>
    <div class="options-grid" id="home-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-2">—</span>/mo</div>
      <button class="btn btn-primary" id="next-2" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 3: Transport ════ -->
  <div class="step" id="step-3">
    <div class="step-header">
      <span class="step-icon">🚗</span>
      <div class="step-title">Getting around</div>
      <div class="step-desc">Car payment, insurance, gas, parking — all included.</div>
    </div>
    <div class="options-grid" id="car-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-3">—</span>/mo</div>
      <button class="btn btn-primary" id="next-3" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 4: Food ════ -->
  <div class="step" id="step-4">
    <div class="step-header">
      <span class="step-icon">🍽️</span>
      <div class="step-title">Eating & drinking</div>
      <div class="step-desc">Groceries, restaurants, coffee, bars — your total food spend.</div>
    </div>
    <div class="options-grid" id="food-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-4">—</span>/mo</div>
      <button class="btn btn-primary" id="next-4" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 5: Travel ════ -->
  <div class="step" id="step-5">
    <div class="step-header">
      <span class="step-icon">✈️</span>
      <div class="step-title">How you explore the world</div>
      <div class="step-desc">Annual travel budget divided into a monthly cost.</div>
    </div>
    <div class="options-grid" id="travel-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-5">—</span>/mo</div>
      <button class="btn btn-primary" id="next-5" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 6: Lifestyle ════ -->
  <div class="step" id="step-6">
    <div class="step-header">
      <span class="step-icon">💅</span>
      <div class="step-title">Your lifestyle & extras</div>
      <div class="step-desc">Fashion, fitness, self-care, entertainment — how you actually live.</div>
    </div>
    <div class="options-grid" id="lifestyle-grid"></div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div class="running-total">Total so far: <span id="rt-6">—</span>/mo</div>
      <button class="btn btn-primary" id="next-6" onclick="nextStep()" disabled>Next →</button>
    </div>
  </div>
  <!-- ════ STEP 7: Current Income ════ -->
  <div class="step" id="step-7">
    <div class="step-header">
      <span class="step-icon">💰</span>
      <div class="step-title">What do you currently earn?</div>
      <div class="step-desc">Optional — we'll calculate the gap between where you are and where you want to be.</div>
    </div>
    <div class="income-wrap">
      <div class="income-label">Your current monthly take-home income (after tax)</div>
      <div class="income-input-row">
        <span class="currency-sign">$</span>
        <input type="number" class="income-input" id="income-input" placeholder="0" min="0" max="999999" />
      </div>
      <span class="income-skip" onclick="skipIncome()">Skip — just show me my number</span>
    </div>
    <div class="info-note">We never store or transmit your income. Everything stays in your browser.</div>
    <div class="nav-row">
      <button class="btn btn-ghost" onclick="prevStep()">← Back</button>
      <div></div>
      <button class="btn btn-primary" onclick="showResult()" style="background: linear-gradient(135deg, #7c5cbf, #c9a84c);">
        Reveal My Number 🔮
      </button>
    </div>
  </div>
  <!-- ════ RESULT ════ -->
  <div id="step-result">
    <div class="result-hero">
      <div class="result-label">Your Soft Life Number</div>
      <div class="result-number" id="result-number">$0</div>
      <div class="result-per">per month after tax</div>
      <div class="result-context" id="result-context"></div>
    </div>
    <div class="breakdown" id="breakdown">
      <div class="breakdown-header">
        <span>Your Breakdown</span>
        <span>Monthly</span>
      </div>
      <div id="breakdown-rows"></div>
    </div>
    <div class="gap-card" id="gap-card"></div>
    <div class="affiliate-section">
      <div class="affiliate-heading">Ready to actually build toward this?</div>
      <div class="affiliate-sub">The gap between your current life and your soft life isn't luck — it's planning. These tools give you an unfair advantage.</div>
      <div class="affiliate-cards">
        <a class="affiliate-card" href="https://monarch.com/referral/xo5trh36x1?r_source=copy" target="_blank" rel="noopener">
          <div class="aff-name">👑 Monarch Money</div>
          <div class="aff-desc">The best budgeting app for people who are serious about closing the gap. Net worth tracking, custom goals, real-time sync.</div>
          <div class="aff-cta">Start free trial →</div>
        </a>
        <a class="affiliate-card" href="https://www.copilot.money" target="_blank" rel="noopener">
          <div class="aff-name">✈️ Copilot Money</div>
          <div class="aff-desc">Beautiful, intelligent money tracking that actually makes sense of where your money goes — and where it should go.</div>
          <div class="aff-cta">Get the app →</div>
        </a>
      </div>
    </div>
    <div class="share-section">
      <div class="share-label">Share your Soft Life Number</div>
      <div class="share-btns">
        <button class="share-btn" onclick="shareTwitter()">🐦 Post on X</button>
        <button class="share-btn" onclick="copyLink(this)">🔗 Copy link</button>
      </div>
    </div>
    <button class="restart-btn" onclick="restart()">↺ Recalculate</button>
  </div>
</div>
<footer>
  <p>Soft Life Calculator · Estimates are based on national average data from BLS, Census Bureau, and Zillow Research.</p>
  <p style="margin-top:6px;">Not financial advice. <a href="#">Privacy</a> · <a href="#">About</a></p>
</footer>
<script>
  // ════ DATA ════
  const CITIES = [
    { id:'nyc',    emoji:'🗽', name:'New York City',   vibe:'Maximum hustle',      mult: 1.0,  rent: { shared:1200, studio:2600, onebr:3600, luxury:12000 } },
    { id:'la',     emoji:'🌴', name:'Los Angeles',     vibe:'Sunshine & chaos',    mult: 0.92, rent: { shared:1000, studio:2100, onebr:2900, luxury:10000 } },
    { id:'sf',     emoji:'🌉', name:'San Francisco',   vibe:'Tech & fog',          mult: 0.98, rent: { shared:1400, studio:2500, onebr:3300, luxury:11000 } },
    { id:'miami',  emoji:'🌊', name:'Miami',           vibe:'Sun, vibes, money',   mult: 0.82, rent: { shared:900,  studio:1900, onebr:2500, luxury:9000  } },
    { id:'chi',    emoji:'🌬️', name:'Chicago',         vibe:'Underrated gem',      mult: 0.72, rent: { shared:800,  studio:1500, onebr:2000, luxury:7000  } },
    { id:'atx',    emoji:'🤠', name:'Austin',          vibe:'Weird & growing',     mult: 0.75, rent: { shared:800,  studio:1600, onebr:2100, luxury:6500  } },
    { id:'sea',    emoji:'☕', name:'Seattle',         vibe:'Rain & tech money',   mult: 0.85, rent: { shared:1000, studio:1900, onebr:2500, luxury:8000  } },
    { id:'dc',     emoji:'🏛️', name:'Washington DC',   vibe:'Power & politics',    mult: 0.88, rent: { shared:1100, studio:2100, onebr:2800, luxury:9500  } },
    { id:'den',    emoji:'🏔️', name:'Denver',          vibe:'Outdoors & chill',    mult: 0.72, rent: { shared:750,  studio:1600, onebr:2100, luxury:6500  } },
    { id:'remote', emoji:'🏡', name:'Remote / Anywhere', vibe:'Location freedom', mult: 0.55, rent: { shared:500,  studio:900,  onebr:1200, luxury:3500  } },
  ];
  const HOME_OPTIONS = [
    { id:'shared',  emoji:'🛋️', name:'Shared apartment', note:'Roommates, split bills', priceKey:'shared' },
    { id:'studio',  emoji:'🏠', name:'Your own studio',  note:'Private, cozy, yours',   priceKey:'studio' },
    { id:'onebr',   emoji:'🛏️', name:'1-bed apartment',  note:'Space + a guest room',   priceKey:'onebr' },
    { id:'luxury',  emoji:'🏙️', name:'Luxury or penthouse', note:'Top floor energy',   priceKey:'luxury' },
  ];
  const CAR_OPTIONS = [
    { id:'none',    emoji:'🚶', name:'No car / transit',   price: 150,  note:'Monthly pass + Uber' },
    { id:'budget',  emoji:'🚙', name:'Budget used car',    price: 550,  note:'Payment + ins + gas' },
    { id:'mid',     emoji:'🚘', name:'Mid-range (Honda/Toyota)', price: 900, note:'Reliable & solid' },
    { id:'luxury',  emoji:'🚗', name:'Luxury (BMW / Mercedes)', price: 1800, note:'Payment + premium ins' },
    { id:'exotic',  emoji:'🏎️', name:'Exotic / supercar', price: 4500, note:'The full flex' },
  ];
  const FOOD_OPTIONS = [
    { id:'homecook', emoji:'🥗', name:'Mostly home cooked', price: 400,  note:'Groceries + occasional out' },
    { id:'balance',  emoji:'🍜', name:'Balance of both',    price: 850,  note:'Restaurants 3–4x/week' },
    { id:'eatingout',emoji:'🍣', name:'Restaurant regular', price: 1600, note:'Dining out most nights' },
    { id:'finedine', emoji:'🥂', name:'Fine dining & bars', price: 3000, note:'Omakase-level life' },
  ];
  const TRAVEL_OPTIONS = [
    { id:'rare',     emoji:'🌍', name:'Once a year or less', price: 150,  note:'~$1,800/yr budget' },
    { id:'moderate', emoji:'✈️', name:'2–3 trips/year',      price: 400,  note:'Economy, mix of trips' },
    { id:'frequent', emoji:'🏝️', name:'4–6 trips/year',     price: 1000, note:'Business class sometimes' },
    { id:'jetset',   emoji:'🛩️', name:'Frequent flyer life', price: 3000, note:'Business class + hotels' },
  ];
  const LIFESTYLE_OPTIONS = [
    { id:'basic',    emoji:'😌', name:'Low-key',        price: 350,  note:'Basic gym, streaming, chill' },
    { id:'moderate', emoji:'🎯', name:'Comfortable',    price: 900,  note:'Nice gym, events, some fashion' },
    { id:'elevated', emoji:'💎', name:'Elevated',       price: 2000, note:'Equinox, designer, spa days' },
    { id:'luxury',   emoji:'👑', name:'Full luxury',    price: 4500, note:'Personal trainer, VIP, designer' },
  ];
  // ════ STATE ════
  let currentStep = 0;
  const totalSteps = 7;
  const selections = {
    city: null, home: null, car: null,
    food: null, travel: null, lifestyle: null,
    income: null
  };
  // ════ INIT ════
  function init() {
    buildCityGrid();
    buildOptionGrid('home-grid', HOME_OPTIONS, 'home', 'next-2', 'rt-2', computeHomePrice);
    buildCarGrid();
    buildSimpleGrid('food-grid', FOOD_OPTIONS, 'food', 'next-4', 'rt-4');
    buildSimpleGrid('travel-grid', TRAVEL_OPTIONS, 'travel', 'next-5', 'rt-5');
    buildSimpleGrid('lifestyle-grid', LIFESTYLE_OPTIONS, 'lifestyle', 'next-6', 'rt-6');
  }
  function buildCityGrid() {
    const grid = document.getElementById('city-grid');
    CITIES.forEach(city => {
      const card = document.createElement('div');
      card.className = 'city-card';
      card.innerHTML = `
        <div class="check-badge">✓</div>
        <span class="city-emoji">${city.emoji}</span>
        <div class="city-name">${city.name}</div>
        <div class="city-vibe">${city.vibe}</div>
      `;
      card.addEventListener('click', () => {
        document.querySelectorAll('.city-card').forEach(c => c.classList.remove('selected'));
        card.classList.add('selected');
        selections.city = city;
        document.getElementById('next-1').disabled = false;
        updateRunningTotal('rt-1');
        // update home prices
        updateHomePrices();
      });
      grid.appendChild(card);
    });
  }
  function updateHomePrices() {
    const city = selections.city;
    if (!city) return;
    const cards = document.querySelectorAll('#home-grid .option-card');
    HOME_OPTIONS.forEach((opt, i) => {
      const price = city.rent[opt.priceKey];
      cards[i].querySelector('.option-price').textContent = `$${price.toLocaleString()}/mo`;
    });
  }
  function computeHomePrice(opt) {
    const city = selections.city;
    if (!city) return 0;
    return city.rent[opt.priceKey];
  }
  function buildOptionGrid(gridId, options, key, nextId, rtId, priceFn) {
    const grid = document.getElementById(gridId);
    options.forEach(opt => {
      const price = priceFn ? priceFn(opt) : opt.price;
      const card = document.createElement('div');
      card.className = 'option-card';
      card.dataset.key = key;
      card.dataset.id = opt.id;
      card.innerHTML = `
        <div class="check-badge">✓</div>
        <span class="option-emoji">${opt.emoji}</span>
        <div class="option-name">${opt.name}</div>
        <div class="option-price">${price > 0 ? '$' + price.toLocaleString() + '/mo' : 'Free'}</div>
        <div class="option-note">${opt.note}</div>
      `;
      card.addEventListener('click', () => {
        document.querySelectorAll(`[data-key="${key}"]`).forEach(c => c.classList.remove('selected'));
        card.classList.add('selected');
        selections[key] = opt;
        document.getElementById(nextId).disabled = false;
        updateRunningTotal(rtId);
      });
      grid.appendChild(card);
    });
  }
  function buildCarGrid() {
    const grid = document.getElementById('car-grid');
    CAR_OPTIONS.forEach(opt => {
      const card = document.createElement('div');
      card.className = 'option-card';
      card.dataset.key = 'car';
      card.dataset.id = opt.id;
      card.innerHTML = `
        <div class="check-badge">✓</div>
        <span class="option-emoji">${opt.emoji}</span>
        <div class="option-name">${opt.name}</div>
        <div class="option-price">$${opt.price.toLocaleString()}/mo</div>
        <div class="option-note">${opt.note}</div>
      `;
      card.addEventListener('click', () => {
        document.querySelectorAll('[data-key="car"]').forEach(c => c.classList.remove('selected'));
        card.classList.add('selected');
        selections.car = opt;
        document.getElementById('next-3').disabled = false;
        updateRunningTotal('rt-3');
      });
      grid.appendChild(card);
    });
  }
  function buildSimpleGrid(gridId, options, key, nextId, rtId) {
    const grid = document.getElementById(gridId);
    options.forEach(opt => {
      const card = document.createElement('div');
      card.className = 'option-card';
      card.dataset.key = key;
      card.dataset.id = opt.id;
      card.innerHTML = `
        <div class="check-badge">✓</div>
        <span class="option-emoji">${opt.emoji}</span>
        <div class="option-name">${opt.name}</div>
        <div class="option-price">$${opt.price.toLocaleString()}/mo</div>
        <div class="option-note">${opt.note}</div>
      `;
      card.addEventListener('click', () => {
        document.querySelectorAll(`[data-key="${key}"]`).forEach(c => c.classList.remove('selected'));
        card.classList.add('selected');
        selections[key] = opt;
        document.getElementById(nextId).disabled = false;
        updateRunningTotal(rtId);
      });
      grid.appendChild(card);
    });
  }
  // ════ CALCULATIONS ════
  function getTotalMonthly() {
    let total = 0;
    if (selections.home && selections.city) total += selections.city.rent[selections.home.priceKey];
    if (selections.car)       total += selections.car.price;
    if (selections.food)      total += selections.food.price;
    if (selections.travel)    total += selections.travel.price;
    if (selections.lifestyle) total += selections.lifestyle.price;
    // Add misc buffer: utilities, subscriptions, health, personal care
    if (selections.city) {
      const base = total;
      const misc = Math.round(base * 0.12 + 200); // 12% buffer + $200 base for subs/utilities
      total += misc;
    }
    return total;
  }
  function getGrossNeeded(monthly) {
    // Assume ~28% effective tax rate for higher earners, ~22% for moderate
    const rate = monthly > 8000 ? 0.30 : 0.24;
    return Math.round(monthly / (1 - rate));
  }
  function updateRunningTotal(rtId) {
    const el = document.getElementById(rtId);
    if (!el) return;
    const t = getTotalMonthly();
    el.textContent = t > 0 ? '$' + t.toLocaleString() : '—';
  }
  // ════ NAVIGATION ════
  function nextStep() {
    document.getElementById(currentStep === 0 ? 'step-0' : `step-${currentStep}`).classList.remove('active');
    currentStep++;
    if (currentStep <= totalSteps) {
      document.getElementById(`step-${currentStep}`).classList.add('active');
    }
    updateProgress();
    // Rebuild home prices after city selected
    if (currentStep === 2) updateHomePrices();
  }
  function prevStep() {
    document.getElementById(`step-${currentStep}`).classList.remove('active');
    currentStep--;
    document.getElementById(currentStep === 0 ? 'step-0' : `step-${currentStep}`).classList.add('active');
    updateProgress();
  }
  function updateProgress() {
    const wrap = document.getElementById('progress-wrap');
    if (currentStep === 0) { wrap.style.display = 'none'; return; }
    wrap.style.display = 'flex';
    const pct = ((currentStep - 1) / totalSteps) * 100;
    document.getElementById('progress-fill').style.width = pct + '%';
    document.getElementById('progress-label').textContent = `${currentStep} / ${totalSteps}`;
  }
  function skipIncome() {
    selections.income = null;
    showResult();
  }
  // ════ RESULT ════
  function showResult() {
    const incomeEl = document.getElementById('income-input');
    if (incomeEl.value) selections.income = parseInt(incomeEl.value);
    document.getElementById(`step-${currentStep}`).classList.remove('active');
    document.getElementById('progress-wrap').style.display = 'none';
    const monthly = getTotalMonthly();
    const annual = monthly * 12;
    const grossNeeded = getGrossNeeded(monthly);
    const medianUS = 4600; // ~$55k/yr median US household take-home
    // Animate number
    const numEl = document.getElementById('result-number');
    animateNumber(numEl, 0, monthly, 1200);
    // Context chips
    const ctx = document.getElementById('result-context');
    const multVsMedian = (monthly / medianUS).toFixed(1);
    ctx.innerHTML = `
      <div class="context-chip"><strong>$${annual.toLocaleString()}</strong> per year</div>
      <div class="context-chip"><strong>$${grossNeeded.toLocaleString()}</strong> gross salary needed</div>
      <div class="context-chip"><strong>${multVsMedian}×</strong> the US median income</div>
    `;
    // Breakdown rows
    const rows = document.getElementById('breakdown-rows');
    const breakdownData = [
      { icon: '🏠', name: 'Housing', label: selections.home?.name || '—', val: selections.city ? selections.city.rent[selections.home?.priceKey || 'studio'] : 0 },
      { icon: '🚗', name: 'Transport', label: selections.car?.name || '—', val: selections.car?.price || 0 },
      { icon: '🍽️', name: 'Food & drink', label: selections.food?.name || '—', val: selections.food?.price || 0 },
      { icon: '✈️', name: 'Travel', label: selections.travel?.name || '—', val: selections.travel?.price || 0 },
      { icon: '💅', name: 'Lifestyle', label: selections.lifestyle?.name || '—', val: selections.lifestyle?.price || 0 },
      { icon: '📱', name: 'Subscriptions & misc', label: 'Utilities, streaming, health', val: Math.round(getTotalMonthly() * 0.10 + 200) },
    ];
    rows.innerHTML = breakdownData.map(r => `
      <div class="breakdown-row">
        <div>
          <div class="breakdown-cat">
            <span class="breakdown-icon">${r.icon}</span>
            <span>${r.name}</span>
          </div>
          <div class="breakdown-label">${r.label}</div>
        </div>
        <div class="breakdown-val">$${r.val.toLocaleString()}</div>
      </div>
    `).join('');
    // Gap card
    const gap = document.getElementById('gap-card');
    if (selections.income) {
      const diff = monthly - selections.income;
      if (diff > 0) {
        gap.innerHTML = `
          <div class="gap-title">Your Gap</div>
          <div class="gap-number" style="color: var(--red)">$${diff.toLocaleString()}/mo</div>
          <div class="gap-desc">You're currently <strong>$${diff.toLocaleString()}/month</strong> away from your soft life — 
          that's <strong>$${(diff*12).toLocaleString()}/year</strong>. The good news: most people close this gap incrementally. 
          Start tracking, start planning.</div>
        `;
      } else {
        gap.innerHTML = `
          <div class="gap-title">You're already there 👑</div>
          <div class="gap-number" style="color: var(--green)">+$${Math.abs(diff).toLocaleString()}/mo</div>
          <div class="gap-desc">Your current income already covers your soft life — you have <strong>$${Math.abs(diff).toLocaleString()}/month</strong> to spare. 
          Time to grow your wealth intentionally.</div>
        `;
      }
    } else {
      gap.innerHTML = `
        <div class="gap-title">To live this life, you need</div>
        <div class="gap-number">$${grossNeeded.toLocaleString()}/yr</div>
        <div class="gap-desc">That's approximately <strong>$${grossNeeded.toLocaleString()}/year</strong> in gross income — 
        or roughly <strong>${(grossNeeded/1000).toFixed(0)}k before taxes</strong>. 
        Not impossible. Not automatic. Plan accordingly.</div>
      `;
    }
    document.getElementById('step-result').classList.add('active');
    document.getElementById('step-result').style.display = 'block';
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
  function animateNumber(el, from, to, duration) {
    const start = performance.now();
    function step(now) {
      const elapsed = now - start;
      const progress = Math.min(elapsed / duration, 1);
      const eased = 1 - Math.pow(1 - progress, 3);
      const val = Math.round(from + (to - from) * eased);
      el.textContent = '$' + val.toLocaleString();
      if (progress < 1) requestAnimationFrame(step);
    }
    requestAnimationFrame(step);
  }
  // ════ SHARE ════
  function shareTwitter() {
    const monthly = getTotalMonthly();
    const text = `My Soft Life Number is $${monthly.toLocaleString()}/month 😳 What's yours?\n\nsoftlifecalc.com`;
    window.open(`https://twitter.com/intent/tweet?text=${encodeURIComponent(text)}`, '_blank');
  }
  function copyLink(btn) {
    navigator.clipboard.writeText(window.location.href).then(() => {
      btn.classList.add('copied');
      btn.textContent = '✓ Copied!';
      setTimeout(() => {
        btn.classList.remove('copied');
        btn.innerHTML = '🔗 Copy link';
      }, 2000);
    });
  }
  function restart() {
    // Reset
    Object.keys(selections).forEach(k => selections[k] = null);
    document.querySelectorAll('.option-card, .city-card').forEach(c => c.classList.remove('selected'));
    document.querySelectorAll('.btn-primary[id^="next"]').forEach(b => b.disabled = true);
    document.getElementById('income-input').value = '';
    currentStep = 0;
    document.getElementById('step-result').style.display = 'none';
    document.getElementById('step-result').classList.remove('active');
    document.getElementById('step-0').classList.add('active');
    document.getElementById('progress-wrap').style.display = 'none';
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
  // ════ START ════
  init();
</script>
</body>
</html>
