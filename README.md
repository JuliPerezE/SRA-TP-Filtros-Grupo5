# SRA-TP-Filtros-Grupo5

Grupo: 5  
Integrantes: Pérez Echeverría Julieta, Rodriguez Alan, Choque Fernando, Mendoza Marcos  
Aproximaciones: Butterworth y Bessel (en filtros Pasabajos LP y Pasabanda BP)  
Filtro implementado: Filtro Pasabajos (LP) Bessel de 3.er orden (N = 3) en cascada (RC + Buffer + Sallen-Key asimétrico)  
Duración: Cinco semanas. Cada grupo estudia dos tipos de filtros con dos aproximaciones (cuatro diseños matemáticos) e implementa un único filtro.

---

## Motivación y Objetivo del Proyecto

El objetivo de este Trabajo Práctico Integrador es abordar el ciclo completo de ingeniería de un filtro analógico activo: desde la síntesis matemática a partir de especificaciones de plantilla, pasando por el análisis simbólico de sensibilidades y la simulación estadística, hasta la implementación física y validación experimental en laboratorio.

A partir de los requerimientos de diseño para el filtro pasabajos (fp = 1000 Hz, fs = 4000 Hz y As >= 24 dB) y pasabanda (1200 Hz a 2400 Hz), se evaluaron las aproximaciones de Butterworth y Bessel mediante cómputo numérico (Python / SciPy). Se seleccionó la topología pasabajos de Bessel de 3.er orden (N = 3) con el propósito de priorizar la linealidad de fase y la máxima planitud del retardo de grupo dentro de la banda de paso, minimizando la distorsión temporal y los sobrepicos (overshoot) ante señales transitorias.

---

## Arquitectura y Síntesis Circuital

La función de transferencia de 3.er orden Ht(s) se sintetizó mediante la conexión en cascada de dos etapas desacopladas de ganancia unitaria (K = 1), implementadas con amplificadores operacionales TL082:

Etapa 1 — Celda pasiva RC de 1.er orden + Buffer:  
Implementa el polo real mediante una red R0 C0 seguida de un seguidor de tensión (buffer) que evita efectos de carga sobre la etapa siguiente.

Etapa 2 — Celda activa bicuadrática Sallen-Key (2.do orden):  
Implementa el par de polos complejos conjugados utilizando un dimensionamiento asimétrico (R1 = 6,8 kΩ, R2 = 16 kΩ, C1 = 22 nF, C2 = 10 nF), optimizado para acotar las sensibilidades paramétricas frente a dispersiones reales de componentes.

Etapa de Ampliación — Ecualizador Pasa-Todo (All-Pass):  
Se diseñó y simuló con componentes comerciales E96 una etapa bicuadrática pasa-todo de 2.do orden en cascada en topología Series-loaded Twin-T (f0 = 1633,75 Hz, Q = 4,1677), destinada a compensar la caída de retardo hacia el límite de la banda de paso y reducir la fluctuación del retardo de grupo a menos de 10 us sin alterar la magnitud.

---

## Metodología de Análisis y Validación

El desarrollo del proyecto se estructuró en cuatro instancias sucesivas de verificación:

Modelado Numérico (Python / SciPy): Normalización de frecuencias, extracción de polos y ceros, y contraste comparativo de magnitud, fase desenrollada y retardo de grupo entre aproximaciones.

Análisis Simbólico (SymPy): Resolución de ecuaciones nodales de las etapas activas y derivación exacta de las sensibilidades relativas respecto a cada componente pasivo.

Simulación Eléctrica y Estadística (LTspice): Validación en régimen permanente (AC) y transitorio con modelos comerciales del TL082, complementada con un análisis Monte Carlo (100 corridas) contemplando tolerancias comerciales (1% en resistencias y 5% en capacitores).

Contrastación Experimental: Montaje físico del prototipo y medición punto a punto en laboratorio de ganancia, desfasaje, retardo de grupo y respuesta al escalón.

---

## Resultados y Conclusiones Técnicas

| Métrica de Desempeño | Teórico (Python / SymPy) | Simulación (LTspice / Monte Carlo) | Validación Experimental |
| :--- | :---: | :---: | :---: |
| Atenuación en fp = 1 kHz | 6,24 dB (Excepción Bessel) | 6,43 dB (desv. est. 0,59 dB) | Desviación < 0,1 dB |
| Atenuación en fs = 4 kHz | > 36 dB | 36,49 dB (desv. est. 0,90 dB) | Cumple (> 24 dB) |
| Retardo de grupo | ~398 us (plano en banda) | ~398 us | Fase con error < 2° |
| Respuesta al escalón (1 V) | Sobrepico de 0,6% (0,006 V) | Sin oscilaciones (ringing) | Respuesta amortiguada |
| Sensibilidad paramétrica máxima | <= 0,5 (|SQ_R| ~ 0,2018) | Dispersión acotada | Alta estabilidad física |

### Hallazgos Principales

Cumplimiento bajo la Excepción Bessel: Al fijar el orden en N = 3 (comparable con Butterworth) para preservar un hardware compacto, la atenuación en fp = 1 kHz alcanza los 6,24 dB debido a la transición suave característica de Bessel, mientras que la banda de rechazo (36,49 dB a 4 kHz) cumple sobradamente con el requisito de >= 24 dB en el 100% de las simulaciones Monte Carlo.

Robustez frente a tolerancias: El dimensionamiento asimétrico de la celda Sallen-Key redujo la sensibilidad del factor de calidad respecto a las resistencias (|SQ_R| ~ 0,2018), dejando a los capacitores (|S| = 0,5) como los elementos críticos del diseño.

Correlación Teoría–Laboratorio: Las mediciones sobre el circuito implementado mostraron un ajuste notable frente a las curvas teóricas, con diferencias menores a 0,1 dB en amplitud y menores a 2° en fase dentro de la banda de paso.

Extensión de planitud mediante ecualización: La incorporación de la celda All-Pass optimizada permitió compensar la caída del retardo de grupo hacia el borde de la banda de paso, logrando un comportamiento temporal casi ideal con una fluctuación menor a 10 us.

---

## Requisitos y Reproducción

Requisitos:  
Google Colab con numpy, scipy, sympy, matplotlib, pandas; LTspice; LaTeX (Overleaf o TeX Live); Git.

Reproducción:
1. Abrir los notebooks de `notebooks/` en orden 01, 02 y 03.
2. Ejecutar todas las celdas y completar las consignas.
3. Abrir archivos de `ltspice/` en LTspice y ejecutar análisis AC y transitorio.
4. Revisar datos originales en `mediciones/` y comparar con los resultados.
5. Compilar `informe/Guia_Trabajo_Practico.tex` para consultar la guía. Para la entrega, usar `informe/Plantilla_Informe.tex`.

---

## Entrega

Enlace al repositorio: [completar con la URL de tu repo en GitHub/GitLab]  
Fecha: 18 de noviembre de 2026  

No se incluyen soluciones de la cátedra.
