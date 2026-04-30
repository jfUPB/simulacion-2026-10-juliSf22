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
// ─────────────────────────────────────────────────────────────────────────────
//  i · m · á · n  —  sketch.js
//  Partículas de campo magnético + letras con Matter.js
//
//  · Click             → iniciar audio
//  · Arrastrar         → mover letras
//  · Doble-click       → reiniciar
//  · Click derecho     → activar / desactivar imán (une / separa la palabra)
//
//  Comportamiento de partículas:
//  · Letras separadas  → flujo de ruido + atracción a cada letra individual
//  · Palabra completa  → las partículas toman la forma de LIMADURAS DE HIERRO
//                        (líneas cortas alineadas con el campo dipolar)
//                        La música las hace brillar, no las desorganiza.
// ─────────────────────────────────────────────────────────────────────────────

const { Engine, Bodies, Body, World, Mouse, MouseConstraint, Events } = Matter;

// ── Constantes de letras ──────────────────────────────────────────────────────
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

// ── Estado de Matter.js ───────────────────────────────────────────────────────
let engine, world, mCons;
let letters = [];
let groups  = new Map();

// ── Audio ─────────────────────────────────────────────────────────────────────
let song, plop;
let fftAnalyzer, ampAnalyzer;
let audioReady    = false;

// ── Imán ──────────────────────────────────────────────────────────────────────
let magnetEnabled = true;

// ── Partículas ────────────────────────────────────────────────────────────────
const NUM_PARTICLES = 560;
let particles = [];
let flowTime  = 0;

// ── Transición suave entre modos ──────────────────────────────────────────────
// fieldBlend: 0 = modo flujo, 1 = modo limadura
let fieldBlend = 0;

// ─────────────────────────────────────────────────────────────────────────────
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
      toggleMagnet();
    });

    const startAudio = () => {
      if (audioReady) return;
      s.userStartAudio().then(() => {
        if (song && song.isLoaded() && !song.isPlaying()) song.loop();
        audioReady = true;
      }).catch(() => {});
    };
    document.addEventListener('click', startAudio);

    // Intentar fullscreen
    const req = () => {
      if (document.documentElement.requestFullscreen)
        document.documentElement.requestFullscreen().catch(() => {});
    };
    document.addEventListener('click', req, { once: true });

    s.textFont('Georgia');

    engine = Engine.create({ gravity: { y: 0.9 } });
    world  = engine.world;

    const T = 60;
    World.add(world, [
      Bodies.rectangle(s.width / 2,     s.height + T / 2, s.width * 3,  T,          { isStatic: true }),
      Bodies.rectangle(-T / 2,           s.height / 2,     T, s.height * 3,           { isStatic: true }),
      Bodies.rectangle(s.width + T / 2,  s.height / 2,     T, s.height * 3,           { isStatic: true }),
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
    flowTime += 0.0016 + amp * 0.005;

    // Actualizar blend suavemente
    const wordComplete = isWordComplete();
    const targetBlend  = wordComplete ? 1 : 0;
    fieldBlend += (targetBlend - fieldBlend) * 0.035;

    updateAndDrawParticles(amp, spectrum, wordComplete);

    if (magnetEnabled) {
      applyMagneticForces();
      applySnap();
    }
    propagateGroupMovement();

    for (const l of letters) drawLetter(l);
  };

  s.windowResized = function () {
    s.resizeCanvas(s.windowWidth, s.windowHeight);
    initParticles();
  };

  // ── Toggle imán ────────────────────────────────────────────────────────────
  function toggleMagnet() {
    magnetEnabled = !magnetEnabled;
    if (!magnetEnabled) splitAllGroups();
  }

  function splitAllGroups() {
    for (let i = 0; i < letters.length; i++) {
      letters[i].leader  = -1;
      letters[i].offsetX = 0;
      letters[i].offsetY = 0;
      Body.setStatic(letters[i].body, false);
      Body.set(letters[i].body, 'ignoreGravity', false);
      groups.set(i, [i]);
      // pequeño impulso al separarse
      Body.setVelocity(letters[i].body, {
        x: (Math.random() - 0.5) * 6,
        y: (Math.random() - 0.5) * 3 - 1,
      });
    }
  }

  // ── ¿Palabra completa? ─────────────────────────────────────────────────────
  function isWordComplete() {
    if (!magnetEnabled) return false;
    const l0 = getLeader(0);
    for (let i = 1; i < letters.length; i++) {
      if (getLeader(i) !== l0) return false;
    }
    const g = groups.get(l0);
    return g && g.length === letters.length;
  }

  function getWordCenter() {
    let cx = 0, cy = 0;
    for (const l of letters) {
      cx += l.body.position.x;
      cy += l.body.position.y;
    }
    return { x: cx / letters.length, y: cy / letters.length };
  }

  // ── Campo dipolar 2D ───────────────────────────────────────────────────────
  // Dipolo horizontal: polo S a la izquierda (letra 'i'), polo N a la derecha ('n')
  // Las líneas de campo forman arcos cerrados de N → S por el exterior.
  function getDipoleField(px, py, cx, cy, halfLen) {
    const eps = 2500; // suavizado cerca de los polos

    // Polo S (izquierda) — campo entra
    const sx   = cx - halfLen, sy = cy;
    const dxs  = px - sx,      dys = py - sy;
    const rs2  = dxs * dxs + dys * dys + eps;
    const rs   = Math.sqrt(rs2);
    const bxs  = -dxs / (rs2 * rs);
    const bys  = -dys / (rs2 * rs);

    // Polo N (derecha) — campo sale
    const nx2  = cx + halfLen, ny2 = cy;
    const dxn  = px - nx2,     dyn = py - ny2;
    const rn2  = dxn * dxn + dyn * dyn + eps;
    const rn   = Math.sqrt(rn2);
    const bxn  =  dxn / (rn2 * rn);
    const byn  =  dyn / (rn2 * rn);

    return { bx: bxn + bxs, by: byn + bys };
  }

  // ── Inicializar partículas ─────────────────────────────────────────────────
  function initParticles() {
    particles = [];
    for (let i = 0; i < NUM_PARTICLES; i++) {
      particles.push({
        x:   s.random(s.width),
        y:   s.random(s.height),
        vx:  0,
        vy:  0,
        col: PALETTE[Math.floor(s.random(PALETTE.length))],
        age: s.random(1000),
      });
    }
  }

  // ── Actualizar y dibujar partículas ───────────────────────────────────────
  function updateAndDrawParticles(amp, spectrum, wordComplete) {
    // Energía de bajos (primeros 5 bins)
    let bassEnergy = 0;
    for (let b = 0; b < 5; b++) bassEnergy += spectrum[b] / 255;
    bassEnergy /= 5;

    let wordCenter, halfLen;
    if (fieldBlend > 0.01) {
      wordCenter = getWordCenter();
      halfLen    = (letters.length - 1) * RADIUS * 1.08;
    }

    for (const p of particles) {

      // ── Fuerza del flujo de ruido (modo normal) ──────────────────────────
      const noiseAng = s.noise(p.x * 0.0026, p.y * 0.0026, flowTime) * s.TWO_PI * 2;
      const specIdx  = Math.min(spectrum.length - 1,
                         Math.floor((p.x / s.width) * spectrum.length * 0.6));
      const specVal  = spectrum[specIdx] / 255;
      const flowSpd  = (0.35 + amp * 1.8 + specVal * 0.5) * (1 - fieldBlend);

      let fxFlow = Math.cos(noiseAng) * flowSpd * 0.12;
      let fyFlow = Math.sin(noiseAng) * flowSpd * 0.12;

      // Atracción a letras individuales (solo en modo flujo)
      if (fieldBlend < 0.95) {
        for (const l of letters) {
          const dx   = l.body.position.x - p.x;
          const dy   = l.body.position.y - p.y;
          const dist = Math.hypot(dx, dy);
          if (dist < 4 || dist > 165) continue;
          const t = (1 - dist / 165) * (1 - fieldBlend);
          fxFlow += (dx / dist) * 0.11 * t * t;
          fyFlow += (dy / dist) * 0.11 * t * t;
        }
      }

      // ── Fuerza del campo dipolar (modo limadura) ──────────────────────────
      let fxField = 0, fyField = 0;
      let fieldAngle = 0, fieldStrength = 0;

      if (fieldBlend > 0.01 && wordCenter) {
        const { bx, by } = getDipoleField(p.x, p.y, wordCenter.x, wordCenter.y, halfLen);
        fieldStrength = Math.hypot(bx, by);
        fieldAngle    = Math.atan2(by, bx);

        const blen   = fieldStrength + 1e-12;
        const fnx    = bx / blen, fny = by / blen;
        // Velocidad de deriva: suave, música solo le da un pequeño impulso
        const driftSpd = (0.45 + amp * 0.55) * fieldBlend;
        fxField = (fnx * driftSpd - p.vx) * 0.07 * fieldBlend;
        fyField = (fny * driftSpd - p.vy) * 0.07 * fieldBlend;

        // Impulso suave de música: existe pero tiende a amortiguarse rápido
        if (bassEnergy > 0.38) {
          const kick = (bassEnergy - 0.38) * amp * 1.1 * fieldBlend;
          fxField += (Math.random() - 0.5) * kick;
          fyField += (Math.random() - 0.5) * kick;
        }
      }

      // ── Integrar ──────────────────────────────────────────────────────────
      p.vx += fxFlow + fxField;
      p.vy += fyFlow + fyField;

      // Bajos en modo flujo
      if (fieldBlend < 0.95 && bassEnergy > 0.42) {
        const kick = (bassEnergy - 0.42) * 2.2;
        p.vx += (Math.random() - 0.5) * kick;
        p.vy += (Math.random() - 0.5) * kick;
      }

      // Clamp de velocidad
      const spd    = Math.hypot(p.vx, p.vy);
      const maxSpd = fieldBlend > 0.5
        ? 1.2 + amp * 1.4
        : 2.0 + amp * 3.8;
      if (spd > maxSpd) { p.vx *= maxSpd / spd; p.vy *= maxSpd / spd; }

      // Amortiguación: más fuerte en modo campo para mantener la forma
      const damp = fieldBlend > 0.5 ? 0.84 : 0.91;
      p.vx *= damp;
      p.vy *= damp;

      p.x  += p.vx;
      p.y  += p.vy;

      // Wrap
      if (p.x < 0)        p.x = s.width;
      if (p.x > s.width)  p.x = 0;
      if (p.y < 0)        p.y = s.height;
      if (p.y > s.height) p.y = 0;
      p.age++;

      // ── Dibujar ───────────────────────────────────────────────────────────
      const [r, g, b] = p.col;

      // Proximidad a cualquier letra (bonus de brillo)
      let proxBonus = 0;
      for (const l of letters) {
        const dd = Math.hypot(l.body.position.x - p.x, l.body.position.y - p.y);
        proxBonus += Math.max(0, 1 - dd / 115) * 0.65;
      }
      proxBonus = Math.min(proxBonus, 1.0);

      // Intensidad del campo local (para brillo de limadura)
      let fg = 0;
      if (fieldBlend > 0.01 && wordCenter) {
        const { bx: bx2, by: by2 } = getDipoleField(p.x, p.y, wordCenter.x, wordCenter.y, halfLen);
        fg = Math.min(Math.hypot(bx2, by2) * 0.55, 1.0);
      }

      if (fieldBlend > 0.05) {
        // ── Modo limadura: línea corta alineada con el campo ──────────────
        // Recalcular ángulo en posición actual
        let drawAngle = fieldAngle;
        if (wordCenter) {
          const { bx: bxD, by: byD } = getDipoleField(p.x, p.y, wordCenter.x, wordCenter.y, halfLen);
          drawAngle = Math.atan2(byD, bxD);
          fg        = Math.min(Math.hypot(bxD, byD) * 0.55, 1.0);
        }

        const alpha  = Math.min(
          55 * (1 - fieldBlend) +
          (70 + amp * 145 + fg * 95 + proxBonus * 80) * fieldBlend,
          240);
        const segLen = (4 + fg * 7 + amp * 3) * fieldBlend + 1.5 * (1 - fieldBlend);
        const ex     = Math.cos(drawAngle) * segLen / 2;
        const ey     = Math.sin(drawAngle) * segLen / 2;

        s.noFill();
        s.strokeWeight((0.7 + amp * 0.7 + fg * 0.5) * fieldBlend + 0.5 * (1 - fieldBlend));
        s.strokeCap(s.ROUND);
        s.stroke(r, g, b, alpha);
        s.drawingContext.shadowBlur  = (3 + amp * 11 + fg * 9 + proxBonus * 10) * fieldBlend;
        s.drawingContext.shadowColor = `rgba(${r},${g},${b},${(0.28 + amp * 0.28 + fg * 0.22) * fieldBlend})`;
        s.line(p.x - ex, p.y - ey, p.x + ex, p.y + ey);

      } else {
        // ── Modo flujo: punto circular ────────────────────────────────────
        const alpha = Math.min(42 + amp * 110 + proxBonus * 85 + specVal * 45, 220);
        const sz    = 1.5 + amp * 2.6 + proxBonus * 1.3;

        s.noStroke();
        s.fill(r, g, b, alpha);
        s.drawingContext.shadowBlur  = 4 + amp * 13 + proxBonus * 15;
        s.drawingContext.shadowColor = `rgba(${r},${g},${b},${0.22 + proxBonus * 0.32})`;
        s.ellipse(p.x, p.y, sz, sz);
      }
    }

    s.drawingContext.shadowBlur = 0;
    s.noStroke();
  }

  // ── Física ─────────────────────────────────────────────────────────────────

  function isAdjacent(a, b) { return Math.abs(a - b) === 1; }

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
      letters.push({
        body,
        char: WORD[i],
        idx:  i,
        col:  PALETTE[i],
        leader:  -1,
        offsetX: 0,
        offsetY: 0,
      });
      groups.set(i, [i]);
    }
  }

  function resetAll() {
    for (const l of letters) World.remove(world, l.body);
    magnetEnabled = true;
    fieldBlend    = 0;
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
          const t = Math.max(0, Math.min(1, (SNAP_DIST * 1.8 - dist) / (SNAP_DIST * 1.8)));
          const f = ATTRACT_S * Math.pow(t, 3);
          applyToGroup(i,  nx * f,  ny * f);
          applyToGroup(j, -nx * f, -ny * f);
        } else if (dist < INFLUENCE) {
          const t = Math.max(0, Math.min(1, (INFLUENCE - dist) / INFLUENCE));
          const f = REPEL_S * t * t;
          applyToGroup(i, -nx * f, -ny * f);
          applyToGroup(j,  nx * f,  ny * f);
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
      letters[mid].leader  = newLeader;
      letters[mid].offsetX = slotX;
      letters[mid].offsetY = 0;
      Body.setStatic(letters[mid].body, true);
    }
    for (const mid of leaderMembers) {
      if (mid === newLeader) {
        letters[mid].leader  = -1;
        letters[mid].offsetX = 0;
        letters[mid].offsetY = 0;
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

    if (plop && plop.isLoaded()) {
      plop.rate(s.random(0.82, 1.18));
      plop.play();
    }
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
      Body.setPosition(m.body, {
        x: lp.x + m.offsetX * Math.cos(la),
        y: lp.y + m.offsetX * Math.sin(la),
      });
      Body.setAngle(m.body, la);
      Body.setVelocity(m.body, { x: 0, y: 0 });
    }
  }

  function getLeader(id) {
    let cur = id, limit = 10;
    while (letters[cur].leader !== -1 && limit-- > 0) cur = letters[cur].leader;
    return cur;
  }

  // ── Dibujar letra (sin cambios respecto al original) ──────────────────────
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
<img width="509" height="376" alt="image" src="https://github.com/user-attachments/assets/1f8decdd-5bc6-45db-813e-cb851301739d" />



<img width="995" height="714" alt="image" src="https://github.com/user-attachments/assets/e780797f-9194-4017-b060-a98960517125" />


## Bitácora de reflexión
