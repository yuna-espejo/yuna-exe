# Yuna.sys — life dashboard

Dashboard personal en un único archivo HTML (sin backend, sin dependencias de build).
Guarda tus datos en el navegador con `localStorage`, así que funciona perfectamente
como página estática en GitHub Pages.

## Subirlo a GitHub Pages (5 minutos)

1. Crea un repo nuevo en GitHub, por ejemplo `yuna-dashboard`. Puede ser público:
   el código no contiene ningún dato personal ni financiero real (lo rellenas tú
   desde el propio dashboard una vez publicado, y se queda solo en tu navegador).
2. Sube este archivo `index.html` a la raíz del repo (importante: debe llamarse
   exactamente `index.html`).
   - Desde la web: botón **Add file → Upload files** → arrastra `index.html` → **Commit**.
   - Desde terminal:
     ```
     git init
     git add index.html README.md
     git commit -m "dashboard inicial"
     git branch -M main
     git remote add origin https://github.com/<tu-usuario>/yuna-dashboard.git
     git push -u origin main
     ```
3. En el repo: **Settings → Pages**.
4. En **Build and deployment → Source**, elige **Deploy from a branch**.
5. En **Branch**, elige `main` y carpeta `/ (root)` → **Save**.
6. Espera 1-2 minutos. La URL final será:
   `https://<tu-usuario>.github.io/yuna-dashboard/`
7. Si te da 404 al principio: **Actions** (pestaña del repo) → comprueba que el
   workflow de Pages ha terminado en verde. Si no arranca solo, en **Settings → Pages**
   dale a **Source** de nuevo y guarda otra vez.

## Cómo funcionan los datos

Todo se guarda con `localStorage` bajo la clave `yuna-dashboard-state-v2`, **en tu
navegador, en tu dispositivo** — no se sube a ningún sitio, ni siquiera a GitHub.
Eso significa:

- Si entras desde el móvil y desde el portátil, son dos "guardados" distintos.
- Si borras el caché/datos del navegador, se pierde — por eso el encabezado
  tiene ahora dos botones: **↓ backup** (descarga un `.json` con todo tu estado)
  y **↑ cargar** (restaura ese `.json` en cualquier dispositivo). Úsalo antes de
  borrar caché o cuando quieras pasar tu progreso de un dispositivo a otro.
- El portfolio empieza vacío a propósito: rellénalo tú una vez que el dashboard
  esté ya en tu navegador, nunca en el código fuente que subes al repo.

## Actualizar el dashboard más adelante

Cada vez que quieras un cambio (nuevo módulo, otro color, otra sección),
pide el archivo `index.html` actualizado, sustitúyelo en el repo (mismo nombre,
misma carpeta) y haz commit. GitHub Pages se actualiza solo en 1-2 minutos.
