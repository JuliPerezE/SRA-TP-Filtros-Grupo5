# Simulaciones en LTspice - Filtro Pasa Bajo Bessel (Modelo Fabricante y Componentes Ideales)

Este directorio contiene los archivos de simulación del circuito **PasaBajo_Bessel_ModeloFabricante** en LTspice, configurado con componentes pasivos ideales (valores nominales sin tolerancia) y utilizando el modelo oficial del amplificador operacional **TL082** de Texas Instruments.

## Requisito Indispensable de Descarga

**Es obligatorio descargar la carpeta completa** y mantener todos los archivos dentro del mismo directorio sin alterar sus nombres.

Las simulaciones dependen de archivos auxiliares del amplificador operacional. Si descargas archivos de forma individual, LTspice arrojará un error al no encontrar las librerías vinculadas. Verifica que en tu carpeta local estén presentes:
- **`TL082.301`**: Archivo del modelo SPICE proporcionado por el fabricante (Texas Instruments).
- **`TL082.asy`**: Archivo del modelo/esquemático del TL082 generado por nosotros para su integración en el circuito.

## Estructura de Archivos

- **Esquemático (`.asc`)**: Diseño del circuito principal `PasaBajo_Bessel_ModeloFabricante`, donde se definen las conexiones y los valores nominales ideales de los componentes.
- **Ejecutable Bode (`.cir`)**: Netlist ejecutable configurado para simular el diagrama de Bode (respuesta en frecuencia) de `PasaBajo_Bessel_ModeloFabricante`.
- **Ejecutable Respuesta Escalón (`.cir`)**: Netlist ejecutable configurado para simular la respuesta temporal al escalón de `PasaBajo_Bessel_ModeloFabricante`.
- **Modelos del AmpOp (`TL082.301` y `TL082.asy`)**: Archivos requeridos para emular el comportamiento real del TL082.

## Parámetros de la Simulación

- **Amplificador Operacional**: Modelo del fabricante **TL082** (Texas Instruments).
- **Componentes Pasivos**: Resistores y capacitores ideales (valores nominales exactos, sin tolerancias asignadas).
- **Tipo de Análisis**: Simulación nominal de corrida única (sin análisis estadístico de Monte Carlo).

## Instrucciones Mínimas de Ejecución

1. **Descargar el directorio completo**: Descarga toda la carpeta del proyecto (y descomprímela si está en formato `.zip`) asegurando que todos los archivos queden en la misma ruta.
2. **Abrir LTspice**: Ejecuta LTspice en tu computadora.
3. **Correr las simulaciones ejecutables (`.cir`)**:
   - Desde LTspice, ve a `File > Open` (o arrastra el archivo hacia la ventana del programa).
   - Abre el **Ejecutable Bode (`.cir`)** para analizar la respuesta en frecuencia, o el **Ejecutable Respuesta Escalón (`.cir`)** para analizar la respuesta transitoria.
   - Presiona **Run** para ejecutar la simulación.
   - Selecciona el nodo de salida mediante `Add Traces` (o haciendo clic sobre la red correspondiente) para visualizar la curva.
4. **Consultar el esquemático (`.asc`)**:
   - Para inspeccionar la topología del filtro, los valores nominales o las directivas de simulación, abre el archivo **Esquemático `.asc`**.
