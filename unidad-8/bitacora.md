
## Bitácora de proceso de aprendizaje

### Actividad 01:
#### Indica qué herramienta te interesa explorar y por qué:
Blender, por el módulo de Geometry Nodes. Esta herramienta la verdad me asusta porque hay que meterle mucha logica par que se fea como quieres y además nunca la he provado entoncews es una buena oportunida, llevándola al modelado y la animación 3D. Con p5.js ya aprendí a manejar la lógica matemática de sistemas complejos (como fuerzas, físicas o ruido). Geometry Nodes me permite aplicar esa misma lógica procesal para modificar mallas, crear animaciones interactivas

#### Explica qué relación tiene esa herramienta con tu línea de énfasis o interés profesional:
Entretenimiento Digital enfasis en la animación los Geometry Nodes son el estándar actual para crear diferentes efectos importantisimos. los Technical Artist o Motion Designer son perfiles altísimamente valorados que saben construir sistemas inteligentes que resuelven problemas visuales.

#### Busca 2 o 3 referentes realizados con esa herramienta o cercanos a su ecosistema:

- vario donde se hacen efectos como de escamas que puede verse interactivo

- tipografias movidas y animadas unicamente por geomety nodes

#### Explica qué te interesa de esos referentes:

- lo de las tipografias está super chevere porque si lo comparamos con una animacion hecha a mano es infinitamente más facil de hacer
- los geomety nodes puede darnos la posibilidad de hacer animaciones que influencian otras cosas

#### Propón uno o dos posibles contextos profesionales para tu pieza final:

- textos para comerciales o vizualizers
- ayuda en animaciones y efectos complejos de hacer con animacion

### Actividad 02:
El sistema que voy a transferir es un sistema de fuerzas y proximidad aplicado a tipografía semántica animada. En p5.js trabajábamos sistemas donde los objetos reaccionaban según distancia, atracción, repulsión y comportamiento espacial. Decidí llevar esa lógica a Blender usando Geometry Nodes, específicamente utilizando Geometry Proximity como base del sistema

#### ¿Cómo funcionaba en p5.js?

En p5.js estos sistemas funcionaban mediante cálculos de distancia entre partículas u objetos. Dependiendo de esa distancia, los elementos podían: acercarse,alejarse,deformarse,cambiar de dirección,o modificar propiedades visuales.

La lógica principal era convertir la proximidad en una fuerza o influencia. 

#### Justifica por qué quieres transferirlo a la herramienta elegida:

He transferido el sistema a Blender porque Geometry Nodes permite trabajar con lógica procedural y sistemas generativos de forma visual y espacial en 3D. A diferencia de p5.js, Blender integra simulación, geometría procedural, materiales, iluminación, cámara y composición cinematográfica. Geometry Nodes ofrece herramientas ideales para este tipo de sistemas: Geometry Proximity, campos, atributos, instancias y deformación procedural. El principio lógico sigue siendo el mismo: usar distancia y fuerzas para generar comportamiento dinámico. Lo que cambia es el medio y el potencial visual

#### Explica qué tipo de pieza visual te imaginas construir con esa combinación:

La pieza propuesta es una tipografía reactiva: varias palabras generan campos de influencia sobre una superficie procedural. Cada letra actúa como un centro de fuerza que altera la geometría cercana, bajando partes de la malla, deformando el espacio

Visualmente, busca inspirarse en los gráficos generativos sobrios, que suelen están loop motion graphics experimentales

#### Señala qué dificultades técnicas anticipas:

- controlar correctamente los atributos y materiales dentro de Geometry Nodes
- y controlar cómo interactúan varias fuerzas al mismo tiempo
- que cada palabra tenga su diferencial
  
### Actividad 03:
#### Describe qué componentes o módulos necesitas aprender en tu herramienta:

el geometry node es el más importante y la base del sistema pero su hermanito sería el map range

<img width="1116" height="744" alt="image" src="https://github.com/user-attachments/assets/2d5e4fa7-d826-4816-836f-1a6516ead2bc" />

<img width="1038" height="650" alt="image" src="https://github.com/user-attachments/assets/f56dd055-e0d8-4d8c-8607-00b76f8a2a00" />

estaba mirando cual de lás 2 opciones quedaba mejor pero como sea lo que ya está resuelto es que si funciona la "interactividad"

pues la verdad los colores, se supone que las bolitas se van a pintar del color de la palabra

### Actividad 04:
| Aspecto            | En p5.js                                                               | En Blender / Geometry Nodes                                         | Qué se mantiene                                     | Qué cambia                                                         | Ventajas nuevas                                 | Limitaciones nuevas                                      |
| ------------------ | ---------------------------------------------------------------------- | ------------------------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------ | ----------------------------------------------- | -------------------------------------------------------- |
| Sistema principal  | Sistema de fuerzas y proximidad basado en distancia entre objetos      | Sistema procedural usando Geometry Proximity y deformación de malla | La lógica de influencia espacial y distancia        | El sistema deja de ser código lineal y pasa a ser nodal/procedural | Mayor control visual y espacial en 3D           | Mayor complejidad técnica en la organización de nodos    |
| Proximidad         | Distancia calculada con vectores y operaciones matemáticas             | Geometry Proximity calcula automáticamente cercanía sobre geometría | La distancia sigue controlando comportamiento       | Ahora la proximidad afecta geometría real en espacio 3D            | Más precisión visual y deformaciones complejas  | Más consumo de rendimiento con geometría densa           |
| Movimiento         | Movimiento generado mediante variables y actualización frame por frame | Transformaciones y deformaciones proceduralmente controladas        | El comportamiento dinámico                          | El movimiento se vuelve dependiente de campos y atributos          | Posibilidad de integrar simulación y materiales | Algunas animaciones son menos intuitivas que programando |
| Sistema generativo | Reglas programadas manualmente en código                               | Sistema construido mediante nodos y campos                          | El uso de reglas para generar resultados emergentes | Cambia la forma de pensar el sistema                               | Visualización inmediata de resultados           | Los nodos pueden volverse difíciles de organizar         |
| Materiales y color | Colores controlados por variables y funciones                          | Materiales procedurales y atributos en shaders                      | El color sigue reaccionando al sistema              | El color ahora puede mezclarse espacialmente sobre superficies     | Integración avanzada con iluminación y render   | Configurar atributos puede ser complejo                  |

la lógica detrás del comportamiento generativo es lo realmente importante,los Geometry Nodes cambia la forma de pensar el sistema. En p5.js el enfoque era más matemático y paso a paso, mientras que en Blender trabajas de manera procedural y visual, conectando nodos, campos y atributos.

Esta transferencia me permitió entender cómo un mismo sistema puede ganar nuevas posibilidades expresivas según la herramienta que uses. En Blender, el sistema adquiere profundidad espacial, materiales, iluminación acercándose más al motion graphics profesional y a la visualización generativa actual

## Bitácora de aplicación 

### Herramienta elegida
Blender 4.2 Geometry Nodes
es la heramienta con la que mas estoy familiarizada y me interesa aprender bastante de esta, más una parte tan importante como los Geometry Nodes

### Sistema transferido

El sistema que voy a transferir es un sistema de fuerzas y proximidad aplicado a tipografía semántica animada

### Contexto profesional concreto

textos para comerciales o vizualizers y obio con un poco más de trabajo para portafolio

### Concepto visual

pues la idea esque asemejara a una de esas animaciones en loop, pero pues aprovehando las palabras para que interactuen diferente y no sea tán repetitivo


### Referencias

<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/87d9ee93-62d5-43ce-840f-3049e081b858" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/871029f3-7630-4766-bd64-fd28f5074f42" />
<img width="1344" height="576" alt="image" src="https://github.com/user-attachments/assets/2280b854-be75-49ea-a6ea-4aedca50570d" />

### Bocetos

<img width="1309" height="693" alt="image" src="https://github.com/user-attachments/assets/a4030909-f4b4-41a1-b36b-b5c50e6a26f5" />
<img width="1457" height="719" alt="image" src="https://github.com/user-attachments/assets/a63394cc-3daa-4e1f-88fa-acce16463b17" />

### Explicación de transferencia

El principio que se mantiene es la lógica de influencia espacial y distancia: en ambos entornos, la proximidad entre elementos genera comportamiento dinámico. Sin embargo, la implementación cambia drásticamente. En p5.js se trabajaba con código lineal, actualizando fuerzas y posiciones frame por frame mediante vectores y operaciones matemáticas. En Blender, el mismo sistema se reconstruye de forma procedural y visual mediante nodos, campos y atributos. La proximidad pasa de ser un cálculo manual con vectores a usar el nodo Geometry Proximity, que afecta directamente a la geometría 3D real. Las ventajas nuevas son evidentes: se obtiene control espacial inmediato, deformaciones complejas sobre mallas, integración con materiales, iluminación y render profesional

### Mapa de decisiones

decidí que queria hacer de esas animaciones en loop queria que fuera un objeto pero luego me decidí por una palabra para poder ponerle tambien una reaccion al color

## Bitácora de reflexión
