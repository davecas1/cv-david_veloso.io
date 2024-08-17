Análisis de Imágenes con PCA
================
<div align="justify">
    Saludos.
    <br>
    
    Este proyecto, trata de hacer un análisis clásico de imágenes. El análisis de imágenes se empezó a estudiar a principios de 1970 y finales de 1960. Lo que se buscaba era obtener información para a partir de las imágenes porder segmentar y clasificar. En estos años,
    debido a que las imágenes a color eran muy caras, se desarrolló muchas técnicas para imágenes en blanco y negro. Por lo tanto, la textura tiene un gran peso, y por eso también se le llama análisis textural. <br>
    En general este campo es muy importante para el campo médico.
    <br>
    <br>
    En este caso, lo que se hará es analizar la imagen de un pez. Para observar si se puede extraer información estructural, en concreto, usaremos el Enfoque Prats-Ferrer, también llamado Enfoque Bharati-MacGregor para los tres canales de color. Este enfoque trata la
    imagen RGB como un cubo, el cual parte de la textura de la imagen está relacionada con la frecuencia espacial, y se aplica el mismo procedimiento a los tres canales de color. 
    <br>
    <br>
    Se debe tener en cuenta que se aplica a los tres canales de color, ya que cada canal de color nos aportará información textural.
<br>
<br>
<img src="https://github.com/davecas1/davecas1.github.io/blob/master/pro_1_img/Amnou_u0%20(1).jpg" alt="Descripción de la imagen" width="500">
<br>
<br>
Se aprecia en la imagen del pez, que tiene algunos tonos rojizos y otras zonas muy marcadas de azul claro y de color negro. Se aprecia que el pez no está en el fondo de la imagen y que de fondo se encuentra la cola de un pez de la especie.

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
</div>

![](z_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->![](z_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->
