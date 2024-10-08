<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evaluación breve entre distintos modelos de Minería de Datos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            text-align: center;
        }

        p, h1, table {
            text-align: justify;
            margin: auto;
            width: 80%;
        }

        table {
            border-collapse: collapse;
            margin-top: 20px;
        }

        table, th, td {
            border: 1px solid black;
            padding: 8px;
        }

        caption {
            font-weight: bold;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <h1>Evaluación breve entre distintos modelos de Minería de Datos</h1>

    <p>Saludos en este artículo se detallará un proyecto que he hecho utilizando modelos de minería de datos.</p>

    <p>Antes de explicar los modelos, quería explicar que en Minería de Datos, en general se dividen los modelos en dos grandes campos: "no supervisados" y "supervisados". A grandes rasgos, en el aprendizaje no supervisado el objetivo, a priori, no se conoce, es decir, que la información que tenemos no está previamente clasificada. Mientras que en el aprendizaje supervisado, sí se conoce el objetivo buscado, y la información está previamente clasificada.</p>

    <p>Algunos de los modelos usados en aprendizaje no supervisado son "PCA" y "CFA". En supervisados, es donde encontramos Random Forest. Dentro del aprendizaje supervisado, hay dos grandes tipos de problemas: los problemas de discriminación/clasificación y los problemas de predicción.</p>

    <p>En este apartado haremos uso de modelos de clasificación, ya que los datos son sobre diabetes, y lo que se busca es poder clasificar a los individuos a partir de las variables que tenemos. Por lo tanto, es un ejemplo clásico de clasificación. Se van a usar 4 modelos distintos y se estudiará cuál es el que proporciona mejores resultados.</p>

    <p>Los modelos son: Random Forest, KNN (Vecinos más próximos), Naive Bayes y SVM (Support Vector Machine). Para analizarlo, se ha hecho un Hold-out repetido 100 veces. El 75% de los datos serán de entrenamiento y el 25% de validación. Esto se hace así para evaluar de mejor manera cómo funcionan los distintos modelos. Por ejemplo, Random Forest tiende al sobreajuste. Existen otras técnicas de partición y evaluación de datos, como el Hold-out estratificado (donde las clases mantienen la misma proporción) o la validación cruzada (donde los datos se dividen en <i>k</i> subconjuntos). En este artículo se hará uso del Hold-out repetido.</p>

    <table>
        <caption>Tasa de aciertos por modelo</caption>
        <thead>
            <tr>
                <th>percentil</th>
                <th>tasa.aciertos.rf</th>
                <th>tasa.aciertos.svm</th>
                <th>tasa.aciertos.knn</th>
                <th>tasa.aciertos.nbayes</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>2.5%</td>
                <td>0.7028646</td>
                <td>0.6847656</td>
                <td>0.6507813</td>
                <td>0.6979167</td>
            </tr>
            <tr>
                <td>97.5%</td>
                <td>0.8125000</td>
                <td>0.8048177</td>
                <td>0.7686198</td>
                <td>0.8152344</td>
            </tr>
        </tbody>
    </table>

    <table>
        <caption>Promedio de tasa de aciertos</caption>
        <thead>
            <tr>
                <th>promedio</th>
                <th>tasa.aciertos.rf</th>
                <th>tasa.aciertos.svm</th>
                <th>tasa.aciertos.knn</th>
                <th>tasa.aciertos.nbayes</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td></td>
                <td>0.7626042</td>
                <td>0.7443750</td>
                <td>0.7140625</td>
                <td>0.7543229</td>
            </tr>
        </tbody>
    </table>

    <p>De las tablas anteriores, se aprecia que Naive Bayes proporciona el mejor valor de tasa de acierto, con un 0.815; sin embargo, el menor resultado ha sido de 0.698, mientras que Random Forest ha obtenido como peor resultado en el percentil 2.5% un 0.703 de tasa de acierto y como mejor un 0.812. Esto mismo se obtiene calculando las medias: de promedio, parece que Random Forest es el mejor modelo, y el peor con diferencia respecto a los otros modelos es el KNN (Vecino más próximo).</p>

    <p>Ahora se realizará un ANOVA, ya que lo que se quiere ver es si la diferencia entre los modelos es significativa, es decir, si realmente las diferencias son lo suficientemente grandes como para ser distintas o si todos los modelos estadísticamente ofrecen los mismos resultados.</p>

    <table>
        <caption>Resultados del ANOVA</caption>
        <thead>
            <tr>
                <th>Df</th>
  
