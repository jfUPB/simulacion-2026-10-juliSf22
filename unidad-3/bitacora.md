# Unidad 3

## Bitácora de proceso de aprendizaje

[simulacion](https://juanferfranco.github.io/simulacion-2026-10/)

### Actividad 1: 

bueno pues la verdad un poco preocupante lo que dice pero muy ierto

### Actividad 2: 

En este ejercicio entendí que programar el movimiento es, en el fondo, reproducir cómo funcionan las cosas en la realidad. Me llamó mucho la atención eso de poner la aceleración en cero al terminar cada frame. Al comienzo me parecía innecesario, pero después comprendí que la aceleración actúa como un impulso momentáneo. Si no se reinicia, ese impulso se seguiría sumando una y otra vez, haciendo que el objeto gane velocidad sin límite, como si mantuvieras el acelerador presionado todo el tiempo sin dejar que el vehículo descanse.

### Actividad 3: 

````js

let mover;
let gravity;

function setup() {
  createCanvas(600, 400);
  mover = new Mover(300, 50, 3);
  gravity = createVector(0, 0.4);
}

function draw() {
  background(240);

  mover.applyForce(gravity);

  if (mover.position.y >= height - mover.mass * 8) {
    let friction = mover.velocity.copy();
    friction.x *= -1;
    friction.y = 0;
    friction.setMag(0.1);
    mover.applyForce(friction);
  }

  mover.update();
  mover.checkEdges();
  mover.show();

  fill(50);
  noStroke();
  rect(0, height - 10, width, 10);
}


class Mover {
  constructor(x, y, m) {
    this.mass = m;
    this.position = createVector(x, y);
    this.velocity = createVector(2, 0);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  checkEdges() {
    if (this.position.y > height - this.mass * 8) {
      this.position.y = height - this.mass * 8;
      this.velocity.y *= -0.6;
    }

    if (this.position.x > width) {
      this.position.x = width;
      this.velocity.x *= -1;
    }

    if (this.position.x < 0) {
      this.position.x = 0;
      this.velocity.x *= -1;
    }
  }

  show() {
    fill(120);
    stroke(0);
    ellipse(this.position.x, this.position.y, this.mass * 16);
  }
}
````

https://github.com/user-attachments/assets/28babadf-83e1-454c-8b88-58d1ee0a6375

 ````js
let movers = [];

function setup() {
  createCanvas(600, 400);

  for (let i = 0; i < 5; i++) {
    movers[i] = new Mover(random(50, width - 50), 0, random(1, 4));
  }
}

function draw() {
  background(255);

  noStroke();
  fill(0, 150, 255, 100);
  rect(0, height / 2, width, height / 2);

  for (let mover of movers) {

    let gravity = createVector(0, 0.1 * mover.mass);
    mover.applyForce(gravity);

    if (mover.position.y > height / 2) {

      let drag = mover.velocity.copy();
      drag.normalize();
      drag.mult(-1);

      let c = 0.08;
      let speedSq = mover.velocity.magSq();
      drag.setMag(c * speedSq);

      mover.applyForce(drag);
    }

    mover.update();
    mover.checkEdges();
    mover.show();
  }
}


class Mover {
  constructor(x, y, m) {
    this.mass = m;
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.color = color(random(255), random(255), random(255));
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  checkEdges() {
    if (this.position.y > height) {
      this.position.y = height;
      this.velocity.y *= -0.6;
    }
  }

  show() {
    fill(this.color);
    stroke(0);
    ellipse(this.position.x, this.position.y, this.mass * 16);
  }
}
````


https://github.com/user-attachments/assets/c1573521-07ca-4533-aab6-4ec64d3b3fe7






## Bitácora de aplicación 
Historia: lo que quria contar era basicamente "encarnarte" en un perro pastor, pues poder jugar como dirigiendo las obejas y así, aparte cuando presionas una tecla las obejas se "asustan" osea su movimiento es más erratico y son difisiles de controlar, aparte que tambien puedas reunirlas si quieres, presionando la g las atraes como si las estubieras llamando.

Fuerza → Aceleración → Velocidad → Posición

````js
let sheep = [];
let frenzy = false;
let guideMode = false;
let prevMouse;

function setup() {
  createCanvas(windowWidth, windowHeight);
  textAlign(CENTER, CENTER);

  prevMouse = createVector(mouseX, mouseY);

  for (let i = 0; i < 60; i++) {
    sheep.push(new Sheep(random(width), random(height)));
  }
}

function draw() {
  drawGrassBackground();

  textSize(28);
  text("🐕", mouseX, mouseY);

  let dogVelocity = createVector(mouseX - prevMouse.x, mouseY - prevMouse.y);
  prevMouse.set(mouseX, mouseY);

  for (let s of sheep) {
    s.flock(sheep);

    if (guideMode) {
      s.followDogDirection(dogVelocity);
    } else {
      s.flee(mouseX, mouseY);
    }

    s.update();
    s.show();
  }
}

function keyPressed() {
  if (key === 'f' || key === 'F') {
    frenzy = !frenzy;
  }

  if (key === 'g' || key === 'G') {
    guideMode = !guideMode;
  }
}

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
      align.mult(0.3);
      cohesion.mult(0.1);
      separation.mult(2.0);

      let angle = random(TWO_PI);
      let chaos = p5.Vector.fromAngle(angle);
      chaos.mult(0.5);
      this.applyForce(chaos);

      this.maxSpeed = 4;
    } else {
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

  followDogDirection(dogVel) {
    if (dogVel.mag() > 0.2) {
      let desired = dogVel.copy();
      desired.setMag(this.maxSpeed);

      let steer = p5.Vector.sub(desired, this.vel);
      steer.limit(this.maxForce * 1.5);
      this.applyForce(steer);
    }
  }

  applyFriction() {
    let friction = this.vel.copy();
    friction.mult(-1);

    if (friction.mag() > 0) {
      friction.normalize();
      friction.mult(0.03);
      this.applyForce(friction);
    }
  }

  update() {
    this.applyFriction();

    this.vel.add(this.acc);
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


<img width="816" height="692" alt="image" src="https://github.com/user-attachments/assets/5ee50fd0-efa0-4059-9bef-129bb5a61be1" />


[View](https://editor.p5js.org/juliSf22/full/S49ufekMr)

[Edit](https://editor.p5js.org/juliSf22/sketches/S49ufekMr)


## Bitácora de reflexión








