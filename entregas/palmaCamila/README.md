# Tic Tac Toe - Reto Documentación

## Descripción del Reto
Este proyecto implementa el juego del Tres en Raya (Tic Tac Toe) utilizando los patrones de diseño **Modelo-Vista-Controlador (MVC)** y **Builder**. El objetivo principal del reto fue diseñar una arquitectura clara, modular y extensible que permita separar las responsabilidades de cada componente del sistema.

---

## Modelo de Dominio
El modelo de dominio se encuentra representado en el archivo [modeloDominio.puml](modelosUML/modeloDominio.puml). Este diagrama muestra las relaciones entre las clases y los paquetes del sistema, organizados según el patrón MVC y el patrón Builder.

### Justificación de las Relaciones

1. **`ConsoleView` implementa `View`**:
   - La clase `ConsoleView` es una implementación concreta de la interfaz `View`. Esto permite que el sistema sea extensible, ya que se pueden crear otras implementaciones de `View` (por ejemplo, una interfaz gráfica) sin modificar el resto del sistema.

2. **`TicTacToe` usa `View`**:
   - La clase `TicTacToe` (Controlador) utiliza la interfaz `View` para interactuar con el usuario. Esto incluye mostrar el tablero, solicitar coordenadas y mostrar mensajes o el ganador.

3. **`TicTacToeBuilder` configura `View`**:
   - El `Builder` se encarga de configurar la vista que será utilizada por el controlador `TicTacToe`. Esto asegura que el objeto `TicTacToe` se cree con todas sus dependencias correctamente configuradas.

4. **`TicTacToe` tiene `Board`, `Player[]` y `Turn`**:
   - El controlador `TicTacToe` gestiona el flujo del juego y utiliza el modelo (`Board`, `Player` y `Turn`) para manejar el estado del juego y la lógica del dominio.

5. **`Main` usa `TicTacToeBuilder` y `ConsoleView`**:
   - La clase `Main` es el punto de entrada del programa. Utiliza el `Builder` para crear una instancia de `TicTacToe` y configura la vista como `ConsoleView`.

6. **`Board` usa `Coordinate`**:
   - La clase `Board` utiliza `Coordinate` para representar las posiciones en el tablero y realizar operaciones como colocar o mover fichas.

7. **`ConsoleView` crea `Coordinate`**:
   - La clase `ConsoleView` solicita al usuario las coordenadas y crea instancias de `Coordinate` para representar las posiciones seleccionadas.

---

## Patrones de Diseño Utilizados

### Modelo-Vista-Controlador (MVC)
El patrón MVC se utilizó para separar las responsabilidades del sistema en tres componentes principales:

1. **Modelo**:
   - **Clases involucradas**: `Board`, `Player`, `Turn`, `Coordinate`.
   - **Responsabilidad**: Gestionar el estado del juego y la lógica del dominio.

2. **Vista**:
   - **Clases involucradas**: `View` (interfaz) y `ConsoleView` (implementación).
   - **Responsabilidad**: Mostrar información al usuario y recibir entradas.

3. **Controlador**:
   - **Clases involucradas**: `TicTacToe` y `Main`.
   - **Responsabilidad**: Coordinar la interacción entre el modelo y la vista, gestionando el flujo del juego.

### Builder
El patrón Builder se utilizó para simplificar la creación de objetos complejos como `TicTacToe`. Este patrón permite construir objetos paso a paso y asegura que todas las dependencias necesarias estén configuradas antes de crear el objeto.

- **Clase involucrada**: `TicTacToeBuilder`.
- **Ventajas**:
  - **Flexibilidad**: Permite configurar diferentes vistas o dependencias sin modificar el constructor de `TicTacToe`.
  - **Legibilidad**: Hace que el código sea más claro y fácil de entender.
  - **Escalabilidad**: Facilita la adición de nuevas configuraciones al objeto `TicTacToe` en el futuro.

Ejemplo de uso del Builder:
```java
TicTacToe ticTacToe = new TicTacToeBuilder()
    .withView(new ConsoleView())
    .build();
```

---

## Conclusión
El uso de los patrones MVC y Builder en este proyecto permitió crear una arquitectura modular y extensible. La separación de responsabilidades facilita el mantenimiento y la evolución del sistema, mientras que el Builder simplifica la creación de objetos complejos y mejora la legibilidad del código.