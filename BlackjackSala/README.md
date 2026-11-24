# Sala de blackjack — Parcial de Estructuras de Datos
Autores: Yerson Chilito Molina, Faber Andres Garzon

Programa de consola en Java (sin paquetes, sin librerías externas).

## Abrir y correr en Visual Studio Code

1. Instala el **JDK 8 o superior** y la extensión **Extension Pack for Java** (Microsoft).
2. `Archivo > Abrir carpeta…` y elige la carpeta `BlackjackSala`.
3. Abre `src/Main.java` y pulsa **Run** sobre `main`, o ve a *Ejecutar y depurar*
   y elige una de las tres configuraciones:
   - **Interfaz gráfica** ← ventana con la mesa, el grafo y la corrida
   - **Menú**
   - **Corrida fija (verificación)** ← la que se califica
   - **Modo libre** (mazo barajado)

### Desde la terminal

```bash
javac -encoding UTF-8 -d bin src/*.java
java -cp bin Main fija      # corrida de verificación
java -cp bin Main libre     # modo libre
java -cp bin Main sala      # solo Dijkstra, Prim y Kruskal
java -cp bin Main           # menú
java -cp bin Interfaz       # interfaz gráfica (igual: java -cp bin Main gui)
```

Si en Windows ves símbolos raros en lugar de flechas o tildes, ejecuta antes
`chcp 65001` en la terminal.

## Dónde está cada estructura

| Estructura | Archivo | Dónde se ve operar |
|---|---|---|
| Cola sobre lista simple | `Cola.java` | El zapato: la carta sale por el frente |
| Pila sobre lista simple | `Pila.java` | Descarte (cima = última carta) e historial (deshacer) |
| Lista doble | `ListaDoble.java` | La mano (`Mano.java`) y los asientos (`Mesa.java`) |
| Tabla hash (5 cubetas) | `TablaHash.java` | Jugadores por id; J01 y J06 en la cubeta 1 |
| Árbol binario de búsqueda | `ArbolRanking.java` | Ranking final: inorden, camino, nivel, grado, peso, altura, hojas, completo |
| Árbol binario de decisión | `ArbolDecision.java` | Cada mano baja por sí/no hasta una acción |
| Grafo (listas de adyacencia) | `Grafo.java`, `Sala.java` | Dijkstra, Prim y Kruskal |
| Reglas y corrida | `Mesa.java`, `Main.java` | Rondas, apuestas, casos de borde |

`transcripcion_corrida_fija.txt` es la salida completa de la corrida de verificación.
`INFORME.md` es el borrador del informe.

## Interfaz gráfica (`Interfaz.java`)

Ventana Swing sin librerías externas; usa las mismas clases del proyecto.

- **Partida**: mesa visual. Se pone la apuesta de cada jugador (0 = no juega), se pulsa
  *Repartir ronda* y, cuando toca decidir, *Pedir carta* o *Plantarse*. Con «Cartas fijas»
  se reproduce la guía (ronda 1: Ana 100 y Luis 50, Luis pide; ronda 2: Marta 80 y Ana 100,
  Marta se planta, Ana pide y se planta). Los botones de abajo muestran cada estructura
  (asientos, tabla hash, manos en los dos sentidos, descarte, historial, deshacer, ranking,
  árbol de decisión, zapato vacío) y el registro de la derecha es lo que imprime el programa.
- **Sala (grafo)**: dibujo del grafo con Dijkstra (casilla «T1 llena»), Prim y Kruskal
  (aristas aceptadas en azul, rechazadas punteadas en rojo) y «Camino a:» (prueba con T9).
- **Corrida de verificación**: la salida completa de consola en un cuadro de texto.
