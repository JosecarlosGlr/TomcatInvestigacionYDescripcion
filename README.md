# Tomcat investigación y descripción

### 🧩 Componentes del Núcleo

* **Catalina (El Corazón):** Es el **Contenedor de Servlets** propiamente dicho. Implementa las especificaciones de Java Servlet y JSP. Es el motor que "piensa", gestiona las sesiones y el ciclo de vida de las aplicaciones web.
* **Coyote (El Oído):** Es el **Conector HTTP**. Su función es escuchar las peticiones entrantes en un puerto TCP (generalmente el 8080), recibir la solicitud del navegador y pasársela a Catalina para su procesamiento. Actúa de puente entre la red y el motor de Java.
* **Jasper (El Traductor):** Es el motor de **JSP (JavaServer Pages)**. Se encarga de analizar los archivos `.jsp`, traducirlos a código Java y compilarlos en Servlets (`.class`) para que puedan ser ejecutados.
    > **Nota técnica:** Jasper almacena los archivos compilados en la carpeta `/work`. Si se borra esta carpeta, Tomcat la regenerará automáticamente al recibir nuevas peticiones.

### 🛠️ Herramientas de Gestión
* **Manager App:** Es la interfaz web para administrar las **aplicaciones** (archivos WAR). Permite desplegar, iniciar, detener y recargar aplicaciones individuales sin necesidad de reiniciar el servidor completo.
* **Host Manager:** Es la interfaz para gestionar **Hosts Virtuales**. Permite configurar múltiples dominios (ej. `web1.com`, `web2.com`) servidos por una única instancia de Tomcat.

---

### Estructura basica de directorios

| Directorio | Descripción |
| :--- | :--- |
| `/bin` | Contiene los scripts ejecutables para el arranque (`startup.sh`) y parada (`shutdown.sh`) del servidor. |
| `/conf` | Almacena los archivos de configuración XML, incluyendo `server.xml` (puertos y conectores) y `tomcat-users.xml` (seguridad). |
| `/lib` | Contiene las librerías Java (`.jar`) compartidas que son accesibles por todas las aplicaciones desplegadas. |
| `/logs` | Directorio de registros. El archivo más importante es `catalina.out`, donde se vuelcan los errores y la salida estándar. |
| `/webapps` | **Directorio de despliegue automático**. Cualquier archivo `.war` o carpeta colocada aquí será detectada y ejecutada por Tomcat. |

---

## Flujo Interno de Funcionamiento

1.  **Recepción:** El cliente envía una petición. **Coyote** la recibe a través del puerto configurado (8080).
2.  **Procesamiento:** Coyote pasa la solicitud al motor **Catalina**.
3.  **Enrutado:** Catalina identifica el `Host` virtual y el `Context` (la aplicación específica) al que va dirigida la petición.
4.  **Ejecución:** Se invoca al Servlet correspondiente. Si es un JSP, **Jasper** lo compila primero.
5.  **Respuesta:** El resultado se envía de vuelta a Coyote, que lo entrega al cliente final.
