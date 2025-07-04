# Clasificación de rango en partidas competitivas de League of Legends

## Definición del problema

El problema plantedo será uno de **clasificación**, específicamente sobre los rangos que uno puede obtener en base a el rendimiento durante partidas clasificatorias del popular juego de categoría Multiplayer Online Battle Arena o MOBA como lo es **League of Legends** o **LoL**. Este problema tiene especial relevancia para mí debido a que soy un jugador de LoL de hace ya varios años y me gustaría poder realizar un trabajo final basado en uno de mis hobbies que llevo practicando durante mucho timepo.
## Plan de acción

El dataset se llama League of Legends Ranked Match Data Season 15 (EUN) y se puede encontrar [aquí](https://www.kaggle.com/datasets/jakubkrasuski/league-of-legends-ranked-match-data-season-15) , posee 68300 filas y 69 columnas además de poseer variables vacías o nulas en ciertas categorías que serán reemplazadas por un valor ya que son significativas al momento de estudiar el dataset. El modelo a utilizar es el de Random Forest. Y para la estrategia de evaluación se separará en entrenamiento y prueba y se utilizaran las métricas de un reporte de clasificación y una matriz de confusión para evaluar el desempeño del modelo.

## Justificación del modelo

Una de las razones principales para escoger el método de Random Forest ya que al utilizar un bagging de desicion tree es bbastante versátil y robusto, además de ser ideal cuando se cuenta con un gran número de características con interacciones complejas entre ellas, además su capacidad para proporcionar estimaciones de la importancia de las características lo hace valioso para problemas de selección de características y comprensión de datos.

- Ventajas:
    - Capacidad para manejar datasets con muchas variables.
    - Reducción del riesgo de sobreajuste mediante el uso de múltiples árboles.
    - Posibilidad de identificar la importancia relativa de las variables predictoras.
- Limitaciones:
    - Menor interpretabilidad en comparación con un Desicion Tree.
- Pertinencia:
    - Este problema es de clasificación multiclase y el Random Forest está bien adaptado para esta clase de problemas.
    - La gran cantidad de variables disponibles favorece un modelo que pueda capturar relaciones no lineales y múltiples interacciones.



