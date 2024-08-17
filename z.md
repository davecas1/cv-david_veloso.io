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
