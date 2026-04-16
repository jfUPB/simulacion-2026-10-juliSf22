# Unidad 6

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### 1. Concepto visual

quiero mostrar una electrocardiograma que suba con las frecuencias bajas, y pueda cambiar de color

### 2. Relación con el tema musical

quiero mostrar el bajo, el intrumento que no se "escucha" ese es el que quiero que se vea, entonces quiero que tenga como una especie de forma como el electrocardiograma para mostrar que es una de las partes fundamentales del las canciones entonces lo relaciono como el corazon.

### 3. Pantalla completa

para que no hayan distracciones inecesarias y te centres en lo que se quiere mostrar

### 4. Interacción performativa e Interacción con sentido musical

cambie el color con una tecla y que cuando preciones (1,2,3) se cambien de "cancion" en verdad son la misma pero una sin bajo otra normal de estudio y una version en vivo

#### moodboard

<img width="318" height="158" alt="image" src="https://github.com/user-attachments/assets/675c6cd2-757e-42e1-98a8-167d4f29a503" />
<img width="337" height="280" alt="image" src="https://github.com/user-attachments/assets/661929cd-fdd1-4db9-904e-92cf791bed90" />
<img width="1200" height="675" alt="image" src="https://github.com/user-attachments/assets/58d4e17b-ff39-4dca-9c35-fee5c872eb09" />

### boceto
<img width="1011" height="229" alt="image" src="https://github.com/user-attachments/assets/0c0cb98b-deef-4cc4-891b-7d1669ae7a2a" />
<img width="423" height="329" alt="image" src="https://github.com/user-attachments/assets/dbaf718c-666d-4423-a74b-8e7782854b3b" />



### mapa de deciciones

- electrocardiograma para mostrar que es una de las partes fundamentales del las canciones entonces lo relaciono como el corazon.

- la c para cambiar de color dependiendo de picos y pues con una tecla

- los numeros para cambiara de cancion/version para mostrar los diferentes bajos y pues puedan tambien sentirlo


### Uso justificado del algoritmo

Usé **flow fields** mediante ruido Perlin para generar pequeñas variaciones en la posición de la línea y en el movimiento de partículas, este campo se modula con el bajo (60–160 Hz), haciendo que el movimiento sea más intenso cuando hay energía grave, para no perder la sincronización con la música o pues que se vea nomá porque xi.

### Uso explícito de IA como materializador

basicamente fue usada para codificar y arreglar errores, porque toda la idea fue meramente mia nada de lo creativo/performativo salió de la ia

````js
let song, fft; 
let songs = [];
let currentSong = 0;

let waveform = [];
let yValues = [];

let palettes = [
  ["#00f5d4", "#0bbcd6", "#2ec4b6"],
  ["#ff006e", "#fb5607", "#ffbe0b"],
  ["#8338ec", "#3a86ff", "#4361ee"]
];
let currentPalette = 0;

let xPos = 0;
let speed = 4; 

let smoothBass = 0;

// flow
let noiseOffset = 0;

// partículas
let particles = [];

// 🔥 control cambio automático
let cooldown = 0;

function preload() {
  soundFormats('mp3', 'wav');
  songs[0] = loadSound('disciple.mp3');
  songs[1] = loadSound('disciple_nobass.mp3'); 
  songs[2] = loadSound('envivo.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  
  fft = new p5.FFT(0.8, 1024); 
  song = songs[currentSong];
  song.loop();

  for (let i = 0; i < width; i++) {
    yValues[i] = height / 2;
  }
}

function draw() {
  background(0);

  fft.analyze();
  waveform = fft.waveform();

  let baselineY = height / 2;
  let maxAmplitude = height * 0.4;

  // bajo
  let bassEnergy = fft.getEnergy(60, 160);
  smoothBass = lerp(smoothBass, bassEnergy, 0.35);

  let threshold = 110;
  let activation = constrain(map(smoothBass, threshold, 255, 0, 1), 0, 1);
  activation = pow(activation, 0.7);

  // punto línea
  let index = floor(map(xPos, 0, width, 0, waveform.length - 1));
  let waveValue = waveform[index];

  let currentY = baselineY;
  if (activation > 0) {
    currentY = baselineY + waveValue * maxAmplitude * activation;
  }

  // FLOW
  let noiseScale = 0.005;
  noiseOffset += map(activation, 0, 1, 0.002, 0.02);

  let flow = noise(xPos * noiseScale, noiseOffset);
  let flowStrength = map(activation, 0, 1, 5, 40);
  let flowOffset = map(flow, 0, 1, -flowStrength, flowStrength);

  currentY += flowOffset * 0.25;

  yValues[xPos] = currentY;

  // 🔥 DETECTAR ALTURA REAL
  let amplitudeNow = abs(currentY - baselineY);

  if (amplitudeNow > maxAmplitude * 0.45 && cooldown <= 0) {
    currentPalette = (currentPalette + 1) % palettes.length;
    cooldown = 20; // evita spam
  }

  cooldown--;

  // colita
  for (let i = 0; i < width; i++) {
    if (i !== xPos) {
      yValues[i] = lerp(yValues[i], baselineY, 0.05);
    }
  }

  // dibujar línea
  strokeWeight(3);
  noFill();

  beginShape();
  for (let i = 0; i < width; i++) {
    let amp = abs(yValues[i] - baselineY);

    let p = palettes[currentPalette];
    let lineColor = p[0];
    if (amp > maxAmplitude * 0.6) lineColor = p[1];
    else if (amp > maxAmplitude * 0.2) lineColor = p[2];

    stroke(lineColor);
    vertex(i, yValues[i]);
  }
  endShape();

  // partículas
  let spawnCount = floor(map(activation, 0, 1, 0, 3));
  for (let i = 0; i < spawnCount; i++) {
    particles.push({
      x: xPos,
      y: currentY,
      life: 255
    });
  }

  noStroke();
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];

    let n = noise(p.x * 0.005, p.y * 0.005, noiseOffset);
    let angle = map(n, 0, 1, -PI, PI);

    p.x += cos(angle) * 1.5;
    p.y += sin(angle) * 1.5;

    p.life -= 4;

    fill(255, p.life);
    circle(p.x, p.y, 2);

    if (p.life <= 0) {
      particles.splice(i, 1);
    }
  }

  xPos += speed;
  if (xPos >= width) xPos = 0;
}

function keyPressed() {
  if (key === 'c' || key === 'C') {
    currentPalette = (currentPalette + 1) % palettes.length;
  }
  if (key === '1') switchSong(0);
  if (key === '2') switchSong(1);
  if (key === '3') switchSong(2);
}

function switchSong(index) {
  if (songs[index].isLoaded()) {
    song.stop();
    currentSong = index;
    song = songs[currentSong];
    song.loop();
  }
}

function mousePressed() {
  let fs = fullscreen();
  fullscreen(!fs);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  background(0);

  yValues = [];
  for (let i = 0; i < width; i++) {
    yValues[i] = height / 2;
  }

  xPos = 0;
}
````

[project](https://editor.p5js.org/juliSf22/full/B6QwrGTzb)

<img width="577" height="408" alt="image" src="https://github.com/user-attachments/assets/9de57ce5-f447-40d9-a81f-313ccf38d99d" />
<img width="331" height="193" alt="image" src="https://github.com/user-attachments/assets/6d5fa94d-7fe6-47eb-8ad7-297aff96aa24" />



## Bitácora de reflexión
