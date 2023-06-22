# **Trabajo final HdE**

Los rizobios son bacterias con la capacidad de fijar N<sub>2</sub> como amonio cuando están asociados simbióticamente con raíces de plantas leguminosas. Si bien la fijación de nitrógeno se produce en estructuras radiculares especializadas (nódulos fijadores de nitrógeno), estas bacterias también tienen una etapa de vida libre en la que se hallan en mayor concentración en la rizósfera, definida como el volumen de suelo afectado directamente por las raíces de las plantas.

Para este trabajo se utilizan datos de 2 ensayos en los que se evalua la competencia por la colonización de la rizosfera de *Medicago sativa* por mutantes de *Sinorhizobium meliloti*. 

Estos mutantes fueron generados mediante la tecnología de mutagénesis etiquetada por firmas (STM, *Signature Tagged Mutagenesis*), por lo que cada uno lleva una marca genética que permite identificarlo y cuantificarlo en ensayos realizados con mezclas de mutantes, mediante el uso de técnicas de secuenciación masiva.


## **1. Análisis estadístico de datos categóricos**

En este caso se utilizó una tabla que cuenta con resultados de ensayos de competencia por la colonización rizosférica en la que se inocularon macetas de alfalfa con *pooles* de mutantes. Para cada uno de los mutantes (columna 'mutant_ID') se registran dos valores M que hacen referencia a la diferencia en la respresentación de cada una de las dos firmas genéticas (obtenida por secuenciamiento de las dos etiquetas presentes en cada mutante) en la mezcla de mutantes en el inóculo y en la mezcla obtenida al final del ensayo. Cada uno de estos valores M (columnas '7dpiAlfL_KValor M' y '7dpiAlfL_HValor M') está asociado a un p-value (columnas '7dpiAlfL_Kt-test' y '7dpiAlfL_Ht-test') y la columna 'contig' contiene la porcion del genoma en la que está ubicada la inserción del transposon.

Con el fin de determinar si exixte una relación entre la ubicación de la mutación (cromosoma(3,65Mpb), plásmidos pSymA(1,35Mpb) o pSymB(1,68Mpb)) y el efecto en la competencia, se clasificaron los mutantes en dos categorías, los afectados negativamente ('negativo'), aquellos que presentaron valores M<-0,7 y un p-value < 0,1 tanto en la firma K como en la firma H (exigencia de consistencia en el resultado observado desde ambas firmas), y 'no_negativo' a aquellos que no cumplen esta condición.

Para esto se plantea la hipóstesis nula: No existe una relación entre la ubicación de la mutación en el genoma y el efecto en la competencia de los mutantes. Luego se realiza un test para probar esta hipótesis.

### **Frecuencia de distribución de las dos variables (localización y efecto en competencia)**
\
![](./figuras/distribucion_inserciones_genoma.jpg "Frecuencia de distribucion de localización de inserciones en el genoma")
![](./figuras/distribucion_mutantes_afectados_negativamente.jpg "Frecuencia de distribucion de condición frente a ensayo de competencia")

Para determinar si la ubicación de las mutaciones tiene una relación con el efecto que genera en la competencia, se realizó una tabla de contingencia en la que se compara el número de mutantes afectado en colonización en relación a la ubicación en el genoma de la inseción del transposón.

|contig | afectado    |    |
| ------------- |------------| -----:|
|Plásmidos |No negativo    |   2407|
|      |Negativo     |     22|
|Cromosoma  |  No negativo    |   2380|
|      |  Negativo     |    150|

Luego se realizó un test de Chi cuadrado para evaluar la hipótesis, ya que se busca determinar la dependencia de dos variables discretas. Esto que dió como resultado los siguientes valores.

|statistic | pvalue |
|:-------------:|:-------------:|
|4301.76    |   0.0|

Esto podría indicar un mayor número de genes en el cromosoma que cumplen una función importante en la competencia en relación al número total de genes que pueden ser afectado sin generar una deficiencia vital en el crecimiento de la bacteria.

Teniendo en cuenta que se conoce que el plásmido pSymA no cumple una función fundamental en el desarrollo de la simbiosis, la tabla fue filtrada para contemplar solo los mutantes afectados en el cromosoma y en el plámido pSymB.

|contig | afectado    |    |
| ------------- |------------| -----:|
|pSymB |No negativo    |   1403|
|      |Negativo     |     19|
|Cromosoma  |  No negativo    |   2380|
|      |  Negativo     |    150|

Evaluando estos datos con un test de Chi cuadrado se obtuvieron los siguientes resultados

|statistic | pvalue |
|:-------------:|:-------------:|
|3796.65    |   0.0|


Lo que permite inferir que las inserciones cromosomales tienen una mayor probabilidad de generan mutantes viables con relevancia en la competencia respecto a las localizadas en el plásmido pSymB.
