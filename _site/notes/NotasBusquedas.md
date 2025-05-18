## Busquedas

# Problemas de busqueda:

* Problemas Deterministicos
* Problemas no observables
* Problemas parcialmente observables / No deterministicos
* Problemas de Estado Espacio Desconocido

# Consisten de:

* Un espacio estado
* Un modelo de transicion
* Un estado inicial, una meta prueba y una funcion camino con costo

# Ejemplos: 

* Pathfinding. Rumania.
* El problema de la gallina, el zorro y la verdura
* 8 Puzzle

# Soluciones: 

* Grafos del espacio estado: Representa todos los posibles estados en nodos y las transiciones que puede tener son las aristas.
* Arboles de busqueda: Una estructura de arbol, en la que cada nodo representa una secuencia de acciones. 
* Busquedas heuristicas: Utiliza lo que sabe para estimar el costo del estado actual a la meta. Reduciendo el numero de nodos explorados al guiarlos hacia la meta.

# Algoritmos:

* Busqueda a profundidad (DFS): Primero explora hasta la profundidad maxima para despues hacer backtracking
* Busqueda en amplitud (BFS): Explora todos los vecinos del primer nodo antes de moverse a otra profundidad.
* A*: Balancea la exploracion con la explotacion, usando la funcion
\[ f(n) = g(n) + h(n) \]
donde:

	* g(n) es el costo del nodo inicial a n.
	* h(n) es la heuristica estimada de n a la meta.
	* f(n) es el costo estimado total.
Esto garantiza optimizacion si h(n) es admisible.

## Arboles de juego: Busqueda con adversarios

Se utilizan arboles de juego para representar una estructura donde los nodos son los estados del juego, las aristas representan los posibles movimientos y el arbol alterna cada profundidad entre un maximo para el jugador que intenta ganar y un minimo para el oponente.

# Minimax

Es un algoritmo para encontrar y decidir cual es el mejor movimiento en un juego donde ambos jugadores hacen movimientos optimos. Primero se genera el arbol de juego hasta la profundidad deseada, se les asignan valores a los nodos hojas. Desde estos nodos se hace un backpropagation tomando el minimo para el peor escenario del jugador y el maximo para el mejor. Ejemplo: 

```markdown
       MAX
      /   \
    MIN    MIN
   /  \    /  \
  3    5  2    9

Elegimos el minimo posible:

       MAX
      /   \
    3	    2
   /  \    /  \
  3    5  2    9

Elegimos el maximo para el jugador:

        3
      /   \
    3	    2
   /  \    /  \
  3    5  2    9
```
# Poda de arboles

Si el arbol es grande, minimax seria muy lento, imposible de procesar. Una forma de acelarlo es haciendo una poda de las ramas del arbol. 

# Poda Alfa-Beta

La idea de la poda Alfa Beta, es obtener el mejor valor maximo que se pueda garantizar como Alpha e igual con el mejor valor minimo que sera Beta. Si se tiene un nodo con valor peor a lo que se tiene, se poda.

Se atraviesa el arbol de juego usando Minimax, con una referencia a Alpha y Beta, que son los mejores maximos y minimos valores que se han tenido hasta el momento. Este hace una poda de la rama sin explorarla mas a fondo, cuando se encuentra un valor Beta menor o igual a Alpha.

Ejemplo: 

```markdown
       MAX
      /   \
    MIN    MIN
   /  \    /  \
  3    5  2    9

El minimo en la izquierda es 3, por lo que es el nuevo valor de Beta:

       MAX
      /   \
     3      MIN
   /  \    /  \
  3    5  2    9

En el nodo raiz, se toma el mejor valor actual y se actualiza Alpha con el 3:

        3
      /   \
    3      MIN
   /  \    /  \
  3    5  2    9

El minimo en la derecha encuentra un 2 para actualizar Beta, al compararlo con Alpha, se tiene que es menor, por lo que se procede a podar y no explorar el 9.


        3
      /   \
    3       2
   /  \    /  \
  3    5  2    [9]
