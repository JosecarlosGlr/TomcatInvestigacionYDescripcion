# Tomcat: Investigación y descripción

### Catalina  
Catalina es el nombre del contenedor de servlets de Apache Tomcat. Catalina implementa las especificaciones de Java para Servlets y JavaServer Pages (JSP), gestionando el ciclo de vida de los componentes Java en las aplicaciones web.
En resumen es corazón de Tomcat; el contenedor que procesa los servlets y JSP.
### Coyote  
Coyote es el conector HTTP principal de Apache Tomcat, permitiendo que Tomcat actúe como un servidor web para manejar peticiones HTTP/1.1 y 2, procesar solicitudes de Java y servir archivos estáticos, conectando así el mundo HTTP con el contenedor de servlets Catalina. En resumen, Coyote es el componente que escucha en un puerto TCP, recibe la petición del cliente (navegador) y la pasa al motor de Tomcat (Catalina) para su procesamiento, y luego devuelve la respuesta.
### Jasper
Jasper, el motor JSP (JavaServer Pages) de Apache Tomcat, que compila las páginas JSP a código Java (servlets) para que Tomcat pueda procesarlas y entregarlas a los usuarios, permitiendo que los cambios en las páginas JSP se detecten y recompilen dinámicamente en tiempo de ejecución. Es decir, es un componente clave para ejecutar aplicaciones web dinámicas basadas en Java en Tomcat.
### Manager y Host Manager  
Apache Tomcat incluye varias aplicaciones web internas diseñadas para facilitar la administración del servidor y de las aplicaciones que se ejecutan sobre él. Entre estas herramientas destacan Manager y Host Manager, dos aplicaciones que, aunque suelen mencionarse juntas, cumplen funciones muy diferentes dentro del ecosistema de Tomcat. A continuación se explica de manera más detallada cuál es el propósito de cada una, cómo se accede a ellas y cuál es su relación con la configuración del servidor.  
Aunque ambas herramientas comparten la idea de ofrecer una administración centralizada del servidor, su ámbito de acción es distinto. El Manager está orientado a la administración de aplicaciones web ya desplegadas o por desplegar, mientras que el Host Manager se ocupa de la estructura de los hosts virtuales donde esas aplicaciones podrían residir.
### Estructura básica de directorios (bin, conf, webapps, lib, logs)  
- bin: Contiene los scripts ejecutables para iniciar (startup.sh/.bat), detener (shutdown.sh/.bat) y administrar Tomcat.  
 - conf: Guarda los archivos de configuración principales en formato XML, especialmente server.xml (configuración global) y web.xml (configuración por defecto para todas las aplicaciones).  
- lib: Aquí van las librerías (archivos JAR) que Tomcat y todas las aplicaciones web pueden usar.  
- logs: Almacena los archivos de registro (logs) generados por Tomcat.  
- webapps: Es el corazón del despliegue; aquí se colocan las aplicaciones web. Por defecto incluye ROOT, docs, examples, etc  
* ### Flujo interno de funcionamiento: recepción de peticiones, contenedores, despliegue de aplicaciones.  
