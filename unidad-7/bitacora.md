# Unidad 7

## Bitácora de proceso de aprendizaje


#### Actividad 1:

el del tunel:
<img width="329" height="334" alt="image" src="https://github.com/user-attachments/assets/62ff8c76-ff0c-4e6c-bc1b-e9028137a97e" />
me parece muy chevere porque es claro donde está expresando/ mostrando el tunel, no impide que se pueda leer correctamente la palabra pero si hace que digas :o claro, un tunel  


sonrisa:
<img width="336" height="336" alt="image" src="https://github.com/user-attachments/assets/5370ba39-3082-4bb3-a42c-901572984a20" />

esto muestra como claramente podemos persivir en este caso la "l" cambiandola ligeramente para que funja como una sonrisa sin que pierda su caracteristica distintiva

Panama:

<img width="337" height="331" alt="image" src="https://github.com/user-attachments/assets/ae79aedc-4209-4dfa-9fd4-7fba84907e5f" />

este es chidoporque puede pasar desapersivido si no conoces el "contexto" o pues no conoces al pais, pero si si lo conoces sabes perfectamente que representa al canal de panama


##### 3) podri pensar en:

- Ondas
- elastico
- Boom

me interesa el elastico y el boom porque ya estoy pensando que hacer con cada una

#### Actividad 2:
````js

// Importar módulos de Matter.js
let Engine = Matter.Engine;
let World = Matter.World;
let Bodies = Matter.Bodies;

let engine, world;
let ball;
let ground;

function setup() {
  createCanvas(600, 400);

  // Crear motor de física
  engine = Engine.create();
  world = engine.world;

  // Crear un círculo (pelota)
  ball = Bodies.circle(300, 50, 20, {
    restitution: 0.8 // rebote
  });

  // Crear suelo
  ground = Bodies.rectangle(300, 380, 600, 40, {
    isStatic: true
  });

  // Añadir al mundo
  World.add(world, [ball, ground]);
}

function draw() {
  background(220);

  // Actualizar física
  Engine.update(engine);

  // Dibujar pelota
  fill(100, 150, 255);
  ellipse(ball.position.x, ball.position.y, 40);

  // Dibujar suelo
  fill(100);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, 600, 40);
}
````
tipo de comportamiento son varias particulas cayyendo y colicionando hasta acoplarse

## Bitácora de aplicación 

### Palabra elegida.
- al principio queria una palabra diferente pero me convenció cambiarla por la palara imán, ya que tambien tiene una interactividad bastante reconocible e hinerente a la palabra

### Justificación conceptual.
- imán tiene una conotacion de atraccion y repulcion por lo que es lo que se implemento dandole singnificado coherente a la aplicacion

### Análisis de su significado visual y comportamental.
- usando matters usé las fisicas para que las letas individuales de la palabra se atrageran entre sí y formaran la palabra, como se sabe los imanes se atraen, y se repelen entonces para poder formar la palabra imán debes poder unir las letras con los polos correctos, aparte de que la reactividad con la musica emula un poco un capo con pequeñas particulas de hierro o algo parecido

### Moodboard o referencias.

<img width="610" height="343" alt="image" src="https://github.com/user-attachments/assets/40aeff90-0dc5-458f-aded-75a126a46184" />
<img width="500" height="460" alt="image" src="https://github.com/user-attachments/assets/52730d13-ad06-478e-82f3-9d96c7545996" />
<img width="241" height="209" alt="image" src="https://github.com/user-attachments/assets/2a4f1103-7a0f-4c81-9a97-94ca7cdd0407" />
<img width="289" height="174" alt="image" src="https://github.com/user-attachments/assets/ba2cfff7-5991-4545-888f-f0f8747d575f" />



### Bocetos.

<img width="640" height="401" alt="image" src="https://github.com/user-attachments/assets/9707be15-306c-45fc-9a83-b409db657859" />

<img width="728" height="427" alt="image" src="https://github.com/user-attachments/assets/9f363155-93d9-483c-8ba0-ccb6715a933a" />

### Mapa de decisiones.

la tipografia es sobria nada fuera de lo normal, las fisicas aquí son importantes porque no queria que se unieran y quedara "flojo" queria que se unieran de verdad ose aque se movieran como una sola identidad y no como una que arrastra a a otra, para el fondo donde están las particulas usé los flowfild que vimos en la unidad pasada porque es algo que le sienta bien ya que medio puede emular lo que queria, el mouse actua como una "mano" moviendo los imanes y viendo como se van pegando unos con otros hasta que quede escrita la palabra, la musica que elegí es tranquila calmada porque quería que se notara los pequeños "golpes de las notas "individuales" sin necesidad de tanto ruido o relleno de musica.

### Mapa de interpretación.

mi interpretacioin va a comenzar mostrando que el fondo, osea las particulas se comportan cuando los imanes están separados, y luego intentar juntar letras que pues no van juntas para que se vea que se están repeliendo, para luego ir juntando las letra que si van juntas para que se forme la palabra "imán" tambien poner el click derecho y mostrar la funcionalidad de que las letras que se juntan ahora se repelen tambien pero que cuando le vueovas a dar ya si fucniona correctamente, para al final mover la palabra un poco por el canvas.

### Explicación de la relación entre audio y comportamiento.

con el ritmo de la musica las particulas se mueven un poco más rapido o más lento aparte de que brillan un poco tambien

````js
// ──────────────────────────────────────────────────────────────────────────────
//  i · m · á · n  –  Audio-reactive flow field · Plop snap · Polarity toggle
//  v3 – Dual-layer particles: slow dust + fast sparks, stronger music reactivity
// ──────────────────────────────────────────────────────────────────────────────

const { Engine, Bodies, Body, World, Mouse, MouseConstraint, Events } = Matter;

// ── Constants (original) ─────────────────────────────────────────────────────
const WORD      = ['i','m','á','n'];
const RADIUS    = 38;
const FONT_SZ   = 90;
const SNAP_DIST = RADIUS * 2.05;
const INFLUENCE = 280;
const ATTRACT_S = 0.007;
const REPEL_S   = 0.016;

const PALETTE = [
  [210, 90,  255],
  [45,  195, 255],
  [255, 190, 35 ],
  [65,  255, 145],
];

// ── Matter.js state ───────────────────────────────────────────────────────────
let engine, world, mCons;
let letters = [];
let groups  = new Map();

// ── Audio state ───────────────────────────────────────────────────────────────
let song, plop;
let fftAnalyzer, ampAnalyzer;
let audioReady       = false;
let polarityInverted = false;

// ── Flow-field + particle state ───────────────────────────────────────────────
//  Two layers share a single array for one iteration pass per frame:
//    · "dust"  (spark=false) — 320 larger, slower, softer particles
//    · "spark" (spark=true)  — 200 smaller, brighter, more audio-reactive
//  Total 520 particles — dense enough to read the music clearly.
const NUM_DUST   = 320;
const NUM_SPARKS = 200;
const NUM_PARTICLES = NUM_DUST + NUM_SPARKS;

const FLOW_COLS = 30;
const FLOW_ROWS = 22;
let particles   = [];
let flowField   = [];
let flowTime    = 0;

// ── Polarity flash overlay ────────────────────────────────────────────────────
let flashAlpha = 0;

// ── Letter influence radii ────────────────────────────────────────────────────
const SOLO_ATTRACT_R    = 170;
const GROUP_INFLUENCE_R = 220;

// ─────────────────────────────────────────────────────────────────────────────
function isAdjacent(a, b) { return Math.abs(a - b) === 1; }

// ═════════════════════════════════════════════════════════════════════════════
new p5(function (s) {

  // ── Preload ────────────────────────────────────────────────────────────────
  s.preload = function () {
    song = s.loadSound('song.mp3');
    plop = s.loadSound('plop.mp3');
  };

  // ── Setup ──────────────────────────────────────────────────────────────────
  s.setup = function () {
    const cnv = s.createCanvas(s.windowWidth, s.windowHeight);

    cnv.elt.addEventListener('dblclick', resetAll);

    cnv.elt.addEventListener('contextmenu', (e) => {
      e.preventDefault();
      polarityInverted = !polarityInverted;
      flashAlpha = 180;
    });

    const startAudio = () => {
      if (audioReady) return;
      s.userStartAudio().then(() => {
        if (song && song.isLoaded() && !song.isPlaying()) song.loop();
        audioReady = true;
      }).catch(() => {});
    };
    document.addEventListener('click', startAudio);

    const req = () => {
      if (document.documentElement.requestFullscreen)
        document.documentElement.requestFullscreen().catch(() => {});
    };
    req();
    document.addEventListener('click', req, { once: true });

    s.textFont('Georgia');

    engine = Engine.create({ gravity: { y: 0.9 } });
    world  = engine.world;

    const T = 60;
    World.add(world, [
      Bodies.rectangle(s.width / 2,     s.height + T / 2,  s.width * 3,  T, { isStatic: true }),
      Bodies.rectangle(-T / 2,          s.height / 2,       T, s.height * 3, { isStatic: true }),
      Bodies.rectangle(s.width + T / 2, s.height / 2,       T, s.height * 3, { isStatic: true }),
    ]);

    spawnLetters();
    initParticles();

    const mm = Mouse.create(cnv.elt);
    mm.pixelRatio = s.pixelDensity();

    mCons = MouseConstraint.create(engine, {
      mouse: mm,
      constraint: { stiffness: 0.4, damping: 0.1 },
    });
    World.add(world, mCons);

    Events.on(mCons, 'enddrag', (ev) => {
      const body = ev.body;
      if (!body) return;
      const li = letters.findIndex(l => l.body === body);
      if (li < 0) return;
      const leaderId = getLeader(li);
      if (groups.has(leaderId)) {
        const g = groups.get(leaderId);
        if (g.length > 1)
          for (const id of g) Body.set(letters[id].body, 'ignoreGravity', true);
      }
    });

    fftAnalyzer = new p5.FFT(0.85, 64);
    ampAnalyzer = new p5.Amplitude(0.9);
  };

  // ── Draw ───────────────────────────────────────────────────────────────────
  s.draw = function () {
    s.background(5, 5, 15);
    Engine.update(engine, 1000 / 60);

    const spectrum = fftAnalyzer.analyze();
    const amp      = ampAnalyzer.getLevel();

    updateFlowField(spectrum, amp);
    updateAndDrawParticles(amp, spectrum);

    if (flashAlpha > 0) {
      const col = polarityInverted ? [255, 60, 60] : [60, 160, 255];
      s.noStroke();
      s.fill(col[0], col[1], col[2], flashAlpha);
      s.rect(0, 0, s.width, s.height);
      flashAlpha = Math.max(0, flashAlpha - 14);
    }

    applyMagneticForces();
    if (!polarityInverted) applySnap();
    propagateGroupMovement();

    for (const l of letters) drawLetter(l);
  };

  s.windowResized = function () {
    s.resizeCanvas(s.windowWidth, s.windowHeight);
    initParticles();
  };

  // ── Particle init ──────────────────────────────────────────────────────────
  function initParticles() {
    particles = [];

    // Slow dust — spread uniformly across the canvas
    for (let i = 0; i < NUM_DUST; i++) {
      particles.push({
        x:     s.random(s.width),
        y:     s.random(s.height),
        vx:    0, vy: 0,
        col:   PALETTE[Math.floor(s.random(PALETTE.length))],
        age:   s.random(1000),
        spark: false,
      });
    }

    // Fast sparks — start more centrally so they're inside the action
    for (let i = 0; i < NUM_SPARKS; i++) {
      particles.push({
        x:     s.random(s.width  * 0.1, s.width  * 0.9),
        y:     s.random(s.height * 0.1, s.height * 0.9),
        vx:    0, vy: 0,
        col:   PALETTE[Math.floor(s.random(PALETTE.length))],
        age:   s.random(1000),
        spark: true,
      });
    }
  }

  // ── Flow-field update ──────────────────────────────────────────────────────
  function updateFlowField(spectrum, amp) {
    flowTime += 0.0018 + amp * 0.014;

    flowField = [];
    for (let row = 0; row < FLOW_ROWS; row++) {
      for (let col = 0; col < FLOW_COLS; col++) {
        const nx = col / FLOW_COLS;
        const ny = row / FLOW_ROWS;

        const specIdx = Math.floor(nx * spectrum.length * 0.65);
        const specVal = spectrum[specIdx] / 255;

        const noiseAng = s.noise(nx * 2.8, ny * 2.8, flowTime) * s.TWO_PI * 2;
        const audioAng = specVal * s.PI * (polarityInverted ? -1.6 : 1.6);

        flowField.push({
          angle:    noiseAng + audioAng,
          strength: 0.35 + specVal * 1.9,
          specVal,                           // local frequency energy (0–1)
        });
      }
    }
  }

  // ── Particle update + draw (single pass) ───────────────────────────────────
  function updateAndDrawParticles(amp, spectrum) {
    s.noStroke();

    const letterInfo = buildLetterInfo();

    // Bass energy (low-freq bins) drives a global kick felt by sparks
    let bassEnergy = 0;
    for (let b = 0; b < 5; b++) bassEnergy += spectrum[b] / 255;
    bassEnergy /= 5;

    for (const p of particles) {

      // ── 1. Flow-field force ──────────────────────────────────────────────
      const gCol = Math.floor((p.x / s.width)  * FLOW_COLS);
      const gRow = Math.floor((p.y / s.height) * FLOW_ROWS);
      const idx  = Math.max(0, Math.min(flowField.length - 1, gRow * FLOW_COLS + gCol));
      const { angle, strength, specVal } = flowField[idx];

      // Sparks respond ~2× harder to the flow than dust
      const reactMult = p.spark ? 1.9 : 1.0;
      const spd0      = (0.5 + amp * 3.8) * strength * reactMult;

      p.vx += Math.cos(angle) * spd0 * 0.1;
      p.vy += Math.sin(angle) * spd0 * 0.1;

      // Sparks: extra random kick on loud bass transients
      if (p.spark && bassEnergy > 0.5) {
        const kick = (bassEnergy - 0.5) * 4.0;
        p.vx += (Math.random() - 0.5) * kick;
        p.vy += (Math.random() - 0.5) * kick;
      }

      // ── 2. Letter magnetic influence ─────────────────────────────────────
      applyLetterInfluence(p, letterInfo, amp);

      // ── 3. Speed clamp + damping ──────────────────────────────────────────
      const spd    = Math.hypot(p.vx, p.vy);
      const maxSpd = p.spark ? 3.4 + amp * 7.0 : 2.4 + amp * 5.5;
      if (spd > maxSpd) { p.vx *= maxSpd / spd; p.vy *= maxSpd / spd; }

      p.vx *= p.spark ? 0.94 : 0.91;
      p.vy *= p.spark ? 0.94 : 0.91;
      p.x  += p.vx;
      p.y  += p.vy;

      // ── 4. Wrap edges ─────────────────────────────────────────────────────
      if (p.x < 0)         p.x = s.width;
      if (p.x > s.width)   p.x = 0;
      if (p.y < 0)         p.y = s.height;
      if (p.y > s.height)  p.y = 0;
      p.age++;

      // ── 5. Proximity bonus (brighter near any letter) ─────────────────────
      const [r, g, b] = p.col;
      let proxBonus = 0;
      for (const info of letterInfo) {
        const dd = Math.hypot(info.x - p.x, info.y - p.y);
        proxBonus += Math.max(0, 1 - dd / 130) * 0.65;
      }
      proxBonus = Math.min(proxBonus, 1.0);

      // ── 6. Draw ───────────────────────────────────────────────────────────
      if (p.spark) {
        // Small, intense, reacts strongly to local frequency energy
        const alpha = Math.min(85 + amp * 165 + proxBonus * 105 + specVal * 80, 245);
        const sz    = (1.1 + amp * 2.6 + specVal * 2.2) * (1 + proxBonus * 0.8);
        s.drawingContext.shadowBlur  = 7 + amp * 22 + proxBonus * 22 + specVal * 14;
        s.drawingContext.shadowColor = `rgba(${r},${g},${b},${0.5 + proxBonus * 0.45})`;
        s.fill(r, g, b, alpha);
        s.ellipse(p.x, p.y, sz, sz);

      } else {
        // Larger, steadier — carries the visible shape of the field
        const alpha = Math.min(58 + amp * 115 + proxBonus * 95 + specVal * 55, 225);
        const sz    = (2.6 + amp * 3.8 + specVal * 1.8) * (1 + proxBonus * 0.8);
        s.drawingContext.shadowBlur  = 5 + amp * 15 + proxBonus * 16;
        s.drawingContext.shadowColor = `rgba(${r},${g},${b},${0.28 + proxBonus * 0.38})`;
        s.fill(r, g, b, alpha);
        s.ellipse(p.x, p.y, sz, sz);
      }
    }

    s.drawingContext.shadowBlur = 0;
  }

  // ── Letter info snapshot ───────────────────────────────────────────────────
  function buildLetterInfo() {
    const info = [];
    for (let i = 0; i < letters.length; i++) {
      const l         = letters[i];
      const leaderId  = getLeader(i);
      const grp       = groups.get(leaderId) || [leaderId];
      const [r, g, b] = l.col;
      info.push({
        x: l.body.position.x, y: l.body.position.y,
        groupSize: grp.length,
        r, g, b,
      });
    }
    return info;
  }

  // ── Magnetic influence on a single particle ───────────────────────────────
  function applyLetterInfluence(p, letterInfo, amp) {
    for (const info of letterInfo) {
      const dx   = info.x - p.x;
      const dy   = info.y - p.y;
      const dist = Math.hypot(dx, dy);
      if (dist < 4) continue;

      const nx = dx / dist;
      const ny = dy / dist;

      if (info.groupSize === 1) {
        if (dist > SOLO_ATTRACT_R) continue;
        const t = 1 - dist / SOLO_ATTRACT_R;
        const f = (0.22 + amp * 0.18) * t * t;
        p.vx += nx * f;
        p.vy += ny * f;

      } else {
        if (dist > GROUP_INFLUENCE_R) continue;
        const t    = 1 - dist / GROUP_INFLUENCE_R;
        const sign = info.groupSize % 2 === 0 ? 1 : -1;
        const tx   = -ny * sign;
        const ty   =  nx * sign;
        p.vx += tx * (0.14 + amp * 0.12) * t * t - nx * (0.06 + amp * 0.04) * t;
        p.vy += ty * (0.14 + amp * 0.12) * t * t - ny * (0.06 + amp * 0.04) * t;
      }
    }
  }

  // ── Physics helpers (IDENTICAL to original) ───────────────────────────────

  function spawnLetters() {
    letters = [];
    groups  = new Map();
    for (let i = 0; i < WORD.length; i++) {
      const body = Bodies.circle(
        s.random(140, s.width - 140),
        s.random(-700, -80) - i * 140,
        RADIUS,
        { restitution: 0.15, friction: 0.05, frictionAir: 0.04, density: 0.003 }
      );
      World.add(world, body);
      letters.push({ body, char: WORD[i], idx: i, col: PALETTE[i], leader: -1, offsetX: 0, offsetY: 0 });
      groups.set(i, [i]);
    }
  }

  function resetAll() {
    for (const l of letters) World.remove(world, l.body);
    spawnLetters();
  }

  function applyMagneticForces() {
    for (let i = 0; i < letters.length; i++) {
      for (let j = i + 1; j < letters.length; j++) {
        if (getLeader(i) === getLeader(j)) continue;
        const a = letters[i], b = letters[j];
        const dx = b.body.position.x - a.body.position.x;
        const dy = b.body.position.y - a.body.position.y;
        const dist = Math.hypot(dx, dy);
        if (dist < 1) continue;
        const nx = dx / dist, ny = dy / dist;
        if (isAdjacent(a.idx, b.idx)) {
          const t    = Math.max(0, Math.min(1, (SNAP_DIST * 1.8 - dist) / (SNAP_DIST * 1.8)));
          const f    = ATTRACT_S * Math.pow(t, 3);
          const sign = polarityInverted ? -1 : 1;
          applyToGroup(i,  sign * nx * f,  sign * ny * f);
          applyToGroup(j, -sign * nx * f, -sign * ny * f);
        } else if (dist < INFLUENCE) {
          const t    = Math.max(0, Math.min(1, (INFLUENCE - dist) / INFLUENCE));
          const f    = REPEL_S * t * t;
          const sign = polarityInverted ? -1 : 1;
          applyToGroup(i, -sign * nx * f, -sign * ny * f);
          applyToGroup(j,  sign * nx * f,  sign * ny * f);
        }
      }
    }
  }

  function applyToGroup(id, fx, fy) {
    const leaderId = getLeader(id);
    const leader   = letters[leaderId];
    if (leader.body.isStatic) return;
    Body.applyForce(leader.body, leader.body.position, { x: fx, y: fy });
  }

  function applySnap() {
    for (let i = 0; i < letters.length; i++) {
      for (let j = i + 1; j < letters.length; j++) {
        if (!isAdjacent(letters[i].idx, letters[j].idx)) continue;
        const li = getLeader(i), lj = getLeader(j);
        if (li === lj) continue;
        const dist = Math.hypot(
          letters[j].body.position.x - letters[i].body.position.x,
          letters[j].body.position.y - letters[i].body.position.y
        );
        if (dist < SNAP_DIST) mergeGroups(i, j);
      }
    }
  }

  function mergeGroups(idA, idB) {
    const la = getLeader(idA), lb = getLeader(idB);
    const newLeader = letters[la].idx < letters[lb].idx ? la : lb;
    const absorbed  = newLeader === la ? lb : la;
    const absorbedMembers = groups.get(absorbed)  || [absorbed];
    const leaderMembers   = groups.get(newLeader) || [newLeader];

    for (const mid of absorbedMembers) {
      const slotX = (letters[mid].idx - letters[newLeader].idx) * RADIUS * 2.0;
      letters[mid].leader = newLeader; letters[mid].offsetX = slotX; letters[mid].offsetY = 0;
      Body.setStatic(letters[mid].body, true);
    }
    for (const mid of leaderMembers) {
      if (mid === newLeader) {
        letters[mid].leader = -1; letters[mid].offsetX = 0; letters[mid].offsetY = 0;
      } else {
        letters[mid].offsetX = (letters[mid].idx - letters[newLeader].idx) * RADIUS * 2.0;
        letters[mid].offsetY = 0;
      }
    }

    const newMembers = [...leaderMembers, ...absorbedMembers];
    groups.set(newLeader, newMembers);
    groups.delete(absorbed);
    Body.set(letters[newLeader].body, 'ignoreGravity', newMembers.length > 1);
    snapPositions(newLeader);

    if (plop && plop.isLoaded()) { plop.rate(s.random(0.82, 1.18)); plop.play(); }
  }

  function propagateGroupMovement() {
    for (const [leaderId, members] of groups.entries()) {
      if (members.length <= 1) continue;
      snapPositions(leaderId);
    }
  }

  function snapPositions(leaderId) {
    const leader = letters[leaderId];
    const lp = leader.body.position, la = leader.body.angle;
    for (const mid of groups.get(leaderId)) {
      if (mid === leaderId) continue;
      const m = letters[mid];
      Body.setPosition(m.body, { x: lp.x + m.offsetX * Math.cos(la), y: lp.y + m.offsetX * Math.sin(la) });
      Body.setAngle(m.body, la);
      Body.setVelocity(m.body, { x: 0, y: 0 });
    }
  }

  function getLeader(id) {
    let cur = id, limit = 10;
    while (letters[cur].leader !== -1 && limit-- > 0) cur = letters[cur].leader;
    return cur;
  }

  // ── Letter renderer (IDENTICAL to original) ───────────────────────────────
  function drawLetter(l) {
    const pos = l.body.position, ang = l.body.angle;
    const [r, g, b] = l.col;
    s.push();
    s.translate(pos.x, pos.y);
    s.rotate(ang);
    s.textAlign(s.CENTER, s.CENTER);
    s.textSize(FONT_SZ);
    s.drawingContext.shadowBlur  = 38;
    s.drawingContext.shadowColor = `rgba(${r},${g},${b},0.85)`;
    s.fill(r, g, b, 210);
    s.text(l.char, 0, 0);
    s.fill(255, 255, 255, 240);
    s.text(l.char, 0, 0);
    s.pop();
  }

});
````
[app](https://editor.p5js.org/juliSf22/full/6ap33djkL)


## Bitácora de reflexión
