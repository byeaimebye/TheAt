# ARCH-BE-07 — Configurar Supabase Storage

**Estado:** TODO
**Depende de:** ARCH-BE-02

---

## Objetivo

Tener un servicio de storage listo para subir archivos (PDFs de comprobantes, logos, imágenes de posts) desde el backend.

---

## Tareas

- [ ] Instalar cliente de Supabase:
  ```bash
  npm install @supabase/supabase-js
  ```
- [ ] Agregar variables al `.env`:
  ```env
  SUPABASE_URL=https://xxxx.supabase.co
  SUPABASE_SERVICE_ROLE_KEY=eyJ...
  ```
- [ ] Crear buckets en Supabase Dashboard:
  - `receipts` — comprobantes de pago (privado)
  - `logos` — logos de coaches (público)
  - `posts` — imágenes de posts de comunidad (público)
- [ ] Instalar multer para manejar multipart/form-data:
  ```bash
  npm install multer
  npm install -D @types/multer
  ```
- [ ] Crear `src/modules/uploads/storage.service.ts`:
  ```typescript
  uploadFile(bucket: string, path: string, file: Buffer, mimeType: string): Promise<string>
  deleteFile(bucket: string, path: string): Promise<void>
  getPublicUrl(bucket: string, path: string): string
  ```
- [ ] Crear middleware de upload con multer (almacena en memoria, luego sube a Supabase)

---

## Uso esperado en rutas

```typescript
router.post(
  '/payments',
  authMiddleware,
  upload.single('receipt'),   // multer procesa el archivo
  paymentsController.create   // el controller sube a Supabase y guarda la URL
)
```

---

## Criterios para marcar como DONE

- [ ] Se puede subir un PDF al bucket `receipts` y obtener su URL
- [ ] Se puede subir una imagen al bucket `logos` y obtener su URL pública
- [ ] El archivo aparece en el dashboard de Supabase Storage
