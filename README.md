<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Reise des Guten – Ein kleines Storyspiel</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    :root {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: #0f172a;
      color: #f9fafb;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    #app {
      background: radial-gradient(circle at top, #1e293b, #020617);
      border-radius: 16px;
      padding: 24px;
      max-width: 950px;
      width: 100%;
      box-shadow: 0 20px 40px rgba(0,0,0,0.45);
      box-sizing: border-box;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 16px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    header h1 {
      font-size: 1.6rem;
      margin: 0;
    }

    header p {
      margin: 0;
      font-size: 0.9rem;
      color: #cbd5f5;
    }

    .tagline {
      font-size: 0.8rem;
      opacity: 0.8;
    }

    .chip {
      padding: 4px 10px;
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.6);
      font-size: 0.75rem;
      white-space: nowrap;
    }

    main {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .card {
      border-radius: 12px;
      background: rgba(15,23,42,0.85);
      padding: 18px 18px 16px 18px;
      border: 1px solid rgba(148,163,184,0.2);
    }

    .hidden {
      display: none;
    }

    h2 {
      margin-top: 0;
      margin-bottom: 10px;
      font-size: 1.2rem;
    }

    p {
      margin: 6px 0;
      font-size: 0.95rem;
      line-height: 1.4;
    }

    .hint {
      font-size: 0.85rem;
      color: #94a3b8;
    }

    .primary-button,
    .secondary-button,
    .voice-button {
      border: none;
      border-radius: 999px;
      padding: 9px 16px;
      font-size: 0.95rem;
      cursor: pointer;
      transition: transform 0.05s ease, box-shadow 0.1s ease, background 0.2s ease;
    }

    .primary-button {
      background: linear-gradient(135deg, #4f46e5, #8b5cf6);
      color: #f9fafb;
      box-shadow: 0 8px 20px rgba(79,70,229,0.45);
    }

    .primary-button:hover {
      transform: translateY(-1px);
      box-shadow: 0 10px 24px rgba(79,70,229,0.55);
    }

    .primary-button:active {
      transform: translateY(0);
      box-shadow: 0 4px 10px rgba(79,70,229,0.4);
    }

    .secondary-button {
      background: transparent;
      color: #e5e7eb;
      border: 1px solid rgba(148,163,184,0.6);
    }

    .secondary-button:hover {
      background: rgba(30,64,175,0.2);
    }

    .voice-button {
      width: 100%;
      text-align: left;
      background: rgba(15,23,42,0.95);
      color: #e5e7eb;
      border: 1px solid rgba(148,163,184,0.4);
      margin-bottom: 8px;
    }

    .voice-button:hover {
      background: rgba(30,64,175,0.25);
    }

    .voice-button.selected {
      background: rgba(79,70,229,0.25);
      border-color: rgba(129,140,248,0.9);
      box-shadow: 0 0 0 1px rgba(129,140,248,0.6);
    }

    .voice-button:disabled {
      opacity: 0.7;
      cursor: default;
      transform: none;
      box-shadow: none;
    }

    .question {
      margin-top: 10px;
      font-weight: 500;
    }

    .voices-label {
      font-size: 0.85rem;
      color: #9ca3af;
      margin-top: 6px;
      margin-bottom: 4px;
    }

    #voice-result {
      margin-top: 10px;
      padding-top: 8px;
      border-top: 1px dashed rgba(148,163,184,0.4);
      font-size: 0.92rem;
    }

    #voice-result strong {
      color: #e5e7eb;
    }

    textarea {
      width: 100%;
      min-height: 70px;
      border-radius: 10px;
      border: 1px solid rgba(148,163,184,0.5);
      background: rgba(15,23,42,0.95);
      color: #e5e7eb;
      padding: 8px 10px;
      font-family: inherit;
      font-size: 0.9rem;
      resize: vertical;
      box-sizing: border-box;
      margin-top: 6px;
    }

    textarea:focus {
      outline: none;
      border-color: rgba(129,140,248,0.9);
      box-shadow: 0 0 0 1px rgba(129,140,248,0.6);
    }

    .controls-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      gap: 8px;
      flex-wrap: wrap;
    }

    .controls-row .hint {
      flex: 1;
      min-width: 180px;
    }

    .status-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.8rem;
      color: #9ca3af;
      margin-top: 10px;
      gap: 8px;
      flex-wrap: wrap;
    }

    .status-bar strong {
      color: #e5e7eb;
    }

    .bar-wrapper {
      flex: 1;
      min-width: 140px;
      background: rgba(15,23,42,0.9);
      border-radius: 999px;
      overflow: hidden;
      border: 1px solid rgba(148,163,184,0.3);
      height: 8px;
    }

    .bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #22c55e, #a3e635);
      transition: width 0.25s ease-out;
    }

    .profile-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: 10px;
      margin: 10px 0;
    }

    .profile-pill {
      padding: 8px 10px;
      border-radius: 10px;
      border: 1px solid rgba(148,163,184,0.4);
      font-size: 0.85rem;
      background: rgba(15,23,42,0.8);
    }

    .profile-pill strong {
      display: block;
      margin-bottom: 3px;
      color: #e5e7eb;
    }

    .diary {
      margin-top: 12px;
      border-top: 1px dashed rgba(148,163,184,0.4);
      padding-top: 10px;
      max-height: 250px;
      overflow-y: auto;
    }

    .diary-entry {
      margin-bottom: 8px;
      padding-bottom: 6px;
      border-bottom: 1px solid rgba(30,41,59,0.6);
      font-size: 0.88rem;
    }

    .diary-entry:last-child {
      border-bottom: none;
    }

    .diary-entry strong {
      color: #e5e7eb;
    }

    @media (max-width: 640px) {
      #app {
        border-radius: 0;
        height: 100vh;
        max-height: 100vh;
        overflow-y: auto;
      }
    }
  </style>
</head>
<body>
<div id="app">
  <header>
    <div>
      <h1>Reise des Guten</h1>
      <p class="tagline">Ein Story-Spiel über Entscheidungen, Folgen und Menschsein.</p>
    </div>
    <div class="chip">ca. 10 Minuten</div>
  </header>

  <main>
    <section id="start-screen" class="card">
      <h2>Wie „gut“ willst du heute sein?</h2>
      <p>
        Du durchläufst mehrere Alltagsszenen. In jeder Szene melden sich verschiedene
        innere Stimmen: Selbstschutz, Mitgefühl, Gerechtigkeit, Ehrlichkeit.
      </p>
      <p>
        Du entscheidest, welcher Stimme du folgst, liest kurz über mögliche Folgen
        und kannst deine eigenen Gedanken dazu aufschreiben.
      </p>
      <p class="hint">
        Am Ende siehst du dein kleines „Profil des Guten“ und ein Tagebuch deiner Entscheidungen:
        eher für andere, eher für dich selbst, eher regelorientiert oder eher bauchgefühl-mäßig?
        Anthropologisch: Was sagt das über unser Bild vom Menschen?
      </p>
      <button class="primary-button" id="start-button">Reise beginnen</button>
    </section>

    <section id="game-screen" class="card hidden">
      <h2 id="scene-title"></h2>
      <p id="scene-text"></p>
      <p class="question" id="scene-question"></p>

      <p class="voices-label">Deine inneren Stimmen heute:</p>
      <div id="voices-container"></div>

      <div id="voice-result" class="hidden"></div>

      <div id="reflection-block" class="hidden">
        <label for="reflection-input" class="voices-label">
          Deine Gedanken dazu (optional, wird im Tagebuch gespeichert):
        </label>
        <textarea
          id="reflection-input"
          placeholder="Wie fühlt sich deine Entscheidung an? Was wäre, wenn alle Menschen so handeln würden?"
        ></textarea>

        <div class="controls-row">
          <p class="hint">
            Du kannst auch ohne Text weitermachen. Das Spiel bewertet nicht,
            es sammelt nur deine Reise.
          </p>
          <button class="primary-button" id="next-button">Weiter zur nächsten Szene</button>
        </div>
      </div>

      <div class="status-bar">
        <span id="scene-counter"></span>
        <div class="bar-wrapper">
          <div class="bar-fill" id="progress-bar"></div>
        </div>
        <span id="profile-preview"></span>
      </div>
    </section>

    <section id="end-screen" class="card hidden">
      <h2>Dein heutiges Bild vom Guten</h2>
      <p>
        In diesem Durchgang hast du bestimmte Aspekte des Guten stärker betont als andere.
        Das ist keine feste Diagnose, eher ein Schnappschuss deiner Entscheidungen.
      </p>

      <div class="profile-grid">
        <div class="profile-pill">
          <strong>Mitgefühl &amp; Fürsorge</strong>
          <span id="score-empathy"></span>
        </div>
        <div class="profile-pill">
          <strong>Gerechtigkeit &amp; Fairness</strong>
          <span id="score-justice"></span>
        </div>
        <div class="profile-pill">
          <strong>Ehrlichkeit &amp; Wahrhaftigkeit</strong>
          <span id="score-honesty"></span>
        </div>
        <div class="profile-pill">
          <strong>Selbstfürsorge &amp; Grenzen</strong>
          <span id="score-selfCare"></span>
        </div>
      </div>

      <p><strong>Fragen an dein Menschenbild:</strong></p>
      <ul>
        <li>Wenn alle so handeln würden wie du im Spiel – wäre die Welt eher weich, gerecht, hart oder chaotisch?</li>
        <li>Ist ein Mensch „gut“, wenn er gute Absichten hat, ehrlich ist oder wenn die Folgen für alle positiv sind?</li>
        <li>Wie viel „gut zu dir selbst“ gehört für dich zum „gut zu anderen“ dazu?</li>
      </ul>

      <div class="diary" id="diary"></div>

      <p class="hint">
        Du kannst die Reise noch einmal machen und bewusst anders entscheiden, um zu sehen,
        wie sich dein Profil verschiebt.
      </p>

      <button class="secondary-button" id="restart-button">Noch einmal reisen</button>
    </section>
  </main>
</div>

<script>
  const scenes = [
    {
      title: "Morgen: Der Blick ins Handy",
      text:
        "Du wachst auf und siehst direkt am Handy eine Nachricht: Eine Freundin schreibt, dass es ihr gerade " +
        "psychisch richtig schlecht geht. Eigentlich bist du selbst total müde, heute steht viel an.",
      question: "Welche innere Stimme bekommt heute den meisten Raum?",
      voices: [
        {
          label: "Mitgefühl: Ich nehme mir Zeit für sie, auch wenn es mich Kraft kostet.",
          tag: "empathy",
          impact: { empathy: 2, justice: 0, honesty: 1, selfCare: -1 },
          explanation:
            "Du stellst ihre Not über deine eigene Müdigkeit und nimmst dir bewusst Zeit.",
          consequence:
            "Die Beziehung kann sich vertiefen, aber du musst aufpassen, dich nicht zu überfordern."
        },
        {
          label: "Selbstschutz: Ich schreibe kurz, dass ich mich später melde, und kümmere mich erst um mich.",
          tag: "selfCare",
          impact: { empathy: 0, justice: 0, honesty: 1, selfCare: 2 },
          explanation:
            "Du nimmst deine Grenzen ernst und kümmerst dich zuerst um deinen Tag.",
          consequence:
            "Du schützt deine Energie, riskierst aber, dass sie sich erstmal allein gelassen fühlt."
        },
        {
          label: "Ehrlichkeit: Ich sage offen, dass ich sie sehe, aber gerade wenig Kraft habe.",
          tag: "honesty",
          impact: { empathy: 1, justice: 0, honesty: 2, selfCare: 1 },
          explanation:
            "Du versuchst, ehrlich über deine eigenen Grenzen und ihre Situation zu sprechen.",
          consequence:
            "Es kann Vertrauen stärken, wenn beide Seiten mit Wahrheit umgehen können."
        }
      ]
    },
    {
      title: "Schulweg: Der Sturz an der Haltestelle",
      text:
        "An der Bushaltestelle stolpert ein jüngeres Kind, fällt hin und alle schauen kurz weg. " +
        "Du bist spät dran und der Bus kommt gleich.",
      question: "Welche Stimme setzt sich durch?",
      voices: [
        {
          label: "Hilfsbereitschaft: Ich helfe ihm hoch und checke, ob alles okay ist, auch wenn ich den Bus verpasse.",
          tag: "empathy",
          impact: { empathy: 2, justice: 1, honesty: 0, selfCare: -1 },
          explanation:
            "Du stellst das Wohlergehen des Kindes über Pünktlichkeit.",
          consequence:
            "Für das Kind kann das ein prägender Moment von Menschlichkeit sein – du nimmst Stress in Kauf."
        },
        {
          label: "Pragmatismus: Ich schaue kurz rüber, aber steige in den Bus, weil mein Tag sonst eskaliert.",
          tag: "selfCare",
          impact: { empathy: -1, justice: 0, honesty: 0, selfCare: 1 },
          explanation:
            "Du entscheidest dich für deinen Zeitplan und gehst davon aus, dass sich schon jemand kümmert.",
          consequence:
            "Du entlastest dich selbst, lässt aber einen möglichen Moment echter Hilfe vorbeiziehen."
        },
        {
          label: "Signal: Ich frage laut in die Runde, ob alles okay ist, und steige dann ein.",
          tag: "justice",
          impact: { empathy: 1, justice: 1, honesty: 1, selfCare: 1 },
          explanation:
            "Du setzt ein Zeichen, dass es nicht egal ist, aber suchst trotzdem Ausgleich mit deinen Pflichten.",
          consequence:
            "Du zeigst Verantwortung in der Gruppe, ohne dich komplett aufzuhalten."
        }
      ]
    },
    {
      title: "Vormittag: Gruppenarbeit",
      text:
        "In einer Präsentation habt ihr die Aufgaben aufgeteilt. Eine Person aus der Gruppe hat kaum etwas gemacht " +
        "und will trotzdem mit euch die Note teilen.",
      question: "Welche innere Haltung prägt dein Handeln?",
      voices: [
        {
          label: "Gerechtigkeit: Ich spreche das direkt an und fordere, dass die Leistung fair benannt wird.",
          tag: "justice",
          impact: { empathy: 0, justice: 2, honesty: 2, selfCare: 0 },
          explanation:
            "Du trittst für Fairness und Ehrlichkeit gegenüber der Lehrkraft und der Gruppe ein.",
          consequence:
            "Das kann Konflikte auslösen, aber auch verhindern, dass Faulheit dauerhaft belohnt wird."
        },
        {
          label: "Harmonie: Ich lasse es laufen, Hauptsache die Stimmung bleibt gut.",
          tag: "empathy",
          impact: { empathy: 1, justice: -1, honesty: -1, selfCare: 1 },
          explanation:
            "Du stellst den Frieden in der Gruppe über Gerechtigkeit.",
          consequence:
            "Kurzfristig bleibt es angenehm, langfristig kann Frust entstehen – bei dir oder anderen."
        },
        {
          label: "Kompromiss: Ich erkläre, dass ich das unfair finde, und schlage vor, dass die Person nächstes Mal mehr übernimmt.",
          tag: "honesty",
          impact: { empathy: 1, justice: 1, honesty: 1, selfCare: 1 },
          explanation:
            "Du benennst das Problem, ohne die Person direkt „abzuschießen“.",
          consequence:
            "Das eröffnet die Chance, dass sich Verhalten ändert, ohne die Beziehung zu zerstören."
        }
      ]
    },
    {
      title: "Mittag: Der Kommentar am Tisch",
      text:
        "Beim Essen macht jemand einen abwertenden Spruch über eine andere Herkunft oder Religion. " +
        "Ein paar lachen, andere sagen nichts.",
      question: "Welche Stimme in dir ist am lautesten?",
      voices: [
        {
          label: "Zivilcourage: Ich sage ruhig, dass das verletzend ist und nicht witzig.",
          tag: "justice",
          impact: { empathy: 2, justice: 2, honesty: 1, selfCare: -1 },
          explanation:
            "Du schützt Menschen, die gerade nicht direkt da sind oder sich nicht trauen, etwas zu sagen.",
          consequence:
            "Du kannst anecken, aber du setzt ein klares Zeichen, wie du dir Gemeinschaft vorstellst."
        },
        {
          label: "Unsichtbar: Ich starre aufs Handy und tue so, als hätte ich nichts gehört.",
          tag: "selfCare",
          impact: { empathy: -1, justice: -1, honesty: 0, selfCare: 2 },
          explanation:
            "Du vermeidest jede Konfrontation und schützt dich vor unangenehmen Situationen.",
          consequence:
            "Der Spruch bleibt unwidersprochen – und wirkt dadurch für andere vielleicht okay."
        },
        {
          label: "Ironie: Ich mache einen Gegenwitz, der zeigt, dass ich das nicht ernst nehme.",
          tag: "honesty",
          impact: { empathy: 0, justice: 0, honesty: 1, selfCare: 1 },
          explanation:
            "Du versuchst, mit Humor Abstand zu schaffen, ohne direkt frontal anzugreifen.",
          consequence:
            "Manche verstehen die Ebene, andere vielleicht nicht – das Risiko der Missinterpretation bleibt."
        }
      ]
    },
    {
      title: "Nachmittag: Eigene Grenzen",
      text:
        "Du hast Hausaufgaben, Lernstoff und gleichzeitig die Chance, jemandem bei einem Umzug oder Projekt zu helfen. " +
        "Eigentlich bist du innerlich schon ziemlich voll.",
      question: "Wie gehst du mit dir selbst um?",
      voices: [
        {
          label: "Selbstfürsorge: Ich sage offen ab und erkläre, dass ich meine Kräfte einteilen muss.",
          tag: "selfCare",
          impact: { empathy: 0, justice: 0, honesty: 2, selfCare: 2 },
          explanation:
            "Du erkennst an, dass du nicht unendlich belastbar bist.",
          consequence:
            "Du schützt dich vor Überforderung – andere müssen mit ihrer Enttäuschung umgehen."
        },
        {
          label: "Aufopferung: Ich helfe trotzdem und mache meine eigenen Sachen später nachts.",
          tag: "empathy",
          impact: { empathy: 2, justice: 0, honesty: 0, selfCare: -2 },
          explanation:
            "Du stellst andere komplett vor dich selbst.",
          consequence:
            "Kurzfristig ist das hilfreich für die anderen, langfristig kann es dich ausbrennen."
        },
        {
          label: "Struktur: Ich biete an, eine kleinere Aufgabe zu übernehmen, die in meinen Plan passt.",
          tag: "justice",
          impact: { empathy: 1, justice: 1, honesty: 1, selfCare: 1 },
          explanation:
            "Du suchst einen Mittelweg zwischen Helfen und Grenzen setzen.",
          consequence:
            "Du bleibst verlässlich, ohne dich komplett zu verlieren."
        }
      ]
    },
    {
      title: "Abend: Online-Spiel und Fairness",
      text:
        "Du spielst online. Jemand im gegnerischen Team hängt und kann sich nicht richtig bewegen. " +
        "Dein Team freut sich über leichte Kills.",
      question: "Was bedeutet „gut“ sein in einem Spiel für dich?",
      voices: [
        {
          label: "Fairplay: Ich schlage vor, die Runde neu zu starten oder nicht voll auszunutzen.",
          tag: "justice",
          impact: { empathy: 1, justice: 2, honesty: 1, selfCare: 0 },
          explanation:
            "Du überträgst dein Gerechtigkeitsgefühl auch auf digitale Räume.",
          consequence:
            "Manche finden das ehrenhaft, andere rollen vielleicht mit den Augen – du stehst zu deinem Fairnessgefühl."
        },
        {
          label: "Kompetitiv: Ich nutze den Vorteil, so ist das Spiel nun mal.",
          tag: "selfCare",
          impact: { empathy: -1, justice: -1, honesty: 0, selfCare: 1 },
          explanation:
            "Du spielst nach dem Motto: Alles, was erlaubt ist, ist okay.",
          consequence:
            "Du gewinnst vielleicht, aber die Frage bleibt: Welche Haltung trainierst du dir damit an?"
        },
        {
          label: "Empathie: Ich schreibe kurz in den Chat, dass es schade ist, und mache mir bewusst, dass da ein echter Mensch sitzt.",
          tag: "empathy",
          impact: { empathy: 2, justice: 0, honesty: 1, selfCare: 0 },
          explanation:
            "Du erinnerst dich daran, dass hinter Avataren reale Personen stehen.",
          consequence:
            "Du bringst Menschlichkeit in eine Umgebung, die oft anonym und hart ist."
        }
      ]
    },
    {
      title: "Nacht: Blick zurück auf den Tag",
      text:
        "Du liegst im Bett und gehst im Kopf noch einmal durch, was heute so passiert ist – " +
        "die kleinen Momente, in denen du gut sein wolltest oder konntest.",
      question: "Wie bewertest du dich selbst als Mensch heute?",
      voices: [
        {
          label: "Sanfter Blick: Ich sehe, wo ich mich bemüht habe, und verzeihe mir, wo es nicht perfekt war.",
          tag: "empathy",
          impact: { empathy: 2, justice: 0, honesty: 1, selfCare: 2 },
          explanation:
            "Du schaust liebevoll auf dich selbst, ohne dich als „perfekt gut“ zu inszenieren.",
          consequence:
            "Das kann helfen, langfristig mutiger zu werden, weil Fehler erlaubt sind."
        },
        {
          label: "Strenger Blick: Ich kritisiere mich hart für alles, was ich besser hätte machen können.",
          tag: "justice",
          impact: { empathy: 0, justice: 1, honesty: 1, selfCare: -2 },
          explanation:
            "Du willst streng gerecht mit dir sein und suchst nach Optimierung.",
          consequence:
            "Das kann dich antreiben, aber auch zu Selbsthass führen, wenn es zu viel wird."
        },
        {
          label: "Verdrängung: Ich denke gar nicht weiter darüber nach und scrolle mich einfach müde.",
          tag: "selfCare",
          impact: { empathy: -1, justice: 0, honesty: 0, selfCare: 1 },
          explanation:
            "Du vermeidest Reflexion und betäubst dich mit Ablenkung.",
          consequence:
            "Kurzfristig beruhigend, langfristig verpasst du die Chance, aus deinem Tag zu lernen."
        }
      ]
    }
  ];

  let currentIndex = 0;
  let profile = {
    empathy: 0,
    justice: 0,
    honesty: 0,
    selfCare: 0
  };
  let diaryEntries = [];
  let currentChoice = null;

  const startScreen = document.getElementById("start-screen");
  const gameScreen = document.getElementById("game-screen");
  const endScreen = document.getElementById("end-screen");

  const sceneTitle = document.getElementById("scene-title");
  const sceneText = document.getElementById("scene-text");
  const sceneQuestion = document.getElementById("scene-question");
  const voicesContainer = document.getElementById("voices-container");
  const voiceResult = document.getElementById("voice-result");
  const reflectionBlock = document.getElementById("reflection-block");
  const reflectionInput = document.getElementById("reflection-input");
  const nextButton = document.getElementById("next-button");

  const sceneCounter = document.getElementById("scene-counter");
  const progressBar = document.getElementById("progress-bar");
  const profilePreview = document.getElementById("profile-preview");

  const scoreEmpathy = document.getElementById("score-empathy");
  const scoreJustice = document.getElementById("score-justice");
  const scoreHonesty = document.getElementById("score-honesty");
  const scoreSelfCare = document.getElementById("score-selfCare");
  const diaryContainer = document.getElementById("diary");

  document.getElementById("start-button").addEventListener("click", startGame);
  document.getElementById("restart-button").addEventListener("click", () => {
    endScreen.classList.add("hidden");
    startScreen.classList.remove("hidden");
  });

  nextButton.addEventListener("click", handleNext);

  function startGame() {
    currentIndex = 0;
    profile = { empathy: 0, justice: 0, honesty: 0, selfCare: 0 };
    diaryEntries = [];
    currentChoice = null;
    reflectionInput.value = "";
    startScreen.classList.add("hidden");
    endScreen.classList.add("hidden");
    gameScreen.classList.remove("hidden");
    renderScene();
  }

  function renderScene() {
    const scene = scenes[currentIndex];
    sceneTitle.textContent = scene.title;
    sceneText.textContent = scene.text;
    sceneQuestion.textContent = scene.question;

    voicesContainer.innerHTML = "";
    voiceResult.classList.add("hidden");
    voiceResult.textContent = "";
    reflectionBlock.classList.add("hidden");
    reflectionInput.value = "";
    currentChoice = null;

    scene.voices.forEach((voice, index) => {
      const btn = document.createElement("button");
      btn.className = "voice-button";
      btn.textContent = voice.label;
      btn.addEventListener("click", () => handleVoiceClick(index));
      voicesContainer.appendChild(btn);
    });

    updateStatus(false);
  }

  function handleVoiceClick(idx) {
    const scene = scenes[currentIndex];
    const voice = scene.voices[idx];
    currentChoice = voice;

    const buttons = voicesContainer.querySelectorAll(".voice-button");
    buttons.forEach((b, i) => {
      b.disabled = true;
      if (i === idx) b.classList.add("selected");
    });

    applyImpact(voice.impact);
    voiceResult.innerHTML =
      "<strong>Deine gewählte Stimme:</strong> " + voice.explanation +
      "<br><br><strong>Mögliche Folgen:</strong> " + voice.consequence;
    voiceResult.classList.remove("hidden");
    reflectionBlock.classList.remove("hidden");

    updateStatus(true);
  }

  function applyImpact(impact) {
    profile.empathy += impact.empathy || 0;
    profile.justice += impact.justice || 0;
    profile.honesty += impact.honesty || 0;
    profile.selfCare += impact.selfCare || 0;
  }

  function handleNext() {
    if (!currentChoice) {
      return;
    }
    const reflectionText = reflectionInput.value.trim();
    diaryEntries.push({
      sceneTitle: scenes[currentIndex].title,
      choiceLabel: currentChoice.label,
      tag: currentChoice.tag,
      reflection: reflectionText
    });

    currentIndex++;
    if (currentIndex >= scenes.length) {
      showEndScreen();
    } else {
      renderScene();
    }
  }

  function updateStatus(showPreview) {
    const total = scenes.length;
    const current = currentIndex + 1;
    sceneCounter.textContent = "Szene " + current + " von " + total;

    const progressPercent = (currentIndex / total) * 100;
    progressBar.style.width = progressPercent + "%";

    if (showPreview) {
      profilePreview.textContent =
        "Mitgefühl: " + profile.empathy +
        " | Gerechtigkeit: " + profile.justice +
        " | Ehrlichkeit: " + profile.honesty +
        " | Selbstfürsorge: " + profile.selfCare;
    } else {
      profilePreview.textContent = "";
    }
  }

  function showEndScreen() {
    gameScreen.classList.add("hidden");
    endScreen.classList.remove("hidden");

    scoreEmpathy.textContent = buildScoreText(profile.empathy);
    scoreJustice.textContent = buildScoreText(profile.justice);
    scoreHonesty.textContent = buildScoreText(profile.honesty);
    scoreSelfCare.textContent = buildScoreText(profile.selfCare);

    diaryContainer.innerHTML = "<strong>Dein Tagebuch der Entscheidungen:</strong>";
    diaryEntries.forEach((entry, index) => {
      const div = document.createElement("div");
      div.className = "diary-entry";
      div.innerHTML =
        "<strong>" + (index + 1) + ". " + entry.sceneTitle + "</strong><br>" +
        "Gewählte Stimme: " + entry.choiceLabel + "<br>" +
        (entry.reflection
          ? "Dein Gedanke: " + entry.reflection
          : "<span class='hint'>Kein Text geschrieben – vielleicht beim nächsten Mal?</span>");
      diaryContainer.appendChild(div);
    });
  }

  function buildScoreText(value) {
    let tendency;
    if (value >= 6) {
      tendency = "sehr stark betont in deinen Entscheidungen.";
    } else if (value >= 3) {
      tendency = "klar erkennbar in deinem Handeln.";
    } else if (value >= 1) {
      tendency = "leicht vorhanden – manchmal wichtig, manchmal nicht.";
    } else if (value === 0) {
      tendency = "heute eher neutral geblieben.";
    } else {
      tendency = "eher zurückgestellt zugunsten anderer Aspekte.";
    }
    return value + " Punkte – " + tendency;
  }
</script>
</body>
</html>
