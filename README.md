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

## Sincronizar entre dispositivos (opcional)

Por defecto tus datos viven solo en el navegador donde los usas. Si quieres que
el móvil y el portátil vean lo mismo, hay que darle al dashboard un sitio en la
nube donde guardar una copia. Usamos **Firebase Realtime Database** (de Google),
que tiene capa gratuita de sobra para esto y no requiere backend propio.

1. Ve a [console.firebase.google.com](https://console.firebase.google.com) →
   **Crear proyecto** (dale el nombre que quieras, ej. `yuna-dashboard`).
   No hace falta activar Analytics.
2. Dentro del proyecto: **Build → Realtime Database → Crear base de datos**.
   Elige la región más cercana (ej. `europe-west1`) → empieza en
   **modo de prueba** (test mode). Esto deja lectura/escritura abierta durante
   30 días; para que no caduque, ve luego a la pestaña **Reglas** y pon:
   ```json
   { "rules": { ".read": true, ".write": true } }
   ```
   (Es una regla abierta a propósito para que el dashboard funcione sin login.
   Tus datos solo son alcanzables por quien conozca la URL exacta + tu código
   de sincronización, que tú eliges y no se sube al repo.)
3. Copia la **URL de la base de datos** (algo como
   `https://yuna-dashboard-default-rtdb.europe-west1.firebasedatabase.app`).
4. En el dashboard, botón **⇄ sync** del encabezado → pega esa URL y elige un
   código de sincronización (lo que quieras, ej. `yuna-2026`) → **Conectar**.
5. Repite el paso 4 en cada dispositivo, con la misma URL y el mismo código.
   A partir de ahí, cada cambio se sube solo, y al abrir el dashboard en otro
   dispositivo se trae automáticamente lo último.

La configuración de sync (URL + código) se guarda solo en ese navegador —
no forma parte del backup JSON ni se sube al repo si tocas el código.



Cada vez que quieras un cambio (nuevo módulo, otro color, otra sección),
pide el archivo `index.html` actualizado, sustitúyelo en el repo (mismo nombre,
misma carpeta) y haz commit. GitHub Pages se actualiza solo en 1-2 minutos.
