# Sistema de Turnos Digital
Nombres
> VICENTE RODRIGUEZ CANCINO - GONZALO MATURANA CRUZES

## Descripción General del Sistema

Este sistema es una versión digitalizada del tradicional sistema de tickets enumerados que todos conocemos. El objetivo principal de este sistema es organizar el flujo de personas que esperan la atención del servicio solicitado.

El sistema abarca ciertos aspectos operacionales como:
- La generación única y ordenada de turnos.
- Asignación de turnos a servicios.
- Notificación al usuario.
- Gestión del tiempo estimado de espera.

---

## 1. Diagrama de Casos de Uso UML

![Caso de uso](https://viroca.cl/patrones/16052025/CASO_DE_USO_PDD.jpg)
> Nota: No se si se vea el diagrama de uso o el diagrama de clases, si no se ven haz los cambios que necesites nomas

### Descripción general

Nuestro análisis permitió identificar los actores involucrados y las funcionalidades del sistema, aplicando correctamente relaciones de `<<include>>` y `<<extend>>` para plasmar las funciones del proceso. 

#### Actores identificados:
- Cliente: Responsable de las acciones de solicitud de número de turno, ver número de turno actual y la anulación del número de turno.
- Empleado: Marca los números de turno atendidos y llama al siguiente número en la cola.

#### Casos de uso destacados y relaciones aplicadas:
- `<<include>>` **Asignar número de turno**: De manera automática y obligatoria se le debe de asignar un número de turno al solicitante.
- `<<extend>>` **Enviar notificación**: La opción de recibir una notificación cuando sea el turno del solicitante siempre será opcional, tanto al solicitar el número de turno, como al ver el número de turno actual.
- `<<include>>` **Llamar al siguiente número de turno**: Al marcar el número de turno como atendido, de manera obligatoria se debe llamar al siguiente número en espera.

#### Justificación de las relaciones aplicadas:
- Se utilizaron `<<include>>` en procesos donde el caso de uso **debe de ocurrir obligatoriamente cuando el caso de uso base sucede**, como en el caso de **Solicitar número de turno**, donde se le asigna un número de turno al solicitante.
- Se utilizó `<<extend>>` en el proceso donde las acciones **no necesariamente deben de suceder para que el sistema completo opere de manera correcta**, como el caso de **Enviar notificación**, donde es completamente decisión del solicitante si desea recibir una notificación cuando sea su turno. 

## 2. Diagrama de Clases UML con Patrones Aplicados

![image](https://www.plantuml.com/plantuml/png/hLN1RjGm4BtdAwnUcWYsubo9gWY1n84AQVS7fixiof2C8tjsrGhwHNm2jtuP4xkXurYe7CYbYkUzcJVFBztho13uE0vDCu7z1WSqPriN6KSmFPhTCP2FP-PxO-In0yHedigvb2hvsHX7qesi0tDPeXI6vuEFODc7Uu7jrAj2aMUtTnPw7mHqy_ocCCM4jljJUMKEo9yMAMrNYr50mW0XdRSHmybPvsSy1qU7Rj6N60-DyY0T5xjRJvpalZLlXEU8zJh74OElZgk9IjfVDBqkUgsMlacbjil5ihRDdLArdcO7JzYk5tvGeVWo0B4RP7ipGO1LCcGSXZrODE-b4zmEk7Qedb6P-ZoYjfVyU1kmbAu2jJHLutIoYdJOWCkLivjUkEwivEBYnvNUB6CgmPlDLIP8fyUVnmYFlmeFbnnRvmbhxtJE2-UGJWv2Eo95-8eg2pr6TWGCOHNRatTzRV2IWUtdxOSxHkMn6YF5DcTiXmFkFUdmCTxnlqnwryEKFWVfPjmu3IZYETORhhw46NvPwzJtgbktB_6w_-gY7fqkknueB4YeYf12f0sOet5U_ZFjSKBgKVwgR3r5whxWbZpHeWYh2DPOtKdXclFCj06bOYOfuc1YPjTTLDI5aHfSY_hvj-Gt)

## Justificación Arquitectónica y Patrones Aplicados

### Selección de patrones
Decidimos implementar 3 de los 4 patrones de diseño que hemos visto en clases, los cuales son los siguientes:

### **1. Singleton (`SistemaTurnos`)**
#### Justificación:
Se utilizó Singleton para el **Sistema de Turnos** para tener una instancia única y central para administrar todos los turnos y coordine el proceso de atención.

#### Intención arquitectónica:
- Asegura que exista una sola instancia global accesible por todo el sistema.
- Centraliza el control de generación de turnos y notificaciones.
- Previene errores por múltiples instancias que estén gestionando turnos en paralelo.

### **2. Prototype (`PlantillasTurno` y `Turno`)**
#### Justificación:
Utilizamos Prototype para poder crear nuevos turnos a través de una plantilla predefinida, quitando la necesidad de crear una nueva cada vez que se crea un turno nuevo.

#### Intención arquitectónica:
- Permite la creación rápida de instancias similares.
- Facilita la definición de plantillas por tipo de servicio.

### **3. Adapter (`AdaptadorSMS`)**
#### Justificación:
Utilizamos este patrón el cual actuará como traductor para poder utilizar servicios externos.

#### Intención arquitectónica:
- Permite que el sistema trabaje de manera correcta, independiente del proveedor externo.
- Facilita el cambio de métodos de notificación.

## 3. Diagrama de Implementación UML


![Diagrama de Implementacion](https://viroca.cl/patrones/16052025/imagen_PDD.png)
#### Justificación: 
_Utilizamos una arquitectura de tres capas para separar la lógica del sistema, la interfaz del usuario y la base de datos, facilitando el mantenimiento y la escalabilidad. Además, empleamos un adaptador para integrar servicios externos de notificaciones sin acoplar el sistema a un proveedor específico._


#### Intención arquitectónica:

_La intención arquitectónica del diagrama de implementación es mostrar cómo los componentes de software del sistema se distribuyen físicamente sobre la infraestructura de hardware, es decir, visualizar la relación entre el software y el hardware donde se desplegará._

_Dónde (en qué nodos/dispositivos/servidores) se ejecutan los distintos artefactos de software.
Cómo se comunican estos nodos entre sí.
Qué dependencias externas existen.
Cómo se organiza la infraestructura para soportar los requisitos de escalabilidad, seguridad, mantenimiento y disponibilidad._
