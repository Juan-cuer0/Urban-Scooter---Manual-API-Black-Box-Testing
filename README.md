# 🛴 Urban Scooter - QA Comprehensive Testing Project (Manual, Mobile & API)

## 📄 Descripción del Proyecto
Este proyecto consistió en la validación integral y pruebas de extremo a extremo (E2E) para la plataforma **Urban Scooter**, un servicio web y móvil de alquiler de scooters eléctricos por días. El objetivo principal y desafío técnico del proyecto fue asegurar la consistencia, integridad de los datos y sincronización fluida entre el **panel Web (Cliente)**, la **App Móvil (Repartidor)** y la **Base de Datos SQL (PostgreSQL)**.

A través de este proyecto se simuló el flujo completo del negocio: el diseño y validación de la UX/UI de cara al usuario, el consumo de endpoints de la API, el procesamiento transaccional en la base de datos (creación, aceptación y eliminación de repartidores/pedidos) y la gestión logística en el entorno móvil.

---

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Pruebas de API y Backend:** Postman, peticiones REST (GET, POST, DELETE), payloads en formato JSON.
* **Bases de Datos:** PostgreSQL (consistencia transaccional, llaves foráneas, comandos de consulta y persistencia).
* **Entorno de Pruebas Móvil:** Android Studio (Emulación de dispositivos móviles, pruebas de UI, red y notificaciones).
* **Técnicas de Diseño de Pruebas:** Clases de equivalencia, análisis de valores límite (BVA), mapas mentales funcionales y listas de comprobación (*Checklists*).
* **Gestión de Defectos:** JIRA (Reportes formales de bugs e historias de usuario).

---

## 🔍 Cobertura del Aseguramiento de Calidad

### 1. Aplicación Web (Flujo del Cliente)
* **Análisis de Requisitos mediante Mapas Mentales:** Diseñé un mapa mental estratégico para desglosar la lógica funcional y de interfaz de las secciones *"Para quién es el scooter"* y *"Alquiler"*, definiendo criterios para 9 campos críticos (límites, restricciones alfabéticas y navegación).

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DE TU MAPA MENTAL -->
<img width="802" height="513" alt="mapa mental" src="https://github.com/user-attachments/assets/ac984f37-4643-4d28-b1df-c6020cf50bb9" />

* **Validación de Formularios de Pedido:** Ejecución de pruebas de equivalencia en 7 campos obligatorios y 2 opcionales[cite: 2]. Restricciones estrictas de caracteres latinos (de 2 a 15 caracteres) en Nombre, Apellido y Dirección.

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DE TU TABLA DE EQUIVALENCIAS -->
<img width="1068" height="530" alt="Screenshot 2026-06-13 120337" src="https://github.com/user-attachments/assets/6b09243c-006d-493f-8781-f72e0dc6dd2f" />


* **Checklist del Estado del Pedido:** Creación y ejecución de una lista de comprobación de 34 puntos que evaluó el ciclo de vida del pedido, flujos logísticos (*"En almacén"*, *"En camino"*, *"Entregado"*) y el módulo de cancelaciones.
* **Manejo de Errores (UI/UX):** 
  * *Resultado:* **33 PASSED / 1 FAILED**.
  * *Hallazgo Clave:* Se detectó un error de usabilidad de prioridad baja en el campo de búsqueda de número de pedido, donde presionar la tecla `Enter` no activaba la consulta.
  * Se documentó el defecto formalmente en JIRA.

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DEL CHECKLIST DE LA PANTALLA ESTADO DEL PEDIDO -->
<img width="1188" height="530" alt="Screenshot 2026-06-12 181706" src="https://github.com/user-attachments/assets/d2dcfb62-320e-4e8f-91f3-bb1a202e3de6" />
<img width="1243" height="655" alt="Screenshot 2026-06-13 163113" src="https://github.com/user-attachments/assets/822dcf03-f41c-4ca0-a804-9920357786f3" />



---

### 2. Aplicación Móvil (Flujo del Repartidor - Android Studio)
* **Simulación en Emulador:** Instalación y vinculación de la APK con el servidor de pruebas para simular las operaciones del personal de entrega.
* **Pruebas de Notificaciones Push:** Validación de las reglas de negocio de alertas de proximidad (notificación de advertencia enviada al restar 2 horas antes de las 11:59 p.m. para completar el pedido).
  * *Hallazgo Clave (FALLÓ):* El sistema móvil falló críticamente al activar la notificación tanto en segundo plano como en estado activo, bloqueando la validación del contenido del mensaje y la redirección de navegación.

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DEL EMULADOR Y LA NOTIFICACIÓN PUSH -->
<img width="626" height="261" alt="Screenshot 2026-06-13 135218" src="https://github.com/user-attachments/assets/3ee557ff-43c1-4f16-9402-2e753272ebc2" />

* **Resiliencia y Conectividad:** Evaluación UX/UI frente a diseños de Figma para el comportamiento del sistema ante la falta de acceso a Internet, comprobando el bucle de la ventana emergente restrictiva.
* **Restricciones de Credenciales:** Validación de login (letras latinas de 2 a 10 caracteres) y contraseña (solo números enteros de exactamente 4 dígitos).

---

### 3. API & Base de Datos (Integridad Transaccional)
* **Validación de Endpoints (Postman):** Pruebas de integración sobre la API REST (`/api/v1/courier`) analizando estructuras JSON de entrada y códigos de estado de respuesta (`201 Created`, `200 OK`).

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DE POSTMAN CREANDO REPARTIDOR -->
<img width="1101" height="640" alt="Screenshot 2026-06-13 133836" src="https://github.com/user-attachments/assets/0958ae8f-adcd-4d8e-aaa7-10a4406b3dc7" />

* **Consistencia en Base de Datos (PostgreSQL):** Mapeo de parámetros y verificación de que el registro de repartidores y pedidos se impactara de manera exacta en las tablas `Couriers` y `Orders`.
* **Cifrado de Seguridad:** Confirmación de que las contraseñas no se guarden en texto plano, verificando los algoritmos de hashing en la columna `passwordHash`.

<!-- REEMPLAZA EL ENLACE DE ABAJO CON LA IMAGEN DE LA TERMINAL SQL -->
<img width="1383" height="703" alt="Screenshot 2026-06-13 133511" src="https://github.com/user-attachments/assets/94123304-fdbe-4893-b7df-0980138d345e" />

* **Ciclo de Vida E2E:** Verificación de la eliminación en cascada de cuentas de repartidores a través de peticiones `DELETE`.
  * *Hallazgo Clave (Persistencia):* Se identificó que, aunque el flujo de cancelación del pedido se completaba con éxito en la interfaz de usuario, el registro permanecía de forma incorrecta como activo en el backend del sistema.

---

## 📈 Conclusiones Técnicas del Proyecto
El proyecto evidenció la importancia crítica de las pruebas de integración. Mientras las interfaces individuales (Frontend web) mostraban comportamientos aprobados en su mayoría, las pruebas automatizadas de API y base de datos descubrieron que la **integridad referencial** y la **persistencia** se veían comprometidas al interactuar de manera conjunta (ej. pedidos huérfanos tras eliminar repartidores o cancelaciones no guardadas)[cite: 2]. Estas detecciones tempranas previenen fallos catastróficos en producción dentro de entornos de alta demanda.
