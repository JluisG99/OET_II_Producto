# Introducción al Filtrado de Imágenes Sentinel-2 en Google Earth Engine 

###### **Por Jose Luis Gamboa Mora, Agosto del 2023**
En el ámbito de la teledetección y el análisis geoespacial, las imágenes satelitales Sentinel-2 proporcionan una valiosa fuente de información para monitorear y comprender los cambios en la superficie terrestre. Sin embargo, debido a factores atmosféricos, condiciones climáticas y otros artefactos, las imágenes capturadas por los sensores no
siempre son ideales para el análisis directo. Es aquí donde el filtrado de imágenes juega un papel crucial.  
### Google Earth Engine (GEE)
[![](https://developers.google.com/static/earth-engine/images/datasets/copernicus_s2_sr_1280_856.jpg)](https://developers.google.com/earth-engine/datasets/catalog/sentinel)  
Permite a sus usuarios filtrar y descargar imágenes desde su entorno virtual, a través de códigos programados en el lenguaje de programación [Java Script.](https://developer.mozilla.org/es/docs/Learn/JavaScript/First_steps/What_is_JavaScript)  

GEE permite acceder a distintos datasets como por ejemplo:  
- Climate and Weather
- Imagery
  - Landsat
  - Sentinel
- Geophysical

#### Productos de Sentinel 2 
[![](https://sentinel.esa.int/documents/247904/266422/Sentinel-2+Processing+Levels+Overview+%28up+to+L2A%29.png/d6743f9c-b43a-b6b0-4c4e-7d89b3f5e5e4?t=1677240675567)](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels)
El filtrado de imágenes *Sentinel-2  en Google Earth Engine (GEE)* nos brinda la capacidad de mejorar la calidad y utilidad de las imágenes adquiridas, permitiéndonos extraer información más precisa y coherente.  
Los niveles de procesamiento a los que se tiene acceso son:
- [Top of Atmosphere L1C](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_HARMONIZED)
- [Surface reflectance 2-L2A](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED)  
A través de técnicas y procesos específicos, podemos filtrar las imágenes según colección, área de interés, fecha e incluso se utilizan **parámetros atmosféricos** para seleccionar las imágenes más adecuadas para nuestro análisis. Las imágenes **Sentinel 2** deben pasar por una serie de procesos técnicos que mejoran la calidad del producto, al ejecutar esos procesos nuevos niveles se van creando. 
En esta presentación, exploraremos una metodología efectiva para filtrar y seleccionar imágenes Sentinel-2 en GEE, permitiendo a nuestro equipo técnico optimizar su flujo de trabajo y maximizar el valor de los datos disponibles.
