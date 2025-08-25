# MySQL con Docker en Kali Linux

Este proyecto muestra cómo levantar un contenedor de **MySQL** utilizando **Docker**, conectado desde Kali Linux.


## 1. Crear la carpeta de proyecto en el Escritorio

Primero ingresamos a nuestra consola del entorno de Kali, e ingresamos este comando

<img width="831" height="146" alt="image1" src="https://github.com/user-attachments/assets/05a5dfe6-11b7-46b6-b0ce-22545e0cb4db" />

Este comando se utiliza para crear la carpeta llamada "mysql-docker"

<img width="1440" height="900" alt="Imagen 2" src="https://github.com/user-attachments/assets/0a74b985-88d7-488b-9ffb-8cac05e471bb" />

Como se puede observar la carpeta se creó con éxito


## 2. Crear un Docker file

Para crear el archivo Dockerfile usamos el siguiente comando en la terminal:

![Imagen 3](https://github.com/user-attachments/assets/2d0b5fcd-b8f6-4e44-91c3-e293b9029b65)

cat > Dockerfile
Crea un archivo llamado Dockerfile.

<<'EOF' ... EOF
Se utiliza un heredoc (Here Document), que permite escribir varias líneas de texto dentro del archivo, hasta que se encuentra la palabra EOF.
Todo lo que se escriba entre <<'EOF' y EOF será el contenido del Dockerfile.

Contenido del Dockerfile

FROM mysql:8.0 → Usamos la imagen oficial de MySQL versión 8.0.

ENV MYSQL_ROOT_PASSWORD=Root123! → Define la contraseña del usuario root.

ENV MYSQL_DATABASE=midb → Crea automáticamente una base de datos llamada midb.

ENV MYSQL_USER=appuser y ENV MYSQL_PASSWORD=sql123! → Crea un usuario appuser con permisos sobre esa base de datos.

EXPOSE 3306 → Expone el puerto 3306 (el que usa MySQL por defecto).

<img width="1440" height="900" alt="Imagen 4" src="https://github.com/user-attachments/assets/1215988e-b86d-45e0-b471-f2b7f0443332" />

De esta forma, el archivo Dockerfile queda creado y listo para usar.

## 3. Construcción de la imagen


Ingresamos el siguiente comando para hacer la contrucción de la imagen:

<img width="2046" height="1377" alt="image" src="https://github.com/user-attachments/assets/8c6e0893-73ae-41fb-a39e-90d1b750629f" />

Una vez creada la imagen verificamos que la imagen exista

<img width="1612" height="205" alt="image" src="https://github.com/user-attachments/assets/af33c314-9500-4d3a-9677-1dc6a457aeaa" />

docker images → lista todas las imágenes que tienes descargadas o construidas en tu máquina.
| grep mi_mysql → el pipe (|) envía la salida anterior al comando grep, que filtra solo las líneas donde aparece la palabra mi_mysql.

Con eso filtraremos y veremos solo la imagen que acabamos de construir.


## 4. Crear un volumen (Opcional)

Procedemos a crear un volumen, un volumen en Docker es un espacio de almacenamiento persistente que vive fuera del contenedor, administrado por Docker.
Para evitar que cuando se cierre o borre el contenedor perdamos los datos creados en el, esto es opcional pero es una buena opción para manejar la persistencia.

<img width="750" height="147" alt="image" src="https://github.com/user-attachments/assets/4f53f948-dcfa-4c0a-bc4d-0c2f3b053390" />


## 5. Correr el contenedor desde la imagen

<img width="1099" height="303" alt="image" src="https://github.com/user-attachments/assets/a1020ad9-2944-43d6-bb36-a5d405e322e4" />

-d lo deja en segundo plano.

--restart unless-stopped lo reinicia si el host reinicia.

-p 3306:3306 expone MySQL al host.

-v mysql_data:/var/lib/mysql guarda los datos en el volumen.


Y ahora comprobamos que el contenedor esté corriendo

<img width="2699" height="174" alt="image" src="https://github.com/user-attachments/assets/8210ad28-6264-487c-8b9b-35d3abe911ca" />

Y como se puede ver la imagen está corriendo con éxito


## 6. Conectarse con el cliente MySQL desde el host

Procedemos a conectarnos con el cliente de MySQL y realizamos una consulta para verificar que funcione bien

<img width="1665" height="1462" alt="image" src="https://github.com/user-attachments/assets/b5814500-4195-4768-baa5-2c0361e6dc01" />





