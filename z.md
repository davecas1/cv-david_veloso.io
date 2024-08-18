Análisis de Imágenes con PCA
================
<div align="justify">
    <p>Saludos en este artículo se detallará el proyecto que realicé sobre Análisis de Imágenes usando PCA. Con dos ejemplos, el primero es sobre un pez y la segunda sobre una palabra escrita en un folio.
    </p>
    <p>
        El caso de la palabra en el folio, hay varios casos. El primero, es la palabra original "HOLA" que se usará como el ideal, luego el mismo folio escaneado a diferente resolución. Y luego habiendo tachado la palabra "HOLA" con un lápiz.
    </p>
    
    <p>
    Este proyecto trata de hacer un análisis clásico de imágenes. El análisis de imágenes comenzó a estudiarse a principios de la década de 1970 y finales de la de 1960. Lo que se buscaba era obtener información a partir de las imágenes para poder segmentar y clasificar. En esos años, debido a que las imágenes a color eran muy costosas, se desarrollaron muchas técnicas para imágenes en blanco y negro. Por lo tanto, la textura tiene un gran peso, y por eso también se le llama análisis textural.
    </p>

    <p>
    En general, este campo es muy importante para la medicina.
    </p>

    <p>
    En este caso, lo que se hará es analizar la imagen de un pez para observar si se puede extraer información estructural. En concreto, usaremos el Enfoque Prats-Ferrer, también llamado Enfoque Bharati-MacGregor, para los tres canales de color. Este enfoque trata la imagen RGB como un cubo, donde parte de la textura de la imagen está relacionada con la frecuencia espacial, y se aplica el mismo procedimiento a los tres canales de color.
    </p>

    <p>
    Se debe tener en cuenta que se aplica a los tres canales de color, ya que cada canal de color nos aportará información textural.
    </p>
<img src="https://raw.githubusercontent.com/davecas1/davecas1.github.io/master/pro_1_img/Amnou_u0%20(1).jpg" alt="Descripción de la imagen" width="500">
    <p>
    Se aprecia en la imagen del pez que tiene algunos tonos rojizos y otras zonas muy marcadas de azul claro y de color negro. Además, se observa que el pez no está en el fondo de la imagen y que de fondo se encuentra la cola de un pez de la misma especie.
    </p>
    <p>
    Se procede a realizar una PCA (Principal Component Analysis). Para realizar la PCA, se ha separado la imagen por cada canal de color, y se usan "ventanas". En este caso, debido a limitaciones computacionales se ha usado una ventana 3x3, ya que una ventana más pequeña requiere más tiempo de computación. Por lo tanto, para cada píxel se ha obtenido 9 valores, es decir que en total habrá 9+9+9 es decir que se obtendrán 27 componentes.
    </p>
</div>
    ## Importance of components:
    ##                           PC1     PC2     PC3     PC4     PC5    PC6     PC7
    ## Standard deviation     5.0180 0.82796 0.63035 0.59101 0.32159 0.2894 0.22965
    ## Proportion of Variance 0.9326 0.02539 0.01472 0.01294 0.00383 0.0031 0.00195
    ## Cumulative Proportion  0.9326 0.95798 0.97270 0.98564 0.98947 0.9926 0.99452
    ##                            PC8     PC9    PC10    PC11   PC12    PC13    PC14
    ## Standard deviation     0.19991 0.16099 0.14766 0.12388 0.1165 0.08004 0.07389
    ## Proportion of Variance 0.00148 0.00096 0.00081 0.00057 0.0005 0.00024 0.00020
    ## Cumulative Proportion  0.99600 0.99696 0.99777 0.99834 0.9988 0.99908 0.99928
    ##                           PC15    PC16    PC17    PC18    PC19    PC20    PC21
    ## Standard deviation     0.06284 0.05899 0.05663 0.05358 0.03570 0.03545 0.03336
    ## Proportion of Variance 0.00015 0.00013 0.00012 0.00011 0.00005 0.00005 0.00004
    ## Cumulative Proportion  0.99943 0.99956 0.99967 0.99978 0.99983 0.99987 0.99992
    ##                           PC22    PC23    PC24    PC25    PC26    PC27
    ## Standard deviation     0.02567 0.02551 0.01816 0.01802 0.01395 0.01125
    ## Proportion of Variance 0.00002 0.00002 0.00001 0.00001 0.00001 0.00000
    ## Cumulative Proportion  0.99994 0.99996 0.99998 0.99999 1.00000 1.00000
<div align="justify">
    Una vez realizado la PCA, como se aprecia en la tabla superior. Se ha obtenido las 27 componentes que sumán una proporción acumulada de 1. Es decir, que estas 27 explican el total de la varianza. En este caso, sólo se utilizará 5. Ya que sacar más componentes no implica que haya más información. Ya que en algunos casos puede ser ruido o simplemente información que no es útil. Cogiendo 5 componentes explicamos el 0,98947 de la varianza.
    <img src="https://raw.githubusercontent.com/davecas1/davecas1.github.io/master/pro_1_img/1LOADING.png" >
    <br><br>
    <img src="https://raw.githubusercontent.com/davecas1/davecas1.github.io/master/pro_1_img/2SCOREIMAGEN.png" >
    <br><br>
A partir de los loadings, se puede explicar. Hay que tener claro que es RGB (Rojo, Verde y Ázul) esto quiere decir, que los nueve primeros son del canal de color rojo. Los nueve siguientes del verde y los 9 últimos son los relativos al ázul. Y a partir de las score imágenes y de los loadings podemos observar características. La primera score imagen corresponde con el primer loading, el segundo con el segundo y así sucesivamente.
<br>
<br>
El primer loading y la primera score imagen, se aprecia que todos los caneles tienen prácticamente los mismos valores. Esto quiere decir, que es una media, que es prácticamente igual a la imagen original pero en blanco y negro. Al usarse ventanas de 3x3 se aprecia que el borde se ha perdido.
<br>
<br>
El segundo loading plot, se aprecia valores elevados de rojo. De verde prácticamente no hay nada, y de ázul vemos valores negativos. Esto se interpreta que en las zonas donde hay rojo hay menos ázul. Y se aprecia en la segunda score imagen, que las zonas más claras de la imagen, es donde en la imagen original hay más color rojo. Mientrás que las zonas oscuras son zonas donde hay presencia de color más ázul pero menos rojo.
<br>
<br>
En el tercer loading plot y en el cuarto, se aprecia que hay una estructura o patrón que se repite. En el caso del tercer loading plot. Se aprecia que los primeros valores de cada canal de color es negativo y de forma progresiva se hace cada vez más positivo. Y lo mismo ocurre en el cuarto loading plot. Hay valores positivos y se observa un decrecimiento. Si atendemos a las score imágenes, se aprecia una cierta rugosidad. Luego se explicará con más detalle.
<br>
<br>
El quinto loading plot, se aprecia valores altos de color verde, y menos de color rojo y ázul. Y atendiendo a la score imagen, está marcando aquellas zonas más verdosas del pez.
<br>
<br>
    <img src="https://raw.githubusercontent.com/davecas1/davecas1.github.io/master/pro_1_img/direccion.png" >
<br>
<br>
Se había comentado antes que era la rugosidad, sin embargo, lo que se aprecia es una dirección donde va cada color. Es decir, que estos loading plots, son sobre la textura de la propia imagen y no sobre la composición del color de los píxeles. Se aprecia, que la tres va de valores positivos a negativos. Lo que esto representado es como se observa en la imagen superior. Se aprecia que hay una dirección que va de la esquina superior derecha a la inferior izquierda (la flecha ázul marca el sentido de la dirección). Y se aprecia en la score imagen es la parte de las aletas y algunas escamas del pez tienen la misma.
<br>
En el cuarto, sucede lo mismo, pero en otro sentido está vez de la esquina inferior derecha a la superior izquierda, y se aprecia en la score imagen que el contorno del pez está mejor definido y se aprecia como se marcan la zona de las escamas.
<br>
<br>
Es decir, de este análisis, hemos obtenido que la componente 2 y 5 explican el color del pez y la 3 y la 4 hablan sobre la textura del pez. A partir, de este conocimiento, se podría hacer por ejemplo utilizar estos componentes para detectar errores. En el caso de los peces no tendría mucho sentido, se podría utilizar por ejemplo para detectar si el pez capturado tiene alguna anomalía. También se puede aplicar este mismo análisis a fruta y con ello detectar si ha recibido picaduras de moscas. Para esto, se haría de la misma manera, pero intentando averiguar cual componente principa explica mejor las picaduras de la mosca.
<br>
Se puede usar para la detección de errores. También se puede usar para comprimir la información de la imagen. Tiene muchas aplicaciones este análisis.
<br>
<br>
<p>
    En la segunda parte, se hará sobre el folio. En este caso, lo que se aprecia en las imágenes superiores son las 4 imágenes. Las dos primeras imágenes corresponden a la palabra "HOLA" sin estar tachado, pero a diferente resolución. La primera tiene la máxima que es 1200x1200, mientras que la segunda está a 150x150. Y lo mismo ocurre con la palabra tachada, está a dos resoluciones. Se tomará como ideal la palabra "HOLA" a mayor resolución. Y lo que se quiere comprobar, es primero, si la resolución del escaneado dificulta la detección. Es decir, si la imagen que uso para detectar que algo es correcto o no es influido por la propia calidad de la resolución. Y el segundo caso, es si la palabra está tachada, ¿se podría identificar cuáles partes han sido añadidas después?.
</p>
<p>
    Para hacer todo esto, primero se realizará el análisis que se ha hecho antes y se usará dos conceptos. La suma de cuadrados residual (SCR o RSS) y la T^2 de Hotelling. Seguimos el mismo enfoque. El de Prats-Ferrer o Bharati-MacGregor para los tres canales de color.
</p>
<p>
    La T^2 de Hotelling, en el caso de la Monitorización y Control Estadístico de Procesos Multivariantes (MSPC), nos ayuda a detectar aquellos valores que se pueden catalogar como observaciones extremas, pero siguen manteniendo la estructura de correlación. En términos más estadísticos, sería aquellos valores que están alejados del centroide pero que siguen manteniendo la misma estructura de correlación. Mientrás que la suma de cuadrados residual, detecta las observaciones anómalas, siendo estás las que rompen la estructura de correlación. O lo que es lo mismo, si no rompen la estructura de correlación es que están dentro del modelo y si lo rompen significa que están fuera del modelo
</p>
<p>
    El procedimiento, para realizarlo es el siguiente. Primero hay que decidir cuál es nuestro modelo "bajo control", en este caso "HOLA" a máxima resolución. Posteriormente, se guarda los valores medios y las desviaciones típicas de la imagen bajo control. Y luego se hace la proyección de las imágenes que no sabemos si contienen error. Y se normaliza utilizando los valores guardados de la imagen "bajo control". Y por último se decide un límite para la Suma de cuadrados residual y para la T2 de Hotelling, que en este caso será el 95% y se procede a calcular los dos estadísticos.
</p>
</div>
