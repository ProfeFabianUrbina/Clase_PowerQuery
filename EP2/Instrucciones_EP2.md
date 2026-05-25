# Evaluación Parcial N°2: Consolidación y Modelado de Datos
**Asignatura:** Herramientas Tecnológicas III (GAA1103)  
**Ponderación:** 30% de la nota final  
**Formato:** Entrega de encargo (Sin presentación)  
**Tiempo asignado:** 2 horas pedagógicas (Individual)  
**Lugar:** Laboratorio de Computación  

---

## 1. Descripción General
El propósito de esta evaluación es medir tu capacidad para integrar, transformar, limpiar y modelar datos provenientes de distintas fuentes, asegurando la reducción de anomalías y la correcta estructuración de la información para la toma de decisiones.

### Indicadores de Logro Evaluados:
* **IL2.1:** Analiza el sistema de información, para normalizar la base de datos en la que se trabajará.
* **IL2.2:** Genera respuestas a desafíos relacionados con la gestión de datos, a través de la ejecución de diversas funciones de Excel.
* **IL2.3:** Crea base de datos en Excel, considerando la reducción del número de anomalías.
* **IL2.4:** Genera soluciones fundamentadas en funciones avanzadas de la gestión de datos, para comunicar y organizar la información.

---

## 2. Contexto del Caso: "Udemia"
**Udemia** es una plataforma internacional de aprendizaje en línea. Actualmente, la información de sus cursos se encuentra descentralizada y distribuida en **4 archivos distintos** correspondientes a sus áreas de negocio. 

Como especialista, has sido asignado para realizar el proceso de extracción, transformación, limpieza e integración de estos datos en una solución unificada.

### Materiales e Insumos Disponibles (Disponibles en GitHub / Carpeta EP2):
* `Curso- Finanzas.xlsx`
* `Curso- Desarrollador web.xlsx`
* `Curso- Diseño.xlsx`
* `Udemia- Música.csv`

---

## 3. Instrucciones Específicas paso a paso

### Parte I: Extracción, Limpieza y Consolidación (Power Query)
Debes cargar los 4 archivos de insumo a **Power Query** y construir una **arquitectura modular** organizada de la siguiente manera:

1. **Consulta "Raw_Data" (Datos Absolutos):** Carga las fuentes originales. Esta consulta debe permanecer intacta, reflejando los datos sin modificaciones de origen.
2. **Consulta "Staging" (Procesamiento y Limpieza):** En esta etapa intermedia deberás realizar el trabajo de carpintería de datos:
   * Eliminar columnas innecesarias o irrelevantes.
   * Corregir rigurosamente los tipos de datos (Textos, Números Enteros, Monedas).
   * Renombrar columnas para mantener un estándar limpio.
3. **Consulta "Base Maestra" (Resultado Final Normalizado):** Será el resultado final de la consolidación de las 4 áreas. Debe cumplir con los siguientes requisitos:
   * **No debe contener registros duplicados.**
   * Debe incluir exactamente las siguientes **9 columnas**: `ID Curso`, `Nombre`, `URL`, `Cantidad de Suscriptores`, `Cantidad de Visualizaciones`, `Precio`, `Área`, `Ganancias`, `Ranking`.

#### Columnas Calculadas Requeridas:
Dentro de tu consulta final en Power Query o mediante fórmulas analíticas, debes generar de manera automatizada:
* **Ganancias:** Multiplicación de `Precio * Cantidad de Suscriptores`.
* **Ranking:** Clasificación ordenada de los cursos basada en la mayor cantidad de suscriptores.
* **Total por Área:** Muestra la suma totalizada de suscriptores agrupada por cada área (*Finanzas, Web, Música, Diseño*).

> 📊 **Cierre de la Parte I:** Carga los datos a Excel y genera una **Tabla Dinámica** en una pestaña nueva que muestre de forma resumida la **cantidad total de cursos por cada área**.

---

### Parte II: Análisis Crítico de Cursos sin Suscriptores
1. Crea una hoja nueva en tu libro de Excel y llámala **"Análisis sin suscriptores"**.
2. Aplica filtros para aislar exclusivamente aquellos cursos cuya **Cantidad de Suscriptores sea igual a 0**.
3. **Análisis Escrito:** Inserta un cuadro de texto (o utiliza celdas combinadas con ajuste de texto) y redacta un informe profesional sobre este fenómeno.
   * *Preguntas guía:* ¿A qué se debe que estos cursos no tengan alumnos? Sugiere causas lógicas (baja visibilidad en la plataforma, precios desproporcionados, falta de descripciones atractivas, etc.).
4. **Soporte Visual:** Tu análisis debe estar estrictamente respaldado por:
   * Al menos **un (1) Gráfico Dinámico** que represente visualmente cómo se distribuyen estos cursos sin alumnos entre las distintas áreas.
   * **Tablas de datos** que justifiquen y demuestren numéricamente tus conclusiones.

---

### Parte III: Modelo Relacional y Power Pivot
Diseña y estructura un **Modelo Entidad-Relación (ERD)** básico para la plataforma Udemia utilizando las herramientas de modelado de Excel (**Power Pivot**):

1. **Entidades Sugeridas:**
   * **Tabla Curso:** Atributos de `ID`, `Nombre`, `URL`, `Precio`, `Visualizaciones`, `Suscriptores`.
   * **Tabla Área:** Atributos de `Nombre del área` y `Total de cursos`.
2. **Relaciones:** Crea las conexiones lógicas correspondientes entre las tablas dentro de la vista de diagrama de Power Pivot.
3. **Representación Gráfica (Opcional):** Puedes añadir una representación visual de este diagrama conceptual en una pestaña de Excel utilizando Formas o herramientas de SmartArt.

---

## 4. Formato de Entrega y Archivos
Para que tu evaluación sea válida, debes subir a la plataforma de entrega los siguientes archivos guardados estrictamente en formato de libro de Excel estándar (`.xlsx` o `.xls` según determine la sección):

* `Nombre_Apellido_Base_Maestra.xlsx` (Tu archivo central de desarrollo con Power Query, tablas dinámicas y modelo).
* `Nombre_Apellido_Finanzas.xlsx`
* `Nombre_Apellido_DesarrolladorWeb.xlsx`
* `Nombre_Apellido_Diseño.xlsx`

**Cronograma:** Las instrucciones se entregan oficialmente en la **Semana 8** y el encargo final consolidado se recibe en la **Semana 10**.

---

## 5. Pauta de Evaluación (Rúbrica de Logro)

| Indicador de Evaluación (IE) | Muy Buen Desempeño (100%) | Buen Desempeño (80%) | Desempeño Aceptable (60%) | Desempeño Incipiente (30%) | No Logrado (0%) | Ponderación |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| **IE1: Análisis y Normalización** *(IL 2.1)* | Consolida con éxito los 4 archivos de origen mediante consultas modulares (Raw, Staging, Base Maestra), incluyendo las 9 columnas requeridas y eliminando duplicados de forma óptima. | Consolida los 4 archivos, pero incluye columnas innecesarias (más de 7 adicionales) o contiene inconsistencias menores en la limpieza de datos. | Consolida entre 3 archivos utilizando una estructura parcial, omitiendo columnas obligatorias o mostrando errores evidentes de tipos de datos. | Consolida 2 o menos archivos sin aplicar un orden modular, dejando campos incompletos o registros duplicados. | No realiza el proceso de consolidación ni de transformación modular de los datos de origen. | **20%** |
| **IE2: Desafíos y Fórmulas** *(IL 2.2)* | Crea de forma 100% automatizada y correcta las columnas de Ganancias, Ranking y Total por Área mediante el uso adecuado de funciones o fórmulas de Excel. | Crea 2 de las 3 columnas solicitadas utilizando fórmulas correctas o con fallas leves de sintaxis. | Crea solo 1 columna calculada de manera correcta o presenta errores conceptuales menores en las demás. | Intenta crear al menos 1 columna usando fórmulas, pero los resultados arrojan errores (`#¡VALOR!`, `#N/D`, etc.). | No crea ninguna de las columnas calculadas requeridas por la pauta. | **20%** |
| **IE3: Reducción de Anomalías** *(IL 2.3)* | Presenta un análisis escrito claro, coherente y lógicamente argumentado, respaldado por al menos 1 gráfico dinámico, 1 tabla de datos y sugerencias viables para el caso. | Presenta un análisis descriptivo parcial que se apoya en solo una de las visualizaciones requeridas (solo la tabla o solo el gráfico). | Presenta un texto de análisis plano en celdas, sin utilizar visualizaciones interactivas ni justificar los argumentos con métricas del caso. | El análisis entregado es marcadamente incompleto, superficial o carece de relación lógica con la problemática de los cursos sin suscriptores. | No realiza ni entrega ningún tipo de análisis o diagnóstico de la base de datos de cursos. | **30%** |
| **IE4: Soluciones Fundamentadas** *(IL 2.4)* | Modela una arquitectura ER correcta y funcional mediante Power Pivot con las entidades Curso y Área bien estructuradas y sus relaciones correctamente vinculadas. | Representa el modelo relacional con las entidades solicitadas, pero evidencia fallas menores en la definición de llaves, atributos o cardinalidad. | Representa de forma aislada las entidades del negocio, pero no establece relaciones claras entre ellas o contiene severos errores conceptuales. | Entrega un esquema de modelo completamente incompleto, desorganizado y sin una lógica de bases de datos relacionales. | No diseña ni entrega ningún tipo de modelo relacional ni de conexiones en Power Pivot. | **30%** |
