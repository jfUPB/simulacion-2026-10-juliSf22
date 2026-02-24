# Unidad 3

## Bitácora de proceso de aprendizaje

[simulacion](https://juanferfranco.github.io/simulacion-2026-10/)

### Actividad 1: 

bueno pues la verdad un poco preocupante lo que dice pero muy ierto

### Actividad 2: 

```js
class Mover {
  constructor() {
    this.position = createVector();
    this.velocity = createVector();
    this.acceleration = createVector();
  }
}
```




## Bitácora de aplicación 


````js
let sheep = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  textAlign(CENTER, CENTER);

  for (let i = 0; i < 60; i++) {
    sheep.push(new Sheep(random(width), random(height)));
  }
}

function draw() {
  drawGrassBackground();

  // 🐕 perro
  textSize(28);
  text("🐕", mouseX, mouseY);

  for (let s of sheep) {
    s.flock(sheep);
    s.flee(mouseX, mouseY);
    s.update();
    s.show();
  }
}

// 🌿 FONDO PASTO
function drawGrassBackground() {
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);

    let c1 = color(120, 180, 90);   // verde claro
    let c2 = color(40, 100, 50);    // verde oscuro

    let c = lerpColor(c1, c2, inter);
    stroke(c);
    line(0, y, width, y);
  }
}

// 🐑 CLASE
class Sheep {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.maxSpeed = 2.5;
    this.maxForce = 0.05;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  // 🧠 COMPORTAMIENTO DE REBAÑO
  flock(sheep) {
    let align = this.align(sheep);
    let cohesion = this.cohesion(sheep);
    let separation = this.separation(sheep);

    align.mult(1.0);
    cohesion.mult(0.6);
    separation.mult(1.5);

    this.applyForce(align);
    this.applyForce(cohesion);
    this.applyForce(separation);
  }

  align(sheep) {
    let perception = 50;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        steering.add(other.vel);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  cohesion(sheep) {
    let perception = 60;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        steering.add(other.pos);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.sub(this.pos);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  separation(sheep) {
    let perception = 30;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        let diff = p5.Vector.sub(this.pos, other.pos);
        diff.div(d * d);
        steering.add(diff);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  // 🐕 HUIR DEL PERRO
  flee(mx, my) {
    let dog = createVector(mx, my);
    let desired = p5.Vector.sub(this.pos, dog);
    let d = desired.mag();

    if (d < 120) {
      desired.setMag(this.maxSpeed);
      let steer = p5.Vector.sub(desired, this.vel);
      steer.limit(this.maxForce * 2);
      this.applyForce(steer);
    }
  }

  update() {
    this.vel.add(this.acc);

    // fricción (más natural)
    this.vel.mult(0.98);

    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // bordes
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  show() {
    let speed = this.vel.mag();

    if (speed > 1.5) {
      textSize(22);
    } else {
      textSize(18);
    }

    text("🐑", this.pos.x, this.pos.y);
  }
}
````

```` js

let sheep = [];
let frenzy = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  textAlign(CENTER, CENTER);

  for (let i = 0; i < 60; i++) {
    sheep.push(new Sheep(random(width), random(height)));
  }
}

function draw() {
  drawGrassBackground();

  // 🐕 perro (mouse)
  textSize(28);
  text("🐕", mouseX, mouseY);

  for (let s of sheep) {
    s.flock(sheep);
    s.flee(mouseX, mouseY);
    s.update();
    s.show();
  }
}

// 🎹 cambiar modo con F
function keyPressed() {
  if (key === 'f' || key === 'F') {
    frenzy = !frenzy;
  }
}

// 🌿 fondo tipo pasto
function drawGrassBackground() {
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c1 = color(120, 180, 90);
    let c2 = color(40, 100, 50);
    let c = lerpColor(c1, c2, inter);
    stroke(c);
    line(0, y, width, y);
  }
}

// 🐑 clase oveja
class Sheep {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.maxSpeed = 2.5;
    this.maxForce = 0.05;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  flock(sheep) {
    let align = this.align(sheep);
    let cohesion = this.cohesion(sheep);
    let separation = this.separation(sheep);

    if (frenzy) {
      // 🔥 modo caótico
      align.mult(0.3);
      cohesion.mult(0.1);
      separation.mult(2.0);

      let angle = random(TWO_PI);
      let chaos = p5.Vector.fromAngle(angle);
      chaos.mult(0.5);
      this.applyForce(chaos);

      this.maxSpeed = 4;
    } else {
      // 🐑 modo normal
      align.mult(1.0);
      cohesion.mult(0.6);
      separation.mult(1.5);

      this.maxSpeed = 2.5;
    }

    this.applyForce(align);
    this.applyForce(cohesion);
    this.applyForce(separation);
  }

  align(sheep) {
    let perception = 50;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        steering.add(other.vel);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  cohesion(sheep) {
    let perception = 60;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        steering.add(other.pos);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.sub(this.pos);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  separation(sheep) {
    let perception = 30;
    let steering = createVector();
    let total = 0;

    for (let other of sheep) {
      let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
      if (other != this && d < perception) {
        let diff = p5.Vector.sub(this.pos, other.pos);
        diff.div(d * d);
        steering.add(diff);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.vel);
      steering.limit(this.maxForce);
    }

    return steering;
  }

  flee(mx, my) {
    let dog = createVector(mx, my);
    let desired = p5.Vector.sub(this.pos, dog);
    let d = desired.mag();

    if (d < 120) {
      desired.setMag(this.maxSpeed);
      let steer = p5.Vector.sub(desired, this.vel);
      steer.limit(this.maxForce * 2);
      this.applyForce(steer);
    }
  }

  update() {
    this.vel.add(this.acc);
    this.vel.mult(0.98);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  show() {
    let speed = this.vel.mag();

    if (frenzy) {
      textSize(24);
    } else {
      textSize(speed > 1.5 ? 22 : 18);
    }

    text("🐑", this.pos.x, this.pos.y);
  }
}
````


## Bitácora de reflexión


