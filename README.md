- 👋 Hi, I’m @marcborjamoll
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
marcborjamoll/marcborjamoll is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->


Documentación Sprint 2 - Hardening de Windows:


Para empezar crearemos un usuario con nuestro nombre, en mi caso “Marc Bauzá” y le asignaremos el rango de cuenta local sin ningún permiso.
Como podemos comprobar al intentar instalar cualquier aplicación nos pedirá la contraseña de administrador indicándonos que el usuario que hemos creado no es administrador.
Si queremos verificar que tenemos los sistemas de seguridad activos podemos buscarlo y configurarlo desde el apartado de “Seguridad De Windows”, el siguiente paso será activar el acceso controlado de carpetas y añadimos la carpeta que nos indica el enunciado.
Para simular un ataque a nuestro ordenador nos instalaremos una herramienta live, en este caso “Kali-linux-2022.3-live-amd64.iso”.  
Al iniciar la la herramienta cargará el sistema operativo entramos en su terminal y nos registramos como root, con el comando fdisk -l nos listará todas las particiones existentes en el disco duro, identificamos la partición que contiene el sistema operativo de windows 10 en mi caso como “/dev/sda2”. 
Para realizar el montaje de este tipo de sistemas se utilizará el comando mount -t ntfs-3g  /dev/sda2  /media donde /media es un directorio existente en Kali Linux, así le daremos acceso a los archivos de windows 10.
las contraseñas de los usuarios se suelen guardan en un archivo el cual es almacenado en C:/Windows/System32/config/SAM, Con chntpw se podrán realizar diferentes acciones sobre el archivo SAM de Windows, entre ellas se podrán administrar los grupos de usuarios añadiendo o quitando usuarios, eliminar contraseñas de usuarios o modificarlas.
Utilizaremos el comando chntpw  -i  /media/Windows/System32/config/SAM y se nos enseñara un menú y utilizaremos la opción 1 para editar los datos de contraseñas de usuarios. 
Luego nos preguntará el usuario al que se le debe modificar la contraseña, nosotros utilizaremos el  admin, una vez seleccionado el administrador seleccionaremos la opción 1 que eliminará la contraseña del usuario.
Cuando hayamos cifrado el disco nos pedirá una contraseña para entrar a la máquina y cuando intentemos limpiar la contraseña con el disco cifrado nos dará error constantemente.
