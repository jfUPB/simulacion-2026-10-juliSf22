# Unidad 5
## Bitácora de proceso de aprendizaje
[simulacion texto guia](https://juanferfranco.github.io/simulacion-2026-10/)

se debe recorrer de atras para adelante. porque se tienen que elimiar lás más viejas osea las que se crearon primero

### Actividad 1: 
¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?
tiene pues sis fisicas y eso pero lo más importante es que tienen un tiempo de vida definido, osea que al momento de crearse ya tenga un tiempo de vida para eliminarse, esto para no saturar y ahorrar recursos del PC

¿Qué condición determina que una partícula “muere”? ¿Es una muerte instantánea o gradual?

el tiempo de vida, so esto se mescla con el cambio en la opacidad de la misma particula, pues provoca que la particula a medida que se hace más vieja tambien de la persepcion de que está desapareciendo

¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula.

pues se genera, y con fuerzas (que se calculan cada frame cada frame) generan movimiento



## Bitácora de aplicación 

<img width="967" height="587" alt="image" src="https://github.com/user-attachments/assets/0aaffba4-0fd2-40e5-9a59-c81e437a30b6" />

````js
/**
 * Sakura Particles - Atardecer Cálido
 * Interacción: Micrófono (Salto) + Mouse (Viento)
 */

let particles = [];
let mic;
let emojis = ['🌸', '🍂'];
let tableY;
let audioStarted = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  tableY = height - 100; 
  mic = new p5.AudioIn();
}

function draw() {
  // --- FONDO DEGRADADO ---
  noStroke();
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(180, 120, 200), color(255, 180, 130), inter);
    stroke(c);
    line(0, y, width, y);
  }

  // 1. DIBUJAR EL ÁRBOL CENTRADO
  drawSakuraTreeCentrado();

  // 2. DIBUJAR LA MESA
  noStroke();
  fill(100, 70, 50); 
  rect(0, tableY, width, 30);
  fill(70, 45, 30); 
  rect(0, tableY + 30, width, 70);

  if (!audioStarted) {
    fill(255, 220);
    textAlign(CENTER, CENTER);
    textSize(22);
    text("🌸 Haz clic para activar el micrófono y el viento", width / 2, height / 2);
    return;
  }

  let micLevel = mic.getLevel();

  // --- LÓGICA DEL VIENTO (MOUSE) ---
  // Calculamos la fuerza del viento basada en la distancia del mouse al centro
  // Si el mouse está en el centro, el viento es 0.
  let windStrength = map(mouseX, 0, width, -0.15, 0.15);
  let wind = createVector(windStrength, 0);

  // 4. GENERAR PÉTALOS
  if (random(1) < 0.12) { 
    particles.push(new Particle(random(width * 0.15, width * 0.85), random(-50, height * 0.4))); 
  }

  let gravity = createVector(0, 0.12);

  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    
    // Aplicamos Gravedad
    p.applyForce(gravity);
    
    // Aplicamos Viento solo si la partícula está en el aire
    if (p.pos.y < tableY - 5) {
      p.applyForce(wind);
    }

    // Salto por ruido
    if (micLevel > 0.05) { 
      if (p.pos.y >= tableY - 5) {
        let jumpPower = map(micLevel, 0.05, 1, -4, -12);
        let jumpForce = createVector(random(-1.5, 1.5), jumpPower);
        p.vel.y = 0; 
        p.applyForce(jumpForce);
        p.lifespan = min(p.lifespan + 30, 255);
      }
    }

    p.update();
    p.checkSurface(tableY);
    p.show();

    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }

  // Opcional: Mostrar una flecha o texto sutil del viento
  /*
  fill(255, 100);
  textSize(14);
  text(windStrength > 0 ? "Viento: Derecha >>" : "<< Viento: Izquierda", width/2, tableY + 50);
  */
}

function mousePressed() {
  if (!audioStarted) {
    userStartAudio();
    mic.start();
    audioStarted = true;
  }
}

function drawSakuraTreeCentrado() {
  push();
  noFill();
  stroke(65, 40, 30); 
  strokeCap(ROUND);
  strokeJoin(ROUND);

  strokeWeight(30);
  bezier(width * 0.5, height, width * 0.52, height * 0.7, width * 0.48, height * 0.4, width * 0.5, height * 0.1);

  strokeWeight(20);
  bezier(width * 0.51, height * 0.65, width * 0.4, height * 0.62, width * 0.2, height * 0.65, width * 0.1, height * 0.55);
  
  strokeWeight(15);
  bezier(width * 0.49, height * 0.45, width * 0.35, height * 0.42, width * 0.25, height * 0.35, width * 0.15, height * 0.25);

  strokeWeight(12);
  bezier(width * 0.5, height * 0.25, width * 0.42, height * 0.2, width * 0.35, height * 0.15, width * 0.3, height * -0.05);

  strokeWeight(20);
  bezier(width * 0.49, height * 0.68, width * 0.6, height * 0.65, width * 0.8, height * 0.62, width * 0.9, height * 0.52);
  
  strokeWeight(15);
  bezier(width * 0.51, height * 0.48, width * 0.65, height * 0.45, width * 0.75, height * 0.38, width * 0.85, height * 0.3);

  strokeWeight(12);
  bezier(width * 0.5, height * 0.3, width * 0.58, height * 0.25, width * 0.65, height * 0.2, width * 0.7, height * -0.1);

  strokeWeight(7);
  bezier(width * 0.25, height * 0.6, width * 0.2, height * 0.55, width * 0.18, height * 0.6, width * 0.1, height * 0.5);
  bezier(width * 0.75, height * 0.42, width * 0.8, height * 0.45, width * 0.82, height * 0.38, width * 0.9, height * 0.4);

  pop();
}

class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-0.5, 0.5), random(0, 1.5));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.decayRate = random(0.4, 1.2);
    this.emoji = random(emojis);
    this.size = random(20, 38);
    this.rotation = random(TWO_PI);
    this.rotSpeed = random(-0.04, 0.04);
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.y < tableY) {
        // La rotación aumenta si hay fuerza horizontal (viento)
        this.rotation += this.rotSpeed + (this.vel.x * 0.05);
    }

    if (this.pos.y >= tableY - 1) {
      this.lifespan -= this.decayRate * 3.5;
      this.vel.x *= 0.85; 
    } else {
      this.lifespan -= this.decayRate;
      this.vel.x *= 0.99; // Un poco de resistencia al aire
    }
  }

  checkSurface(surfaceY) {
    if (this.pos.y >= surfaceY) {
      this.pos.y = surfaceY;
      this.vel.y *= -0.1;
    }
  }

  show() {
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.rotation);
    let alphaVal = 255;
    if (this.lifespan < 50) {
      alphaVal = map(this.lifespan, 0, 50, 0, 255);
    }
    fill(255, alphaVal);
    textAlign(CENTER, CENTER);
    textSize(this.size);
    text(this.emoji, 0, 0);
    pop();
  }

  isDead() {
    return this.lifespan <= 0;
  }
}
````


## Bitácora de reflexión
