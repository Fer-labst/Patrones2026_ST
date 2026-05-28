# Patrones2026_ST

## Descripción General del Sistema
Este proyecto corresponde al modelado completo de un **Sistema de Gestión de Turnos de Atención Medicó**, enfocado en la toma de turnos e ingreso de datos de los pacientes.

----
## Objetivos del Modelado
- Desarrollar una transición completa desde la visión funcional hasta el despliegue físico.
----

## 1. Diagrama de Casos de Uso UML

<img width="1216" height="961" alt="" src="https://github.com/Fer-labst/Patrones2026_ST/blob/main/imagenes/Caso%20de%20uso.png" />

## Descripción General
En el analisis funcional nos permitio identificar a los actores involucrados y las funcionalidades críticas del sistema. Además, se aplicaron correctamente **relaciones de `<<include>>` y `<<extend>>`** para reflejar flujos obligatorios y opcionales en el proceso.

## Actores Identificados
Paciente: Responsable de utilizar el sistema para pedir un turno para una consulta medica.
Recepcionista: Responsable de realizar el proceso del paciente si este no sabe realizarlo o es incapaz de tomar un turno por cualquier otro motivo.

## Casos de uso destacados y relaciones aplicadas:
- **Ingresar datos**
  - `<<include>>` **Pedir Turno**: El usuario despues de ingresar sus datos se le permite poder sacar un turno.
  - `<<include>>` **Reprogramar Turno**: El usuario despues de ingresar sus datos se le permite reprogramar su turno para otro momento.
  - `<<include>>` **Cancelar Turno**: El usuario despues de ingresar sus datos se le permite cancelar su turno si lo encuentra necesario.
- **Pedir Turno**
  - `<<include>>` **Verificar disponibilidad**: El sistema revisa si hay turnos disponibles.
- **Reprogramar Turno**
  - `<<include>>` **Verificar disponibilidad**: El sistema revisa si es posible modificar el turno ya existente.
- **Verificar disponibilidad**
  -  `<<include>>` **Enviar Confirmación**: Se le envia una confirmación al usuario para confirmar que su turno fue sacado exitosamente.
- **Enviar Confirmación**
  - `<<extend>>` **Enviar Recordatorio**: Se le envia al usuario un recordatorio sobre la hora que tomo.
- **Ingresar datos paciente**
  - `<<include>>` **Pedir Turno**: La Recepcionista ingresa los datos del usuario para poder pedir el turno para el.
- **Pedir Turno**
  -  `<<include>>` **Enviar Confirmación**: Se le envia una confirmación al usuario para confirmar que su turno fue sacado exitosamente.
- **Enviar Confirmación**
  - `<<extend>>` **Enviar Recordatorio**: Se le envia al usuario un recordatorio sobre la hora que tomo.

## Justificación de las relaciones aplicadas:
- Se utilizaron `<<include>>` en procesos donde el caso de uso base **siempre depende de otro caso obligatorio**, como en el **Ingreso de datos y Enviar confirmación.**
- Se aplicaron `<<extend>>` en procesos donde las acciones son **condicionadas o opcionales**, como **Enviar Recordatorio.**

## 2. Diagrama de Clases UML con Patrones Aplicados

<img width="1216" height="961" alt="" src="https://github.com/Fer-labst/Patrones2026_ST/blob/main/imagenes/Diagrama%20de%20Clases.png" />

### **1. Singleton (`ContadorHoras`)**
## Justificación:
Se seleccionó Singleton para la **gestión centralizada de las horas disponibles** para agregar o restar las horas que han sido reclamadas o canceladas y que el sistema pueda verificar de manera mas facil las horas que esten disponibles en ese dia.  
Este patrón permite garantizar que **exista una única instancia accesible globalmente**.

## Intención arquitectónica:
- Centralizar el control de las horas disponibles.

---

### **2. Prototype (`PlantillaDatos`)**
## Justificación:
La atención hospitalaria exige rapidez y eficiencia en la gestión de movimientos repetitivos.  
Se implementó Prototype para **permitir la clonación de plantillas de datos de los pacientes** para agilizar el ingreso de datos de los pacientes.

#### Intención arquitectónica:
- Permitir la creación rápida de nuevas instancias de movimientos desde plantillas base.
- Reducir la complejidad y tiempo de operaciones manuales.

---

## **3. Bridge (`InterfazUsuario`)**
## Justificación:
Considerando la diversidad de usuarios permitiendo adaptar la experiencia según el usuario y el dispositivo utilizado, sin afectar la lógica central del sistema.

## Intención arquitectónica:
- Garantizar independencia entre interfaz y lógica.

---
## 3. Diagrama de Implementación UML

<img width="1216" height="961" alt="" src="https://github.com/Fer-labst/Patrones2026_ST/blob/main/imagenes/Diagrama%20de%20Implementaci%C3%B3n.png" />

## Despliegue Físico
- **Nodos físicos diferenciados**.
- Separación clara de responsabilidades entre el servidor y el tunomaticó.
