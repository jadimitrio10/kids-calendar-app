# 🤝 Contribuyendo a KidsCalendar

¡Gracias por tu interés en contribuir a KidsCalendar! Este documento proporciona directrices para contribuir al proyecto.

## 📋 Tabla de Contenidos

- [Código de Conducta](#código-de-conducta)
- [Cómo Contribuir](#cómo-contribuir)
- [Estándares de Código](#estándares-de-código)
- [Proceso de Pull Request](#proceso-de-pull-request)
- [Reportar Bugs](#reportar-bugs)
- [Sugerir Mejoras](#sugerir-mejoras)

---

## 📖 Código de Conducta

Esperamos que todos los contribuyentes sigan nuestro Código de Conducta. Por favor, sé respetuoso y constructivo en tus interacciones con otros miembros de la comunidad.

---

## 🎯 Cómo Contribuir

### 1. Fork el Repositorio
```bash
git clone https://github.com/tu-usuario/kids-calendar-app.git
cd kids-calendar-app
```

### 2. Crear una Rama
```bash
git checkout -b feature/mi-nueva-feature
# o para fixes
git checkout -b fix/corregir-bug
```

### 3. Hacer Cambios
Realiza tus cambios siguiendo los estándares de código del proyecto.

### 4. Hacer Commit
```bash
git commit -m "feat: agregar nueva característica" 
# o
git commit -m "fix: corregir error en componente X"
```

### 5. Push a tu Fork
```bash
git push origin feature/mi-nueva-feature
```

### 6. Abrir un Pull Request
- Describe claramente qué cambios realizaste
- Referencia cualquier issue relacionado
- Incluye screenshots si es relevante

---

## 📝 Estándares de Código

### TypeScript
- Siempre usa tipos explícitos
- Evita `any` a menos que sea absolutamente necesario
- Usa interfaces para objetos complejos

```typescript
// ✅ Correcto
interface User {
  id: string;
  name: string;
  email: string;
}

const user: User = { id: '1', name: 'John', email: 'john@example.com' };

// ❌ Evitar
const user: any = { id: '1', name: 'John', email: 'john@example.com' };
```

### React Components
- Usa componentes funcionales
- Mantén los componentes pequeños y enfocados
- Usa custom hooks para lógica reutilizable

```typescript
// ✅ Correcto
export const MyComponent = ({ children }: { children: ReactNode }) => {
  const [state, setState] = useState(false);
  
  return <div>{children}</div>;
};

// ❌ Evitar
export const MyComponent = (props: any) => {
  // ...
};
```

### Naming Conventions
- Componentes: `PascalCase` (e.g., `UserProfile.tsx`)
- Funciones: `camelCase` (e.g., `getUserData()`)
- Constantes: `UPPER_SNAKE_CASE` (e.g., `API_BASE_URL`)
- Archivos: `kebab-case` o `PascalCase` (según el contenido)

### Estilos
- Usa Tailwind CSS para estilos
- Evita CSS-in-JS cuando sea posible
- Mantén los className cortos y legibles

```typescript
// ✅ Correcto
<button className="px-4 py-2 bg-primary text-white rounded-lg hover:bg-opacity-90">
  Click me
</button>

// ❌ Evitar estilos inline
<button style={{ padding: '8px 16px', backgroundColor: 'red' }}>
  Click me
</button>
```

---

## 📋 Proceso de Pull Request

### Antes de Subir tu PR
1. [ ] Código sigue los estándares del proyecto
2. [ ] Tests pasan localmente (si aplica)
3. [ ] No hay conflictos con la rama main
4. [ ] Commit messages son claros y descriptivos
5. [ ] TypeScript no tiene errores

### Template de PR
```markdown
## Descripción
Breve descripción de los cambios

## Tipo de Cambio
- [ ] Bug fix
- [ ] Nueva característica
- [ ] Mejora
- [ ] Cambio en la documentación

## Issues Relacionados
Closes #123

## Cambios Propuestos
- Cambio 1
- Cambio 2
- Cambio 3

## Screenshots (si aplica)
[Agregar screenshots aquí]

## Testing
¿Cómo se prueba este cambio?
```

---

## 🐛 Reportar Bugs

### Template de Issue para Bug
```markdown
## Descripción del Bug
Descripción clara de lo que está pasando

## Pasos para Reproducir
1. ...
2. ...
3. ...

## Comportamiento Esperado
¿Qué debería pasar?

## Comportamiento Actual
¿Qué está pasando en lugar de eso?

## Entorno
- OS: [e.g. Windows, macOS, Linux]
- Navegador: [e.g. Chrome, Firefox, Safari]
- Versión: [e.g. 1.0.0]

## Logs o Screenshots
[Agregar logs o screenshots si aplica]
```

---

## 💡 Sugerir Mejoras

### Template de Issue para Feature
```markdown
## Descripción
Descripción clara de la mejora propuesta

## Problema que Resuelve
¿Qué problema o necesidad resuelve esto?

## Solución Propuesta
Cómo podrías implementar esta mejora

## Alternativas Consideradas
Otras soluciones que podrían funcionar

## Contexto Adicional
Información adicional relevante
```

---

## 📚 Área de Enfoque Actual

Si quieres contribuir, estas áreas son especialmente importantes:

### Backend
- [ ] Tests unitarios
- [ ] Validación mejorada de entrada
- [ ] Rate limiting
- [ ] Caching con Redis

### Frontend
- [ ] Optimización de performance
- [ ] Temas oscuros
- [ ] Internacionalización (i18n)
- [ ] Progressive Web App (PWA)

### DevOps
- [ ] CI/CD pipeline
- [ ] Monitoreo y logging
- [ ] Backup automáticos
- [ ] Scaling automático

---

## 🚀 Configuración del Entorno de Desarrollo

### Backend
```bash
cd backend
npm install
cp .env.example .env
npm run prisma:migrate
npm run dev
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Debugging
- Backend: Usa `console.log` o debugger de Node.js
- Frontend: Usa React DevTools y Chrome DevTools
- Base de datos: Usa `npm run prisma:studio`

---

## 📞 Comunicación

- **Issues**: Para bugs y features
- **Discussions**: Para preguntas generales
- **Email**: Para cuestiones sensibles

---

## 📄 Licencia

Al contribuir a este proyecto, aceptas que tus contribuciones se licencien bajo la MIT License.

---

¡Gracias por contribuir a KidsCalendar! 🙌
