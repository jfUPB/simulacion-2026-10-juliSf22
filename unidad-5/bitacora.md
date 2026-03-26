# Unidad 5
## Bitácora de proceso de aprendizaje
[simulacion texto guia](https://juanferfranco.github.io/simulacion-2026-10/)

se debe recorrer de atras para adelante. porque se tienen que elimiar lás más viejas osea las que se crearon primero

### Actividad 1: 
¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?
tiene pues sis fisicas y eso pero lo más importante es que tienen un tiempo de vida definido, osea que al momento de crearse ya tenga un tiempo de vida para eliminarse, esto para no saturar y ahorrar recursos del PC

¿Qué condición determina que una partícula “muere”? ¿Es una muerte instantánea o gradual?

el tiempo de vida, so esto se mescla con el cambio en la opacidad de la misma particula, pues provoca que la particula a medida que se hace más vieja tambien de la persepcion de que está desapareciendo

¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula.

pues se genera, y con fuerzas (que se calculan cada frame cada frame) generan movimiento, En cada frame se sigue el esquema de Motion 101, Al mismo tiempo, el lifetime disminuye constantemente, reflejando el envejecimiento de la partícula

¿Quién crea las partículas? ¿Cuándo?
Las partículas son generadas desde el programa principal, normalmente dentro de la función draw(), por lo que se crean de manera continua en cada frame

¿Quién decide eliminarlas?
El sistema principal controla cuándo eliminar una partícula del arreglo. La partícula solo indica si ya “murió”, pero no se elimina por sí misma

¿Por qué recorrer el array en orden inverso?
Se recorre en orden inverso porque al eliminar elementos, los índices cambian. Si se hiciera hacia adelante, algunas partículas podrían saltarse y no evaluarse correctamente, causando fallos en el sistema

¿Qué pasa si no se eliminan?
Si nunca se eliminaran, el arreglo crecería indefinidamente, consumiendo más memoria y reduciendo el rendimiento, lo que provocaría una caída notable en el frame rate

¿Cómo se representa una partícula?
Visualmente, cada partícula se muestra como una figura simple (generalmente un círculo) con color y nivel de transparencia

Relación entre tiempo de vida y apariencia
El lifetime controla la transparencia: a medida que disminuye, la partícula se vuelve más tenue hasta desaparecer completamente

### Actividad 2

¿Qué responsabilidades pasaron a la clase Emitter?
En el ejemplo anterior, draw() manejaba todo: crear partículas, almacenarlas, recorrer el arreglo, actualizarlas y eliminarlas. Ahora, esas tareas se trasladan al Emitter, que se encarga internamente de todo ese proceso. El draw() solo le indica al emisor que ejecute su ciclo (run())

Ventaja de encapsular la lógica
La principal ventaja es la organización y escalabilidad. Al tener emisores independientes, puedes manejar múltiples sistemas (como humo, fuego o lluvia) sin complicar el código principal ni mezclar responsabilidades

¿Quién crea los emisores y quién las partículas?
El programa principal crea los emisores y los guarda en un arreglo. Luego, cada emisor genera sus propias partículas dentro de su estructura interna
[editar](https://editor.p5js.org/juliSf22/sketches/28kmEcal5)

### Actividad 3: 
¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?


Todas las subclases comparten lo básico porque heredan de la clase principal: posición, velocidad, aceleración y lifespan. También usan el mismo comportamiento para actualizarse y para saber cuándo desaparecen
Lo diferente está en cómo se ven y en pequeños cambios propios. Por ejemplo, una puede dibujarse como círculo y otra como un cuadrado que gira, agregando cosas extra como un ángulo.

¿Por qué es importante que el Emitter no necesite saber qué tipo específico de partícula está gestionando?


Porque así el código se mantiene simple. El emisor no tiene que estar preguntando qué tipo es cada partícula, solo las recorre y les dice que se actualicen y se dibujen. Cada una ya sabe cómo hacerlo. Eso hace que sea más fácil agregar nuevos tipos sin romper nada.

Si quisieras agregar un tercer tipo de partícula, ¿qué tendrías que crear y qué NO tendrías que modificar?


Tendrías que crear una nueva clase que herede de la partícula base y cambiar cómo se dibuja. También tocar un poco la parte donde se crean para incluir ese nuevo tipo.
No tendrías que modificar la lógica principal: ni cómo se actualizan, ni cómo se eliminan, ni cómo el emisor recorre el arreglo.

Compara con Example 4.2: ¿Cambió la lógica del Emitter? ¿Cambió la lógica de muerte? ¿Qué capa se modificó y cuáles quedaron intactas?


No cambió ni la lógica del emisor ni la forma en que las partículas mueren, todo eso sigue igual
Se mantiene igual la parte de estructura y la base del comportamiento. Lo que cambia es la parte visual y la forma en que se crean distintos tipos de partículas

### Actividad 4:

¿Dónde se define la gravedad y quién la aplica? ¿Es global o local?:


 La gravedad se define en el entorno principal. El sistema de partículas se encarga de aplicarla a cada partícula. Es una fuerza global porque afecta a todas por igual.

¿Qué diferencia hay entre la gravedad y el repeller?:


 La gravedad es constante y viene del entorno general. El repeller está en su propia clase y calcula la fuerza dependiendo de la posición de cada partícula. Por eso la gravedad es global y el repeller es local.

¿Qué principio físico se está modelando?:


 Se basa en una relación donde la fuerza depende de la distancia, más cerca es más fuerte. Es como la Ley de Gravitación Universal de Newton.

¿Cambió la clase Particle entre 4.6 y 4.7? ¿Qué implica?: 


 No cambió. Eso significa que la partícula está separada de las fuerzas. Solo recibe vectores y los aplica, sin importar de dónde vienen.

---

**Tabla comparativa**

| Aspecto                 | 4.2          | 4.4          | 4.5          | 4.6          | 4.7          |
| ----------------------- | ------------ | ------------ | ------------ | ------------ | ------------ |
| ¿Quién crea partículas? | draw()       | Emisor       | Emisor       | Emisor       | Emisor       |
| ¿Hay emisor?            | No           | Sí           | Sí           | Sí           | Sí           |
| ¿Hay herencia?          | No           | No           | Sí           | No           | No           |
| ¿Hay fuerzas externas?  | No           | No           | No           | Sí           | Sí           |
| ¿Hay interacción?       | No           | No           | No           | No           | Sí           |
| ¿Cómo mueren?           | lifespan ≤ 0 | lifespan ≤ 0 | lifespan ≤ 0 | lifespan ≤ 0 | lifespan ≤ 0 |

---
¿Qué cambiaste?:


 Solo cambié la dirección del vector en el repeller, multiplicándolo por -1.

¿Qué modificaste?:


 Solo el método del repeller que calcula la fuerza.

¿Qué no tocaste?:


 No cambié ni la partícula, ni el sistema, ni el draw().

¿Por qué funcionó sin romper todo?: 


 Porque cada parte está separada. El repeller solo manda una fuerza, y el resto del sistema la usa igual sin importar cómo se calculó.



## Bitácora de aplicación 

<img width="966" height="584" alt="image" src="https://github.com/user-attachments/assets/7cdea1b6-d202-4f84-95c7-f1a0dda0a0c6" />


### Fase1: 
en la priemera fase queria que se vea un arbol de cerezo que lentamente vaya soltando florecitas(particulas) que cahen he interactuan con el suelo, ya que tienen fisicas

### Fase2:

una vez caen pueden tener diferentes interacciones como lo es el viento y un golpe que las levanta "como lo harian en la vida real" luego de un tiempito estas se transforman entrando a la fase3

### Fase3:

para la ultima fase de transformacion se convierten en hojas, reprecentando como cuando se marchitan las flores y una vez marchitas estas entran en la tierra para luego subir y darle nutrientes al arbol para continuar el cilo.




### Mapa De Deciciones:

**por qué un arbol?** es un ejemplo muy lindo de la vida, aparte que se ve super lindo, obviamente las particulas tenddrían que ser emojis de flores de cerezo

**fuerzas e interaccion:** la gravedad obviamente para que caigan y emulen un poco la vida real, aparte de una fuerza cuando arrastres el mouse simulando un brisa o el viento, tambien pues cuando alquien "pise" muy duro el suelo que hace que se levanten un poco lás hojas del suelo.

**ParticleLife:** la particula tiene diferentes comportamientos a lo largo de este proyecto, por lo que lo voy a dividir para mejor explicacion:

- flores: caen y se transforma en hojas despues de un tiempo
- hojas: bajan un poco, van hacia el centro del arbol donde empiezan a subir mientras lentamente se hacen más pequeñas hasta desaparecer

**Shaders:** el shader solo afectará a las hojas porque es una especie de retroalimentacion visual de que dan "nutrientes" o revitalizan el arbol

**otros efectos:** en otros efectos están el hecho de que cuando desaparecen/mueren las particulas de las hojas hay una especie de luz en el arbol para enfatizar la narrativa.

**por qué esa condicion de muerte** porque cierra muy bien el ciclo, es un arbol que se autosostiene, esta condicion de muerte de las particulas mesclada con el cambio hacen que se entienda el mensaje o la intencion que tengo.

````js
let particles = [];
let mic, tableY, imgArbol;
let audioStarted = false;
let myShader, layer, glowLayer;


let lastSpawn = 0;
let spawnInterval = 1000;


let windForce = 0;


let treeFlash = 0;


const vertShader = `
precision mediump float;
attribute vec3 aPosition;
attribute vec2 aTexCoord;
varying vec2 vTexCoord;
void main() {
    vTexCoord = aTexCoord;
    vec4 positionVec4 = vec4(aPosition, 1.0);
    positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
    gl_Position = positionVec4;
}`;

const fragShader = `
precision mediump float;
varying vec2 vTexCoord;
uniform sampler2D tex0;
void main() {
    vec2 uv = vec2(vTexCoord.x, 1.0 - vTexCoord.y);
    vec4 col = texture2D(tex0, uv);
    vec4 bloom = vec4(0.0);
    for(float i = -2.0; i <= 2.0; i++) {
        for(float j = -2.0; j <= 2.0; j++) {
            bloom += texture2D(tex0, uv + vec2(i, j) * 0.002);
        }
    }
    bloom /= 25.0;
    gl_FragColor = col + bloom * 1.5;
}`;

function preload() {
  imgArbol = loadImage('./arbol.png');
}

function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  myShader = createShader(vertShader, fragShader);

  layer = createGraphics(windowWidth, windowHeight);
  glowLayer = createGraphics(windowWidth, windowHeight);

  layer.imageMode(CENTER);
  layer.textAlign(CENTER, CENTER);
  glowLayer.textAlign(CENTER, CENTER);

  tableY = height - 100;
  mic = new p5.AudioIn();
}

function draw() {
  if (!imgArbol || imgArbol.width <= 0) return;

  layer.clear();
  glowLayer.clear();

  // FONDO
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(180, 120, 200), color(255, 180, 130), inter);
    layer.stroke(c);
    layer.line(0, y, width, y);
  }

  // ÁRBOL
  let escala = height * 0.85;
  layer.image(imgArbol, width / 2, height / 2, escala * (imgArbol.width/imgArbol.height), escala);

  // ✨ FLASH SUAVE (SIN BORDES DUROS)
  if (treeFlash > 0) {
    layer.noStroke();

    let maxR = escala * 0.6;

    for (let i = 0; i < 5; i++) {
      let r = map(i, 0, 4, maxR * 0.2, maxR);
      let alpha = map(i, 0, 4, treeFlash, 0);

      layer.fill(255, 220, 180, alpha * 0.4);
      layer.ellipse(width/2, height/2, r);
    }

    treeFlash *= 0.9; // más suave
  }

  // SUELO
  layer.noStroke();
  layer.fill(60, 40, 30);
  layer.rect(0, tableY, width, 100);

  if (audioStarted) {
    let micLevel = mic.getLevel();
    let wind = createVector(windForce, 0);

    if (millis() - lastSpawn > spawnInterval) {
      particles.push(new Particle());
      lastSpawn = millis();
      spawnInterval = random(900, 1600);
    }

    for (let i = particles.length - 1; i >= 0; i--) {
      let p = particles[i];

      if (!p.isFeeding) {
        p.applyForce(createVector(0, 0.15));
        p.applyForce(wind);

        if (micLevel > 0.05 && p.pos.y >= tableY - 5) {
          p.vel.y = map(micLevel, 0.05, 1, -4, -15);
          p.lifespan = 255;
        }
      } else {
        let centro = width / 2;

        if (!p.hasDropped) {
          p.vel.y = 2;
          p.dropTimer--;
          if (p.dropTimer <= 0) p.hasDropped = true;
        } else {
          let dx = centro - p.pos.x;
          p.vel.x += dx * 0.05;
          p.vel.x *= 0.8;

          if (abs(dx) < 20) {
            p.pos.x = lerp(p.pos.x, centro, 0.2);
            p.vel.y = -6;
            p.size *= 0.95;
            p.fade *= 0.94;
          } else {
            p.vel.y *= 0.5;
          }
        }
      }

      p.update();

      if (p.isFeeding) {
        p.show(glowLayer);
      } else {
        p.show(layer);
      }

      if (p.isDead()) {
        treeFlash = 80; // antes 150 → ahora más suave
        particles.splice(i, 1);
      }
    }
  } else {
    layer.fill(255);
    layer.textSize(32);
    layer.text("🌸 Click para iniciar", width/2, height/2);
  }

  resetShader();
  image(layer, -width/2, -height/2);

  shader(myShader);
  myShader.setUniform('tex0', glowLayer);
  rect(-width/2, -height/2, width, height);
}

function mousePressed() {
  if (!audioStarted) {
    userStartAudio();
    mic.start();
    audioStarted = true;
  }
}

function mouseDragged() {
  windForce = movedX * 0.02;
}

function mouseReleased() {
  windForce = 0;
}

class Particle {
  constructor() {
    this.pos = createVector(
      random(width * 0.3, width * 0.7),
      random(height * 0.25, height * 0.45)
    );

    this.vel = createVector(random(-1, 1), random(1, 2));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.size = random(20, 35);
    this.fade = 1;

    this.emoji = '🌸';
    this.isFeeding = false;
    this.rot = random(TWO_PI);

    this.hasDropped = false;
    this.dropTimer = 20;
  }

  applyForce(f) { this.acc.add(f); }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.y >= tableY) {
      if (!this.isFeeding) {
        this.pos.y = tableY;
        this.vel.y *= -0.1;

        if (abs(this.vel.y) < 0.2) this.vel.y = 0;
        if (this.vel.mag() < 0.3) this.vel.set(0, 0);
      }

      this.lifespan -= 2.5;

      if (this.lifespan < 160) {
        this.emoji = '🍂';
        this.isFeeding = true;
      }
    } else if (!this.isFeeding) {
      this.rot += 0.05;
    }
  }

  show(c) {
    c.push();
    c.translate(this.pos.x, this.pos.y);
    c.rotate(this.rot);

    let alpha = this.isFeeding ? 255 * this.fade : this.lifespan;

    c.fill(255, alpha);
    c.textSize(this.size);
    c.text(this.emoji, 0, 0);

    c.pop();
  }

  isDead() {
    return this.lifespan <= 0 || this.size < 2 || this.fade < 0.05 || this.pos.y < -100;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  layer = createGraphics(windowWidth, windowHeight);
  glowLayer = createGraphics(windowWidth, windowHeight);
} 
````

[ver](https://editor.p5js.org/juliSf22/full/28kmEcal5)

#### cuando son florecitas

<img width="729" height="564" alt="image" src="https://github.com/user-attachments/assets/a7434857-1772-4863-a598-b55ae1301c5b" />



#### cuando se transforma en hojas

<img width="674" height="563" alt="image" src="https://github.com/user-attachments/assets/00c4179a-0818-4ea3-9c3a-e71541f83ad6" />




#### cuando mueren y dan un feedback visual


<img width="523" height="596" alt="image" src="https://github.com/user-attachments/assets/cc72a6e0-dda7-4abe-9485-11b871120514" />



## Bitácora de reflexión

1) Una partícula es una entidad con estado.
- este principio indica que una partícula no es solo un objeto, sino que también tiene un conjunto de propiedades que describen su condición en un momento dado, gracias a ese conjunto de valores  puede determinar cómo se comporta y cómo cambia con el tiempo

2) Una partícula tiene ciclo de vida.
- las particulas cuentan con diferentes etapas en la vida representado con estados donde unos de los más importantes y fundamentales son su "nacimiento y muerte"
  
3) Un sistema de partículas gestiona colecciones dinámicas de elementos.
- un sistema de particulas maneja muchas particulas al mismo tiempo las cuales cambian/evolve constantemente

4) La creación y eliminación de partículas no es un detalle técnico menor, sino parte central del modelo.   
- es muy importante, no se puedem crear particulas infinitamente sin que "mueran" porque el rendimiento se verá muuuuuy afectado

5) Debe haber separación entre la lógica de una partícula individual y la lógica del sistema/emisor.
- porque el sistema emisor es el que maneja la creación de las particulas como tal, pero la logica de las particulas puede variar sin afectar su emision osea pueden haber varios tipos de particulas las cuales son manejadas por el mismo emisor
  
6) Un emisor o particle system es una abstracción importante.
- cuando abstraes un sistema lo que haces es mantener lo importante por lo que ves el funcionamiento del sistema más a lo general

7) Pueden existir sistemas de sistemas.
- este principio significa que un sistema de partículas puede formar parte de otro sistema más grande osea, pueden existir varios sistemas trabajando en conjunto

8) Puede haber heterogeneidad usando herencia y polimorfismo.
- permite tener distintos tipos de partículas con comportamientos diferentes dentro de un mismo sistema, reutilizando estructuras comunes y adaptando lo que cambia

9) Las partículas pueden responder a fuerzas globales y locales.
- si, si pueden

10) La representación visual puede variar sin cambiar el principio algorítmico de fondo.
- la apariencia externa puede variar sin necesidad de que el funcionamiento de la particula cambie

¿Qué se mantendría igual y qué cambiaría? ¿Qué partes de tu diseño son independientes de la herramienta?

- unity: no sabria hacerlo ni con IA :c

- Blender: quedaria más chido

pero en genral la idea no depende del programa en cualquiera se podria representar la misma narrativa solo que con una "skin diferente"
