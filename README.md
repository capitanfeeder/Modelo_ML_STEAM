## PI_1-MLOps Juegos Steam - Modelo de recomendación

Repositorio correspondiente al Proyecto Individual 1 del bootcamp de Machine Learning en Henry.

### Descripción del Proyecto:

Este proyecto tiene como finalidad simular las responsabilidades de un MLOps Engineer, que desempeña un papel combinado de Data Engineer y Data Scientist, dentro del entorno de la plataforma de juegos Steam. El desafío empresarial planteado consiste en desarrollar un `Producto Mínimo Viable (MVP)`. Este MVP incluirá una `API` implementada, junto con un modelo de `Machine Learning` que realizará un análisis de sentimientos basado en los comentarios de los usuarios y proporcionará un sistema de recomendación de videojuegos para la plataforma.

### Datos:

El proyecto se basa en tres archivos de tipo JSON GZIP:

+ **output_steam_games.json**: Contiene información detallada sobre los juegos, incluyendo nombre, editor, desarrollador, precios y etiquetas.

+ **australian_users_items.json**: Proporciona información sobre los juegos utilizados por los usuarios y la cantidad de tiempo que cada usuario ha dedicado a cada juego.

+ **australian_users_reviews.json**: Contiene los comentarios de los usuarios sobre los juegos, así como sus recomendaciones y otros datos relevantes como URL y user_id.