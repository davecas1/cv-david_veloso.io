Análisis de Imágenes con PCA
================

``` r
# Instalar las bibliotecas necesarias
# Biblioteca para análisis de PCA

# Cargar las bibliotecas
library(jpeg)
library(stats)

# Leer la imagen JPEG
imagen <- readJPEG(source = "Amnou_u0.jpg")

# Extraer los canales de color
rojo <- imagen[,,1]
verde <- imagen[,,2]
azul <- imagen[,,3]

# Procesamiento del canal rojo
n_filas <- nrow(rojo)
n_columnas <- ncol(rojo)
matriz_v_rojo <- matrix(0, nrow = (n_filas - 2) * (n_columnas - 2), ncol = 9)

for (i in 1:(n_filas - 2)) {
  for (j in 1:(n_columnas - 2)) {
    # Obtener la ventana de 3x3
    w <- rojo[i:(i+2), j:(j+2)]
    v <- as.vector(w)
    matriz_v_rojo[((i - 1) * (n_columnas - 2)) + j, ] <- v
  }
}


# Procesamiento del canal verde
n_filas <- nrow(verde)
n_columnas <- ncol(verde)
matriz_v_verde <- matrix(0, nrow = (n_filas - 2) * (n_columnas - 2), ncol = 9)

for (i in 1:(n_filas - 2)) {
  for (j in 1:(n_columnas - 2)) {
    # Obtener la ventana de 3x3
    w <- verde[i:(i+2), j:(j+2)]
    v <- as.vector(w)
    matriz_v_verde[((i - 1) * (n_columnas - 2)) + j, ] <- v
  }
}

# Procesamiento del canal azul
n_filas <- nrow(azul)
n_columnas <- ncol(azul)
matriz_v_azul <- matrix(0, nrow = (n_filas - 2) * (n_columnas - 2), ncol = 9)

for (i in 1:(n_filas - 2)) {
  for (j in 1:(n_columnas - 2)) {
    # Obtener la ventana de 3x3
    w <- azul[i:(i+2), j:(j+2)]
    v <- as.vector(w)
    matriz_v_azul[((i - 1) * (n_columnas - 2)) + j, ] <- v
  }
}

# Unión de las 3 matrices
matriz_combinada <- cbind(matriz_v_rojo, matriz_v_verde, matriz_v_azul)
media_columnas <- colMeans(matriz_combinada)
desviacion_columnas <- apply(matriz_combinada, 2, sd)
matriz_combinada_escalada <- scale(matriz_combinada, center = media_columnas, scale = desviacion_columnas)

# Análisis PCA
pca_resultado <- prcomp(matriz_combinada_escalada, scale. = FALSE)
summary(pca_resultado)
```

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

``` r
loadings <- pca_resultado$rotation

# Gráficos de Loadings
par(mfrow = c(3, 2))
for (i in 1:5) {
  barplot(loadings[,i], type = "b", xlab = "Variables", ylab = paste("PC", i, "Loading"), 
          main = paste("Loading Plot PC", i))
}

# Visualización de imágenes basadas en PCA
score_images <- array(0, dim = c(n_filas - 2, n_columnas - 2, ncol(pca_resultado$x)))

for (i in 1:ncol(pca_resultado$x)) {
  score_images[, , i] <- matrix(pca_resultado$x[, i], nrow = n_filas - 2, ncol = n_columnas - 2, byrow = TRUE)
}

par(mfrow = c(3, 2))
```

![](z_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
for (i in 1:5) {
  flipped_image <- t(score_images[nrow(score_images):1,,i])
  image(flipped_image, col = gray.colors(256), main = paste("Score Image PC", i))
}
```

![](z_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->
