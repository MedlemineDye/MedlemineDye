<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MedLemine – Programmeur scientifique</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@500;700;800&family=IBM+Plex+Sans:wght@400;500&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --paper: #f3f6f8;
    --grid: #d9e2ea;
    --ink: #14243b;
    --muted: #4d5f78;
    --blue: #2457c5;
    --mint: #1f8a70;
    --card: #ffffff;
    --line: #c3d0dc;
    --display: "Bricolage Grotesque", "Trebuchet MS", system-ui, sans-serif;
    --body: "IBM Plex Sans", system-ui, -apple-system, "Segoe UI", sans-serif;
    --mono: "IBM Plex Mono", ui-monospace, Consolas, monospace;
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --paper: #0f1a2b;
      --grid: #1b2a40;
      --ink: #e8eef7;
      --muted: #9db0c9;
      --blue: #7ba4ff;
      --mint: #5fd0b0;
      --card: #14233a;
      --line: #2b405c;
    }
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0;
    background-color: var(--paper);
    background-image:
      linear-gradient(var(--grid) 1px, transparent 1px),
      linear-gradient(90deg, var(--grid) 1px, transparent 1px);
    background-size: 32px 32px;
    color: var(--ink);
    font-family: var(--body);
    font-size: 17px;
    line-height: 1.6;
  }
  a { color: var(--blue); }
  :focus-visible { outline: 3px solid var(--blue); outline-offset: 3px; border-radius: 4px; }
  .wrap { max-width: 1040px; margin: 0 auto; padding: 0 24px; }

  header.top { padding: 20px 0; }
  header.top .wrap { display: flex; justify-content: space-between; align-items: center; gap: 16px; flex-wrap: wrap; }
  .logo { font-family: var(--display); font-weight: 800; font-size: 1.15rem; letter-spacing: -0.01em; }
  nav a { margin-left: 20px; color: var(--ink); text-decoration: none; font-weight: 500; font-size: 0.95rem; }
  nav a:hover { color: var(--blue); }

  .hero { padding: 56px 0 72px; }
  .hero-grid { display: grid; grid-template-columns: 1.05fr 1fr; gap: 48px; align-items: start; }
  h1 {
    font-family: var(--display);
    font-weight: 800;
    font-size: clamp(2.6rem, 6vw, 4.6rem);
    line-height: 1;
    letter-spacing: -0.03em;
    margin: 0 0 24px;
  }
  .lead { font-size: 1.15rem; color: var(--muted); max-width: 34em; margin: 0 0 28px; }
  .tags { display: flex; flex-wrap: wrap; gap: 8px; padding: 0; margin: 0 0 28px; list-style: none; }
  .tags li { border: 1.5px solid var(--ink); border-radius: 999px; padding: 4px 14px; font-size: 0.9rem; font-weight: 500; background: var(--card); }
  .btn {
    display: inline-block; background: var(--ink); color: var(--paper);
    padding: 12px 22px; border-radius: 8px; text-decoration: none; font-weight: 500;
  }
  .btn:hover { background: var(--blue); color: #fff; }

  /* Calculateur */
  .calc { background: var(--card); border: 2px solid var(--ink); border-radius: 14px; padding: 24px; box-shadow: 6px 6px 0 var(--blue); }
  .calc h2 { font-family: var(--display); font-size: 1.25rem; margin: 0 0 4px; }
  .calc p.sub { margin: 0 0 18px; color: var(--muted); font-size: 0.92rem; }
  .fields { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .field label { display: block; font-size: 0.88rem; color: var(--muted); margin-bottom: 4px; }
  .field input {
    width: 100%; padding: 9px 10px; font: 500 1rem var(--mono);
    border: 1.5px solid var(--line); border-radius: 8px; background: var(--paper); color: var(--ink);
  }
  .result { margin-top: 20px; padding-top: 16px; border-top: 1.5px dashed var(--line); }
  .result .big { font-family: var(--display); font-weight: 800; font-size: 2.2rem; color: var(--mint); line-height: 1.1; }
  .result .small { font-size: 0.92rem; color: var(--muted); }
  svg.chart { width: 100%; height: auto; margin-top: 12px; display: block; }
  .legend { display: flex; gap: 18px; font-size: 0.85rem; color: var(--muted); margin-top: 6px; }
  .legend span::before { content: ""; display: inline-block; width: 14px; height: 3px; margin-right: 6px; vertical-align: middle; }
  .legend .l1::before { background: var(--mint); }
  .legend .l2::before { background: var(--muted); }
  .formula { font-family: var(--mono); font-size: 0.82rem; background: var(--paper); border: 1px solid var(--line); border-radius: 8px; padding: 8px 10px; margin-top: 14px; overflow-x: auto; }

  section.block { padding: 56px 0; }
  section.block.solid { background: var(--card); border-top: 2px solid var(--ink); border-bottom: 2px solid var(--ink); }
  h2.title { font-family: var(--display); font-size: clamp(1.7rem, 3.5vw, 2.4rem); letter-spacing: -0.02em; margin: 0 0 8px; }
  p.intro { color: var(--muted); max-width: 40em; margin: 0 0 32px; }

  .maths { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 0; border: 2px solid var(--ink); border-radius: 12px; overflow: hidden; background: var(--paper); }
  .maths div { padding: 20px 22px; border-right: 1.5px solid var(--line); border-bottom: 1.5px solid var(--line); margin: -0.75px; }
  .maths h3 { font-family: var(--display); font-size: 1.1rem; margin: 0 0 4px; }
  .maths p { margin: 0; color: var(--muted); font-size: 0.95rem; }
  .maths code { font-family: var(--mono); font-size: 0.85rem; color: var(--blue); }

  .stack { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 28px; }
  .stack h3 { font-family: var(--display); font-size: 1.05rem; margin: 0 0 10px; }
  .stack ul { list-style: none; padding: 0; margin: 0; display: flex; flex-wrap: wrap; gap: 8px; }
  .stack li { font-family: var(--mono); font-size: 0.85rem; padding: 3px 10px; border: 1.5px solid var(--line); border-radius: 6px; background: var(--card); }

  pre {
    background: #101c30; color: #dce7f7; border-radius: 12px; padding: 22px;
    overflow-x: auto; font: 400 0.88rem/1.65 var(--mono); margin: 0;
  }
  pre .k { color: #8db4ff; } pre .s { color: #8fe0c2; } pre .c { color: #7f93b3; }

  .projects { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
  .project { background: var(--card); border: 2px solid var(--ink); border-radius: 12px; padding: 20px; }
  .project h3 { font-family: var(--display); margin: 0 0 6px; font-size: 1.1rem; }
  .project p { margin: 0 0 10px; color: var(--muted); font-size: 0.95rem; }
  .project .meta { font-family: var(--mono); font-size: 0.8rem; color: var(--blue); }

  footer { padding: 48px 0 56px; }
  footer .wrap { display: flex; justify-content: space-between; gap: 20px; flex-wrap: wrap; align-items: end; }
  footer p { margin: 0; color: var(--muted); }
  .contact a { margin-right: 18px; font-weight: 500; }

  @media (max-width: 860px) {
    .hero-grid { grid-template-columns: 1fr; }
    nav a:first-child { margin-left: 0; }
  }
  @media (prefers-reduced-motion: reduce) { html { scroll-behavior: auto; } }
</style>
</head>
<body>

<header class="top">
  <div class="wrap">
    <div class="logo">VOTRE_NOM</div>
    <nav aria-label="Navigation principale">
      <a href="#maths">Maths du quotidien</a>
      <a href="#outils">Outils</a>
      <a href="#projets">Projets</a>
      <a href="#contact">Contact</a>
    </nav>
  </div>
</header>

<main>
  <section class="hero">
    <div class="wrap hero-grid">
      <div>
        <h1>Je programme pour calculer le réel.</h1>
        <p class="lead">Programmeur scientifique, je transforme les mathématiques en outils concrets : budget, probabilités, optimisation, mesures. Essayez le calculateur d’épargne ci-contre, c’est le genre de problème que j’aime résoudre.</p>
        <ul class="tags">
          <li>Calcul scientifique</li>
          <li>Simulation numérique</li>
          <li>Statistiques</li>
          <li>Maths pratiques</li>
        </ul>
        <a class="btn" href="#projets">Voir mes projets</a>
      </div>

      <div class="calc">
        <h2>Combien vaudra mon épargne ?</h2>
        <p class="sub">Intérêts composés avec versements mensuels.</p>
        <div class="fields">
          <div class="field"><label for="capital">Capital de départ (€)</label><input id="capital" type="number" value="1000" min="0" step="100"></div>
          <div class="field"><label for="versement">Versement par mois (€)</label><input id="versement" type="number" value="100" min="0" step="10"></div>
          <div class="field"><label for="taux">Taux annuel (%)</label><input id="taux" type="number" value="4" min="0" max="30" step="0.1"></div>
          <div class="field"><label for="annees">Durée (années)</label><input id="annees" type="number" value="10" min="1" max="50" step="1"></div>
        </div>
        <div class="result" aria-live="polite">
          <div class="big" id="total">–</div>
          <div class="small" id="detail">–</div>
          <svg class="chart" id="chart" viewBox="0 0 400 150" role="img" aria-label="Évolution du capital dans le temps"></svg>
          <div class="legend"><span class="l1">Capital avec intérêts</span><span class="l2">Somme versée</span></div>
        </div>
        <div class="formula">V = C·(1 + r/12)^(12t) + P·((1 + r/12)^(12t) − 1) / (r/12)</div>
      </div>
    </div>
  </section>

  <section class="block solid" id="maths">
    <div class="wrap">
      <h2 class="title">Les maths dans ma vie quotidienne</h2>
      <p class="intro">Chaque situation ordinaire cache un outil mathématique. Voici ceux que j’utilise le plus.</p>
      <div class="maths">
        <div><h3>Comparer des offres</h3><p>Pourcentages et proportionnalité. Un rabais de 30 % puis 10 % ne fait pas 40 % : <code>0,7 × 0,9 = 0,63</code>.</p></div>
        <div><h3>Épargner et emprunter</h3><p>Suites géométriques et intérêts composés, comme dans le calculateur.</p></div>
        <div><h3>Estimer un risque</h3><p>Probabilités et espérance pour décider quand le résultat est incertain.</p></div>
        <div><h3>Suivre mes dépenses</h3><p>Moyenne, écart-type et régression pour repérer les tendances d’un budget.</p></div>
        <div><h3>Optimiser</h3><p>Trajets, temps, ressources : minimiser ce qui coûte, maximiser ce qui compte.</p></div>
        <div><h3>Cuisiner pour N personnes</h3><p>La règle de trois, utilisée presque chaque semaine.</p></div>
      </div>
    </div>
  </section>

  <section class="block" id="outils">
    <div class="wrap">
      <h2 class="title">Mes outils</h2>
      <p class="intro">Une boîte à outils orientée calcul, données et visualisation.</p>
      <div class="stack">
        <div><h3>Langages</h3><ul><li>Python</li><li>Julia</li><li>C++</li><li>R</li><li>Bash</li><li>JavaScript</li></ul></div>
        <div><h3>Science des données</h3><ul><li>NumPy</li><li>SciPy</li><li>Pandas</li><li>Matplotlib</li><li>scikit-learn</li><li>Jupyter</li></ul></div>
        <div><h3>Environnement</h3><ul><li>GNU/Linux</li><li>Git</li><li>VS Code</li><li>LaTeX</li><li>SQLite</li></ul></div>
      </div>
    </div>
  </section>

  <section class="block solid">
    <div class="wrap">
      <h2 class="title">Mon style de code</h2>
      <p class="intro">Court, documenté, utile au quotidien.</p>
<pre><span class="k">import</span> numpy <span class="k">as</span> np

<span class="k">def</span> valeur_future(capital, taux, annees, n=12):
    <span class="s">"""Épargne avec intérêts composés."""</span>
    <span class="k">return</span> capital * (1 + taux / n) ** (n * annees)

<span class="c"># 1000 € à 5 % pendant 10 ans</span>
<span class="k">print</span>(<span class="s">f"{valeur_future(1000, 0.05, 10):.2f} €"</span>)</pre>
    </div>
  </section>

  <section class="block" id="projets">
    <div class="wrap">
      <h2 class="title">Projets</h2>
      <p class="intro">Remplacez ces exemples par vos propres dépôts.</p>
      <div class="projects">
        <div class="project"><h3>Simulateur d’épargne</h3><p>Calcule l’évolution d’un capital avec intérêts composés et versements réguliers.</p><span class="meta">Python · NumPy</span></div>
        <div class="project"><h3>Analyseur de budget</h3><p>Importe des dépenses et en tire moyennes, tendances et prévisions.</p><span class="meta">Pandas · Matplotlib</span></div>
        <div class="project"><h3>Jeux de probabilités</h3><p>Simulations Monte-Carlo pour comprendre le hasard par l’expérience.</p><span class="meta">Julia · Jupyter</span></div>
      </div>
    </div>
  </section>
</main>

<footer id="contact">
  <div class="wrap">
    <div>
      <h2 class="title">Me contacter</h2>
      <p class="contact">
        <a href="mailto:votre.adresse@exemple.com">Courriel</a>
        <a href="https://github.com/VOTRE_NOM_UTILISATEUR">GitHub</a>
        <a href="https://linkedin.com/in/VOTRE_PROFIL">LinkedIn</a>
      </p>
    </div>
    <p>Calculer, comprendre, créer.</p>
  </div>
</footer>

<script>
  const $ = id => document.getElementById(id);
  const eur = new Intl.NumberFormat("fr-FR", { style: "currency", currency: "EUR", maximumFractionDigits: 0 });

  function balanceAt(C, P, rate, months) {
    const i = rate / 12;
    if (i === 0) return C + P * months;
    const g = Math.pow(1 + i, months);
    return C * g + P * (g - 1) / i;
  }

  function update() {
    const C = Math.max(0, parseFloat($("capital").value) || 0);
    const P = Math.max(0, parseFloat($("versement").value) || 0);
    const rate = Math.max(0, (parseFloat($("taux").value) || 0) / 100);
    const years = Math.min(50, Math.max(1, Math.round(parseFloat($("annees").value) || 1)));

    const total = balanceAt(C, P, rate, years * 12);
    const paid = C + P * years * 12;
    $("total").textContent = eur.format(total);
    $("detail").textContent = "Dont " + eur.format(paid) + " versés et " + eur.format(total - paid) + " d’intérêts.";

    const W = 400, H = 150, padL = 6, padB = 8, padT = 8;
    const pts1 = [], pts2 = [];
    for (let y = 0; y <= years; y++) {
      pts1.push(balanceAt(C, P, rate, y * 12));
      pts2.push(C + P * y * 12);
    }
    const max = Math.max(...pts1, 1);
    const x = i => padL + (i / years) * (W - padL * 2);
    const yv = v => H - padB - (v / max) * (H - padB - padT);
    const path = arr => arr.map((v, i) => (i ? "L" : "M") + x(i).toFixed(1) + " " + yv(v).toFixed(1)).join(" ");
    const css = getComputedStyle(document.documentElement);
    const mint = css.getPropertyValue("--mint").trim();
    const muted = css.getPropertyValue("--muted").trim();
    const line = css.getPropertyValue("--line").trim();

    $("chart").innerHTML =
      '<line x1="' + padL + '" y1="' + (H - padB) + '" x2="' + (W - padL) + '" y2="' + (H - padB) + '" stroke="' + line + '" stroke-width="1.5"/>' +
      '<path d="' + path(pts2) + '" fill="none" stroke="' + muted + '" stroke-width="2" stroke-dasharray="5 4"/>' +
      '<path d="' + path(pts1) + '" fill="none" stroke="' + mint + '" stroke-width="3" stroke-linejoin="round"/>';
  }

  ["capital", "versement", "taux", "annees"].forEach(id => $(id).addEventListener("input", update));
  update();
</script>
</body>
</html>
