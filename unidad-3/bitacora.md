# Unidad 3

## Bitácora de proceso de aprendizaje
## Actividad 01  

## Proceso de la implementación 
Me llevó a ver cómo extender la máquina de estado que habíamos desarrollado sin romper la lógica que habíamos puesto en funcionamiento. Decidí mantener la estructura de la de eventos (`ENTRY`, `EXIT`, `Timeout`, `A`, `B`) y no adaptar las luces en los estados.

## Modo peatonal
Para implementar el modo de peatonal:
1. Añadí la variable `modo_peatonal`.
2. En el caso de que la variable `modo_peatonal` esté activa:
   1. Si se pulsa el botón `A` en verde:
   2. Se activa la bandera.
   3. El sistema pasa a amarillo.
3. Después de que se produzca el `Timeout` en amarillo:
   1. Si `modo_peatonal` está activa se pasa al estado nuevo `estado_peatonalRed`.
4. En rojo peatonal:
   1. Se mantiene el tiempo normal de rojo.
   2. Después se vuelve al ciclo normal.
Esto permitió respetar la lógica real de un semáforo (no pasar directamente de verde a rojo).

---

## Modo Nocturno
Para el modo nocturno:
1. Si se pulsa el botón `B` desde cualquier estado se va a estado `estado_nocturno`.
2. En este nuevo estado el amarillo parpadea.
3. El parpadeo se implementó aprovechando el mismo evento `Timeout`, alternando a su vez una variable `yellow_on`.
4. No se implementó un evento nuevo (tipo `Blink`) sino que se reutilizó el mismo temporizador.
5. Si se pulsa el botón `A` se vuelve al estado normal (rojo).

---

### Dificultades y errores
- Al principio quise implementar el manejo de luces de manera directa sin modo y eso rompía la coherencia del sistema que habíamos logrado.
- La idea del parpadeo inicialmente lo pensé con un evento nuevo, luego me di cuenta que reutilizando `Timeout` podía hacerlo.
- Era necesario organizar bien las transiciones para no entrar en conflicto entre modos.

---

### Aprendizajes
- Una máquina de estados se puede escalar sin desorganizar el sistema.
- Es importante tener bien separada la lógica de eventos y la visualización.
- El sistema queda más limpio si se reutilizan eventos (ej. `Timeout`).
- Pensar primero en estados me ha permitido no cometer errores antes de ya tener el código.


## Bitácora de aplicación 



## Bitácora de reflexión
