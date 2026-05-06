# ARCH-00 — Configuración del Monorepo

**Estado:** TODO
**Prioridad:** Alta — bloquea todo lo demás

---

## Objetivo

Crear la estructura base del repositorio con los dos proyectos (mobile y api) organizados como monorepo.

---

## Estructura esperada al terminar

```
athletica/
├── apps/
│   ├── mobile/          ← proyecto Expo
│   └── api/             ← proyecto Express
├── packages/
│   └── shared-types/    ← tipos TypeScript compartidos entre mobile y api
├── package.json         ← raíz del monorepo (workspaces)
└── .gitignore
```

---

## Tareas

- [ ] Crear `package.json` raíz con workspaces configurados
- [ ] Configurar `.gitignore` general (node_modules, .env, builds nativos)
- [ ] Crear carpeta `apps/mobile/` (vacía por ahora)
- [ ] Crear carpeta `apps/api/` (vacía por ahora)
- [ ] Crear carpeta `packages/shared-types/` con `package.json` e `index.ts` vacío
- [ ] Verificar que `npm install` desde la raíz instala dependencias de todos los workspaces

---

## package.json raíz

```json
{
  "name": "athletica",
  "private": true,
  "workspaces": [
    "apps/*",
    "packages/*"
  ],
  "scripts": {
    "dev:api": "npm run dev --workspace=apps/api",
    "dev:mobile": "npm run start --workspace=apps/mobile"
  }
}
```

---

## .gitignore

```
node_modules/
.env
.env.*
!.env.example
apps/mobile/.expo/
apps/mobile/android/
apps/mobile/ios/
dist/
build/
*.log
.DS_Store
```

---

## Criterios para marcar como DONE

- [ ] La estructura de carpetas existe en el repo
- [ ] `npm install` desde la raíz no da errores
- [ ] `.gitignore` está configurado correctamente
