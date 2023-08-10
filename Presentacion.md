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

### Productos de Sentinel 2 
[![](https://sentinel.esa.int/documents/247904/266422/Sentinel-2+Processing+Levels+Overview+%28up+to+L2A%29.png/d6743f9c-b43a-b6b0-4c4e-7d89b3f5e5e4?t=1677240675567)](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels)
El filtrado de imágenes *Sentinel-2  en Google Earth Engine (GEE)* nos brinda la capacidad de mejorar la calidad y utilidad de las imágenes adquiridas, permitiéndonos extraer información más precisa y coherente.  
Los niveles de procesamiento a los que se tiene acceso son:
- [Top of Atmosphere L1C](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_HARMONIZED)
- [Surface reflectance 2-L2A](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED)  
A través de técnicas y procesos específicos, podemos filtrar las imágenes según colección, área de interés, fecha e incluso se utilizan **parámetros atmosféricos** para seleccionar las imágenes más adecuadas para nuestro análisis. Las imágenes **Sentinel 2** deben pasar por una serie de procesos técnicos que mejoran la calidad del producto, al ejecutar esos procesos nuevos niveles se van creando. 
En esta presentación, exploraremos una metodología efectiva para filtrar y seleccionar imágenes Sentinel-2 en GEE, permitiendo a nuestro equipo técnico optimizar su flujo de trabajo y maximizar el valor de los datos disponibles.

## Hay tres etapas de filtrado:
### Filtrado
```// Agregar la variable ROI o Area de Interes... Se debe subir a GEE.

// Acceder a la coleccion de imagenes Sentinel 2-L1C
var sentinel2A = ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED")

// Aplicar los filtros oportunos:
var ROI1_2021 = sentinel2A.filterBounds(ROI1)
           .filterDate('2021-01-01','2021-12-31')
           .filterMetadata('CLOUDY_PIXEL_PERCENTAGE', 'less_than', 30)
           

// Obtener la lista de imágenes de la colección filtrada
var imageList = ROI1_2021.toList(ROI1_2021.size());

// Iterar sobre la lista de imágenes y obtener el ID de cada imagen
for (var i = 0; i < imageList.length().getInfo(); i++) {
  var image = ee.Image(imageList.get(i));
  var id = image.id().getInfo();
  print('ID de la imagen ' + i + ': ' + id);
}
```
### Selección de Imágenes
```// Primero agregar mi variable ROI
// Generar una variable que contenga un diccionario que permita enlistar las imagenes filtradas.

var imageList = [
  {id: 'COPERNICUS/S2/20210105T160511_20210105T160512_T16PHR', name: 'Image 0'},
  {id: 'COPERNICUS/S2/20210105T160511_20210105T160512_T17PKL', name: 'Image 1'},
  {id: 'COPERNICUS/S2/20210105T160511_20210105T160512_T17PLL', name: 'Image 2'},
  {id: 'COPERNICUS/S2/20210117T155529_20210117T155525_T17PLL', name: 'Image 3'},
  {id: 'COPERNICUS/S2/20210120T160509_20210120T160511_T16PHR', name: 'Image 4'},
  {id: 'COPERNICUS/S2/20210120T160509_20210120T161043_T17PKL', name: 'Image 5'},
  {id: 'COPERNICUS/S2/20210125T160511_20210125T160512_T16PHR', name: 'Image 6'},
  {id: 'COPERNICUS/S2/20210127T155529_20210127T155525_T17PLL', name: 'Image 7'},
  {id: 'COPERNICUS/S2/20210130T160509_20210130T160949_T17PKL', name: 'Image 8'},
  {id: 'COPERNICUS/S2/20210204T160511_20210204T160511_T16PHR', name: 'Image 9'},
  {id: 'COPERNICUS/S2/20210206T155529_20210206T155524_T17PLL', name: 'Image 10'},
  {id: 'COPERNICUS/S2/20210209T160509_20210209T160752_T16PHR', name: 'Image 11'},
  {id: 'COPERNICUS/S2/20210221T155531_20210221T160006_T17PLL', name: 'Image 12'},
  {id: 'COPERNICUS/S2/20210224T160511_20210224T160840_T16PHR', name: 'Image 13'},
  {id: 'COPERNICUS/S2/20210224T160511_20210224T160840_T17PKL', name: 'Image 14'},
  {id: 'COPERNICUS/S2/20210224T160511_20210224T160840_T17PLL', name: 'Image 15'},
  {id: 'COPERNICUS/S2/20210226T155529_20210226T155524_T17PLL', name: 'Image 16'},
  {id: 'COPERNICUS/S2/20210306T160511_20210306T160616_T16PHR', name: 'Image 17'},
  {id: 'COPERNICUS/S2/20210306T160511_20210306T160616_T17PKL', name: 'Image 18'},
  {id: 'COPERNICUS/S2/20210313T155531_20210313T155525_T17PLL', name: 'Image 19'},
  {id: 'COPERNICUS/S2/20210318T155529_20210318T155625_T17PLL', name: 'Image 20'},
  {id: 'COPERNICUS/S2/20210326T160511_20210326T160907_T16PHR', name: 'Image 21'},
  {id: 'COPERNICUS/S2/20210520T160509_20210520T160844_T17PLL', name: 'Image 22'},
  {id: 'COPERNICUS/S2/20210530T160509_20210530T160845_T16PHR', name: 'Image 23'},
  {id: 'COPERNICUS/S2/20210619T160509_20210619T160856_T16PHR', name: 'Image 24'},
  {id: 'COPERNICUS/S2/20210619T160509_20210619T160856_T17PKL', name: 'Image 25'},
  {id: 'COPERNICUS/S2/20210619T160509_20210619T160856_T17PLL', name: 'Image 26'},
  {id: 'COPERNICUS/S2/20210716T155529_20210716T155527_T17PLL', name: 'Image 27'},
  {id: 'COPERNICUS/S2/20210902T160511_20210902T160512_T17PLL', name: 'Image 28'},
  {id: 'COPERNICUS/S2/20211012T160521_20211012T160702_T17PLL', name: 'Image 29'},
  {id: 'COPERNICUS/S2/20211106T160509_20211106T160855_T17PLL', name: 'Image 30'},
  {id: 'COPERNICUS/S2/20211111T160511_20211111T160513_T17PLL', name: 'Image 31'},
  {id: 'COPERNICUS/S2/20211116T160509_20211116T161005_T16PHR', name: 'Image 32'},
  {id: 'COPERNICUS/S2/20211116T160509_20211116T161005_T17PKL', name: 'Image 33'},
  {id: 'COPERNICUS/S2/20211116T160509_20211116T161005_T17PLL', name: 'Image 34'},
  {id: 'COPERNICUS/S2/20211126T160509_20211126T160507_T16PHR', name: 'Image 35'},
  {id: 'COPERNICUS/S2/20211211T160511_20211211T160510_T16PHR', name: 'Image 36'},
  {id: 'COPERNICUS/S2/20211211T160511_20211211T160510_T17PKL', name: 'Image 37'},
  {id: 'COPERNICUS/S2/20211211T160511_20211211T160510_T17PLL', name: 'Image 38'}
];

// Loop sobre la lista de imágenes
for (var i = 0; i < imageList.length; i++) {
  var image = ee.Image(imageList[i].id);
  var imageName = imageList[i].name;
  
  // Visualiza la imagen en RGB
  Map.addLayer(image, {bands: ['B4', 'B3', 'B2'], min: 0, max: 3000}, imageName);
}

// Set the outline color
var outlineColor = '000000';

// Create an image with a constant value of 0
var emptyImage = ee.Image().byte().paint({
  featureCollection: roi,
  color: 0,
  width: 1
});

// Create a visualization parameter to display the outline
var outlineParams = {
  palette: outlineColor,
  opacity: 1,
  forceRgbOutput: true
};

// Display the ROI on the map with no filling color
Map.addLayer(emptyImage, outlineParams, 'ROI without Filling Color');
```
### Obtención del ID del producto Copernicus:
```var image = ee.Image("COPERNICUS/S2_SR/20210206T155529_20210206T155524_T17PLL");

// Get all metadata properties of the image
image.getInfo(function(info) {
  // Print the metadata in the console
  print('Metadata:', info.properties);
});
```
