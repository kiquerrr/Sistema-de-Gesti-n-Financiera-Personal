# ROADMAP.md: Sistema de Gestión Financiera Personal

Este documento es la hoja de ruta para el desarrollo del Sistema de Gestión Financiera. Cada ítem es una tarea que debe ser completada. Marca cada tarea con una `[x]` una vez que esté finalizada.

## Fase 0: Planificación y Arquitectura (El Cimiento)

* [ ] **Definición del Stack Tecnológico:**
    * [ ] **Backend:** Decidir los lenguajes/frameworks para los módulos (Ej: Python con FastAPI, Node.js con Express).
    * [ ] **Base de Datos:** Elegir el motor de base de datos (Ej: PostgreSQL, MongoDB).
    * [ ] **Frontend:** Seleccionar la tecnología para la interfaz de usuario (Ej: React, Vue, Svelte).
    * [ ] **Cloud/Hosting:** Decidir la plataforma de despliegue (Ej: Vercel, Heroku, AWS).
* [ ] **Configuración del Entorno de Desarrollo:**
    * [ ] Crear el repositorio en **GitHub**.
    * [ ] Estructurar las carpetas del proyecto (`/backend`, `/frontend`, `/docs`, `/changelogs`).
    * [ ] Inicializar este archivo (`ROADMAP.md`) en la raíz del proyecto.
    * [ ] Crear el archivo `.gitignore` para excluir archivos innecesarios (ej: `node_modules`, `__pycache__`).
* [ ] **Diseño de la Arquitectura (Modular):**
    * [ ] **Diagrama de Módulos/Microservicios:** Dibujar cómo se comunicarán los servicios.
        * Servicio de Transacciones
        * Servicio de Divisas
        * Servicio de Autenticación y Usuarios
        * Servicio de Reportes y Auditoría
        * API Gateway
* [ ] **Diseño de la Base de Datos (Schema):**
    * [ ] Diseñar la tabla/colección `transactions` (monto, moneda, fecha, hora, tipo, descripción, id_cuenta, id_entidad, id_tasa_cambio).
    * [ ] Diseñar la tabla/colección `accounts` (nombre, banco, tipo, moneda_principal).
    * [ ] Diseñar la tabla/colección `entities` (nombre, tipo [proveedor, cliente, personal]).
    * [ ] Diseñar la tabla/colección `exchange_rates` (fecha, hora, tasa_oficial, tasa_paralela, fuente_paralela, medio_operacion).
    * [ ] Diseñar la tabla/colección `exchange_operations` (id_transaccion_origen, id_transaccion_destino, porcentaje_perdida_ganancia, tipo [venta_divisa, compra_divisa]).
    * [ ] Diseñar la tabla/colección `audit_log` (usuario, tabla_afectada, accion, datos_viejos, datos_nuevos, fecha_hora).

---

## Fase 1: Desarrollo del Núcleo del Backend (El Motor)

* [ ] **Módulo de Divisas y Tasas de Cambio:**
    * [ ] Crear endpoints CRUD para `exchange_rates`.
    * [ ] Integrar (opcional) un servicio externo para obtener tasas oficiales automáticamente.
* [ ] **Módulo de Cuentas y Entidades:**
    * [ ] Crear endpoints CRUD para `accounts`.
    * [ ] Crear endpoints CRUD para `entities`.
* [ ] **Módulo de Transacciones (Core):**
    * [ ] Crear endpoint para **registrar un ingreso** (Bolívares o Divisa).
    * [ ] Crear endpoint para **registrar un egreso**.
    * [ ] Lógica para asociar cada transacción a una cuenta y una entidad.
    * [ ] Validar que los datos de la transacción sean consistentes.
* [ ] **Módulo de Conversión de Divisas:**
    * [ ] Crear un endpoint específico para registrar una **operación de cambio** (venta o compra de divisa).
    * [ ] Este endpoint debe generar dos transacciones internamente (una de egreso en una moneda y otra de ingreso en la otra).
    * [ ] Calcular y almacenar el **porcentaje de pérdida/ganancia** en la tabla `exchange_operations`.
    * [ ] Registrar si la operación fue para proteger contra la inflación o si resultó en una pérdida/ganancia real.

---

## Fase 2: Desarrollo de la Interfaz de Usuario (El Tablero de Control)

* [ ] **Diseño Básico de la Interfaz (UI/UX):**
    * [ ] Crear bocetos (wireframes) de las pantallas principales (Dashboard, Registro de Transacción, Reportes).
* [ ] **Conexión con el Backend:**
    * [ ] Configurar el cliente para que se comunique con la API del backend.
* [... ] **Desarrollo de Componentes:**
    * [ ] Crear formulario para **añadir ingresos/egresos**.
    * [ ] Crear formulario específico para **registrar operaciones de cambio de divisa**.
    * [ ] Crear una tabla o lista para visualizar las transacciones recientes.
    * [ ] Crear un dashboard principal que muestre saldos actuales por cuenta y un resumen del día.
    * [ ] Crear vistas para gestionar Cuentas y Entidades.
* [ ] **Integración de Funcionalidades:**
    * [ ] Conectar los formularios a los endpoints del backend.
    * [ ] Mostrar los datos recibidos del backend en el dashboard y las listas de transacciones.

---

## Fase 3: Funcionalidades Avanzadas (Inteligencia y Control)

* [ ] **Módulo de Auditoría y Logs:**
    * [ ] Implementar lógica en el backend para que cada cambio (Crear, Actualizar, Borrar) en tablas críticas se registre en `audit_log`.
    * [ ] Crear una vista en el frontend para poder consultar el `audit_log` con filtros.
* [ ] **Módulo de Reportes:**
    * [ ] Desarrollar endpoints en el backend para generar reportes:
        * [ ] Flujo de caja por período (día, semana, mes).
        * [ ] Gastos por categoría o entidad.
        * [ ] Ingresos por categoría o entidad.
        * [ ] Análisis de pérdidas/ganancias por cambio de divisa.
    * [ ] Crear las vistas correspondientes en el frontend para visualizar estos reportes, preferiblemente con gráficos.

---

## Fase 4: Despliegue y Mantenimiento

* [ ] **Preparación para Producción:**
    * [ ] Configurar variables de entorno (claves de API, credenciales de BD).
    * [ ] Escribir Dockerfiles para contenedorizar las aplicaciones (backend/frontend).
* [ ] **Despliegue:**
    * [ ] Subir el backend a la plataforma elegida.
    * [ ] Subir el frontend a la plataforma elegida.
    * [ ] Configurar el dominio y el DNS si aplica.
* [ ] **Mantenimiento y Mejoras:**
    * [ ] Configurar un sistema de monitoreo y alertas de errores.
    * [ ] Implementar un sistema de copias de seguridad automáticas de la base de datos.
    * [ ] Planificar e implementar nuevas funcionalidades basadas en el uso.
