# ReelStudio

PWA de una sola página especializada en generar **prompts para reels y carruseles** (flujo ChatGPT + prompt final).
Es totalmente autocontenida: el `index.html` genera su propio manifest y service worker en línea, sin assets externos.

Parte del ecosistema **VibeSystems / IAreal** (Docker + Coolify + Cloudflare Tunnel).

## Desarrollo local

Abrir directamente `index.html` en el navegador, o servirlo:

```bash
docker build -t generador-prompts .
docker run --rm -p 3000:3000 generador-prompts
# http://localhost:3000
```

## Despliegue (Coolify)

- Imagen base ligera `nginx:alpine`, sirve estático en el puerto `3000`.
- Healthcheck en `/healthz`.
- Se despliega desde este repo de GitHub mediante Coolify, con su propio subdominio vía Cloudflare Tunnel.

## Estructura

```
index.html             # La app (UI + lógica)
manifest.webmanifest   # Manifest PWA (instalable en móvil)
sw.js                  # Service worker (offline / app shell)
icons/                 # Iconos y favicons (192/512, maskable, apple-touch, favicon)
nginx.conf             # Config de nginx (listen 3000, SPA fallback, gzip, /healthz)
Dockerfile             # nginx:alpine sirviendo el estático
```

## PWA / móvil

- Instalable en Android e iOS ("Agregar a pantalla de inicio").
- Iconos en todos los tamaños (incluye `maskable` y `apple-touch-icon` 180×180).
- Funciona offline gracias al service worker (`sw.js`).
- Para regenerar iconos: editar `icons/favicon.svg` y reexportar los PNG.
