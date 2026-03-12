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
let emojis = [];
let springs = [];

let num = 10;
let spacing = 50;

let t = 0;

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
  leader.position.y = height/2 + sin(t)*80;

  // actualiza resortes
  for(let s of springs){
    s.update();
    s.display();
  }

  // actualiza emojis
  for(let e of emojis){
    e.update();
    e.display();
  }

  t += 0.05;

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

    this.velocity.add(this.acceleration);
    this.velocity.mult(0.95);

    this.position.add(this.velocity);

    this.acceleration.mult(0);

  }

  display(){

    textSize(30);
    textAlign(CENTER,CENTER);
    text("🐶",this.position.x,this.position.y);

  }

}


// clase Spring

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
````
[View](https://editor.p5js.org/juliSf22/full/pdduBOFzy)
## Bitácora de reflexión


