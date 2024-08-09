# Proyecto de Mentoria - FaMAF 2024

## Predicción del tránsito en la Ciudad de Córdoba, aportes para la construcción de un mapa de ruido


### Descripción y objetivos del proyecto

Los mapas de ruidos son herramientan con que cuentan los municipios para planificar y monitorear el crecimiento de las ciudades. 
La construcción de estos mapas depende de la disponibilidad de datos, entre algunos de los más importantes podemos mencionar los obtenidos de las estaciones de monitoreo, simulaciones numéricas y de colaboración abiertas de la ciudadanía (crowdsourcing), entre otras.
Para las simulaciones numéricas, la principal fuente de generación de ruido se corresponde con el tránsito vehicular y factores asociados al mismo.

El objetivo de este proyecto es la construcción de un modelo predictivo y de
clasificación del tránsito y caracterización de calles de la ciudad de Córdoba,
ambos dependientes del tiempo como principal variable. El modelado se realizará
a través de modelos de Aprendizaje Supervisado/no Supervisado principalmente.

El trabajo propuesto busca relacionar y vincular el dataset con datos sobre el clima, paros de transporte, marchas, restricción vehicular por situaciones eventuales u ordenanza municipal, etc. y ver su efecto en el flujo del tránsito. 

Si bien no será parte del presente proyecto, los resultados serán de utilidad para alimentar un modelo de mapa de ruido para la Ciudad de Córdoba.

El proyecto busca responder las siguientes preguntas:

- ¿Cómo se comporta el flujo vehicular en las principales avenidas de la Ciudad
  de Córdoba?
- ¿Cómo varía el flujo vehicular durante los distintos días de la semana y
  horarios?
- ¿El flujo vehicular presenta características estacionales?
- ¿Cómo afecto la pandemia al tránsito?
- ¿Qué otros factores se pueden identificar que afecten al flujo vehicular?


En este __Proyecto de Ciencia de Datos__ se analizará el flujo vehicular en la
Ciudad de Córdoba con datos disponibles desde Agosto de 2019 a la actualidad
(Marzo 2024), obtenidos de la página de la [Analítica de Tráfico de la
Municipalidad de
Córdoba](https://app.powerbi.com/view?r=eyJrIjoiMjg1YmRjODktZGRjOS00ODMxLWFiOTMtZTQzZDViZjNkMWE5IiwidCI6ImU4YjUzOTJiLWM1NmQtNGM4Ni1iNjU4LWJjYmFhNzM1ZDFjZCIsImMiOjR9)
correspondiente a la cámara ubicada en Bv. Chacabuco y Bv. Illia con orientación
hacia puente Maipú.

La carpeta con los datos contiene archivos `.json` con información del flujo
vehicular. El nombre de cada archivo se especifica de la siguiente forma:

> _año_._mes_._it_.json

Donde _it_ es el _indicador de turno_, puede tomar los siguientes valores y se
corresponde con el siguiente _turno_ y _rango horario_:

 _it_ | _turno_ | _rango horario_
-------|:-:|:------:
 0 | MADRUGADA | de 0 a 6 h
 1 | MAÑANA | de 6 a 12 h
 2 | SIESTA | de 12 a 16 h
 3 | TARDE | de 16 a 21 h
 4 | NOCHE | de 21 a 24 h


Dentro de cada archivo `.json` las variables con datos, en principio relevantes,
son (tener cuidado que se presentan como listas/vectores):

	results[0] > resutl > data > dsr -> DS[0]: toda la info relevante

	  > PH[0] > DM0[#] > C: datos de vehículos para cada columna (0 hasta el valor final)
				   vector [día-1, cantidad, día de semana según cuando comienza]
					Ver el significado del resto de datos 
	  > ValueDicts 
	    > D0: fechas (vector)
	    > D1: turno (vector)
	    > D2: va la cantidad de vehículos sacada de DM0 (vector vacío) 
	    > D3: día de la semana, se corresponde con el tercer elemento de C en DM0 comenzando por el primer día en el mes (vector)
	    > D4: fecha (año/mes, vector)
	    > D5: rango horario (vector, se encuentra ordenado temporalmente)


La salida para que se vea como se presenta en la web debería ser:

    Fecha, # vehículos, turno, activo, mark, diaSemana, periodo (año/mes), IntervaloSegmento

<!---
_mark_ no es relevante.
--->
---


### Hitos de la Mentoria

#### Práctico Nº1 - Análisis y visualización

> Entrega: 1/7

Durante la primera etapa se busca familiarizarse con el conjunto de datos
(_dataset_) y aprender a administrar/trabajar con datos en formato `json`. Luego
de unificar los datos en un único _dataset_, se analizarán los mismos, tanto en
cantidad y como en calidad.  Se indagará no sólo el tipo de cada dato sino su
naturaleza, su evolución y agrupación temporal principalmente.

Se utilizarán visualizaciones y herramientas estadísticas para facilitar
encontrar correlación entre las variables. Los gráficos de las distribuciones de
los datos, los estadísticos necesarios utilizados para caracterizar las
distintas variables e identificar los valores atípicos (_outliers_) o datos
faltantes serán el resultado de estos análisis.	

Por último, se identificará la variable objetivo (_target_) que será aquella a
predecir.


#### Práctico Nº2 - Análisis exploratorio y curación de datos

> Entrega: 29/7

El análisis exploratorio de los datos nos permitirá haber identificado valores
faltantes y tomar acciones sobre ellos. ¿Estos datos serán suprimidos del
_dataset_?, si no se eliminan, ¿serán imputados? ¿de qué forma y con qué
criterio?. ¿Existen datos duplicados en el _dataset_?
El análisis de los _outliers_ es encesario para comprender si realmente son
atípicos o son casos excepcionales que deben tenerse en cuenta. ¿Qué porcentaje
representan? ¿Los datos serán eliminamos o se mantiene cierto porcentaje de ellos y con qué criterio?

La inspección de las variables disponibles nos permitirá responder: ¿todos los
datos son relevantes para el problema o podemos prescindir de algunos? ¿Será
necesario incorporar otros datos para una mejor comprensión del problema? ¿Será
posible clasificar el flujo vehicular a grandes rasgos? El estudio de estas
preguntas posibilitará generar nuevas variables y/o incorporar variables
externas al _dataset_.

Por último se deben aplicar transformación sobre los datos existentes, como 
`normalización`, `estandarización`, `encoding numérico` sobre variables
categóricas, etc., para dejar el _dataset_ en condiciones para su modelado.

#### Vídeo de presentación intermedia del proyecto y del _dataset_

> Entrega: 12/8


#### Práctico Nº3 - Aprendizaje supervisado/no supervisado

> Entrega: 16/9

Durante la etapa final se analizará qué tipo de problema de aprendizaje
supervisado/no supervisado se desea atacar. ¿Será un problema de regresión, de
clasificación o de agrupamiento (_clustering_)? Si es clasificación, ¿será
clasificación binario o multiclase? O quizás se corresponda con un problema
mixto, que requiera tanto de regresión como clasificación y/o agrupamiento. Esto
permitirá pensar qué tipos de modelos son adecuados para la predicción.

Con el _dataset_ **"limpio"**, se comenzará con la etapa de preprocesamiento, en
la que se prepararan los datos para ser insertados a los distintos modelos.
Primero se generá un modelo simple de base (_baseline_), que servirá de punto de
partida y comparación con otros modelos más complejos a implementar a
continuación.
Luego se analizará qué métricas son apropiadas para el problema/los problemas
(Accuracy, F1-Score, Recall, Precision, etc.) y se trabajará en optimizar las
mismas.
Se realizarán ajuste por hiperparámetros en diferentes modelos para obtener los
mejores resultados según los criterios establecidos.

Estos análisis permitiran seleccionar los mejores modelos y poder realizar
predicciones en una posible puesta en producción.


#### Vídeo de presentación final de mentoría

> Entrega: 30/9


#### Jornadas de presentación de mentorías

> 15 y 16 de noviembre

