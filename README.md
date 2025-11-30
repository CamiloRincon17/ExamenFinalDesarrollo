# Cinema Plus — Sistema de Gestión (Vue 3 + Bootstrap 5.3)

Aplicación web modular y responsiva para administrar películas y usuarios con control de acceso basado en roles. Construida con **Vue 3**, **Bootstrap 5.3**, **Bootstrap Icons** y una API simulada con JSON Server.

## 🎯 Objetivo del Negocio

Proporcionar una plataforma completa para:
- **Gestión de películas**: Crear, listar, editar y eliminar películas del catálogo
- **Gestión de usuarios**: Administración de cuentas con diferentes niveles de permisos
- **Control de acceso**: Sistema de roles (Usuario, Admin, Super Admin)
- **Interfaz moderna**: UI responsiva con componentes Bootstrap 5 reutilizables

## 📁 Estructura del Proyecto

```
src/
  ├── assets/              # Estilos personalizados (custom.scss)
  ├── components/          # Componentes reutilizables
  │   ├── AlertComponent.vue         # Sistema de alertas Bootstrap
  │   ├── ConfirmModal.vue          # Modal de confirmación
  │   ├── FooterComponent.vue       # Footer de la aplicación
  │   ├── LoadingSpinner.vue        # Indicador de carga
  │   ├── MovieCarousel2025.vue     # Carrusel de películas
  │   ├── MovieModal.vue            # Modal para crear/editar películas
  │   ├── NavbarComponent.vue       # Barra de navegación
  │   ├── SidebarComponent.vue      # Sidebar del dashboard
  │   └── UserModal.vue             # Modal para crear/editar usuarios
  ├── layouts/             # Layouts de la aplicación
  │   └── DashboardLayout.vue       # Layout principal con Sidebar
  ├── router/              # Configuración de rutas (Vue Router)
  │   └── index.js
  ├── service/             # Servicios de API (Axios)
  │   └── api.js
  ├── views/               # Vistas principales
  │   ├── DashboardProductoView.vue  # Gestión de películas (Admin)
  │   ├── LoginView.vue              # Página de inicio de sesión
  │   ├── MovieCard.vue              # Tarjeta de película
  │   ├── MovieDetailModal.vue       # Modal de detalles
  │   ├── ProductoView.vue           # Catálogo público
  │   └── UserManagementView.vue     # Gestión de usuarios (Super Admin)
  ├── data/                # Datos locales
  │   └── usuarios.json    # Base de datos local de usuarios
  ├── App.vue              # Componente raíz
  └── main.js              # Punto de entrada
```

## 🚀 Instalación y Ejecución

```bash
# 1. Instalar dependencias
npm install

# 2. Ejecutar la aplicación en modo desarrollo
npm run serve

La aplicación estará disponible en `http://localhost:8080`

## 🎨 Características de Diseño

### Stack Tecnológico
- **Vue 3**: Framework JavaScript progresivo
- **Bootstrap 5.3**: Framework CSS con componentes modernos
- **Bootstrap Icons**: Iconografía completa para todas las acciones
- **Sass**: Preprocesador CSS para estilos personalizados
- **Axios**: Cliente HTTP para consumo de API
- **Vue Router**: Navegación SPA con guardias de ruta

### Componentes Bootstrap 5
- ✅ Modales personalizados para CRUD
- ✅ Sistema de alertas nativo de Bootstrap
- ✅ Confirmaciones con modal en lugar de `alert()` nativo
- ✅ Cards responsivas
- ✅ Tablas con acciones
- ✅ Formularios validados
- ✅ Spinner de carga

### Iconos Bootstrap
Todas las acciones CRUD incluyen iconos intuitivos:
- 🎬 **Crear**: `bi-plus-circle`
- ✏️ **Editar**: `bi-pencil-square`
- 🗑️ **Eliminar**: `bi-trash`
- 👁️ **Ver**: `bi-eye`
- 💾 **Guardar**: `bi-check-circle`
- ❌ **Cancelar**: `bi-x-circle`

## 🔐 Sistema de Autenticación

### Roles Disponibles
1. **Usuario** (`user`): Acceso de solo lectura al catálogo
2. **Administrador** (`admin`): Gestión completa de películas
3. **Super Administrador** (`superadmin`): Control total (películas + usuarios)

### Funcionamiento
- Guardias de navegación que protegen rutas según permisos
- **Nota**: Sistema educativo, no apto para producción

## 🗺️ Rutas de la Aplicación

| Ruta | Vista | Permisos | Descripción |
|------|-------|----------|-------------|
| `/` | - | Público | Redirección a `/login` |
| `/login` | LoginView | Público | Inicio de sesión |
| `/productos` | ProductoView | Público | Catálogo público (solo lectura) |
| `/dashboard` | DashboardLayout | Autenticado | Layout principal con sidebar |
| `/dashboard/productos` | DashboardProductoView | Admin/SuperAdmin | Gestión de películas (CRUD) |
| `/users` | UserManagementView | SuperAdmin | Gestión de usuarios (CRUD) |

## 🔌 Consumo de API

### Servicio de Películas
Ubicado en `src/service/api.js` (Axios con baseURL `https://6929a1e39d311cddf34aa637.mockapi.io/api/v1`):

```js
// Películas
export const getMovies = () => api.get('/movies')
export const getMovie = (id) => api.get(`/movies/${id}`)
export const createMovie = (data) => api.post('/movies', data)
export const updateMovie = (id, data) => api.put(`/movies/${id}`, data)
export const deleteMovie = (id) => api.delete(`/movies/${id}`)

// Usuarios
export const getUsers = () => api.get('/users')
export const createUser = (data) => api.post('/users', data)
export const updateUser = (id, data) => api.put(`/users/${id}`, data)
export const deleteUser = (id) => api.delete(`/users/${id}`)
```

### Estructura de Datos

#### Película (Movie)
```json
{
  "id": 1,
  "title": "The Shawshank Redemption",
  "genre": "Drama",
  "year": 1994,
  "director": "Frank Darabont",
  "poster": "url-to-poster.jpg",
  "description": "Descripción..."
}
```

#### Usuario (User)
```
{
  "id": 1,
  "username": "admin",
  "password": "admin123",
  "role": "superadmin",
  "email": "admin@example.com",
  "active": true
}
```

## 🧩 Componentes Principales

### Componentes Reutilizables
- **`AlertComponent.vue`**: Sistema de notificaciones con variantes Bootstrap (success, danger, warning, info)
- **`ConfirmModal.vue`**: Modal de confirmación para acciones destructivas
- **`MovieModal.vue`**: Modal para crear/editar películas con validación
- **`UserModal.vue`**: Modal para gestionar usuarios con roles
- **`NavbarComponent.vue`**: Barra de navegación con información de sesión
- **`SidebarComponent.vue`**: Menú lateral dinámico según permisos
- **`FooterComponent.vue`**: Footer con información del sistema
- **`LoadingSpinner.vue`**: Indicador de carga durante operaciones async

### Comunicación entre Componentes

```vue
<!-- Padre emite con AlertComponent -->
<AlertComponent 
  :show="showAlert" 
  :message="alertMessage" 
  :variant="alertType"
  @close="showAlert = false"
/>

<!-- Confirmación antes de eliminar -->
<ConfirmModal
  :show="showConfirm"
  title="¿Eliminar película?"
  message="Esta acción no se puede deshacer"
  @confirm="deleteMovie"
  @cancel="showConfirm = false"
/>

<!-- Modal de película con eventos -->
<MovieModal
  :show="showModal"
  :movie="selectedMovie"
  :genres="availableGenres"
  @saved="handleSaved"
  @close="showModal = false"
/>
```

## 🎓 Características Educativas

### Mejores Prácticas Implementadas
✅ Componentización modular  
✅ Props y eventos para comunicación  
✅ Composables de Vue 3 (`@vueuse/core`)  
✅ Guardias de navegación  
✅ Lazy loading de rutas  
✅ Separación de responsabilidades (service layer)  
✅ Estilos SCSS con variables  
✅ Sistema de diseño consistente con Bootstrap  

### Reemplazo de Funciones Nativas
- ❌ `alert()` → ✅ `AlertComponent.vue`
- ❌ `confirm()` → ✅ `ConfirmModal.vue`
- ❌ `prompt()` → ✅ Modales personalizados con formularios



## 🤝 Evidencia Colaborativa

### Repositorio GitHub
- **Ramas**: [Ver todas las ramas](https://github.com/CamiloRincon17/TercerParcialDesarrollo/branches)
- **Pull Requests**: [Historial de PRs](https://github.com/CamiloRincon17/TercerParcialDesarrollo/pulls?q=is%3Apr+is%3Aclosed)
- **Commits**: [Historial de commits](https://github.com/CamiloRincon17/TercerParcialDesarrollo/commits/main/)

### Flujo de Trabajo
1. Creación de ramas por feature (`feature/user-management`, `feature/bootstrap-components`)
2. Pull Requests con revisión de código
3. Merge a `main` después de aprobación
4. Commits descriptivos siguiendo convenciones


**Desarrollado con ❤️ usando Vue 3 + Bootstrap 5**