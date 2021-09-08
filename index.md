
# Introducción a OpenCV con Python
Autores: [Fabrizio Gilio](https://github.com/Fabriziogilio) y [Camila Vives](https://github.com/camvives)

## ¿Qué es OpenCV?

<p style='text-align: justify;'> 
OpenCV (Open Source Computer Vision Library) es una librería de código abierto multiplataforma, construida con el objetivo de proveer una infraestructura común para aplicaciones de visión artificial, y para acelerar el uso de machine perception en productos comerciales. 
</p>

### Historia

### Usos de OpenCV

### Links de utilidad
- Página principal: <https://opencv.org>

-  Repositorio en Github: <https://github.com/opencv/opencv>

- Documentación: <https://docs.opencv.org/master/>

- Foro Q&A: <https://forum.opencv.org>

- Repositorio con funcionalidades extra: <https://github.com/opencv/opencv_contrib>

## Proceso de instalación
### Windows
<p style='text-align: justify;'>
La forma más simple de instalar la librería OpenCV en Windows es a través de un wrapper package (no oficial) construido con paquetes pre-compilados para Python, usando la herramienta <code>pip</code>. 
</p>
El proceso es entonces el siguiente:

<ol>
<li> En primer lugar, comprobamos que la versión de Python es mayor a 3.6.X (Septiembre de 2021) con `python -V` o `python --version`</li>

<center>
<img src="images\Picture1.png"/>
</center>

<li>(Opcional) Creamos un entorno virtual con `python -m env [nombre_entorno]` y lo activamos con `[nombre_entorno]\Scripts\activate.bat`

Esto sirve para que no colisionen las dependencias de paquetes y las versiones y además para ver qué otros paquetes instala OpenCV </li>

<center>
<img src="images\Picture2.png"/>
</center>

<li>Para ver los paquetes del entorno utilizamos `pip list`</li>

<center>
<img src="images\Picture3.png"/>
</center>

<li>Instalamos OpenCV con el comando `pip install opencv-python`. OpenCV requiere de la librería numpy, por eso la va a instalar automáticamente</li>

<center>
<img src="images\Picture4.png"/>
</center>

<li>Verificamos los nuevos paquetes instalados, utilizando nuevamente `pip list`</li>

<center>
<img src="images\Picture5.png" style="zoom: 85%";/>
</center>

<li>Comprobamos que se haya instalado correctamente: iniciamos la consola de python con el comando `python`, importamos OpenCV con `import cv2 as cv` e imprimimos la versión con `print(cv.__version__)`</li>

<center>
<img src="images\Picture6.png" style="zoom: 85%";/>
</center>

<li> (Recomendado) Instalar la librería matplotlib a través de `pip install matplotlib`. Este paso no es obligatorio, pero muchas de las funciones que se usan en OpenCV se pueden simplificar usando funciones de esa librería </li>

### Ubuntu
De la misma forma que en Windows, OpenCV puede ser instalado en Ubuntu a partir de paquetes pre-compilados.  

Para instalarlo, utilizamos el siguiente comando en la terminal (como usuario root): 

```
$ sudo apt-get install python3-opencv
```

Luego, abrimos el IDLE de Python y comprobamos que se haya instalado correctamente:

```
import cv2 as cv
print(cv.__version__)
```
Si el resultado de la version actual se imprime sin ningún error, quiere decir que se ha instalado correctamente.

### Fedora
Para el sistema operativo Fedora, los paquetes pre-compilados de OpenCV se instalan a través del siguiente comando:
```
$ yum install numpy opencv*
```
Luego, abrimos el IDLE de Python y comprobamos que se haya instalado correctamente:
```
>>> import cv2 as cv
>>> print(cv.__version__)
```
Si el resultado de la version actual se imprime sin ningún error, quiere decir que se ha instalado correctamente.

## Procesamiento de imágenes
### ¿Qué es una imagen digital?

<p style='text-align: justify;'>
Antes de comenzar a hablar de procesamiento de imágenes, debemos saber exactamente qué es una imagen digital. Existen múltiples formas de obtener imágenes digitales: sacando una foto con un smartphone, creándola con alguna herramienta de software, escaneándola, o bien, a través de procesos más complejos como lo pueden ser las tomografías computadas o las resonancias magnéticas. 
</p>

<p style='text-align: justify;'>
De cualquier forma, mientras nosotros (los humanos) vemos una representación gráfica, los dispositivos que capturan la imagen la almacenan como una gran matriz de dos dimensiones, formada por valores numéricos que representan cada uno de los puntos que se encuentran en ella. Los elementos que conforman la matriz son llamados <i>Picture Elements</i>, <i>Image Elements</i>, o simplemente <i>Pixels</i>.
</p>


<center>
<img src="https://docs.opencv.org/master/MatBasicImageForComputer.jpg"/>
</center>
<center>
Fuente:
<a href="https://docs.opencv.org/master/d6/d6d/tutorial_mat_the_basic_image_container.html">OpenCV</a>
</center>

<p style='text-align: justify;'>
A modo de ejemplo, en la imagen de arriba se puede ver que el espejo del auto no es más que una matriz que contiene el nivel de intensidad de cada pixel. 
</p>

### Almacenamiento de Pixels
<p style='text-align: justify;'>
La forma de almacenar los pixels varía según las necesidades del problema que se quiera resolver. 
Como se mencionó anteriormente, cada uno de ellos contendrá el color o la intensidad de color de la imagen. 
</p>

<p style='text-align: justify;'>
En el caso de las imagenes que se encuentran en escala de grices (<i>grayscale</i>), el color final se logra a través de un sólo valor por pixel que indica la información de intensidad, o dicho de otra manera, la cantidad de luz que contiene cada elemento de la imagen. Por lo tanto, los únicos colores que serán visibles son el blanco y el negro, teniendo como opción la combinación de ellos para permitirnos crear distintas tonalidades de gris.
</p>

<center>
<img src="https://upload.wikimedia.org/wikipedia/commons/f/fa/Grayscale_8bits_palette_sample_image.png"/>
</center>
<center>
<a href="https://commons.wikimedia.org/wiki/File:Grayscale_8bits_palette_sample_image.png">Ricardo Cancho Niemietz</a>, Public domain, via Wikimedia Commons
</center>

<p style='text-align: justify;'>
Por otro lado, para poder obtener imágenes a color, existen diferentes métodos, donde cada uno de ellos divide los pixeles en tres o cuatro componentes básicos. 
De esta forma, para representar al color que contendrá cada pixel, en lugar de contar con una sóla matriz bidimensional, se tiene una colección de tres o cuatro matrices bidimensionales las cuales a su vez contienen valores numéricos que indican la intensidad.
</p>

#### RGB

<p style='text-align: justify;'>
El más popular de los métodos es el <i>RGB</i> dado que esa es la forma en la que nuestros ojos construyen los colores. En este caso particular, los componentes básicos son rojo, verde y azul y en ocaciones se agrega un cuarto elemento (alpha) que es la transparencia. 
</p>

<center>
<img src="https://e2eml.school/images/image_processing/three_d_array.png" style="zoom: 35%;"/>
</center>
<center>
Fuente:
<a href="https://e2eml.school/convert_rgb_to_grayscale.html">e2eml.school</a>
</center>


<p style='text-align: justify;'>
Cada una de las matrices que representan a los elementos rojo, verde y azul se llaman canales. Si la imagen RGB es de 24 bits (estándar actual), cada canal tiene 8 bits. Esto quiere decir que la imagen final está compuesta de tres imágenes, una por cada canal, donde cada sub-imagen puede almacenar pixeles discretos con una intensidad medida con valores numéricos en el rango de 0 y 255. 
</p>

<center>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/Beyoglu_4671_tricolor.png/800px-Beyoglu_4671_tricolor.png" style="zoom: 50%;"/>
</center>
<center>
<a href="https://commons.wikimedia.org/wiki/File:Beyoglu_4671_tricolor.png">© Nevit Dilmen</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>, via Wikimedia Commons
</center>

<p style='text-align: justify;'>
Esto quiere decir que partiendo de las tres imágenes en escala de grices de los canales, se puede construir una imagen a color. Por ejemplo, en la figura superior, la columna de la derecha muestra los canales aislados en escalas de grices, mientras que en la columna de la izquierda se encuentran su equivalencia en colores naturales. Por último se muestra la combinación de dichas sub-imagenes.
</p>

<p style='text-align: justify;'>
Algo que es importante mencionar es que la operación inversa también es posible: a partir de la imagen a color, se pueden obtener las imágenes en escala de grices de cada uno de los canales. Si se manejan los canales (tanto separados como en conjunto) con diferentes técnicas, se consiguen distintos resultados de efectos artisticos, los cuales son comunmente llamados <i>filtros</i>. 
</p>

#### HLS y HSV 
<p style='text-align: justify;'>
El espacio de colores HSL fue inventado en 1938 por Georges Valensi, un ingeniero de telecomunicaciones francés, que lo que buscaba era un método para añadir color a la forma existente de codificación monocrómica utilizada para transmitir video, dado que sólo tenían la componente de luminancia. Con esto, la cadena de televisión emisora podía enviar imágenes a color y los receptores que aún contaban con dispositivos monocromáticos podían recibir "colores" traducidos en blanco y negro, sin modificar las señales transmitidas. 
</p>

<center>
<img src="https://i.insider.com/604bba8910c8760018b92fcc?width=700&format=jpeg&auto=webp" style="zoom: 45%;"/>


<img src="https://i.insider.com/604bba6bfea127001886a814?width=700&format=jpeg&auto=webpg" style="zoom: 41.5%;"/>
</center>
<center>
Marvel Studios/Disney Plus
</center>


<p style='text-align: justify;'>
Ahora, volviendo a lo digital, a pesar de que la mayoría de los dispositivos producen colores con la combinación RGB, la relación entre la cantidad de rojo, verde y azul y el color resultante no es intuitiva. Por este motivo, se intentó buscar una forma de representar el color que tenga que ver con la manera en la que los artistas lo creaban, es decir a través de distintas tinturas y sombras. 
Este tipo de representación del color, llamada HSV, fue creada en los años 70 por el ingeniero norteamericano Alvy Ray Smith, el cual fue uno de los fundadores de PIXAR y de la división de computación en Lucasfilm. Para poder construirlo tomó como base al modelo HSL mencionado anteriormente, y de ahí vienen las similitudes entre ambos.
</p>

<p style='text-align: justify;'>
A diferencia del modelo RGB que es cúbico, los modelos HSV y HLS son cilíndricos. Al ser de esta forma, los colores se definen a través de dimensiones angulares, teniendo en el eje vertical los colores neutros, acromáticos o grices. Tanto la representacion HLS como la HSV incluyen tres canales:
</p>

- <u>Hue (Matiz o Tono)</u>, que representa a los colores digitales primarios (rojo, verde, azul) con todos los matices intermedios (naranjas, amarillos, violetas, entre otros).
- <u>Saturation (Saturación)</u>, que indica la "cantidad de color". Esto quiere decir que el valor mínimo de saturación para cualquier color es el gris, mientras que el máximo es el más "puro" o "intenso".
-  <u>Value (Valor) en HLS o Lightness (Luminosidad) en HSV</u>, que mide la cantidad de luz. Cualquier color al aumentar su cantidad de luz tiende al blanco y al disminuirla, tiende al negro. 

<center>
<img src="https://upload.wikimedia.org/wikipedia/commons/0/05/RGB_Cube_Show_lowgamma_cutout_a.png" style="zoom: 13%;"/>

<img src="https://upload.wikimedia.org/wikipedia/commons/3/33/HSV_color_solid_cylinder_saturation_gray.png" style="zoom: 13%;"/>

<img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/HSL_color_solid_cylinder_saturation_gray.png" style="zoom: 13%;"/>
</center>
<center>
<a href="https://commons.wikimedia.org/wiki/File:RGB_Cube_Show_lowgamma_cutout_b.png">SharkD</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>, via Wikimedia Commons
</center>

<p style='text-align: justify;'>
Como puede verse en la figura, la principal diferencia entre HSV y HSL es que en HSL la saturación va del color puro al gris medio y en HSV la saturación va del color puro al blanco. En consecuencia, el tono en HSL va desde el negro al blanco y en HSV va desde el negro al color intenso.
</p>

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
- Channel (digital image): <https://en.wikipedia.org/wiki/Channel_(digital_image)>
- HSL and HSV: <https://en.wikipedia.org/wiki/HSL_and_HSV>
- Antonio Herrera - Modelos de Color: <https://ahenav.com/2014/04/09/modelos-de-color/>
- Descripción del modelo de color HSL: <http://guiadigital.uam.es/SCUAM/documentacion/pdfs_a_descargar/color.pdf>