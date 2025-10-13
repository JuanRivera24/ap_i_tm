======================================================================
💈 DOCUMENTACIÓN: AP_I_TM - KINGDOM BARBER
======================================================================

👥 Integrantes:
  - Juan Manuel
  - Oscar
  - Juan Fernando

🏫 Institución: Instituto Tecnológico Metropolitano (ITM)
📘 Asignatura: Estructura de Datos
📆 Fecha: Octubre, 2025

======================================================================
                      🚀 INFORMACIÓN DE DESPLIEGUE
======================================================================

🌐 Plataforma: Vercel (https://vercel.com/)  
🔗 URL Pública: https://front-beta-sable.vercel.app 
🌐 Plataforma: Render (https://render.com/)  
🧩 API Consumida: https://ap-i-tm.onrender.com  
📦 Estado: Activo y en Producción  

======================================================================
📘 1. RESUMEN EJECUTIVO Y VISIÓN GENERAL
======================================================================

1.1. Resumen del Proyecto:
  La API Central de Kingdom Barber (AP_I_TM) es el núcleo del ecosistema digital, desarrollada con Java y Spring Boot.
  Su objetivo principal es centralizar la lógica de negocio y la persistencia de datos, convirtiendo la gestión de barberías
  en una plataforma moderna, segura y escalable.
  La arquitectura es desacoplada y la API actúa como fuente única de verdad (Single Source of Truth), sirviendo a clientes front-end como:
    - 🌐 Front (Plataforma Web - Next.js/React): Para agendar citas, explorar servicios y visualizar la galería.

1.2. Planteamiento del Problema:
  Las barberías enfrentaban dificultades por procesos manuales:
    - Procesos ineficientes y errores de agendamiento.
    - Comunicación fragmentada entre barberos y clientes.
    - Falta de análisis de datos o métricas.
    - Sin trazabilidad ni historial del cliente.
  Esto generaba baja eficiencia y una experiencia obsoleta.

1.3. Solución Propuesta:
  Kingdom Barber propone una API que:
    - 🔒 Centraliza y asegura la información.
    - ⚙️ Permite escalabilidad hacia nuevas plataformas.
    - 🤝 Facilita integración mediante API REST.
    - 📊 Permite análisis y toma de decisiones estratégicas.

======================================================================
🎯 2. OBJETIVOS DE LA API CENTRAL
======================================================================

2.1. Objetivo General:
  Desarrollar una API RESTful robusta, segura y escalable que centralice la lógica de negocio y los datos del ecosistema Kingdom Barber.

2.2. Objetivos Específicos:
  - 🧩 Centralizar la lógica del negocio (citas, clientes, barberos, servicios).
  - 🔗 Exponer endpoints RESTful claros para CRUD y operaciones clave.
  - 🧠 Desacoplar el front-end de la base de datos.
  - 🔒 Garantizar la integridad y consistencia de los datos en todas las capas.

======================================================================
🏗️ 3. ARQUITECTURA Y STACK TECNOLÓGICO
======================================================================

La API sigue una arquitectura de servicios desacoplados, donde toda la lógica y datos residen en el back-end, y los clientes se comunican vía HTTP/REST.

Diagrama General:
  ┌──────────────────────────────┐
  │        API CENTRAL (Back-End)│
  │   Java + Spring Boot (Render)│
  │   └── Lógica de Negocio      │
  │   └── Acceso a Datos (JPA)   │
  └──────────────┬───────────────┘
                 │
        (HTTP/JSON Requests)
                 │
                 ▼
  ┌──────────────────────────────┐
  │     CLIENTE (Front-End)      │
  │     Next.js / React (Vercel) │
  └──────────────────────────────┘

3.1. Stack Tecnológico Consolidado:
  💻 Lenguaje: Java 17+
  ⚙️ Framework: Spring Boot 3.x
  🗃️ Acceso a Datos: Spring Data JPA / Hibernate
  🧩 Base de Datos: H2 Database (en desarrollo)
  🌐 Servidor: Apache Tomcat (embebido)
  🧰 Utilidades: Lombok (para reducir código repetitivo)

3.2. Estructura de Carpetas:
  controller/  →  Controladores REST (manejan peticiones HTTP)
  model/       →  Entidades @Entity (tablas de la BD)
  repository/  →  Repositorios JPA (CRUD automático)
  resources/   →  Configuración y scripts de datos (application.properties, data.sql)

======================================================================
🧠 4. USO DE CONCEPTOS DE POO Y ESTRUCTURAS DE DATOS
======================================================================

4.1. Herencia:
  ✅ Presente.  
  CitaRepository hereda de JpaRepository y obtiene métodos CRUD automáticamente.

  Ejemplo:
    public interface CitaRepository extends JpaRepository<Cita, Long> {}

4.2. Polimorfismo y Sobrescritura:
  ✅ Presente en configuraciones personalizadas.

  Ejemplo:
    public class WebConfig implements WebMvcConfigurer {
        @Override
        public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/**").allowedOrigins("*");
        }
    }

4.3. Estructuras de Datos:
  - 🔹 Arrays: No usados directamente (⚠️)
  - 🔹 List<T>: Estructura principal para devolver colecciones (✅)
  - 🔹 Map / HashMap: Usado en serialización JSON (✅)
  - 🔹 Set<T>: Garantiza unicidad en relaciones @ManyToMany (✅)

======================================================================
🌐 5. ENDPOINTS PRINCIPALES
======================================================================

📅 AgendamientoController:
  - GET /citas-activas → Lista todas las citas activas.
  - POST /citas-activas → Crea una nueva cita.
  - PUT /citas-activas/{id} → Actualiza una cita existente.
  - DELETE /citas-activas/{id} → Elimina una cita.

🖼️ GaleriaController:
  - GET /galeria → Devuelve las imágenes en Base64.
  - POST /galeria/upload → Sube una nueva imagen.
  - PUT /galeria/{id} → Modifica descripción/categoría.
  - DELETE /galeria/{id} → Elimina imagen de la base de datos.

🧾 DatosMaestrosController:
  - GET /sedes → Lista todas las sedes.
  - GET /barberos → Lista todos los barberos.
  - GET /servicios → Lista todos los servicios.

💬 ContactoController:
  - POST /contactanos → Recibe y guarda mensajes del formulario.

======================================================================
🔄 6. FLUJO DE DATOS: CREACIÓN DE UNA CITA
======================================================================

1️⃣ Front-End (pi_web2.0): Usuario completa el formulario.  
2️⃣ Se envía una petición POST JSON → `/citas-activas`.  
3️⃣ Spring Boot mapea el JSON a un objeto Java.  
4️⃣ El controlador valida y guarda usando `repository.save()`.  
5️⃣ Hibernate ejecuta el `INSERT INTO` en la base de datos.  
6️⃣ La API responde con el JSON del nuevo registro (200 OK).  
7️⃣ El front-end actualiza la interfaz y muestra la nueva cita.

======================================================================
🚀 7. DESPLIEGUE Y PRODUCCIÓN
======================================================================

🐳 Contenerización: Implementada con Dockerfile para empaquetar la app.  
☁️ Plataforma PaaS: Desplegada en Render.com.  
🔄 CI/CD: Render compila automáticamente al hacer push en `main`.  
🔑 Variables de Entorno: Configuradas de forma segura en Render.  
🌍 URL Pública: https://ap-i-tm.onrender.com

======================================================================
⚙️ 8. DESAFÍOS Y LECCIONES APRENDIDAS
======================================================================

A. Configuración de CORS:
  - Problema: Bloqueo de peticiones entre dominios (Vercel ↔ Render).
  - Solución: Implementación manual de políticas CORS en Spring Boot.

B. Imágenes Base64:
  - Problema: Respuestas JSON pesadas.
  - Solución: Se propone migrar a almacenamiento en la nube (ej. AWS S3).

C. Arranque en Frío (Cold Start):
  - Problema: Render “duerme” instancias inactivas.
  - Solución: Se recomienda plan pago o mantener pings periódicos.

D. Mapeo de Entidades:
  - Problema: Relaciones @ManyToMany generaban bucles JSON.
  - Solución: Uso de @JsonIgnore y optimización de FetchType.

======================================================================
🏁 9. CONCLUSIONES FINALES
======================================================================

✅ Evolución Arquitectónica: API consolidada como fuente única de verdad.  
🔗 Consistencia: Sincronización total entre front-end y back-end.  
⚙️ Escalabilidad: Lista para expandirse a móvil o nuevos módulos.  
💪 Logro Técnico: Integración completa entre Java, React y Spring Boot.  

El proyecto AP_I_TM - Kingdom Barber demuestra dominio en POO, diseño de APIs RESTful y despliegue profesional.

======================================================================
✨ FIN DEL DOCUMENTO
======================================================================
