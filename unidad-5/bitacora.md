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

pues se genera, y con fuerzas (que se calculan cada frame cada frame) generan movimiento



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




[editar](https://editor.p5js.org/juliSf22/sketches/28kmEcal5)
[ver](https://editor.p5js.org/juliSf22/full/28kmEcal5)




## Bitácora de reflexión
