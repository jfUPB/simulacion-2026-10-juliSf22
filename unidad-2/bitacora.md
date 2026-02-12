# Unidad 2

## Bitácora de proceso de aprendizaje

### Actividad 1:

[simulacion 2026-10](http://juanferfranco.github.io/simulacion-2026-10/)

### Actividad 2:

¿Cómo funciona la suma dos vectores en p5.js?

En p5.js, la suma de vectores se hace con `p5.Vector.add()`. Combina dos vectores sumando sus componentes (x, y, z). Puedes crear uno nuevo (`v3 = p5.Vector.add(v1, v2)`) o modificar uno existente (`v1.add(v2)`). Se usa para mover objetos, combinar fuerzas o direcciones.

<img width="873" height="711" alt="image" src="https://github.com/user-attachments/assets/763ff76d-21ef-499a-ba24-776c24acb769" />

¿Por qué esta línea position = position + velocity; no funciona?

porque no está en p5js por lo que no puede suamr cada numer del vvector

### Actividad 3:


vectorizar un ramdom walk
¿Qué resultado esperabas obtener?

Esperaba que al trabajar con un vector y pasarlo a una función, el programa generara una nueva posición basada en ese vector, mostrando el cambio en sus valores.

¿Qué resultado obtuviste?

El vector sí cambió sus valores, pero noté que el vector original también se modificó cuando lo pasé a la función.

¿Qué tipo de paso se realiza en el código?

En este caso se está usando un objeto p5.Vector, y en JavaScript los objetos se pasan por referencia.
Eso significa que cuando una función recibe ese vector y modifica sus propiedades (por ejemplo x o y), está alterando directamente el objeto original, no una copia.

¿Qué aprendí?

Comprendí mejor la diferencia entre pasar datos por valor y por referencia.
Los tipos primitivos (como números) se copian y no afectan el original, mientras que los objetos comparten la misma referencia en memoria.
Como p5.Vector es un objeto, cualquier modificación dentro de una función impacta el vector original.


### Actividad 4:

```js
let position;

function setup() {
    createCanvas(400, 400);
    position = createVector(6,9);
    console.log(position.toString());
    playingVector(position);
    console.log(position.toString());
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```
1- ¿Qué resultado esperas obtener en el programa anterior?:

Espero que el vector position cambie sus valores después de llamar a playingVector, porque dentro de la función se modifican directamente las componentes x y y. el segundo console.log debería mostrar un vector distinto al inicial

2- ¿Qué resultado obtuviste?:

El primer console.log muestra (6, 9). Después de ejecutar playingVector(position), el segundo console.log muestra (20, 30). Esto confirma que el vector fue modificado correctamente desde dentro de la función

3- Recuerda los conceptos de paso por valor y paso por referencia en programación

Se realiza un paso por referencia. Los vectores en p5.js son objetos, y al pasarlos como parámetros se pasa la referencia al mismo objeto en memoria, no una copia de sus valores

4- ¿Qué tipo de paso se está realizando en el código?

Se realiza un paso por referencia. Los vectores en p5.js son objetos, y al pasarlos como parámetros se pasa la referencia al mismo objeto en memoria, no una copia de sus valores

5- ¿Qué aprendiste?

Aprendí que al pasar objetos como vectores a funciones, cualquier cambio dentro de la función afecta al objeto original. Para evitarlo, sería necesario crear una copia del vector antes de modificarlo.


### Actividad 5:

¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

para ahorrarnos sacar o calcular la raiz

¿Para qué sirve el método normalize()?

para tener la direccion para que solo sea multiplicar por un nnumero y sacar la magnitud
ajusta la magnitud del vector a 1 sin cambiar su dirección.

Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?

producto punto y sirve para ver si es paralelo o perpendicular

Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

sirve para enontrar un nuevo vector que sea perpendicular ambos vectores

¿Para que te puede servir el método dist()?
 para calular la distancia entre la (cabeza) de 2 vectores

 ¿Para qué sirven los métodos normalize() y limit()?

ajusta la magnitud del vector a 1 sin cambiar su dirección.

limit() restringe la magnitud del vector a un valor máximo.

### Actividad 6:

sin editar

```js

function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}

```


codigo editado

```js


function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
   let v5 = createVector(80,50);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
   let v4 = p5.Vector.sub(v2, v1); 

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
   drawArrow(v5, v4, 'green');


}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```
<img width="162" height="165" alt="image" src="https://github.com/user-attachments/assets/1b5682e7-ca0b-4956-98d1-5e10910fc9fd" />

¿Cuál es el concepto de Motion 101 y su interpretación geométrica?

Motion 101 es la base del movimiento en programación con vectores. Se basa en tres elementos principales:

Aceleración modifica la velocidad.

Velocidad modifica la posición.

Posición determina dónde se dibuja el objeto.

Geométricamente, se puede entender como una cadena de vectores:

La aceleración cambia la longitud o dirección de la flecha de velocidad.

La velocidad actúa como una flecha que indica hacia dónde y qué tan rápido se mueve el objeto.

Al sumar la velocidad a la posición en cada frame, el objeto avanza siguiendo esa dirección.

Es como si en cada cuadro el objeto siguiera la flecha de su velocidad actual.

¿Cómo se aplica en el ejemplo?

En el ejemplo del Mover:

update() se encarga de actualizar la física (aceleración → velocidad → posición).

show() dibuja el objeto usando su posición actual.

checkEdges() permite que el objeto reaparezca del otro lado cuando toca un borde, creando un espacio continuo.

draw() ejecuta todo en orden cada frame.

En resumen, el movimiento se produce acumulando pequeños cambios en cada cuadro.


### Actividad 7:
¿Qué observaste al usar distintos tipos de aceleración?

Noté que dependiendo de cómo se calcule la aceleración, el comportamiento del objeto cambia completamente:

Aceleración constante:
Produce un movimiento uniforme y predecible, generalmente en línea recta.

Aceleración aleatoria:
Hace que el objeto se mueva de forma impredecible y errática, cambiando de dirección constantemente.

Aceleración hacia el mouse:
Genera un movimiento más controlado y fluido, ya que el objeto se dirige hacia un punto específico. Se siente más natural porque responde a una referencia clara.

En conclusión, pequeños cambios en la fórmula de aceleración producen trayectorias muy distintas. La aceleración es lo que realmente define el comportamiento del movimiento.

## Bitácora de aplicación 
La idea era hacer algo que se viera bonito y fluido, pero que no fuera simplemente partículas moviéndose al azar.
Quería mezclar tres cosas de los ejemplos anteriores:

-El movimiento orgánico tipo olas (Perlin Noise).

-l cambio de color y vibración tipo ondas.

Básicamente, el sistema es un montón de partículas que se mueven con un flujo suave, pero cuando el mouse se acerca, reaccionan. No huyen como locas, solo se desplazan un poco formando una especie de onda alrededor del cursor, no quiero nada tan alocado, sol un movimiento "suave"






```js
let particles = [];
let total = 350;

function setup() {
  createCanvas(900, 600);
  colorMode(HSB, 360, 100, 100, 100);
  background(230, 40, 10);

  for (let i = 0; i < total; i++) {
    particles.push(new Petal());
  }
}

function draw() {
  fill(230, 40, 10, 15);
  noStroke();
  rect(0, 0, width, height);

  for (let p of particles) {
    p.applyFlow();
    p.softRepel();
    p.oscillate();
    p.update();
    p.display();
  }
}

class Petal {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.maxSpeed = 2;
    this.noiseOffset = random(1000);
    this.baseHue = random(180, 320);
    this.size = random(3, 6);
  }

  applyFlow() {
    let angle = noise(this.position.x * 0.002, this.position.y * 0.002, frameCount * 0.002) * TWO_PI * 2;
    let flow = p5.Vector.fromAngle(angle);
    flow.setMag(0.1);
    this.acceleration.add(flow);
  }

  softRepel() {
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(this.position, mouse);
    let d = dir.mag();

    if (d < 150) {
      let strength = map(d, 0, 150, 0.5, 0);
      dir.setMag(strength);
      this.acceleration.add(dir);
    }
  }

  oscillate() {
    let wave = sin(frameCount * 0.05 + this.noiseOffset) * 0.05;
    let perp = createVector(-this.velocity.y, this.velocity.x);
    perp.setMag(wave);
    this.acceleration.add(perp);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }

  display() {
    let hueShift = sin(frameCount * 0.02 + this.noiseOffset) * 20;
    let finalHue = (this.baseHue + hueShift + 360) % 360;

    noStroke();
    fill(finalHue, 70, 100, 80);
    ellipse(this.position.x, this.position.y, this.size);
  }
}

function keyPressed() {
  if (key === ' ') {
    for (let p of particles) {
      p.velocity.mult(-1);
    }
  }
}


```

<img width="753" height="570" alt="image" src="https://github.com/user-attachments/assets/bd77f296-0240-4006-ab5c-950db627a4c6" />


Repulsión suave al mouse 
Cuando el mouse se acerca, se aplica una fuerza que empuja las partículas hacia afuera

Motion 101:
primero la velocidad se actualiza sumándole la aceleración, luego la posición se actualiza sumándole la velocidad, después limito la velocidad para que no crezca sin control y finalmente reinicio la aceleración en cada frame, esa secuencia es la base de todo el comportamiento. La aceleración es la que define cómo se quiere mover la partícula en ese instante (si fluye, si se aleja del mouse, si vibra). La velocidad acumula ese efecto a lo largo del tiempo, generando continuidad en el movimiento. Y la posición simplemente refleja el resultado final en pantalla. Si no limitara la velocidad, las partículas empezarían a moverse cada vez más rápido hasta volverse incontrolables. Y si no reiniciara la aceleración, las fuerzas se acumularían indefinidamente, por eso Motion 101 funciona como el motor del sistema, organiza y controla toda la dinámica del movimiento



[p5js_Codigo_Unidad2](https://editor.p5js.org/juliSf22/sketches/CtqU-vh0w)


## Bitácora de reflexión











