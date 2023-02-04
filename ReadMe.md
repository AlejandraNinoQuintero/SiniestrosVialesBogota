# Análisis de Siniestros Viales en Bogotá 2019
## Población de análisis: menores de edad – entre 0 y 17 años por localidades

#### Autora:  María Alejandra Niño Quintero
#### Métodos Computacionales para Políticas Públicas
#### Maestría en Economía de las Políticas Públicas
#### Universidad del Rosario

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Siniestros%202015-2020.png)

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Siniestros%20x%20localidad.png)

# Descripción y motivación:

Según cifras de la Secretaria de Movilidad de Bogotá entre 2015 y 2019 se presentaron en promedio 34 mil siniestros viales, lo que indica que cada 5 minutos ocurre un accidente en la ciudad (1). Esto representa un problema de salud pública para los gobiernos, pues según Fasecolda, en 2018 estos accidentes le costaron al Estado cerca de 3,6 billones de pesos (2). 
<br> Por otra parte, la Organización Mundial de la Salud indica que la principal causa de muerte entre los jóvenes de 15 a 29 años en el mundo se debe a los traumatismos por accidentes de tránsito (3).
<br>Teniendo en cuenta lo anterior, y las noticias recientes (4) (5) (6) donde se han reportado accidentes de tránsito en la ciudad. 
<br> En este estudio se analizó los datos existentes sobre siniestros viales en la ciudad con el objetivo de determinar aspectos importantes que permitan la toma de decisiones para reducir esta cifra en la ciudad. Este análisis se puede hacer por diferentes poblaciones. En el presente estudi se escogió la población de menores de edad entre 0 y 17 años. Sin embargo existen otras poblaciones que pueden presentar condiciones particulares como los ciclistas y los motociclistas, quienes también se ven involucrados en sinisestros viales.  

Algunas preguntas que motivaron el análisis hecho fueron: 

1. Los gobiernos tienen que pagar un alto costo por los siniestros viales que ocurren en la ciudad y en general en el país, por lo cual se implementan diferentes medidas como la disminución de velocidad en las principales vías, se invierte en señalización entre otros que también genran un gasto. Sabiendo que se han tomado medidas que buscan reducir los accidentes viales ¿Por qué las cifras siguen siendo tan altas? incluso en el 2020, un año en el que de marzo a septiembre Colombia estuvo en cuarentena por el COVID 19 y la movilidad y el desplazamiento se restringieron, los accidentes superan los 20mil sinisestros. 

2. Siendo la población jóven afectada por este problema al punto de representar su principal causa de muerte, ¿qué ocurre con los menores entre 0 y 17 años? ¿Dónde ocurren los accidentes donde esta población está involucrada en los accidentes?

3. ¿Existe algun patrón en la accidentalidad de los menores? ¿Qué tan cerca a los colegios y zonas residenciales o parques se dan? ¿Qué tan importante es la educación vial para disminuir la cifra de accidentes?

4. ¿Qué tan importante es la educación vial? ¿Cómo se puede evitar que los menores de edad sufran accidentes cuando se desplazan hacia el colegio o desde el colegio a sus viviendas?

5. Si bien la principal causa de muerte de jóvenes entre 15 y 29 años de edad son los siniestros ¿Qué pasa con aquellos que quedan heridos y a quienes este tipo de eventos puede alterar el desarrollo normal de sus vidas?

6. ¿Existe alguna diferencia en la accidnetalidad de menores según su género? 

# Metodología usada:

1. **EDA:** La data se descargó de Datos Abiertos de Bogotá, la cual estaba separada por siniestros, actores y vehículos. Por lo cual se requirió de un merge (proceso de unión de bases de datos) que permitiera relacionar el accidente y su información general con los accidentados y sus características. De igual manera era necesario hacer un merge con los tipos de vehículos. 
    - Dado este análisis exploratorio y la cantidad de siniestros ocurridos entre 2015 y 2020 (aproximadamente más de 600 mil) y que la tendencia ha sido muy similar desde 2015 en cuanto al número de accidentes se decide analizar el 2019 (no el 2020 debido a las medidas de distanciamiento social que restringieron la movilidad). 
    - Se filtra de manera tal que la base quede con toda la información para 2019 y para la población de estudio del análisis y por localidades de la ciudad. 
    - La información de los siniestros se descargaron de Datos Abierto de Bogotá con la geolocalización de las direcciones de los accidentes lo cual permitió hacer un análisis geoespacial de los datos completos para menores de edad en 2019 (al rededor de 1900 siniestros)
    - Se realizó en Pyhton.
<br>

2. **Análisis Geoespacial:** 
    - Una vez se obtuvo la data organziada se realizó un análisis geoespacial en Qgis versión 3.20.3
    - El análisis se realizó en este orden:
        - Población de Bogotá (Secretaría Distrital de Planeación (7)) vs Accidentalidad total por localidad. De manera tal que se pueda evidenciar si hay mayor accidentalidad en localidades con más población (sería lo esperado) o si existe alguna localidad donde a pensar de tener menor población tuvo una alta accidentalidad. 
        - Población de menores (proyección para 2019 - Secretaría Distrital de Planeación (8)) para hacer una comparación similar a la anterior pero para la población objetivo de este estudio. 
        - Concentración de accidentes: mapa de calor con los accidentes viales de menores geocodificados de la base manipulada en Python.
        - Con el análisis anterior se pueden identificar las localidades con mayor accidentalidad de menores, así como concentración de zonas. Por lo cual para estas localidades se ubican los colegios (SDP (9)) y se realizan áreas de influencia de estos colegios a 100 y 200 metros para identificar cuantos accidentes ocurren es este rango. 
        - Estas áreas de influencia se hacen mediante buffer, para una mejor visualización se aplicó la opción de disolver - los buffer se convierten en nuevas capas en polígono. 
        - Para calcular el número de accidentes en las áreas de influencia, los buffer tienen la opción de generar para cada buffer la intersección, creando capas transitorias (no se pueden guardar) con el sub grupo de accidentes que cumplen la condición. 
<br>    

3. **Análisis gráfico:**
    - Se realizó en Tableau
    - Se realizó con el objetivo de complementar el análisis geoespacial, para poder concluir si la cercanía de los accidentes a los colegios tiene una relación, es necesario consederar temas como las horas en las que se dan los accidentes, la condición de los menores como peatones entre otras características. 
    - Se incluyó el género para revisar si hay alguna diferencia. 

# Resultados: 

1. A pesar de diferentes políticas como la reducción de velocidad en las principales vías Bogotá, se mantiene una alta accidentalidad desde 2015.
2. Los accidentes que involucran menores de edad en 2019 se concentran principalmente en las localidades de Kennedy, Ciudad Bolívar, Bosa, Suba y Engativá – las cuales a su vez tienen la mayor población de menores. 
3. En promedio el 33.7% de los accidentes de menores ocurren a 100 metros de colegios y el 63.2% a 200 metros de colegios en las localidades mencionadas. En bogotá una cuadra tiene en prmedio 100 metros, por lo cual esta concentración de accidentes se está presnetando a una o dos cuadras de los colegios.
4. Los menores accidentados son principalmente peatones o pasajeros. 
5. Se evidencia una concentración de accidentes en la mayoría de localidades en horarios comprendidos entre la 12pm y las 7pm. 
6. En 15 de las 20 localidades más del 50% de los accidentados son de genero masculino.

## Población Bogotá 2019

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Poblacion2019.png)

## Accidentalidad Total Bogotá 2019

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/AccidentalidadTotal2019.png)

## Población Menores Bogotá 2019

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/PoblacionMenores2019.png)

## Accidentalidad Menores Bogotá 2019

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/3c578267a719df7841feafdbe809fbbd5ac3d133/Archivos%20para%20README/AccidentalidadMenores2019.png)

## Concentración Accidentes Menores 2019

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/ConcentracionAcc2019.png)

## Áreas de Influencia

### Kennedy

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Kennedy.png)

### Bosa

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Bosa.png)

### Ciudad Bolivar

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/CiudadBolivar.png)

### Engativá

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Engativa.png)

### Suba

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Suba.png)

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Condicion.png)

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Gravedad.png)

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/Horas.png)

![Image text](https://github.com/AlejandraNinoQuintero/SiniestrosVialesBogota/blob/main/Archivos%20para%20README/genero.png)

#### Nota: Todas las gráficas y mapas son de elaboración propia

#### Link bases usadas: https://drive.google.com/drive/folders/1Mz7GfP7hHgp0EyCB4wO9ScJs01xixigz?usp=sharing 

# Referencias: 
(1) https://www.eltiempo.com/datos/cifras-de-accidentes-y-muertes-por-accidentes-de-transito-en-bogota-578915#:~:text=Las%20cifras%20de%20la%20Secretar%C3%ADa,fue%202015%2C%20con%2031.341%20casos.
<br>(2) https://www.portafolio.co/economia/accidentes-de-transito-cuestan-3-6-billones-a-la-seguridad-social-521678
<br>(3) https://www.who.int/es/news/item/16-05-2017-more-than-1-2-million-adolescents-die-every-year-nearly-all-preventable
<br>(4) https://www.eltiempo.com/bogota/siniestros-viales-en-bogota-empeoraron-en-2021-omar-orostegui-609390
<br>(5) https://www.youtube.com/watch?v=T8z9dNT8MEw
<br>(6) https://noticias.caracoltv.com/bogota/motociclista-murio-arrollado-por-culpa-de-un-hueco-en-vez-de-ayudarlo-lo-robaron-al-verlo-herido 
<br>(7)https://sdpbogota.maps.arcgis.com/apps/MapSeries/index.html?appid=baabe888c3ab42c6bb3d10d4eaa993c5
<br>(8)http://www.sdp.gov.co/sites/default/files/boletin69.pdf 
<br>(9)Secretaría Distrital de Planeación 2021 
