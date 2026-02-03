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



## Bitácora de aplicación 



## Bitácora de reflexión







