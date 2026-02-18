# Unidad 1

## Bitácora de proceso de aprendizaje
## Actividad 1
### ¿Qué es un sistema físico interactivo?
Se entiende como la coneccion entre lo fisico y lo digital, por medio de microcontroladores, luces, sonidos, etc.

### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
Me prepara como una persona tecnica y creativa, un campo laboral usualmente muy buscado, como una persona capaz de manejar hardware y software, entendiendo como se conecta el mundo digital con el mundo fisico.

## Actividad 2
### ¿Qué es el diseño/arte generativo?
Se basa en crear un tipo de "reglas" las cuales generan imagenes, sonidos, formmas, etc, de una manera automatica en vez de crear cada elemento a mano.

### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
Me hace capaz de crear experiencias que conecten con el usuario, a la vez que me hace una persona mas creativa, me hace capaz de pasar de diseñar piezas a diseñar sistemas con infinitas variaciones.

## Actividad 4
### ¿Por qué no funcionaba el programa con was_pressed() y por qué funciona con is_pressed()? Explica detalladamente.

El programa no funcionaba con `was_pressed()` porque este método solo detecta el momento exacto en que se presiona el botón y devuelve `True` una sola vez. Eso hacía que el micro:bit enviara `"A"` solo en un instante, y en los siguientes ciclos ya no enviara nada. Como p5.js dibuja en cada frame, el cuadrado cambiaba de color solo un momento y luego volvía al original.

En cambio, `is_pressed()` devuelve `True` mientras el botón esté presionado. Así, el micro:bit envía constantemente `"A"` cuando el botón está oprimido y `"N"` cuando se suelta. Esto permite que p5.js reciba siempre el estado actual del botón y mantenga el color correcto del cuadrado.


## Bitácora de aplicación 
### Programa en p5.js

```js
let port;
let connectBtn;
let connectionInitialized = false;

let x; // posición horizontal del círculo
let y;

function setup() {
  createCanvas(400, 400);
  x = width / 2;
  y = height / 2;

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 350);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);

    if (dataRx == "L") {
      x -= 5;
    } else if (dataRx == "R") {
      x += 5;
    }
  }

  // Limitar movimiento dentro del canvas
  x = constrain(x, 25, width - 25);

  fill("blue");
  circle(x, y, 50);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

```


## Bitácora de reflexión

