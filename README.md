# Instalación de Geoserver

El objetivo de esta guía es instalar un GEOSERVER para producción y que se comporte lo más estable posible.

## Primeros pasos
Para obtener el archivo `.war`, ingresaremos a la siguiente dirección : 
   
   `http://geoserver.org/download/`  

#### Instalación del Geoserver
 Ahora procedemos a copiar el archivo `.war` al folder **webapps** dentro de **Tomcat** (tomcat/webapss)  
  ```
  sudo cp  geoserver.war root/tomcat/webapps/
  ```

### Requerimientos Técnicos
   * Sistemas operativo Ubuntu
   * Servidor Tomcat  

### Configuración del GEOSERVER  

Con el GEOSERVER ya instalado sobre tomcat, por medio de un explorador web ingresamos la url `http://localhost:8080/geoserver/web`:  
   
   * Nos autenticamos por default con ***username*** : **admin** y **password** : **geoserver**  
   * Por seguridad creamos un nuevo usuario  en *Security* -> *Users,Groups, and Roles* -> *Add new user*
     y asignamos los roles de ADMIN y GROUP_ADMIN.
   * Borramos las group-layers, layers, stores, styles y workspaces que vienen por default en el Geoserver en este orden.
  
## Construido con
* [Geoserver][1] Lenguaje de programación
* [Rsync][2] Usado para generar la sincronización de las carpetas.

## Versionando  
Usamos [SemVer][3] para versionar. Para las versiones disponibles, consulte [las etiquetas en este repositorio][4].

## Autores
* **Raúl Medina Peña** - [Github][5]

## Licencia
Este proyecto está licenciado bajo la licencia MIT; consulte el archivo [LICENSE](LICENSE) para obtener detalles.

## Agradecimientos  
* Agradecemos a [Olmo Zavala][6] por su colaboración y todo su apoyo en este proyecto.

[1]: https://www.gnu.org/software/bash/
[2]: http://rsync.samba.org/
[3]: https://semver.org/lang/es/
[4]: https://github.com/grupoioa/respaldo_automatizado/tags
[5]: https://github.com/rmedina09
[6]: https://github.com/olmozavala

