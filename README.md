# Pronóstico de pedidos de taxi — Sweet Lift Taxi

Proyecto de series temporales del bootcamp de Ciencia de Datos de TripleTen.

## Problema de negocio

Sweet Lift Taxi recopiló datos históricos de pedidos de taxi en aeropuertos. Para atraer más conductores en las horas pico, la empresa necesita **predecir la cantidad de pedidos de la próxima hora**. El modelo debe tener una **RECM menor a 48** en el conjunto de prueba.

## Datos

- Archivo `taxis.csv` con 26.496 observaciones de pedidos registrados cada 10 minutos, durante 6 meses.

## Metodología

1. **Preparación**: carga con índice de fecha, verificación del orden cronológico y **remuestreo a intervalos de una hora**.
2. **Análisis de la serie**: tendencia creciente y estacionalidad diaria, mediante descomposición con `statsmodels`.
3. **Ingeniería de características**: día, día de la semana, hora, **rezagos de 48 horas** y **media móvil de 24 horas**.
4. **Modelo de referencia**: predicción con el valor de la hora anterior.
5. **Modelado y validación cruzada temporal**: regresión lineal, árbol de decisión y bosque aleatorio con distintas configuraciones de hiperparámetros.
6. **Evaluación en el conjunto de prueba**.

## Resultados

| Modelo | RECM validación cruzada | RECM prueba |
|---|---|---|
| **Bosque aleatorio** (100 árboles, profundidad 12) | 24,40 | **41,39** |
| Regresión lineal | 24,76 | 42,00 |
| Modelo de referencia (hora anterior) | — | 59,02 |

- El bosque aleatorio cumple el requisito (RECM menor a 48) y reduce el error en cerca de un 30 % frente al modelo de referencia.
- El árbol de decisión mostró la mayor variación entre configuraciones y se descartó para la prueba final.

## Conclusiones

- Las variables de calendario, los rezagos y la media móvil capturan bien la tendencia y la estacionalidad diaria de los pedidos.
- El bosque aleatorio es el modelo recomendado. Al ser no lineal, puede incorporar más adelante otras variables, como las condiciones climáticas.

## Herramientas

Python · pandas · NumPy · Matplotlib · statsmodels · scikit-learn

## Archivos

- [`sweetlift_pronostico_pedidos_taxi.ipynb`](sweetlift_pronostico_pedidos_taxi.ipynb): notebook completo con código, gráficos y análisis.
- `requirements.txt`: librerías utilizadas.

Los datos fueron proporcionados por TripleTen y no se incluyen en el repositorio. El notebook conserva las salidas de la ejecución original.

---

**Iván Ricardo Navarro Espinosa** — Ingeniero Químico, MSc · [GitHub](https://github.com/ivanrnavarro) · ivanrnavarro@gmail.com
Más proyectos del bootcamp en [tripleten-ciencia-de-datos](https://github.com/ivanrnavarro/tripleten-ciencia-de-datos).
