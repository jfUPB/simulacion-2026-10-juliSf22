# Unidad 4

## Bitácora de proceso de aprendizaje

## ctividad 1:
Lo más impactante de Memo Akten es cómo fusiona arte, tecnología y física para crear movimientos orgánicos. En *Simple Harmonic Motion*, transforma conceptos matemáticos en ritmos visuales hipnóticos que imitan la naturaleza. Al definir reglas en lugar de diseñar cada detalle, demuestra el poder de los sistemas generativos: las matemáticas no solo resuelven problemas, sino que se convierten en herramientas creativas capaces de transmitir armonía y vida.

## ctividad 2:

En la primera simulación, trasladar el origen al centro facilita las rotaciones: no se mueve el objeto, sino que gira todo el sistema de coordenadas con `rotate()`, haciendo que los elementos dibujados sigan ese nuevo referencia.

La segunda muestra cómo orientar un objeto según su movimiento. Usando vectores de velocidad, la función `heading()` calcula el ángulo de dirección para rotar la figura y que apunte hacia donde avanza. Aquí, `push()` y `pop()` son clave para aislar estas transformaciones sin afectar al resto del lienzo, mientras que `rectMode(CENTER)` asegura que la rotación ocurra alrededor del propio centro del objeto, logrando un movimiento natural y coherente.



## Actividad 3:
En esta actividad creé un vehículo controlado por flechas aplicando el marco Motion 101. Usé aceleración y velocidad para un desplazamiento natural, evitando cambios bruscos de posición. Lo clave fue orientar el triángulo con heading() según el vector de velocidad. Combinando translate() y rotate(), el sistema de coordenadas se ajusta para que la figura apunte siempre hacia donde avanza. Esto reforzó mi comprensión sobre cómo los vectores dictan la orientación y cómo las transformaciones permiten visualizar ese comportamiento dinámico en el canvas. Para mejorarlo, agregué fricción para que el vehículo se detenga suavemente al soltar las teclas

````
let vehicle;

function setup() {
  createCanvas(640, 360);
  vehicle = new Vehicle();
}

function draw() {
  background(240);
  vehicle.update();
  vehicle.checkEdges();
  vehicle.display();
}

class Vehicle {
  constructor() {
    this.position = createVector(width/2, height/2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.topSpeed = 5;
    this.friction = 0.98; // Nueva variable de fricción
  }

  update() {
    if (keyIsDown(LEFT_ARROW)) {
      this.acceleration.x = -0.2;
    } else if (keyIsDown(RIGHT_ARROW)) {
      this.acceleration.x = 0.2;
    } else {
      this.acceleration.x = 0;
      this.velocity.mult(this.friction); // Aplicar fricción si no hay input
    }

    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
  }

  display() {
    let angle = this.velocity.heading();
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    fill(120);
    stroke(0);
    strokeWeight(2);
    triangle(-15, -10, -15, 10, 15, 0);
    pop();
  }

  checkEdges() {
    if (this.position.x > width) this.position.x = 0;
    else if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    else if (this.position.y < 0) this.position.y = height;
  }
}

````
## Actividad 4:


El análisis de la simulación Motion 101 con fuerzas consolida el marco de posición, velocidad y aceleración. La clave es calcular la aceleración sumando las fuerzas en cada frame y reiniciarla después para evitar acumulaciones erróneas.

El objeto Attractor ejerce una fuerza de atracción similar a la gravedad. Incluye atributos como `dragging` y `rollover`, diseñados para interacción con el mouse, lo que permitiría mover el atractor o cambiar su color al detectarlo.

Este ejercicio clarifica cómo integrar sistemas de fuerzas e interacción en simulaciones físicas. Pequeñas modificaciones, como resetear la aceleración o añadir un atractor interactivo, generan comportamientos dinámicos complejos. Entendí mejor cómo las fuerzas dirigen el movimiento y cómo la interactividad enriquece la experiencia visual dentro del entorno de programación creativa.

## Actividad 5:

En esta actividad exploré coordenadas polares (radio y ángulo) como alternativa al sistema cartesiano. Trasladar el origen al centro facilita visualizar el movimiento circular.

Noté que usar `p5.Vector.fromAngle(theta)` crea un vector unitario, dejando el punto cerca del origen por falta de magnitud. Sin embargo, al agregar el radio `r` como segundo parámetro `fromAngle(theta, r)`, el vector escala correctamente.

Esto demuestra que los vectores simplifican la conversión polar a cartesiana, generando la trayectoria circular sin calcular manualmente seno y coseno. Entendí que el ángulo define la dirección y el radio la distancia, permitiendo posicionar elementos en el plano de forma más eficiente usando herramientas vectoriales.

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
## ctividad 7:


## Actividad 8:
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
## ctividad 10:
````
let pendulum1;
let pendulum2;

function setup() {
  createCanvas(640, 400);

  pendulum1 = new Pendulum(width/2, 40, 140);
  pendulum2 = new Pendulum(width/2, 180, 140);

  pendulum1.angle = PI/3;
  pendulum2.angle = PI/6;
}

function draw() {
  background(240);

 
  pendulum1.pivot.x = mouseX;

  pendulum1.update();
  pendulum1.show(color(70,130,255));

  
  pendulum2.pivot = pendulum1.bob;

  pendulum2.update();
  pendulum2.show(color(255,120,80));

  // línea entre las bolas
  stroke(150);
  strokeWeight(1);
  line(pendulum1.bob.x, pendulum1.bob.y, pendulum2.bob.x, pendulum2.bob.y);
}

class Pendulum {

  constructor(x,y,r){
    this.pivot = createVector(x,y);
    this.bob = createVector();

    this.r = r;

    this.angle = PI/4;
    this.angleVelocity = 0;
    this.angleAcceleration = 0;

    this.damping = 0.995;

    this.ballr = 14;
  }

  update(){

    let gravity = 0.5;

    this.angleAcceleration = (-gravity / this.r) * sin(this.angle);

    this.angleVelocity += this.angleAcceleration;
    this.angle += this.angleVelocity;

    this.angleVelocity *= this.damping;
  }

  show(c){

    this.bob.set(
      this.r * sin(this.angle),
      this.r * cos(this.angle)
    );

    this.bob.add(this.pivot);

    stroke(0);
    strokeWeight(3);

    line(this.pivot.x,this.pivot.y,this.bob.x,this.bob.y);

    fill(c);
    noStroke();
    circle(this.bob.x,this.bob.y,this.ballr*2);
  }

}
````

## Bitácora de aplicación 

````js
let emojis = [];
let springs = [];

let num = 10;
let spacing = 50;

let t = 0;
let n = 0;

let useCos = false;

function setup() {

  createCanvas(800,500);

  for (let i = 0; i < num; i++) {

    let x = 100 + i*spacing;
    let y = height/2;

    let e = new Emoji(x,y);
    emojis.push(e);

    if(i > 0){
      springs.push(new Spring(emojis[i-1], emojis[i], spacing));
    }

  }

}

function draw(){

  background(20,20,35);

  let leader = emojis[0];

  let perlinOffset = map(noise(n),0,1,-40,40);

  if(useCos){
    leader.position.y = height/2 + cos(t)*80 + perlinOffset;
  } else {
    leader.position.y = height/2 + sin(t)*80 + perlinOffset;
  }

  t += 0.05;
  n += 0.01;

  if(mouseIsPressed){
    leader.position.y = mouseY;
  }

  for(let s of springs){
    s.update();
    s.display();
  }

  for(let e of emojis){
    e.update();
    e.display();
  }

}

class Emoji{

  constructor(x,y){

    this.position = createVector(x,y);
    this.velocity = createVector(0,0);
    this.acceleration = createVector(0,0);

  }

  applyForce(force){
    this.acceleration.add(force);
  }

  update(){

    let friction = this.velocity.copy();
    friction.mult(-0.02);
    this.applyForce(friction);

    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);

    this.acceleration.mult(0);

  }

  display(){

    textSize(30);
    textAlign(CENTER,CENTER);
    text("🐛",this.position.x,this.position.y);

  }

}

class Spring{

  constructor(a,b,len){

    this.a = a;
    this.b = b;

    this.restLength = len;
    this.k = 0.08;

  }

  update(){

    let force = p5.Vector.sub(this.b.position,this.a.position);

    let d = force.mag();

    let stretch = d - this.restLength;

    force.setMag(-this.k * stretch);

    this.b.applyForce(force);
    this.a.applyForce(p5.Vector.mult(force,-1));

  }

  display(){

    stroke(200);

    line(
      this.a.position.x,
      this.a.position.y,
      this.b.position.x,
      this.b.position.y
    );

  }

}

function keyPressed(){

  if(key === "c" || key === "C"){
    useCos = !useCos;
  }

}
````
[View](https://editor.p5js.org/juliSf22/full/JFeb8SdI8)

<img width="699" height="406" alt="image" src="https://github.com/user-attachments/assets/96005859-470c-45f6-9d74-b5c5066e502a" />

## Bitácora de reflexión








