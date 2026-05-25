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

### Materiales e Insumos Disponibles (en la nube):
* `Curso-Finanzas.csv`: https://raw.githubusercontent.com/ProfeFabianUrbina/Clase_PowerQuery/refs/heads/main/EP2/Curso-Finanzas.csv
* `Curso-Desarrollador web.csv`: https://raw.githubusercontent.com/ProfeFabianUrbina/Clase_PowerQuery/refs/heads/main/EP2/Curso-DesarrolladorWeb.csv
* `Curso-Diseño.csv`: https://raw.githubusercontent.com/ProfeFabianUrbina/Clase_PowerQuery/refs/heads/main/EP2/Curso-Diseno.csv
* `Udemia-Música.csv`: https://raw.githubusercontent.com/ProfeFabianUrbina/Clase_PowerQuery/refs/heads/main/EP2/Udemia-Musica.csv
* `Precios.csv`: https://raw.githubusercontent.com/ProfeFabianUrbina/Clase_PowerQuery/refs/heads/main/EP2/Precios.csv
---

## 3. Instrucciones Específicas paso a paso

### Parte I: Extracción, Limpieza y Consolidación (Power Query)
Debes cargar los 5 archivos de insumo a **Power Query** y construir una **arquitectura modular** organizada de la siguiente manera:

1. **Conecta tu archivo a las 5 fuentes de información, crea un "grupo" (carpeta) en el área de consultas llamado "Originales". 
2. **Asegurate de que los documentos se importan adecuadamente como tablas, sino modifiquelos en "Origen" según la extensión del archivo y el delimitador adecuado. Recuerde promover los encabezados cuando corresponda.
3. **Duplica las 5 consultas/tablas y guarda los originales en un grupo que debes crear en la zona e consultas. Modifica el nombre de las consultas originales de la siguiente manera del ejemplo: `Curso- Finanzas` se modifica como `Curso-Finanzas-RAW`
4. **Anexar Consulta:
   * Verifica que las 4 consultas (Curso-Finanzas, Curso-Desarrollador, Curso-Diseño y Udemia-Música) tengan los mismos nombres y los mismos tipos de datos para cada campos. 
   * Los campos resultantes deben ser: ID_Curso, Área, Nombre_Curso, URL, Precio, Sucriptores, Vistas y Nivel. 
     Todos son campos del tipo texto (ABC), salvo los campos Precio, Visitas, Suscriptores, que son de número entero (123). Si un campo numérico fue reconocido como texto, es probable que debas reemplazar espacio, nulos (null) u otros caracteres. Si no tiene el valor se debe reemplazar por cero (0).
   * Genera un consulta nueva llamada "Maestro Cursos" que debe ser un "anexo" de las 4 consultas. 
5. **Normalización:** 
   * Elimina columna URL
   * Columna Área: Asegurate que la columna "Área", sólo tiene 4 valores distintos (en el filtro puedes poner "Cargar más" para ver la totalidad de los datos). Utiliza formato poner en mayuscula cada palabra. Filtra los registros que se encuentren en blanco o nulos.
   * Columna Nivel: Asegurate que sólo existan valores válidos (Nivel Principiante, Nivel Intermedio, Nivel Experto y Todos los niveles). Registros en blanco, errores o nulos deben ser filtrados. Cambia el formato a poner en mayuscula cada palabra.
6. **Consulta "Base Maestra" (Resultado Final Normalizado):** Será el resultado final de la consolidación de las 4 áreas. Debe cumplir con los siguientes requisitos:
   * **No debe contener registros duplicados.**
   * Debe incluir exactamente las siguientes **7 columnas**: `ID_Curso`, `Área`, `Nombre_Curso`, `Precio`, `Suscriptores`, `Vistas`, `Nivel`
7. **Combinar Consultas:**
   * En la misma consulta "Base Maestra", combina con la consulta Precios a traves del campo ID_Curso. Expande el campo "Precio" solamente. En la tabla precios no están todos los códigos, por lo tanto no existirá respuesta para todos los ID_Curso. Cambia el nombre de la nueva columna como "Precio_Actualizado"
   * En la nueva consulta, reemplaza los valores "null" como 0   

#### Columnas Calculadas y Condicionales Requeridas:
Dentro de tu consulta "Base Maestra" en Power Query, debes generar de manera automatizada:
* Columnas Condicional: **Precio_Final**: Si la columna "Precio_Actualizado" es mayor que el valor de "Precio" entonces deben dejar el valor de la columna "Precio_Actualizado", de lo contrario dejarán el valor de la columna "Precio"
* Columna Personalizada: **Ingresos:** Multiplicación de `Precio_Final * Suscriptores`.
* Columna Personalizada: **Ranking:** Clasificación ordenada de los cursos basada en la mayor cantidad de suscriptores, ordenando los registros de la tabla y luego agregándo un índice, renombra la columna como "Ranking" 


**Cierre de la Parte I:** Carga los datos a Excel como "Cerrar y cargar en", y luego escoge "Crear unicamente la conexión". Posteriormente en la opción Consultas y Conexiones en el excel, escoge la consulta "Maestro Cursos" y en "Cargar en" elige mostrarla como una Tabla en una Hoja nueva.

---

### Parte II: Análisis Crítico
Tabla 1:
1. A partir de la Tabla "Maestro Cursos" crea una tabla dinámica en un hoja nueva y llámala **"Análisis"**.
2. Aplica filtros para aislar exclusivamente aquellos cursos cuya **Cantidad de Suscriptores sea igual a 0**.
3. **Tabla y gráfico dinámico:** Muestra la cantidad de cursos sin suscriptores por cada Área, muestralo en la tabla dinámica y en un gráfico dinámico.

Tabla 2:
1. Genera una nueva tabla y gráfico dinámico en la misma hoja "Análisis".
2. En esta tabla y gráfico muestra cuandos Ingresos se generan por cada Nivel


## 3. Formato de Entrega y Archivos
Entrega tu documento de excel finalizado como "EP2_Apellido_Nombre.xlsx"

## 5. Pauta de Evaluación (Rúbrica de Logro)

| Indicador de Evaluación (IE) | Muy Buen Desempeño (100%) | Buen Desempeño (80%) | Desempeño Aceptable (60%) | Desempeño Incipiente (30%) | No Logrado (0%) | Ponderación |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| **IE1: Análisis y Normalización** *(IL 2.1)* | Consolida con éxito los 4 archivos de origen mediante consultas modulares (Raw, Staging, Base Maestra), incluyendo las 9 columnas requeridas y eliminando duplicados de forma óptima. | Consolida los 4 archivos, pero incluye columnas innecesarias (más de 7 adicionales) o contiene inconsistencias menores en la limpieza de datos. | Consolida entre 3 archivos utilizando una estructura parcial, omitiendo columnas obligatorias o mostrando errores evidentes de tipos de datos. | Consolida 2 o menos archivos sin aplicar un orden modular, dejando campos incompletos o registros duplicados. | No realiza el proceso de consolidación ni de transformación modular de los datos de origen. | **20%** |
| **IE2: Desafíos y Fórmulas** *(IL 2.2)* | Crea de forma 100% automatizada y correcta las columnas de Ganancias, Ranking y Total por Área mediante el uso adecuado de funciones o fórmulas de Excel. | Crea 2 de las 3 columnas solicitadas utilizando fórmulas correctas o con fallas leves de sintaxis. | Crea solo 1 columna calculada de manera correcta o presenta errores conceptuales menores en las demás. | Intenta crear al menos 1 columna usando fórmulas, pero los resultados arrojan errores (`#¡VALOR!`, `#N/D`, etc.). | No crea ninguna de las columnas calculadas requeridas por la pauta. | **20%** |
| **IE3: Reducción de Anomalías** *(IL 2.3)* | Presenta un análisis escrito claro, coherente y lógicamente argumentado, respaldado por al menos 1 gráfico dinámico, 1 tabla de datos y sugerencias viables para el caso. | Presenta un análisis descriptivo parcial que se apoya en solo una de las visualizaciones requeridas (solo la tabla o solo el gráfico). | Presenta un texto de análisis plano en celdas, sin utilizar visualizaciones interactivas ni justificar los argumentos con métricas del caso. | El análisis entregado es marcadamente incompleto, superficial o carece de relación lógica con la problemática de los cursos sin suscriptores. | No realiza ni entrega ningún tipo de análisis o diagnóstico de la base de datos de cursos. | **30%** |
| **IE4: Soluciones Fundamentadas** *(IL 2.4)* | Modela una arquitectura ER correcta y funcional mediante Power Pivot con las entidades Curso y Área bien estructuradas y sus relaciones correctamente vinculadas. | Representa el modelo relacional con las entidades solicitadas, pero evidencia fallas menores en la definición de llaves, atributos o cardinalidad. | Representa de forma aislada las entidades del negocio, pero no establece relaciones claras entre ellas o contiene severos errores conceptuales. | Entrega un esquema de modelo completamente incompleto, desorganizado y sin una lógica de bases de datos relacionales. | No diseña ni entrega ningún tipo de modelo relacional ni de conexiones en Power Pivot. | **30%** |
