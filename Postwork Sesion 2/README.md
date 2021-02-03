# Postwork Sesión 2.
Equipo 12
### Solución

#### Objetivo
* Importar múltiples archivos .csv a R.
* Observar algunas características y manipular los data frames.
* Combinar múltiples data frames en un único data frame

#### Desarrollo

Ahora vamos a generar un cúmulo de datos mayor al que se tenía, esta es una situación habitual que se puede presentar para complementar un análisis, siempre es importante estar revisando las características o tipos de datos que tenemos, por si es necesario realizar alguna transformación en las variables y poder hacer operaciones aritméticas si es el caso, además de sólo tener presente algunas de las variables, no siempre se requiere el uso de todas para ciertos procesamientos.

1. Importa los datos de soccer de las temporadas 2017/2018, 2018/2019 y 2019/2020 de la primera división de la liga española a R, los datos los puedes encontrar en el siguiente enlace: https://www.football-data.co.uk/spainm.php

2. Obten una mejor idea de las características de los data frames al usar las funciones: str, head, View y summary

3. Con la función select del paquete dplyr selecciona únicamente las columnas Date, HomeTeam, AwayTeam, FTHG, FTAG y FTR; esto para cada uno de los data frames. (Hint: también puedes usar lapply).

4. Asegúrate de que los elementos de las columnas correspondientes de los nuevos data frames sean del mismo tipo (Hint 1: usa as.Date y mutate para arreglar las fechas). Con ayuda de la función rbind forma un único data frame que contenga las seis columnas mencionadas en el punto 3 (Hint 2: la función do.call podría ser utilizada).

#### Código

Importación de datos desde la url.
```R
u1718 <- "https://www.football-data.co.uk/mmz4281/1718/SP1.csv"
u1819 <- "https://www.football-data.co.uk/mmz4281/1819/SP1.csv"
u1920 <- "https://www.football-data.co.uk/mmz4281/1920/SP1.csv"

download.file(url = u1718, destfile = "SP1-1718.csv", mode = "wb")
download.file(url = u1819, destfile = "SP1-1819.csv", mode = "wb")
download.file(url = u1920, destfile = "SP1-1920.csv", mode = "wb")

lista <- lapply(dir(), read.csv)

```
Visualización de las características de los datasets
```R
str(lista[1])
head(lista[1])
View(lista[1])
summary(lista[1])
```
Selección de columnas indicadas
```R
library(dplyr)
lista <- lapply(lista, select, Date,HomeTeam,AwayTeam,FTHG,FTAG,FTR)
```
Se iguala el formato de la fecha para cada uno de los dataframes y se unen en uno solo
```R
lista[[1]] <- mutate(lista[[1]], Date = as.Date(Date, "%d/%m/%y"))
lista[[2]] <- mutate(lista[[2]], Date = as.Date(Date, "%d/%m/%Y"))
lista[[3]] <- mutate(lista[[3]], Date = as.Date(Date, "%d/%m/%Y"))

data <- do.call(rbind, lista)
```
#### Resultado

#### Conslusion
Habran ocaciones en que los datos que requerimos estarán separados en diferentes archivos con diferente orden en las columnas o formato de fechas, en esta sesión aprendimos cómo unir los dataframes en uno solo dandole un formato común para las fechas y seleccionando solo las columnas requeridas.


