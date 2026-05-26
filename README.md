# 📅 KidsCalendar - Gestor de Tareas para Niños

Una aplicación web profesional y amigable para que los padres gestionen las tareas diarias de sus hijos en tablets y dispositivos móviles.

## 🎯 Características

- ✅ Autenticación segura con JWT
- 📅 Calendario interactivo mes a mes
- 👨‍👩‍👧 Gestión de múltiples niños
- 🎨 Interfaz colorida y amigable para niños
- 📊 Barra de progreso de tareas completadas
- 🎯 Iconos personalizables para cada tarea
- 📱 Diseño responsive optimizado para tablets
- 🔐 Base de datos PostgreSQL segura

## 🏗️ Arquitectura

```
kids-calendar-app/
├── backend/
│   ├── src/
│   │   ├── routes/        # Rutas API
│   │   ├── controllers/   # Lógica de negocios
│   │   ├── middleware/    # Middlewares
│   │   ├── config/        # Configuración
│   │   └── utils/         # Utilidades
│   ├── prisma/            # Schema y migrations
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── components/    # Componentes React
│   │   ├── pages/         # Páginas
│   │   ├── context/       # Zustand stores
│   │   ├── types/         # TypeScript types
│   │   ├── utils/         # Utilidades
│   │   └── styles/        # Estilos CSS
│   └── Dockerfile
└── docker-compose.yml
```

## 🚀 Inicio Rápido

### Requisitos
- Docker y Docker Compose
- Node.js 20+ (si ejecutas localmente sin Docker)
- PostgreSQL (si ejecutas localmente sin Docker)

### Con Docker (Recomendado)

```bash
# Clonar el repo
git clone <repo>
cd kids-calendar-app

# Levantar toda la aplicación
docker-compose up -d

# Ejecutar migraciones (primera vez)
docker-compose exec backend npm run prisma:migrate

# Cargar datos de ejemplo
docker-compose exec backend npm run db:seed
```

La aplicación estará disponible en:
- Frontend: http://localhost:3000
- Backend API: http://localhost:3001/api
- Base de datos: localhost:5432

### Sin Docker (Local)

#### Backend

```bash
cd backend

# Instalar dependencias
npm install

# Crear archivo .env
cp .env.example .env
# Editar .env con tus valores de base de datos

# Generar cliente Prisma
npm run prisma:generate

# Ejecutar migraciones
npm run prisma:migrate

# Cargar datos de ejemplo
npm run db:seed

# Iniciar servidor
npm run dev
```

El servidor estará en http://localhost:3001

#### Frontend

```bash
cd frontend

# Instalar dependencias
npm install

# Iniciar desarrollo
npm run dev
```

La app estará en http://localhost:3000

## 📚 API Endpoints

### Autenticación
```
POST /api/auth/register
POST /api/auth/login
GET  /api/auth/profile (Requiere autenticación)
```

### Niños
```
GET    /api/children                    (Obtener todos)
POST   /api/children                    (Crear)
PUT    /api/children/:id               (Actualizar)
DELETE /api/children/:id               (Eliminar)
```

### Tareas
```
GET    /api/children/:childId/tasks    (Obtener por fecha)
POST   /api/children/:childId/tasks    (Crear)
PUT    /api/children/tasks/:taskId     (Actualizar)
DELETE /api/children/tasks/:taskId     (Eliminar)
```

## 🔑 Credenciales Demo

Email: `parent@example.com`
Contraseña: `password123`

## 🗄️ Schema de Base de Datos

### User
```sql
- id (String, primary key)
- email (String, unique)
- password (String)
- name (String)
- createdAt
- updatedAt
```

### Child
```sql
- id (String, primary key)
- name (String)
- color (String)
- avatarUrl (String, nullable)
- userId (Foreign Key)
- createdAt
- updatedAt
```

### Task
```sql
- id (String, primary key)
- title (String)
- completed (Boolean)
- dueDate (DateTime)
- icon (String)
- notes (String, nullable)
- childId (Foreign Key)
- createdAt
- updatedAt
```

## 🛠️ Stack Tecnológico

### Backend
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Auth**: JWT (jsonwebtoken)
- **Validation**: Zod

### Frontend
- **Framework**: React 18
- **Language**: TypeScript
- **Build**: Vite
- **Styling**: Tailwind CSS
- **State Management**: Zustand
- **Routing**: React Router
- **HTTP Client**: Axios

### DevOps
- Docker
- Docker Compose
- PostgreSQL 15 Alpine

## 📝 Desarrollo

### Generar nuevas migraciones
```bash
cd backend
npm run prisma:migrate
```

### Ver Prisma Studio
```bash
cd backend
npm run prisma:studio
```

### Build para producción
```bash
# Backend
cd backend
npm run build

# Frontend
cd frontend
npm run build
```

## 🔒 Seguridad

- Contraseñas hasheadas con bcryptjs
- JWT para autenticación stateless
- CORS configurado
- Validación de entrada con Zod
- Protección de rutas con middleware

## 📱 Optimización para Tablet

- Interfaz touch-friendly con botones grandes
- Diseño responsive con Tailwind CSS
- Iconos legibles y vibrantes
- Animaciones suaves
- Colores contrastantes para mejor legibilidad

## 🚢 Deployment

### Usando Railway, Vercel o Heroku

```bash
# Backend
git push heroku backend:main

# Frontend  
git push heroku frontend:main
```

Actualizar variables de entorno:
- `DATABASE_URL`
- `JWT_SECRET`
- `API_PORT`
- `CORS_ORIGIN`

## 📄 Licencia

MIT

## 👨‍💻 Contribuciones

Las contribuciones son bienvenidas. Por favor, abre un PR con tus cambios.

## 📞 Soporte

Para reportar bugs o sugerencias, abre un issue en el repositorio.

---

Hecho con ❤️ para los padres y sus hijos
