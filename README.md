# Agustín Pluda

**Data Science · Data Engineering · Analytics**

Estudiante de Ingeniería en Informática. Acá están reunidos los proyectos que uso para mostrar mi
trabajo: cada uno resuelve un problema de punta a punta —desde el dato crudo y sucio hasta el
hallazgo comunicado— y documenta el porqué de cada decisión, no sólo el resultado.

Están armados con un criterio deliberado: cada proyecto nuevo cubre una herramienta o un dominio que
los anteriores no mostraban. Por eso conviven el modelado y la construcción de pipelines —capas
`raw` → `core` → `marts`, ETL y cubos OLAP—, el machine learning aplicado, el SQL analítico y la
visualización en Power BI y Tableau, sobre dominios tan distintos como la banca minorista, el retail
mayorista y la logística portuaria.

## Índice

- [Proyectos personales](#proyectos-personales)
- [Proyectos universitarios (grupales)](#proyectos-universitarios-grupales)
- [Proyectos de práctica](#proyectos-de-práctica)
- [Contacto](#contacto)

---

## Proyectos personales

### [Czech Bank SQL Analytics](https://github.com/AgusPluda/czech-bank-sql-analytics)

Análisis del comportamiento financiero de un banco minorista checo (1993-1998) resuelto íntegramente
en PostgreSQL, sin notebooks: un modelo en tres capas (`raw` → `core` → `marts`) construido desde 8
tablas relacionales sin limpiar y 1.056.320 transacciones, y 13 preguntas de negocio contestadas en
SQL puro —una por archivo versionado—, incluyendo un problema de *gaps-and-islands* para detectar
rachas de descubierto y un módulo de riesgo crediticio con control explícito de *leakage* temporal.
Los hallazgos se comunican en 4 dashboards interactivos publicados en Tableau Public.

**Stack:** PostgreSQL 18 (CTEs, window functions, `DISTINCT ON`, `COPY`) · SQL · Python 3.14 (`psycopg`, sólo para ingesta y exportación) · Tableau Public

### [Product Classifier Project](https://github.com/AgusPluda/product-classifier-project)

Clasificación de un catálogo de 4.724 productos que no tenía columna de categoría, mediante *weak
supervision*: reglas de keywords generan las etiquetas de entrenamiento, un set gold de 400 productos
etiquetado a mano —a ciegas, sin ver la predicción de las reglas— funciona como única fuente de verdad
confiable, y un TF-IDF + SVM lineal se entrena sobre las reglas pero se **evalúa contra el gold**, que
es la única forma honesta de saber si generaliza. Las 15 categorías resultantes alimentan un análisis
de ventas y un dashboard de 4 páginas en Power BI, cuyo layout se genera y verifica por código en vez
de armarse a mano.

**Stack:** Python 3.14 · Pandas / NumPy · scikit-learn (TF-IDF, K-Means, SVM lineal, `GridSearchCV`) · Matplotlib / Seaborn · Jupyter Notebook · Power BI Desktop

### [Online Retail Analysis](https://github.com/AgusPluda/online-retail-analysis)

Análisis exploratorio completo sobre el dataset Online Retail II (más de un millón de filas), con un
proceso de limpieza y curado justificado paso a paso: nulos, duplicados, códigos administrativos no
comerciales, y cantidades y precios negativos. Sobre esa base, hallazgos de negocio sobre artículos,
facturas, concentración de clientes, estacionalidad y geografía, cerrando con una hipótesis
—¿se cancelan más las facturas grandes?— contrastada con una prueba de Mann-Whitney U.

**Stack:** Python · Pandas / NumPy · Matplotlib / Seaborn · SciPy · Jupyter Notebook

---

## Proyectos universitarios (grupales)

Trabajos prácticos de Ingeniería en Informática (Universidad Católica de Santiago del Estero,
Departamento Académico Rafaela), reorganizados y documentados después de la entrega. En cada uno
detallo cuál fue mi participación dentro del grupo.

### [Data Warehouse y cubos OLAP para logística internacional](https://github.com/AgusPluda/bdd3-tp2-DW-OLAP)

Trabajo Práctico Final de Base de Datos III (2025). Data Warehouse en **esquema de constelación**
sobre SQL Server para una naviera de contenedores: dos tablas de hechos —contratos e inventario— que
comparten dos dimensiones conformadas, alimentadas por un ETL de once flujos en SSIS y explotadas por
tres cubos multidimensionales en Analysis Services, más una notebook PySpark sobre Google Colab. El
README documenta con detalle tanto el diseño como los once defectos que hoy corregiría.

*Mi participación:* el proyecto completo de Analysis Services —Data Source View, las diez dimensiones
con sus jerarquías y los tres cubos, incluido el que cruza ambos grupos de medida— y la notebook de
PySpark, además de la generación de los datos operacionales.

**Stack:** SQL Server 2022 · SQL Server Integration Services (SSIS) · Analysis Services multidimensional (MOLAP) · Visual Studio 2022 · PySpark / Google Colab · JDBC

### [Gestión de Puertos con PostGIS](https://github.com/AgusPluda/bdd2-tp2-postgis)

Trabajo Práctico N°2 de Base de Datos II (2024). Base de datos **geoespacial** de cuatro puertos
argentinos con sus muelles, amarres, equipos y navíos. La decisión que sostiene todo el trabajo es
modelar el puerto como un polígono y no como un punto: eso permite resolver qué amarres le pertenecen
por contención geométrica en lugar de por clave foránea, y que la distancia de un navío sea al borde
real del puerto y no a un centroide arbitrario. El schema es una reconstrucción **verificable**: se
contrasta automáticamente contra los ocho resultados publicados en el informe original de 2024.

*Mi participación:* el modelado y la carga de datos —diseño del schema, relevamiento de los polígonos
de los cuatro puertos y carga de amarres, equipos y navíos—, las tres consultas espaciales del
ejercicio VI, y la instalación de PostGIS con la visualización sobre el Geometry Viewer.

**Stack:** PostgreSQL 16 · PostGIS 3.4 (EPSG:4326, índices GiST) · pgAdmin Geometry Viewer · Docker Compose

---

## Proyectos de práctica

Proyectos más acotados que los anteriores: dos ejercicios guiados del career path *Data Scientist*
de Codecademy, que recorren el circuito completo de análisis exploratorio, y un tercero de práctica
autodirigida para incorporar herramientas puntuales de ingeniería de datos.

### [BCRA Data Pipeline](https://github.com/AgusPluda/bcra-data-pipeline)

Pipeline de datos que extrae 5 series económicas de la API del BCRA, las carga de forma idempotente
en PostgreSQL y las transforma con dbt (capas staging → mart, con tests que cortan el pipeline si
fallan), todo orquestado por Airflow y empaquetado en Docker Compose. Construido específicamente para
practicar orquestación y transformación-como-código antes de encarar un proyecto de ingeniería de
datos más grande.

**Stack:** Apache Airflow 3 (LocalExecutor) · dbt · PostgreSQL · Docker Compose · Python

### [Life Expectancy & GDP Analysis](https://github.com/AgusPluda/life-expectancy-gdp-analysis)

Análisis exploratorio de la evolución de la esperanza de vida y el PBI de seis países (Chile, China,
Alemania, México, Estados Unidos y Zimbabue) entre 2000 y 2015, guiado por preguntas: cada
visualización responde una. Examina la relación entre ambas variables tanto en el conjunto agregado
(r = 0,79) como dentro de cada país por separado, donde la correlación resulta bastante más fuerte
(r entre 0,93 y 0,98).

**Stack:** Python · Pandas / NumPy · Matplotlib / Seaborn · Jupyter Notebook

### [Medical Insurance Cost Analysis](https://github.com/AgusPluda/insurance-cost-analysis)

Análisis exploratorio de los factores demográficos y de estilo de vida que más influyen en el costo
de un seguro médico individual —edad, IMC, tabaquismo, región, sexo y cantidad de dependientes—, con
cada visualización respondiendo una pregunta de negocio concreta. El resultado más claro es que el
tabaquismo es, por lejos, el factor más asociado a un costo alto.

**Stack:** Python · Pandas / NumPy · Matplotlib / Seaborn · Jupyter Notebook

---

## Contacto

- **GitHub:** [github.com/AgusPluda](https://github.com/AgusPluda)
- **LinkedIn:** [linkedin.com/in/agustinpluda](https://www.linkedin.com/in/agustinpluda/)
