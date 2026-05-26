# 🚀 Guía de Instalación - KidsCalendar

## Opción 1: Docker (La más fácil - Recomendada)

### Requisitos
- Docker Desktop instalado
- Git

### Pasos

1. **Clonar o descargar el proyecto**
```bash
git clone <url-del-repo>
cd kids-calendar-app
```

2. **Levantar la aplicación completa**
```bash
docker-compose up -d
```

3. **Esperar a que todo esté listo** (30-60 segundos)
```bash
docker-compose logs -f
```

4. **Ejecutar migraciones de BD** (primera vez)
```bash
docker-compose exec backend npm run prisma:migrate
```

5. **Cargar datos de ejemplo**
```bash
docker-compose exec backend npm run db:seed
```

6. **Acceder a la aplicación**
- Frontend: http://localhost:3000
- Backend API: http://localhost:3001/api
- Adminer (BD): http://localhost:8080

7. **Credenciales de demo**
- Email: `parent@example.com`
- Contraseña: `password123`

### Comandos útiles

```bash
# Ver logs
docker-compose logs -f

# Entrar en contenedor
docker-compose exec backend sh

# Parar servicios
docker-compose down

# Parar y borrar volúmenes
docker-compose down -v
```

---

## Opción 2: Local (Node.js + PostgreSQL)

### Requisitos
- Node.js 20+
- PostgreSQL 12+
- Git

### Pasos Backend

1. **Navegar a backend**
```bash
cd backend
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Crear archivo .env**
```bash
cp .env.example .env
```

4. **Editar .env con tus datos**
```
DATABASE_URL="postgresql://user:password@localhost:5432/kids_calendar"
JWT_SECRET="tu-secreto-super-seguro-cambiar-en-produccion"
API_PORT=3001
NODE_ENV="development"
CORS_ORIGIN="http://localhost:3000"
```

5. **Generar cliente Prisma**
```bash
npm run prisma:generate
```

6. **Ejecutar migraciones**
```bash
npm run prisma:migrate
```

7. **Cargar datos de ejemplo (opcional)**
```bash
npm run db:seed
```

8. **Iniciar servidor**
```bash
npm run dev
```

El servidor estará en: **http://localhost:3001**

### Pasos Frontend

1. **En otra terminal, navegar a frontend**
```bash
cd frontend
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Iniciar desarrollo**
```bash
npm run dev
```

La aplicación estará en: **http://localhost:3000**

---

## Configuración Base de Datos (PostgreSQL Local)

Si no tienes PostgreSQL instalado:

### Windows
```bash
# Descargar instalador desde https://www.postgresql.org/download/windows/
# O usar Chocolatey:
choco install postgresql
```

### macOS
```bash
# Con Homebrew
brew install postgresql@15
brew services start postgresql@15
```

### Linux (Ubuntu)
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
```

### Crear base de datos
```bash
# Conectar a PostgreSQL
psql -U postgres

# En el prompt de psql:
CREATE DATABASE kids_calendar;
CREATE USER "user" WITH PASSWORD 'password';
ALTER ROLE "user" SET client_encoding TO 'utf8';
ALTER ROLE "user" SET default_transaction_isolation TO 'read committed';
ALTER ROLE "user" SET default_transaction_deferrable TO on;
ALTER ROLE "user" SET default_transaction_deferrable TO on;
ALTER ROLE "user" SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE "kids_calendar" TO "user";
\q
```

---

## Troubleshooting

### "Cannot connect to database"
- Verificar que PostgreSQL está corriendo
- Verificar DATABASE_URL en .env
- Verificar usuario y contraseña

### "Port already in use"
```bash
# Linux/Mac
lsof -i :3000  # o :3001
kill -9 <PID>

# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### "Module not found"
```bash
# Backend
rm -rf node_modules package-lock.json
npm install

# Frontend
rm -rf node_modules package-lock.json
npm install
```

### Problemas con Docker
```bash
# Limpiar todo y empezar de nuevo
docker-compose down -v
docker system prune -a

# Luego ejecutar de nuevo
docker-compose up -d
```

---

## Siguientes pasos

1. ✅ Acceder a http://localhost:3000
2. ✅ Registrarse o usar demo
3. ✅ Crear un niño
4. ✅ Agregar tareas
5. ✅ Explorar el calendario

¡Listo! Tu aplicación KidsCalendar está funcionando 🎉
