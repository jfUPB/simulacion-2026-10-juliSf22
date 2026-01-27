# Unidad 1

## Bitácora de proceso de aprendizaje

### analisis del segundo video https://www.youtube.com/watch?v=_8DMEHxOLQE

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


### aActividad 4:

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



## Bitácora de reflexión


estuvo chevere :)



