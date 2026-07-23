# Taller Práctico 01 — [Nombre del equipo]

**Curso:** Fundamentos en Ciencia de Datos — Maestría en Ciencia de Datos y Analítica, EAFIT
**Conjunto de datos elegido:** C - Movilidad
**Fecha límite de entrega:** domingo 26 de julio de 2026
**Fecha de entrega real:** [dd/mm/aaaa]

**Integrantes del equipo:**

| Nombre completo | Cédula         |
| --------------- | -------------- |
| Daniel Felipe Arango Guarín | 1018227831 |
| Daniel Correa Botero | 1023624609 |
| Miguel Ángel Cano Salinas | 1023522662 |

---

## 1. Resumen ejecutivo (máx. 8 líneas)

> Escriba aquí, en lenguaje para un gerente no técnico, cuál era la pregunta de negocio,
> qué encontraron y cuál es la recomendación final. Esta sección se lee primero: debe
> poder entenderse sin abrir el notebook.

## 2. Pregunta de negocio

- **Pregunta ancla del conjunto de datos:** [copie la pregunta de negocio de la Guía del Taller]
- **Pregunta específica que su equipo decidió responder:** [reformúlenla en términos
  de probabilidad/decisión, no de "cuánto", siguiendo el ejemplo del Taller de Decisión
  de la Sesión 1]

## 3. Estructura del repositorio

```
.
├── README.md
├── data/
│   ├── raw/                  # datos originales (sin modificar)
│   └── processed/            # datos ya limpios, generados por el notebook
├── notebooks/
│   └── taller_practico_01_analisis.ipynb
├── src/                      # funciones auxiliares (opcional)
├── results/
│   ├── figuras/
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
| 1   |          |                          |
| 2   |          |                          |
| 3   |          |                          |

## 6. Problemas de calidad de datos encontrados (resumen GIGO)

| Problema | Estrategia de corrección | Justificación |
| -------- | ------------------------ | ------------- |
|          |                          |               |

*(Tabla completa en `results/tabla_diagnostico_gigo.csv`)*

## 7. Decisión recomendada

- **Recomendación:** [acción concreta y accionable]
- **Costo de un Falso Positivo:** [...]
- **Costo de un Falso Negativo:** [...]
- **Limitación principal de los datos que persiste tras la limpieza:** [...]

## 8. Declaración de uso de Inteligencia Artificial

Ver `docs/declaracion_uso_IA.md`. Resumen: [1-2 líneas, ej. "Se usó IA generativa para
sintaxis de pandas en la Tarea 3; la elección de estrategia de imputación y la
interpretación de resultados fue realizada y validada por el equipo."]
