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

<img width="966" height="584" alt="image" src="https://github.com/user-attachments/assets/7cdea1b6-d202-4f84-95c7-f1a0dda0a0c6" />


````js
let particles = [];
let mic, tableY, imgArbol;
let audioStarted = false;
let myShader, layer;

// --- SHADERS INTEGRADOS ---
const vertShader = `
precision mediump float;
attribute vec3 aPosition;
attribute vec2 aTexCoord;
varying vec2 vTexCoord;
void main() {
    vTexCoord = aTexCoord;
    vec4 positionVec4 = vec4(aPosition, 1.0);
    positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
    gl_Position = positionVec4;
}`;

const fragShader = `
precision mediump float;
varying vec2 vTexCoord;
uniform sampler2D tex0;
void main() {
    vec2 uv = vec2(vTexCoord.x, 1.0 - vTexCoord.y);
    vec4 col = texture2D(tex0, uv);
    vec4 bloom = vec4(0.0);
    for(float i = -2.0; i <= 2.0; i++) {
        for(float j = -2.0; j <= 2.0; j++) {
            bloom += texture2D(tex0, uv + vec2(i, j) * 0.002);
        }
    }
    bloom /= 25.0;
    float bright = (col.r + col.g + col.b) / 3.0;
    if(bright > 0.4) {
        col += bloom * 0.5;
    }
    gl_FragColor = col;
}`;

function preload() {
  imgArbol = loadImage('./arbol.png');
}

function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  myShader = createShader(vertShader, fragShader);
  layer = createGraphics(windowWidth, windowHeight);
  layer.imageMode(CENTER);
  layer.textAlign(CENTER, CENTER);
  tableY = height - 100; 
  mic = new p5.AudioIn();
}

function draw() {
  if (!imgArbol || imgArbol.width <= 0) return;

  layer.clear();
  
  // 1. FONDO
  layer.noStroke();
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(180, 120, 200), color(255, 180, 130), inter);
    layer.stroke(c);
    layer.line(0, y, width, y);
  }

  // 2. ÁRBOL (Dibujado antes de la mesa para que las raíces se vean "dentro")
  let escala = height * 0.85;
  layer.image(imgArbol, width / 2, height / 2, escala * (imgArbol.width/imgArbol.height), escala);

  // 3. MESA / TIERRA (Con transparencia para ver las hojas pasar por debajo)
  layer.noStroke();
  layer.fill(60, 40, 30, 240); // 240 de opacidad para efecto de profundidad
  layer.rect(0, tableY, width, 150);

  // 4. PARTÍCULAS
  if (audioStarted) {
    let micLevel = mic.getLevel();
    let wind = createVector(map(mouseX, 0, width, -0.2, 0.2), 0);

    if (random(1) < 0.15) particles.push(new Particle());

    for (let i = particles.length - 1; i >= 0; i--) {
      let p = particles[i];
      
      if (!p.isFeeding) {
        p.applyForce(createVector(0, 0.15)); // Gravedad normal
        p.applyForce(wind);
        
        if (micLevel > 0.05 && p.pos.y >= tableY - 5) {
          p.vel.y = map(micLevel, 0.05, 1, -4, -15);
          p.lifespan = 255;
        }
      } else {
        // --- LÓGICA SUBTERRÁNEA ---
        let centroTronco = width / 2;
        let distAlCentro = centroTronco - p.pos.x;
        
        // 1. Bajar a la tierra: Si aún no está "profunda", forzar caída
        if (p.pos.y < tableY + 40) {
            p.vel.y = 2; 
        } else {
            p.vel.y *= 0.1; // Se detiene verticalmente para viajar horizontal
        }

        // 2. Viaje horizontal al centro
        p.vel.x += distAlCentro * 0.04;
        p.vel.x *= 0.8; 
        
        // 3. Ascenso por el tronco
        if (abs(distAlCentro) < 15 && p.pos.y > tableY + 20) {
            p.pos.x = centroTronco; 
            p.vel.y = -8; // ¡Sube!
            p.size *= 0.94; 
        }
      }

      p.update();
      p.show(layer);
      if (p.isDead()) particles.splice(i, 1);
    }
  } else {
    layer.fill(255);
    layer.textSize(32);
    layer.text("🌸 Click para iniciar", width/2, height/2);
  }

  shader(myShader);
  myShader.setUniform('tex0', layer);
  rect(-width / 2, -height / 2, width, height);
}

function mousePressed() {
  if (!audioStarted) {
    userStartAudio();
    mic.start();
    audioStarted = true;
  }
}

class Particle {
  constructor() {
    this.pos = createVector(random(width * 0.1, width * 0.9), random(-50, height * 0.4));
    this.vel = createVector(random(-1, 1), random(1, 2));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.size = random(20, 35);
    this.emoji = '🌸';
    this.isFeeding = false;
    this.rot = random(TWO_PI);
  }

  applyForce(f) { this.acc.add(f); }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // Si es flor, rebota. Si es hoja, ignora el rebote para "enterrarse"
    if (!this.isFeeding) {
        if (this.pos.y >= tableY) {
            this.pos.y = tableY;
            this.vel.y *= -0.1;
            this.lifespan -= 3;
            if (this.lifespan < 160) {
                this.emoji = '🍂';
                this.isFeeding = true;
            }
        }
        this.rot += 0.05;
    } else {
        this.lifespan -= 1.5;
        this.rot += 0.02;
    }
  }

  show(c) {
    c.push();
    c.translate(this.pos.x, this.pos.y);
    c.rotate(this.rot);
    
    // Si está bajo tierra, se ve más oscura y transparente
    let alpha = this.isFeeding ? map(this.lifespan, 0, 160, 0, 180) : this.lifespan;
    if (this.isFeeding && this.pos.y > tableY) {
        c.fill(100, 50, 50, alpha); // Tono tierra
    } else {
        c.fill(255, alpha);
    }
    
    c.textSize(this.size);
    c.text(this.emoji, 0, 0);
    c.pop();
  }

  isDead() {
    // Si ya subió más allá de la pantalla después de alimentar, muere
    return this.lifespan <= 0 || (this.isFeeding && this.pos.y < -150);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  layer = createGraphics(windowWidth, windowHeight);
}
````

````js
let particles = [];
let mic, tableY, imgArbol;
let audioStarted = false;
let myShader, layer;

// --- SHADERS INTEGRADOS ---
const vertShader = `
precision mediump float;
attribute vec3 aPosition;
attribute vec2 aTexCoord;
varying vec2 vTexCoord;
void main() {
    vTexCoord = aTexCoord;
    vec4 positionVec4 = vec4(aPosition, 1.0);
    positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
    gl_Position = positionVec4;
}`;

const fragShader = `
precision mediump float;
varying vec2 vTexCoord;
uniform sampler2D tex0;
void main() {
    vec2 uv = vec2(vTexCoord.x, 1.0 - vTexCoord.y);
    vec4 col = texture2D(tex0, uv);
    vec4 bloom = vec4(0.0);
    for(float i = -2.0; i <= 2.0; i++) {
        for(float j = -2.0; j <= 2.0; j++) {
            bloom += texture2D(tex0, uv + vec2(i, j) * 0.002);
        }
    }
    bloom /= 25.0;
    float bright = (col.r + col.g + col.b) / 3.0;
    if(bright > 0.4) {
        col += bloom * 0.5;
    }
    gl_FragColor = col;
}`;

function preload() {
  imgArbol = loadImage('./arbol.png');
}

function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  myShader = createShader(vertShader, fragShader);
  layer = createGraphics(windowWidth, windowHeight);
  layer.imageMode(CENTER);
  layer.textAlign(CENTER, CENTER);
  tableY = height - 100; 
  mic = new p5.AudioIn();
}

function draw() {
  if (!imgArbol || imgArbol.width <= 0) return;

  layer.clear();
  
  // 1. FONDO
  layer.noStroke();
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(180, 120, 200), color(255, 180, 130), inter);
    layer.stroke(c);
    layer.line(0, y, width, y);
  }

  // 2. ÁRBOL
  let escala = height * 0.85;
  layer.image(imgArbol, width / 2, height / 2, escala * (imgArbol.width/imgArbol.height), escala);

  // 3. MESA
  layer.noStroke();
  layer.fill(60, 40, 30);
  layer.rect(0, tableY, width, 100);

  // 4. PARTÍCULAS
  if (audioStarted) {
    let micLevel = mic.getLevel();
    let wind = createVector(map(mouseX, 0, width, -0.2, 0.2), 0);

    if (random(1) < 0.15) particles.push(new Particle());

    for (let i = particles.length - 1; i >= 0; i--) {
      let p = particles[i];
      
      if (!p.isFeeding) {
        p.applyForce(createVector(0, 0.15)); // Gravedad normal
        p.applyForce(wind);
        
        // Salto por mic
        if (micLevel > 0.05 && p.pos.y >= tableY - 5) {
          p.vel.y = map(micLevel, 0.05, 1, -4, -15);
          p.lifespan = 255;
        }
      } else {
        // --- LÓGICA DE ABSORCIÓN REFORZADA ---
        let centroTronco = width / 2;
        let distAlCentro = centroTronco - p.pos.x;
        
        // Atracción horizontal fuerte al centro
        let fuerzaAtraccion = distAlCentro * 0.05;
        p.vel.x += fuerzaAtraccion;
        p.vel.x *= 0.8; // Fricción para que no "orbite" y se quede en el centro
        
        // Si ya está centrada, empieza a subir
        if (abs(distAlCentro) < 20) {
            p.pos.x = lerp(p.pos.x, centroTronco, 0.1); // Forzar posición al centro
            p.vel.y = -6; // Sube
            p.size *= 0.95; // Se encoge
        } else {
            p.vel.y *= 0.5; // Se frena en Y mientras llega al centro
        }
      }

      p.update();
      p.show(layer);
      if (p.isDead()) particles.splice(i, 1);
    }
  } else {
    layer.fill(255);
    layer.textSize(32);
    layer.text("🌸 Click para iniciar", width/2, height/2);
  }

  shader(myShader);
  myShader.setUniform('tex0', layer);
  rect(-width / 2, -height / 2, width, height);
}

function mousePressed() {
  if (!audioStarted) {
    userStartAudio();
    mic.start();
    audioStarted = true;
  }
}

class Particle {
  constructor() {
    this.pos = createVector(random(width * 0.1, width * 0.9), random(-50, height * 0.4));
    this.vel = createVector(random(-1, 1), random(1, 2));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.size = random(20, 35);
    this.emoji = '🌸';
    this.isFeeding = false;
    this.rot = random(TWO_PI);
  }

  applyForce(f) { this.acc.add(f); }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.y >= tableY) {
      if (!this.isFeeding) {
        this.pos.y = tableY;
        this.vel.y *= -0.1;
      }
      this.lifespan -= 2.5;
      if (this.lifespan < 160) {
        this.emoji = '🍂';
        this.isFeeding = true;
      }
    } else if (!this.isFeeding) {
      this.rot += 0.05;
    }
  }

  show(c) {
    c.push();
    c.translate(this.pos.x, this.pos.y);
    c.rotate(this.rot);
    let a = this.isFeeding ? map(this.lifespan, 0, 160, 0, 255) : this.lifespan;
    c.fill(255, a);
    c.textSize(this.size);
    c.text(this.emoji, 0, 0);
    c.pop();
  }

  isDead() {
    return this.lifespan <= 0 || this.size < 2 || this.pos.y < -100;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  layer = createGraphics(windowWidth, windowHeight);
}
````
[editar](https://editor.p5js.org/juliSf22/sketches/I-X0Jiq7-)
[ver](https://editor.p5js.org/juliSf22/full/I-X0Jiq7-)

## Bitácora de reflexión
