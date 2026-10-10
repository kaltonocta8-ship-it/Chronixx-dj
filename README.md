# Chronixx-dj<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>ChronixDJ Pro</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #090b10;
  color: #f5f5f5;
  font-family: Arial, sans-serif;
}

header {
  padding: 18px 12px;
  text-align: center;
  background: #141821;
  border-bottom: 2px solid #00e5ff;
}

header h1 {
  margin: 0;
  color: #00e5ff;
  letter-spacing: 3px;
}

header p {
  color: #aaa;
  margin-bottom: 0;
}

main {
  padding: 12px;
  max-width: 1100px;
  margin: auto;
}

.decks {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}

.deck {
  background: #171b25;
  padding: 12px;
  border: 1px solid #333b4c;
  border-radius: 12px;
  min-width: 0;
}

.deck h2 {
  text-align: center;
  margin-top: 4px;
}

.deck-a h2 {
  color: #00e5ff;
}

.deck-b h2 {
  color: #ff4bd8;
}

video {
  display: block;
  width: 100%;
  aspect-ratio: 16 / 9;
  background: #000;
  border-radius: 8px;
  object-fit: contain;
}

.track {
  display: block;
  width: 100%;
  margin: 12px 0;
  font-size: 12px;
}

input[type="range"] {
  width: 100%;
  accent-color: #00e5ff;
}

button, .file-button {
  border: 0;
  border-radius: 7px;
  padding: 10px 7px;
  margin: 3px 0;
  color: white;
  background: #30394b;
  cursor: pointer;
  font-size: 12px;
}

button:active {
  transform: scale(.97);
}

.play {
  background: #087d68;
}

.stop {
  background: #9f2942;
}

.controls {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 4px;
}

.section {
  margin-top: 14px;
  padding: 15px;
  background: #171b25;
  border: 1px solid #333b4c;
  border-radius: 12px;
}

.section h3 {
  margin-top: 0;
  color: #00e5ff;
}

.mixer-row {
  margin: 14px 0;
}

.mixer-row label {
  display: block;
  font-size: 13px;
  margin-bottom: 7px;
}

.cues {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 5px;
  margin-top: 10px;
}

.cue {
  background: #5d327e;
  min-height: 40px;
}

.status {
  color: #aab5c8;
  font-size: 12px;
}

footer {
  text-align: center;
  padding: 22px 8px;
  color: #778397;
  font-size: 12px;
}

@media (max-width: 560px) {
  main {
    padding: 7px;
  }

  .decks {
    gap: 7px;
  }

  .deck {
    padding: 7px;
  }

  .deck h2 {
    font-size: 16px;
  }

  button, .file-button {
    font-size: 11px;
    padding: 9px 3px;
  }

  .section {
    padding: 11px;
  }
}
</style>
</head>

<body>

<header>
  <h1>CHRONIXDJ</h1>
  <p>PRO DJ & VIDEO MIXING STUDIO</p>
</header>

<main>

<div class="decks">

  <section class="deck deck-a">
    <h2>DECK A</h2>

    <video id="videoA" playsinline></video>

    <label class="track">
      LOAD AUDIO OR VIDEO
      <input id="fileA" type="file"
      accept="audio/*,video/*">
    </label>

    <p id="nameA" class="status">No track loaded</p>

    <div class="controls">
      <button class="play" onclick="playDeck('A')">
        ▶ PLAY
      </button>
      <button onclick="pauseDeck('A')">
        ❚❚ PAUSE
      </button>
      <button class="stop" onclick="stopDeck('A')">
        ■ STOP
      </button>
    </div>

    <div class="mixer-row">
      <label>Track position</label>
      <input id="seekA" type="range"
      min="0" max="100" value="0"
      oninput="seekDeck('A', this.value)">
      <div id="timeA" class="status">00:00 / 00:00</div>
    </div>

    <div class="mixer-row">
      <label>Deck volume</label>
      <input id="volumeA" type="range"
      min="0" max="1" step="0.01" value="0.8"
      oninput="updateMixer()">
    </div>

    <div class="mixer-row">
      <label>Playback speed</label>
      <input type="range" min="0.5" max="1.5"
      step="0.01" value="1"
      oninput="setSpeed('A', this.value)">
    </div>

    <div class="mixer-row">
      <label>Filter</label>
      <input type="range" min="0" max="100"
      value="100"
      oninput="setFilter('A', this.value)">
    </div>

    <div class="mixer-row">
      <label>Touch to scratch</label>
      <input type="range" min="0" max="100"
      value="0"
      oninput="scratchDeck('A', this.value)">
    </div>

    <div class="cues">
      <button class="cue" onclick="setCue('A',0)">CUE 1</button>
      <button class="cue" onclick="setCue('A',1)">CUE 2</button>
      <button class="cue" onclick="setCue('A',2)">CUE 3</button>
      <button class="cue" onclick="setCue('A',3)">CUE 4</button>
    </div>

    <button onclick="toggleLoop('A')"
    style="width:100%">LOOP IN / OUT</button>

  </section>

  <section class="deck deck-b">
    <h2>DECK B</h2>

    <video id="videoB" playsinline></video>

    <label class="track">
      LOAD AUDIO OR VIDEO
      <input id="fileB" type="file"
      accept="audio/*,video/*">
    </label>

    <p id="nameB" class="status">No track loaded</p>

    <div class="controls">
      <button class="play" onclick="playDeck('B')">
        ▶ PLAY
      </button>
      <button onclick="pauseDeck('B')">
        ❚❚ PAUSE
      </button>
      <button class="stop" onclick="stopDeck('B')">
        ■ STOP
      </button>
    </div>

    <div class="mixer-row">
      <label>Track position</label>
      <input id="seekB" type="range"
      min="0" max="100" value="0"
      oninput="seekDeck('B', this.value)">
      <div id="timeB" class="status">00:00 / 00:00</div>
    </div>

    <div class="mixer-row">
      <label>Deck volume</label>
      <input id="volumeB" type="range"
      min="0" max="1" step="0.01" value="0.8"
      oninput="updateMixer()">
    </div>

    <div class="mixer-row">
      <label>Playback speed</label>
      <input type="range" min="0.5" max="1.5"
      step="0.01" value="1"
      oninput="setSpeed('B', this.value)">
    </div>

    <div class="mixer-row">
      <label>Filter</label>
      <input type="range" min="0" max="100"
      value="100"
      oninput="setFilter('B', this.value)">
    </div>

    <div class="mixer-row">
      <label>Touch to scratch</label>
      <input type="range" min="0" max="100"
      value="0"
      oninput="scratchDeck('B', this.value)">
    </div>

    <div class="cues">
      <button class="cue" onclick="setCue('B',0)">CUE 1</button>
      <button class="cue" onclick="setCue('B',1)">CUE 2</button>
      <button class="cue" onclick="setCue('B',2)">CUE 3</button>
      <button class="cue" onclick="setCue('B',3)">CUE 4</button>
    </div>

    <button onclick="toggleLoop('B')"
    style="width:100%">LOOP IN / OUT</button>

  </section>
</div>

<section class="section">
  <h3>🎚️ MASTER MIXER</h3>

  <div class="mixer-row">
    <label>Crossfader — Deck A ↔ Deck B</label>
    <input id="crossfader" type="range"
    min="0" max="100" value="50"
    oninput="updateMixer()">
  </div>

  <div class="mixer-row">
    <label>Master volume</label>
    <input id="master" type="range"
    min="0" max="1" step="0.01" value="0.8"
    oninput="updateMixer()">
  </div>

  <button onclick="toggleVideoFullscreen()">
    📺 FULL-SCREEN VIDEO
  </button>

  <p id="message" class="status">
    ChronixDJ ready. Load a track to begin.
  </p>
</section>

<footer>
  CHRONIXDJ PRO • YOUR MUSIC, YOUR MIX
</footer>

</main>

<script>
const decks = {
  A: {
    video: document.getElementById("videoA"),
    cues: [null, null, null, null],
    loopIn: null,
    loopOut: null,
    objectURL: null,
    filter: 100
  },
  B: {
    video: document.getElementById("videoB"),
    cues: [null, null, null, null],
    loopIn: null,
    loopOut: null,
    objectURL: null,
    filter: 100
  }
};

function message(text) {
  document.getElementById("message").textContent = text;
}

function formatTime(seconds) {
  if (!Number.isFinite(seconds)) return "00:00";
  const m = Math.floor(seconds / 60);
  const s = Math.floor(seconds % 60);
  return String(m).padStart(2, "0") + ":" +
         String(s).padStart(2, "0");
}

["A", "B"].forEach(id => {
  const d = decks[id];
  const v = d.video;

  document.getElementById("file" + id)
    .addEventListener("change", event => {
      const file = event.target.files[0];
      if (!file) return;

      if (d.objectURL) URL.revokeObjectURL(d.objectURL);

      d.objectURL = URL.createObjectURL(file);
      v.src = d.objectURL;
      v.load();

      document.getElementById("name" + id).textContent =
        file.name;

      d.cues = [null, null, null, null];
      d.loopIn = null;
      d.loopOut = null;

      message("Loaded " + file.name + " on Deck " + id);
    });

  v.addEventListener("timeupdate", () => {
    const seek = document.getElementById("seek" + id);

    if (Number.isFinite(v.duration) && v.duration > 0) {
      seek.value = v.currentTime / v.duration * 100;
    }

    document.getElementById("time" + id).textContent =
      formatTime(v.currentTime) + " / " +
      formatTime(v.duration);

    if (d.loopIn !== null && d.loopOut !== null &&
        v.currentTime >= d.loopOut) {
      v.currentTime = d.loopIn;
    }
  });

  v.addEventListener("ended", () => {
    message("Deck " + id + " finished playing.");
  });
});

function playDeck(id) {
  const v = decks[id].video;

  if (!v.src) {
    message("Load a track on Deck " + id + " first.");
    return;
  }

  v.play().then(() => {
    message("Playing Deck " + id);
  }).catch(() => {
    message("Playback unavailable. Try loading another file.");
  });
}

function pauseDeck(id) {
  decks[id].video.pause();
  message("Deck " + id + " paused.");
}

function stopDeck(id) {
  const v = decks[id].video;
  v.pause();
  v.currentTime = 0;
  message("Deck " + id + " stopped.");
}

function seekDeck(id, value) {
  const v = decks[id].video;

  if (Number.isFinite(v.duration) && v.duration > 0) {
    v.currentTime = Number(value) / 100 * v.duration;
  }
}

function setSpeed(id, value) {
  decks[id].video.playbackRate = Number(value);
}

function setFilter(id, value) {
  const d = decks[id];
  d.filter = Number(value);

  // Basic high-frequency reduction.
  // Full DJ filter effects need Web Audio processing.
  const brightness = 0.5 + d.filter / 200;
  d.video.style.filter = "brightness(" + brightness + ")";
}

function scratchDeck(id, value) {
  const v = decks[id].video;

  if (!Number.isFinite(v.duration) || v.duration <= 0) {
    return;
  }

  // Basic touch-position seeking prototype,
  // not a full vinyl scratching engine.
  if (!v.paused) {
    v.currentTime = Number(value) / 100 * v.duration;
  }
}

function setCue(id, index) {
  const d = decks[id];
  const v = d.video;

  if (!v.src) {
    message("Load a track before setting hot cues.");
    return;
  }

  if (d.cues[index] === null) {
    d.cues[index] = v.currentTime;
    message("Saved Cue " + (index + 1) + " on Deck " + id);
  } else {
    v.currentTime = d.cues[index];
    message("Jumped to Cue " + (index + 1) + " on Deck " + id);
  }
}

function toggleLoop(id) {
  const d = decks[id];
  const v = d.video;

  if (!v.src) {
    message("Load a track before creating a loop.");
    return;
  }

  if (d.loopIn === null) {
    d.loopIn = v.currentTime;
    d.loopOut = null;
    message("Loop IN set on Deck " + id + ". Press again to set OUT.");
  } else if (d.loopOut === null) {
    if (v.currentTime <= d.loopIn) {
      message("Move forward in the track before setting Loop OUT.");
      return;
    }

    d.loopOut = v.currentTime;
    message("Loop active on Deck " + id);
  } else {
    d.loopIn = null;
    d.loopOut = null;
    message("Loop disabled on Deck " + id);
  }
}

function updateMixer() {
  const cross =
    Number(document.getElementById("crossfader").value) / 100;

  const master =
    Number(document.getElementById("master").value);

  const volumeA =
    Number(document.getElementById("volumeA").value);

  const volumeB =
    Number(document.getElementById("volumeB").value);

  // Equal-power crossfader.
  decks.A.video.volume =
    Math.cos(cross * Math.PI / 2) * volumeA * master;

  decks.B.video.volume =
    Math.sin(cross * Math.PI / 2) * volumeB * master;
}

function toggleVideoFullscreen() {
  const a = decks.A.video;
  const b = decks.B.video;

  const target = !a.paused ? a : b;

  if (!target.src) {
    message("Load a video on either deck first.");
    return;
  }

  if (target.requestFullscreen) {
    target.requestFullscreen().catch(() => {
      message("Use your browser's video fullscreen control.");
    });
  } else if (target.webkitEnterFullscreen) {
    target.webkitEnterFullscreen();
  } else {
    message("Fullscreen is not supported in this browser.");
  }
}

updateMixer();
</script>

</body>
</html>
Chronixx DJ pro - professional DJ and Video mixing App
