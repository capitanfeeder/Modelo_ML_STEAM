## PI_1-MLOps Juegos Steam - Modelo de recomendación

Repositorio correspondiente al Proyecto Individual 1 del bootcamp de Machine Learning en Henry.

### Descripción del Proyecto:

Este proyecto tiene como finalidad simular las responsabilidades de un MLOps Engineer, que desempeña un papel combinado de Data Engineer y Data Scientist, dentro del entorno de la plataforma de juegos Steam. El desafío empresarial planteado consiste en desarrollar un `Producto Mínimo Viable (MVP)`. Este MVP incluirá una `API` implementada, junto con un modelo de `Machine Learning` que realizará un análisis de sentimientos basado en los comentarios de los usuarios y proporcionará un sistema de recomendación de videojuegos para la plataforma.

### Datos:

El proyecto se basa en tres archivos de tipo JSON y vienen comprimidos:

+ **output_steam_games.json**: Contiene información detallada sobre los juegos, incluyendo nombre, desarrollador, género y etiquetas.

+ **australian_users_items.json**: Proporciona información sobre los juegos utilizados por los usuarios y la cantidad de tiempo que cada usuario ha dedicado a un juego.

+ **australian_users_reviews.json**: Contiene los comentarios de los usuarios sobre los juegos, así como sus recomendaciones y la fecha de los mismos.


### Tareas desarrolladas:

#### ETL (Extracción, Transformación y Carga)

Para el análisis de los archivos creamos los Notebooks [ETL_JSON(output_steam_games)](/1-ETL_JSON(output_steam_games).ipynb),[ETL_JSON(australian_users_items)](/2-ETL_JSON(australian_users_items).ipynb) y [ETL_JSON(australian_user_reviews)](/3-ETL_JSON(australian_user_reviews).ipynb).

En esta etapa del proyecto, se llevó a cabo la extracción de datos desde los dataframes iniciales con el fin de familiarizarse con ellos y comenzar la fase de 'limpieza de datos'. Para lograr esto, se consideraron las directrices proporcionadas en el enunciado del proyecto, eliminando todo lo que pudiera obstaculizar el correcto entendimiento y la lectura del archivo, con el propósito de alcanzar los objetivos establecidos.

Se empleó la biblioteca 'NLTK' en la columna 'reviews', que contiene los comentarios de los usuarios en el conjunto de datos de 'reviews'. Se realizó un análisis de sentimientos clasificando los comentarios según la polaridad del sentimiento en positivos (2), neutrales (1) y negativos (0), y como resultado se creó una nueva columna llamada 'sentiment_analysis'.

Concluida la fase de limpieza, se generaron los conjuntos de datos para la siguiente etapa, comprimiéndolos en formato 'parquet'.

#### EDA (Análisis Exploratorio de Datos)

Durante esta etapa del proyecto, se llevó a cabo el análisis de los tres conjuntos de datos después del proceso ETL, con el objetivo de lograr una visualización más clara de cada variable categórica y numérica. El propósito principal fue identificar las variables esenciales para los endpoints y el modelo de recomendación, que constituyen el objetivo final del aprendizaje automático. Por último, se crearon nuevos datasets que se utilizaron en la fase de 'feature engineering'.

Notebook [Analisis exploratorio](/4-EDA.ipynb)

#### Creación de funciones

En esta fase del proyecto, después de depurar la información, se seleccionaron los conjuntos de datos necesarios para abordar cada función específica. Este enfoque se llevó a cabo con el objetivo de lograr una optimización significativa y mejorar los tiempos computacionales asociados a cada tarea.

Las funciones creadas son las siguientes: 

* **`PlayTimeGenre`**: Esta función recibe como parámetro un género y devuelve el año con mas horas jugadas para dicho género.

* **`UserForGenre`**: Esta función recibe un género y devuelve el usuario con mayor tiempo de juego en un diccionario donde la clave es el año y el valor la acumulación de tiempo de juego para cada uno.

* **`UserRecommend`**: Esta función recibe un año y devuelve el Top 3 de juegos recomendados para dicho período.

* **`UsersWorstDeveloper`**: Esta función recibe de parámetro un año y retorna un Top 3 de peores empresas desarrolladoras para ese año basándose en el análisis de sentimientos en las reviews.

* **`sentiment_analysis`**: Esta función toma el año de lanzamiento de un juego como parámetro y devuelve una lista que contiene la cantidad de registros de reseñas de usuarios clasificados con un análisis de sentimiento, ya sea Negativo, Neutral o Positivo, correspondientes a ese año.

Notebook [Funciones_Endpoints](/5-Funciones_Endpoints.ipynb)

#### Modelado Machine Learning

En esta etapa del proyecto, se utilizan los conjuntos de datos obtenidos durante las fases de ETL y EDA. Se centra particularmente en el conjunto de datos llamado modelo_item, el cual incluye columnas que contienen información sobre los géneros de videojuegos, los títulos y sus identificaciones. 

* **`recomendacion_juego`**: Esta función acepta el parámetro "item_id" de un título de juego y genera una lista que incluye los cinco juegos más similares al ingresado, proporcionando recomendaciones basadas en la similitud de género. Este enfoque busca ofrecer sugerencias relevantes y específicas, teniendo en cuenta las preferencias de género del juego proporcionado. Realizando una comparación  `item_item`.

Notebook [Modelado_ML](/6-Modelado_ML.ipynb)

### FastAPI

El código para generar la API se encuentra en el archivo [Main](/main.py). En caso de querer ejecutar la API desde localHost se deben seguir los siguientes pasos:

- Clonar el proyecto haciendo `git clone https://github.com/capitanfeeder/Modelo_ML_STEAM.git`.
- Preparación del entorno de trabajo en Visual Studio Code:
    * Crear entorno `python -m venv env`
    * Ingresar al entorno haciendo `env\Scripts\activate`
    * Instalar dependencias con `pip install -r requirements.txt`
- Ejecutar el archivo `main.py` desde consola activando uvicorn. Para ello, hacer `uvicorn main:app --host 127.0.0.1 --port 8000`
- Hacer Ctrl + clic sobre la dirección `http://XXX.X.X.X:XXXX` (se muestra en la consola).
- Una vez en el navegador, agregar `/docs` para acceder.
- En cada una de las funciones hacer clic en *Try it out* y luego introducir el dato que requiera o utilizar los ejemplos por defecto. Finalmente Ejecutar y observar la respuesta.


### Deploy 

Despliegue en Railway:
Se eligió la plataforma Railway para implementar la API. Railway se presenta como una solución de nube integral diseñada para la creación y ejecución de aplicaciones y sitios web. Su funcionalidad de despliegue automático directamente desde GitHub añade eficiencia al proceso de implementación.

Elección sobre Render:
La preferencia por Railway en lugar de Render se basa en varias consideraciones. Railway ofrece una experiencia de despliegue más integrada y automatizada, permitiendo una implementación más fluida y eficiente desde el repositorio de GitHub. Esta característica, combinada con la versatilidad y facilidad de uso de Railway, hizo que fuera la elección preferida para este proyecto en comparación con Render. 

* Se generó un nuevo servicio en `railway.app`, conectando a este repositorio

* Proporciono el link donde queda corriendo https://modelomlsteam-production.up.railway.app/docs#/ 


### Video

Explicación y demostración del funcionamiento de la API en el [Video](https://youtu.be/RP9muYjjTjw)


### Conclusiones 

La ejecución del proyecto se basó en la aplicación de conocimientos adquiridos durante el programa de Data Science en HENRY. Las labores abordadas abarcan las responsabilidades típicas de un Data Engineer y un Data Scientist.

Se ha alcanzado con éxito la meta de desarrollar un Producto Mínimo Viable (MPV), que engloba una API junto con su implementación en un servicio web. Aunque se logró cumplir con el objetivo establecido, es esencial destacar que, debido a limitaciones de almacenamiento, en algunos casos se han llevado a cabo procesos básicos. Por ende, existe margen para optimizar aún más las funciones empleadas y obtener resultados más eficientes.


## Autor ✒️
* **Osvaldo Gabriel Sosa**  - [LinkedIn](https://www.linkedin.com/in/gabriel-sosa26)