======================================================================
         📱 KINGDOM BARBER - API
======================================================================

🗓️ **Documentación Técnica: Kingdom Barber - API**  
📅 **Última actualización:** Octubre 2025  
👥 **Autores:** Juan Rivera, Oscar

Este repositorio contiene el código fuente del **backend** para el ecosistema digital de Kingdom Barber.  
Se trata de una **API RESTful** desarrollada con **Java + Spring Boot**, que funciona como el **núcleo central** y la **fuente única de verdad** del sistema.

======================================================================
        📖 GUÍA DE EJECUCIÓN Y ENDPOINTS
======================================================================

-----------------------------
📌 1. REQUISITOS PREVIOS
-----------------------------

Asegúrate de tener instaladas las siguientes herramientas:

- ☕ **Java Development Kit (JDK)** – Versión 17 o superior  
- 🔧 **Apache Maven** – Para compilar el proyecto y gestionar dependencias  

-----------------------------
🚀 2. INSTALACIÓN Y EJECUCIÓN
-----------------------------

**Paso 1: Clonar el repositorio**

```bash
git clone https://github.com/JuanRivera24/ap_i_tm.git
cd ap_i_tm
```

**Paso 2: Ejecutar la aplicación**

Puedes ejecutar directamente desde tu IDE (por ejemplo, clic en `Run` sobre `ApiApplication.java`)  
o usar Maven desde terminal:

```bash
# Windows/macOS/Linux
./mvnw spring-boot:run
```

La API quedará disponible en:  
👉 **http://localhost:8080**

🗃️ **Base de Datos:**  
La aplicación utiliza **H2 Database (en memoria)**, por lo que:
- No es necesario instalar una base de datos externa.
- Los datos se cargan automáticamente desde `src/main/resources/data.sql` al iniciar.

======================================================================
               🧠 1. RESUMEN DEL PROYECTO
======================================================================

La API de Kingdom Barber es el **núcleo de la arquitectura** y expone servicios RESTful para ser consumidos por diferentes clientes.

📱 **Cliente actual:**  
- `pi_web2.0` → Aplicación web moderna (Next.js) para agendar citas, consultar servicios, contactar, etc.

🧠 Esta arquitectura permite mantener un backend **desacoplado** de los frontends, facilitando escalabilidad y mantenimiento.

======================================================================
               🎯 2. OBJETIVOS DEL PROYECTO
======================================================================

-----------------------------
🎯 OBJETIVO GENERAL
-----------------------------

Centralizar la lógica de negocio y la persistencia del ecosistema **Kingdom Barber** en una API segura, robusta y escalable.

-----------------------------
📌 OBJETIVOS ESPECÍFICOS
-----------------------------

- ✅ **Proveer Endpoints REST claros** para operaciones CRUD.  
- 🧩 **Desacoplar los frontends** del backend para permitir evolución independiente.  
- 🚀 **Preparar una base sólida** para futuras apps móviles u otros clientes.

======================================================================
               ⚙️ 3. STACK TECNOLÓGICO
======================================================================

- 💻 **Lenguaje:** Java 17+  
- 🧱 **Framework:** Spring Boot 3.5.x  
- 🗄️ **Persistencia:** Spring Data JPA + Hibernate  
- 🧬 **Base de Datos:** H2 (en memoria)  
- 🌐 **Servidor Web:** Apache Tomcat (embebido)  
- 📦 **Dependencias:** Maven  
- 🧰 **Utilidades:** Lombok (reducción de boilerplate)

======================================================================
      🏗️ 4. ARQUITECTURA Y ESTRUCTURA DEL PROYECTO
======================================================================

Estructura principal:

```
src/main/java/com/kingdombarber/api/
├── 📂 controller/       # Controladores REST
│   ├── AgendamientoController.java
│   ├── ContactoController.java
│   ├── DatosMaestrosController.java
│   └── GaleriaController.java
│
├── 📂 model/            # Entidades JPA (tablas)
│   ├── Barbero.java
│   ├── Contacto.java
│   ├── Galeria.java
│   ├── NuevaCita.java
│   ├── Sede.java
│   └── Servicio.java
│
├── 📂 repository/       # Repositorios (interfaces JPA)
│   ├── BarberoRepository.java
│   └── ...
│
├── 📜 ApiApplication.java            # Punto de entrada principal
├── 📜 WebConfig.java                 # Configuraciones web y CORS
└── 📜 RequestLoggingInterceptor.java # Interceptor de peticiones HTTP
```

```
src/main/resources/
├── 📜 application.properties  # Configuración general
└── 📜 data.sql                # Datos precargados para desarrollo
```

======================================================================
      🌐 5. DESCRIPCIÓN DE ENDPOINTS PRINCIPALES
======================================================================

### 📂 DatosMaestrosController
- `GET /sedes` → Lista todas las sedes  
- `GET /barberos` → Lista todos los barberos  
- `GET /servicios` → Lista todos los servicios  

### 📂 AgendamientoController
- `GET /citas-activas` → Lista citas activas  
- `POST /citas-activas` → Crea nueva cita  
- `PUT /citas-activas/{id}` → Modifica cita existente  
- `DELETE /citas-activas/{id}` → Elimina una cita  

### 📂 ContactoController
- `POST /contactanos` → Envía mensaje desde el formulario de contacto  

### 📂 GaleriaController
- `GET /galeria` → Lista imágenes de la galería  
- `POST /galeria/upload` → Sube nueva imagen  
- `PUT /galeria/{id}` → Actualiza datos de imagen  
- `DELETE /galeria/{id}` → Elimina imagen (base de datos y archivo)

======================================================================
   🔁 6. FLUJO DE DATOS: CREACIÓN DE UNA CITA (FRONT → BACK)
======================================================================

1️⃣ **Usuario en Frontend (pi_web2.0)**  
→ Llena el formulario de agendamiento y envía los datos.

2️⃣ **JavaScript (React)**  
→ Construye el objeto JSON y realiza un `POST` a:  
   `http://localhost:8080/citas-activas`

3️⃣ **Controlador Java (`@PostMapping`)**  
→ Recibe la solicitud y convierte el JSON a un objeto `NuevaCita`.

4️⃣ **Lógica del controlador**  
→ Completa datos si es necesario (ej. nombre de sede) y delega al repositorio.

5️⃣ **Capa de persistencia (JPA)**  
→ Guarda la cita con `save()` en la base de datos H2.

6️⃣ **Respuesta del servidor**  
→ Devuelve un JSON con la cita registrada y un status `200 OK`.

7️⃣ **Frontend actualiza estado**  
→ React recibe el JSON, actualiza la UI y muestra confirmación al usuario.

======================================================================
        ✅ FIN DE LA DOCUMENTACIÓN TÉCNICA
======================================================================
