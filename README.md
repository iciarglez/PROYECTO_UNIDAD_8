# PROYECTO_UNIDAD_8
Proyecto de la unidad 8. EDA en Python

## Descripción del proyecto

En este proyecto se aplican los conocimientos aprendidos hasta el momento. En este proyecto se realiza un análisis exploratorio de datos (EDA) sobre una campaña de marketing de una entidad bancaria portuguesa, utilizando Python y las principales librerías para análisis de datos.


En el repositorio constan:

- Archivo README.md, que recoge los pasos seguidos durante el proyecto y el informe del análisis.
- Una carpeta de datos donde se encuentran los archivos en bruto (raw), asociados a este proyecto, y los datos guardados después de las transformaciones (processed).
- Una carpeta con el notebook donde se han realizado todos los pasos del proyecto.
- Una carpeta de imágenes donde se han guardado los resultados de los gráficos procesados en el notebook.


## Tecnologías utilizadas

- El análisis EDA se ha llevado a cabo en código Python 3.13.15, en un documento Jupyter Notebook.
- Se han utilizado librerías como Pandas, NumPy, Matplotlib, Seaborn.
- Visual Studio Code ha sido el visor utilizado para el desarrollo.
- Los ficheros del proyecto se entregan en GitHub.


## Requisitos

- Transformación y limpieza de los datos.
- Uso de los conceptos cubiertos en los módulos de “Python” y “Python for data”.
- Análisis descriptivo de los datos.
- Uso eficiente de pandas.
- Optimización del código en Python.
- Visualización de los datos.
- Informe explicativo del análisis.
- Readme del proyecto.



## Pasos del proyecto

### Datos

Los datos con los que vamos a trabajar están relacionados con campañas de marketing directo de una institución bancaria portuguesa. Las campañas de marketing se basaron en llamadas telefónicas. A menudo, se requería más de un contacto con el mismo cliente para determinar si el producto (depósito a plazo bancario) sería suscrito o no. Además, tenemos información sobre las características demográficas y comportamiento de compra de los clientes del banco.

Contamos con dos datasets: 
    - bank-additional.csv
    - customer-details.xlsx



### Limpieza de datos

Se lleva a cabo una limpieza de los dos ficheros de datos, para terminar unificándolos en un único fichero.

La limpieza de datos consiste en:
- Exploración inicial de los dos ficheros de datos.
Aunque la documentación proporcionada indicaba la existencia de las variables contact_month y contact_year, el conjunto de datos utilizado contiene las variables latitude y longitude, que corresponden a coordenadas geográficas. Se mantuvieron estas columnas respetando el contenido real del dataset.
- Tratamiento de duplicados. Como en los ficheros no hay, no tenemos que hacer ninguna modificación.
- Tratamiento de los valores nulos. Se observa que, mientras el fichero de clientes no tiene valores nulos, el fichero de banca sí. Las variables con valores nulos se analizaron individualmente. Las variables categóricas se completaron con la categoría "Unknown" y las variables numéricas se mantuvieron como valores faltantes (NaN) cuando su imputación podía alterar el análisis.
- Antes de tratar los valores nulos de las variables, se procede a corregir los tipos de datos:
    - Eliminar la columna Unnamed de ambos conjuntos de datos, ya que es igual que el índice.
    - Pasar las variables "default", "housing" y "loan" a variables categóricas (1: "Sí", 0: "No").
    - Convertir las variables numéricas "cons.price.idx", "cons.conf.idx", "euribor3m" y "nr.employed" a float, ya que están almacenadas como texto.
    - Corregir el tipo de variable de "date" para que tenga un formato de fecha.

Se guardan estas modificaciones en dos nuevos ficheros de datos, "bank_clean" y "customer_clean". En el código se guardan tanto en .csv como en .xlsx. De cara a la entrega, solo se subirán los datos en .xlsx.



### Unificación de los ficheros

En ambos ficheros hay una variable de id que podría permitir la unión. Antes de hacer el merge se comprueba que la columna identificadora es compatible.

Después de hacer el merge se comprueba que el número de filas y de columnas es correcto.



### Análisis descriptivo

El objetivo del análisis descriptivo llevado a cabo es conocer el dataset antes de buscar relaciones.
A continuación, se describen las variables numéricas y categóricas.

- Se observa que la media de edad es de 39,9 años y la mediana 38 años.
- El número medio de contactos realizados es 2.56, con una mediana de 2. Sorprende un valor máximo de 56 contactos.
La mayoría de los clientes fueron contactados entre una y pocas veces durante la campaña. Sin embargo, existen algunos casos aislados con un número muy elevado de contactos, lo que genera una distribución asimétrica hacia la derecha y posibles valores atípicos.
- La duración tiene una media de 257,74 segundos, esto es, en torno a 4 minutos 18 seg. La mediana está en 179 seg, esto es, 3 minutos.
- La media de los salarios es 93.241,2 €, muy próxima a la mediana 93.050,5 €, lo que sugiere una distribución aproximadamente simétrica. Los ingresos muestran una elevada variabilidad (desviación estándar de 50.498 €), reflejando la diversidad económica de los clientes incluidos en el estudio.
- Las visitas mensuales del cliente al sitio web de la empresa son, de media, 16,6. El mínimo es 1 visita y el máximo, 32. La mediana está en 25 visitas mensuales, con una desviación de 9,2.
- Hay 12 tipos de empleo, siendo el más común admin. Por otra parte, hay 8 niveles de educación, siendo el más común university.degree.
- Predomina el estado civil casado.
- En cuanto a pagos y préstamos, la mayoría no tiene historial de incumplimiento (de hecho, solo 3 tienen incumplimiento, frente a 34.016 que no incumplen y 8.961 valores ausentes), sí tiene préstamo hipotecario y no tiene otro tipo de préstamo.
- Además, el cliente mayoritariamente no se suscribe a ningún servicio (solo un 11,27% está suscrito).


### Análisis bivariante y correlaciones. Principales visualizaciones

No se comentan todos los gráficos ni todas las tablas, solo los resultados que se consideran más relevantes.

Antes de realizar un análisis de la relación entre las variables vamos a crear tres nuevas variables:
- Grupos de edad ("age_group")
- Hijos, suma "Kidhome" y "Teenhome" ("children")
- Préstamos, une "housing" y "loan" ("has_loan")


Con respecto a la relación de las variables con la contratación:
- Por grupos de edad, diferencias en la tabla de porcentajes. Hay más contrataciones en los grupos de edad 15-25, 25-35, 55-65, 65+.
- No hay diferencias en función de los hijos o de los préstamos. En particular, se analiza la nueva variable de préstamos y "housing" y "loan" por separado, por su hubiera alguna diferencia en función del tipo de préstamos. No la hay.
- No hay diferencias en función del ingreso.
- Diferencias significativas en función de la duración de las llamadas. Se observa en el gráfico de densidad y en los datos numéricos en la tabla por grupos. 
- En la tabla de porcentajes de empleo y educación también se observan diferencias: 
    - hay mayor contratación en los empleos "admin.", "management", "retired", "self-employed", "student", "technician" y "unemployed".
    - hay mayor contratación en aquellos con educación "basic.4y", "high.school", "illiterate", "professional.course" y "university.degree".
- No se observan diferencias en función del número de visitas por mes.
- Se observan diferencias por el contacto previo (si ha habido contacto, la contratación es mayor) y en el número de contactos durante la campaña (mayor porcentaje de contratación en el rango 1-4 contactos; esto es, los clientes que contrataron el depósito suelen haber necesitado un menor número de contactos durante la campaña.).


Aunque no sea el objetivo principal de nuestro estudio, el pairplot permite observar que no existen relaciones lineales fuertes entre las principales variables numéricas analizadas. En general, las observaciones correspondientes a clientes que contrataron y no contrataron el depósito presentan un elevado solapamiento, lo que indica que ninguna variable por sí sola permite diferenciar claramente ambos grupos. La duración de la llamada es la variable que muestra una mayor separación visual entre ambas categorías, en línea con el análisis bivariante realizado previamente.

Por otra parte, analizando la correlación entre las variables numéricas, las variables macroeconómicas (euribor3m, emp.var.rate y nr.employed) presentan una fuerte correlación entre sí, lo que es coherente al describir indicadores relacionados con la situación económica. En cambio, variables como la edad, los ingresos o el número de contactos muestran correlaciones débiles con el resto, lo que sugiere que aportan información complementaria.


### Conclusiones

En base al análisis que se ha llevado a cabo, se pueden responder algunas cuestiones acerca del perfil de los contratantes.

•	¿Qué perfil de cliente contrata más depósitos? (edad, profesión, educación)

Teniendo en cuenta los porcentajes comentados previamente y los totales, el grupo de edad en el que predomina la contratación es 25-35 años, y en segundo lugar, 55-65 años. A nivel laboral, destacan aquellos con perfil administrativo y técnico, y a nivel educativo, con grado universitario y high school.


•	¿Influye la duración de la llamada?

Sí, hay diferencias significativas en función de la duración de la llamada. Aquellos que sí contratan tienen una duración de llamadas mayor que los que no. Una media de 551 segundos en los que sí, frente a los 220 en los que no (medianas 449 y 278 respectivamente).


•	¿Los clientes con mayores ingresos aceptan más?

No hay relación significativa entre los ingresos y las contrataciones.


•	¿Los clientes con hijos aceptan menos?

No hay relación significativa entre el número de hijos y las contrataciones.


•	¿Los clientes antiguos responden mejor?

Con este análisis, futuras campañas podrían priorizar perfiles de clientes con estas características: rangos de edad 25-35 y 55-65, con trabajos administrativos o técnicos y con grado universitario o al menos high school. Además, no son necesarios muchos contactos y habrá mayor éxito de contratación en aquellos clientes que han sido contactados antes de esta campaña.


En estas conclusiones hay que tener en cuenta que el análisis es exclusivamente exploratorio y no permite establecer relaciones de causalidad. Además, algunas variables presentan valores faltantes. Por último, La duración de la llamada es una variable conocida una vez realizada la llamada, por lo que no puede utilizarse para seleccionar previamente a qué clientes contactar.


