## Usar CodeDeploy y CodeBuild
### 1. Crear roles para la fase de deploy
Debemos crear roles tanto para la EC2 que nos permita leer el bucket S3 donde se almacenará el código (AmazonS3ReadOnlyAccess) como para el servicio de CodeDeploy para que pueda arrancar la instancia de EC2 y acceder a ELB y ASG (AWSCodeDeployRole)
### 2. Instalar en el EC2 la aplicación de CodeDeploy
Con los comandos que se encuentran en commands.sh se instala en la instancia de EC2 el acceso a CodeDeploy
### 3. Crear un deployment group
Primero se le añade a las EC2 que perteneceran a dicho grupo un tag para poder identificarlas. Acto seguido crearemos el deployment group, le asignaremos el rol previamente creado y le asignaremos las EC2 instances del tag que hemos creado
