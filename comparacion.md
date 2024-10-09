Análisis de Imágenes con PCA
================
<div align="justify">
    <p>Saludos en este artículo se detallará la realización de un diseño sencillo de experimentos para evaluar cuál de los siguientes modelos proporciona mejores resultados.
    </p>   
    <p>
  Antes de explicar los modelos, quería explicar que en Minería de Datos, en general se dividen los modelos en dos grandes campos uno son los "no supervisados" y los "supervisados". A grandes rasgos, el aprendizaje no supervisado el objetivo, a priori, no se conoce es decir, que la información que tenemos no está previamente clasificada. Mientrás que el aprendizaje supervisado, si se conoce el objetivo buscado, y la información está previamente clasificada.
    </p>

    <p>
     Algunos de los modelos usados en aprendizaje no supervisado es "PCA" y "CFA". Y en supervisados es donde se encuentra el Random Forest. Dentro del aprenizaje supervisado, hay dos grandes tipos de problemas, los problemas de discriminación/clasificación y el problema de la predicción. 
    </p>

    <p>
    En este apartado haremos uso de modelos de clasificación, ya que los datos son sobre la diabetes, y lo que se busca es poder clasificar a los individuos a partir de las variables que tenemos. Por lo tanto, es un ejemplo clásico de clasificación. Se van a usar 4 modelos distintos y se estudiará cuál es el que proporciona mejores resultados. 
    </p>

    <p>
    Los modelos son: Random Forest, KNN (Vecinos más próximo), Naive Bayes y SVM (Support Vector Machine). Para analizarlo se ha hecho un Hold-out repetido 100 veces. 75% serán los datos de entrenamiento y el 25% de validación. Esto se hace así para poder evaluar de mejor manera como funciona los distintos modelos. Ya que por ejemplo, Random Forest, tiende al sobreajuste. Existen otras técnicas de partición de datos y de evaluación de datos, como por ejemplo, Hold-Out estratificado, el cuál las clases mantienen la misma proporción o validación cruzada que los datos se dividen en k subconjuntos. En este artículo se hará uso del Hold-Out repetido. 
    </p>
</div>
    ##          tasa.aciertos.rf tasa.aciertos.svm tasa.aciertos.knn  tasa.aciertos.nbayes
    ## 2.5%         0.7028646         0.6847656         0.6507813            0.6979167
    ## 97.5%        0.8125000         0.8048177         0.7686198            0.8152344

     ##   tasa.aciertos.rf    tasa.aciertos.svm    tasa.aciertos.knn tasa.aciertos.nbayes 
     ##      0.7626042            0.7443750            0.7140625            0.7543229 

<div align="justify">
    <p>
    De las dos tablas superiores, se aprecia que Naive Bayes proporciona el mejor valor de tasa de acierto, con un 0,815 sin embargo, el menor resultado ha sido de 0,698 mientras que Random Forest ha obtenido como peor resultado en un 2,5% un 0,703 de tasa de acierto y como mejor un 0,812. Es lo mismo que se obtiene haciendo las medias. Que de promedio, parece que Random Forest es el mejor modelo, y el peor con diferencia respecto a los otros modelos es el KNN (Vecino más próximo). 
    </p>

<div align="justify">
    Ahora se realizará un ANOVA, ya que lo que se quiere ver es, si la diferencia entre los modelos es significativa, es decir, si realmente las diferencias son lo suficientemente grandes como para ser distintos o si todos los modelos estadísticamente dan los mismos resultados. 
</div>

    ##             Df Sum Sq Mean Sq F value Pr(>F)    
    ## metodo        3 0.1349 0.04497 115.136 <2e-16 ***
    ## bloque       99 0.2346 0.00237   6.068 <2e-16 ***
    ## Residuals   297 0.1160 0.00039  

<img src="https://raw.githubusercontent.com/davecas1/davecas1.github.io/master/pro2_img/pressure-3.png" alt="SIGNIFICATIVIDAD DEL ANOVA" width="500">
<div align="justify">
    <br><br>
    De la tabla ANOVA, se aprecia que tanto el método como en bloque son significativos. El método, son los modelos, lo que implica que si hay diferencias entre los modelos. Y luego el bloque. Observando el Mean Sq, podemos ver como el método tiene 0,04497 y el bloque 0,00237. Y los dos son superiores al residual. Que el bloque sea significativo, implica que las diferentes particiones que se han hecho en Hold-Out repetido son distintos y que son significativamente distintas entre ellas. Es esperable este resultado.
    <br>
<br>
    La gráfica superior, es un intervalo LSD con el método de Bonferroni. El intervalo LSD, crea intervalos de confianza para cada nivel, por lo tanto, si dos niveles se solapan son parecidos un trozo de los dos intervalos estará en la misma zona, lo que implica que no existan diferencias estadísticamente significativas. En este caso, debido a la representación que hace R, enumera con letras y con colores. Si dos son iguales pondrá la misma letra y el mismo color. Lo que se aprecia es que ninguno es estadísticamente igual a otro. Y, se observa que el primero, el Random Forest, es el mejor modelo. 
    <br>
    <br>
    Esto lo que quiere decir, es que Random Forest, en este caso, es el mejor modelo, pues proporciona los mejores valores promedios de tasa de aciertos. Esto es debido a que como hemos explicado, al realizar el experimento con los datos se ha obtenido que los modelos son estadísticamente significativos. Si no lo fuesen, significaría que todos los modelos planteados darían estadísticamente los mismos resultados y por lo tanto, daría igual que modelo seleccionasemos. 
    <br>
    <br>
    Igualmente cabe mencionar, que aquí sólo se ha prentidido explicar brevemente las herramientas de Minería de datos y ponerlo en un ejemplo. También se puede utilizar otras medidas como la curva ROC, En este caso al ser un modelo de clasificación se podría usar, y se podría hacer uso de distintas métricas, pero eso ya depende de la problemática del problema interesa más usar una métrica u otra. Por ello, la minería de datos no se presenta como un fin en si mismo, sino una herramienta que se puede usar en muchos campos. Y en mi humilde opinión, debemos tener siempre presente las palabras de Box, que todos los modelos son falsos pero hay algunos útiles y lo que buscamos es esa utilidad.
</div>
