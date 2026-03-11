# Unidad 4

## Bitácora de proceso de aprendizaje

## ctividad 6:
Recuerda estos conceptos: velocidad angular, frecuencia, periodo, amplitud y fase.
Realiza una simulación en la que puedas modificar estos parámetros y observar cómo se comporta la función sinusoide.

 ````js

let period = 120;
let amplitude = 200;
let phase = 0;

function setup() {
  createCanvas(640, 240);
  phase = TWO_PI/8;
  
}

function draw() {
  background(255);
  
  let x = amplitude * sin( ((TWO_PI * frameCount) / period));
  let x2 = amplitude * sin( ((TWO_PI * frameCount) / period) + phase);

  stroke(0);
  strokeWeight(2);
  translate(width / 2, height / 2);

  fill(127);
  line(-50, -50, x, -50);
  circle(x, -50, 48);
  
  fill(0);
  line(0, 0, x2, 0);
  circle(x2, 0, 48);  
}

function keyPressed(){
  phase += TWO_PI/360;  
}

````

## Actividad 7
## Actividad 8
````js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com


let angleVelocity = 0.2;
let amplitude = 100;
 let angle2 = 0;

function setup() {
  createCanvas(640, 240);
  background(255);

  stroke(0);
  strokeWeight(2);
  fill(127, 127);

  
}

function draw() {
   background(255);
  
   let angle = angle2;

  for (let x = 0; x <= width; x += 24) {
    // 1) Calculate the y position according to amplitude and sine of the angle.
    let y = amplitude * sin(angle);
    // 2) Draw a circle at the (x,y) position.
    circle(x, y + height / 2, 48);
    // 3) Increment the angle according to angular velocity.
     angle += angleVelocity;
  }
   angle2+= 0.05;
}


````

## Bitácora de aplicación 

````

let mic;
let particles = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  mic = new p5.AudioIn();
  mic.start();
  
  background(10);
}

function draw() {
  
  background(10, 20); // efecto de rastro
  
  let vol = mic.getLevel();
  
  let cantidad = map(vol, 0, 0.2, 0, 20);
  
  for (let i = 0; i < cantidad; i++) {
    particles.push(new Particle(width/2, height/2, vol));
  }
  
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    
    if (particles[i].life <= 0) {
      particles.splice(i, 1);
    }
  }
}

class Particle {
  
  constructor(x, y, vol) {
    this.x = x;
    this.y = y;
    
    this.vx = random(-2, 2);
    this.vy = random(-2, 2);
    
    this.size = random(5, 20) + vol * 200;
    
    this.life = 255;
    
    this.color = color(
      random(100,255),
      random(100,255),
      random(255),
      this.life
    );
  }
  
  update() {
    
    this.x += this.vx;
    this.y += this.vy;
    
    let angle = atan2(mouseY - this.y, mouseX - this.x);
    
    this.vx += cos(angle) * 0.01;
    this.vy += sin(angle) * 0.01;
    
    this.life -= 2;
  }
  
  display() {
    
    noStroke();
    
    fill(
      red(this.color),
      green(this.color),
      blue(this.color),
      this.life
    );
    
    ellipse(this.x, this.y, this.size);
  }
}

````

## Bitácora de reflexión

