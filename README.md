## Práctica 5 Visión por Computador


### Contenidos 

[Preparación](#preparación)

[Entrenar modelo emociones](#entrenar-modelo-emociones)

[Filtro de emociones](#filtro-de-emociones)

[Filtro señor monopoly](#filtro-señor-monopoly)

### Preparación

En esta práctica 5, para la preparación será necesario importar los siguientes módulos:
- kagglehub: Usado para descargar datasets desde Kaggle
- ultralytics (YOLOv8): Usado para entrenar el modelo de clasificación de emociones
- opencv-python: Usado para la captura y procesamiento de vídeo
- numpy: Operaciones matemáticas
- deepface: Detección de rostros
- shutil / os:  gestión de archivos y carpetas

Además se preparan 2 funciones: 
- `load_image(path)`: Que se encarga de cargar una imagen que se usará en los filtros
- `overlay_image(bg, overlay, x, y, scale=1.0)`: Ajusta la imagen sobre el fondo, la escala, ajusta el canal de transparencias y recorta lo que salga fuera de la pantalla.

### Entrenar Modelo

Para la detección de emociones para esta práctica se ha utilizado `YOLO11s`, al igual que en la práctica anterior, que ofrece un buen equilibrio entre precisión y velocidad.  
Este modelo se entrenó utilizando un conjunto de imágenes provenientes de un dataset de kaggle a partir del siguiente link:
https://www.kaggle.com/datasets/ananthu017/emotion-detection-fer?resource=download

El dataset cuenta con imágenes imagenes de personas divididas en 6 emociones:

- Enfado
- Miedo
- Felicidad
- Tristeza
- Sorpresa
- Neutral
  
Una vez acabado su entrenamiento, en las siguientes gráficas se puede observar su resultado:
<img width="639" height="639" alt="image" src="https://github.com/user-attachments/assets/935decdd-842e-4e48-973b-d23372aee263" />


### Filtro de emociones

Una vez entrenado el modelo, se procede al procesamiento del vídeo para incluir el filtro.

Además para localizar la región donde aplicaremos los efectos se ha decidido usar el detector Haar Cascade de openCV.
Esto nos devuelve la posición (x, y, w, h) del rostro dentro de cada fotograma de vídeo. Se ha optado por usarlo porque es rápido y provoca que la cámara vaya a altos `fps`

Se decidió aplicar los siguientes filtros:

- Felicidad: Carita sonriente sobre la cabeza de la persona
- Tristeza: Nube lloviendo sobre la cabeza de la persona
- Enfado: Humo saliendo de las orejas
- Miedo: Sudor en la frente
- Sorpresa: Signo de exclamación rojo sobre la cabeza
- Neutral: Filtro gris en la pantalla

Las imágenes utilizadas son las siguientes:

<table align="center">
  <tr>
    <td><img src="assets/smile.png" width="120"/></td>
    <td><img src="assets/rain.png" width="120"/></td>
    <td><img src="assets/smoke.png" width="120"/></td>
    <td><img src="assets/sweat.png" width="120"/></td>
  </tr>
</table>

Este sería el resultado en formato gif del filtro:
![python_bG9uKZG5W7](https://github.com/user-attachments/assets/554f6e32-796e-48d0-a346-3c46179bcfee)

### Filtro señor monopoly

Como segundo filtro planteado se optó por imitar a un personaje antiguo con monóculo, bigote blanco y sombrero de copa.

En esta ocasión, en lugar de usar Haar Cascade, se prefirió por probar otro metodo de detección de caras usar `Deepface`

Los pasos a seguir son añadir sobre el ojo un monóculo, sobre la cabeza el sombrero y a la altura entre la boca y la nariz el bigote.

Las imágenes utilizadas son las siguientes:
<table align="center">
  <tr>
    <td><img src="assets/monocle.png" width="120"/></td>
    <td><img src="assets/mustache.png" width="120"/></td>
    <td><img src="assets/top_hat.png" width="120"/></td>
  </tr>
</table>

Para añadirle un toque extra, se aplicó a la imagen un filtro blanco y negro y estática recordando las teles antiguas.

Este sería el resultado en formato gif del filtro:
![python_v86y6vg3w0](https://github.com/user-attachments/assets/8dae7641-be7a-4bdb-b9f2-212f63dfb7d0)


Saúl Expósito Morales



