
# Introducción a OpenCV con Python
Autores: [Fabrizio Gilio](https://github.com/Fabriziogilio) y [Camila Vives](https://github.com/camvives)

## ¿Qué es OpenCV?

<p style='text-align: justify;'> 
OpenCV (Open Source Computer Vision Library) es una librería de código abierto multiplataforma, construida con el objetivo de proveer una infraestructura común para aplicaciones de visión artificial, y para acelerar el uso de machine perception en productos comerciales. 

### Historia

### Usos de OpenCV

### Links de utilidad
- Página principal: <https://opencv.org>

-  Repositorio en Github: <https://github.com/opencv/opencv>

- Documentación: <https://docs.opencv.org/master/>

- Foro Q&A: <https://forum.opencv.org>

- Repositorio con funcionalidades extra: <https://github.com/opencv/opencv_contrib>

## Proceso de instalación

## Procesamiento de imágenes
### ¿Qué es una imagen digital?

<p style='text-align: justify;'>
Antes de comenzar a hablar de procesamiento de imágenes, debemos saber exactamente qué es una imagen digital. Existen múltiples formas de obtener imágenes digitales: sacando una foto con un smartphone, creándola con alguna herramienta de software, escaneándola, o bien, a través de procesos más complejos como lo pueden ser las tomografías computadas o las resonancias magnéticas. 

<p style='text-align: justify;'>
De cualquier forma, mientras nosotros (los humanos) vemos una representación gráfica, los dispositivos que capturan la imagen la almacenan como una gran matriz de dos dimensiones, formada por valores numéricos que representan cada uno de los puntos que se encuentran en ella. Los elementos que conforman la matriz son llamados <i>Picture Elements</i>, <i>Image Elements</i>, o simplemente <i>Pixels</i>.

<center>

![><](https://docs.opencv.org/master/MatBasicImageForComputer.jpg#center,)

*Fuente de la imagen: [OpenCV](https://docs.opencv.org/master/d6/d6d/tutorial_mat_the_basic_image_container.html)*
</center>

<p style='text-align: justify;'>
A modo de ejemplo, en la imagen de arriba se puede ver que el espejo del auto no es más que una matriz que contiene el nivel de intensidad de cada pixel. 

### Almacenamiento de Pixels
<p style='text-align: justify;'>
La forma de almacenar los pixels varía según las necesidades del problema que se quiera resolver. 
Como se mencionó anteriormente, cada uno de ellos contendrá el color o la intensidad de color de la imagen. 

<p style='text-align: justify;'>
En el caso de las imagenes que se encuentran en escala de grices (grayscale), el color final se logra a través de un sólo valor por pixel que indica la información de intensidad, o dicho de otra manera, la cantidad de luz que contiene cada elemento de la imagen. Por lo tanto, los únicos colores que serán visibles son el blanco y el negro, teniendo como opción la combinación de ellos para permitirnos crear distintas tonalidades de gris.

<center>

![><](https://upload.wikimedia.org/wikipedia/commons/f/fa/Grayscale_8bits_palette_sample_image.png)

*Fuente de la imagen: Ricardo Cancho Niemietz en [Wikipedia](https://en.wikipedia.org/wiki/Grayscale)*
</center>

<p style='text-align: justify;'>
Por otro lado, para poder obtener imágenes a color, existen diferentes métodos, donde cada uno de ellos divide los pixeles en tres o cuatro componentes básicos. 
De esta forma, para representar al color que contendrá cada pixel, en lugar de contar con una sóla matriz bidimensional, se tiene una colección de tres o cuatro matrices bidimensionales las cuales a su vez contienen valores numéricos que indican la intensidad.

<p style='text-align: justify;'>
El más popular de los métodos es el <i>RGB</i> dado que esa es la forma en la que nuestros ojos construyen los colores. En este caso particular, los componentes básicos son rojo, verde y azul y en ocaciones se agrega un cuarto elemento que es la transparencia. 

<center>

<img src="https://e2eml.school/images/image_processing/three_d_array.png" style="zoom: 35%;"/>

*Fuente de la imagen: [Brandon Rohrer](https://e2eml.school/convert_rgb_to_grayscale.html)*
</center>

<p style='text-align: justify;'>
Cada una de las matrices que representan a los elementos rojo, verde y azul se llaman canales. Si la imagen RGB es de 24 bits (estándar actual), cada canal tiene 8 bits. Esto quiere decir que la imagen final está compuesta de tres imágenes, una por cada canal, donde cada sub-imagen puede almacenar pixeles discretos con una intensidad medida con valores numéricos en el rango de 0 y 255. 


## Ejemplos 
### Ejemplo 1 - ¿Dónde está Wally?
<script src="https://gist.github.com/camvives/63d6a2373a687176d82131e2e7c6d8f0.js"></script>

### Ejemplo 2 - Filtros en Cámara Web
<script src="https://gist.github.com/camvives/b9cda75cbd3b855771c7be2c65a356af.js"></script>

## Recursos Adicionales
- Canal de Youtube  de  Murtaza's Workshop - Robotics and AI: <https://www.youtube.com/c/MurtazasWorkshopRoboticsandAI>

## Referencias
- OpenCV - About: <https://opencv.org/about/>
- Mat - The Basic Image Container: <https://docs.opencv.org/master/d6/d6d/tutorial_mat_the_basic_image_container.html>
- How do digital images work?: <https://www.bbc.co.uk/bitesize/topics/zf2f9j6/articles/z2tgr82>
- Grayscale: <https://en.wikipedia.org/wiki/Grayscale>
- How to Convert an RGB Image to Grayscale: <https://e2eml.school/convert_rgb_to_grayscale.html>

