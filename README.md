## Usar CodeDeploy, CodeBuild y CodePipeline

### 1. Crear roles para la fase de deploy
Debemos crear roles tanto para la EC2 que nos permita leer el bucket S3 donde se almacenará el código (AmazonS3ReadOnlyAccess) como para el servicio de CodeDeploy para que pueda arrancar la instancia de EC2 y acceder a ELB y ASG (AWSCodeDeployRole)
### 2. Instalar en el EC2 la aplicación de CodeDeploy
Con los comandos que se encuentran en commands.sh se instala en la instancia de EC2 el acceso a CodeDeploy
### 3. Crear un deployment group
Primero se le añade a las EC2 que perteneceran a dicho grupo un tag para poder identificarlas. Acto seguido crearemos el deployment group, le asignaremos el rol previamente creado hace 2 pasos y le asignaremos las EC2 instances del tag que hemos creado
### 4. Almacenar nuestra aplicacion en un S3
Creamos un cubo de S3 para almacenar nuestra aplicacion en un .zip y luego referenciamos dicho cubo
### 5. Crear la pipeline
Se crea la pipeline con un nuevo service rol que será capaz de ejecutar todo lo que tengamos que hacer. De fuente ponemos lo que queramos, en nuestro caso GitHub
#### 5.1 Fase de build
En la fase de build y test instalaremos los requisitos previos que hagan falta y tambien haremos un pequeño test que comprobara si congratulations esta en el index.html. Para ello, elegiremos una managed image en Ubuntu cuyo tipo de entorno sea Linux, crearemos un nuevo service role y usaremos un archivo buildspec.yml
#### 5.2 Fase de deployment
Por último, elegiremos en la fase de deployment nuestra aplicacion y nuestro deployment group

