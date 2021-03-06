﻿# Contenido
- Introducción
- Objetivo
- Fuentes de datos
- Diccionario de datos
- Datos de envíos
- Datos de llamadas
- Instrucciones para replicar proyecto
- Librerías y Requerimientos
- Ejecución de Notebooks

# Predicción número de llamadas en un servicio de Contact Center

## Introducción
Las empresas de mensajería tienen un gran volumen de llamadas telefónicas, se podría decir que el 90% de los envíos que se realizan por particulares son a través de una llamada telefónica.

La empresa Angel24 SL, dispone de un departamento de Contact Center, donde se presta servicio a empresas de toda índole. 

Uno de los clientes del departamento de Contact center es un grupo de agencias de mensajería de una conocida marca de transporte urgente que opera a nivel nacional. 

En esta campaña de atención telefónica se reciben llamadas de varios tipos:

- Solicitar un envío
- Solicitar información sobre agencias
- Solicitar información sobre el estado de un envío

El porcentaje de llamadas que hacen referencia al tercer punto, *‘Solicitar información sobre el estado de un envío’*, es bastante alto, y tiene relación con la cantidad de envíos que llegan a las oficinas, para posteriormente ser entregados.
## Objetivo
Predecir la cantidad de llamadas que recibirá “mañana” esta campaña, aplicando mecanismos de Data Science, con el objetivo de ser proactivos en cuanto a la configuración del equipo de teleoperadores asignados a ésta. Con el fin de mejorar el nivel de servicio prestado y el rendimiento económico, maximizando la productividad de los teleoperadores.

## Fuentes de datos
Para realizar este estudio tenemos dos fuentes de datos. 

- Los envíos que llegan a las diferentes oficinas de transporte, que nos facilita el sistema informático de la marca a través de sus listados en Excel. 
- El histórico de llamadas de esa campaña desde el propio departamento de Contact center.
## Diccionario de datos
### Datos de envíos
Los datos referentes a los envíos de las oficinas de transporte son:

1. Fecha envío = Fecha creación de envío
1. Número envío = Identificador del envío
1. Id. Fiscal = identificación fiscal cliente
1. Nombre Comercial = Nombre del cliente
1. Código servicio = Tipo de servicio, este está vinculado con las horas en las que tendrá que ser repartido
1. Nombre Rem = Nombre remitente a la atención de
1. Población Rem = población remitente
1. CP Rem = CP remitente
1. Nombre vía Rem = Nombre domicilio remitente
1. Nombre = Nombre del cliente destino
1. Población = población destino
1. Código postal = Código postal destino
1. Nombre vía = Nombre domicilio cliente destino
1. Total bultos = Numero de bultos en el envío
1. Franquicia origen = Desde que oficina se envía el/los paquetes
1. Franquicia destino = A que oficina se envía el/los paquetes
1. Total = Importe envío
1. Estado = Situación del envío
1. Tipo anomalía = Incidencias en el envió
1. Motivo = Motivo del estado del envió
1. Importe Total = Importe total con gastos extras

De los cuales en este estudio vamos a trabajar únicamente con:

1. Fecha envío
1. Código servicio
1. Franquicia
### Datos de llamadas
Los datos referentes a las llamadas telefónicas que recibe el contact center son:

1. IDCAMPANYA = Codigo de la oficina de transpote a la pertenece la llamada
1. IDSUJETO = Numero de telefono que efectua la llamada
1. VALOR = El motivo de la llamada
1. DATACREACIO = Fecha de la llamada

El único dato que no vamos a utilizar es el número de teléfono 
## Instrucciones para replicar proyecto
### Librerías y Requerimientos
El proyecto se ha realizado en un entorno virtual de Python 3.9.5, el proyecto funciona igualmente en Windows como en UNIX, las principales librerías utilizadas son:

- numpy==1.19.5
- pandas==1.2.4
- pmdarima==1.8.2
- scikit-learn==0.24.2
- seaborn==0.11.1
- sklearn==0.0
- statsmodels==0.12.2
- streamlit==0.83.0

Con sus correspondientes dependencias. 

En el repositorio existe un fichero llamado “Requerimientos.txt” extraído del comando pip freeze, para poder realizar la instalación de todos los paquetes con sus correspondientes versiones y de esta forma, replicar el entorno de desarrollo. (pip install -r Requerimientos.txt)

Para ejecutar el dashBoard.py de streamlit, será necesario tener el “Microsoft® ODBC Driver 17 for SQL Server” descargable desde la página de Microsoft, [enlace](https://www.microsoft.com/es-es/download/details.aspx?id=56567) y la contraseña de la conexión, ya que una de las fuentes de datos se consulta en una Base de Datos SQL en Azure.
### Ejecución de Notebooks
El repositorio cuenta con los siguientes notebooks:

- 1\_CargaDataEnvios.ipynb
- 2\_CargaDataCall.ipynb
- 3\_AnalisisData.ipynb
- 4\_Model.ipynb
- 5\_DashBoard_TFM.ipynb

Cada notebook, en su nombre, tiene un número que indica su orden para procesarlos. En la raiz de los notebooks debe existir una carpeta data, donde estaran los ficheros de datos (los datos no son públicos, no se adjuntan en el repo).

En este repositorio también encontramos 2 librerias .py:
- functionsTFM.py, donde se encuentran funciones de usuario para no tener el codigo sucio
- SessionState.py, una librería para poder trabajar con la cache de navegador en Streamlit 

Y por supesto el fichero .py donde se ejecuta el cuadro de mando de Streamlit
- dashBoard.py

Para ejecutar el dashboard, se realizará de la siguiente forma: 
streamlit run dashBoard.py


### Manual para cuadro de mando
El cuadro de mando es una webApp donde, cargando los ficheros de los envios que se van a recibir en las oficinas, se 
realiza una prediccion de la cantidad de llamadas que se va a recibir en el departamento de Contact Center.

La disposición del cuadro de mando es de la siguiente manera:
![imagen](images/dashboard.JPG)

Tenemos un panel lateral donde se podran subir los ficheros con los datos de los envios (No se adjuntan en el repo)

![imagen](images/barra.JPG)

En la parte central tenemos informacion de las distribuciones de los envios y de las llamadas de nuestro set de datos, para los que
está entrenado el modelo

![imagen](images/panel_info.JPG)

Una vez cargado los ficheros de los envíos, el propio dashboard hace una llamada SQL (los datos de conexión SQL no se proporcionan en el repo) 
para la carga de los datos de las llamadas, y tras el procesamiento de la información, hace la predicción de llamadas para 
el día en el cual se han cargado los datos.

![imagen](images/panel_predict.JPG)
