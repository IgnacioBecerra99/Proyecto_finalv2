# Clasificación de rango en partidas competitivas de League of Legends

## Definición del problema

El problema plantedo será uno de **clasificación**, específicamente sobre los rangos que uno puede obtener en base a el rendimiento durante partidas clasificatorias del popular juego de categoría Multiplayer Online Battle Arena o MOBA como lo es **League of Legends** o **LoL**. Este problema tiene especial relevancia para mí debido a que soy un jugador de LoL de hace ya varios años y me gustaría poder realizar un trabajo final basado en uno de mis hobbies que llevo practicando durante mucho timepo.

## Plan de acción

El dataset se llama League of Legends Ranked Match Data Season 15 (EUN) y se puede encontrar [aquí](https://www.kaggle.com/datasets/jakubkrasuski/league-of-legends-ranked-match-data-season-15) , posee 68300 filas y 69 columnas además de poseer variables vacías o nulas en ciertas categorías que serán reemplazadas por un valor ya que son significativas al momento de estudiar el dataset. Dentro de las características que encuentro son más importantes para el análisis serían las de solo_tier, solo_rank, flex_tier, flex_rank, champion_id/champion_name, kills, deaths, assists o kda_ratio, gold_per_min, damage_per_min, vision_score y junto con todo esto se podria conocer el rendimiento del jugador durante la partida y los campeones utilizados para cada rol y así clasificar de mejor manera el rango al que se pertenece, pero la característica target si nos queremos centrar en un solo tipo de partida clasificatoria sería la de solo_tier. El modelo a utilizar es el de Random Forest. Y para la estrategia de evaluación se separará en entrenamiento y prueba y se utilizaran las métricas de un reporte de clasificación y una matriz de confusión para evaluar el desempeño del modelo.

## Justificación del modelo

Una de las razones principales para escoger el método de Random Forest ya que al utilizar un bagging de desicion tree es bastante versátil y robusto, además de ser ideal cuando se cuenta con un gran número de características con interacciones complejas entre ellas, además su capacidad para proporcionar estimaciones de la importancia de las características lo hace valioso para problemas de selección de características y comprensión de datos.

- Ventajas:
    - Capacidad para manejar datasets con muchas variables.
    - Reducción del riesgo de sobreajuste mediante el uso de múltiples árboles.
    - Posibilidad de identificar la importancia relativa de las variables predictoras.
- Limitaciones:
    - Menor interpretabilidad en comparación con un Desicion Tree.
- Pertinencia:
    - Este problema es de clasificación multiclase y el Random Forest está bien adaptado para esta clase de problemas.
    - La gran cantidad de variables disponibles favorece un modelo que pueda capturar relaciones no lineales y múltiples interacciones.

## Metodología aplicada

- Se leyó el dataset y se hizo una exploración rápida de los datos.
- Se contaron las características que tenían valores vacíos y luego estos se rellenaron con el valor de UNRANKED ya que el que estuvieran vacíos nos indicaba que no habían realizado sus partidas de posicionamiento lo cual nos entrega información y no era buena idea simplemente eliminarlos.
- Le di un orden a los rangos disponibles.
- Los grafiqué con un countplot y además los conté tanto las clasificatorias en solitario como flexible.
- Junté en un diccionario los ID de los campeones junto con sus nombres.
- Eliminé las características que no eran necesarias como tiempo de juego, tipo de id, el mapa utilizado, etc. Además de las que a mi parecer no iban a influenciar o proporcionarían buena información como por ejemplo los objetos comprados, las estadisticas finales, los puntos de maestría necesarios para subir el nivel de maestría, etc. Finalmente eliminé las características relacionadas con las partidas de clasificatoria flexible para centrarme en las clasificatorias en solitario ya que estas son las que más jugadores clasificados tiene, y también eliminé la característica de los puntos lp que se poseían ya que esta es una forma de clasificación.
- Eliminé los valores de personas en el rango de IRON ya que eran muy pocas.
- Usé la función de LabelEncoder para darle valores a las posiciones dentro de una partida.
- Definí los valores de X e y.
- Creé una variable con la función RandomUnderSampler con la estrategia de "majority"
- Apliqué esta función a mis valores X e y para balancear los datos. Siendo este el motivo por el que eliminé el rango IRON para poder tener más datos luego de aplcar el RandomUnderSampler con minority.
- Separé los datos para entrenarlos en X_train, X_test, y_train, y_test.
- Realicé un histograma para ver como iban las cosas.
- Apliqué el modelo RandomForestClassifier sin parámetros y le pedí imprimir la matriz de confusión y un classification report.
- Luego creé una variable para el RandomForestClassifier, otra con las variables para el grid y después use la función de GrisSearchCV con las dos variables anteriores, con un cv de 3, un scoring de f1 macro y un verbose de 3, luego le hie un fit y terminé con un print de los mejores hiperparametros y el mejor score.
- Y finalmente grafiqué las importancias de las características.

## Resultados obtenidos

Dentro de los resultados obtenidos tenemos que los mejores hiperparametros para el random forest son:
- 'max_depth': 10, 'max_features': 20, 'min_samples_leaf': 2, 'n_estimators': 100

Y que el mejor f1_score que se puede obtener es de: 0.21789439139471253
También tenemos que las 2 características más importantes al momento de clasificar son solo_wins y solo_losses. Y las 2 peores serían team_baronKills y team_riftHeraldKills.

## Conclusiones

Con estos datos podemos concluir que el modelo no está clasificando de la mejor manera posible y que posee un amplio rango de mejora, también que el modelo necesita una profundidad bastante grande. Y finalmente que las mejores características para clasificar tienen sentido en su mayoría, ya que si bien dentro del juego la cantidad de victorias y derrotas influye de gran manera en la cantidad de puntos lp obtenidos o perdidos también se toma en cuenta el desempeño dentro de la partida para calcular estos puntos.  
