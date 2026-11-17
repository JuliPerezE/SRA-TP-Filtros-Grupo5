# Simulaciones en LTspice - Filtro Pasa Bajo Bessel (Ideal)

Este directorio contiene los archivos de simulación del circuito **PasaBajo_Bessel_Ideal** en LTspice. Todo el diseño utiliza componentes pasivos ideales y el amplificador operacional provisto por la librería nativa de LTspice, por lo que no requiere archivos externos adicionales para ejecutarse.

## Estructura de Archivos

- **Esquemático (`.asc`)**: Diseño gráfico del circuito `PasaBajo_Bessel_Ideal`, donde se definen la topología, los valores nominales ideales de los componentes y el amplificador operacional de librería.
- **Ejecutable Bode (`.cir`)**: Netlist ejecutable configurado para simular exclusivamente el diagrama de Bode (respuesta en frecuencia) de `PasaBajo_Bessel_Ideal`.
- **Ejecutable Respuesta Escalón (`.cir`)**: Netlist ejecutable configurado para simular exclusivamente la respuesta temporal al escalón de `PasaBajo_Bessel_Ideal`.

## Parámetros de la Simulación

- **Amplificador Operacional**: Modelo provisto por la librería interna de LTspice.
- **Componentes Pasivos**: Resistores y capacitores ideales (valores nominales exactos, sin tolerancias).
- **Análisis configurados**: Diagrama de Bode y Respuesta al Escalón (corrida nominal única).

## Cómo Usar los Archivos `.cir` y `.asc`

### Ejecutar simulaciones directas (`.cir`)
Los archivos `.cir` contienen las directivas listas para correr cada análisis sin necesidad de configurar el entorno gráfico:
1. Abre **LTspice**.
2. Ve a `File > Open` (o arrastra el archivo directamente a la ventana del programa) y selecciona el **Ejecutable Bode (`.cir`)** o el **Ejecutable Respuesta Escalón (`.cir`)**.
3. Presiona el botón **Run** (ícono del corredor) para ejecutar la simulación.
4. Selecciona el nodo de salida mediante `Add Traces` (o haciendo clic sobre la red de salida) para visualizar la gráfica correspondiente.

### Inspeccionar o modificar el circuito (`.asc`)
1. Desde **LTspice**, ve a `File > Open` y abre el archivo **Esquemático `.asc`**.
2. Desde esta vista puedes revisar las conexiones, editar los valores ideales de resistores y capacitores, o modificar las directivas de simulación (`Edit Simulation Cmd`) antes de presionar **Run**.
