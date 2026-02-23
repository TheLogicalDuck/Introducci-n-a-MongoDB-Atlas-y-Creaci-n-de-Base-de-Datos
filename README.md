# Práctica 1 — Introducción a MongoDB Atlas y Creación de Base de Datos

**Asignatura:** Base de Datos No Relacionales  
**Semestre:** 4°  
**Alumno:** Carrillo Hernández Hugo Iván 

## 📝 Descripción de la Práctica

En esta práctica se realizó la introducción al ecosistema de **MongoDB Atlas**, el servicio en la nube oficial para gestionar bases de datos NoSQL. El objetivo principal fue comprender la diferencia entre bases de datos relacionales y las orientadas a documentos, así como configurar un entorno de desarrollo en la nube.

Todo el proceso consistió en:
1.  **Creación de Cuenta y Proyecto:** Se registró una cuenta institucional y se configuró un proyecto llamado `Practica1Carrillohernandez`.
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


### 🔎 SECCIÓN A — ANÁLISIS Y DISEÑO
🧠 Actividad 1 — Pensamiento estructural
¿Qué problema resolverá tu base de datos?
Resolverá la necesidad de gestionar la información académica y administrativa de los estudiantes de un plantel, permitiendo un acceso rápido a sus datos personales, materias cursadas y estatus actual.
¿Qué tipo de información almacenará?
Almacenará datos alfanuméricos (nombres, matrículas), numéricos (edades, promedios), lógicos (si están activos o no) y listas de datos (materias).
¿Qué entidades principales existirán?
La entidad principal es Estudiantes. Al ser una base NoSQL orientada a documentos, no necesitamos tablas separadas para "Materias" o "Contactos" obligatoriamente, ya que pueden vivir dentro del documento del estudiante.
¿Qué campos mínimos debe tener cada documento?
Matrícula, nombre, edad, grupo, especialidad, materias, promedio, estatus activo y fecha de registro.
¿Qué tipo de datos tendrá cada campo?
String: matrícula, nombre, grupo, especialidad.
Number: edad, promedio.
Boolean: activo.
Array: materias.
Date: fecha_registro.
🏗 Actividad 2 — Diseño del Documento Base (Reflexiones)
¿Por qué materias es un array?
Porque un estudiante cursa más de una materia a la vez. Un array (arreglo) nos permite guardar una lista de varios elementos (ej. ["Base de Datos", "Inglés"]) dentro del mismo campo, evitando tener que crear campos como "materia1", "materia2".
¿Por qué activo es boolean?
Porque el estado de un alumno es binario: o está activo (True) o dado de baja (False). Es el tipo de dato más eficiente para este tipo de validaciones lógicas.
¿Por qué no usamos esquema rígido como en SQL?
Para tener flexibilidad. En el futuro podríamos necesitar agregar un campo nuevo solo a algunos alumnos (como "beca" o "tutor") y MongoDB nos permite hacerlo sin romper la base de datos ni tener que rediseñar toda la estructura, cosa que en SQL sería muy complejo.
### ☁ SECCIÓN B — IMPLEMENTACIÓN EN MONGODB ATLAS
🔧 Actividad 3 — Creación Técnica (Explicaciones)
¿Qué es un cluster?
Es un conjunto de servidores (nodos) que trabajan juntos para alojar la base de datos. En MongoDB, un cluster asegura que si un servidor falla, otro tome su lugar (alta disponibilidad) y permite distribuir la carga de datos.
¿Por qué Atlas es considerado DBaaS (Database as a Service)?
Porque es un servicio gestionado en la nube. Nosotros no nos preocupamos por instalar el software, actualizar servidores, configurar la seguridad física o hacer copias de seguridad manuales; MongoDB Atlas (el proveedor) se encarga de toda la infraestructura y nosotros solo "consumimos" el servicio de base de datos.
¿Qué ventaja tiene trabajar en la nube?
Accesibilidad (puedes conectarte desde cualquier lugar), escalabilidad (puedes aumentar la potencia con un clic), seguridad gestionada y ahorro de costos al no tener que comprar y mantener servidores físicos propios.
### 🧩 SECCIÓN C — INSERCIÓN ELEMENTO POR ELEMENTO
🔹 Actividad 4 — Insertar Documento 1
¿Qué hace use?
Es el comando que selecciona la base de datos con la que vamos a trabajar. Si la base de datos no existe, prepara el contexto para crearla en cuanto insertemos el primer dato.
¿Qué sucede si la base no existe?
MongoDB es "perezoso" (lazy). No crea la base de datos físicamente solo con el comando use. La crea realmente en el momento en que insertamos el primer documento (con insertOne).
¿Qué es BSON?
Significa Binary JSON. Es el formato interno que usa MongoDB para guardar los datos. Es similar a JSON pero permite guardar más tipos de datos (como fechas Date o enteros específicos) y es más eficiente para que la computadora lo lea y procese rápidamente.
🔹 Actividad 5 — Insertar 4 Documentos Más
¿Por qué MongoDB permite agregar campos nuevos sin alterar toda la colección?
Porque es una base de datos sin esquema (schema-less) o de esquema dinámico. Cada documento es independiente; el estudiante A puede tener el campo "beca" y el estudiante B no tenerlo, y ambos conviven en la misma colección sin problemas.
¿Qué pasaría en SQL si agregas un nuevo campo?
Tendrías que ejecutar un comando ALTER TABLE para modificar la estructura de toda la tabla. Esto obligaría a que todos los registros existentes tengan ese campo (rellenándolos con NULL), lo cual es más rígido y costoso computacionalmente.
### 🔎 SECCIÓN D — CONSULTAS INTELIGENTES
🔹 Actividad 7 — Consultas con Operadores
¿Qué significa $gt?
Significa Greater Than (Mayor que, >). Se usa para buscar valores estrictamente mayores al número indicado.
¿Qué significa $gte?
Significa Greater Than or Equal (Mayor o igual que, >=). Incluye el valor exacto que estás buscando y los superiores.
¿Qué son operadores de comparación?
Son comandos especiales (que empiezan con $) utilizados en las consultas para filtrar documentos basándose en comparaciones de valores (mayor, menor, igual, diferente, etc.), permitiendo búsquedas más precisas que una simple igualdad.
### 🔄 SECCIÓN E — ACTUALIZACIONES CONTROLADAS
🔹 Actividad 8 — updateOne()
¿Qué hace $set?
Es un operador atómico que indica que solo queremos modificar o agregar el campo especificado, manteniendo el resto de la información del documento intacta.
¿Qué pasa si no se usa $set?
En una actualización (dependiendo del comando exacto, como en versiones antiguas o replaceOne), si no usas operadores de actualización, podrías correr el riesgo de reemplazar todo el documento por solo el campo que enviaste, borrando el resto de los datos (nombre, edad, etc.). $set protege la integridad del resto del documento.
Diferencia entre updateOne y updateMany:
updateOne busca y modifica solo el primer documento que coincida con el criterio de búsqueda. updateMany modifica todos los documentos que cumplan con el criterio.
### ❌ SECCIÓN F — ELIMINACIÓN RESPONSABLE
🔹 Actividad 9 — deleteOne()
¿Qué riesgos tiene eliminar datos sin respaldo?
La pérdida permanente de información. En bases de datos, normalmente no hay un botón de "deshacer" (Ctrl+Z). Si borras un alumno por error y no tienes respaldo, esa información desaparece para siempre.
¿Qué buenas prácticas deberías aplicar antes de eliminar?
Hacer una consulta (find) primero con los mismos criterios para verificar qué datos se van a borrar.
Tener copias de seguridad (backups) recientes.
Usar "Borrado Lógico" (Soft Delete): en lugar de usar deleteOne, actualizar el campo activo: false. Así el dato no se ve, pero sigue existiendo por seguridad.
### 🧠 SECCIÓN G — ANÁLISIS COMPARATIVO
Actividad 10 — Comparación SQL vs NoSQL

<img width="800" height="203" alt="image" src="https://github.com/user-attachments/assets/7f6534cd-3ab5-4ed1-90b1-320b67d7f6e7" />

### 📊 SECCIÓN H — RETO AVANZADO
Documento anidado
¿Qué es un documento anidado?
Es tener un documento (objeto JSON) dentro de otro documento. Por ejemplo, el campo contacto no es un simple texto, sino que dentro tiene { telefono: "...", correo: "..." }. Es una jerarquía padre-hijo dentro del mismo registro.
¿Qué ventaja tiene frente a relaciones JOIN?
El rendimiento (velocidad). En SQL, para obtener los datos del alumno y su contacto, la base de datos tiene que buscar en dos tablas diferentes y unirlas (JOIN), lo cual consume recursos. En MongoDB, al tener el documento anidado, obtienes toda la información en una sola lectura, siendo mucho más rápido.

<img width="556" height="349" alt="image" src="https://github.com/user-attachments/assets/a9243d5b-17c4-4152-9dda-cb4e4f405c59" />


"Durante esta práctica aprendí que MongoDB cambia el paradigma de 'normalización' que usamos en SQL. En lugar de dividir la información en muchas tablas para evitar duplicidad, MongoDB prioriza la forma en que accedemos a los datos. Si siempre necesito ver las materias junto con el alumno, es mejor tenerlas anidadas en un Array o subdocumento. Esto hace que las aplicaciones web modernas sean mucho más rápidas, ya que la base de datos entrega la información lista para ser consumida en formato JSON, que es el estándar de la web."
