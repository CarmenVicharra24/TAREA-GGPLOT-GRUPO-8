TAREA GGPLOT_GRUPO8
================
GRUPO 8
23/1/2022

## Pasos iniciales

``` r
library(ggplot2)
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v tibble  3.1.6     v dplyr   1.0.7
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.1     v forcats 0.5.1
    ## v purrr   0.3.4

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(datos)
```

## 10.1 Parte 1: Ggplot base

## 1.1. Ejecuta ggplot(data = millas). ¿Qué observas?

``` r
ggplot(data = millas)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
## Al ejecutar el ggplot, no nos arroja ni un grafico.
```

## 1.2. ¿Cuántas filas hay en millas? ¿Cuántas columnas?

``` r
view(millas)
```

``` r
## Hay 234 filas y 11 columnas
```

## 1.3. ¿Qué describe la variable traccion? Lee la ayuda de millas para encontrar la respuesta.

``` r
?millas
```

    ## starting httpd help server ... done

``` r
## La variable traccion describe el tipo de traccion, donde d = delantera, t = trasera, 4 = 4 ruedas. Lo que hace referencia al reparto de potencia hacia las ruedas, siendo estas traseras delanteras o todas a la vez. 
```

## 1.4 Realiza un gráfico de dispersión de autopista versus cilindros.

``` r
disp_AC <- ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista))
disp_AC
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

## 1.5. ¿Qué sucede cuando haces un gráfico de dispersión (scatterplot) de clase versus traccion? ¿Por qué no es útil este gráfico?

``` r
disp_TC <- ggplot(data = millas) +
  geom_point(mapping = aes(x = traccion, y = clase))
disp_TC
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
## Este gráfico no es util porque las variables usadas estan categorizadas en. por ello vemos en "X" a 4, d, t y en "Y" las 7 clases de vehículos. 
```

## 10.2 Parte 2: Mapeos estéticos

## 2.1. ¿Qué no va bien en este código? ¿Por qué hay puntos que no son azules?

``` r
## El codigo era incorrecto ya que dentro del aes() se inserto el color, cuando lo correcto es lo siguiente: 
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista), color = "blue")
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

## 2.2. ¿Qué variables en millas son categóricas? ¿Qué variables son continuas? (Pista: escribe ?millas para leer la documentación de ayuda para este conjunto de datos). ¿Cómo puedes ver esta información cuando ejecutas millas?

``` r
?millas
names(millas)
```

    ##  [1] "fabricante"  "modelo"      "cilindrada"  "anio"        "cilindros"  
    ##  [6] "transmision" "traccion"    "ciudad"      "autopista"   "combustible"
    ## [11] "clase"

``` r
summary(millas)
```

    ##   fabricante           modelo            cilindrada         anio     
    ##  Length:234         Length:234         Min.   :1.600   Min.   :1999  
    ##  Class :character   Class :character   1st Qu.:2.400   1st Qu.:1999  
    ##  Mode  :character   Mode  :character   Median :3.300   Median :2004  
    ##                                        Mean   :3.472   Mean   :2004  
    ##                                        3rd Qu.:4.600   3rd Qu.:2008  
    ##                                        Max.   :7.000   Max.   :2008  
    ##    cilindros     transmision          traccion             ciudad     
    ##  Min.   :4.000   Length:234         Length:234         Min.   : 9.00  
    ##  1st Qu.:4.000   Class :character   Class :character   1st Qu.:14.00  
    ##  Median :6.000   Mode  :character   Mode  :character   Median :17.00  
    ##  Mean   :5.889                                         Mean   :16.86  
    ##  3rd Qu.:8.000                                         3rd Qu.:19.00  
    ##  Max.   :8.000                                         Max.   :35.00  
    ##    autopista     combustible           clase          
    ##  Min.   :12.00   Length:234         Length:234        
    ##  1st Qu.:18.00   Class :character   Class :character  
    ##  Median :24.00   Mode  :character   Mode  :character  
    ##  Mean   :23.44                                        
    ##  3rd Qu.:27.00                                        
    ##  Max.   :44.00

``` r
## Las variables categóricas son fabricante, traccion, modelo, transmision, combustible y clase . Las continuas son cilindrada, clindros, anio, autopista, ciudad. Al ejecutar millas, nos dan las variables con <chr< (categóricas) e <int> <dbl> (continuas)
```

## 2.3. Asigna una variable continua a color, size, y shape. ¿Cómo se comportan estas estéticas de manera diferente para variables categóricas y variables continuas?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista, color = ciudad))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista, size = ciudad))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
## ggplot(data = millas) + geom_point(mapping = aes(x = cilindrada, y = autopista, shape = ciudad))

## Al hacer ggplot a una variable continua con shape, nos sale un mensaje de error ya que no puede ser mapeada. 
```

## 2.4. ¿Qué ocurre si asignas o mapeas la misma variable a múltiples estéticas?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista, color = autopista, size = autopista))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

## 2.5. ¿Qué hace la estética stroke? ¿Con qué formas trabaja? (Pista: consulta ?geom_point)

``` r
?geom_point
## La estetica stroke, modifica el ancho del borde. Trabaja con las formas de puntos. 
```

## 2.6 ¿Qué ocurre si se asigna o mapea una estética a algo diferente del nombre de una variable, como aes(color = cilindrada \< 5)?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista, color = cilindrada < 5))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
## Obtenemos un gráfico con una leyenda donde los valores de la cilindrada menores a 5 es celeste con TRUE y los mayores de rojo con FALSE
```

## 10.3 Parte 3: Facetas

## 3.1. ¿Qué ocurre si intentas separar en facetas una variable continua?

``` r
v_autopista <- ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_wrap(~ autopista)
v_autopista
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
v_cilindrada <- ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_wrap(~ cilindrada)
v_cilindrada
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
## Ocurre que al separarlas en facetas, cada subplot nos muestra la cantidad de automoviles con cierto valor en cilindrada y autopista.
```

## 3.2 ¿Qué significan las celdas vacías que aparecen en el gráfico generado usando facet_grid(traccion \~ cilindros)? ¿Cómo se relacionan con este gráfico?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = traccion, y = cilindros)) +
facet_grid(traccion ~ cilindros)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

``` r
## Las celdas que se encuentran en blanco es porque no presentan subconjunto de datos. 
## Se relaciona con el gráfico porque ayuda a dividir las facetas según la combinación de dos variables.
```

## 3.3 ¿Qué grafica el siguiente código? ¿Qué hace . ?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_grid(traccion ~ .)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggplot(data = millas) +
 geom_point(mapping = aes(x = cilindrada, y = autopista)) +
 facet_grid(. ~ cilindros)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
## Grafica la tracción por un lado y por el otro los cilindros. Separa de forma independiente cada uno para poder observarlos mejor.
## El símbolo . ignora la dimensión al momento de dibujar las facetas. Por ejemplo, autopista ~ . divide por los valores de autopista en el eje y.
```

## 3.4 ¿Cuáles son las ventajas de separar en facetas en lugar de aplicar una estética de color?

``` r
## Las ventajas de separar en facetas es que ayuda a distinguir las variables que se encuentran en el gráfico.
```

## 3.5 ¿Cuáles son las desventajas?

``` r
## Que no se pueden distinguir de acuerdo a la fecha, año, tiempo, etc.
```

## 3.6 ¿Cómo cambiaría este balance si tuvieras un conjunto de datos más grande?

``` r
## Se observaron más facetas con más variables.
```

## 3.7 - Lee ?facet_wrap.

``` r
## Nos sale “Wrap a 1d ribbon of panels into 2d”
```

## 3.8 ¿Qué hace nrow? ¿Qué hace ncol?

``` r
## La función de nrow devuelve el número de filas que están presentes en un marco de datos o matriz.
## La función ncol devuelve el número de columnas de una matriz o marco de datos.
```

## 3.9 ¿Qué otras opciones controlan el diseño de los paneles individuales?

``` r
##Cambiar las coordenadas x,y. También la variable que desees que se visualice en los gráficos.
```

## 3.10 ¿Por qué facet_grid() no tiene argumentos nrow y ncol?

``` r
## nrow y ncol no son necesarios con facet_grid ya que el número de valores únicos en la función determina el número de filas y columnas.
```

## 3.1 - Cuando usas facet_grid(), generalmente deberías poner la variable con un mayor número de niveles únicos en las columnas. ¿Por qué?

``` r
## Genera más espacio para las columnas en caso que nuestro gráfico se ubique de forma horizontal.
```

## 10.4 Parte 4: Objetos geométricos

## 4.1 ¿Qué geom usarías para generar un gráfico de líneas? ¿Y para un diagrama de caja? ¿Y para un histograma? ¿Y para un gráfico de área?

``` r
## grafico de lineas: geom_line()
## diagrama de caja: geom_boxplot()
## histograma: geom_histogram() 
## grafico de area: geom_area()
```

## 4.2 Ejecuta este código en tu mente y predice cómo se verá el output. Luego, ejecuta el código en R y verifica tus predicciones.

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista, color = traccion)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
## Se encuentra un diagrama de dispersión, donde el eje x es cilindrada y el eje y es autopista. Los puntos que se encuentran de colores son la tracción.
```

## 4.3 ¿Qué muestra show.legend = FALSE? ¿Qué pasa si lo quitas? ¿Por qué crees que lo utilizamos antes en el capítulo?

``` r
## Oculta la leyenda. Si lo quito mostrará la relación entre traccion y la paleta de colores.Lo utilizamos antes porque nos ayuda a diferenciar sin grupos, por eso usamos los grupos y colores. 
```

## 4.4 ¿Qué hace el argumento se en geom_smooth()?

``` r
## Agrega bandas de error estándar a las líneas que se visualizan en nuestro gráfico
```

## 4.5 ¿Se verán distintos estos gráficos? ¿Por qué sí o por qué no?

``` r
##  No, porque se presenta el mismo gráfico, utilizando los códigos. 
```

## 4.6 Recrea el código R necesario para generar los siguientes gráficos:

## 1

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_point() +
   geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->
## 2

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_smooth(aes(group = traccion), se = FALSE) +
   geom_point()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->
## 3

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista, color = traccion)) +
   geom_point() +
   geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->
## 4

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_point(aes(color = traccion)) +
   geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->
## 5

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_point(aes(color = traccion)) +
   geom_smooth(aes(linetype = traccion), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->
## 6

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_point(size = 4, colour = "white") +
   geom_point(aes(colour = traccion))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

## 10.5 parte 5

## 5.1 ¿Cuál es el geom predeterminado asociado con stat_summary()? ¿Cómo podrías reescribir el gráfico anterior para usar esa función geom en lugar de la función stat?

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
   geom_point(size = 4, colour = "white") +
   geom_point(aes(colour = traccion))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->

``` r
## La geometría que se usa para stat_summary() es geom_pointrange()
```

## 1er gráfico

``` r
ggplot(data = diamantes) +
  stat_summary(
    mapping = aes(x = corte, y = profundidad),
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median
  )
```

    ## Warning: `fun.y` is deprecated. Use `fun` instead.

    ## Warning: `fun.ymin` is deprecated. Use `fun.min` instead.

    ## Warning: `fun.ymax` is deprecated. Use `fun.max` instead.

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

``` r
## El estadístico para geom_pointrange() es identity() pero puede incluir el argumento stat = "summary" para usar stat_summary() en lugar de stat_identity().
```

``` r
ggplot(data = diamantes) +
  geom_pointrange(
    mapping = aes(x = corte, y = profundidad),
    stat = "summary"
  )
```

    ## No summary function supplied, defaulting to `mean_se()`

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

``` r
## El mensaje resultante en stat_summary() indica que se usó mean y sd para calcular el centro y los extremos de la línea. Sin embargo, en el gráfico original se usaron el máximo y mínimo para los extremos. Para recrear el gráfico original hay que especificar los valores de fun.ymin, fun.ymax, y fun.y.
```

``` r
ggplot(data = diamantes) +
  geom_pointrange(
    mapping = aes(x = corte, y = profundidad),
    stat = "summary",
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median
  )
```

    ## Warning: Ignoring unknown parameters: fun.ymin, fun.ymax, fun.y

    ## No summary function supplied, defaulting to `mean_se()`

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

## 5.2 ¿Qué hace geom_col()? ¿En qué se diferencia de geom_bar()?

``` r
##  El estadístico por defecto en geom_col() es distinto de geom_bar().geom_col() usa stat_identity(), que deja los datos sin transformar.geom_col() espera que los datos contengan los valores de x y los valores de y que representan la altura de las columnas.geom_bar() usa stat_bin() y espera únicamente los valores de x.stat_bin(), procesa los datos de entrada y realiza un conteo del número de observaciones para cada valor de x, lo cual genera la variable.
```

## 5.3 La mayoría de los geoms y las transformaciones estadísticas vienen en pares que casi siempre se usan en conjunto. Lee la documentación y haz una lista de todos los pares. ¿Qué tienen en común?

``` r
## geom_bar()           |stat_count() 
## geom_bin2d()         |stat_bin_2d()
## geom_boxplot()       |stat_boxplot()
## geom_contour()       |stat_contour()
## geom_count()       |stat_sum()
## geom_density()       |stat_density()
## geom_density_2d()    |stat_density_2d()
## geom_hex()           |stat_hex()
## geom_freqpoly()    |stat_bin()
## geom_histogram()   |stat_bin()
## geom_qq_line()       |stat_qq_line()
## geom_qq()            |stat_qq()
## geom_quantile()      |stat_quantile()
## geom_smooth()        |stat_smooth()
## geom_violin()        |stat_violin()
## geom_sf()            |stat_sf()
```

``` r
## geometria               |estadistico                  |documentacion 
## geom_abline()        
## geom_hline()     
## geom_vline()     
## geom_bar()               stat_count()                       x
## geom_col()       
## geom_bin2d()           stat_bin_2d()                    x
## geom_blank()     
## geom_boxplot()           stat_boxplot()                   x
## geom_countour()        stat_countour()                    x
## geom_count()           stat_sum()                         x
## geom_density()           stat_density()                   x
## geom_density_2d()        stat_density_2d()                  x
## geom_dotplot()       
## geom_errorbarh()     
## geom_hex()               stat_hex()                       x
## geom_freqpoly()        stat_bin()                         x
## geom_histogram()       stat_bin()                         x
## geom_crossbar()      
## geom_errorbar()      
## geom_linerange()     
## geom_pointrange()        
## geom_map()       
## geom_point()     
## geom_map()       
## geom_path()      
## geom_line()      
## geom_step()      
## geom_point()     
## geom_polygon()       
## geom_qq_line()           stat_qq_line()                  x
## geom_qq()                stat_qq()                         x
## geom_quantile()        stat_quantile()                   x
## geom_ribbon()        
## geom_area()      
## geom_rug()       
## geom_smooth()            stat_smooth()                     x
## geom_spoke()     
## geom_label()     
## geom_text()      
## geom_raster()        
## geom_rect()      
## geom_tile()       
## geom_violin()            stat_ydensity()                x
## geom_sf()                stat_sf()                        x
```

``` r
## geometria               |estadistico                  |documentacion 
## stat_ecdf()              geom_step() 
## stat_ellipse()           geom_path() 
## stat_function()        geom_path()   
## stat_identity()        geom_point()  
## stat_summary_2d()        geom_tile() 
## stat_summary_hex()       geom_hex()  
## stat_summary_bin()       geom_pointrange()   
## stat_summary()           geom_pointrange()   
## stat_unique()            geom_point()    
## stat_count()           geom_bar()                            x
## stat_bin_2d()            geom_tile()                         x
## stat_boxplot()           geom_boxplot()                      x
## stat_countour()        geom_contour()                        x
## stat_sum()               geom_point()                          x
## stat_density()           geom_area()                         x
## stat_density_2d()        geom_density_2d()                     x
## stat_bin_hex()           geom_hex()                          x
## stat_bin()               geom_bar()                          x
## stat_qq_line()           geom_path()                         x
## stat_qq()                geom_point()                          x
## stat_quantile()        geom_quantile()                       x
## stat_smooth()            geom_smooth()                       x
## stat_ydensity()        geom_violin()                       x
## stat_sf()                geom_rect()                         x
```

## 5.4 ¿Qué variables calcula stat_smooth()? ¿Qué parámetros controlan su comportamiento?

``` r
## La función stat_smooth() calcula las siguientes variables:
## y: valor predicho
## ymin: menor valor del intervalo de confianza
## ymax: mayor valor del intervalo de confianza
## se: error estándar

## La sección “Computed Variables” en la documentación de stat_smooth() contiene estas variables.
## Los parámetros que controlan stat_smooth() incluyen
## ●    method: cuál método utilizar
## ●    formula: las fórmulas, al igual que method, determinan cómo se hará el cálculo del intervalo de confianza y los argumentos adicionales que se requieran.
## ●    na.rm: si acaso se eliminarán los casos perdidos
```

## 5.5 En nuestro gráfico de barras de proporción necesitamos establecer group = 1. ¿Por qué? En otras palabras, ¿cuál es el problema con estos dos gráficos?

``` r
ggplot(data = diamantes) +
geom_bar(mapping = aes(x = corte, y = ..prop..))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

``` r
ggplot(data = diamantes) +
geom_bar(mapping = aes(x = corte, fill = color, y = ..prop..))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-52-2.png)<!-- -->

``` r
## Si no se incluye group = 1, todas las barras en el gráfico tendrán altura 1.
```

``` r
## La función geom_bar() asume que los grupos son iguales a los valores de x dado que el estadístico realiza un conteo dentro de los grupos.
```

``` r
ggplot(data = diamantes) +
  geom_bar(mapping = aes(x = corte, y = ..prop..))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-55-1.png)<!-- -->

``` r
ggplot(data = diamantes) +
  geom_bar(mapping = aes(x = corte, y = ..prop..))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-56-1.png)<!-- -->

``` r
ggplot(data = diamantes) +
  geom_bar(mapping = aes(x = corte, fill = color, y = ..prop..))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-57-1.png)<!-- -->

``` r
ggplot(data = diamantes) +
  geom_bar(mapping = aes(x = corte, y = ..prop.., group = 1))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-58-1.png)<!-- -->

``` r
ggplot(data = diamantes) + 
  geom_bar(aes(x = corte, y = ..count.. / sum(..count..), fill = color))
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-59-1.png)<!-- -->

## 10.6 Parte 6

## 6.1 ¿Cuál es el problema con este gráfico? ¿Cómo podrías mejorarlo?

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-60-1.png)<!-- -->

``` r
## Respuesta:

ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point(position = "jitter")
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-61-1.png)<!-- -->

## 6.2 ¿Qué parámetros de geom_jitter() controlan la cantidad de ruido?

``` r
## Respuesta:
## A partir de la documentación de geom_jitter(), existen dos argumentos:
## width controla el desplazamiento vertical
## height controla el desplazamiento horizontal
## Los valores por defecto de width y height introducen ruido en ambas direcciones.

ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point(position = position_jitter())
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-62-1.png)<!-- -->

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_jitter(width = 0)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-63-1.png)<!-- -->

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_jitter(width = 20)
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-64-1.png)<!-- -->

## 6.3 Compara y contrasta geom_jitter() con geom_count()

``` r
## Respuesta:
## geom_jitter() agrega una variación al azar a los puntos del gráfico, es decir que distorsiona la ubicación de los puntos en el gráfico. Este método reduce la superposición ya que es poco probable que al mover los puntos al azar estos queden en la misma ubicación. Sin embargo, el problema de reducir la superposición es que se distorsionan los valores mostrados de x e y.
```

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_jitter()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-66-1.png)<!-- -->

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_count()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-67-1.png)<!-- -->

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista, color = clase)) +
  geom_jitter()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-68-1.png)<!-- -->

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista, color = clase)) +
  geom_count()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-69-1.png)<!-- -->

## 6.4 ¿Cuál es el ajuste de posición predeterminado de geom_boxplot()? Crea una visualización del conjunto de datos de millas que lo demuestre.

``` r
## Respuesta:
## La posición por defecto para geom_boxplot() es "dodge2", que es un atajo de position_dodge2.
## Este ajuste no cambia la posición vertical pero mueve las geometrías horizontalmente para evitar la superposición.
```

``` r
ggplot(data = millas, aes(x = transmision, y = autopista, colour = clase)) +
  geom_boxplot()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-71-1.png)<!-- -->

``` r
ggplot(data = millas, aes(x = transmision, y = autopista, colour = clase)) +
  geom_boxplot(position = "identity")
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-72-1.png)<!-- -->

## 10.7 Parte 7

## 7.1 Convierte un gráfico de barras apiladas en un gráfico circular usando coord_polar().

``` r
## Respuesta

ggplot(millas, aes(x = factor(1), fill = traccion)) +
  geom_bar()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-73-1.png)<!-- -->

``` r
ggplot(millas, aes(x = factor(1), fill = traccion)) +
  geom_bar(width = 1) +
  coord_polar(theta = "y")
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-74-1.png)<!-- -->

``` r
ggplot(millas, aes(x = factor(1), fill = traccion)) +
  geom_bar(width = 1) + coord_polar()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-75-1.png)<!-- -->

## 7.2 ¿Qué hace labs()? Lee la documentación

``` r
## Respuesta:
## labs agrega los títulos de los ejes, título del gráfico y la leyenda.
```

``` r
ggplot(data = millas, mapping = aes(x = clase, y = autopista)) +
  geom_boxplot() +
  coord_flip() +
  labs(y = "Millas por Galón en Autopista", x = "Clase",
       title = "Millas por Galón en Autopista por Tipo de Vehículo",
       subtitle = "1999-2008",
caption = "Fuente: http://fueleconomy.gov")
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-77-1.png)<!-- -->

## 7.3 ¿Cuál es la diferencia entre coord_quickmap() y coord_map()?

``` r
## Respuesta:
## coord_map() usa una proyección cartográfica para proyectar la Tierra sobre una superficie bidimensional. Por defecto usa la Proyección de Mercator, la cual se aplica a todas las geometrías del gráfico.

## coord_quickmap() usa una aproximación más rápida que ignora la curvatura de la tierra y ajusta de acuerdo a la razón de latitud y longitud. Esta es una alternativa computacionalmente más rápida que no genera la necesidad de transformar las geometrías individuales.
```

## 7.4 ¿Qué te dice la gráfica siguiente sobre la relación entre ciudad y autopista? ¿Por qué es coord_fixed() importante? ¿Qué hace geom_abline()?

``` r
## Respuesta

ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point() +
  geom_abline() +
  coord_fixed()
```

![](TAREA-GGPLOT_-GRUPO-8_files/figure-gfm/unnamed-chunk-79-1.png)<!-- -->

``` r
## Respuesta:
## La función coord_fixed() asegura que la línea que genera geom_abline() tenga un ángulo de 45 grados. De este modo es más fácil comparar a partir de los casos en que los rendimientos en autopista y ciudad son iguales.
```
