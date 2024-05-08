# Proyecto de Mentoria - FaMAF 2024

## Flujo Vehicular en la Ciudad de Córdoba

Proyecto de Ciencia de Datos para analizar el flujo vehicular en la Ciudad de
Córdoba con datos disponibles desde Agosto de 2019 a la actualidad (Marzo 2024),
obtenidos de la página de la [Analítica de Tráfico de la Municipalidad de
Córdoba](https://app.powerbi.com/view?r=eyJrIjoiMjg1YmRjODktZGRjOS00ODMxLWFiOTMtZTQzZDViZjNkMWE5IiwidCI6ImU4YjUzOTJiLWM1NmQtNGM4Ni1iNjU4LWJjYmFhNzM1ZDFjZCIsImMiOjR9)
correspondiente a la cámara ubicada de Bv. Chacabuco y Bv. Illia con orientación
hacia puente Maipú.

La carpeta contiene archivos `.json` con información del flujo vehicular. El
nombre de cada archivo se especifica de la siguiente forma:

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


Dentro de cada archivo `.json` las variables con datos relevantes son (cuidado
que vienen como vectores):

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
	    > D5: rango horario (vector, se descarga ordenado)


La salida para que se vea como se presenta en la web debería ser:

    Fecha, # vehículos, turno, activo, mark, diaSemana, periodo (año/mes), IntervaloSegmento

_mark_ no es relevante.
