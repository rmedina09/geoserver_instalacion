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

#### Instalación nativa de JAI y JAI Image I/O
   **JAI**
   * Descargamos JAI 1.1.3 para linux [jai-1.1.3-lib-linux-amd-4-jdk.bin][1]
   * Hacemos los sigueinte pasos :
     ```
     export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_101  
     sudo cp jai-1_1_3-lib-linux-amd64-jdk.bin $JAVA_HOME  
     cd $JAVA_HOME  
     sudo chmod u+x jai-1_1_3-lib-linux-amd64-jdk.bin  
     sudo ./jai-1_1_3-lib-linux-amd64-jdk.bin  
     sudo rm jai-1_1_3-lib-linux-amd64-jdk.bin  
     ```
     
   **JAI-IMAGIO**
   * Descargamos JAI-IMAGIO para linux [jai_imagio-1_1-lib-linux-amd64-jdk.bin][2]
   * Hacemos los siguientes pasos :  
     ```
     export _POSIX2_VERSION=199209  
     sudo cp jai_imageio-1_1-lib-linux-amd64-jdk.bin $JAVA_HOME  
     cd $JAVA_HOME  
     sudo chmod u+x jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     sudo ./jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     ```
   * En caso de que ocurra el siguiente error  `cannot open 215 for reading No such file or directory`
     Se puede hacer lo siguiente 
     ```
     sudo cp jai_imageio-1_1-lib-linux-amd64-jdk.bin jai_imageio-1_1-lib-linux-amd64-jdk.bin.old  
     sudo chmod 777 jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     sed s/+215/-n+215/ jai_imageio-1_1-lib-linux-amd64-jdk.bin.old > jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     sudo ./jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     sudo rm jai_imageio-1_1-lib-linux-amd64-jdk.bin  
     sudo rm jai_imageio-1_1-lib-linux-amd64-jdk.bin.old  
     ```
   
   
   Al final reiniciamos el servidor Tomcat
   ```
    sudo service tomcat stop
    sudo service tomcat start
   ```
   
  **NOTA :** GeoSolitions nos ofrece una guía para poder hacer la instalación. [link][3]
### Requerimientos Técnicos
   * Sistemas operativo Ubuntu
   * Servidor Tomcat  
   * GeoServer

### Configuración del GEOSERVER  

#### Interfaz Web 
Con el GEOSERVER ya instalado sobre tomcat, por medio de un explorador web ingresamos la url `http://localhost:8080/geoserver/web` :  
   
   * Nos autenticamos por default con ***username*** : **admin** y **password** : **geoserver**  
   * Por seguridad creamos un nuevo usuario  en  
     *Security* -> *Users,Groups, and Roles* -> *Add new user* y asignamos los roles de ADMIN y GROUP_ADMIN.
   * Borramos las group-layers, layers, stores, styles y workspaces que vienen por default en el Geoserver en este orden.
   * Habilitamos el *GeoWebCache* :  
     *Tile Caching* -> *Caching Defaults* -> *Provided Services*  
     Y marcamos las casillas de *Enable direct integration with GeoServer WMS*, *Enable WMS-C Service* y *Enable TMS Service*
   * Cambiamos las opciones del **log** a **PRODUCTION**  
     En *Settings* -> *Global* -> *Internal Settings* -> *Logging Settings* y seleccionamos **PRODUCTION_LOGGING.properties**
   * Cambiamos el numero máximo de "features" devueltas por WFS por 1000

#### Web.xml
Editamos el archivo web.xml para agregar las configuraciones que listamos en seguida:
   * Cambiar el directorio 'data' que es en donde se almacena la información, lo hacemos por medio de la variable 
     *GEOSERVER_DATA_DIRECTORY*.
     ```
     <context-param>
       <param-name>GEOSERVER_DATA_DIR</param-name>
       <param-value>root/Geoserver/data</param-value>
     </context-param>
     ```
   * Habilitamos el formato de salida JSONP (text/javascript), por medio de la variable *ENABLE_JSONP*
     ```
     <context-param>
       <param-name>ENABLE_JSONP</param-name>
       <param-value>true</param-value>
     </context-param>
     ```
## Construido con
* [Geoserver][4] GeoServer
* [Tomcat][5] Servidor de aplicaciones

## Versionando  
Usamos [SemVer][6] para versionar. Para las versiones disponibles, consulte [las etiquetas en este repositorio][7].

## Autores
* **Raúl Medina Peña** - [Github][8]

## Licencia
Este proyecto está licenciado bajo la licencia MIT; consulte el archivo [LICENSE](LICENSE) para obtener detalles.

## Agradecimientos  
* Agradecemos a [Olmo Zavala][9] por la creación de la primera versión, colaboración y su apoyo en este proyecto.

[1]: http://download.java.net/media/jai/builds/release/1_1_3/jai-1_1_3-lib-linux-amd64.tar.gz
[2]: http://download.java.net/media/jai-imageio/builds/release/1.1/jai_imageio-1_1-lib-linux-amd64.tar.gz
[3]: https://geoserver.geo-solutions.it/edu/en/install_run/jai_io_install.html
[4]: https://docs.geoserver.org/
[5]: http://tomcat.apache.org/
[6]: https://semver.org/lang/es/
[4]: https://github.com/grupoioa/respaldo_automatizado/tags
[5]: https://github.com/rmedina09
[6]: https://github.com/olmozavala

