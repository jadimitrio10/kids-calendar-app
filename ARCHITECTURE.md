# 🏗️ Arquitectura de KidsCalendar

## Diagrama de Componentes

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENTE (NAVEGADOR)                       │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │              FRONTEND (React + TypeScript)           │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │                                                        │   │
│  │  ┌─────────────┐  ┌──────────┐  ┌─────────────────┐  │   │
│  │  │   Pages     │  │Components│  │    Hooks        │  │   │
│  │  │             │  │          │  │                 │  │   │
│  │  │ - Login     │  │- Calendar│  │- useAuth()      │  │   │
│  │  │ - Register  │  │- TaskList│  │- useChild()     │  │   │
│  │  │ - Dashboard │  │- AddForm │  │                 │  │   │
│  │  └─────────────┘  └──────────┘  └─────────────────┘  │   │
│  │                       ↓                                 │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │        STATE MANAGEMENT (Zustand)               │  │   │
│  │  │  - authStore (Usuario y autenticación)         │  │   │
│  │  │  - childStore (Niños y tareas)                 │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  │                       ↓                                 │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │         HTTP CLIENT (Axios)                      │  │   │
│  │  │    apiClient.ts - Todas las llamadas API        │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────┘   │
│                           ↓ HTTP/REST                        │
└─────────────────────────────────────────────────────────────┘
           ↓ INTERNET / LOCALHOST:3000 → 3001
┌─────────────────────────────────────────────────────────────┐
│                 SERVIDOR (Express + Node.js)                 │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │            API ROUTES & CONTROLLERS                  │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │                                                        │   │
│  │  ┌────────────────────────────────────────────────┐  │   │
│  │  │  POST   /api/auth/register                    │  │   │
│  │  │  POST   /api/auth/login                       │  │   │
│  │  │  GET    /api/auth/profile                     │  │   │
│  │  └────────────────────────────────────────────────┘  │   │
│  │                                                        │   │
│  │  ┌────────────────────────────────────────────────┐  │   │
│  │  │  GET    /api/children                         │  │   │
│  │  │  POST   /api/children                         │  │   │
│  │  │  PUT    /api/children/:id                     │  │   │
│  │  │  DELETE /api/children/:id                     │  │   │
│  │  └────────────────────────────────────────────────┘  │   │
│  │                                                        │   │
│  │  ┌────────────────────────────────────────────────┐  │   │
│  │  │  GET    /api/children/:childId/tasks          │  │   │
│  │  │  POST   /api/children/:childId/tasks          │  │   │
│  │  │  PUT    /api/children/tasks/:taskId           │  │   │
│  │  │  DELETE /api/children/tasks/:taskId           │  │   │
│  │  └────────────────────────────────────────────────┘  │   │
│  │                       ↓                                 │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │       MIDDLEWARE & AUTENTICACIÓN               │  │   │
│  │  │  - CORS                                         │  │   │
│  │  │  - JWT Auth                                    │  │   │
│  │  │  - Request Logging (Morgan)                    │  │   │
│  │  │  - Error Handling                              │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  │                       ↓                                 │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │        PRISMA ORM                               │  │   │
│  │  │  - Schema definition                           │  │   │
│  │  │  - Database migrations                         │  │   │
│  │  │  - Type-safe queries                           │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────┘   │
│                           ↓ SQL                               │
└─────────────────────────────────────────────────────────────┘
           ↓ LOCALHOST:5432
┌─────────────────────────────────────────────────────────────┐
│              BASE DE DATOS (PostgreSQL)                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────┐    │
│  │   users     │  │   children  │  │      tasks       │    │
│  ├─────────────┤  ├─────────────┤  ├──────────────────┤    │
│  │ id (PK)     │  │ id (PK)     │  │ id (PK)          │    │
│  │ email       │  │ name        │  │ title            │    │
│  │ password    │  │ color       │  │ completed        │    │
│  │ name        │  │ userId (FK) │  │ dueDate          │    │
│  │ createdAt   │  │ createdAt   │  │ icon             │    │
│  │ updatedAt   │  │ updatedAt   │  │ notes            │    │
│  │             │  │             │  │ childId (FK)     │    │
│  │             │  │             │  │ createdAt        │    │
│  │             │  │             │  │ updatedAt        │    │
│  └─────────────┘  └─────────────┘  └──────────────────┘    │
│                                                               │
└─────────────────────────────────────────────────────────────┘
```

## Flujo de Datos

### 1. Autenticación

```
User Input (Email/Password)
           ↓
    Login Component
           ↓
    authStore.login()
           ↓
    apiClient.post('/auth/login')
           ↓
    Backend: POST /api/auth/login
           ↓
    authController.login()
           ↓
    Validar credenciales (bcrypt)
           ↓
    Generar JWT Token
           ↓
    Response: { user, token }
           ↓
    localStorage.setItem('token')
           ↓
    Update authStore
           ↓
    Navigate to Dashboard
```

### 2. Crear Tarea

```
User Input (Título, Fecha, Ícono)
           ↓
    AddTaskForm Component
           ↓
    childStore.addTask()
           ↓
    apiClient.post('/children/:childId/tasks')
           ↓
    Backend: POST /api/children/:childId/tasks
           ↓
    authMiddleware (Valida JWT)
           ↓
    taskController.createTask()
           ↓
    Validar permisos (childId pertenece al user)
           ↓
    prisma.task.create()
           ↓
    Guardar en PostgreSQL
           ↓
    Response: { task }
           ↓
    Update childStore.tasks
           ↓
    TaskList re-renders
```

### 3. Marcar Tarea Completada

```
User Click en checkbox
           ↓
    TaskList Component
           ↓
    childStore.updateTask()
           ↓
    apiClient.put('/children/tasks/:taskId')
           ↓
    Backend: PUT /api/children/tasks/:taskId
           ↓
    authMiddleware (Valida JWT)
           ↓
    taskController.updateTask()
           ↓
    Validar permisos
           ↓
    prisma.task.update({ completed: true })
           ↓
    Actualizar en PostgreSQL
           ↓
    Response: { task }
           ↓
    Update childStore.tasks
           ↓
    UI actualiza (animación, progreso)
```

## Estructura de Carpetas Detallada

```
kids-calendar-app/
│
├── backend/
│   ├── src/
│   │   ├── index.ts              # Punto de entrada
│   │   │
│   │   ├── config/
│   │   │   └── index.ts          # Configuración centralizada
│   │   │
│   │   ├── middleware/
│   │   │   └── auth.ts           # JWT authentication middleware
│   │   │
│   │   ├── controllers/          # Lógica de negocio
│   │   │   ├── auth.controller.ts
│   │   │   ├── child.controller.ts
│   │   │   └── task.controller.ts
│   │   │
│   │   ├── routes/               # Definición de rutas
│   │   │   ├── auth.routes.ts
│   │   │   ├── child.routes.ts
│   │   │   └── task.routes.ts
│   │   │
│   │   ├── utils/
│   │   │   ├── jwt.ts            # Funciones JWT
│   │   │   └── types.ts          # TypeScript interfaces
│   │   │
│   │   └── models/               # (Opcional) Si usas modelos adicionales
│   │
│   ├── prisma/
│   │   ├── schema.prisma         # Definición de modelos
│   │   └── seed.ts               # Script para popular BD
│   │
│   ├── package.json
│   ├── tsconfig.json
│   ├── Dockerfile
│   ├── .env.example
│   └── README.md
│
├── frontend/
│   ├── src/
│   │   ├── main.tsx              # Punto de entrada
│   │   ├── App.tsx               # Router y estructura
│   │   │
│   │   ├── pages/                # Full-page components
│   │   │   ├── Login.tsx
│   │   │   ├── Register.tsx
│   │   │   └── Dashboard.tsx
│   │   │
│   │   ├── components/           # Componentes reutilizables
│   │   │   ├── ProtectedRoute.tsx
│   │   │   ├── Calendar.tsx
│   │   │   ├── TaskList.tsx
│   │   │   └── AddTaskForm.tsx
│   │   │
│   │   ├── context/              # Zustand stores
│   │   │   ├── authStore.ts
│   │   │   └── childStore.ts
│   │   │
│   │   ├── types/                # TypeScript types
│   │   │   └── index.ts
│   │   │
│   │   ├── utils/                # Utilidades
│   │   │   └── api.ts            # Cliente HTTP
│   │   │
│   │   └── styles/
│   │       └── index.css
│   │
│   ├── public/
│   │   └── index.html
│   │
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── Dockerfile
│   └── README.md
│
├── docker-compose.yml
├── .gitignore
├── README.md
├── SETUP.md
├── ARCHITECTURE.md
└── (otros archivos de config)
```

## Tecnologías por Capa

### Frontend Layer
- **UI**: React 18
- **Styling**: Tailwind CSS
- **State**: Zustand (ligero y eficiente)
- **Routing**: React Router v6
- **HTTP**: Axios
- **Build**: Vite
- **Language**: TypeScript

### API Layer
- **Framework**: Express.js
- **Validation**: Zod
- **Authentication**: JWT + bcryptjs
- **CORS**: Habilitado
- **Logging**: Morgan

### Data Layer
- **Database**: PostgreSQL 15
- **ORM**: Prisma
- **Migrations**: Prisma Migrate

### DevOps
- **Containerization**: Docker
- **Orchestration**: Docker Compose
- **Version Control**: Git

## Decisiones Arquitectónicas

### 1. ¿Por qué Zustand en lugar de Redux?
- Más ligero (boilerplate mínimo)
- API simple y directa
- Perfecto para aplicaciones medianas
- Mejor rendimiento en React 18

### 2. ¿Por qué Prisma?
- Type-safe queries
- Migraciones automáticas
- Introspection de BD
- Excelente DX (Developer Experience)

### 3. ¿Por qué JWT en lugar de sessions?
- Stateless (perfecto para APIs)
- Escalable horizontalmente
- Funciona bien con SPAs
- Compatible con OAuth

### 4. ¿Por qué Tailwind CSS?
- Utility-first (desarrollo más rápido)
- Customizable
- Excelente para diseños responsive
- Pequeño bundle size con PurgeCSS

## Seguridad

### Frontend
- Tokens almacenados en localStorage
- Rutas protegidas con ProtectedRoute
- Validación de entrada antes de enviar

### Backend
- JWT validation en todas las rutas
- Passwords hasheados con bcrypt
- SQL injection prevención (Prisma)
- CORS configurado
- Input validation con Zod

### Base de Datos
- PostgreSQL con usuario restringido
- Encriptación de conexión (en producción)
- Backups automáticos (en producción)

## Escalabilidad

### Frontend
- Code splitting automático con Vite
- Lazy loading de componentes posible
- Caché de assets con service workers (futuro)

### Backend
- Stateless (fácil de escalar horizontalmente)
- Database connection pooling (Prisma)
- Rate limiting (implementar en futuro)
- Caching (Redis posible en futuro)

### Database
- Índices en foreign keys
- Índices en fecha (para queries de calendario)
- Connection pooling con Prisma

## Performance Optimization

1. **Frontend**
   - Vite lazy loading
   - Tailwind PurgeCSS
   - Minificación automática

2. **Backend**
   - Prisma select selectivo
   - Índices en BD
   - Compression middleware

3. **Network**
   - Gzip compression
   - API response caching
   - Conditional requests

## Monitoring & Logging

### Backend
- Morgan para HTTP requests
- Console.error para errores
- Posible integración con Sentry

### Frontend
- Error boundaries (React 18)
- Posible integración con Sentry

---

Esta arquitectura es modular, escalable y fácil de mantener. Está diseñada para crecer con tu aplicación.
