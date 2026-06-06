# Trabajo Práctico Integrador - Procesamiento de Ventas de Supermercado

**Alumno:** Matías Fasolato

---

Este proyecto implementa una solución modularizada en Python para el procesamiento y
consolidación de datos de ventas de un supermercado mediante la técnica de **Corte de
Control**. Está diseñado bajo buenas prácticas de arquitectura de software, incluyendo
pruebas unitarias automatizadas e Integración Continua (CI) con GitHub Actions.

---

## Estructura del Repositorio

```
├── main.py                        # Código fuente principal
├── test_main.py                   # Pruebas unitarias con pytest
├── requirements.txt               # Dependencias del proyecto
├── .gitignore                     # Archivos y carpetas ignorados por Git
├── data/
│   └── supermercado_desordenado.csv   # Archivo de datos de entrada
└── .github/
    └── workflows/
        └── ci.yml                 # Pipeline de Integración Continua
```

---

## Arquitectura en Capas

El código está dividido en capas con responsabilidades independientes
(alta cohesión, bajo acoplamiento):

1. **Capa de Datos (Data Access):** Lectura del archivo CSV mediante Pandas.
2. **Capa de Algoritmos (Sorting):** Implementación manual del algoritmo Bubble Sort
   para garantizar el orden requerido por el Corte de Control.
3. **Capa de Lógica (Business Logic):** Cálculo de totales, máximos y mínimos por
   sucursal. Al ser funciones puras sin I/O, son 100% testeables.
4. **Capa de Presentación (UI):** Formateo y visualización de resultados por consola.

---

## Instalación y Ejecución

**1. Clonar el repositorio**

```bash
git clone https://github.com/MatiFasolato/mfasolato_tpi.git
cd mfasolato_tpi
```

**2. Instalar dependencias**

```bash
pip install -r requirements.txt
```

**3. Ejecutar el programa**

```bash
python main.py
```

**4. Ejecutar los tests**

```bash
pytest test_main.py
```

---

## Pruebas Unitarias

El proyecto cuenta con 5 pruebas unitarias desarrolladas con `pytest` que validan:

| Test                           | Función evaluada        | Qué verifica                                                    |
| ------------------------------ | ----------------------- | --------------------------------------------------------------- |
| `test_calcular_subtotal`       | `calcular_subtotal`     | Precisión aritmética en el cálculo de subtotales                |
| `test_ordenar_datos_burbuja`   | `ordenar_datos_burbuja` | Correcto ordenamiento ascendente por sucursal                   |
| `test_procesar_ventas_totales` | `procesar_ventas`       | Consolidación de registros y totales generales                  |
| `test_procesar_ventas_vacio`   | `procesar_ventas`       | Robustez ante una lista de datos vacía                          |
| `test_procesar_ventas_max_min` | `procesar_ventas`       | Identificación correcta del producto mayor y menor por sucursal |

---

## Pipeline de Integración Continua (CI)

El repositorio cuenta con un pipeline configurado en **GitHub Actions** (`.github/workflows/ci.yml`) que se ejecuta automáticamente ante cada Pull Request hacia `main`. El pipeline:

- Instala las dependencias del proyecto
- Ejecuta la suite completa de tests con `pytest`
- Bloquea el merge si algún test falla

La rama `main` está protegida: no se puede hacer push directo ni mergear un PR con pipeline fallida.
