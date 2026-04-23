# Unidad 7

## Bitácora de proceso de aprendizaje


#### Actividad 1:

el del tunel:
<img width="329" height="334" alt="image" src="https://github.com/user-attachments/assets/62ff8c76-ff0c-4e6c-bc1b-e9028137a97e" />
me parece muy chevere porque es claro donde está expresando/ mostrando el tunel, no impide que se pueda leer correctamente la palabra pero si hace que digas :o claro, un tunel  


sonrisa:
<img width="336" height="336" alt="image" src="https://github.com/user-attachments/assets/5370ba39-3082-4bb3-a42c-901572984a20" />

esto muestra como claramente podemos persivir en este caso la "l" cambiandola ligeramente para que funja como una sonrisa sin que pierda su caracteristica distintiva

Panama:

<img width="337" height="331" alt="image" src="https://github.com/user-attachments/assets/ae79aedc-4209-4dfa-9fd4-7fba84907e5f" />

este es chidoporque puede pasar desapersivido si no conoces el "contexto" o pues no conoces al pais, pero si si lo conoces sabes perfectamente que representa al canal de panama


##### 3) podri pensar en:

- Ondas
- elastico
- Boom

me interesa el elastico y el boom porque ya estoy pensando que hacer con cada una

## Bitácora de aplicación 

````js
const {
  Engine,
  World,
  Bodies,
  Body,
  Constraint,
  Mouse,
  MouseConstraint,
  Render
} = Matter;

let engine, world;
let letterL;
let mouseConstraint;
let pullPoint;

function setupMatter() {
  engine = Engine.create();
  world = engine.world;

  // ❌ SIN GRAVEDAD
  engine.gravity.y = 0;

  const render = Render.create({
    element: document.body,
    engine: engine,
    options: {
      width: window.innerWidth,
      height: window.innerHeight,
      wireframes: false,
      background: "#111"
    }
  });

  Render.run(render);
  Engine.run(engine);

  // 📌 UNA SOLA "L" (cuerpo compuesto)
  const centerX = window.innerWidth / 2;
  const centerY = window.innerHeight / 2;

  const vertical = Bodies.rectangle(centerX, centerY, 40, 300, {
    render: { fillStyle: "white" }
  });

  const horizontal = Bodies.rectangle(centerX + 120, centerY + 130, 300, 40, {
    render: { fillStyle: "white" }
  });

  letterL = Body.create({
    parts: [vertical, horizontal],
    frictionAir: 0.08
  });

  World.add(world, letterL);

  // 🎯 punto de “estiramiento”
  pullPoint = Constraint.create({
    pointA: { x: centerX, y: centerY },
    bodyB: letterL,
    pointB: { x: 0, y: 0 },
    stiffness: 0.02,
    length: 0
  });

  World.add(world, pullPoint);

  // 🖱️ mouse control
  const mouse = Mouse.create(render.canvas);

  mouseConstraint = MouseConstraint.create(engine, {
    mouse: mouse,
    constraint: {
      stiffness: 0.2,
      render: { visible: false }
    }
  });

  World.add(world, mouseConstraint);

  // 👇 mover punto de estiramiento con el mouse
  render.canvas.addEventListener("mousemove", (e) => {
    pullPoint.pointA.x = e.clientX;
    pullPoint.pointA.y = e.clientY;
  });
}

setupMatter();
````


## Bitácora de reflexión
