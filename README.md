# Clasificación de géneros musicales
Por Jordan Alessandro Villamil

Link del video: https://drive.google.com/file/d/1uNPuWtOsV5asGOs6tfX3vBLmxRMrqQgV/view?usp=sharing

Introducción:
El presente proyecto fue realizado a partir del dataset obtenido en Kaggle (https://www.kaggle.com/datasets/purumalgi/music-genre-classification), el cual cuenta con 17996 muestras, con 16 características distintas. Adicionalmente, trae 11 clases distintas para los géneros de Folk, Alt, Blues, Bollywood, Country, Hip Hop, Indie, Instrumental, Metal, Pop y Rock respectivamente. Sin embargo, cabe aclarar que las clases en el conjunto de entrenamiento no se encuentran balanceadas, dado que la mayoría de las muestras pertenecen a la clase de Rock.

Desarrollo:
Para el desarrollo del proyecto, lo primero que se hizo fue la limpieza del dataset, que consistió inicialmente en eliminar las características no necesarias. En primer lugar, se retiran las características del nombre de artista y nombre de pista, pues no aportan información al datsaset. Por otro lado, las únicas características que se utilizaron para clasificar son las de danceability, energy, speechiness, acousticness, instrumentalness y valence. Estas se escogieron dado que son características extraídas a partir de otras características incluidas en el dataset, por ejemplo, el valor del danceability se calcula a partir de distintos elementos como el tempo o la marca de tiempo, con lo cual se pueden omitir estas otras características y únicamente dejar las que se extraen a partir de ellas. Adicionalmente, se excluyeron características que se sabe que no tienen mucha correlación con algún género como lo es liveness (Que identifica si una grabación es en vivo) o la popularidad de la canción. Habiendo dejado únicamente las características mencionadas, se procedió a remover todas las muestras con nulos en alguna de las características que se mantuvieron, reduciendo notablemente el número de muestras a 13619. Con esto, se crearon las variables de X, que alberga todas las características mencionadas, y Y con las clases.
Posteriormente, se dividó el conjunto de datos en 80% para entrenamiento de 20% para validación, y apartir de ello se normalizó el dataset resultante con el StandardScaler de Sklearn. Posteriormente, se realizó la descomposición de componentes por medio de PCA para evaluar la viabilidad de la reducción dimensional. Para ello se realizó la reducción hasta una sola dimensión, y se halló la varianza explicada de cada reducción, llegando a la conclusión de que no es adecuado hacerla dado que en el mejor de los casos se mantiene menos del 97% de la información.
Finalmente, para generar los modelos de clasificación se escogieron dos métodos distintos: Random Forest por su utilidad para datasets desbalanceados y Logistic regression por su simplicidad. Para poder optimizar los hiperparametros de estos, se realizó el procedimiendo de GridSearch, variando el número de estimadores y el criterio para Random Forest, y el coeficiente de regularización y el tipo de penalidad para la regresión logística. Con ello se hallaron los mejores conjuntos de hiperparametros para ambos métodos.
Habiendo hallado los mejores hiperparametros, se procedió a generar los dos respectivos módelos con dichos hiperparametros y entrenarlos con el conjunto de entrenamiento entero, para posteriormente hallar el MCC, F1 y AUC-ROC de cada uno mediante el conjunto de validación.

Resultados:
A continuación se presenta una tabla con los puntajes calculados para los dos métodos optimizados e implementados:

![imagen](https://user-images.githubusercontent.com/69338741/171969450-b5dd780e-f8ae-4ecf-bb40-b13a35a01188.png)

Como se evidencia, los puntajes son bastante similares para ambos métodos, con la regresión logística teniendo mayor puntaje de MCC y AUC-ROC, pero un F1 menor que el random forest. 

Conclusiones:
Finalmente, con el proyecto realizado es posible evidenciar las dificultades para la clasificación del género musical de una pista, pues los puntajes obtenidos son bastante bajos. Sin embargo, vale la pena hacer al mismo procedimiento con un dataset mucho más balanceado y comprobar nuevamente la capacidad de clasificación de los métodos entrenados. De igual manera, es importante destacar que muchas veces las diferencias entre géneros musicales no solo no son específicas sino tampoco son cuantizables, por lo cual el desarrollo de algoritmos para su clasificación es una tarea difícil que podría requerir de otros métodos o algoritmos de mayor complejidad, al igual que extraer características más significativas con los géneros musicales a clasificar. Quizás la mayor aplicación de estos algoritmos vendría siendo en los servicios de streaming de música como Spotify, para los cuales es importante encontrar características en las canciones y así generar playlists y recomendaciones que mejoren la experiencia de los usuarios, y por medio de este proyecto fue posible no solo entender las bases de dichos procedimientos, sino también sus complejidades y limitaciones.



