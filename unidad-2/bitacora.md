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




## Bitácora de aplicación 



## Bitácora de reflexión



