# Generador Integral de Prompts Pro v4

PWA de una sola página para construir prompts estructurados (flujo ChatGPT + prompt final).
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
index.html     # La PWA completa (autocontenida)
nginx.conf     # Config de nginx (listen 3000, SPA fallback, gzip, /healthz)
Dockerfile     # nginx:alpine sirviendo el estático
```
