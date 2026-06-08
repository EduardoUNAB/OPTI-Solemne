# Solemne — Optimización (CINF105) · 2026

Distribución de combustibles con flota de camiones cisterna de doble compartimento.
Resolución mediante **metaheurística en Python** (Algoritmo Genético), con verificación exacta por enumeración.

> **Nombre:** Vicente Díaz - Eduardo Zepeda - Fernando Chávez · **NRC:** 7924 · **RUT:** 21761195-4 -- 20834105-7 -- 21777267-2

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| [`Solemne_Optimizacion.ipynb`](./Solemne_Optimizacion.ipynb) | Notebook principal **ya ejecutado**, con las 4 partes resueltas |
| `build_notebook.py` | Script que genera el notebook (reproducibilidad) |
| `requirements.txt` | Dependencias de Python |

## Partes resueltas

1. **Modelamiento determinista (MILP).** Formulación completa (conjuntos, variables, objetivo y restricciones: flujo, demanda con shortage, compatibilidad compartimento–producto, capacidad, estabilidad Δ=0.30 y ventanas de tiempo) y resolución con Algoritmo Genético para el escenario s=1. **Costo óptimo: \$1.130** (la metaheurística coincide con el óptimo exacto).
2. **Scheduling de carga en el depósito.** Cálculo de tiempos de carga, modelo de makespan y diagrama de Gantt. **Makespan = 32,5 min** (igual a la cota inferior); ambos camiones salen a su hora.
3. **Análisis de la solución del operador.** La propuesta **viola la estabilidad** en T2 y su costo declarado es falso: el costo real es **\$21.200** (dominado por \$20.000 de shortage). Una mejora factible lo reduce a **\$1.200**.
4. **Extensión estocástica de dos etapas.** Decisiones here-and-now (rutas/cargas) vs. recourse (entregas/shortage) sobre 3 escenarios. **Costo esperado \$1.200**, **EVPI \$49**.

## Enfoque y supuestos

- **Metaheurística:** Algoritmo Genético (codificación de 6 bits: asignación de estaciones + orientación de compartimentos; el orden de visita se obtiene por un TSP por enumeración). Operadores: torneo, cruce uniforme, mutación bit-flip y elitismo.
- **Ventanas de tiempo:** se permite que el camión **espere** si llega antes de la apertura `a_j`; no se admite llegar después de `b_j`.
- **Estabilidad Δ=0.30:** se evalúa en cada instante (salida del depósito y después de cada entrega).
- **Escenario estocástico:** se asume que el Diésel de la Est.3 se mantiene en su valor base (3.000 L), ya que el enunciado sólo informa la variación del Regular en esa estación.
