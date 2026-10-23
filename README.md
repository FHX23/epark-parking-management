# 🅿️ E-Park: Sistema de Gestión de Estacionamiento

> Plataforma web full-stack para la administración, asignación y control de espacios de estacionamiento universitario. Desarrollada con arquitectura desacoplada: **React + Vite** en el frontend, **Node.js + Express** en el backend, persistencia NoSQL con **MongoDB / Mongoose** y despliegue rápido con **Docker**.

[![Frontend: React](https://img.shields.io/badge/Frontend-React_18_%2B_Vite-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![UI: Tailwind + shadcn](https://img.shields.io/badge/UI-TailwindCSS_%2B_shadcn%2Fui-38B2AC?logo=tailwind-css&logoColor=white)](https://ui.shadcn.com/)
[![Backend: Node.js + Express](https://img.shields.io/badge/Backend-Node.js_%2B_Express-339933?logo=node.js&logoColor=white)](https://expressjs.com/)
[![Database: MongoDB](https://img.shields.io/badge/Database-MongoDB_7-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Docker: Compose](https://img.shields.io/badge/DevOps-Docker_Compose-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📌 Contexto del Proyecto y Contribución Individual

Este repositorio es una versión extendida y finalizada construida a partir del proyecto colaborativo universitario original [Not-Minimal/Epark](https://github.com/Not-Minimal/Epark). 

### Mi Contribución en este Proyecto:
- **Backend (Módulo de Vehículos):**
  - Modelado de datos en Mongoose con referencias cruzadas y relaciones con la entidad `User`.
  - Implementación de controladores para registro, consulta por patente, filtrado avanzado por query (`brand`, `model`) y eliminación en cascada.
  - Protección de rutas con middlewares de autenticación basada en sesiones y roles (`isAdmin`, `isUser`).
- **Frontend (Panel Administrativo de Vehículos):**
  - Implementación completa de la vista administrativa `GetAllVehicles.jsx` utilizando componentes de **shadcn/ui** y Tailwind CSS.
  - Sistema de filtros reactivos multi-criterio en tiempo real (búsqueda simultánea por patente, modelo, color y marca).
  - Edición en caliente mediante modales interactivos (`Dialog`), validación y feedback con notificaciones toast (`useToast`).
  - Refactor de la barra de navegación (`Navbar.jsx`) para control dinámico de permisos según el rol del usuario autenticado.
- **Entorno y DevOps:**
  - Configuración de contenedor **Docker** para MongoDB 7 y parametrización limpia de variables de entorno mediante `.env.example`.

---

## ⚙️ Módulos y Funcionalidades

1. **Autenticación y Roles (RBAC):**
   - Manejo de sesiones seguras con `express-session` y encriptación de contraseñas con `bcryptjs`.
   - Roles diferenciados para **Administradores** y **Usuarios**.
2. **Gestión de Vehículos:**
   - Alta de vehículos vinculados al perfil del usuario.
   - Búsqueda, filtrado y edición desde el panel administrativo.
3. **Control de Espacios y Cuadrantes:**
   - Visualización y reserva de plazas de estacionamiento organizadas por cuadrantes.
4. **Reporte de Incidencias:**
   - Registro de reportes y problemas asociados a vehículos o plazas de estacionamiento.
5. **Generación de Códigos QR:**
   - Soporte para validación y control de acceso vehicular mediante códigos QR (`qrcode`).

---

## 🏗️ Arquitectura del Repositorio

```
.
├── docker-compose.yml        # Servicio MongoDB listo para desarrollo local
├── backend/
│   ├── src/
│   │   ├── config/           # Conexión DB, variables de entorno y seeder inicial
│   │   ├── controllers/      # Lógica de controladores (auth, vehicle, user, issues)
│   │   ├── middlewares/      # Verificación de sesiones y roles (isAdmin, isUser)
│   │   ├── models/           # Modelos Mongoose (User, Role, Vehicle, Issue, etc.)
│   │   └── routes/           # Definición de rutas REST
│   └── package.json
└── frontend/
    ├── src/
    │   ├── components/       # Componentes shadcn/ui, layout y navegación
    │   ├── pages/            # Vistas protegidas y públicas (Login, Dashboard, Vehicles)
    │   └── services/         # Clientes Axios desacoplados por entidad
    └── package.json
```

---

## 🚀 Puesta en Marcha Local

### Prerrequisitos
- [Node.js](https://nodejs.org/) v18 o superior.
- [pnpm](https://pnpm.io/) (o npm).
- [Docker](https://www.docker.com/) y Docker Compose.

### 1. Iniciar la Base de Datos
Desde la raíz del proyecto, ejecuta:
```bash
docker compose up -d
```
Esto levantará una instancia de MongoDB 7 en el puerto `27017` con un volumen persistente.

### 2. Configurar y Ejecutar el Backend
```bash
cd backend

# Copiar variables de entorno
cp src/config/.env.example src/config/.env

# Instalar dependencias
pnpm install

# Iniciar servidor en modo desarrollo
pnpm dev
```
> El backend correrá en `http://localhost:5000/api`. Al conectarse por primera vez, `initSetup.js` sembrará automáticamente los roles, usuarios y vehículos de prueba.

### 3. Configurar y Ejecutar el Frontend
En otra terminal:
```bash
cd frontend

# Copiar variables de entorno
cp .env.example .env

# Instalar dependencias
pnpm install

# Iniciar Vite dev server
pnpm dev
```
> La aplicación estará disponible en `http://localhost:5173/` (o el puerto asignado por Vite).

---

## 🧪 Credenciales de Prueba

El sistema incluye usuarios iniciales generados en el seeder:

| Rol | Correo Electrónico | Contraseña |
|---|---|---|
| **Administrador** | `admin@epark.com` | `eparkadmin123` |
| **Usuario** | `user@gmail.com` | `eparkuser123` |
| **Usuario Alternativo** | `mark@gmail.com` | `mark123` |

---

## 👥 Créditos y Licencia

- **Proyecto Base:** [Not-Minimal/Epark](https://github.com/Not-Minimal/Epark)
- **Desarrollado y extendido por:** Matias Arenas ([@FHX23](https://github.com/FHX23))
- **Licencia:** Distribuido bajo la Licencia **MIT**. Consulta el archivo [LICENSE](LICENSE) para más detalles.
