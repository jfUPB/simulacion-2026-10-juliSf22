# Unidad 6

## Bitácora de proceso de aprendizaje
### actividad 1

Obra 1

Decisiones visuales:
La composición llena el lienzo pero mantiene márgenes definidos, como si estuviera enmarcada. La densidad varía mucho: hay zonas con muchas líneas finas y otras más despejadas con formas gruesas. El movimiento sigue curvas suaves y orgánicas que, en conjunto, generan estructuras más complejas como remolinos. El color se basa en paletas cuidadosamente elegidas, generalmente tonos cálidos con algunos acentos vivos, sobre fondos tipo papel en lugar de negro. El ritmo surge de la variación en longitud y grosor de las líneas: se repite la dirección general, pero los cambios evitan que se vuelva monótono.

¿Por qué funciona?
Fidenza destaca porque rompe con la perfección digital y parece hecha a mano. La restricción de que las líneas no se crucen genera tensión visual, como si las formas compitieran por el espacio, dando sensación de peso a lo digital.

Hipótesis del sistema:
Se basa en un Flow Field estático creado con ruido de Perlin de baja frecuencia, lo que produce curvas amplias. Muchos agentes recorren este campo dibujando líneas, pero se detienen si van a chocar con otras (evitan colisiones). Cada agente tiene características aleatorias como grosor, color y longitud, lo que introduce variedad en el resultado.

### actividad 2

¿Qué es un agente autónomo?
Es una entidad computacional con estado propio que percibe su entorno y toma decisiones para cumplir un objetivo. A diferencia de una partícula que solo sigue reglas físicas, un agente actúa con “intención”: sabe dónde está, evalúa lo que lo rodea (objetivos, obstáculos u otros agentes) y decide hacia dónde moverse, limitado por su velocidad y capacidad de giro.

¿Qué es una steering force (fuerza de dirección)?
Es el cálculo matemático que traduce esa intención en movimiento. En vez de ir directamente al objetivo, el agente ajusta su trayectoria comparando su estado actual con el deseado:
Fuerza = Velocidad deseada − Velocidad actual
Es básicamente una corrección que lo empuja a alinearse con su meta.

Comparación: steering force vs. fuerzas externas
Las fuerzas externas (como gravedad o viento) pertenecen al entorno: son pasivas y afectan al objeto sin que este decida. En cambio, las steering forces nacen dentro del agente: son activas y dependen de su percepción. Es la diferencia entre una roca que cae y un pájaro que ajusta su vuelo para llegar a un punto.

¿Por qué esto es útil visualmente?
Porque permite crear comportamientos emergentes y orgánicos. En lugar de animar todo manualmente o usar azar sin control, se diseñan “personalidades” (huir, agruparse, evitar choques). Con eso, muchos agentes generan movimientos complejos, fluidos y naturales sin intervención directa: en vez de dibujar formas, se diseña el comportamiento que las produce.

### actividad 3

Arquitectura del sistema
El campo de flujo se construye como una cuadrícula que cubre el lienzo, donde cada celda guarda un vector con una dirección. Estas direcciones suelen generarse con ruido de Perlin para que cambien de forma suave entre celdas. Cada vector representa la “velocidad deseada” en ese punto, como si fuera la corriente de un río.
El agente usa su posición para ubicar en qué celda está (dividiendo sus coordenadas según la resolución) y toma ese vector como referencia. Luego aplica la regla:
Fuerza = Velocidad deseada − Velocidad actual,
lo que curva su movimiento para alinearse con el flujo.

Parámetros críticos
La resolución define el nivel de detalle: baja resolución produce movimientos bruscos, alta resolución genera fluidez.
La velocidad máxima limita qué tan rápido se mueve el agente.
La fuerza máxima define su “personalidad”: valores altos hacen que siga el flujo de forma inmediata, mientras que valores bajos lo vuelven más pesado y con curvas amplias.
La cantidad de agentes controla la densidad visual: pocos muestran trayectorias individuales, muchos crean texturas colectivas.

Análisis perceptual y musical
Este sistema genera movimientos continuos, suaves y orgánicos, similares al humo o al agua. Visualmente transmite calma e inevitabilidad, aunque con cambios más extremos puede sugerir caos o turbulencia.
Funciona mejor con música ambiental o de evolución lenta (como ambient, post-rock o piezas orquestales suaves), ya que no tiene ritmo marcado sino un flujo constante que acompaña bien cambios progresivos de intensidad.

## Bitácora de aplicación 

### 1. Concepto visual

quiero mostrar una electrocardiograma que suba con las frecuencias bajas, y pueda cambiar de color

#### 2. Relación con el tema musical

quiero mostrar el bajo, el intrumento que no se "escucha" ese es el que quiero que se vea, entonces quiero que tenga como una especie de forma como el electrocardiograma para mostrar que es una de las partes fundamentales del las canciones entonces lo relaciono como el corazon.

#### 3. Pantalla completa

para que no hayan distracciones inecesarias y te centres en lo que se quiere mostrar

#### 4. Interacción performativa e Interacción con sentido musical

cambie el color con una tecla y que cuando preciones (1,2,3) se cambien de "cancion" en verdad son la misma pero una sin bajo otra normal de estudio y una version en vivo

#### moodboard

<img width="318" height="158" alt="image" src="https://github.com/user-attachments/assets/675c6cd2-757e-42e1-98a8-167d4f29a503" />
<img width="337" height="280" alt="image" src="https://github.com/user-attachments/assets/661929cd-fdd1-4db9-904e-92cf791bed90" />
<img width="1200" height="675" alt="image" src="https://github.com/user-attachments/assets/58d4e17b-ff39-4dca-9c35-fee5c872eb09" />

#### boceto
<img width="1011" height="229" alt="image" src="https://github.com/user-attachments/assets/0c0cb98b-deef-4cc4-891b-7d1669ae7a2a" />
<img width="423" height="329" alt="image" src="https://github.com/user-attachments/assets/dbaf718c-666d-4423-a74b-8e7782854b3b" />



#### mapa de deciciones

- electrocardiograma para mostrar que es una de las partes fundamentales del las canciones entonces lo relaciono como el corazon.

- la c para cambiar de color dependiendo de picos y pues con una tecla

- los numeros para cambiara de cancion/version para mostrar los diferentes bajos y pues puedan tambien sentirlo


#### Uso justificado del algoritmo

Usé **flow fields** mediante ruido Perlin para generar pequeñas variaciones en la posición de la línea y en el movimiento de partículas, este campo se modula con el bajo (60–160 Hz), haciendo que el movimiento sea más intenso cuando hay energía grave, para no perder la sincronización con la música o pues que se vea nomá porque xi.

#### Uso explícito de IA como materializador

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

// control cambio automático
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

  //  DETECTAR ALTURA REAL
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
