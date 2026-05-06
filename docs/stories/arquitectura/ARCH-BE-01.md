# ARCH-BE-01 — Inicializar proyecto Express + TypeScript

**Estado:** TODO
**Depende de:** ARCH-00

---

## Objetivo

Tener un servidor Express corriendo en TypeScript con la configuración base lista para construir encima.

---

## Estructura esperada al terminar

```
apps/api/
├── src/
│   └── index.ts         ← entry point
├── .env.example
├── package.json
└── tsconfig.json
```

---

## Tareas

- [ ] Inicializar `package.json` en `apps/api/`
- [ ] Instalar dependencias principales:
  ```bash
  npm install express cors helmet dotenv
  npm install -D typescript ts-node-dev @types/express @types/cors @types/node
  ```
- [ ] Crear `tsconfig.json` con `strict: true`
- [ ] Crear `src/index.ts` con servidor Express básico (puerto desde env)
- [ ] Agregar scripts en `package.json`:
  - `dev`: `ts-node-dev --respawn src/index.ts`
  - `build`: `tsc`
  - `start`: `node dist/index.js`
- [ ] Crear `.env.example` con las variables necesarias
- [ ] Verificar que `npm run dev` levanta el servidor en `localhost:3000`
- [ ] Ruta de health check: `GET /health` devuelve `{ status: 'ok' }`

---

## tsconfig.json base

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

---

## .env.example

```env
PORT=3000
NODE_ENV=development
DATABASE_URL=postgresql://...
JWT_SECRET=change-me-min-32-characters
JWT_REFRESH_SECRET=change-me-refresh-min-32-chars
JWT_EXPIRES_IN=15m
JWT_REFRESH_EXPIRES_IN=7d
```

---

## Criterios para marcar como DONE

- [ ] `npm run dev` levanta sin errores
- [ ] `GET /health` devuelve `200 { status: 'ok' }`
- [ ] TypeScript en modo strict sin errores
