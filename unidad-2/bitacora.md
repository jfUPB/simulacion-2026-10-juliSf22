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





## Bitácora de aplicación 



## Bitácora de reflexión




