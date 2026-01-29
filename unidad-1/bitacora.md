# Unidad 1

## Bitácora de proceso de aprendizaje

### analisis del segundo video

https://www.youtube.com/watch?v=_8DMEHxOLQE

nos dice que se trata de crear imagenes a partir de un codigo, el cual iteras muchas veces, reglas simples que juntas pueden crear cosas increibles, no tener un camino que seguir, practicamente todas las veces que el software se ejecuta lo hace de manera diferente, por más que las computadoras son conocidas por su alta precision, el que puedan hacer cosas inesperadas hace que dibujar con codigo sea emocionante.
diseña un conjunto de reglas, un sistema. no un resultado final, la aleatoriedad se usa para variar el resultado y que no sea igual.

strudel

# estan vivoooooooos!!!!!


## Bitácora de aplicación 

### actividad 2:
quiero hacer 2 experimentos por lo que voy a hacer 2 predicciones 

1: cambio el  step()


```
 step() {
    const choice = floor(random(4));
    if (choice < 1) {
      this.x++;
    } else if (choice < 2) {
      this.x--;
    } else if (choice < 3) {
      this.y++;
    } else {
      this.y--;
    }
  }

```
acá lo que hice fue quitar los iguales y usar < lo que pienso que va a pasar es que va a quedar practicamente igual



<img width="1455" height="645" alt="image" src="https://github.com/user-attachments/assets/67d2e81f-0dbc-4f42-bb0c-8d56a8ade4d1" />





luego de hacerlo creo que si es un resultado muy parecidoal de el cod original maybe un poco más pegados




2: cambio 2
```
 step() {
    const choice = (random(4));
    if (choice < 1) {
      this.x++;
    } else if (choice < 2) {
      this.x--;
    } else if (choice < 3) {
      this.y++;
    } else {
      this.y--;
    }
  }

```
pensé que cambiaria más




<img width="1636" height="779" alt="image" src="https://github.com/user-attachments/assets/d8be8efd-894f-4812-b67a-d080ea4e9c07" />




pero la verdad no, sigue siendo bastante parecido a el original solo que ya no redondea por lo que asumo yo que es más probable que salgan varias veces ejemplo un numero menor a 1 ya que como no se redondean los decimales entran y puede llegar a hacer una lidea más larga si entra varias veces ahí por eso se ve más separado que el anterior.


### Actividad 3

distribución uniforme: todos los valores posibles tienen la misma probabilidad de ocurrir 

 
distribución no uniforme: algunos valores tienen más probabilidad que otros, Los números siguen siendo aleatorios pero con una tendencia marcada a donde tenga más probabilidad de ocurrir, en cierto modo dicta un poco o bueno hace un poco más preedcible el resultado del sistema.



 usamos la  randomGaussian(media, desviación)

```
 let stepX = randomGaussian(0.5, 0.5);
  let stepY = randomGaussian(0, 0.5);

  this.x += stepX;
  this.y += stepY;
```
 
 <img width="1547" height="635" alt="image" src="https://github.com/user-attachments/assets/34a94ee2-fb2d-4e3e-9caf-9e8244c0c012" />

  
como la media es la tendencia central pues con un 0.5 en el eje x nos da una inclinacion a que se vaya hacia la derecha


### Actividad 4:

```

function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  
  let x = randomGaussian(320, 120);
  noStroke();
  
  
  let y = randomGaussian(320, 120);
  noStroke();
  
  fill(0, 10);
  circle(x, y, 15);

}


```

https://editor.p5js.org/juliSf22/sketches/Wk7DYZtdj


<img width="1464" height="489" alt="image" src="https://github.com/user-attachments/assets/8b6cd071-0091-4741-88d6-2bc4af9b7d7c" />

### Actividad 5
```
let xoff = 0;
let yoff = 0;

function setup() {
  createCanvas(600, 400);
  background(255);
}

function draw() {
  stroke(0, 150); 
  let x = 0;
  xoff = 0;

  while (x < width) {
  
    let y = noise(xoff, yoff) * height * 1;
    line(x, height, x, height - y);

    xoff += 0.2 ;
    x += 10;
  }

  yoff += 0.01; 
}
```


### Actividad 6
```
let xoff = 0;
let yoff = 0;

function setup() {
  createCanvas(600, 400);
  background(255);
}

function draw() {
  stroke(0, 150); 
  let x = 0;
  xoff = 0;

  while (x < width) {
  
    let y = noise(xoff, yoff) * height * 1;
    line(x, height, x, height - y);

    xoff += 0.2 ;
    x += 10;
  }

  yoff += 0.01; 
}
```
<img width="610" height="413" alt="image" src="https://github.com/user-attachments/assets/cc623755-13dd-432b-aa93-3a7029db5183" />


### Actividad 7
```
let walkers = [];
let numWalkers = 50;
let noiseScale = 0.01;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(10);
  for (let i = 0; i < numWalkers; i++) {
    walkers.push(new Walker(random(width), random(height)));
  }
}

function draw() {

  for (let w of walkers) {
    w.update();
    w.display();
  }
}

class Walker {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.t = random(1000);
  }

  update() {
    // ruido Perlin
    let angle = noise(this.pos.x * noiseScale,
                      this.pos.y * noiseScale,
                      this.t) * TWO_PI * 2;

    let stepSize;

    // Lévy flight salto largo
    if (random(1) < 0.02) {
      stepSize = pow(random(1), -1.5) * map(mouseX, 0, width, 2, 15);
    } else {
      stepSize = randomGaussian(2, 0.5);
    }

    let velocity = map(mouseY, 0, height, 0.5, 3);

    this.pos.x += cos(angle) * stepSize * velocity;
    this.pos.y += sin(angle) * stepSize * velocity;

    this.t += 0.01;

    // Bordes infinitos
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  display() {
    // distribución normal
    let size = constrain(randomGaussian(4, 1.5), 1, 8);

    // Color ruido Perlin
    let r = map(noise(this.t), 0, 1, 100, 255);
    let g = map(noise(this.t + 50), 0, 1, 50, 200);
    let b = map(noise(this.t + 100), 0, 1, 150, 255);

    noStroke();
    fill(r, g, b, 150);
    ellipse(this.pos.x, this.pos.y, size);
  }
}

function keyPressed() {
  if (key === 'r' || key === 'R') {
    walkers = [];
    for (let i = 0; i < numWalkers; i++) {
      walkers.push(new Walker(random(width), random(height)));
    }
    background(10);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}


```
```
let walkers = []; //crea un arrayd de walkers
let numWalkers = 50; // limitanumero maximo de walkers 50
let noiseScale = 0.01; // esto es para que tenga un movimiento continuo con cambios suabes, no bruscos

function setup() {
  createCanvas(windowWidth, windowHeight); //un canvas de tamaño de la pestaña
  background(10); // casi negro pero no
  for (let i = 0; i < numWalkers; i++) {
    walkers.push(new Walker(random(width), random(height))); 
  } // se repite 50 veces creando los walkers en una posicion ramdom del canvas
}

function draw() { // se ejecuta 60 veces por s

  for (let w of walkers) { // llama w a cada walker
    w.update(); // actualiza la poscicion
    w.display(); // los dibuja
  }
}

class Walker { // es un molde para todos los walkers ya que funcionan igual
  constructor(x, y) { // recive poscicion x,y?
    this.pos = createVector(x, y); // setea un vector en la poscicion actual x , y
    this.t = random(1000); // Da a cada walker un tiempo inicial' aleatorio entre 0 y 1000 para evita que todos tengan los mismos colores y movimientos sincronizados al inicio
  }

  update() {
    // ruido Perlin
    let angle = noise(this.pos.x * noiseScale,
                      this.pos.y * noiseScale,
                      this.t) * TWO_PI * 6; // esto hace que se muevan de forma ramdom pero con cierta tendencia y el 6 hace que pueda tener giros más extremos 

    let stepSize;

    // Lévy flight salto largo
    if (random(1) < 0.02) { // tiene 2% de probabilidad de suceder
      stepSize = pow(random(1), -1.5) * map(mouseX, 0, width, 2, 15); // los saltos largos que se multiplican por un valor que depende de si el mouse en x osea a lo horizontal está a la izquierda 2 o a la derecha 15 por lo que pueden sér más largos dependiendo
    } else {
      stepSize = randomGaussian(2, 0.5); // da un valor promedio de 2 y con una dispercion del 0.5 La mayoría de pasos serán entre 1.5 y 2.5 píxeles
    }

    let velocity = map(mouseY, 0, height, 0.5, 3); // setea una velocidad dependiendo de la poscicion del mouse en vertical siendo arriba 0.5 (lento) y abajo 3(rapido)

    this.pos.x += cos(angle) * stepSize * velocity; // lo que hace es que se muva en x y deoende de la poscicion del mouse para la velocidad y los saltos
    this.pos.y += sin(angle) * stepSize * velocity; // lo que hace es que se muva en y y deoende de la poscicion del mouse para la velocidad y los saltos

    this.t += 0.01; // aumenta el tiempo 0.01 en el parametro this.t (unico para cada walker)

    // Bordes infinitos
    if (this.pos.x > width) this.pos.x = 0; 
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  } // basicamente si se sale del cambas por un lado salga del otro

  display() {
    // distribución normal
    let size = constrain(randomGaussian(4, 1.5), 1, 8); // setea el tamaño como de media 4 con una variabilidad de 1.5 pero que solo esté limitado a 1 o 8

    // Color ruido Perlin
    let r = map(noise(this.t), 0, 1, 100, 255); //en el canal rojo del color crea un ruido que devuelve una cantidad entre 0 y 1 depeendiendo del resultado siendo 0 = 100 y 1 = 255 todo esto en t que se va actualizando 0.01 de antes
    let g = map(noise(this.t + 50), 0, 1, 50, 200); //en el canal verde del color crea un ruido que devuelve una cantidad entre 0 y 1 depeendiendo del resultado siendo 0 = 50 y 1 = 200 todo esto en t + 50 que se va actualizando 0.01 de antes
    let b = map(noise(this.t + 100), 0, 1, 150, 255); //en el canal azul del color crea un ruido que devuelve una cantidad entre 0 y 1 depeendiendo del resultado siendo 0 = 150 y 1 = 255 todo esto en  t + 100 que se va actualizando 0.01 de antes

// el +50 y el +100 se usan para que se cree un degradado y no sea el mismo color siempre

    noStroke();
    fill(r, g, b, 150); // rellena la figura con los colores que seteamos antes y una opacidad
    ellipse(this.pos.x, this.pos.y, size); // crea una elipse en la pscicion actual x, y y el tamaño establecido antes
  }
}

function keyPressed() {
  if (key === 'r' || key === 'R') {
    walkers = [];
    for (let i = 0; i < numWalkers; i++) {
      walkers.push(new Walker(random(width), random(height)));
    }
    background(10);
  }
} // basicamente reinicia el programa a grandes razgos

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
} // ajusta el canvas a la pestaña si esta sufre algún cambio


```

https://editor.p5js.org/juliSf22/sketches/N3fE5KwTg

<img width="937" height="790" alt="image" src="https://github.com/user-attachments/assets/5cf37c33-4a5e-4a34-a789-6c4e6b0ad613" />



## Bitácora de reflexión


estuvo chevere :)









