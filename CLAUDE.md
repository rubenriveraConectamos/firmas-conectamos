# Proyecto: Generador de Firmas HTML — Conectamos

## Qué es este proyecto

Herramienta interna para que empleados de Conectamos generen su firma corporativa HTML lista para pegar en Gmail. Proyecto completamente independiente del cronograma.

## Stack

- HTML/CSS/JS vanilla — un solo archivo `index.html`
- Sin framework, sin build step, sin backend
- Archivos estáticos: `logo.svg`, `instagram.svg`, `linkedin.svg`, `facebook.svg`

## Deploy

- **URL producción**: https://firmas-conectamos.vercel.app
- **Repo GitHub**: https://github.com/rubenriveraConectamos/firmas-conectamos
- **Proyecto Vercel**: `rubenrivera-4578s-projects/firmas-conectamos`
- **Branch**: `master`
- **Deploy**: `vercel --yes --scope rubenrivera-4578s-projects --prod` desde `C:\Users\openC\firmas-conectamos`

## Archivos

```
index.html       ← App completa (formulario + preview + generador)
logo.svg         ← Isotipo Conectamos (columna derecha de la firma)
instagram.svg    ← Ícono Instagram
linkedin.svg     ← Ícono LinkedIn
facebook.svg     ← Ícono Facebook
```

## Campos del formulario

| Campo | Tipo | Placeholder |
|---|---|---|
| Nombre completo | Texto | Ej. Nombre(s) Apellidos |
| Área / Departamento | Texto | Ej. Área o Departamento |
| WhatsApp | Texto | Ej. 55 1234 5678 |
| Foto | Archivo o URL | — |

## Campos fijos en la firma (hardcodeados)

| Campo | Valor |
|---|---|
| Sitio web | `https://conectamos.ai/` |
| Dirección línea 1 | `Oficina 702, Laguna de Terminos 221` |
| Dirección línea 2 | `Torre A. Miguel Hidalgo, 11520 CDMX.` |
| Instagram | `https://www.instagram.com/conectamos__/` |
| LinkedIn | `https://mx.linkedin.com/company/conectamosai` |
| Facebook | `https://www.facebook.com/p/Conectamos-M%C3%A9xico-61569813066235/` |

## Layout de la firma generada

```
┌────────────┬──────────────────────────────┬─────────────────┐
│            │ Nombre completo (bold blanco) │ Logo Conectamos │
│  Foto      │ Área (italic teal)            │                 │
│  circular  │ 📱 WhatsApp                   │ [IG] [LI] [FB]  │
│  borde     │ 🌐 https://conectamos.ai/     │                 │
│  teal      │ 📍 Dirección (2 líneas)       │                 │
└────────────┴──────────────────────────────┴─────────────────┘
Fondo: #0f1628 | Teal: #00C9B1
```

## Decisiones técnicas clave

- **Foto**: se redimensiona a 110×110px JPEG 60% via canvas antes de base64 — mantiene el HTML bajo el límite de Gmail
- **Logo e íconos**: servidos como URLs estáticas desde `firmas-conectamos.vercel.app` — sin base64, sin peso extra
- **Copia para Gmail**: usa `ClipboardItem` con `text/html` para que Gmail reciba HTML renderizado, no texto plano
- **Fallback copia**: si `ClipboardItem` no está disponible, usa `createRange` + `execCommand('copy')` con un div renderizado

## Cómo hacer cambios

1. Editar `index.html` en `C:\Users\openC\firmas-conectamos`
2. `git add . && git commit -m "..." && git push origin master`
3. `vercel --yes --scope rubenrivera-4578s-projects --prod`
