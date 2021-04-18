Untitled
================

``` r
library(quanteda)
```

    ## Warning: package 'quanteda' was built under R version 4.0.5

    ## Package version: 3.0.0
    ## Unicode version: 10.0
    ## ICU version: 61.1

    ## Parallel computing: 8 of 8 threads used.

    ## See https://quanteda.io for tutorials and examples.

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.1.0     v stringr 1.4.0
    ## v tidyr   1.1.3     v forcats 0.5.1
    ## v readr   1.4.0

    ## Warning: package 'ggplot2' was built under R version 4.0.5

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(utf8)
library(ggplot2)

setwd("C:/Users/Dieca/OneDrive/Escritorio")
primer_tiempo2020 <- read_csv("Primer_Tiempo2020.csv",col_names = TRUE)
```

    ## 
    ## -- Column specification --------------------------------------------------------
    ## cols(
    ##   .default = col_double(),
    ##   torneo = col_character(),
    ##   equipo = col_character(),
    ##   id_partido = col_character(),
    ##   partido = col_character(),
    ##   fasepartido = col_character(),
    ##   local = col_logical(),
    ##   tiempo = col_character()
    ## )
    ## i Use `spec()` for the full column specifications.

``` r
#str(primer_tiempo2020)
attach(primer_tiempo2020)

summary(primer_tiempo2020)
```

    ##     torneo             equipo           id_partido          partido         
    ##  Length:130         Length:130         Length:130         Length:130        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  fasepartido          local            tiempo           accuratePass  
    ##  Length:130         Mode :logical   Length:130         Min.   : 62.0  
    ##  Class :character   FALSE:65        Class :character   1st Qu.:115.2  
    ##  Mode  :character   TRUE :65        Mode  :character   Median :143.5  
    ##                                                        Mean   :147.5  
    ##                                                        3rd Qu.:181.2  
    ##                                                        Max.   :269.0  
    ##    wonTackle       lostCorners    goalsConceded        saves    
    ##  Min.   : 0.000   Min.   :0.000   Min.   :0.0000   Min.   :0.0  
    ##  1st Qu.: 3.000   1st Qu.:1.000   1st Qu.:0.0000   1st Qu.:1.0  
    ##  Median : 5.000   Median :2.000   Median :0.0000   Median :1.0  
    ##  Mean   : 5.154   Mean   :2.277   Mean   :0.5923   Mean   :1.5  
    ##  3rd Qu.: 7.000   3rd Qu.:3.000   3rd Qu.:1.0000   3rd Qu.:2.0  
    ##  Max.   :14.000   Max.   :7.000   Max.   :3.0000   Max.   :5.0  
    ##  ontargetScoringAtt totalScoringAtt     subsMade       totalThrows   
    ##  Min.   :0.000      Min.   : 0.000   Min.   :0.0000   Min.   : 3.00  
    ##  1st Qu.:1.000      1st Qu.: 4.000   1st Qu.:0.0000   1st Qu.: 8.00  
    ##  Median :2.000      Median : 6.000   Median :0.0000   Median :11.00  
    ##  Mean   :2.108      Mean   : 5.938   Mean   :0.1077   Mean   :10.98  
    ##  3rd Qu.:3.000      3rd Qu.: 7.750   3rd Qu.:0.0000   3rd Qu.:13.00  
    ##  Max.   :5.000      Max.   :14.000   Max.   :1.0000   Max.   :26.00  
    ##  totalYellowCard    goalKicks        totalPass       fkFoulWon     
    ##  Min.   :0.0000   Min.   : 0.000   Min.   : 93.0   Min.   : 2.000  
    ##  1st Qu.:0.0000   1st Qu.: 2.000   1st Qu.:159.5   1st Qu.: 5.000  
    ##  Median :1.0000   Median : 4.000   Median :189.0   Median : 6.000  
    ##  Mean   :0.9077   Mean   : 3.962   Mean   :190.9   Mean   : 6.338  
    ##  3rd Qu.:1.0000   3rd Qu.: 5.000   3rd Qu.:222.5   3rd Qu.: 8.000  
    ##  Max.   :3.0000   Max.   :11.000   Max.   :304.0   Max.   :12.000  
    ##   totalTackle       fkFoulLost     possessionPercentage totalClearance  
    ##  Min.   : 1.000   Min.   : 2.000   Min.   :23.60        Min.   : 0.000  
    ##  1st Qu.: 5.000   1st Qu.: 6.000   1st Qu.:45.62        1st Qu.: 4.000  
    ##  Median : 7.000   Median : 7.000   Median :50.00        Median : 7.000  
    ##  Mean   : 7.192   Mean   : 7.054   Mean   :50.00        Mean   : 7.385  
    ##  3rd Qu.: 9.000   3rd Qu.: 9.000   3rd Qu.:54.38        3rd Qu.:10.000  
    ##  Max.   :15.000   Max.   :13.000   Max.   :76.40        Max.   :16.000  
    ##  formationUsed blockedScoringAtt   goalAssist         goals       
    ##  Min.   :0     Min.   :0.000     Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0     1st Qu.:0.000     1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0     Median :1.000     Median :0.0000   Median :0.0000  
    ##  Mean   :0     Mean   :1.262     Mean   :0.3769   Mean   :0.5923  
    ##  3rd Qu.:0     3rd Qu.:2.000     3rd Qu.:1.0000   3rd Qu.:1.0000  
    ##  Max.   :0     Max.   :6.000     Max.   :2.0000   Max.   :3.0000  
    ##   totalOffside   shotOffTarget     wonCorners     cornerTaken   
    ##  Min.   :0.000   Min.   :0.000   Min.   :0.000   Min.   :0.000  
    ##  1st Qu.:0.000   1st Qu.:1.000   1st Qu.:1.000   1st Qu.:1.000  
    ##  Median :1.000   Median :2.000   Median :2.000   Median :2.000  
    ##  Mean   :1.038   Mean   :2.569   Mean   :2.277   Mean   :2.269  
    ##  3rd Qu.:2.000   3rd Qu.:4.000   3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :5.000   Max.   :7.000   Max.   :7.000   Max.   :7.000  
    ##  penaltyConceded   penaltyFaced    penGoalsConceded   penaltyWon    
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :0.0000   Median :0.0000   Median :0.0000   Median :0.0000  
    ##  Mean   :0.1692   Mean   :0.1692   Mean   :0.1308   Mean   :0.1692  
    ##  3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000   3rd Qu.:0.0000  
    ##  Max.   :2.0000   Max.   :2.0000   Max.   :1.0000   Max.   :2.0000  
    ##     ownGoals        penaltySave       secondYellow      totalRedCard    
    ##  Min.   :0.00000   Min.   :0.00000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.00000   Median :0.00000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.02308   Mean   :0.02308   Mean   :0.01538   Mean   :0.04615  
    ##  3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.00000   Max.   :1.00000   Max.   :1.00000   Max.   :1.00000  
    ##  posesion_Rival  precision_pases precision_tiros  minutos_juego  
    ##  Min.   :23.60   Min.   :50.68   Min.   :  0.00   Min.   :10.62  
    ##  1st Qu.:45.62   1st Qu.:70.71   1st Qu.: 25.00   1st Qu.:20.53  
    ##  Median :50.00   Median :76.40   Median : 40.00   Median :22.50  
    ##  Mean   :50.00   Mean   :75.99   Mean   : 41.20   Mean   :22.50  
    ##  3rd Qu.:54.38   3rd Qu.:82.28   3rd Qu.: 57.14   3rd Qu.:24.47  
    ##  Max.   :76.40   Max.   :89.43   Max.   :100.00   Max.   :34.38  
    ##  minutos_juegorival golesSalvados   foulsInofensivos cortarJuegoContrario
    ##  Min.   :10.62      Min.   :0.000   Min.   : 1.000   Min.   : 4.00       
    ##  1st Qu.:20.53      1st Qu.:1.000   1st Qu.: 5.000   1st Qu.:10.00       
    ##  Median :22.50      Median :1.000   Median : 6.000   Median :12.00       
    ##  Mean   :22.50      Mean   :1.523   Mean   : 6.146   Mean   :12.21       
    ##  3rd Qu.:24.47      3rd Qu.:2.000   3rd Qu.: 8.000   3rd Qu.:15.00       
    ##  Max.   :34.38      Max.   :5.000   Max.   :11.000   Max.   :24.00       
    ##   juegoCortado  
    ##  Min.   : 8.00  
    ##  1st Qu.:17.00  
    ##  Median :20.00  
    ##  Mean   :20.64  
    ##  3rd Qu.:25.00  
    ##  Max.   :40.00

``` r
## Borrar Datos Char

primer_tiempo2020
```

    ## # A tibble: 130 x 49
    ##    torneo   equipo   id_partido  partido   fasepartido local tiempo accuratePass
    ##    <chr>    <chr>    <chr>       <chr>     <chr>       <lgl> <chr>         <dbl>
    ##  1 Primera~ Uni<f3>~ 6xszsf73jq~ Universi~ Regular Se~ FALSE fh              235
    ##  2 Primera~ Univers~ 6xszsf73jq~ Universi~ Regular Se~ TRUE  fh              199
    ##  3 Primera~ Everton  e88gat05jr~ Universi~ Regular Se~ FALSE fh              157
    ##  4 Primera~ Univers~ e88gat05jr~ Universi~ Regular Se~ TRUE  fh              192
    ##  5 Primera~ Curic<f~ 35ijq76er8~ Universi~ Regular Se~ FALSE fh              142
    ##  6 Primera~ Univers~ 35ijq76er8~ Universi~ Regular Se~ TRUE  fh              168
    ##  7 Primera~ Coquimb~ 9o9ji2f68p~ Universi~ Regular Se~ FALSE fh              190
    ##  8 Primera~ Univers~ 9o9ji2f68p~ Universi~ Regular Se~ TRUE  fh              200
    ##  9 Primera~ Santiag~ 357wqv3701~ Universi~ Regular Se~ FALSE fh              156
    ## 10 Primera~ Univers~ 357wqv3701~ Universi~ Regular Se~ TRUE  fh               92
    ## # ... with 120 more rows, and 41 more variables: wonTackle <dbl>,
    ## #   lostCorners <dbl>, goalsConceded <dbl>, saves <dbl>,
    ## #   ontargetScoringAtt <dbl>, totalScoringAtt <dbl>, subsMade <dbl>,
    ## #   totalThrows <dbl>, totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>,
    ## #   fkFoulWon <dbl>, totalTackle <dbl>, fkFoulLost <dbl>,
    ## #   possessionPercentage <dbl>, totalClearance <dbl>, formationUsed <dbl>,
    ## #   blockedScoringAtt <dbl>, goalAssist <dbl>, goals <dbl>, totalOffside <dbl>,
    ## #   shotOffTarget <dbl>, wonCorners <dbl>, cornerTaken <dbl>,
    ## #   penaltyConceded <dbl>, penaltyFaced <dbl>, penGoalsConceded <dbl>,
    ## #   penaltyWon <dbl>, ownGoals <dbl>, penaltySave <dbl>, secondYellow <dbl>,
    ## #   totalRedCard <dbl>, posesion_Rival <dbl>, precision_pases <dbl>,
    ## #   precision_tiros <dbl>, minutos_juego <dbl>, minutos_juegorival <dbl>,
    ## #   golesSalvados <dbl>, foulsInofensivos <dbl>, cortarJuegoContrario <dbl>,
    ## #   juegoCortado <dbl>

``` r
primer_tiempo2020 <- primer_tiempo2020[,!(colnames(primer_tiempo2020) %in% c("id_partido", "fasepartido", "local", "tiempo","formationUsed", "torneo"))]
primer_tiempo2020
```

    ## # A tibble: 130 x 43
    ##    equipo    partido      accuratePass wonTackle lostCorners goalsConceded saves
    ##    <chr>     <chr>               <dbl>     <dbl>       <dbl>         <dbl> <dbl>
    ##  1 Uni<f3>n~ Universidad~          235         2           3             1     4
    ##  2 Universi~ Universidad~          199         2           0             0     1
    ##  3 Everton   Universidad~          157         7           6             0     3
    ##  4 Universi~ Universidad~          192         4           1             0     2
    ##  5 Curic<f3~ Universidad~          142         6           3             2     2
    ##  6 Universi~ Universidad~          168         8           1             1     2
    ##  7 Coquimbo~ Universidad~          190         3           0             0     2
    ##  8 Universi~ Universidad~          200         5           0             0     0
    ##  9 Santiago~ Universidad~          156         4           3             0     0
    ## 10 Universi~ Universidad~           92         4           1             1     1
    ## # ... with 120 more rows, and 36 more variables: ontargetScoringAtt <dbl>,
    ## #   totalScoringAtt <dbl>, subsMade <dbl>, totalThrows <dbl>,
    ## #   totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>, fkFoulWon <dbl>,
    ## #   totalTackle <dbl>, fkFoulLost <dbl>, possessionPercentage <dbl>,
    ## #   totalClearance <dbl>, blockedScoringAtt <dbl>, goalAssist <dbl>,
    ## #   goals <dbl>, totalOffside <dbl>, shotOffTarget <dbl>, wonCorners <dbl>,
    ## #   cornerTaken <dbl>, penaltyConceded <dbl>, penaltyFaced <dbl>,
    ## #   penGoalsConceded <dbl>, penaltyWon <dbl>, ownGoals <dbl>,
    ## #   penaltySave <dbl>, secondYellow <dbl>, totalRedCard <dbl>,
    ## #   posesion_Rival <dbl>, precision_pases <dbl>, precision_tiros <dbl>,
    ## #   minutos_juego <dbl>, minutos_juegorival <dbl>, golesSalvados <dbl>,
    ## #   foulsInofensivos <dbl>, cortarJuegoContrario <dbl>, juegoCortado <dbl>

``` r
## Analisis descriptivo


fh2020 <- primer_tiempo2020[order(primer_tiempo2020$goalAssist, decreasing = TRUE),]
fh2020
```

    ## # A tibble: 130 x 43
    ##    equipo    partido      accuratePass wonTackle lostCorners goalsConceded saves
    ##    <chr>     <chr>               <dbl>     <dbl>       <dbl>         <dbl> <dbl>
    ##  1 Universi~ Universidad~          168         8           1             1     2
    ##  2 Audax It~ Uni<f3>n Es~           94         7           2             1     1
    ##  3 O'Higgins O'Higgins v~          114         9           2             1     1
    ##  4 La Serena La Serena v~          129         1           0             0     3
    ##  5 Huachipa~ Huachipato ~           89         4           7             0     2
    ##  6 Universi~ Deportivo A~          202         6           2             1     3
    ##  7 Deportiv~ Deportivo A~          162         9           1             0     0
    ##  8 Colo Colo Colo Colo v~          231         4           0             0     0
    ##  9 Audax It~ Audax Itali~          219         6           1             0     0
    ## 10 Universi~ Universidad~          199         2           0             0     1
    ## # ... with 120 more rows, and 36 more variables: ontargetScoringAtt <dbl>,
    ## #   totalScoringAtt <dbl>, subsMade <dbl>, totalThrows <dbl>,
    ## #   totalYellowCard <dbl>, goalKicks <dbl>, totalPass <dbl>, fkFoulWon <dbl>,
    ## #   totalTackle <dbl>, fkFoulLost <dbl>, possessionPercentage <dbl>,
    ## #   totalClearance <dbl>, blockedScoringAtt <dbl>, goalAssist <dbl>,
    ## #   goals <dbl>, totalOffside <dbl>, shotOffTarget <dbl>, wonCorners <dbl>,
    ## #   cornerTaken <dbl>, penaltyConceded <dbl>, penaltyFaced <dbl>,
    ## #   penGoalsConceded <dbl>, penaltyWon <dbl>, ownGoals <dbl>,
    ## #   penaltySave <dbl>, secondYellow <dbl>, totalRedCard <dbl>,
    ## #   posesion_Rival <dbl>, precision_pases <dbl>, precision_tiros <dbl>,
    ## #   minutos_juego <dbl>, minutos_juegorival <dbl>, golesSalvados <dbl>,
    ## #   foulsInofensivos <dbl>, cortarJuegoContrario <dbl>, juegoCortado <dbl>

``` r
## Sub DataFrames

fh2020_corners = fh2020[,colnames(primer_tiempo2020) %in% c( "equipo", "lostCorners", "partido", "wonCorners", "cornerTaken", "shotogTarget")]
fh2020_corners = fh2020_corners[order(fh2020_corners$wonCorners, decreasing = TRUE),]
fh2020_corners
```

    ## # A tibble: 130 x 5
    ##    equipo           partido                   lostCorners wonCorners cornerTaken
    ##    <chr>            <chr>                           <dbl>      <dbl>       <dbl>
    ##  1 Audax Italiano   Huachipato vs Audax Ital~           5          7           7
    ##  2 Uni<f3>n La Cal~ Uni<f3>n La Calera vs Co~           2          6           6
    ##  3 Universidad de ~ Universidad de Chile vs ~           1          6           6
    ##  4 Universidad de ~ Huachipato vs Universida~           3          6           6
    ##  5 Uni<f3>n La Cal~ Everton vs Uni<f3>n La C~           1          6           6
    ##  6 Huachipato       Huachipato vs Audax Ital~           7          5           5
    ##  7 Uni<f3>n La Cal~ Uni<f3>n La Calera vs La~           3          5           5
    ##  8 Uni<f3>n Espa<f~ O'Higgins vs Uni<f3>n Es~           0          5           5
    ##  9 Santiago Wander~ O'Higgins vs Santiago Wa~           1          5           5
    ## 10 Deportivo Antof~ La Serena vs Deportivo A~           3          5           5
    ## # ... with 120 more rows

``` r
fh2020_fauls <- NULL
fh2020_fauls = fh2020[,colnames(primer_tiempo2020) %in% c("equipo", "partido", "totalTackle", "totalYellowCard", "fkFoulWon", "fkFoulLost", "totalOffside", "totalRedCard")]

#fh2020_fauls = fh2020_fauls[order(fh2020_tiros$totalYellowCard, decreasing = TRUE),]
#fh2020_fauls


## Filtrar Datos
Palestino <- filter(primer_tiempo2020, equipo == "Palestino")
Palestino_corners <- filter(fh2020_corners, equipo == "Palestino")
Palestino_fauls <- filter(fh2020_fauls, equipo == "Palestino")


## Agregar Promedio/Suma Total/Min/...

Palestino_corners <- Palestino_corners[,!(colnames(Palestino_corners) %in% c("equipo"))] 
Promedios_corners <- c("Promedio de Corners",mean(Palestino_corners$lostCorners),mean(Palestino_corners$wonCorners),mean(Palestino_corners$cornerTaken))
Palestino_corners <- rbind(Palestino_corners, Promedios_corners)

Max_Corners <- c("Max de Corners",max(Palestino_corners$lostCorners),max(Palestino_corners$wonCorners),max(Palestino_corners$cornerTaken))
Palestino_corners <- rbind(Palestino_corners, Max_Corners)

Min_corners <- c("Min corners",min(Palestino_corners$lostCorners),min(Palestino_corners$wonCorners),min(Palestino_corners$cornerTaken))
Palestino_corners <- rbind(Palestino_corners, Min_corners)
Palestino_corners
```

    ## # A tibble: 10 x 4
    ##    partido                       lostCorners      wonCorners     cornerTaken    
    ##    <chr>                         <chr>            <chr>          <chr>          
    ##  1 Palestino vs Deportivo Antof~ 1                5              5              
    ##  2 Santiago Wanderers vs Palest~ 2                2              2              
    ##  3 Colo Colo vs Palestino        2                2              2              
    ##  4 Audax Italiano vs Palestino   2                1              1              
    ##  5 Uni<f3>n Espa<f1>ola vs Pale~ 4                0              0              
    ##  6 Palestino vs Huachipato       3                0              0              
    ##  7 Palestino vs O'Higgins        5                0              0              
    ##  8 Promedio de Corners           2.71428571428571 1.42857142857~ 1.428571428571~
    ##  9 Max de Corners                5                5              5              
    ## 10 Min corners                   1                0              0

``` r
## Graficos

rendimiento_everton <- Palestino$goalAssist
Palestino2 <- Palestino[order(Palestino$goalAssist, decreasing = FALSE),]
dotchart(Palestino$goals, labels = Palestino$partido, cex=0.5, xlab = "goles", ylab = "Partido")
```

![](diego_herrera2_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
dotchart(Palestino$totalPass, labels = utf8_encode(Palestino$partido), cex=0.5, xlab = "pases", ylab = "Partido")
```

![](diego_herrera2_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->

``` r
dotchart(Palestino$accuratePass, labels = utf8_encode(Palestino$partido), cex=0.5, xlab = "pases", ylab = "Partido")
```

![](diego_herrera2_files/figure-gfm/unnamed-chunk-1-3.png)<!-- -->

``` r
dotchart(Palestino$goalsConceded, labels = utf8_encode(Palestino$partido), cex=0.5, xlab = "goles concedidos", ylab = "Partido")
```

![](diego_herrera2_files/figure-gfm/unnamed-chunk-1-4.png)<!-- -->

``` r
dotchart(Palestino$goalAssist, labels = utf8_encode(Palestino$partido), main="asistenicias", pch = 16, col=c("darkblue","dodgerblue"),lcolor="gray90", cex=0.8, xlab = "asistencias", ylab = "Partido", cex.main=2,cex.lab=1.5)
```

![](diego_herrera2_files/figure-gfm/unnamed-chunk-1-5.png)<!-- -->

``` r
## Analisis de Texto

texto <- primer_tiempo2020$partido
texto <- char_tolower(texto)
texto <- iconv(texto, to = "ASCII//TRANSLIT")
a <- dfm(texto, remove = c(stopwords("es"), "vs", "Universidad"))
```

    ## Warning: 'dfm.character()' is deprecated. Use 'tokens()' first.

    ## Warning: 'remove' is deprecated; use dfm_remove() instead

``` r
dim(a)
```

    ## [1] 130  31
