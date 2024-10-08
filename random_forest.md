# Evaluación breve entre distintos modelos de Minería de Datos

Saludos en este artículo se detallará un proyecto que he hecho utilizando modelos de minería de datos.

Antes de explicar los modelos, quería explicar que en Minería de Datos, en general se dividen los modelos en dos grandes campos: "no supervisados" y "supervisados". A grandes rasgos, en el aprendizaje no supervisado el objetivo, a priori, no se conoce, es decir, que la información que tenemos no está previamente clasificada. Mientras que en el aprendizaje supervisado, sí se conoce el objetivo buscado, y la información está previamente clasificada.

Algunos de los modelos usados en aprendizaje no supervisado son "PCA" y "CFA". En supervisados, es donde encontramos Random Forest. Dentro del aprendizaje supervisado, hay dos grandes tipos de problemas: los problemas de discriminación/clasificación y los problemas de predicción.

En este apartado haremos uso de modelos de clasificación, ya que los datos son sobre diabetes, y lo que se busca es poder clasificar a los individuos a partir de las variables que tenemos. Por lo tanto, es un ejemplo clásico de clasificación. Se van a usar 4 modelos distintos y se estudiará cuál es el que proporciona mejores resultados.

Los modelos son: Random Forest, KNN (Vecinos más próximos), Naive Bayes y SVM (Support Vector Machine). Para analizarlo, se ha hecho un Hold-out repetido 100 veces. El 75% de los datos serán de entrenamiento y el 25% de validación. Esto se hace así para evaluar de mejor manera cómo funcionan los distintos modelos. Por ejemplo, Random Forest tiende al sobreajuste. Existen otras técnicas de partición y evaluación de datos, como el Hold-out estratificado (donde las clases mantienen la misma proporción) o la validación cruzada (donde los datos se dividen en *k* subconjuntos). En este artículo se hará uso del Hold-out repetido.

| percentil | tasa.aciertos.rf | tasa.aciertos.svm | tasa.aciertos.knn | tasa.aciertos.nbayes |
|-----------|------------------|-------------------|-------------------|----------------------|
| 2.5%      | 0.7028646         | 0.6847656         | 0.6507813         | 0.6979167            |
| 97.5%     | 0.8125000         | 0.8048177         | 0.7686198         | 0.8152344            |

| promedio  | tasa.aciertos.rf  | tasa.aciertos.svm  | tasa.aciertos.knn  | tasa.aciertos.nbayes |
|-----------|-------------------|-------------------|--------------------|----------------------|
|           | 0.7626042          | 0.7443750         | 0.7140625          | 0.7543229            |

De las tablas anteriores, se aprecia que Naive Bayes proporciona el mejor valor de tasa de acierto, con un 0.815; sin embargo, el menor resultado ha sido de 0.698, mientras que Random Forest ha obtenido como peor resultado en el percentil 2.5% un 0.703 de tasa de acierto y como mejor un 0.812. Esto mismo se obtiene calculando las medias: de promedio, parece que Random Forest es el mejor modelo, y el peor con diferencia respecto a los otros modelos es el KNN (Vecino más próximo).

Ahora se realizará un ANOVA, ya que lo que se quiere ver es si la diferencia entre los modelos es significativa, es decir, si realmente las diferencias son lo suficientemente grandes como para ser distintas o si todos los modelos estadísticamente ofrecen los mismos resultados.

| Df       | Sum Sq | Mean Sq | F value | Pr(>F)    |
|----------|--------|---------|---------|-----------|
| método   | 3      | 0.1349  | 0.04497 | 115.136   | <2e-16 *** |
| bloque   | 99     | 0.2346  | 0.00237 | 6.068     | <2e-16 *** |
| residual | 297    | 0.1160  | 0.00039 |           |           |

Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

De la tabla ANOVA, se aprecia que tanto el método como el bloque son significativos. El método representa los modelos, lo que implica que sí hay diferencias entre ellos. Además, observando el *Mean Sq*, podemos ver cómo el método tiene 0.04497 y el bloque 0.00237. Ambos valores son superiores al residual. Que el bloque sea significativo implica que las diferentes particiones que se han hecho en el Hold-out repetido son distintas y que esas diferencias son significativas, lo cual era esperable.

La gráfica superior es un intervalo LSD con el método de Bonferroni. El intervalo LSD crea intervalos de confianza para cada nivel; por lo tanto, si dos niveles se solapan, significa que son parecidos (es decir, que un trozo de los dos intervalos estará en la misma zona, lo que implica que no existen diferencias estadísticamente significativas). En este caso, debido a la representación que hace R, se enumeran con letras y colores. Si dos modelos son iguales, se les asigna la misma letra y el mismo color. Lo que se aprecia es que ninguno es estadísticamente igual a otro. Y, se observa que el primero, Random Forest, es el mejor modelo.

Esto quiere decir que Random Forest, en este caso, es el mejor modelo, ya que proporciona los mejores valores promedio de tasa de aciertos. Como hemos explicado, al realizar el experimento con los datos, se ha obtenido que los modelos son estadísticamente significativos. Si no lo fuesen, significaría que todos los modelos planteados darían estadísticamente los mismos resultados y, por lo tanto, daría igual qué modelo seleccionásemos.

Igualmente, cabe mencionar que aquí solo se ha pretendido explicar brevemente las herramientas de Minería de Datos y ejemplificarlas. También se pueden utilizar otras medidas como la curva ROC. En este caso, al ser un modelo de clasificación, se podría usar, así como otras métricas, dependiendo de la problemática. Por ello, la minería de datos no se presenta como un fin en sí mismo, sino como una herramienta que se puede usar en muchos campos. Y en mi humilde opinión, debemos tener siempre presentes las palabras de Box: "todos los modelos son falsos, pero algunos son útiles", y lo que buscamos es esa utilidad.
