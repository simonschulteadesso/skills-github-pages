<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <title>Experiment E-Mail-Personalisierung</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      margin: 0;
      padding: 1.5rem;
      background: #f5f5f5;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      background: #ffffff;
      padding: 1.5rem 2rem;
      border-radius: 6px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.08);
    }
    h1, h2 {
      margin-top: 0;
    }
    .email-box {
      border: 1px solid #ddd;
      border-radius: 4px;
      padding: 1rem 1.25rem;
      background: #fcfcfc;
      margin-bottom: 1.5rem;
      white-space: pre-line;
    }
    .hidden {
      display: none;
    }
    .btn {
      display: inline-block;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      border: none;
      background: #0070f3;
      color: #ffffff;
      font-size: 1rem;
      cursor: pointer;
    }
    .btn:disabled {
      opacity: 0.6;
      cursor: default;
    }
    .question {
      margin-bottom: 1rem;
    }
    .question label {
      display: block;
      font-weight: 600;
      margin-bottom: 0.25rem;
    }
    .scale-labels {
      font-size: 0.85rem;
      display: flex;
      justify-content: space-between;
      margin-top: -0.25rem;
      margin-bottom: 0.25rem;
    }
    .likert {
      display: flex;
      gap: 0.5rem;
    }
    .likert input {
      margin: 0 auto;
    }
    textarea, input[type="text"] {
      width: 100%;
      box-sizing: border-box;
      padding: 0.4rem;
      font-family: inherit;
    }
    .debug-output {
      margin-top: 1.5rem;
      font-family: "SF Mono", Menlo, monospace;
      font-size: 0.85rem;
      white-space: pre-wrap;
      background: #fafafa;
      border-radius: 4px;
      border: 1px solid #eee;
      padding: 0.75rem;
    }
  </style>
</head>
<body>
<div class="container">
  <h1>Studie: Wirkung von Personalisierung in E-Mails</h1>

  <!-- Schritt 1: E-Mail anzeigen -->
  <section id="step-email">
    <p>Bitte lies die folgende E-Mail aufmerksam durch. Klicke anschließend auf „Weiter zum Fragebogen“.</p>

    <!-- Variante 0: keine Personalisierung -->
    <div id="email-variant-0" class="email-box hidden">
      <h2>Betreff: Beispiel-E-Mail – Variante A (ohne Personalisierung)</h2>
      <p>
        [Hier steht der Text der E-Mail ohne Personalisierung.]
      </p>
    </div>

    <!-- Variante 1: wenig Personalisierung -->
    <div id="email-variant-1" class="email-box hidden">
      <h2>Betreff: Beispiel-E-Mail – Variante B (leichte Personalisierung)</h2>
      <p>
        [Hier steht der Text der E-Mail mit geringer Personalisierung.]
      </p>
    </div>

    <!-- Variante 2: starke Personalisierung -->
    <div id="email-variant-2" class="email-box hidden">
      <h2>Betreff: Beispiel-E-Mail – Variante C (starke Personalisierung)</h2>
      <p>
        [Hier steht der Text der E-Mail mit hoher Personalisierung.]
      </p>
    </div>

    <button id="btn-to-survey" class="btn">Weiter zum Fragebogen</button>
  </section>

  <!-- Schritt 2: Fragebogen -->
  <section id="step-survey" class="hidden">
    <h2>Fragebogen zur gezeigten E-Mail</h2>
    <p>Bitte beantworte die folgenden Fragen zur E-Mail, die du gerade gesehen hast.</p>

    <form id="survey-form">
      <!-- versteckt: welche Variante wurde gezeigt -->
      <input type="hidden" id="variant-id" name="variant_id" />

      <div class="question">
        <label>Wie ansprechend fandst du die E-Mail insgesamt?</label>
        <div class="scale-labels">
          <span>1 = gar nicht ansprechend</span>
          <span>5 = sehr ansprechend</span>
        </div>
        <div class="likert">
          <label><input type="radio" name="q_appeal" value="1" required />1</label>
          <label><input type="radio" name="q_appeal" value="2" />2</label>
          <label><input type="radio" name="q_appeal" value="3" />3</label>
          <label><input type="radio" name="q_appeal" value="4" />4</label>
          <label><input type="radio" name="q_appeal" value="5" />5</label>
        </div>
      </div>

      <div class="question">
        <label>Wie glaubwürdig fandst du die E-Mail?</label>
        <div class="scale-labels">
          <span>1 = gar nicht glaubwürdig</span>
          <span>5 = sehr glaubwürdig</span>
        </div>
        <div class="likert">
          <label><input type="radio" name="q_trust" value="1" required />1</label>
          <label><input type="radio" name="q_trust" value="2" />2</label>
          <label><input type="radio" name="q_trust" value="3" />3</label>
          <label><input type="radio" name="q_trust" value="4" />4</label>
          <label><input type="radio" name="q_trust" value="5" />5</label>
        </div>
      </div>

      <div class="question">
        <label>Wie wahrscheinlich wäre es, dass du auf diese E-Mail reagierst (z.B. klickst oder antwortest)?</label>
        <div class="scale-labels">
          <span>1 = sehr unwahrscheinlich</span>
          <span>5 = sehr wahrscheinlich</span>
        </div>
        <div class="likert">
          <label><input type="radio" name="q_intent" value="1" required />1</label>
          <label><input type="radio" name="q_intent" value="2" />2</label>
          <label><input type="radio" name="q_intent" value="3" />3</label>
          <label><input type="radio" name="q_intent" value="4" />4</label>
          <label><input type="radio" name="q_intent" value="5" />5</label>
        </div>
      </div>

      <div class="question">
        <label>Freitext: Was ist dir an der E-Mail besonders positiv oder negativ aufgefallen?</label>
        <textarea name="q_open" rows="4" placeholder="Deine Antwort (optional)"></textarea>
      </div>

      <div class="question">
        <label>Kohorte / Gruppe (z.B. Studiengang, Abteilung, Altersgruppe):</label>
        <input type="text" name="q_cohort" placeholder="z.B. Marketing, Informatik, 18–25" />
      </div>

      <button type="submit" class="btn">Antworten absenden</button>
    </form>

    <div id="debug-output" class="debug-output hidden"></div>
  </section>
</div>

<script>
  // Zufällige Zuteilung zu einer von drei Varianten (0,1,2)
  const variant = Math.floor(Math.random() * 3); // 0,1,2
  const emailBox = document.getElementById("email-variant-" + variant);
  emailBox.classList.remove("hidden");

  const btnToSurvey = document.getElementById("btn-to-survey");
  const stepEmail = document.getElementById("step-email");
  const stepSurvey = document.getElementById("step-survey");
  const variantInput = document.getElementById("variant-id");
  variantInput.value = variant.toString();

  btnToSurvey.addEventListener("click", () => {
    stepEmail.classList.add("hidden");
    stepSurvey.classList.remove("hidden");
  });

  // Form-Handling: hier nur Demo -> Daten im Browser anzeigen
  const form = document.getElementById("survey-form");
  const debugOutput = document.getElementById("debug-output");

  form.addEventListener("submit", (event) => {
    event.preventDefault();

    const formData = new FormData(form);
    const payload = {};

    for (const [key, value] of formData.entries()) {
      payload[key] = value;
    }

    // In der echten Studie: hier per fetch() an einen Server senden
    // fetch('/save', { method: 'POST', body: JSON.stringify(payload), headers: {'Content-Type': 'application/json'}})

    debugOutput.textContent =
      "Simulation: Folgende Daten würden gespeichert werden:\n\n" +
      JSON.stringify(payload, null, 2);
    debugOutput.classList.remove("hidden");

    // Optional: Formular deaktivieren, um Mehrfachsendungen zu vermeiden
    form.querySelectorAll("input, textarea, button").forEach(el => el.disabled = true);
  });
</script>
</body>
</html>
