# Introducción 

- Workshop introductorio a Docker con hands-on
 
# Requisitos

 - Docker desktop o cuenta en Docker.com y utilizar https://labs.play-with-docker.com 

# Temario
  
 - Qué es Docker?
 - Qué es una imagen?
 - Qué es un contenedor?
 - Diferencia entre contenedor y máquina virtual
 - Comandos útiles
 - Docker Compose
 - Cómo crear nuestras imágenes
 - Cómo crear contenedores
 - Otras cosas

# Grabación

## 2021
 - [Sesión 1](https://web.microsoftstream.com/video/c9c2d739-25c2-4cc9-8bdf-ec661a923f52?channelId=824fd8b2-bda4-49bf-a031-0ed921faa1c9)
 - [Sesión 2](https://web.microsoftstream.com/video/ce23278d-0206-4804-9b22-654cea10768d)
## 2020

 - [Sesión 1](https://web.microsoftstream.com/video/c9c2d739-25c2-4cc9-8bdf-ec661a923f52)

# Material de apoyo

[Presentación](https://tokiota-my.sharepoint.com/:p:/p/leonardo_micheloni/Ee0GuHKRJhVAjufPXJZxz2wB7mkJx-wSEVSZtOJubHDZZQ?e=U3rOaX)

# Preguntas de auto-evaluación

 - Un contenedor es una instancia de una imagen. v/f
 - Una imagen se puede modificar uan vez creada, es editable. v/f
 - Una contenedor puede crearse sin necesidad de una imagen. v/f
 - Un contenedor no está aislado, es posible ingresar a todos sus puertos desde el sistema host sin necesidad de configurar nada. v/f
 - Si al crear un contenedor se configura algún puerto con la opción -p , luego no puede cambiarse. v/f
 - Podemos ejecutar comandos sobre un contenedor en ejecución. v/f
 - No es posible ingresar dentro del sistema operativo de un contenedor para, por ejemplo, revisar carpetas y archivos, editar, etc. v/f
 - En un contenedor en ejecución es posible hacer cosas como instalar VIM. v/f
 - Un registro como hub.docker es un lugar desde donde se pueden descargar imágenes. v/f
 - Al crear un contenedor desde una imagen, si no especifico el tag (versión) por defecto se busca la versión etiquetada con "latest". v/f
 - Es posible tener varias imágenes con el mismo ID que tengan diferentes tags, es decir, que sean lo mismo. v/f
 - Cuando no se especifica un path completo y solo el nombre de la imagen que quiero utilizar, por defecto, Docker busca en hub.docker. v/f
 - Lo primero que ocurre cuando hago docker run nginx, es que se busca la imagen localmente. v/f
 - Las imágenes se componen de layers, con el fin de optimizar recursos al poder "reutilizar" layers en caso que se repitan en diferentes imágenes. v/f
 - Un docker-compose permite definir uno o varios servicios para que se ejecuten en conjunto. v/f
 - Los servicios dentro de un docker-compose no comparten su red interna, sino que es necesario conocer su IP para que se pueden "ver" entre ellos. v/f
 - Es posible pasar variables de entorno en un docker-compose.  v/f
 - Un Dockerfile sirve para definir contenedores. v/f
 - Por defecto al ejecutar docker build . se busca un fichero con el nombre "Dockerfile", pero es posible detallar el nombre del fichero si fuera otro. v/f
 - Cuando se crea una imagen es necesario pasar el "contexto" como parámetro, el que será el punto de partida de los paths internos a los que se haga referencia en el Dockerfile. v/f
 - Cuando creamos una imagen no podemos basarnos en una existentes, sino que tenemos que comenzar con FROM empty y luego ejecutar todos los comandos RUN dentro del Dockerfile para instalar todas las dependencias. v/f
 - Docker es la única herramienta para crear y ejecutar contenedores. v/f
 - OCI hace referencia a un standard en el formato de imágenes, que hacer posible la compatibilidad, por ejemplo, de imágenes Docker con otros sistemas como ContainerD. v/f
 