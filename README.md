# Práctica 1 — Introducción a MongoDB Atlas y Creación de Base de Datos

**Asignatura:** Base de Datos No Relacionales  
**Semestre:** 4°  
**Alumno:** Carrillo Hernández Hugo Iván 

## 📝 Descripción de la Práctica

En esta práctica se realizó la introducción al ecosistema de **MongoDB Atlas**, el servicio en la nube oficial para gestionar bases de datos NoSQL. El objetivo principal fue comprender la diferencia entre bases de datos relacionales y las orientadas a documentos, así como configurar un entorno de desarrollo en la nube.

Todo el proceso consistió en:
1.  **Creación de Cuenta y Proyecto:** Se registró una cuenta institucional y se configuró un proyecto llamado `Practica1_[Nombre]`.
2.  **Despliegue del Clúster:** Se configuró un clúster gratuito (M0 Sandbox) utilizando AWS como proveedor de nube.
3.  **Seguridad:** Se establecieron las reglas de acceso, creando un usuario administrador de base de datos y configurando la lista blanca de IP (Network Access) para permitir conexiones remotas.
4.  **Gestión de Datos:** Se creó la base de datos `Practica1BD` y la colección `estudiantes`, donde se realizaron operaciones de manipulación de datos directamente desde la interfaz gráfica de Atlas (Data Explorer).

## ⚙️ Explicación de Operaciones CRUD

CRUD es el acrónimo de las cuatro operaciones fundamentales en una base de datos: **C**reate (Crear), **R**ead (Leer), **U**pdate (Actualizar) y **D**elete (Eliminar). A continuación, se explica cómo se aplicaron en esta práctica:

### 1. Create (Insertar)
Consiste en agregar nuevos documentos a la colección. En MongoDB, los datos se guardan en formato JSON (BSON).
*   **En la práctica:** Insertamos 5 documentos con información de alumnos (matrícula, nombre, edad, grupo y especialidad).
*   **Ejemplo del documento:**
    ```json
    {
      "matricula": "2026001",
      "nombre": "Luis",
      "edad": 18,
      "grupo": "4010",
      "especialidad": "Programación"
    }
    ```

### 2. Read (Consultar)
Permite buscar y filtrar información dentro de la base de datos.
*   **En la práctica:** Utilizamos la barra de filtros de Atlas para realizar consultas específicas.
*   **Ejemplos utilizados:**
    *   *Ver todos:* `{}`
    *   *Filtrar por edad (mayores de 17):* `{ "edad": { "$gt": 17 } }`
    *   *Filtrar por grupo:* `{ "grupo": "4010" }`
 
    (En la captura se observa de manera organizada en una gráfica

### 3. Update (Actualizar)
Se refiere a la modificación de datos existentes en un documento.
*   **En la práctica:** Seleccionamos un estudiante específico y editamos el campo `edad`, cambiándolo de 18 a 19 años para reflejar una corrección o actualización de datos.

### 4. Delete (Eliminar)
Es la acción de borrar registros de la base de datos de forma permanente.
*   **En la práctica:** Se seleccionó un documento de la lista de estudiantes y se eliminó utilizando la opción de la interfaz gráfica, confirmando la acción para asegurar la integridad de los datos restantes.

---

## 📸 Evidencias

<img width="1430" height="748" alt="coleccion" src="https://github.com/user-attachments/assets/f89c52a2-02b4-4d0d-aa44-ed740b9b9e17" />
<img width="1193" height="666" alt="documentos insertados" src="https://github.com/user-attachments/assets/2ac3ae4d-c544-4b0a-8932-73c82824f25c" />
<img width="1431" height="693" alt="Filtros aplicados" src="https://github.com/user-attachments/assets/9f2583b5-dbf9-4071-b48e-aa536a50dce4" />
<img width="1152" height="515" alt="protectoatlas" src="https://github.com/user-attachments/assets/b922feb3-1a6c-42fc-b267-3735579d24a2" />
<img width="1141" height="611" alt="clustercreado" src="https://github.com/user-attachments/assets/e165918a-3465-46bf-b1d0-b0be62d7a4a7" />
<img width="1169" height="280" alt="Usuario configurado" src="https://github.com/user-attachments/assets/adafa6ae-cf75-4bf9-b5ed-b21ba03007fc" />
