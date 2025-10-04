======================================================================
             💈 DOCUMENTACIÓN: AP_I_TM - KINGDOM BARBER
======================================================================

👥 **Integrantes:**  
- Juan Manuel Rivera  
- Oscar  

🏫 **Institución:**  
Instituto Tecnológico Metropolitano (ITM)  

📘 **Asignatura:**  
Estructura de Datos  

📆 **Fecha:**  
Octubre, 2025  

======================================================================
                   📘 1. RESUMEN EJECUTIVO Y VISIÓN GENERAL
======================================================================

### 1.1. Resumen del Proyecto

La **API Central de Kingdom Barber (AP_I_TM)** es el **núcleo del ecosistema digital**, desarrollada con **Java y Spring Boot**.  
Su objetivo principal es **centralizar toda la lógica de negocio y la persistencia de datos**, transformando la gestión de barberías en una plataforma **robusta, segura y escalable**.

La arquitectura se compone de un **ecosistema cohesivo y desacoplado**, donde la API actúa como **fuente única de verdad**, dando servicio a clientes front-end como:

- 🌐 **pi_web2.0 (Plataforma Web para Clientes):** Aplicación moderna en Next.js/React para agendar citas, explorar servicios y visualizar la galería de trabajos.

---

### 1.2. Planteamiento del Problema

Las barberías enfrentaban múltiples problemas debido a su dependencia de métodos manuales:

- Procesos ineficientes y lentos.  
- Comunicación fragmentada entre clientes y barberos.  
- Ausencia de análisis de datos y trazabilidad.  
- Falta de un punto central para administrar información.  

Esto resultaba en una **baja eficiencia operativa** y una **experiencia del cliente limitada**.

---

### 1.3. Solución Propuesta

**Kingdom Barber** propone una solución moderna y centralizada mediante esta API de Java.  
Su arquitectura digitaliza y optimiza las operaciones, asegurando:

- 🔒 **Seguridad y consistencia** de los datos.  
- ⚙️ **Escalabilidad** para futuras expansiones.  
- 🤝 **Integración transparente** con los clientes front-end.  
- 📊 **Base sólida** para incorporar análisis e inteligencia de negocio.

---

======================================================================
               🎯 2. OBJETIVOS DE LA API CENTRAL
======================================================================

### 2.1. Objetivo General

Desarrollar una **API RESTful robusta, segura y escalable** que **centralice toda la lógica de negocio y la persistencia de datos** del ecosistema **Kingdom Barber**, sirviendo como base para futuras extensiones como una aplicación móvil.

---

### 2.2. Objetivos Específicos

- 🧩 **Centralizar la Lógica de Negocio:**  
  Crear una API RESTful en **Java + Spring Boot** como **fuente única de verdad** para entidades como citas, clientes, barberos y servicios.  

- 🔗 **Proveer Endpoints Claros:**  
  Exponer operaciones CRUD bien definidas para cada módulo del sistema (citas, galería, contacto, etc.).  

- 🧠 **Desacoplar Clientes:**  
  Eliminar la dependencia directa de los front-end con la base de datos, asegurando independencia de capas.  

- 🔒 **Garantizar Consistencia:**  
  Mantener una sola fuente de datos sincronizada y coherente para todos los consumidores del sistema.

---

======================================================================
               🏗️ 3. ARQUITECTURA Y STACK TECNOLÓGICO
======================================================================

La API **AP_I_TM** sigue una arquitectura de **servicios desacoplados**, donde **la lógica y los datos** residen en el back-end, y la **interfaz de usuario** se comunica mediante peticiones HTTP (REST).

```
┌──────────────────────────────┐
│        API CENTRAL           │
│   Java + Spring Boot (8080)  │
│   └── Lógica y datos (H2 DB) │
└──────────────┬───────────────┘
               │
               ▼
     🌐 Plataforma Web (Next.js)
```

---

### 3.1. Stack Tecnológico Consolidado

| Capa | Tecnología | Propósito |
|------|-------------|-----------|
| 💻 Lenguaje | **Java 17+** | Lenguaje principal de desarrollo. |
| ⚙️ Framework | **Spring Boot 3.x** | Creación rápida de API REST y configuración automática. |
| 🗃️ Acceso a Datos | **Spring Data JPA / Hibernate** | ORM y operaciones CRUD. |
| 🧩 Base de Datos | **H2 Database** | Almacenamiento en memoria para desarrollo/pruebas. |
| 🌐 Servidor | **Apache Tomcat (Embebido)** | Ejecución de la API. |
| 🧰 Utilidades | **Lombok** | Reducción de código repetitivo (getters/setters). |

---

### 3.2. Estructura de Carpetas

| Carpeta | Descripción | Ejemplos |
|----------|-------------|-----------|
| `controller/` | Gestiona peticiones HTTP y define endpoints. | `AgendamientoController.java`, `GaleriaController.java` |
| `model/` | Clases `@Entity` que representan las tablas. | `NuevaCita.java`, `Barbero.java`, `Galeria.java` |
| `repository/` | Interfaces que extienden `JpaRepository`. | `CitaRepository.java`, `ServicioRepository.java` |
| `resources/` | Configuración y datos iniciales. | `application.properties`, `data.sql` |

---

======================================================================
     🧠 4. USO DE CONCEPTOS DE POO Y ESTRUCTURAS DE DATOS
======================================================================

### 4.1. Herencia  
**Veredicto:** ✅ *Sí, y es fundamental en el proyecto.*

Ejemplo:
```java
public interface CitaRepository extends JpaRepository<Cita, Long> {}
```
`CitaRepository` **hereda** de `JpaRepository`, obteniendo automáticamente métodos como `save()`, `findById()`, `findAll()` y `deleteById()`.  
Esto demuestra el uso de **herencia de interfaces** para implementar una arquitectura limpia y reutilizable.

---

### 4.2. Polimorfismo y Sobrescritura (Overriding)  
**Veredicto:** ✅ *Presentes en las clases de configuración.*

Ejemplo:
```java
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(requestLoggingInterceptor);
    }
}
```
Aquí, `WebConfig` **implementa** `WebMvcConfigurer`, sobrescribiendo métodos estándar para personalizar el comportamiento del framework.

---

### 4.3. Estructuras de Datos

| Tipo | Uso | Veredicto |
|------|-----|-----------|
| 🔹 **Arrays (String[])** | No usados directamente, pero su concepto está presente en listas. | ⚠️ |
| 🔹 **List<T>** | Retorno común de datos (`findAll()` → `List<Entity>`). | ✅ |
| 🔹 **Map / HashMap** | Implícitos en JSON y búsquedas por ID. | ✅ |
| 🔹 **Set<T>** | Usados en relaciones @ManyToMany (unicidad). | ✅ |

Ejemplo:
```java
@ManyToMany
private Set<Servicio> services;
```

---

### 4.4. Conclusión (POO y Estructuras)

El proyecto **Kingdom Barber - API Central** aplica eficazmente los pilares de la **POO** y las **estructuras de datos dinámicas**, garantizando una arquitectura **modular, mantenible y escalable**.

---

======================================================================
               🌐 5. DESCRIPCIÓN DE ENDPOINTS PRINCIPALES
======================================================================

### 📅 AgendamientoController
| Método | Endpoint | Descripción |
|---------|-----------|-------------|
| GET | `/citas-activas` | Devuelve todas las citas activas. |
| POST | `/citas-activas` | Crea una nueva cita. |
| PUT | `/citas-activas/{id}` | Modifica una cita existente. |
| DELETE | `/citas-activas/{id}` | Elimina una cita por ID. |

---

### 🖼️ GaleriaController
| Método | Endpoint | Descripción |
|---------|-----------|-------------|
| GET | `/galeria` | Devuelve las imágenes en Base64. |
| POST | `/galeria/upload` | Sube y guarda una nueva imagen. |
| PUT | `/galeria/{id}` | Modifica los datos de una imagen. |
| DELETE | `/galeria/{id}` | Elimina una imagen. |

---

### 🧾 DatosMaestrosController
| Método | Endpoint | Descripción |
|---------|-----------|-------------|
| GET | `/sedes` | Devuelve todas las sedes. |
| GET | `/barberos` | Devuelve los barberos registrados. |
| GET | `/servicios` | Devuelve los servicios disponibles. |

---

### 💬 ContactoController
| Método | Endpoint | Descripción |
|---------|-----------|-------------|
| POST | `/contactanos` | Registra un mensaje del formulario web. |

---

======================================================================
         🔄 6. FLUJO DE DATOS TÍPICO: CREACIÓN DE UNA CITA
======================================================================

1️⃣ **Front-End (pi_web2.0):**  
El usuario agenda una cita → React envía un JSON vía POST a `http://localhost:8080/citas-activas`.  

2️⃣ **Recepción (API Java):**  
El `AgendamientoController` recibe y mapea el JSON al objeto `NuevaCita`.  

3️⃣ **Lógica de Negocio:**  
Se enriquece el objeto con datos del barbero y la sede.  

4️⃣ **Persistencia (JPA):**  
Se ejecuta `repository.save()`, generando un `INSERT INTO` en H2.  

5️⃣ **Respuesta:**  
La API devuelve el objeto creado como JSON con código `200 OK`.  

6️⃣ **Front-End:**  
React actualiza el estado y renderiza la cita en el calendario del usuario.

---

======================================================================
        ⚙️ 7. DESAFÍOS Y LECCIONES APRENDIDAS
======================================================================

### 🧩 A. CORS e Integración
Configurar correctamente **CORS** fue esencial para permitir peticiones desde el front-end (`localhost:3000`).  

### 🧠 B. Manejo de Archivos Base64
Inicialmente las imágenes daban errores `400 Bad Request`.  
**Solución:** convertir y almacenar las imágenes en **Base64** directamente en la base de datos → cero conflictos de rutas o permisos.  

### 🔒 C. Contrato de API
Se mantuvo un “contrato” formal de endpoints y estructuras JSON entre backend y frontend para evitar errores en producción.  

---

======================================================================
                   🏁 8. CONCLUSIONES FINALES
======================================================================

- 🧠 **Evolución Arquitectónica:**  
  Se consolidó la API como el eje central del ecosistema Kingdom Barber.  

- 🔗 **Consistencia Global:**  
  Todos los clientes consumen una única fuente de datos.  

- ⚙️ **Escalabilidad y Mantenimiento:**  
  La arquitectura modular permite incorporar nuevas capas (como una app móvil).  

- 💪 **Logro Técnico:**  
  Integración exitosa entre **Java/Spring**, **React/Next.js** y **Python/Streamlit**.  

---

El proyecto **AP_I_TM - Kingdom Barber** representa un paso firme hacia una **plataforma digital completa**, mostrando dominio en programación orientada a objetos, diseño de APIs y buenas prácticas de desarrollo backend.

======================================================================
                     ✨ FIN DEL DOCUMENTO
======================================================================
