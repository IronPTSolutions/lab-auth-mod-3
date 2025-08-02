# 🧪 LAB: Autenticación de Usuarios con Cookies y Sessions

En este laboratorio vamos a construir una API mínima con autenticación basada en cookies utilizando sesiones. Usaremos `express-session` para manejar las sesiones y `connect-mongo` para almacenarlas en MongoDB.

---

## 🎯 Objetivo

Implementar autenticación de usuarios en una API REST utilizando cookies de sesión y proteger los recursos privados (como tareas) para que sólo los usuarios autenticados puedan acceder a ellos.

---

## 🧱 Requisitos del sistema

### 1. Modelo de Usuario (`User`)
Debe tener los siguientes campos:

- `username` (string, **único**)
- `password` (string, encriptado con `bcryptjs`)

---

## 🧩 Funcionalidades

### 🔐 Autenticación y sesiones (`express-session`, `connect-mongo`)

#### 🟢 Crear sesión (Login)
- **Método:** `POST /sessions`
- **Descripción:** Valida las credenciales (`username` y `password`) y si son correctas, crea una sesión con el `userId` y devuelve una cookie de sesión al cliente y el usuario autenticado.

#### 🔴 Cerrar sesión (Logout)
- **Método:** `DELETE /sessions`
- **Descripción:** Destruye la sesión activa y elimina la cookie del cliente.

---

### 👤 CRUD de usuarios

#### 🟢 Crear usuario
- **Método:** `POST /users`
- **Descripción:** Crea un nuevo usuario. Cualquier usuario puede acceder a este endpoint.  
  - Antes de guardar, el `username` debe ser único.
  - La contraseña debe almacenarse encriptada usando `bcryptjs`.

---

### ✅ CRUD de tareas (recurso protegido)

#### 📄 Modelo de Tarea (`Task`)
Debe contener los siguientes campos:

- `name` (string)
- `owner` (referencia al modelo `User`)

#### 🟢 Crear tarea
- **Método:** `POST /tasks`
- **Descripción:** Requiere autenticación. Crea una nueva tarea asignada al usuario autenticado.

#### 📄 Listar tareas
- **Método:** `GET /tasks`
- **Descripción:** Requiere autenticación. Devuelve solo las tareas pertenecientes al usuario autenticado.

---

## 🧪 Seguridad

- Las contraseñas **nunca deben almacenarse en texto plano**. Usa `bcryptjs` para encriptarlas.
- Protege los endpoints `/tasks` con middleware de autenticación que verifique la sesión activa.
- Asegúrate de configurar correctamente las cookies de sesión:
  - Usa `httpOnly: true` para evitar acceso desde el navegador.
  - En producción, considera usar `secure: true`.

---

## 📦 Tecnologías requeridas

- `express`
- `mongoose`
- `express-session`
- `connect-mongo`
