# 📚 Documentación de API - KidsCalendar

## Base URL
```
http://localhost:3001/api
```

## Headers Requeridos
```
Content-Type: application/json
Authorization: Bearer <JWT_TOKEN>
```

---

## 🔐 Autenticación (Auth)

### POST /auth/register
Registrar un nuevo usuario

**Body:**
```json
{
  "email": "parent@example.com",
  "password": "password123",
  "name": "Juan García"
}
```

**Response (201):**
```json
{
  "user": {
    "id": "user_123",
    "email": "parent@example.com",
    "name": "Juan García"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### POST /auth/login
Iniciar sesión

**Body:**
```json
{
  "email": "parent@example.com",
  "password": "password123"
}
```

**Response (200):**
```json
{
  "user": {
    "id": "user_123",
    "email": "parent@example.com",
    "name": "Juan García"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### GET /auth/profile
Obtener perfil del usuario autenticado

**Headers:**
```
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
{
  "id": "user_123",
  "email": "parent@example.com",
  "name": "Juan García",
  "createdAt": "2024-05-26T10:30:00.000Z"
}
```

---

## 👨‍👩‍👧 Niños (Children)

### GET /children
Obtener todos los niños del usuario

**Headers:**
```
Authorization: Bearer <JWT_TOKEN>
```

**Response (200):**
```json
[
  {
    "id": "child_1",
    "name": "Carlos",
    "color": "#D85A30",
    "avatarUrl": null,
    "createdAt": "2024-05-26T10:30:00.000Z",
    "updatedAt": "2024-05-26T10:30:00.000Z",
    "tasks": []
  }
]
```

---

### POST /children
Crear un nuevo niño

**Body:**
```json
{
  "name": "María",
  "color": "#1D9E75"
}
```

**Response (201):**
```json
{
  "id": "child_2",
  "name": "María",
  "color": "#1D9E75",
  "avatarUrl": null,
  "createdAt": "2024-05-26T10:30:00.000Z",
  "updatedAt": "2024-05-26T10:30:00.000Z"
}
```

---

### PUT /children/:id
Actualizar un niño

**Body (opcional):**
```json
{
  "name": "María García",
  "color": "#963AFF"
}
```

**Response (200):**
```json
{
  "id": "child_2",
  "name": "María García",
  "color": "#963AFF",
  "avatarUrl": null,
  "createdAt": "2024-05-26T10:30:00.000Z",
  "updatedAt": "2024-05-26T11:45:00.000Z"
}
```

---

### DELETE /children/:id
Eliminar un niño (elimina también todas sus tareas)

**Response (204):**
No content

---

## 📝 Tareas (Tasks)

### GET /children/:childId/tasks
Obtener tareas de un niño (opcionalmente filtrar por mes/año)

**Query Parameters:**
- `month` (opcional): Número de mes (1-12)
- `year` (opcional): Año (ej: 2024)

**Example:**
```
GET /children/child_1/tasks?month=5&year=2024
```

**Response (200):**
```json
[
  {
    "id": "task_1",
    "title": "Hacer la tarea",
    "completed": false,
    "dueDate": "2024-05-26T00:00:00.000Z",
    "icon": "📚",
    "notes": "Matemáticas página 45",
    "childId": "child_1",
    "createdAt": "2024-05-26T10:30:00.000Z",
    "updatedAt": "2024-05-26T10:30:00.000Z"
  }
]
```

---

### POST /children/:childId/tasks
Crear una nueva tarea

**Body:**
```json
{
  "title": "Practicar deporte",
  "dueDate": "2024-05-27",
  "icon": "⚽",
  "notes": "30 minutos de fútbol"
}
```

**Response (201):**
```json
{
  "id": "task_2",
  "title": "Practicar deporte",
  "completed": false,
  "dueDate": "2024-05-27T00:00:00.000Z",
  "icon": "⚽",
  "notes": "30 minutos de fútbol",
  "childId": "child_1",
  "createdAt": "2024-05-26T10:30:00.000Z",
  "updatedAt": "2024-05-26T10:30:00.000Z"
}
```

---

### PUT /children/tasks/:taskId
Actualizar una tarea

**Body (todos los campos opcionales):**
```json
{
  "title": "Practicar deporte (actualizado)",
  "completed": true,
  "dueDate": "2024-05-28",
  "icon": "🏆",
  "notes": "Completado exitosamente"
}
```

**Response (200):**
```json
{
  "id": "task_2",
  "title": "Practicar deporte (actualizado)",
  "completed": true,
  "dueDate": "2024-05-28T00:00:00.000Z",
  "icon": "🏆",
  "notes": "Completado exitosamente",
  "childId": "child_1",
  "createdAt": "2024-05-26T10:30:00.000Z",
  "updatedAt": "2024-05-26T11:45:00.000Z"
}
```

---

### DELETE /children/tasks/:taskId
Eliminar una tarea

**Response (204):**
No content

---

## 📊 Estadísticas y Recompensas (Rewards)

### GET /children/:childId/stats
Obtener estadísticas de un niño

**Response (200):**
```json
{
  "childId": "child_1",
  "childName": "Carlos",
  "todaysStats": {
    "total": 5,
    "completed": 3,
    "percentage": 60
  },
  "monthlyStats": {
    "total": 45,
    "completed": 32,
    "percentage": 71
  },
  "streak": 7,
  "level": 4,
  "points": 350
}
```

---

### GET /children/leaderboard
Obtener tabla de posiciones de todos los niños del usuario

**Response (200):**
```json
{
  "month": "mayo de 2024",
  "leaderboard": [
    {
      "childId": "child_2",
      "name": "María",
      "color": "#1D9E75",
      "completed": 35,
      "total": 40,
      "percentage": 87,
      "points": 350
    },
    {
      "childId": "child_1",
      "name": "Carlos",
      "color": "#D85A30",
      "completed": 32,
      "total": 45,
      "percentage": 71,
      "points": 320
    }
  ]
}
```

---

## 🔴 Códigos de Error

| Código | Descripción |
|--------|------------|
| 200 | OK - Solicitud exitosa |
| 201 | Created - Recurso creado |
| 204 | No Content - Eliminado correctamente |
| 400 | Bad Request - Datos inválidos |
| 401 | Unauthorized - Token inválido/expirado |
| 404 | Not Found - Recurso no encontrado |
| 409 | Conflict - El recurso ya existe |
| 500 | Internal Server Error - Error del servidor |

**Respuesta de Error:**
```json
{
  "error": "Invalid credentials"
}
```

---

## 📦 Ejemplos de Uso con cURL

### Registrarse
```bash
curl -X POST http://localhost:3001/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "parent@example.com",
    "password": "password123",
    "name": "Juan García"
  }'
```

### Iniciar sesión
```bash
curl -X POST http://localhost:3001/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "parent@example.com",
    "password": "password123"
  }'
```

### Obtener niños
```bash
curl -X GET http://localhost:3001/api/children \
  -H "Authorization: Bearer <JWT_TOKEN>"
```

### Crear tarea
```bash
curl -X POST http://localhost:3001/api/children/child_1/tasks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <JWT_TOKEN>" \
  -d '{
    "title": "Hacer la tarea",
    "dueDate": "2024-05-27",
    "icon": "📚"
  }'
```

### Obtener estadísticas
```bash
curl -X GET http://localhost:3001/api/children/child_1/stats \
  -H "Authorization: Bearer <JWT_TOKEN>"
```

---

## 🔐 Notas de Seguridad

- Los tokens JWT expiran en 7 días
- Todos los endpoints excepto `/auth/register` y `/auth/login` requieren autenticación
- Las contraseñas se hashean con bcryptjs
- Las consultas están protegidas contra SQL injection mediante Prisma ORM
- CORS está habilitado solo para `http://localhost:3000` (configurable)

---

## 📚 Más Recursos

- [Documentación de Prisma](https://www.prisma.io/docs/)
- [Documentación de Express.js](https://expressjs.com/)
- [JWT.io](https://jwt.io/)
