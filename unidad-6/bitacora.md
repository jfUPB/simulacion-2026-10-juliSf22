# Unidad 6

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 
let song, fft;
let songs = [];
let currentSong = 0;

let agents = [];
let flowField = [];
let cols, rows;
let scale = 40;

let zoff = 0;
let lowEnergy = 0;

let palettes = [
  ["#00f5d4", "#0bbcd6", "#2ec4b6"],
  ["#ff006e", "#fb5607", "#ffbe0b"],
  ["#8338ec", "#3a86ff", "#4361ee"]
];
let currentPalette = 0;

function preload() {
  soundFormats('mp3', 'wav');
  songs[0] = loadSound('disciple.mp3');
  songs[1] = loadSound('disciple_nobass.mp3'); 
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  fft = new p5.FFT(0.7, 512);
  song = songs[currentSong];
  song.loop();
  cols = floor(width / scale);
  rows = floor(height / scale);
}

function draw() {
  background(0, 40);
  analyzeAudio();
  
  if (lowEnergy > 100) updateFlowField();

  // EXPLOSIÓN - Mantenemos el umbral pero con la señal más filtrada
  if (lowEnergy > 215) { 
    let centerX = random(width * 0.1, width * 0.9);
    let centerY = random(height * 0.1, height * 0.9);
    for (let i = 0; i < 15; i++) {
      agents.push(new Agent(centerX, centerY));
    }
  }

  strokeWeight(0.5);
  for (let i = 0; i < agents.length; i++) {
    let a = agents[i];
    let checkLimit = min(i + 20, agents.length); 
    for (let j = i + 1; j < checkLimit; j++) {
      let b = agents[j];
      let dSq = (a.pos.x - b.pos.x)**2 + (a.pos.y - b.pos.y)**2;
      if (dSq < 6400) {
        let alpha = map(dSq, 0, 6400, a.lifespan, 0);
        stroke(a.color.levels[0], a.color.levels[1], a.color.levels[2], alpha);
        line(a.pos.x, a.pos.y, b.pos.x, b.pos.y);
      }
    }
    a.follow(flowField);
    a.update();
    a.show();
  }

  for (let i = agents.length - 1; i >= 0; i--) {
    if (agents[i].isDead()) agents.splice(i, 1);
  }
  zoff += 0.005;
}

function analyzeAudio() {
  fft.analyze();
  // Rango ultra-bajo: 20Hz a 50Hz (Puro sub-bajo)
  let subEnergy = fft.getEnergy(20, 50);   
  // Suavizado ultra-lento: 0.04 para ignorar transitorios rápidos
  lowEnergy = lerp(lowEnergy, subEnergy, 0.04);
}

function updateFlowField() {
  let yoff = 0;
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      let angle = noise(xoff, yoff, zoff) * TWO_PI;
      flowField[index] = p5.Vector.fromAngle(angle).setMag(0.2);
      xoff += 0.2;
    }
    yoff += 0.2;
  }
}

class Agent {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(5, 12)); 
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.friction = 0.9;
    let p = palettes[currentPalette];
    this.color = color(random(p));
  }
  follow(vectors) {
    if (vectors.length === 0) return;
    let x = floor(this.pos.x / scale);
    let y = floor(this.pos.y / scale);
    x = constrain(x, 0, cols - 1);
    y = constrain(y, 0, rows - 1);
    this.applyForce(vectors[x + y * cols]);
  }
  applyForce(force) { this.acc.add(force); }
  update() {
    this.vel.add(this.acc);
    this.vel.mult(this.friction);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 3; 
  }
  show() {
    stroke(this.color.levels[0], this.color.levels[1], this.color.levels[2], this.lifespan);
    strokeWeight(2);
    point(this.pos.x, this.pos.y);
  }
  isDead() {
    return (this.lifespan < 0 || this.pos.x < 0 || this.pos.x > width || this.pos.y < 0 || this.pos.y > height);
  }
}

function keyPressed() {
  if (key === 'c' || key === 'C') {
    currentPalette = (currentPalette + 1) % palettes.length;
  }
  if (key === '1') switchSong(0);
  if (key === '2') switchSong(1);
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
  cols = floor(width / scale);
  rows = floor(height / scale);
  background(0);
}

## Bitácora de reflexión
