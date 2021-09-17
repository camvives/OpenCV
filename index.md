
# Introducción a OpenCV con Python
Autores: [Fabrizio Gilio](https://github.com/Fabriziogilio) y [Camila Vives](https://github.com/camvives)

  * [¿Qué es OpenCV?](#qué-es-opencv)
    + [Historia](#historia)
    + [Usos de OpenCV](#usos-de-opencv)
    + [Links de utilidad](#links-de-utilidad)
  * [Proceso de instalación](#proceso-de-instalación)
    + [Windows](#windows)
    + [Ubuntu](#ubuntu)
    + [Fedora](#fedora)
  * [Procesamiento de imágenes](#procesamiento-de-imágenes)
    + [¿Qué es una imagen digital?](#qué-es-una-imagen-digital)
    + [Almacenamiento de Pixels](#almacenamiento-de-pixels)
      - [RGB](#rgb)
      - [HLS y HSV](#hls-y-hsv)
  * [Ejemplos](#ejemplos)
    + [Ejemplo 1 - ¿Dónde está Wally?](#ejemplo-1---dónde-está-wally)
      - [Código](#código)
    + [Ejemplo 2 - Filtros en Cámara Web](#ejemplo-2---filtros-en-cámara-web)
      - [Código](#código-1)
  * [Recursos Adicionales](#recursos-adicionales)
  * [Referencias](#referencias)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## ¿Qué es OpenCV?

<p style='text-align: justify;'> 
OpenCV (Open Source Computer Vision Library) es una librería de código abierto multiplataforma, construida con el objetivo de proveer una infraestructura común para aplicaciones de <i>visión artificial</i>, y para acelerar el uso de <i>machine perception</i> en productos comerciales. 
</p>

<p style='text-align: justify;'>
La visión artificial (también conocida como computer vision), se trata de una disciplina que provee métodos para adquirir, procesar, analizar y comprender imágenes del mundo real. De esta manera, la visión artificial intenta reproducir en las computadoras la forma en la que los humanos vemos el mundo que nos rodea. 
</p>

<p style='text-align: justify;'>
El machine perception es entonces, la capacidad de un sistema de computación de interpretar los datos que se obtienen a través de computer vision, computer audition, machine touch o machine olfaction. El objetivo final de este campo es que la interpretación sea similar a la forma en la que los humanos usan sus sentidos para ver el mundo que los rodea.
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
<li style="padding-top:1em; padding-bottom:0.5em"> En primer lugar, comprobamos que la versión de Python es mayor a 3.6.X (Septiembre de 2021) con <code>python -V </code> o <code>python --version</code></li>

<center>
<img src="images\Picture1.png"/>
</center>

<li style="padding-top:1em; padding-bottom:0.5em">(Opcional) Creamos un entorno virtual con <code>python -m env [nombre_entorno]</code> y lo activamos con <code>[nombre_entorno]\Scripts\activate.bat</code>

Esto sirve para que no colisionen las dependencias de paquetes y las versiones y además para ver qué otros paquetes instala OpenCV </li>

<center>
<img src="images\Picture2.png"/>
</center>

<li style="padding-top:1em; padding-bottom:0.5em">Para ver los paquetes del entorno utilizamos <code>pip list</code></li>

<center>
<img src="images\Picture3.png"/>
</center>

<li style="padding-top:1em; padding-bottom:0.5em">Instalamos OpenCV con el comando <code>pip install opencv-python</code>. OpenCV requiere de la librería numpy, por eso la va a instalar automáticamente</li>

<center>
<img src="images\Picture4.png"/>
</center>

<li style="padding-top:1em; padding-bottom:0.5em">Verificamos los nuevos paquetes instalados, utilizando nuevamente <code>pip list</code></li>

<center>
<img src="images\Picture5.png" style="zoom: 85%;"/>
</center>


<li style="padding-top:1em; padding-bottom:0.5em">Comprobamos que se haya instalado correctamente: iniciamos la consola de python con el comando <code>python</code>, importamos OpenCV con <code>import cv2 as cv</code> e imprimimos la versión con <code>print(cv.__version__)</code></li>

<center>
<img src="images\Picture6.png" style="zoom: 85%;"/>
</center>

<li style="padding-top:1em; padding-bottom:0.5em"> (Recomendado) Instalar la librería matplotlib a través de <code>pip install matplotlib</code>. Este paso no es obligatorio, pero muchas de las funciones que se usan en OpenCV se pueden simplificar usando funciones de esa librería </li>
</ol>

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

<p style='text-align: justify;'>  ¿Dónde está Wally? es una serie de libros para niños creada por el ilustrador inglés Martin Handford. El juego que presentan los libros se basa en encontrar al personaje Wally, que está oculto dentro de una multitud de ilustraciones que representan a cientos de personas, objetos y animales haciendo cosas divertidas. 
</p>


<center>
<img src="https://upload.wikimedia.org/wikipedia/en/e/ec/MartinHandfordWally%26Friends.PNG" style="zoom: 85%;"/>
</center>

<center>
By <a rel="nofollow" class="external free" href="http://waldo.wikia.com">http://waldo.wikia.com</a>, <a href="//en.wikipedia.org/wiki/File:MartinHandfordWally%26Friends.PNG" title="Fair use of copyrighted material in the context of Where's Wally?">Fair use</a>, <a href="https://en.wikipedia.org/w/index.php?curid=23173518">Link</a>
</center>

<p style='text-align: justify;'>
En este ejemplo intentaremos que el programa escrito en Python con OpenCV, encuentre a Wally en una ilustración completa, teniendo previamente un recorte de lo que debe encontrar. Para esto vamos a proveer al programa con dos imágenes, una del escenario completo, a la cual se le llama <i>Source image</i> (I): 
</p>

<center>
<img src="images\where-is-wally.jpg" style="zoom: 7%;"/>
</center>
<center>
<a href="https://imgur.com/user/WhereWasWaldo">WhereWasWaldo</a> via Imgur
</center>

y otra del recorte de Wally en el escenario, la cual es llamada <i>Template image</i> (T):
<center>
<img src="images\Wally.jpg" style="zoom: 50%;"/>
</center>

<p style='text-align: justify;'>
Para identificar la zona en las que ambas imágenes coinciden, OpenCV compara la imagen T contra la imagen I desplazándola. Es decir, la matriz de números de la imagen plantilla se compara pixel por pixel con la imagen fuente, y a través de una métrica se calcula que tan "buena" o "mala" es la comparación. 
</p>

<p style='text-align: justify;'>
En nuestro ejemplo, una vez que encuentre una comparación satisfactoria, marcará la zona en la que se encuentra Wally con un rectángulo.
</p>

<center>
<img src="images\wally_found.jpg" style="zoom: 50%;"/>
</center>

#### Código 

<script src="https://gist.github.com/camvives/63d6a2373a687176d82131e2e7c6d8f0.js"></script>

### Ejemplo 2 - Filtros en Cámara Web
<p style='text-align: justify;'>
En este segundo ejemplo haremos uso de la cámara web, y aplicaremos distintos filtros a la imagen que se está capturando a tiempo real. Para que puedan verse todos los filtros a la vez crearemos una ventana dividida en cuatro porciones en las que se reproduzca la misma imagen.
</p>

<p style='text-align: justify;'>
El siguiente paso será aplicar filtros que provee OpenCV a tres de las cuatro porciones de la ventana, manteniendo en una la imagen original. En este caso aplicaremos los siguientes filtros:
</p>
<ol>
<li><u>Desenfoque gaussiano:</u> es un efecto de suavizado, en donde se mezclan ligeramente los colores de los pixels, lo que provoca que la imagen pierda detalle y se vea menos nítida.</li>
<li><u>Filtro Laplaciano:</u> este filtro destaca las regiones de la imagen que tienen un rápido cambio en sus pixels, lo cual se da generalmente en los bordes de los objetos que se encuentran en la imagen.</li>
<li><u>Cambio de BGR a RGB:</u> como se vió anteriormente, las imágenes pueden descomponerse en sus canales básicos. OpenCV almacena los pixels de video en formato BGR, es decir que las matrices de azul y rojo se encuentran invertidas. Con este filtro, podremos ver que al convertir la imagen a RGB, el objeto que en este caso es rojo, se verá azul y lo mismo ocurrirá con los tonos intermedios de estos dos colores. 
</ol>

<center>
<img src="images\Deadpool.png" style="zoom: 50%;"/>
</center>

#### Código 
<script src="https://gist.github.com/camvives/b9cda75cbd3b855771c7be2c65a356af.js"></script>

## Recursos Adicionales
- Canal de Youtube  de  Murtaza's Workshop - Robotics and AI: <https://www.youtube.com/c/MurtazasWorkshopRoboticsandAI>
- Blog de OMES: <https://omes-va.com/>
- Curso oficial OpenCV con Python: <https://opencv.org/course-opencv-python/>

## Referencias
- OpenCV - About: <https://opencv.org/about/>
- Computer vision: <https://en.wikipedia.org/wiki/Computer_vision>
- Machine perception: <https://en.wikipedia.org/wiki/Machine_perception>
- Introduction to OpenCV: <https://docs.opencv.org/master/da/df6/tutorial_py_table_of_contents_setup.html>
- Mat - The Basic Image Container: <https://docs.opencv.org/master/d6/d6d/tutorial_mat_the_basic_image_container.html>
- How do digital images work?: <https://www.bbc.co.uk/bitesize/topics/zf2f9j6/articles/z2tgr82>
- Grayscale: <https://en.wikipedia.org/wiki/Grayscale>
- How to Convert an RGB Image to Grayscale: <https://e2eml.school/convert_rgb_to_grayscale.html>
- Channel (digital image): <https://en.wikipedia.org/wiki/Channel_(digital_image)>
- HSL and HSV: <https://en.wikipedia.org/wiki/HSL_and_HSV>
- Antonio Herrera - Modelos de Color: <https://ahenav.com/2014/04/09/modelos-de-color/>
- Descripción del modelo de color HSL: <http://guiadigital.uam.es/SCUAM/documentacion/pdfs_a_descargar/color.pdf>
- Template Matching: <https://docs.opencv.org/3.4/de/da9/tutorial_template_matching.html>
- Desenfoque Gaussiano: <https://es.wikipedia.org/wiki/Desenfoque_gaussiano>
- Laplacian Filter: <https://www.sciencedirect.com/topics/engineering/laplacian-filter>