

# Proyecto 7: Explorando drivers de comportamiento en NovaRetail+

Repositorio del proyecto de análisis exploratorio y correlacional desarrollado para **NovaRetail+**, enfocado en identificar los factores del comportamiento del cliente asociados al valor económico generado en la plataforma durante 2024. El proyecto se desarrolló en **Google Colab** y **Jupyter Notebook**.

## 📋 Contexto del Negocio

**NovaRetail+** es una plataforma de comercio electrónico en Latinoamérica. Para el cierre de 2024, el equipo de **Crecimiento y Retención** busca responder una pregunta clave:

> *¿Qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado (`ingreso_anual`)?*

Para responderla se realizó un análisis correlacional que combina variables de comportamiento, segmentación y valor económico sobre un conjunto de **15,000 registros**.

## 🎯 Objetivos del Proyecto

1. **Integrar múltiples técnicas de correlación** (Pearson, Spearman, Punto-biserial y V de Cramér) en un mismo flujo de análisis.
2. **Identificar asociaciones relevantes** con visualizaciones (*heatmap* y *pairplot*) y respaldarlas con coeficientes calculados.
3. **Detectar correlaciones engañosas** y evitar conclusiones causales.
4. **Documentar supuestos, hallazgos y limitaciones.**
5. **Convertir la evidencia en recomendaciones de negocio** prudentes.

## 🛠️ Herramientas y Entorno de Desarrollo

* **Entorno:** Google Colab / Jupyter Notebook
* **Lenguaje:** Python
* **Librerías principales:**
  * `pandas` y `numpy` para manipulación de datos.
  * `seaborn` y `matplotlib` para visualización.
  * `scipy.stats` para correlaciones y pruebas estadísticas.

## 📊 Estructura del Dataset

El conjunto de datos (`/datasets/novaretail_comportamiento_clientes_2024.csv`) contiene **15,000 filas y 12 columnas**:

| Columna | Tipo de dato | Descripción |
| :--- | :--- | :--- |
| `id_cliente` | `string` | Identificador único del cliente. |
| `edad` | `int` | Edad del cliente. |
| `nivel_ingreso` | `float` | Ingreso anual estimado del cliente. |
| `visitas_mes` | `int` | Visitas a la app o sitio web en el mes. |
| `compras_mes` | `int` | Compras realizadas en el mes. |
| `gasto_publicidad_dirigida` | `float` | Gasto en anuncios asignado al usuario. |
| `satisfaccion` | `float` | Calificación de satisfacción (escala de 1 a 5). |
| `miembro_premium` | `int` (0/1) | Suscripción premium (1) o estándar (0). |
| `abandono` | `int` (0/1) | Abandonó la plataforma (1) o sigue activo (0). |
| `tipo_dispositivo` | `string` | Dispositivo utilizado (móvil, escritorio, tablet). |
| `region` | `string` | Región geográfica (norte, sur, oeste, este). |
| `ingreso_anual` | `float` | **Métrica foco:** ingreso anual generado por el cliente para la empresa. |

## 🔍 Flujo de Trabajo y Metodología

1. **Carga y exploración inicial:** validación de tipos, ausencia de nulos y diagnóstico de variables numéricas (media, mediana, percentil 75, máximo y desviación estándar, con atención al sesgo y a posibles valores atípicos).
2. **Preparación y limpieza:** ajuste de formatos y clasificación de variables (numéricas, binarias y categóricas).
3. **Análisis exploratorio y visualización:** *heatmap* de correlación y *pairplot* que incluye `ingreso_anual`, con transparencia en los puntos para reducir la superposición.
4. **Coeficientes de asociación**, centrados en `ingreso_anual`:
   * **Pearson / Spearman:** `compras_mes` y `visitas_mes` frente a `ingreso_anual`.
   * **Punto-biserial:** `miembro_premium` y `abandono` frente a `ingreso_anual`.
   * **V de Cramér:** pares entre `region`, `tipo_dispositivo`, `miembro_premium` y `abandono`.
5. **Interpretación y hallazgos:** conclusiones redactadas en términos de asociación, no de causalidad.
6. **Limitaciones y próximos pasos.**

## 💡 Hallazgos Principales

* **`compras_mes` e `ingreso_anual` se mueven casi al unísono (Pearson = 0.967, Spearman = 0.967).** La asociación es muy fuerte y consistente, y los clientes con 0 compras tienen ingreso 0. Esto sugiere que `ingreso_anual` probablemente se construye a partir de las compras, así que el 0.97 puede reflejar cómo se calcula la variable más que un hallazgo independiente sobre el comportamiento. Antes de usarlo como evidencia hay que verificar su construcción (por ejemplo, con el ticket implícito `ingreso_anual / compras_mes`).
* **Las visitas y la publicidad dirigida se asocian débilmente con `ingreso_anual`.** `visitas_mes` muestra una asociación positiva débil a moderada (Pearson = 0.337, Spearman = 0.321), y `gasto_publicidad_dirigida` una más débil (r ≈ 0.20, tomado del heatmap). Las visitas pueden verse como una señal modesta del valor del cliente. Entre predictores, visitas y gasto publicitario se mueven juntos (Pearson = 0.58, Spearman = 0.56), pero esto no permite concluir que la publicidad genere visitas: el gasto se asigna por usuario y podría dirigirse a quienes ya visitan más.
* **Membresía premium y abandono: asociaciones débiles.** `miembro_premium` tiene una asociación positiva muy débil con `ingreso_anual` (punto-biserial = 0.093), y `abandono` prácticamente nula (-0.003), por lo que el ingreso no distingue a quienes abandonan de quienes se quedan. La asociación más alta entre variables categóricas fue `miembro_premium` vs `abandono` (V de Cramér = 0.12), consistente con el -0.12 del heatmap: los miembros premium tienden a abandonar algo menos.
* **Edad, satisfacción, nivel de ingreso, región y tipo de dispositivo:** no muestran evidencia de asociación relevante con `ingreso_anual` o con `abandono` (V de Cramér ≤ 0.02 en los demás pares). Esto no demuestra independencia: son medidas de fuerza, no pruebas de significancia.

## ⚠️ Limitaciones

* **Correlación ≠ causalidad:** los coeficientes describen asociaciones, no efectos.
* **Posible correlación por construcción** entre `ingreso_anual` y `compras_mes`.
* **Alcance de los coeficientes:** Pearson y Spearman solo capturan patrones lineales y monótonos; no se calcularon valores p.
* **Desbalance de clases:** cerca del 86% de los clientes es estándar y cerca del 15% abandonó, lo que vuelve menos estables los coeficientes con estas variables.
* **Valores atípicos y sesgo a la derecha** en varias variables numéricas, en especial `ingreso_anual` y `compras_mes`.
* **Variables no probadas frente a `ingreso_anual`:** región y tipo de dispositivo solo se evaluaron entre sí y con `abandono`, por lo que no se descarta su papel como variables de confusión.
* **Análisis transversal** del período 2024, sin series temporales.

## 🚀 Próximos Pasos

1. **Verificar la construcción de `ingreso_anual`** y separar frecuencia de compra y ticket promedio como palancas de valor.
2. **Comparar el ingreso por región y tipo de dispositivo** para evaluar posibles variables de confusión, y profundizar en el segmento estándar para campañas de conversión a premium.
3. **Modelar el abandono** (regresión logística o árboles de decisión) combinando variables, manejando el desbalance de clases. Se justifica porque ninguna métrica individual lo explica de forma lineal.
4. **Evaluar el ROI de la publicidad dirigida** frente al LTV, con comparación entre grupos o una prueba controlada.

## 🚀 Cómo Ejecutar el Proyecto

1. **Google Colab:** sube el archivo `.ipynb` a tu Google Drive, ábrelo con Colab y ejecuta las celdas en orden.
2. **Entorno local (Jupyter):**
   * Clona este repositorio:
     ```bash
     git clone https://github.com/tu-usuario/proyecto-novaretail.git
     ```
   * Instala las librerías requeridas (`pandas`, `numpy`, `seaborn`, `matplotlib`, `scipy`).
   * Abre el cuaderno y ejecútalo paso a paso.

*Desarrollado como parte del programa de análisis de datos y ciencia de datos.*
