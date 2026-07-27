# Taller Práctico 01

**Curso:** Fundamentos en Ciencia de Datos — Maestría en Ciencia de Datos y Analítica, EAFIT
**Conjunto de datos elegido:** C - Movilidad
**Fecha límite de entrega:** domingo 27 de julio de 2026
**Fecha de entrega real:** 26/07/2026

**Integrantes del equipo:**

| Nombre completo | Cédula         |
| --------------- | -------------- |
| Daniel Felipe Arango Guarín | 1018227831 |
| Daniel Correa Botero | 1023624609 |
| Miguel Ángel Cano Salinas | 1023522662 |

---

## 1. Resumen ejecutivo

La Secretaría de Movilidad tiene que decidir dónde y a qué horas pilotear semaforización inteligente.
Sobre 1351 lecturas limpias de seis sensores de tráfico en Medellín encontramos que el corredor casi
no importa: los seis registran entre 22.2 y 23.4 vehículos promedio. Lo que importa es la hora. En
las franjas de 6:00–9:00 y 16:00–19:00 la probabilidad de que un corredor pase de 40 vehículos por
intervalo es del 51.8 %; fuera de esas franjas es del 0 %. El clima no aporta nada. Recomendamos
operar el piloto solo en esas dos franjas, empezando por Circular 4ta, Autopista Norte y Av. Regional.

## 2. Pregunta de negocio

- **Pregunta ancla del conjunto de datos:** ¿En qué corredores y horarios se debe pilotear semaforización inteligente?
- **Pregunta específica que su equipo decidió responder:** ¿Cuál es la probabilidad de que un corredor
  esté en congestión alta, dado el momento del día en que se mide?


## 3. Estructura del repositorio

```
├── README.md
├── data/
│   ├── raw/                  # datos originales (sin modificar)
│   └── processed/            # datos ya limpios, generados por el notebook
├── notebooks/
│   └── taller_practico_01_analisis.ipynb
├── results/
│   ├── figuras/
│   ├── coordenadas_corregidas.csv
│   └── tabla_diagnostico_gigo.csv
└── docs/
    └── declaracion_uso_IA.md
```

## 4. Cómo reproducir el análisis (Solamente vía terminal)

```bash
# 1. Clonar el repositorio
git clone https://github.com/DanielC19/DataScienceFundamentals_Challenge01
cd DataScienceFundamentals_Challenge01/

# 2. Crear entorno e instalar dependencias
pip install -r requirements.txt

# 3. Ejecutar el notebook de inicio a fin
jupyter notebook notebooks/taller_practico_01_analisis.ipynb
```

## 5. Principales hallazgos

| #   | Hallazgo | Evidencia (tabla/figura) |
| --- | -------- | ------------------------ |
| 1   | La hora del día es lo único que explica la congestión: 51.8 % de probabilidad en hora pico contra 0 % fuera de pico. | Tabla `time_band` × `congestion_level`; `results/figuras/g1_conteo_por_hora.png` |
| 2   | El conteo son dos grupos separados (≈14 y ≈40 vehículos), así que la media de 22.84 no describe ningún momento real del día. | `results/figuras/g2_histograma_conteo.png` |
| 3   | Ni el corredor ni el clima discriminan: los seis sensores dan entre 22.2 y 23.4 vehículos y la correlación temperatura–conteo es 0.006. | `g3_mapa_sensores.png` y `g4_boxplot_clima.png` |
| 4   | Corregir el intercambio de coordenadas de SEN04 nos dejó 1351 filas (93 %) y los tres tipos de vía con casi las mismas lecturas. | Tabla de frecuencias de `tipo_via`, figura 3 |

## 6. Problemas de calidad de datos encontrados (resumen GIGO)

| Problema | Estrategia de corrección | Justificación |
| -------- | ------------------------ | ------------- |
| 145 nulos en conteo, 72 en temperatura, 87 en clima | Imputar con la mediana del mismo sensor a la misma hora; en clima marcar "Desconocido" | La mediana no se deja arrastrar por valores extremos; en clima preferimos decir que no sabemos antes que inventar |
| 11 etiquetas de clima para 3 categorías | `str.strip()`, `str.lower()` y un diccionario | El problema es de escritura, no del dato |
| 14 filas repetidas por sensor e instante (7 idénticas, 7 con contenido distinto) | `drop_duplicates` con la llave `sensor_id` + `timestamp` | Un sensor no puede tener dos lecturas en el mismo momento |
| 90 fechas en formatos mezclados | Eliminar esas filas | La hora es la variable principal y no se puede estimar |
| 6 conteos negativos y 4 lecturas de 99999 | Pasar a nulo y luego imputar | Son imposibles, pero el resto de la fila sirve |
| 121 coordenadas fuera de Medellín, todas de SEN04 con lat/lon cambiadas | Intercambiar lat y lon cuando el cambio deja el punto en la ciudad | El patrón es idéntico en todas; descartarlas costaba la mitad de un corredor |

## 7. Decisión recomendada

- **Recomendación:** operar el piloto solo en las franjas 6:00–9:00 y 16:00–19:00, empezando por
  Circular 4ta (61.8 %), Autopista Norte (56.8 %) y Av. Regional (54.1 %), con Av. 33 y Av. Oriental
  como control. Monitorear hora y día de la semana, no el clima.
- **Costo de un Falso Positivo:** se invierte donde ya fluye bien. Además de la plata perdida,
  reajustar semáforos donde no hacía falta puede mover el trancón a una calle que no tiene sensor.
- **Costo de un Falso Negativo:** no se interviene un corredor colapsado. Se paga en tiempo de la
  gente y, como no hay intervención, tampoco hay medición: el problema no aparece en ningún reporte.
  Nos preocupa más este, y fue la razón para corregir las coordenadas de SEN04 en vez de botarlas.
- **Limitación principal que persiste tras la limpieza:** el intercambio de lat/lon de SEN04 es una
  suposición nuestra. La comprobamos en parte (tras el cambio las lecturas caen en un radio menor a
  100 m), pero si la causa fuera otra estaríamos ubicando 112 lecturas mal y ya no se notaría. Quedan
  registradas en `results/coordenadas_corregidas.csv`. Además, el 10.8 % de los conteos finales son
  estimaciones nuestras y no mediciones.

## 8. Declaración de uso de Inteligencia Artificial

Ver `docs/declaracion_uso_IA.md`. Resumen: se usó IA generativa para sintaxis de pandas y matplotlib
en las Tareas 3 y 4; la estrategia de imputación, la decisión de corregir las coordenadas y la
interpretación de los resultados fue del equipo.
