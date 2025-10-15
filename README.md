# Examen Práctico — Programación 4 (Proyecto Fullstack)

---

_Fecha inicio:_ 13/10/2025

_Fecha entrega:_ 12/11/2025 (23:59 hs)

---

_Objetivo:_ Diseñar y desarrollar, en equipos, un proyecto fullstack bajo arquitectura cliente-servidor. El frontend se implementará en React y el backend en ASP.NET Core (C#) con Entity Framework Core, siguiendo una arquitectura en capas (onion) con separación clara entre modelos, servicios y controladores. Se evaluarán diseño, arquitectura, buenas prácticas, calidad de código y experiencia de usuario.

---

## 1) Enunciado general

El “elemento” es el dominio central del proyecto y puede ser libre (cursos, productos, tareas, proyectos, etc.).

- Autenticación y autorización con roles (p. ej., admin y user).
- Listado de elementos.
- Vista de detalle del elemento con información asociada.
- Formulario para crear/editar elementos (solo usuarios con rol admin).
- Panel de administración con estadísticas simples (cantidad de elementos, usuarios, métricas relevantes).

> La app debe implementar ruteo en el frontend y exponer una API REST en el backend. Debe haber componentes y rutas cargadas perezosamente en el frontend con _React.lazy_ + _Suspense_.

---

## 2) Requisitos técnicos obligatorios

### 2.1 Frontend (React)

Tecnologías mínimas a utilizar explícitamente:

1. _useState_: manejar al menos 2 estados locales en componentes (p. ej. toggles, inputs controlados, filtros).
2. _useEffect_: usar para efectos secundarios (p. ej. fetch inicial, suscripciones simuladas, limpieza en un efecto).
3. _wouter_: ruteo del lado del cliente. Rutas mínimas: `/`, `/login`, `/elementos`, `/elementos/:id`, `/admin`.
4. _axios_: todas las llamadas HTTP deben realizarse con axios hacia el backend.
5. _Lazy loading_: al menos 2 componentes grandes deben importarse con `React.lazy` y mostrarse con `Suspense` (p. ej. `ElementoDetail`, `AdminPanel`).
6. _zustand_: usar para estado global (al menos autenticación y sesión de usuario).
7. _zod_: definir esquemas de validación para los formularios; validar antes de enviar.
8. _react-hook-form_: formularios (login, crear/editar elementos) integrados con zod (`@hookform/resolvers/zod`).

Notas:

- Se pueden añadir bibliotecas auxiliares (UI kits, date pickers, charting, etc.) sin cambiar el ecosistema de React.
- Manejar errores y mostrar feedback (toasts, loaders, vacíos de datos, estados de error).

### 2.2 Backend (ASP.NET Core + EF Core)

Requerimientos mínimos:

1. _ASP.NET Core Web API_: exponer endpoints REST para CRUD de elementos y autenticación.
2. _Entity Framework Core_: persistencia con migraciones; seed de datos iniciales opcional.
3. _Arquitectura en capas (onion)_: separar claramente `Modelos` (dominio/entidades), `Servicios` (lógica de negocio) y `Controladores` (capa de presentación/API). Evitar que los controladores accedan directamente a la capa de datos sin pasar por servicios.
4. _Seguridad_: autenticación y autorización por roles.
   - Autenticación con JWT (recomendado) o ASP.NET Core Identity.
   - Autorización con `[Authorize]` y policies/roles (p. ej. `[Authorize(Roles = "Admin")]`).
5. _Buenas prácticas API_: status codes adecuados, DTOs para requests/responses, manejo de errores estándar (problem details), validación de entrada (DataAnnotations o FluentValidation).
6. _Configuración_: usar `appsettings.json` para cadenas de conexión y variables; usar inyección de dependencias para servicios/repositorios.

---

## 3) Requisitos funcionales mínimos (entregable obligatorio)

### A. Autenticación y autorización

- Form de login (`/login`) validado con zod + react-hook-form.
- Al loguearse, guardar usuario y rol en _zustand_; almacenar y enviar token en axios (header `Authorization`).
- Ocultar/mostrar rutas y acciones de admin según rol.

### B. Listado de elementos

- Ruta `/elementos`: listado paginado o con lazy load. Cada elemento muestra atributos clave (p. ej. título, autor, categoría, cantidad).
- Búsqueda y filtro simple (por id, nombre o categoría) usando _useState_.

### C. Detalle de elemento

- Ruta `/elementos/:id`: mostrar detalles del elemento. Este componente debe cargarse con `React.lazy`.

### D. Formulario admin

- Ruta `/admin` o `/admin/elementos/new`: formulario para crear/editar elementos (título, descripción, categoría, etc.), validado con zod + react-hook-form. Solo accesible para rol admin.

### E. Administración / Estadísticas

- Panel `/admin` cargado perezosamente con métricas: total de elementos, total de usuarios y al menos una estadística relevante (p. ej., elementos por categoría), pudiendo usar gráficos.

### F. Persistencia y API

- Consumir la API REST propia (backend ASP.NET Core) con axios. Definir endpoints para autenticación (login/refresh opcional) y CRUD de elementos.

---

## 4) Criterios de evaluación

- _Funcionalidad mínima completada_

  - Login/Logout, control de acceso por roles
  - Listado y búsqueda de elementos
  - Vista de detalle
  - Formularios de creación/edición con validación
  - Panel admin con estadísticas

- _Calidad de código y arquitectura_

  - Frontend: uso correcto de hooks, separación de componentes, servicios de API con axios, estado global con zustand, lazy loading
  - Backend: capas claras (modelos/servicios/controladores), DI, DTOs, manejo de errores, validaciones

- _Validación y experiencia de usuario_

  - Formularios con react-hook-form y zod
  - Feedback visual y manejo de errores en peticiones

- _Bonus (hasta +10 pts)_
  - Interceptores axios / refresco de token
  - Tests básicos.
  - Documentación de API (Swagger)
  - Paginación/filtrado avanzados, ordenamiento en servidor
  - CI/CD simple y commits claros

---

## 5) Entregables (obligatorio)

1. Repositorio Git público (frontend y backend) o monorepo claramente organizado.
2. README.md(s) con pasos para instalar, correr (dev + build) y configuración (variables/connection strings).
3. Documentación de API (Swagger o README con endpoints y ejemplos).
4. URL de la app desplegada (opcionalmente backend publicado o mock remoto si aplica).

---

## 6) Checklist para corrección rápida

- [ ] El frontend corre con `npm install` y `npm run dev`.
- [ ] Autenticación con JWT o Identity; autorización por roles aplicada en endpoints sensibles.
- [ ] Frontend usa zustand para auth/estado global y protege rutas.
- [ ] Formularios usan react-hook-form y validan con zod.
- [ ] Axios se usa para todas las llamadas y envía token en headers; manejo de errores presente.
- [ ] Rutas con wouter y al menos 2 componentes con React.lazy + Suspense.
- [ ] README(s) y Swagger/Docs claros.

---
