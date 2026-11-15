# Proyecto 7: Explorando drivers de comportamiento en NovaRetail+

Repositorio oficial del proyecto de análisis exploratorio y correlacional desarrollado para **NovaRetail+**, enfocado en identificar los factores del comportamiento del cliente asociados al valor económico generado en la plataforma durante 2024. Este proyecto fue desarrollado e implementado utilizando **Google Colab** y **Jupyter Notebook**.

## 📋 Contexto del Negocio

**NovaRetail+** es una plataforma líder de comercio electrónico en Latinoamérica con millones de usuarios. Para el cierre del año 2024, el equipo de **Crecimiento y Retención** busca responder una pregunta clave de negocio:

> *¿Qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado (`ingreso_anual`)?*

Para dar respuesta a este interrogante, se realizó un análisis correlacional estructurado combinando variables de comportamiento, segmentación demográfica y valor económico sobre un conjunto de datos de $15,000$ registros.

## 🎯 Objetivos del Proyecto

1. **Integrar múltiples técnicas de correlación** (Pearson, Spearman, Punto-biserial y V de Cramér) en un flujo de análisis robusto.
2. **Identificar relaciones significativas** mediante el uso de visualizaciones avanzadas (*heatmaps* y *pairplots*).
3. **Detectar correlaciones engañosas** y descartar falsas hipótesis de causalidad.
4. **Documentar supuestos, hallazgos y limitaciones** bajo un enfoque analítico riguroso.
5. **Convertir evidencia cuantitativa en recomendaciones de negocio** accionables.

## 🛠️ Herramientas y Entorno de Desarrollo

* **Entorno de ejecución:** Google Colab / Jupyter Notebook
* **Lenguaje:** Python
* **Librerías principales:**
  * `pandas` y `numpy` para la manipulación y procesamiento de datos.
  * `seaborn` y `matplotlib` para la visualización gráfica avanzada.
  * `scipy.stats` para el cálculo de pruebas estadísticas y correlaciones.

## 📊 Estructura del Dataset

El conjunto de datos (`/datasets/novaretail_comportamiento_clientes_2024.csv`) contiene **15,000 filas y 12 columnas**:

| Columna | Tipo de dato | Descripción |
| :--- | :--- | :--- |
| `id_cliente` | `string` | Identificador único del cliente. |
| `edad` | `int` | Edad del cliente. |
| `nivel_ingreso` | `float` | Ingreso anual estimado del cliente. |
| `visitas_mes` | `int` | Número de visitas a la app o sitio web en el mes. |
| `compras_mes` | `int` | Compras realizadas en el mes. |
| `gasto_publicidad_dirigida` | `float` | Gasto en anuncios asignado al usuario. |
| `satisfaccion` | `float` | Calificación de satisfacción del cliente (escala de 1 a 5). |
| `miembro_premium` | `int` (0/1) | Indica si el cliente tiene suscripción premium (1) o estándar (0). |
| `abandono` | `int` (0/1) | Si el cliente abandonó la plataforma (1) o se mantiene activo (0). |
| `tipo_dispositivo` | `string` | Dispositivo utilizado (móvil, escritorio, tablet). |
| `region` | `string` | Región geográfica (norte, sur, oeste, este). |
| `ingreso_anual` | `float` | **Métrica foco:** Ingreso anual generado por el cliente para la empresa. |

## 🔍 Flujo de Trabajo y Metodología

1. **Carga y Exploración Inicial:** Validación de tipos de datos, verificación de ausencia de valores nulos e inspección estructural del *dataframe*.
2. **Preparación y Limpieza:** Ajuste de formatos numéricos en la edad y clasificación formal de variables (numéricas, binarias y categóricas).
3. **Análisis Exploratorio y Visualización:** Generación de mapas de calor (*Heatmap*) global y matrices de dispersión bivariadas (*Pairplot*).
4. **Pruebas Estadísticas y Coeficientes:**
   * Correlaciones lineales y monótonas (**Pearson / Spearman**).
   * Evaluación entre variables continuas y binarias (**Punto-biserial**).
   * Análisis de asociación entre variables categóricas (**V de Cramér**).
5. **Interpretación y Hallazgos:** Traducción de la evidencia numérica y visual en conclusiones de negocio estructuradas.
6. **Limitaciones y Próximos Pasos:** Definición de alcances del análisis correlacional y propuestas de valor futuras.

## 💡 Hallazgos Principales

* **El principal motor de ingresos (`ingreso_anual` vs `compras_mes`):** Se identificó una correlación positiva extremadamente fuerte de $0.97$, demostrando que el volumen de compras mensuales es el factor determinante y directo de la rentabilidad del cliente.
* **Impacto del tráfico y la publicidad (`visitas_mes` vs `gasto_publicidad_dirigida`):** Se observó una correlación moderada de $0.58$, lo que confirma que las pautas publicitarias dirigidas son eficaces para estimular la recurrencia y el tráfico de los usuarios en la plataforma.
* **Independencia transversal:** Las pruebas estadísticas (Punto-biserial y V de Cramér) demostraron que variables como la región geográfica, el tipo de dispositivo y la membresía premium operan de forma independiente y no guardan una asociación lineal fuerte con el abandono o los ingresos directos.

## 🚀 Cómo Ejecutar el Proyecto

Puedes abrir y ejecutar este cuaderno directamente en tu entorno favorito:

1. **Google Colab:** Sube el archivo `.ipynb` a tu Google Drive, ábrelo con Google Colab y ejecuta las celdas de forma secuencial.
2. **Entorno Local (Jupyter):**
   * Clona este repositorio:
     ```bash
     git clone https://github.com/tu-usuario/proyecto-novaretail.git
     ```
   * Asegúrate de tener instaladas las librerías requeridas (`pandas`, `numpy`, `seaborn`, `matplotlib`, `scipy`).
   * Abre el cuaderno y ejecútalo paso a paso.

*Desarrollado como parte del programa de análisis de datos y ciencia de datos.*
