# Estimado de Costos de Deploy — Athletica

Los costos dependen de la etapa del producto. Se dividen en tres fases según la cantidad de usuarios.

---

## Fase 1 — MVP / Desarrollo (0 a ~100 usuarios)

| Servicio | Para qué | Costo |
|---|---|---|
| **Railway o Render** | Hostear el backend (NestJS) | $0–$20/mes |
| **Supabase** | Base de datos PostgreSQL | $0 (free tier: 500MB) |
| **Cloudinary** | Guardar imágenes (comprobantes, logos, posts) | $0 (free tier: 25GB) |
| **Firebase** | Notificaciones push | $0 |
| **Resend** | Emails (reset de contraseña) | $0 (3.000 emails/mes) |
| **Expo EAS Build** | Generar builds de la app | $0 (30 builds/mes) |
| **Google Play** | Publicar en Android | $25 único |
| **Apple Developer** | Publicar en iOS | $99/año |
| **Dominio** | Para la API | ~$15/año |

**Total estimado fase 1: $0–$20/mes + $125 inicial**

> Con los free tiers de Supabase, Cloudinary y Firebase alcanza perfectamente para un MVP con uso real pero limitado.

---

## Fase 2 — Producción temprana (~100 a 500 usuarios)

Cuando los free tiers se queden cortos:

| Servicio | Costo estimado |
|---|---|
| Backend hosting | $20–$30/mes |
| Base de datos (Supabase Pro) | $25/mes |
| Cloudinary | $0 (free tier todavía alcanza) |
| Firebase | $0 |
| **Total** | **~$45–$55/mes** |

---

## Fase 3 — Crecimiento (500 a 5.000 usuarios)

| Servicio | Costo estimado |
|---|---|
| Backend (puede necesitar escalar) | $50–$100/mes |
| Base de datos | $25–$50/mes |
| Cloudinary | $89/mes (paid tier) |
| Monitoreo (Sentry) | $0–$26/mes |
| **Total** | **~$165–$265/mes** |

---

## Lo que más impacta el costo en Athletica

- **Imágenes** — cada comprobante de pago y cada post con fotos ocupa storage. Con 1.000 pagos/mes son ~500MB. Cloudinary free aguanta bastante.
- **Notificaciones push** — Firebase es gratuito sin límite práctico.
- **Base de datos** — el volumen de datos es moderado. No hay videos ni archivos pesados en el MVP.

---

## Resumen

| Etapa | Costo mensual |
|---|---|
| MVP / testing | $0–$20 |
| Primeros clientes reales | ~$50 |
| Crecimiento | ~$200 |

> El costo de infraestructura no es el riesgo financiero principal en esta etapa. El costo real es el desarrollo.
